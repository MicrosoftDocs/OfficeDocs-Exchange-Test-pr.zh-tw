---
title: '使用批次移轉公用資料夾從舊版移轉至 Exchange 2013: Exchange 2013 Help'
TOCTitle: 使用批次移轉公用資料夾從舊版移轉至 Exchange 2013
ms:assetid: da808e27-d2b7-4fbd-915c-a600751f526c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn912663(v=EXCHG.150)
ms:contentKeyID: 64131352
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用批次移轉公用資料夾從舊版移轉至 Exchange 2013

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2018-03-26_

**摘要：** 本文會告訴您如何將公用資料夾從 Exchange 2007 或 Exchange 2010 移至 Exchange 2013。

本文說明如何將公用資料夾移轉從 Exchange Server 2010 SP3 RU8 或 Exchange 2007 SP3 RU15 Microsoft Exchange Server 2013 CU7 或稍後將在同一個樹系。

我們將 Exchange 2010 SP3 RU8 和 Exchange 2007 SP3 RU15 伺服器參照為*舊版 Exchange 伺服器*。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>本文所述的批次移轉方法是將舊版公用資料夾遷移至 Exchange 2013 僅支援的方法。舊序列移轉方法將公用資料夾已正在過時且不再支援 microsoft。</td>
</tr>
</tbody>
</table>


您將使用**\*MigrationBatch**指令程式和**\*PublicFolderMigrationRequest** cmdlet 疑難排解執行移轉。此外，您將會使用下列 PowerShell 指令碼：

  - `Export-PublicFolderStatistics.ps1` 此指令碼會建立資料夾名稱至資料夾大小的對應檔案。

  - ` Export-PublicFolderStatistics.psd1` 此支援檔案由 Export-publicfolderstatistics.ps1 指令碼及應下載到相同位置。

  - `PublicFolderToMailboxMapGenerator.ps1` 此指令碼會建立公用資料夾至信箱的對應檔案。

  - `PublicFolderToMailboxMapGenerator.strings.psd1` 此支援檔案由 PublicFolderToMailboxMapGenerator.ps1 指令碼及應下載到相同位置。

  - `Create-PublicFolderMailboxesForMigration.ps1` 此指令碼會建立目標公用資料夾信箱移轉。此外，此指令碼來計算處理估計的使用者負載，根據 \[使用者登入每個公用資料夾信箱中[公用資料夾的限制](limits-for-public-folders-exchange-2013-help.md)建議數的準則所需的信箱數目。

  - `Create-PublicFolderMailboxesForMigration.strings.psd1` 此支援檔案由建立 PublicFolderMailboxesForMigration.ps1 指令碼及應下載到相同位置。

步驟 1： 下載移轉指令碼提供關於到哪裡下載這些指令碼的詳細資訊。請確定所有的指令碼會下載到相同位置。

如需與公用資料夾相關的其他管理工作，請參閱 [公用資料夾程序](public-folder-procedures-exchange-2013-help.md)。

## 哪些版本的 Exchange 支援將公用資料夾移轉至 Exchange 2013？

Exchange 支援從下列舊版 Exchange Server 移轉公用資料夾：

  - Exchange 2010 SP3 RU8 或更新版本

  - Exchange 2007 SP3 RU15 或更新版本

如果您需要將您的公用資料夾移至 Exchange 2013，但您的內部伺服器未執行 Exchange 2010 或 Exchange 2007 的最小支援版本，請參閱[使用序列遷移公用資料夾從舊版移轉至 Exchange 2013](https://technet.microsoft.com/zh-tw/library/jj150486\(v=exchg.150\))。序列移轉則使用此選項，我們強烈建議您升級您的內部伺服器並使用批次移轉。批次移轉允許大幅更快且更大的可靠性。

您無法直接從 Exchange 2003 移轉公用資料夾。如果您正在執行 Exchange 2003 組織中，您必須移動所有公用資料夾資料庫和為 Exchange 2010 SP3 RU8 或更新版本，或以 Exchange 2007 SP3 RU15 或更新版本的複本。沒有公用資料夾複本可保留在 Exchange 2003。此外，目的地 Exchange 2013 公用資料夾的郵件無法透過 Exchange 2003 伺服器。

## 開始之前有哪些須知？

  - 開始之前，建議您閱讀本主題全文，因為部分步驟需要停機。

  - Exchange 2010 伺服器必須執行 Exchange 2010 SP3 RU8 或更新版本。

  - Exchange 2007 伺服器必須執行 Exchange 2007 SP3 RU15 或更新版本。

  - 可在單一遷移遷移至 Exchange 2013 公用資料夾數目上限為 500000。

  - 在 Exchange 2013，您需要為組織管理角色群組的成員。如需如何啟用 「 組織管理角色群組的詳細資訊，請參閱[管理角色群組](manage-role-groups-exchange-2013-help.md)。

  - 在 Exchange 2010，您需要為組織管理或伺服器管理 RBAC 角色群組的成員。如需詳細資訊，請參閱[新增成員至角色群組](https://go.microsoft.com/fwlink/?linkid=299212)。

  - 在 Exchange 2007 中，您需要 Exchange 組織系統管理員角色或 Exchange Server 系統管理員角色指派。此外，您需要指派公用資料夾系統管理員角色和目標伺服器的本機管理員群組。如需詳細資訊，請參閱 ＜[如何新增使用者或系統管理員角色群組](https://go.microsoft.com/fwlink/p/?linkid=81779)。

  - 在 Exchange 2007 伺服器上，升級為 [Windows PowerShell 2.0 和 WinRM 2.0 for Windows Server 2008 x64 Edition](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=968930)。

  - 在遷移之前，您應考量[公用資料夾的限制](limits-for-public-folders-exchange-2013-help.md)。

  - 在遷移之前，將所有使用者信箱都移至 Exchange 2013 因為具有 Exchange 2007 或 Exchange 2010 信箱的使用者將無法存取 Exchange 2013 公用資料夾。如需詳細資訊，請參閱[在 Exchange 2013 移動信箱](mailbox-moves-in-exchange-2013-exchange-2013-help.md)。

  - 在多個網域環境中，擁有郵件功能的公用資料夾會停止如果子網域中執行 Exchange 移轉至 Exchange 2013 之後使用。這是因為在 Exchange 2013、 擁有郵件功能的公用資料夾物件所需的根網域之下。若要解決這個問題，您需要停用郵件功能啟用郵件功能的公用資料夾，然後啟用郵件功能它們同樣地，可讓您將其移至正確的網域位置。

  - 移轉後已完成，如果您想要將郵件傳送給移轉擁有郵件功能的公用資料夾的外部寄件者，**匿名**使用者必須要授與至少**建立項目**權限。如果您不這麼做，外部寄件者會收到傳遞失敗通知及訊息將不會傳遞至已移轉擁有郵件功能的公用資料夾。閱讀更多有關如何設定權限匿名使用者，請參閱[郵件啟用或停用郵件功能的公用資料夾](mail-enable-or-mail-disable-a-public-folder-exchange-2013-help.md)。

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

## 步驟 2：準備移轉

先執行下列必要步驟，再開始移轉。

**舊版 Exchange 伺服器上的必要步驟**

1.  為了驗證移轉的結尾，建議您先採取的目前的公用資料夾部署的快照舊版 Exchange 伺服器上執行下列命令：
    
      - 執行下列命令以擷取原始來源資料夾結構的快照：
        
            Get-PublicFolder -Recurse | Export-CliXML C:\PFMigration\Legacy_PFStructure.xml
    
      - 執行下列命令以取得快照的等項目計數、 大小以及擁有者的公用資料夾統計資料：
        
            Get-PublicFolderStatistics | Export-CliXML C:\PFMigration\Legacy_PFStatistics.xml
    
      - 執行下列命令以取得快照的權限：
        
            Get-PublicFolder -Recurse | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML C:\PFMigration\Legacy_PFPerms.xml
    
    儲存來自前述命令的資訊，以便在移轉完成後進行比較。

2.  如果公用資料夾的名稱包含反斜線 (**\\**)，移轉時會將公用資料夾建立在公用資料夾的上層資料夾中。移轉之前，建議您將所有名稱含有反斜線的公用資料夾重新命名。
    
    1.  在 Exchange 2010 中，想要找到名稱包含反斜線的公用資料夾，可執行下列命令：
        
            Get-PublicFolderStatistics -ResultSize Unlimited | Where {($_.Name -like "*\*") -or ($_.Name -like "*/*") } | Format-List Name, Identity
    
    2.  在 Exchange 2007 中，想要找到名稱包含反斜線的公用資料夾，可執行下列命令：
        
            Get-PublicFolderDatabase | ForEach {Get-PublicFolderStatistics -Server $_.Server | Where {$_.Name -like "*\*"}}
    
    3.  如果傳回任何公用資料夾，可以執行下列命令將其重新命名：
        
            Set-PublicFolder -Identity <public folder identity> -Name <new public folder name>

3.  請確定沒有成功完成遷移上一筆記錄。
    
    1.  以下範例會檢查公用資料夾移轉狀態。
        
            Get-OrganizationConfig | Format-List PublicFoldersLockedforMigration, PublicFolderMigrationComplete
        
        如果已先前成功完成遷移， *PublicFoldersLockedforMigration*或*PublicFolderMigrationComplete*屬性的值為`$true`。若要將值設定為`$false`用於步驟 3b 命令。如果值設為`$true`、 遷移要求將會失敗。
    
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


如需詳細的語法及參數資訊，請參閱下列主題：

  - [Get-PublicFolder](https://technet.microsoft.com/zh-tw/library/aa997615\(v=exchg.150\))

  - [Get-PublicFolderDatabase](https://technet.microsoft.com/zh-tw/library/jj733416\(v=exchg.150\))

  - [Set-PublicFolder](https://technet.microsoft.com/zh-tw/library/aa998596\(v=exchg.150\))

  - [Get-PublicFolderStatistics](https://technet.microsoft.com/zh-tw/library/aa998663\(v=exchg.150\))

  - [Get-PublicFolderClientPermission](https://technet.microsoft.com/zh-tw/library/bb124365\(v=exchg.150\))

  - [Get-organizationconfig](https://go.microsoft.com/fwlink/p/?linkid=183212)

  - [Set-organizationconfig](https://go.microsoft.com/fwlink/p/?linkid=183213)

**Exchange 2013 伺服器上的必要步驟**

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

2.  確定沒有公用資料夾或公用資料夾信箱存在 Exchange 2013 伺服器上。
    
    1.  執行下列命令，以查看是否有任何公用資料夾信箱存在。
        
            Get-Mailbox -PublicFolder 
    
    2.  如果命令沒有傳回任何公用資料夾信箱，請繼續進行步驟 3： 產生.csv 檔案。如果此命令會傳回任何公用資料夾，請執行下列命令，以查看是否有任何公用資料夾存在：
        
            Get-PublicFolder
    
    3.  如果您有任何公用資料夾，請執行下列 PowerShell 命令加以移除。請確定您已儲存在公用資料夾中的任何資訊。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>當您移除它們會永久刪除公用資料夾中所包含的所有資訊。</td>
        </tr>
        </tbody>
        </table>
        
            Get-Mailbox -PublicFolder | Where{$_.IsRootPublicFolderMailbox -eq $false} | Remove-Mailbox -PublicFolder -Force -Confirm:$false
        
            Get-Mailbox -PublicFolder | Remove-Mailbox -PublicFolder -Force -Confirm:$false

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

1.  在舊版 Exchange 伺服器上執行`Export-PublicFolderStatistics.ps1`指令碼來建立資料夾名稱至資料夾大小的對應檔案。此指令碼必須以本機系統管理員身分執行。檔案會包含兩個資料行： **FolderName**和**FolderSize**。**FolderSize**欄的值將會顯示以位元組為單位。例如， **\\PublicFolder01,10000**。
    
        .\Export-PublicFolderStatistics.ps1  <Folder to size map path> <FQDN of source server>
    
      - *FQDN of source server* 等於主控公用資料夾階層的信箱伺服器之完整網域名稱。
    
      - *Folder to size map path*等於您想要儲存.csv 檔案的網路共用資料夾的路徑與檔案名稱。在本主題稍後您需要從 Exchange 2013 伺服器存取此檔案。如果您指定的檔案名稱，該檔案會產生於本機電腦的目前 PowerShell 目錄中。

2.  執行`PublicFolderToMailboxMapGenerator.ps1`指令碼建立公用資料夾至信箱的對應檔案。此檔案用來計算的 Exchange 2013 Mailbox server 上的公用資料夾信箱的正確的號碼。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果公用資料夾的名稱包含反斜線<strong>\</strong>，將公用資料夾會建立上層公用資料夾中。我們建議您檢閱.csv 檔案並編輯任何名稱包含反斜線。</td>
    </tr>
    </tbody>
    </table>
    
        .\PublicFolderToMailboxMapGenerator.ps1 <Maximum mailbox size in bytes> <Folder to size map path> <Folder to mailbox map path>
    
      - *Maximum mailbox size in bytes*等於您想要設定新的公用資料夾信箱的大小上限。指定此設定時，請確定允許擴充，讓公用資料夾信箱擁有成長空間。
    
      - *Folder to size map path* 等於執行 `Export-PublicFolderStatistics.ps1` 指令碼時建立之 .csv 檔案的路徑。
    
      - *Folder to mailbox map path* 等於您使用此步驟建立的資料夾至信箱 .csv 檔案的檔案名稱與路徑。如果您僅指定檔案名稱，檔案將在本機電腦上目前的 PowerShell 位置中產生。

## 步驟 4： 建立公用資料夾信箱在 Exchange 2013

1.  執行下列命令以建立目標公用資料夾信箱。指令碼會建立您先前在步驟 3 中產生的 .csv 檔案中每個信箱的目標信箱，方法是執行 PublicFoldertoMailboxMapGenerator.ps1 指令碼。
    
        .\Create-PublicFolderMailboxesForMigration.ps1 -FolderMappingCsv Mapping.csv -EstimatedNumberOfConcurrentUsers:<estimate>
    
    *Mapping.csv* 是 PublicFoldertoMailboxMapGenerator.ps1 指令碼在步驟 3 建立的檔案。瀏覽公用資料夾階層的使用者同時連線估計數量通常小於組織中使用者的總數。

## 步驟 5：啟動移轉要求

將 Exchange 2007 公用資料夾的步驟是將 Exchange 2010 公用資料夾的步驟與不同。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>是否從 Exchange 2007 或 Exchange 2010 移轉批次移轉要求使用適當的指令程式建立之後，您可以再檢視要求和管理它們在 EAC 中。</td>
</tr>
</tbody>
</table>


**移轉 Exchange 2007 公用資料夾**

1.  例如 OWAScratchPad 與結構描述根資料夾樹狀子目錄的舊版系統公用資料夾在 Exchange 2007 Exchange 2013 將不會辨識與因此會被視為 「 故障 」 項目。這會導致移轉失敗。移轉要求的一部分，您必須指定`BadItemLimit`參數的值。這個值將會取決於您所具有的公用資料夾資料庫數目而有所不同。下列命令將會決定多少公用資料夾資料庫有和計算`BadItemLimit`遷移要求。
    
        $PublicFolderDatabasesInOrg = @(Get-PublicFolderDatabase)
    
        $BadItemLimitCount = 5 + ($PublicFolderDatabasesInOrg.Count -1)

2.  在 Exchange 2013 伺服器上，執行下列命令：
    
        New-MigrationBatch -Name PFMigration -SourcePublicFolderDatabase (Get-PublicFolderDatabase -Server <Source server name>) -CSVData (Get-Content <Folder to mailbox map path> -Encoding Byte) -NotificationEmails <email addresses for migration notifications> -BadItemLimit $BadItemLimitCount 

3.  開始移轉使用下列命令：
    
        Start-MigrationBatch PFMigration

**移轉 Exchange 2010 公用資料夾**

1.  在 Exchange 2013 伺服器上，執行下列命令。
    
        New-MigrationBatch -Name PFMigration -SourcePublicFolderDatabase (Get-PublicFolderDatabase -Server <Source server name>) -CSVData (Get-Content <Folder to mailbox map path> -Encoding Byte) -NotificationEmails <email addresses for migration notifications> 
    
    `NotificationEmails`參數是選擇性的。

2.  開始移轉使用下列命令：
    
        Start-MigrationBatch PFMigration
    
    或者：
    
    您可以在 EAC 中啟動移轉。
    
    1.  登入 Exchange Online 並開啟 EAC。
    
    2.  瀏覽至 \[**收件者**\>**移轉**。
    
    3.  選取您剛建立的遷移批次然後再按一下 \[開始\] 按鈕。

\[狀態\] 欄會將初始批次狀態顯示為 \[已建立\]。狀態會在移轉期間變更為 \[正在同步處理\]。完成移轉要求時，而狀態為 \[已同步處理\]。您可以按兩下批次以檢視批次中個別信箱的狀態。信箱工作的開始狀態為 \[已排入佇列\]。工作開始時的狀態為 \[正在同步處理\]，一旦 `InitialSync` 完成，狀態會顯示為 \[已同步處理\]。

可以檢視及管理在 EAC 中的進度和完成移轉。因為**New-migrationbatch**指令程式起始每個公用資料夾信箱的信箱遷移要求，您可以檢視信箱移轉\] 頁面上使用這些要求的狀態。您可以取得信箱移轉\] 頁面上，並建立可執行下列動作傳送至您的移轉報告：

1.  登入 Exchange Online 並開啟 EAC。

2.  瀏覽至 \[信箱\] \> \[移轉\]。

3.  選取剛建立的移轉要求和**詳細資料**窗格中 \[**檢視詳細資料**。

如需詳細的語法及參數資訊，請參閱下列主題：

  - [New-PublicFolderMigrationRequest](https://technet.microsoft.com/zh-tw/library/jj218636\(v=exchg.150\))

  - [Get-PublicFolderDatabase](https://technet.microsoft.com/zh-tw/library/jj733416\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequest](https://technet.microsoft.com/zh-tw/library/jj218718\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequestStatistics](https://technet.microsoft.com/zh-tw/library/jj218697\(v=exchg.150\))

## 步驟 6：鎖定舊版 Exchange 伺服器上的公用資料夾以進行最終移轉 (需停機)

到了移轉的這個階段，使用者已經可以存取公用資料夾。後續步驟會將使用者從舊版公用資料夾登出，並且鎖定資料夾，讓遷移能夠完成其最後同步處理。使用者將無法在此程序期間存取公用資料夾。另外，所有傳送到擁有郵件功能之公用資料夾的郵件都將排入佇列，直到公用資料夾移轉完成後才進行遞送。

在執行`PublicFoldersLockedForMigration`命令如下所示之前，請確定所有工作都是**已同步**狀態。您可以執行`Get-PublicFolderMailboxMigrationRequest`命令來這麼做。您已驗證的所有工作都會在**已同步**狀態後繼續執行此步驟。

在舊版 Exchange 伺服器上，執行下列命令鎖定舊版公用資料夾以完成移轉。

    Set-OrganizationConfig -PublicFoldersLockedForMigration:$true

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果有任何原因的遷移批次檔案不會未完成 （<strong>PublicFolderMigrationComplete</strong>顯示<strong>為 False</strong>），舊版伺服器上，請重新啟動資訊存放區 (IS)。</td>
</tr>
</tbody>
</table>


如需詳細的語法及參數資訊，請參閱 [Set-OrganizationConfig](https://technet.microsoft.com/zh-tw/library/aa997443\(v=exchg.150\))。

如果組織有多個公用資料夾資料庫，必須等到公用資料夾複寫完成，才能確認所有公用資料夾資料庫已選取 `PublicFoldersLockedForMigration` 標幟，且已集中整個組織中使用者最近對資料夾進行而遭擱置的所有變更。可能會花幾小時的時間。

## 步驟 7：完成公用資料夾移轉 (需要停機)

首先，執行下列 cmdlet 以將 Exchange 2013 部署類型變更為**遠端**：

    Set-OrganizationConfig -PublicFoldersEnabled Remote

完成之後，您可以執行下列命令來完成公用資料夾移轉︰

    Complete-MigrationBatch PublicFolderMigration

或者在 EAC 中，您可以藉由按一下 **\[完成此移轉批次\]** 來完成移轉。

當您完成移轉時，Exchange 會執行舊版 Exchange server 與 Exchange 2013 間的最終同步處理。如果最終同步處理成功，在 Exchange 2013 伺服器上的公用資料夾會先解除鎖定並的遷移批次狀態會變更為**完成**，然後按一下 \[**已完成**。常見的遷移批次所從**已同步**其狀態變更前的幾小時才需**完成**，最終同步處理會開始在其中點。

## 步驟 8：測試並解除鎖定公用資料夾移轉

完成公用資料夾移轉後，應該執行下列測試以確定移轉成功。這可讓您先測試移轉後的公用資料夾階層，再切換為使用 Exchange 2013 公用資料夾。

1.  在 PowerShell 中執行下列命令來指派一些測試信箱使用新遷移的公用資料夾信箱作為預設公用資料夾信箱。
    
        Set-Mailbox -Identity <Test User> -DefaultPublicFolderMailbox <Public Folder Mailbox Identity>

2.  以上一個步驟的測試使用者身分登入 Outlook 2007 或更新版本，然後執行下列公用資料夾測試：
    
      - 檢視階層。
    
      - 檢查權限。
    
      - 建立與刪除公用資料夾。
    
      - 張貼內容至公用資料夾以及刪除公用資料夾的內容。

3.  如果您執行發生任何問題，請參閱本主題稍後的回復移轉。如果公用資料夾內容和階層是可接受且正常運作，執行下列命令以解除鎖定的所有其他使用者的公用資料夾。
    
        Get-Mailbox -PublicFolder | Set-Mailbox -PublicFolder -IsExcludedFromServingHierarchy $false
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>在完成初始遷移驗證後，請不要使用 <em>IsExcludedFromServingHierarchy</em> 參數，因為此參數是由 Exchange Online 的自動儲存管理服務所使用。</td>
    </tr>
    </tbody>
    </table>


4.  在舊版 Exchange 伺服器上，執行下列命令列以指出公用資料夾移轉完成：
    
        Set-OrganizationConfig -PublicFolderMigrationComplete:$true

5.  移轉已完成之後，執行下列命令：
    
        Set-OrganizationConfig -PublicFoldersEnabled Local

6.  最後，如果您想要將郵件傳送給移轉擁有郵件功能的公用資料夾的外部寄件者，**匿名**使用者必須取得至少**建立項目**權限。如果您不這麼做，外部寄件者會收到傳遞失敗通知及訊息將不會傳遞至已移轉擁有郵件功能的公用資料夾。
    
    您可以使用命令介面或 Outlook 在匿名使用者設定權限。閱讀更多有關如何設定權限匿名使用者，請參閱[郵件啟用或停用郵件功能的公用資料夾](mail-enable-or-mail-disable-a-public-folder-exchange-2013-help.md)。

## 如何知道這是否正常運作？

在步驟 2： 準備移轉、 所指示開始移轉之前所採取的公用資料夾結構、 統計資料，以及權限的快照。下列步驟將協助您確認您的公用資料夾移轉成功完成移轉後採取相同的快照集。您可以再比較若要驗證成功這兩個檔案中的資料。

1.  執行下列命令以擷取新資料夾結構的快照。
    
        Get-PublicFolder -Recurse | Export-CliXML C:\PFMigration\Cloud_PFStructure.xml

2.  執行下列命令以擷取公用資料夾統計資料的快照，例如項目計數、大小以及擁有者。
    
        Get-PublicFolderStatistics -ResultSize Unlimited | Export-CliXML C:\PFMigration\Cloud_PFStatistics.xml

3.  執行下列命令以擷取權限的快照。
    
        Get-PublicFolder -Recurse | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML  C:\PFMigration\Cloud_PFPerms.xml

## 移除舊版 Exchange 伺服器上的公用資料夾資料庫

完成移轉後，且已驗證 Exchange 2013 公用資料夾運作如預期，您應該移除舊版 Exchange 伺服器上的公用資料夾資料庫。

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
<td>如果您回復移轉到舊版的 Exchange 伺服器，您會失去所有電子郵件傳送至擁有郵件功能的公用資料夾或張貼至 Exchange 2013 公用資料夾的移轉後的內容。若要儲存此內容，您需要將公用資料夾內容匯出至.pst 檔案並再匯入舊版公用資料夾回復完成時。</td>
</tr>
</tbody>
</table>


1.  在舊版 Exchange 伺服器上，執行下列命令解除鎖定舊版 Exchange 公用資料夾。此程序可能會花幾小時的時間。
    
        Set-OrganizationConfig -PublicFoldersLockedForMigration:$False

2.  在 Exchange 2013 伺服器上，執行下列命令移除公用資料夾信箱。
    
        Get-Mailbox -PublicFolder | Where{$_.IsRootPublicFolderMailbox -eq $false} | Remove-Mailbox -PublicFolder -Force -Confirm:$false
        
        Get-Mailbox -PublicFolder | Remove-Mailbox -PublicFolder -Force -Confirm:$false

3.  在舊版 Exchange 伺服器上，執行下列命令將 `PublicFolderMigrationComplete` 標幟設定為 `$false`。
    
        Set-OrganizationConfig -PublicFolderMigrationComplete:$False

