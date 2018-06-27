---
title: '設定 Exchange Online 公用資料夾以進行混合部署: Exchange Online Help'
TOCTitle: 設定 Exchange Online 公用資料夾以進行混合部署
ms:assetid: d979edb3-967b-4431-8beb-0c236bf7f56d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Mt729076(v=EXCHG.150)
ms:contentKeyID: 72768738
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定 Exchange Online 公用資料夾以進行混合部署

 

_<strong>適用版本：</strong>Exchange Server 2013_

_<strong>上次修改主題的時間：</strong>2016-12-15_

**摘要：** 說明啟用內部部署 Exchange 2013 使用者可以存取 Exchange Online 中的公用資料夾。

在混合式部署中，您的使用者可以在 Exchange Online、 內部，或兩者，且您的公用資料夾其在 Exchange 線上\] 或 \[內部部署。有時 online 使用者可能會需要用來存取 Exchange Server 2013 內部部署環境中的公用資料夾。同樣地，Exchange 2013 使用者可能需要存取 Office 365 或 Exchange Online 中的公用資料夾。

本文說明如何讓 Exchange 2013 內部部署環境中的使用者可以存取 Exchange Online/Office 365 的公用資料夾。若要啟用 Exchange Online/Office 365 使用者存取內部部署 Exchange 2013 公用資料夾，請參閱 ＜ [設定混合式部署的 Exchange 2013 公用資料夾](configure-exchange-2013-public-folders-for-a-hybrid-deployment-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ150559.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您有 Exchange 2010 或 Exchange 2007 公用資料夾，請參閱<a href="configure-legacy-on-premises-public-folders-for-a-hybrid-deployment-exchange-2013-help.md">為混合部署設定舊版的內部部署公用資料夾</a>。</td>
</tr>
</tbody>
</table>


## 開始之前有哪些須知？

1.  這些指示假設您已使用混合組態精靈來設定及同步處理您的內部部署與 Exchange Online 環境，且使用者的「自動探索」所使用的 DNS 記錄是參考內部部署端點。如需詳細資訊，請參閱 [混合組態精靈](hybrid-configuration-wizard-exchange-2013-help.md)。

2.  這些指示假設 Outlook 無所不在 」 是已啟用且在內部部署 Exchange 伺服器功能。如需如何啟用 Outlook 無所不在 」 的資訊，請參閱 ＜ [Outlook 無所不在](https://technet.microsoft.com/zh-tw/library/bb123741\(v=exchg.150\))。

3.  實作 Exchange 與 Office 365 的混合式部署的公用資料夾共存可能需要修正匯入程序期間發生衝突。因為指派給郵件已啟用的公用資料夾與其他使用者和群組的 Office 365 及其他屬性發生衝突的非路由傳送的電子郵件地址的可以發生衝突。

4.  若要能夠跨部署來存取公用資料夾，使用者必須將其 Outlook 用戶端升級至 2012 年 11 月或更新的 Outlook 公用更新。
    
    1.  若要下載 November 2012 Outlook 更新 Outlook 2010，請參閱[Microsoft Outlook 2010 (KB2687623) 32 位元版本的更新](https://www.microsoft.com/en-us/download/details.aspx?id=35702)。
    
    2.  下載 November 2012 Outlook 更新 Outlook 2007，查看[Microsoft Office Outlook 2007 (KB2687404) 更新](https://www.microsoft.com/en-us/download/details.aspx?id=35718)。

5.  Outlook 2011 for Mac 和 Outlook for Mac 中的 Office 365 不支援跨部署公用資料夾。使用者必須在相同位置存取其與 Outlook 2011 for Mac 或 Outlook for Mac 的 Office 365 的公用資料夾。此外，信箱已在 Exchange Online 使用者將無法存取內部部署公用資料夾使用 Outlook Web App。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ150559.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Outlook 2016 for Mac 支援跨部署公用資料夾。如果用戶端在組織中的使用 Outlook 2016 for Mac，請務必先安裝年 4 月 2016年更新。否則，這些使用者將無法存取公用共存或混合式拓撲中的資料夾。如需詳細資訊，請參閱<a href="https://technet.microsoft.com/zh-tw/library/mt788631(v=exchg.150)">存取公用資料夾與 Outlook 2016 for Mac</a>。</td>
    </tr>
    </tbody>
    </table>


## 步驟 1： 下載指令碼

1.  下載下列檔案從[擁有郵件功能的公用資料夾-從 EXO 上 prem 指令碼的目錄同步處理](https://go.microsoft.com/fwlink/p/?linkid=797795)。
    
      - `Import-PublicFolderMailboxes.ps1`
    
      - `ImportPublicFolderMailboxes.strings.psd1`
    
      - `Sync-MailPublicFoldersCloudToOnprem.ps1`
    
      - `Sync-MailPublicFoldersCloudToOnprem.strings.psd1`

2.  將檔案儲存至將要執行 PowerShell 的本機電腦。例如，C:\\PFScripts。

## 步驟 2： 設定目錄同步處理

執行指令碼`Sync-MailPublicFoldersCloudToOnprem.ps1`會同步處理具有郵件功能的公用資料夾之間 Exchange Online 和 Exchange 2013 內部部署環境。由於跨內部部署權限不支援在混合部署案例中重新建立雲端中需要特殊權限指派給擁有郵件功能的公用資料夾。如需詳細資訊，請參閱[Exchange Server 2013 混合式部署](exchange-server-hybrid-deployments-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ150559.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>同步處理具有郵件功能的公用資料夾會出現郵件連絡人物件的郵件流程用途並將無法檢視在 Exchange 系統管理中心。 請參閱 ＜ Get MailPublicFolder 命令。 若要重新建立雲端中的 SendAs 權限、 使用 Add Add-recipientpermission 指令。</td>
</tr>
</tbody>
</table>


1.  在 Exchange 2013 伺服器上，執行下列命令來同步處理具有郵件功能的公用資料夾從 Exchange Online/Office 365 到本機內部部署 Active Directory。
    
        Sync-MailPublicFoldersCloudToOnprem.ps1 -Credential (Get-Credential)
    
    其中`Credential`是您的 Office 365 使用者名稱和密碼。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ150559.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>我們建議您執行此指令碼每天同步處理具有郵件功能的公用資料夾。</td>
</tr>
</tbody>
</table>


## 步驟 3： 設定內部部署使用者可以存取 Exchange Online 公用資料夾

此程序的最後一個步驟是設定 Exchange 2013 內部部署組織允許存取 Exchange Online 公用資料夾。

執行指令碼`Import-PublicFolderMailboxes.ps1`將物件匯入公用資料夾信箱從雲端為擁有郵件功能的使用者內部部署環境。指令碼也會以遠端的公用資料夾信箱設定匯入的物件。

1.  在 Exchange 2013 伺服器上，執行以下命令至雲端的公用資料夾信箱物件匯入您的內部部署 Active Directory。
    
        Import-PublicFolderMailboxes.ps1 -Credential (Get-Credential)
    
    其中`Credential`是您的 Office 365 使用者名稱和密碼。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ150559.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>建議您每天此指令碼執行因為它們每當公用資料夾信箱到達其臨界值容量，自動分割成多個新信箱匯入在公用資料夾信箱物件。因此，您一律要確定您已從雲端匯入最新公用資料夾信箱。</td>
    </tr>
    </tbody>
    </table>


2.  啟用 Exchange 2013 內部部署組織來存取 Exchange Online 公用資料夾。
    
        Set-OrganizationConfig -PublicFoldersEnabled Remote

<table>
<thead>
<tr class="header">
<th><img src="images/JJ150559.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您必須等到 ActiveDirectory 同步處理已完成查看所做的變更。此程序可能需要最多 3 小時才能完成。如果您不想等待發生每三個小時週期性同步處理，您可以強制任何時候的目錄同步處理。不要強制進行目錄同步處理的詳細步驟，請參閱<a href="http://technet.microsoft.com/en-us/library/jj151771.aspx">強制進行目錄同步處理</a>。</td>
</tr>
</tbody>
</table>


## 如何知道這是否正常運作？

1.  代表存在於 Exchange Online 的使用者登入 Outlook，並執行下列公用資料夾測試：
    
      - 檢視階層。
    
      - 檢查權限
    
      - 建立與刪除公用資料夾。
    
      - 張貼內容至公用資料夾以及刪除公用資料夾的內容。

