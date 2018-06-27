---
title: '使用批次移轉至 Office 365 和 Exchange Online 移轉舊版公用資料夾: Exchange Online Help'
TOCTitle: 使用批次移轉至 Office 365 和 Exchange Online 移轉舊版公用資料夾
ms:assetid: e8ab9309-7d12-4f02-bfc4-14e61a373958
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn874017(v=EXCHG.150)
ms:contentKeyID: 63806349
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用批次移轉至 Office 365 和 Exchange Online 移轉舊版公用資料夾

 

_**適用版本：**Exchange Online, Exchange Server, Exchange Server 2013_

_**上次修改主題的時間：**2018-03-26_

**摘要：** 將 Exchange 2007 和 Exchange 2010 公用資料夾移至 Office 365 使用這些程序。

本主題說明如何將您在轉換或分段遷移的公用資料夾從更新彙總套件 8 以Exchange Server 2010 Service Pack 3 (SP3) 或 Exchange 2007 SP3 的更新彙總套件 15 移轉至 Office 365 或 Exchange Online。

本主題 Exchange 2010 SP3 RU8 和 Exchange 2007 SP3 RU15 伺服器統稱為*舊版 Exchange 伺服器*。此外，本主題中的步驟適用於 Exchange Online 與 Office 365。條款可能會使用本主題中的交替。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>本文所述的批次移轉方法是將舊版公用資料夾遷移至 Office 365 和 Exchange Online 僅支援的方法。舊序列移轉方法將公用資料夾已正在過時且不再支援 microsoft。</td>
</tr>
</tbody>
</table>


我們建議您不要使用 Outlook 的 PST 匯出功能將公用資料夾遷移至 Office 365 或 Exchange Online。Office 365 和 Exchange online 的公用資料夾信箱成長管理使用分割公用資料夾信箱超過時自動分割功能大小配額。當您使用 PST 匯出遷移公用資料夾與您可能必須等待最多兩週從主要信箱移動資料的自動分割為自動分割無法處理突發公用資料夾信箱的成長。建議您在本文件中使用的指令程式為基礎的指示，將公用資料夾移轉至 Office 365 和 Exchange Online。不過，如果您選取要將公用資料夾使用 PST 匯出遷移，請參閱\] 區段中遷移公用資料夾遷移至 Office 365 使用 Outlook PST 匯出本主題稍後的。

您將會執行使用**\*-MigrationBatch**指令程式和下列 PowerShell 指令碼的移轉：

  - `Export-PublicFolderStatistics.ps1`   此指令碼會建立資料夾名稱至資料夾大小的對應檔案。您將在舊版 Exchange 伺服器上執行此指令碼。

  - `Export-PublicFolderStatistics.psd1`   此支援檔案由 `Export-PublicFolderStatistics.ps1` 指令碼使用，應下載到相同位置。

  - `PublicFolderToMailboxMapGenerator.ps1`   此指令碼會使用 `Export-PublicFolderStatistics.ps1` 指令碼的輸出，建立公用資料夾至信箱的對應檔案。您將在舊版 Exchange 伺服器上執行此指令碼。

  - `PublicFolderToMailboxMapGenerator.strings.psd1`   此支援檔案由 `PublicFolderToMailboxMapGenerator.ps1` 指令碼使用，應下載到相同位置。

  - `Create-PublicFolderMailboxesForMigration.ps1` 此指令碼會建立目標公用資料夾信箱移轉。此外，此指令碼來計算處理估計的使用者負載，根據 \[使用者登入每個公用資料夾信箱中[公用資料夾的限制](limits-for-public-folders-exchange-2013-help.md)建議數的準則所需的信箱數目。

  - `Create-PublicFolderMailboxesForMigration.strings.psd1` 此支援檔案由建立 PublicFolderMailboxesForMigration.ps1 指令碼及應下載到相同位置。

  - `Sync-MailPublicFolders.ps1`  此指令碼進行同步處理本機 Exchange 部署和 Office 365 之間的郵件功能的公用資料夾物件。您將在舊版 Exchange 伺服器上執行此指令碼。

  - `SyncMailPublicFolders.strings.psd1`  這是由`Sync-MailPublicFolders.ps1`指令碼的支援檔案，應複製到與前述指令碼相同的位置。

步驟 1： 下載移轉指令碼提供關於到哪裡下載這些指令碼的詳細資訊。請確定所有的指令碼會下載到相同位置。

如需與公用資料夾相關的其他管理工作，請參閱 [公用資料夾程序](public-folder-procedures-exchange-2013-help.md)。

## 支援哪些 Exchange 版本將公用資料夾遷移至 Office 365 和 Exchange Online？

Exchange 支援從下列舊版 Exchange Server 將您的公用資料夾移至 Office 365 和 Exchange Online：

  - Exchange 2010 SP3 RU8 或更新版本

  - Exchange 2007 SP3 RU15 或更新版本

如果您需要將您的公用資料夾移至 Exchange Online，但您的內部伺服器未執行 Exchange 2010 或 Exchange 2007 的最小支援版本，我們強烈建議您升級您的內部伺服器並使用批次移轉，這是僅支援公用資料夾移轉方法。

您無法直接從 Exchange 2003 移轉公用資料夾。如果您正在執行 Exchange 2003 組織中，您必須移動所有的公用資料夾資料庫和複本為 Exchange 2010 SP3 RU8 或更新版本或 Exchange 2007 SP3 RU10 或更新版本。沒有公用資料夾複本可保留在 Exchange 2003。此外，目的地 Exchange 2013 公用資料夾的郵件無法透過 Exchange 2003 伺服器。

## 開始之前有哪些須知？

  - Exchange 2010 伺服器必須執行 Exchange 2010 SP3 RU8 或更新版本。

  - Exchange 2007 伺服器必須執行 Exchange 2007 SP3 RU15 或更新版本。

  - 在 Office 365 和 Exchange Online，您必須是 「 組織管理角色群組的成員。此角色群組是不同 Office 365 或 Exchange Online 訂閱時指派給您的權限。如需如何啟用 「 組織管理角色群組的詳細資訊，請參閱[管理角色群組](manage-role-groups-exchange-2013-help.md)。

  - 在 Exchange 2010，您需要為組織管理或伺服器管理 RBAC 角色群組的成員。如需詳細資訊，請參閱[新增成員至角色群組](https://go.microsoft.com/fwlink/?linkid=299212)。

  - 在 Exchange 2007 中，您需要 Exchange 組織系統管理員角色或 Exchange Server 系統管理員角色指派。此外，您需要指派公用資料夾系統管理員角色和目標伺服器的本機管理員群組。如需詳細資訊，請參閱 ＜[如何新增使用者或系統管理員角色群組](https://go.microsoft.com/fwlink/p/?linkid=81779)。

  - 在 Exchange 2007 伺服器上，升級為 [Windows PowerShell 2.0 和 WinRM 2.0 for Windows Server 2008 x64 Edition](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=968930)。

  - 在遷移之前，如果組織中有任何公用資料夾大於 2 GB，建議您刪除該資料夾的一些內容，或將其分割為多個公用資料夾。如果這些方式都不可行，建議您不要將公用資料夾移至 Office 365 和 Exchange Online。

  - 在 Office 365 和 Exchange Online，您可以建立 1000 個公用資料夾信箱的最大值。

  - 將公用資料夾移轉之前，建議您先將所有使用者信箱都移至 Office 365 和 Exchange Online。如需詳細資訊，請參閱 ＜[移轉至 Office 365 的多個電子郵件帳戶的方式](https://go.microsoft.com/fwlink/p/?linkid=524030)。

  - Outlook 無所不在 」 必須能夠使用舊版 Exchange 伺服器上。如需 Exchange 2010 伺服器上啟用 Outlook 無所不在 」 的詳細資訊，請參閱 ＜[啟用 Outlook 無所不在](https://go.microsoft.com/fwlink/p/?linkid=187249)。如需 Exchange 2007 伺服器上啟用 Outlook 無所不在 」 的詳細資訊，請參閱 ＜[如何啟用 Outlook 無所不在](https://go.microsoft.com/fwlink/p/?linkid=167210)。

  - 您無法使用 Exchange 系統管理中心 (EAC) 或 Exchange 管理主控台 (EMC) 來執行此程序。在舊版的 Exchange 伺服器，您需要使用Exchange 管理命令介面。Exchange Online 中，您需要使用 Exchange Online PowerShell。如需詳細資訊，請參閱[使用遠端 PowerShell 連線到 Exchange Online](https://technet.microsoft.com/zh-tw/library/jj984289\(v=exchg.150\))。

  - 開始之前，建議您閱讀本主題全文，因為部分步驟需要停機。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 該怎麼做？

## 步驟 1：下載移轉指令碼

1.  從[公用資料夾移轉指令碼](https://go.microsoft.com/fwlink/?linkid=299838)下載所有指令碼和支援的檔案。

2.  將指令碼儲存至將要執行 PowerShell 的本機電腦。例如，C:\\PFScripts。請確定所有的指令碼儲存在相同的位置。

3.  從[擁有郵件功能的公用資料夾-目錄同步處理指令碼](https://go.microsoft.com/fwlink/p/?linkid=532376)下載下列檔案：
    
    1.  `Sync-MailPublicFolders.ps1`
    
    2.  `SyncMailPublicFolders.strings.psd1`

4.  將指令碼儲存至與步驟 2 相同的位置。例如，C:\\PFScripts。

## 步驟 2：準備移轉

先執行下列必要步驟，再開始移轉。

**一般的必要步驟**

  - 請確定任何孤立的公用資料夾郵件物件中沒有 Active Directory、 Active Directory 中沒有對應的 Exchange 物件的意義物件。

  - 確認 SMTP 電子郵件地址設定公用資料夾的 Active Directory 相符項目中的 SMTP 電子郵件地址 Exchange 物件上呼叫。

  - 請務必在 Active Directory，以避免其中兩個或多個 Active Directory 物件會指向相同擁有郵件功能的公用資料夾之情況中有無任何重複的公用資料夾物件。

**舊版 Exchange 伺服器上的必要步驟**

1.  在舊版 Exchange 伺服器上，確定在網際網路上所有 DNS 快取都更新成指向組織現在所在的 Office 365 或 Exchange Online DNS 之前，連到將出現在 Office 365 或 Exchange Online 上具有郵件功能的公用資料夾的路由仍可繼續運作。若要執行此動作，請執行下列命令來設定知名的公認網域，以適當地將電子郵件路由傳送至 Office 365 或 Exchange Online 網域。
    
        New-AcceptedDomain -Name "PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99" -DomainName contoso.onmicrosoft.com -DomainType InternalRelay 

2.  如果公用資料夾的名稱包含反斜線 (**\\**)，移轉時會將公用資料夾建立在公用資料夾的上層資料夾中。移轉之前，建議您將所有名稱含有反斜線的公用資料夾重新命名。
    
    1.  在 Exchange 2010 中，想要找到名稱包含反斜線的公用資料夾，可執行下列命令：
        
            Get-PublicFolderStatistics -ResultSize Unlimited | Where {($_.Name -like "*\*") -or ($_.Name -like "*/*") } | Format-List Name, Identity
    
    2.  在 Exchange 2007 中，想要找到名稱包含反斜線的公用資料夾，可執行下列命令：
        
            Get-PublicFolderDatabase | ForEach {Get-PublicFolderStatistics -Server $_.Server | Where {$_.Name -like "*\*"}}
    
    3.  如果傳回任何公用資料夾，可以執行下列命令將其重新命名：
        
            Set-PublicFolder -Identity <public folder identity> -Name <new public folder name>

3.  請確定沒有任何先前移轉成功的記錄。如果有，您必須將該值設定為 `$false`。如果此值設定為 `$true`，則遷移要求將會失敗。
    
    1.  以下範例會檢查公用資料夾移轉狀態。
        
            Get-OrganizationConfig | Format-List PublicFoldersLockedforMigration, PublicFolderMigrationComplete
    
    2.  如果 *PublicFoldersLockedforMigration* 或 *PublicFolderMigrationComplete* 屬性的狀態為 `$true`，則執行下列命令將值設定為 `$false`。
        
            Set-OrganizationConfig -PublicFoldersLockedforMigration:$false -PublicFolderMigrationComplete:$false
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb125224.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>重設這些屬性之後, 必須等待 Exchange 偵測新的設定。這可能需要兩個小時才能完成。</td>
    </tr>
    </tbody>
    </table>


4.  為了驗證移轉的結尾，我們建議您先執行下列Exchange 管理命令介面命令在舊版 Exchange 伺服器所採取的目前的公用資料夾部署的快照。
    
    1.  執行下列命令以擷取原始來源資料夾結構的快照。
        
            Get-PublicFolder -Recurse | Export-CliXML C:\PFMigration\Legacy_PFStructure.xml
    
    2.  執行下列命令以擷取公用資料夾統計資料的快照，例如項目計數、大小、擁有者。
        
            Get-PublicFolderStatistics -ResultSize Unlimited | Export-CliXML C:\PFMigration\Legacy_PFStatistics.xml
    
    3.  執行下列命令以擷取權限的快照。
        
            Get-PublicFolder -Recurse | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML C:\PFMigration\Legacy_PFPerms.xml
    
    儲存來自前述命令的資訊，以便在移轉結束時進行比較。

5.  如果您使用 Microsoft Azure Active Directory 連線 （Azure AD 連線） 與 Azure Active Directory 同步處理內部部署目錄，您需要執行下列動作 （如果您不使用 Azure AD 連線，您可以略過此步驟）：
    
    1.  內部部署電腦上，開啟 Microsoft Azure Active Directory 連線，並再選取 \[**設定\]**。
    
    2.  在**其他工作**\] 畫面上，選取**自訂同步處理選項**\] 然後再按 \[**下一步**。
    
    3.  在**連線至 Azure AD** \] 畫面上，輸入適當的憑證，並再按 \[**下一步**。一旦連線、 保留按一下 \[**下一步**直到您是**選用的功能**螢幕上。
    
    4.  請確定未選取 \[ **Exchange 郵件公用資料夾**。如果未選取，您可以繼續下一步\] 區段中， *Office 365 或 Exchange Online 中的先決條件步驟*。如果選取，按一下來清除\] 核取方塊，並再按 \[**下一步**。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>如果您未看見<strong>Exchange 郵件公用資料夾</strong>是<strong>選用的功能</strong>] 畫面上的選項，您可以結束 Microsoft Azure Active Directory 連線並繼續進行下一步] 區段中， <em>Office 365 或 Exchange Online 中的先決條件步驟</em>。</td>
        </tr>
        </tbody>
        </table>
    
    5.  已清除**Exchange 郵件公用資料夾**選取項目之後，請按一下 \[**下一步**，直到您已**準備好設定**在畫面上，然後按一下 \[**設定**。

如需詳細的語法及參數資訊，請參閱下列主題：

  - [New-AcceptedDomain](https://technet.microsoft.com/zh-tw/library/aa995975\(v=exchg.150\))

  - [Get-PublicFolder](https://technet.microsoft.com/zh-tw/library/aa997615\(v=exchg.150\))

  - [Get-PublicFolderDatabase](https://technet.microsoft.com/zh-tw/library/jj733416\(v=exchg.150\))

  - [Set-PublicFolder](https://technet.microsoft.com/zh-tw/library/aa998596\(v=exchg.150\))

  - [Get-PublicFolderStatistics](https://technet.microsoft.com/zh-tw/library/aa998663\(v=exchg.150\))

  - [Get-PublicFolderClientPermission](https://technet.microsoft.com/zh-tw/library/bb124365\(v=exchg.150\))

  - [Get-organizationconfig](https://go.microsoft.com/fwlink/p/?linkid=183212)

  - [Set-organizationconfig](https://go.microsoft.com/fwlink/p/?linkid=183213)

**Office 365 或 Exchange Online 中的先決條件步驟**

1.  確保沒有任何現有的公用資料夾移轉要求。如果有，請清除其或您自己的移轉要求將會失敗。在所有的情況下，不需要此步驟僅有必要如果您認為管線中可能會有現有的移轉要求。
    
    現有的移轉要求可以是下列其中一種： 批次移轉或序列移轉。若非要求每個類型並移除要求每種類型的命令如下所示。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>然後再移除移轉要求，請務必了解原因有現有的欄位。執行下列命令將會決定何時進行上一個要求並協助您診斷任何可能發生的問題。您可能需要通訊與您組織中其他管理員來判斷為何進行變更。</td>
    </tr>
    </tbody>
    </table>
    
    下列範例會將發現任何現有的序列的移轉要求。
    
        Get-PublicFolderMigrationRequest | Get-PublicFolderMigrationRequestStatistics -IncludeReport | Format-List
    
    下列範例會移除任何現有的公用資料夾序列的移轉要求。
    
        Get-PublicFolderMigrationRequest | Remove-PublicFolderMigrationRequest
    
    下列範例會將發現任何現有的批次移轉要求。
    
        $batch = Get-MigrationBatch | ?{$_.MigrationType.ToString() -eq "PublicFolder"}
    
    下列範例會移除任何現有的公用資料夾批次移轉要求。
    
        $batch | Remove-MigrationBatch -Confirm:$false

2.  確定 Office 365 中沒有公用資料夾或公用資料夾信箱存在。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您看到 Office 365 或 Exchange Online 中的公用資料夾，務必決定為何他們有與組織中誰啟動之前先移除公用資料夾和公用資料夾信箱的公用資料夾階層。</td>
    </tr>
    </tbody>
    </table>
    
    1.  在 Office 365 或 Exchange Online PowerShell 中執行下列命令，查看是否有任何公用資料夾信箱存在。
        
            Get-Mailbox -PublicFolder 
    
    2.  如果命令沒有傳回任何公用資料夾信箱，請繼續進行步驟 3： 產生.csv 檔案。如果此命令會傳回任何公用資料夾信箱，執行下列命令來看是否有任何公用資料夾存在：
        
            Get-PublicFolder
    
    3.  如果您有任何 Office 365 或 Exchange Online 中的公用資料夾，請執行下列 PowerShell 命令加以移除。請確定您已儲存在 Office 365 中的公用資料夾中的任何資訊。當您移除的公用資料夾時將會永久刪除公用資料夾中所包含的所有資訊。
        
            Get-MailPublicFolder | where {$_.EntryId -ne $null}| Disable-MailPublicFolder -Confirm:$false 
            
            
            Get-PublicFolder -GetChildren \ | Remove-PublicFolder -Recurse -Confirm:$false
    
    4.  會移除公用資料夾之後，請執行下列命令來移除所有的公用資料夾信箱。
        
            $hierarchyMailboxGuid = $(Get-OrganizationConfig).RootPublicFolderMailbox.HierarchyMailboxGuid
            
            Get-Mailbox -PublicFolder:$true | Where-Object {$_.ExchangeGuid -ne $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false
            
            Get-Mailbox -PublicFolder:$true | Where-Object {$_.ExchangeGuid -eq $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false

如需詳細的語法及參數資訊，請參閱下列主題：

  - [Get-MigrationBatch](https://technet.microsoft.com/zh-tw/library/jj219164\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequest](https://technet.microsoft.com/zh-tw/library/jj218718\(v=exchg.150\))

  - [Remove-PublicFolderMigrationRequest](https://technet.microsoft.com/zh-tw/library/jj218625\(v=exchg.150\))

  - [Get-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123685\(v=exchg.150\))

  - [Get-PublicFolder](https://technet.microsoft.com/zh-tw/library/aa997615\(v=exchg.150\))

  - [Get-MailPublicFolder](https://technet.microsoft.com/zh-tw/library/bb124772\(v=exchg.150\))

  - [Disable-MailPublicFolder](https://technet.microsoft.com/zh-tw/library/bb123781\(v=exchg.150\))

  - [Remove-PublicFolder](https://technet.microsoft.com/zh-tw/library/bb124894\(v=exchg.150\))

  - [Remove-Mailbox](https://technet.microsoft.com/zh-tw/library/aa995948\(v=exchg.150\))

## 步驟 3：產生 .csv 檔案

1.  在舊版 Exchange 伺服器上執行`Export-PublicFolderStatistics.ps1`指令碼來建立資料夾名稱至資料夾大小的對應檔案。此指令碼必須一律本機系統管理員身分執行。檔案會包含兩個資料行： **FolderName**和**FolderSize**。**FolderSize**欄的值將會顯示以位元組為單位。例如， **\\PublicFolder01,10000**。
    
        .\Export-PublicFolderStatistics.ps1  <Folder to size map path> <FQDN of source server>
    
      - *FQDN of source server* 等於主控公用資料夾階層的信箱伺服器之完整網域名稱。
    
      - *Folder to size map path* 等於您要在網路共用資料夾上儲存 .csv 檔案的檔案名稱和路徑。在本主題稍後的內容中，您將需要使用 Exchange Online PowerShell 存取此檔案。如果您僅指定檔案名稱，檔案將在本機電腦上目前的 PowerShell 位置中產生。
    
      - 如有必要，請從再繼續執行指令碼輸出中移除任何具有郵件功能的系統資料夾。

2.  執行 `PublicFolderToMailboxMapGenerator.ps1` 指令碼以建立公用資料夾至信箱的對應檔案。此檔案用於計算 Exchange Online 中正確的公用資料夾信箱數目。
    
        .\PublicFolderToMailboxMapGenerator.ps1 <Maximum mailbox size in bytes> <Folder to size map path> <Folder to mailbox map path>
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>公用資料夾至信箱的對應檔案不應該超過 1000 列。如果此檔案超過 1000 列，在您的公用資料夾結構必須簡體中文。繼續進行大於 1000 列的檔案不建議使用，並造成遷移錯誤。</td>
    </tr>
    </tbody>
    </table>
    
      - 才可執行指令碼，使用下列 cmdlet 來檢查您的 Exchange Online 租用戶中目前的公用資料夾限制。然後，請注意目前的配額值的公用資料夾。 `Get-OrganizationConfig | fl *quota*`
        
        Exchange Online 中的預設值為 1.7 GB **DefaultPublicFolderIssueWarningQuota**和**DefaultPublicFolderProhibitPostQuota**2 GB。
    
      - *Maximum mailbox size in bytes*等於您想要設定新的公用資料夾信箱的大小上限。Exchange Online 中公用資料夾信箱的大小上限為 100 GB。我們建議您使用 15 GB 的設定，讓每個公用資料夾信箱擁有成長空間。Exchange Online 具有預設公用資料夾 」 就禁止張貼"配額 2 gb。如果您有超過 2 GB 的個別公用資料夾，您可以使用下列選項的任何修正此問題：
        
          - 啟動遷移批次之前，請增加的預設公用資料夾 」 就禁止張貼"配額來執行下列 cmdlet：
            
            `Set-OrganizationConfig -DefaultPublicFolderProhibitPostQuota <size value> -DefaultPublicFolderIssueWarningQuota <size value>`
        
          - 啟動遷移批次之前，請刪除公用資料夾內容的內容大小降至 2 GB 或更低。
        
          - 啟動遷移批次之前，請公用資料夾分割成多個公用資料夾之每個 2 gb 或更低。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>若在公用資料夾超過 30 GB，且如果它不是合適刪除內容或分割成多個公用資料夾，我們建議您不要移動公用資料夾至 Exchange Online。</td>
        </tr>
        </tbody>
        </table>
    
      - *Folder to size map path*等於執行`Export-PublicFolderStatistics.ps1`指令碼時所建立之.csv 檔案的檔案路徑。
    
      - *Folder to mailbox map path*等於您在此步驟中建立資料夾至信箱.csv 檔案的路徑與檔案名稱。如果您指定的檔案名稱，該檔案所產生之本機電腦上目前的 PowerShell 目錄中。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>執行指令碼並產生.csv 檔案之後，不會收集任何新的公用資料夾或更新現有的公用資料夾。</td>
</tr>
</tbody>
</table>


## 步驟 4：在 Exchange Online 中建立公用資料夾信箱

1.  執行下列命令以建立目標公用資料夾信箱。指令碼會建立您先前在步驟 3 中產生的 .csv 檔案中每個信箱的目標信箱，方法是執行 PublicFoldertoMailboxMapGenerator.ps1 指令碼。
    
        .\Create-PublicFolderMailboxesForMigration.ps1 -FolderMappingCsv Mapping.csv -EstimatedNumberOfConcurrentUsers:<estimate>
    
    *Mapping.csv* 是 PublicFoldertoMailboxMapGenerator.ps1 指令碼在步驟 3 建立的檔案。瀏覽公用資料夾階層的使用者同時連線估計數量通常小於組織中使用者的總數。

## 步驟 5：啟動移轉要求

1.  在舊版 Exchange 伺服器上，執行下列命令來同步處理具有郵件功能的公用資料夾從本機 Active Directory 至 Exchange Online。
    
        Sync-MailPublicFolders.ps1 -Credential (Get-Credential) -CsvSummaryFile:sync_summary.csv
    
    `Credential`為您的 Office 365 使用者名稱和密碼。`CsvSummaryFile`是您想要在記錄檔路徑。CSV 格式\]，再同步處理作業錯誤。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>我們建議您先模擬指令碼來採用之前實際執行它，您可以使用<code>-WhatIf</code>參數執行指令碼中執行的動作。</td>
    </tr>
    </tbody>
    </table>


2.  在舊版 Exchange 伺服器上，取得下列在執行遷移要求時會需要的資訊：
    
    1.  尋找屬於「公用資料夾系統管理員」角色成員之使用者帳戶的 `LegacyExchangeDN`。在此程序的步驟 3 中，您將需要使用這位使用者的認證。
        
            Get-Mailbox <PublicFolder_Administrator_Account> | Select-Object LegacyExchangeDN
    
    2.  尋找任何具有公用資料夾資料庫的 Mailbox server `LegacyExchangeDN` 。
        
            Get-ExchangeServer <public folder server> | Select-Object -Expand ExchangeLegacyDN
    
    3.  尋找 Outlook Anywhere 主機名稱的 FQDN。如果您有多個 Outlook Anywhere 執行個體，建議您選取最接近遷移端點的執行個體，或是選取與舊版 Exchange 組織中的公用資料夾複本最接近的執行個體。下列命令會尋找所有 Outlook Anywhere 執行個體：
        
            Get-OutlookAnywhere | Format-Table Identity,ExternalHostName

3.  在 Office 365 PowerShell 中執行下列命令以傳遞給變數，然後將在遷移要求中使用前一個步驟中所傳回的資訊。
    
    1.  傳遞至變數`$Source_Credential`舊版 Exchange 伺服器具有系統管理權限的使用者認證。具有執行 Exchange Online 的移轉要求將會使用此認證來存取舊版 Exchange 伺服器上複製的內容。
        
            $Source_Credential = Get-Credential <source_domain\PublicFolder_Administrator_Account>
    
    2.  使用您在步驟 2a 中找到並將其傳至變數`$Source_RemoteMailboxLegacyDN`舊版 Exchange 伺服器上的遷移使用者`ExchangeLegacyDN` 。
        
            $Source_RemoteMailboxLegacyDN = "<paste the value here>"
    
    3.  使用您在步驟 2b 中找到並將其傳至變數`$Source_RemotePublicFolderServerLegacyDN`之公用資料夾伺服器`ExchangeLegacyDN` 。
        
            $Source_RemotePublicFolderServerLegacyDN = "<paste the value here>"
    
    4.  使用外部主機名稱的 Outlook 無所不在您在步驟 2c 找到並將其傳至變數`$Source_OutlookAnywhereExternalHostName`。
        
            $Source_OutlookAnywhereExternalHostName = "<paste the value here>"

4.  最後，在 Exchange Online PowerShell 中執行下列命令來建立遷移要求。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>在下列Exchange 管理命令介面範例必須符合您的 Outlook 無所不在設定中的驗證方法，否則命令將會失敗。</td>
    </tr>
    </tbody>
    </table>
    
        $PfEndpoint = New-MigrationEndpoint -PublicFolder -Name PublicFolderEndpoint -RPCProxyServer $Source_OutlookAnywhereExternalHostName -Credentials $Source_Credential -SourceMailboxLegacyDN $Source_RemoteMailboxLegacyDN -PublicFolderDatabaseServerLegacyDN $Source_RemotePublicFolderServerLegacyDN -Authentication Basic
        
        [byte[]]$bytes = Get-Content -Encoding Byte <folder_mapping.csv>
        
        New-MigrationBatch -Name PublicFolderMigration -CSVData $bytes -SourceEndpoint $PfEndpoint.Identity -NotificationEmails <email addresses for migration notifications>
    
    \<*folder\_mapping.csv*\> 檔案所在中產生的檔案步驟 3： 產生.csv 檔案。

5.  開始移轉使用下列命令：
    
        Start-MigrationBatch PublicFolderMigration

雖然批次移轉需要Exchange 管理命令介面中使用**New-MigrationBatch**指令程式來建立，進度和完成移轉可以檢視及管理在 EAC 中。因為**New-migrationbatch**指令程式起始每個公用資料夾信箱的信箱遷移要求，您可以檢視信箱移轉\] 頁面上使用這些要求的狀態。您可以取得信箱移轉\] 頁面上，並建立可執行下列動作傳送至您的移轉報告：

1.  登入 Exchange Online 並開啟 EAC。

2.  瀏覽至 \[信箱\] \> \[移轉\]。

3.  選取剛建立的移轉要求和**詳細資料**窗格中 \[**檢視詳細資料**。

如需詳細的語法及參數資訊，請參閱下列主題：

  - [Get-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123685\(v=exchg.150\))

  - [Get-ExchangeServer](https://technet.microsoft.com/zh-tw/library/bb123873\(v=exchg.150\))

  - [Get-OutlookAnywhere](https://technet.microsoft.com/zh-tw/library/bb124263\(v=exchg.150\))

  - [New-PublicFolderMigrationRequest](https://technet.microsoft.com/zh-tw/library/jj218636\(v=exchg.150\))

  - [Get-PublicFolderDatabase](https://technet.microsoft.com/zh-tw/library/jj733416\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequest](https://technet.microsoft.com/zh-tw/library/jj218718\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequestStatistics](https://technet.microsoft.com/zh-tw/library/jj218697\(v=exchg.150\))

## 步驟 6：鎖定舊版 Exchange 伺服器上的公用資料夾以進行最終移轉 (需停機)

移轉程序為止，直到使用者已能夠存取公用資料夾。下一個步驟將使用者登出舊版公用資料夾和鎖定資料夾時移轉完成其最終同步處理。使用者將無法在此程序期間存取公用資料夾。另外，任何寄送郵件功能的公用資料夾的郵件會排入佇列並不會等到公用資料夾移轉完成後傳送。

在執行`PublicFoldersLockedForMigration`命令如下所示之前，請確定所有工作都是**已同步**狀態。您可以執行`Get-PublicFolderMailboxMigrationRequest`命令來這麼做。您已驗證的所有工作都會在**已同步**狀態後繼續執行此步驟。

在舊版 Exchange 伺服器上，執行下列命令鎖定舊版公用資料夾以完成移轉。

    Set-OrganizationConfig -PublicFoldersLockedForMigration:$true

如需詳細的語法及參數資訊，請參閱 [Set-OrganizationConfig](https://technet.microsoft.com/zh-tw/library/aa997443\(v=exchg.150\))。

如果組織有多個公用資料夾資料庫，必須等到公用資料夾複寫完成，才能確認所有公用資料夾資料庫已選取 `PublicFoldersLockedForMigration` 標幟，且已集中整個組織中使用者最近對資料夾進行而遭擱置的所有變更。可能會花幾小時的時間。

## 步驟 7：完成公用資料夾移轉 (需要停機)

若要完成公用資料夾移轉，執行下列命令：

    Complete-MigrationBatch PublicFolderMigration

當您完成移轉時，Exchange 會執行舊版 Exchange 伺服器和 Exchange Online 之間的最終同步處理。如果最終同步處理成功，Exchange Online 中的公用資料夾會先解除鎖定並遷移批次的狀態會變更為 \[**已完成**。常見的遷移批次所從**已同步**其狀態變更前的幾小時才需**完成**，最終同步處理會開始在其中點。

如果您已設定您的內部部署 Exchange 伺服器和 Office 365 之間的混合部署，您需要執行下列命令在 Exchange Online PowerShell 完成移轉後：

    Set-OrganizationConfig -RemotePublicFolderMailboxes $Null -PublicFoldersEnabled Local

## 步驟 8：測試並解除鎖定公用資料夾移轉

完成公用資料夾移轉後，應該執行下列測試以確定移轉成功。這可讓您先測試遷移後的公用資料夾階層，再切換為使用 Office 365 或 Exchange Online 公用資料夾。

1.  在 Office 365 或 Exchange Online PowerShell 中指派一些測試信箱，以使用新遷移的公用資料夾信箱作為預設公用資料夾信箱。
    
        Set-Mailbox -Identity <Test User> -DefaultPublicFolderMailbox <Public Folder Mailbox Identity>

2.  以上一個步驟的測試使用者身分登入 Outlook 2007 或更新版本，然後執行下列公用資料夾測試：
    
      - 檢視階層。
    
      - 檢查權限。
    
      - 建立與刪除公用資料夾。
    
      - 張貼內容至公用資料夾以及刪除公用資料夾的內容。

3.  如果您執行發生任何問題，請參閱本主題稍後的回復移轉。如果公用資料夾內容和階層是可接受且正常運作，繼續下一個步驟。

4.  在舊版 Exchange 伺服器上，執行下列命令列以指出公用資料夾移轉完成：
    
        Set-OrganizationConfig -PublicFolderMigrationComplete:$true

5.  移轉已完成之後，執行下列命令在 Exchange Online PowerShell 確認上**Set-OrganizationConfig***PublicFoldersEnabled*參數會設為`Local`：
    
        Set-OrganizationConfig -PublicFoldersEnabled Local

如需詳細的語法及參數資訊，請參閱下列主題：

[Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\))

[Get-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123685\(v=exchg.150\))

[Set-OrganizationConfig](https://technet.microsoft.com/zh-tw/library/aa997443\(v=exchg.150\))

## 如何才能了解運作是否正常？

在步驟 2： 準備移轉、 所指示開始移轉之前所採取的公用資料夾結構、 統計資料，以及權限的快照。下列步驟將協助您確認您的公用資料夾移轉成功完成移轉後採取相同的快照集。您可以再比較若要驗證成功這兩個檔案中的資料。

1.  在 Exchange Online PowerShell 中執行下列命令，以擷取新資料夾結構的快照。
    
        Get-PublicFolder -Recurse | Export-CliXML C:\PFMigration\Cloud_PFStructure.xml

2.  在 Exchange Online PowerShell 中執行下列命令，以擷取公用資料夾統計資料的快照，例如項目計數、大小以及擁有者。
    
        Get-PublicFolderStatistics -ResultSize Unlimited | Export-CliXML C:\PFMigration\Cloud_PFStatistics.xml

3.  在 Exchange Online PowerShell 中執行下列命令，以擷取權限的快照。
    
        Get-PublicFolder -Recurse | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML  C:\PFMigration\Cloud_PFPerms.xml

## 移除舊版 Exchange 伺服器上的公用資料夾資料庫

完成遷移，且已驗證 Exchange Online 公用資料夾運作如預期之後，您應移除舊版 Exchange 伺服器上的公用資料夾資料庫。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>由於您的信箱的所有已移轉至 Office 365 公用資料夾移轉之前，強烈建議您透過 Office 365 （分散式的郵件流程） 流量路由，而不是透過內部部署環境的集中式的郵件流程。如果您選擇要保留集中式郵件流程，它可能會導致您公用資料夾的傳遞問題之後您移除了從內部部署組織的公用資料夾信箱資料庫。</td>
</tr>
</tbody>
</table>


  - 如需如何移除 Exchange 2007 伺服器上的公用資料夾資料庫的詳細資訊，請參閱[移除公用資料夾資料庫](https://go.microsoft.com/fwlink/?linkid=123678)。

  - 如需如何移除 Exchange 2010 伺服器上的公用資料夾資料庫的詳細資訊，請參閱[移除公用資料夾資料庫](https://go.microsoft.com/fwlink/?linkid=81409)。

## 回復移轉

如果遷移發生問題，且需要重新啟動舊版 Exchange 公用資料夾，請執行下列步驟。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您回復移轉到舊版的 Exchange 伺服器，您會失去所有電子郵件傳送至擁有郵件功能的公用資料夾或張貼至公用資料夾移轉後的內容。若要儲存此內容，您需要將公用資料夾內容匯出至.pst 檔案並再匯入舊版公用資料夾回復完成時。</td>
</tr>
</tbody>
</table>


1.  在舊版 Exchange 伺服器上，執行下列命令解除鎖定舊版 Exchange 公用資料夾。此程序可能會花幾小時的時間。
    
        Set-OrganizationConfig -PublicFoldersLockedForMigration:$False

2.  在 Exchange Online PowerShell 中執行下列命令，以移除所有的 Exchange Online 公用資料夾。
    
        $hierarchyMailboxGuid = $(Get-OrganizationConfig).RootPublicFolderMailbox.HierarchyMailboxGuid
        
        Get-Mailbox -PublicFolder:$true | Where-Object {$_.ExchangeGuid -ne $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
        
        Get-Mailbox -PublicFolder:$true | Where-Object {$_.ExchangeGuid -eq $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force

3.  在舊版 Exchange 伺服器上，執行下列命令將 `PublicFolderMigrationComplete` 標幟設定為 `$false`。
    
        Set-OrganizationConfig -PublicFolderMigrationComplete:$False

## 使用 Outlook PST 匯出將公用資料夾遷移至 Office 365

如果您的內部部署公用資料夾階層大於 30 GB，我們建議您不要使用 Outlook 的 PST 匯出功能將公用資料夾遷移到 Office 365 或 Exchange Online。Office 365 線上公用資料夾信箱的成長由自動分割功能來管理，此功能會在公用資料夾信箱超出大小配額時將其分割。當您使用 PST 匯出來遷移公用資料夾時，自動分割無法處理公用資料夾信箱的突然成長，您可能必須等候長達兩週，自動分割才能將資料從主要信箱移走。此外，在使用 Outlook PST 將公用資料夾匯出至 Office 365 或 Exchange Online 之前，請考慮下列事項：

  - 公用資料夾權限會在此過程中遺失。請在遷移之前擷取目前的權限，然後在完成遷移後手動將其加回。

  - 如果您使用複雜的權限或有許多資料夾要遷移，我們建議您使用 Cmdlet 方法來進行遷移。

  - 在 PST 匯出遷移期間對來源公用資料夾所做的任何項目與資料夾的變更將會遺失。因此，如果此匯出和匯入程序會花很長時間才能完成，我們建議您使用 Cmdlet 方法。

如果您仍想要使用 PST 檔案遷移公用資料夾，請遵循下列步驟以確保遷移成功。

1.  使用中的指示步驟 1： 下載移轉指令碼下載移轉指令碼。您只需要下載`PublicFolderToMailboxMapGenerator.ps1`檔案。

2.  請遵循的步驟 2步驟 3： 產生.csv 檔案建立公用資料夾至信箱的對應檔案。此檔案用來計算 Exchange Online 中公用資料夾信箱的正確的號碼。

3.  根據對應檔案建立您需要的公用資料夾信箱。如需詳細資訊，請參閱[建立公用資料夾信箱](create-a-public-folder-mailbox-exchange-2013-help.md)。

4.  使用 New-PublicFolder Cmdlet 並使用 *Mailbox* 參數在每個公用資料夾信箱中建立最上層的公用資料夾。

5.  使用 Outlook 匯出及匯入 PST 檔案。

6.  使用 EAC 設定公用資料夾的權限。如需相關資訊，請遵循[設定新的組織中的公用資料夾](set-up-public-folders-in-a-new-organization-exchange-2013-help.md)主題中的[Step 3: Assign permissions to the public folder](set-up-public-folders-in-a-new-organization-exchange-2013-help.md)。

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您已開始 PST 遷移，並遭遇主要信箱已滿的問題，則有兩個選擇可用來復原 PST 遷移：
<ol>
<li><p>等待自動分割將資料從主要信箱移出。這最多可能要花兩個星期的時間。但完全已滿的公用資料夾信箱中，所有公用資料夾在自動分割完成之前將無法收到新的內容。</p></li>
<li><p><a href="create-a-public-folder-mailbox-exchange-2013-help.md">建立公用資料夾信箱</a>，然後使用 <strong>New-PublicFolder</strong> Cmdlet 搭配 <em>Mailbox</em> 參數，在次要公用資料夾信箱中建立剩餘的公用資料夾。本範例會在次要公用資料夾信箱中，建立一個名為 PF201 的新公用資料夾。</p>
<pre><code>New-PublicFolder -Name PF201 -Mailbox SecondaryPFMbx</code></pre></li>
</ol></td>
</tr>
</tbody>
</table>


## 初次使用 Office 365 嗎？


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><img src="images/Bb123521.eac8a413-9498-4220-8544-1e37d1aaea13(EXCHG.150).png" title="LinkedIn Learning 的短圖示" alt="LinkedIn Learning 的短圖示" /> <strong>初次使用 Office 365？</strong><br />
探索 LinkedIn Learning 提供的 <a href="https://support.office.com/zh-tw/article/office-365-admin-and-it-pro-courses-68cc9b95-0bdc-491e-a81f-ee70b3ec63c5">Office 365 admins and IT pros</a> 免費影片課程。</p></td>
</tr>
</tbody>
</table>

