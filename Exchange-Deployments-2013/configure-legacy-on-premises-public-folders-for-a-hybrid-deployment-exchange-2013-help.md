---
title: '為混合部署設定舊版的內部部署公用資料夾: Exchange Online Help'
TOCTitle: 為混合部署設定舊版的內部部署公用資料夾
ms:assetid: bcb0ac98-2949-486b-a8ab-8549c021651b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn249373(v=EXCHG.150)
ms:contentKeyID: 54914965
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 為混合部署設定舊版的內部部署公用資料夾

 


_**適用版本：** Exchange Online, Exchange Server 2010, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：** 2018-05-22_


**摘要：** 使用本文中的步驟，同步處理 Office 365 和 Exchange 2007 或 Exchange 2010 內部部署之間的公用資料夾。

在混合式部署中，您的使用者可能存在於 Exchange Online、內部部署或同時存在於兩者，而您的公用資料夾可能存在於 Exchange Online 或內部部署中。公用資料夾只能存在於單一位置，因此您必須決定要將公用資料夾放在 Exchange Online 還是內部部署中。公用資料夾無法同時存在於這兩個位置。「目錄同步處理」服務會將公用資料夾信箱同步處理至 Exchange Online。但具有郵件功能的公用資料夾無法跨部署進行同步處理。

本主題將說明當您的使用者存在於 Office 365，而 Exchange 2010 SP3 或 Exchange 2007 SP3 RU10 公用資料夾存在於內部部署時，要如何同步處理具有郵件功能的公用資料夾。不過，不是由 MailUser 物件內部部署代表的 Office 365 使用者 (目標公用資料夾階層的本機)，不能存取舊版或 Exchange 2013 內部部署公用資料夾。

> [!NOTE]  
> 本主題中將 Exchange 2010 SP3 和 Exchange 2007 SP3 RU10 伺服器統稱為「舊版 Exchange 伺服器」。


您將使用下列指令碼對具有郵件功能的公用資料夾進行同步處理，而這些指令碼會由內部部署環境中執行的 Windows 工作啟動：

1.  `Sync-MailPublicFolders.ps1`   這個指令碼會將您的本機 Exchange 內部部署中具有郵件功能的公用資料夾物件，與 Office 365 同步處理。指令碼使用本機 Exchange 內部部署的部署作為主檔，判斷需要將什麼變更套用至 O365。指令碼會根據本機內部部署 Exchange 部署中存在的物件，建立、更新或刪除 O365 Active Directory 上具有郵件功能的公用資料夾物件。

2.  `SyncMailPublicFolders.strings.psd1`   這是前述同步處理指令碼會使用的支援檔案，應複製到與前述指令碼相同的位置。

當您完成此程序後，您的內部部署與 Office 365 使用者將可存取相同的內部部署公用資料夾基礎結構。

## Exchange 的版本組合中有哪些支援公用資料夾的使用？

下表說明支援的使用者信箱與公用資料夾的版本與位置組合。「不適用混合」仍是支援的案例，但因為公用資料夾與使用者存在於相同的位置中，所以不會視為混合式部署。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>內部部署 Exchange 2007 或 Exchange 2010 使用者信箱</th>
<th>內部部署 Exchange 2013 使用者信箱</th>
<th>Exchange Online 使用者信箱</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>內部部署 Exchange 2007 或 Exchange 2010 公用資料夾</p></td>
<td><p>不適用混合</p></td>
<td><p>不適用混合</p></td>
<td><p>支援</p></td>
</tr>
<tr class="even">
<td><p>內部部署 Exchange 2013 公用資料夾</p></td>
<td><p>不適用混合</p></td>
<td><p>不適用混合</p></td>
<td><p>支援</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Online 公用資料夾</p></td>
<td><p>不支援</p></td>
<td><p>支援</p></td>
<td><p>不適用混合</p></td>
</tr>
</tbody>
</table>


無法支援使用 Exchange 2003 公用資料夾的混合式設定。如果您的組織中執行 Exchange 2003，您必須將所有的公用資料夾資料庫與複本移至 Exchange 2007 SP3 RU10 或更新版本。Exchange 2003 上無法保留任何公用資料庫複本。

> [!NOTE]  
> Outlook 2016 不支援存取 Exchange 2007 舊版公用資料夾。如果您有 Outlook 2016 的使用者，您必須將公用資料夾移至較新版本的 Exchange。有關 Outlook 2016 和 Office 2016 與 Exchange 2007 和較舊版本的相容性詳細資訊，請參閱<a href="https://go.microsoft.com/fwlink/p/?linkid=849053">此文章</a>。


## 步驟 1：開始之前有哪些須知？

1.  這些指示假設您已使用混合組態精靈來設定及同步處理您的內部部署與 Exchange Online 環境，且使用者的「自動探索」所使用的 DNS 記錄是參考內部部署端點。如需詳細資訊，請參閱 [混合組態精靈](hybrid-configuration-wizard-exchange-2013-help.md)。

2.  這些指示假設在內部部署舊版 Exchange 伺服器上，Outlook 無所不在已啟用並可運作。如需如何啟用 Outlook 無所不在的相關資訊，請參閱 [Outlook 無所不在](https://technet.microsoft.com/zh-tw/library/bb123741\(v=exchg.150\))。

3.  針對 Exchange 與 Office 365 的混合式部署實作舊版公用資料夾共存時，您可能需要解決匯入過程中發生的衝突。衝突的原因可能是指派給擁有郵件功能之公用資料夾的非路由電子郵件地址與 Office 365 中的其他使用者和群組以及其他屬性發生衝突。

4.  這些指示假設您的 Exchange Online 組織已升級至支援公用資料夾的版本。

5.  在 Exchange Online 中，您必須是「組織管理」角色群組的成員。此角色群組不同於您在訂閱 Exchange Online 時被指派的權限。如需關於如何啟用「組織管理」角色群組的詳細資訊，請參閱[管理角色群組](https://technet.microsoft.com/zh-tw/library/jj657480\(v=exchg.150\))。

6.  在 Exchange 2010 中，您必須是「組織管理」或「伺服器管理」RBAC 角色群組的成員。如需詳細資訊，請參閱＜[新增成員至角色群組](https://go.microsoft.com/fwlink/?linkid=299212)＞。

7.  在 Exchange 2007，您必須獲指派為「Exchange 組織系統管理員」角色或「Exchange Server 系統管理員」角色。除此之外，您必須獲指派為「公用資料夾系統管理員」角色和目標伺服器的本機 Administrators 群組。如需詳細資訊，請參閱＜[如何新增使用者或群組至系統管理員角色](https://go.microsoft.com/fwlink/p/?linkid=81779)＞。

8.  如果您在 Windows Server 2008 x64 上執行 Exchange Server 2007，您必須升級至 [Windows PowerShell 2.0 和 WinRM 2.0 for Windows Server 2008 x64 Edition](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=968930)。如果您在 Windows Server 2003 x64 上執行 Exchange Server 2007，您必須升級至 Windows PowerShell 2.0。如需詳細資訊，請參閱 [Windows Server 2003 x64 版本的更新](https://www.microsoft.com/en-us/download/details.aspx?id=10512)。

9.  若要能夠跨部署來存取公用資料夾，使用者必須將其 Outlook 用戶端升級至 2012 年 11 月或更新的 Outlook 公用更新。
    
    1.  若要下載 2012 年 11 月針對 Outlook 2010 發佈的 Outlook 更新，請參閱 [Microsoft Outlook 2010 (KB2687623) 32 位元版本的更新](https://www.microsoft.com/en-us/download/details.aspx?id=35702)。
    
    2.  若要下載 2012 年 11 月針對 Outlook 2007 發佈的 Outlook 更新，請參閱 [Microsoft Office Outlook 2007 (KB2687404) 的更新](https://www.microsoft.com/en-us/download/details.aspx?id=35718)。

10. 跨部門部署的舊版公用資料夾不支援 Outlook 2016 for Mac (和較舊版本) 和 Outlook for Mac for Office 365。使用者必須與公用資料夾位於相同位置，才能使用 Outlook for Mac 或 Outlook for Mac for Office 365 存取公用資料夾。此外，信箱位於 Exchange Online 的使用者無法使用 Outlook Web App 存取內部部署的公用資料夾。

11. 在您依照本文的指示設定混合部署的內部部署公用資料夾後，您組織的外部使用者將無法傳送訊息至內部部署的公用資料夾，除非您採取額外步驟。您可以將公用資料夾公認的網域設定為內部轉送 (請參閱 [管理 Exchange Online 中公認的網域](https://technet.microsoft.com/zh-tw/library/jj945194\(v=exchg.150\)) 取得詳細資訊)，或者您可以如 [使用目錄架構邊緣封鎖以拒絕傳送至無效收件者的郵件](https://technet.microsoft.com/zh-tw/library/dn600322\(v=exchg.150\)) 所述，停用目錄架構邊緣封鎖 (DBEB)。

## 步驟 2：使遠端公用資料夾可被探索到

1.  如果您的公用資料夾位於 Exchange 2010 或更新版本的伺服器上，您就必須在所有具有公用資料夾資料庫的 Mailbox Server 上安裝 Client Access server role。如此，Microsoft Exchange RpcClientAccess 服務即得以執行，進而讓所有用戶端都能存取公用資料夾。Exchange 2007 公用資料夾伺服器不需要用戶端存取角色，無須執行此步驟。如需詳細資訊，請參閱[安裝 Exchange Server 2010](https://technet.microsoft.com/zh-tw/library/bb124778\(v=exchg.141\).aspx)。對於 Exchange 2007 公用資料夾，無須執行此步驟。
    
       > [!NOTE]  
       > 此伺服器無須成為用戶端存取負載平衡的一部分。如需詳細資訊，請參閱＜<a href="https://technet.microsoft.com/zh-tw/library/ff625247(v=exchg.141).aspx">了解 Exchange 2010 中的負載平衡</a>＞。


2.  在每個公用資料夾伺服器上建立空的信箱資料庫。
    
    在 Exchange 2010 中執行下列命令。此命令會將信箱資料庫排除在信箱佈建負載平衡器以外。這樣可以防止自動將新的信箱新增至此資料庫中。
    
        New-MailboxDatabase -Server <PFServerName_with_CASRole> -Name <NewMDBforPFs> -IsExcludedFromProvisioning $true
    
    在 Exchange 2007 中執行下列命令：
    
        New-MailboxDatabase -StorageGroup "<PFServerName>\StorageGroup>" -Name <NewMDBforPFs>
    
    > [!NOTE]  
    > 我們建議您增加到此資料庫的唯一信箱就是您將在步驟 3 中建立的 Proxy 信箱。不得在此信箱資料庫上建立其他信箱。


3.  在新的信箱資料庫中建立 Proxy 信箱，然後在通訊錄中隱藏該信箱。「自動探索」會傳回此信箱的 SMTP 作為 *DefaultPublicFolderMailbox* SMTP，因此只要解析此 SMTP，用戶端即可連到舊版 Exchange 伺服器來存取公用資料夾。
    
        New-Mailbox -Name <PFMailbox1> -Database <NewMDBforPFs>
    
        Set-Mailbox -Identity <PFMailbox1> -HiddenFromAddressListsEnabled $true

4.  在 Exchange 2010 中，讓「自動探索」傳回 Proxy 公用資料夾信箱。對於 Exchange 2007，無須執行此步驟。
    
        Set-MailboxDatabase <NewMDBforPFs> -RPCClientAccessServer <PFServerName_with_CASRole>

5.  對組織中的每部公用資料夾伺服器重複前述步驟。

## 步驟 3：下載指令碼

1.  從[具有郵件功能的公用資料夾 - 目錄同步指令碼](https://www.microsoft.com/en-us/download/details.aspx?id=46381)下載下列檔案：
    
      - `Sync-MailPublicFolders.ps1`
    
      - `SyncMailPublicFolders.strings.psd1`

2.  將檔案儲存至將要執行 PowerShell 的本機電腦。例如，C:\\PFScripts。

## 步驟 4：設定目錄同步處理

「目錄同步處理」服務不會同步處理具有郵件功能的公用資料夾。執行下列指令碼，將會跨部署來同步處理具有郵件功能的公用資料夾。需要在雲端裡重新建立指派給具有郵件功能公用資料夾的特殊權限，因為混合部署案例不支援跨部署權限。如需詳細資訊，請參閱 [Exchange Server 2013 混合式部署](exchange-server-hybrid-deployments-exchange-2013-help.md)。

> [!NOTE]  
> 為了郵件流程用途，已同步的具有郵件功能公用資料夾會顯示為郵件連絡人物件，而不可在 Exchange 系統管理中心 中檢視。請參閱 Get-MailPublicFolder 命令。若要在雲端中重新建立 SendAs 權限，請使用 Add-RecipientPermission 命令。

1.  在舊版 Exchange 伺服器上，執行下列命令將本機內部部署 Active Directory 中具有郵件功能的公用資料夾與 O365 同步處理。
    
        Sync-MailPublicFolders.ps1 -Credential (Get-Credential) -CsvSummaryFile:sync_summary.csv
    
    `Credential` 是您的 Office 365 使用者名稱和密碼，而 `CsvSummaryFile` 是您想要記錄同步處理作業和錯誤的路徑，檔案為 CSV 格式。

> [!NOTE]  
> 執行指令碼之前，我們建議您先模擬指令碼在您的環境中會執行的動作，方法是使用 <code>-WhatIf</code> 參數依照上述來執行此指令碼。<br />
我們也建議您每天執行此指令碼，以同步處理具有郵件功能的公用資料夾。

## 步驟 5：設定讓 Exchange Online 使用者存取內部部署公用資料夾

此程序的最後一個步驟是設定 Exchange Online 組織，並允許存取舊版內部部署公用資料夾。

讓 Exchange Online 組織能夠存取內部部署公用資料夾。您將會指向先前在步驟 2：使遠端公用資料夾可被探索到中建立的所有 Proxy 公用資料夾信箱。

在 **Windows PowerShell** 中執行下列命令：

    Set-OrganizationConfig -PublicFoldersEnabled Remote -RemotePublicFolderMailboxes PFMailbox1,PFMailbox2,PFMailbox3

您必須等到 ActiveDirectory 同步處理完成後，才會看見變更。這個過程最多需要 3 小時才能完成。如果您不想等待每三小時執行的週期性同步處理，您可以隨時強制執行目錄同步處理。如需強制執行目錄同步處理的詳細步驟，請參閱＜[強制執行目錄同步處理](http://technet.microsoft.com/zh-tw/library/jj151771.aspx)＞。Office 365 隨機選取此命令中提供的其中一個公用資料夾信箱。

> [!IMPORTANT]  
> 沒有由 MailUser 物件內部部署代表的 Office 365 使用者 (目標公用資料夾階層的本機)，不能存取舊版或 Exchange 2013 內部部署公用資料夾。請參閱知識庫文章＜<a href="https://go.microsoft.com/fwlink/p/?linkid=699451">Exchange Online 使用者無法存取舊版內部部署公用資料夾</a>＞，查看解決方案。


## 如何知道這是否正常運作？

1.  代表存在於 Exchange Online 的使用者登入 Outlook，並執行下列公用資料夾測試：
    
      - 檢視階層。
    
      - 檢查權限
    
      - 建立與刪除公用資料夾。
    
      - 張貼內容至公用資料夾以及刪除公用資料夾的內容。

## 初次使用 Office 365 嗎？


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><img src="images/Dn249373.eac8a413-9498-4220-8544-1e37d1aaea13(EXCHG.150).png" title="LinkedIn Learning 的短圖示" alt="LinkedIn Learning 的短圖示" /> <strong>初次使用 Office 365？</strong><br />
探索 LinkedIn Learning 提供的 <a href="https://support.office.com/zh-tw/article/office-365-admin-and-it-pro-courses-68cc9b95-0bdc-491e-a81f-ee70b3ec63c5">Office 365 admins and IT pros</a> 免費影片課程。</p></td>
</tr>
</tbody>
</table>

