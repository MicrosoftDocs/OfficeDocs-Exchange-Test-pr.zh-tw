---
title: '使用批次移轉至 Exchange 2013 公用資料夾移轉到 Office 365 群組: Exchange 2013 Help'
TOCTitle: 使用批次移轉至 Exchange 2013 公用資料夾移轉到 Office 365 群組
ms:assetid: 1d800576-957d-4916-ae2a-55c08ca75be1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Mt843873(v=EXCHG.150)
ms:contentKeyID: 74468742
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用批次移轉至 Exchange 2013 公用資料夾移轉到 Office 365 群組

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2018-03-26_

**摘要：** 如何將 Exchange 2013 公用資料夾移至 Office 365 群組。

透過稱為*批次移轉*程序，則可以移到 Office 365 群組的部分或所有 Exchange 2013 公用資料夾。群組是具有某些優點透過公用資料夾的 microsoft 提供新的共同作業。請參閱[將公用資料夾移轉至 Office 365 群組](migrate-your-public-folders-to-office-365-groups-exchange-2013-help.md)如需公用資料夾及群組，並原因為何您的組織可能有或可能不會受益於切換到群組之間的差異的概觀。

本文包含 Exchange 2013 公用資料夾的實際的批次移轉執行的逐步程序。

## 開始之前有哪些須知？

請確定符合下列條件的所有符合之前準備的移轉。

  - Exchange 2013 伺服器必須執行**Exchange 2013 CU15**或更新版本。

  - 在 Exchange Online 中，您需要為組織管理角色群組的成員。此角色群組是不同 Office 365 或 Exchange Online 訂閱時指派給您的權限。如需如何啟用 「 組織管理角色群組的詳細資訊，請參閱[管理角色群組](manage-role-groups-exchange-2013-help.md)。

  - 在 Exchange 2013，您需要為組織管理或伺服器管理 RBAC 角色群組的成員。如需詳細資訊，請參閱[新增成員至角色群組](https://go.microsoft.com/fwlink/?linkid=299212)。

  - 將公用資料夾移轉至 Office 365 群組之前，建議您先將移使用者信箱至 Office365 的移轉後需要存取 Office 365 群組的使用者。如需詳細資訊，請參閱 ＜[移轉至 Office 365 的多個電子郵件帳戶的方式](https://support.office.com/article/ways-to-migrate-multiple-email-accounts-to-office-365-0a4913fe-60fb-498f-9155-a86516418842)。

  - 需要至少一部 Exchange 伺服器上，啟用 MRS Proxy 及該伺服器必須也要主控公用資料夾信箱。請參閱[啟用遠端移動 MRS Proxy 端點](enable-the-mrs-proxy-endpoint-for-remote-moves-exchange-2013-help.md)如需詳細資訊。

  - 您無法使用 Exchange 系統管理中心 (EAC) 或 Exchange 管理主控台 (EMC) 來執行此程序。Exchange 2013 伺服器上，您需要使用 Exchange 管理命令介面。Exchange Online 中，您需要使用Exchange Online PowerShell。如需詳細資訊，請參閱 ＜ [Connect to Exchange Online 使用遠端 PowerShell](https://technet.microsoft.com/library/jj984289\(v=exchg.150\).aspx)。

  - 僅限類型行事曆和郵件的公用資料夾可移轉至 Office 365 群組在此階段;其他類型的公用資料夾的移轉不受支援。此外，Office 365 中的目標群組期望建立才能進行移轉。

  - 批次移轉程序只會複製郵件和行事曆項目從公用資料夾遷移至 Office 365 群組。由於這些不支援的 Office 365 群組，它不會複製 like 原則、 規則及權限的公用資料夾的其他實體。

  - Office 365 群組隨附 50 GB 信箱。請確認您要移轉的公用資料夾資料的總和合計小於 50 GB。此外，未來，新增您的使用者所擁有的其他內容的儲存空間移轉後保留。建議您將公用資料夾遷移不人質大於 25 GB 的總大小。

  - 這不是"所有或 nothing"移轉。您可以挑選特定的公用資料夾移轉，並將移轉只有那些公用資料夾。如果要移轉的公用資料夾的子資料夾，這些子資料夾將不會自動包含在移轉。如果您需要移轉這些，您需要明確納入它們。

  - 將公用資料夾將不會受到任何方式此移轉。不過，一次您使用我們向下鎖定指令碼唯讀，讓使用者將會強制使用 Office 365 群組而不是公用資料夾進行移轉的公用資料夾。

  - 開始之前，建議您先閱讀本文全文，因為部分步驟需要停機。

## 步驟 1： 取得指令碼

批次移轉至 Office 365 群組需要於不同時間點的移轉執行許多指令碼如下所示的本文。下載指令碼和其支援的檔案[從這個位置](https://www.microsoft.com/en-us/download/details.aspx?id=55985)。下載所有指令碼和檔案之後，請將其儲存至相同的位置，例如`c:\PFtoGroups\Scripts`。

再繼續執行，確認您已下載並儲存的所有下列指令碼及檔案：

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>請確定所有指令碼檔案儲存到相同位置。</td>
</tr>
</tbody>
</table>


  - **AddMembersToGroups.ps1**。 此指令碼會新增成員與 Office 365 群組擁有者根據來源公用資料夾中的權限項目。

  - **AddMembersToGroups.strings.psd1**。 此支援檔案由指令碼`AddMembersToGroups.ps1`。

  - **LockAndSavePublicFolderProperties.ps1**。 此指令碼建立公用資料夾，以避免任何修改、 唯讀並且轉接郵件相關的公用資料夾內容 （提供公用資料夾所擁有郵件功能） 到目標群組，其重新將路由的公用資料夾的電子郵件傳送至目標群組。此指令碼也會備份權限項目和 mail 屬性然後再修改它們。

  - **LockAndSavePublicFolderProperties.strings.psd1：** 此支援檔案由指令碼`LockAndSavePublicFolderProperties.ps1`。

  - **UnlockAndRestorePublicFolderProperties.ps1**。 此指令碼還原存取權限及使用`LockandSavePublicFolderProperties.ps1`所建立的備份檔案的公用資料夾的郵件內容。

  - **UnlockAndRestorePublicFolderProperties.strings.psd1**。 此支援檔案由指令碼`UnlockAndRestorePublicFolderProperties.ps1`。

  - **WriteLog.ps1**。 此指令碼可讓上述的三個指令碼可寫入記錄檔。

  - **RetryScriptBlock.ps1**。 此指令碼可讓特定動作發生暫時性錯誤時的重試`AddMembersToGroups`、 `LockAndSavePublicFolderProperties`，以及`UnlockAndRestorePublicFolderProperties`指令碼。

如需`AddMembersToGroups.ps1`的詳細資訊， `LockAndSavePublicFolderProperties.ps1`，及`UnlockAndRestorePublicFolderProperties.ps1`、 及它們在您的環境中執行的工作請參閱移轉指令碼本文稍後的。

## 步驟 2：準備移轉

下列步驟所需準備您的組織進行移轉：

1.  編譯公用資料夾 （郵件和行事曆類型） 您要移轉至 Office 365 群組的清單。

2.  必須針對每個要移轉的公用資料夾的對應目標群組的清單。您可以在 Office 365 中建立新群組的每個公用資料夾或使用現有的群組。如果您正在建立新的群組，請參閱[了解 Office 365 群組](https://go.microsoft.com/fwlink/p/?linkid=858521)了解群組必須具備的設定。如果您要移轉的公用資料夾設為**作者**或高於預設權限，您應該在 Office 365 中建立對應的群組與**公用**的隱私權設定。不過，請參閱在 Outlook 中的 \[**群組**\] 節點下的 \[公用\] 群組的使用者，他們仍然可以加入群組。

3.  重新命名任何包含在其名稱 (\\) 反斜線的公用資料夾。否則，這些公用資料夾可能會移轉正確。

4.  您需要有**PAW**啟用您的 Office 365 租用戶移轉功能。若要確認此，請在 Exchange Online PowerShell 中執行下列命令：
    
        Get-MigrationConfig
    
    如果**功能**下的輸出會列出**PAW**，則會啟用的功能和您可以繼續*步驟 3： 花費.csv 檔案*。
    
    如果不是爪尚未啟用您的租用戶，它可能是因為您有一些現有的遷移批次，公用資料夾批次或使用者批次。這些批次可能是任何的狀態，包括已完成。如果是這樣，請完成並移除任何現有的遷移批次直到您執行`Get-MigrationBatch`時不會傳回任何記錄。移除所有現有的批次之後, 爪應取得自動啟用。請注意變更可能不會反映在`Get-MigrationConfig`立即，這是外觀可以。這個步驟完成之後，您可以繼續建立新的批次的使用者移轉。

## 步驟 3： 建立.csv 檔案

建立.csv 檔案中，輸入提供一個移轉指令碼。

.Csv 檔案必須包含下列資料行：

  - **FolderPath**。要移轉的公用資料夾的路徑。

  - **TargetGroupMailbox**。Office 365 中的目標群組的 SMTP 地址。您可以執行下列命令，請參閱的主要 SMTP 位址。
    
        Get-UnifiedGroup <alias of the group> | Format-Table PrimarySmtpAddress

範例.csv：

    "FolderPath","TargetGroupMailbox"
    "\Sales","sales@contoso.onmicrosoft.com"
    "\Sales\EMEA","emeasales@contoso.onmicrosoft.com"

請注意的郵件資料夾和行事曆\] 資料夾可被合併到 Office 365 中的單一群組。不過，合併成一個群組的多個公用資料夾的任何其他案例不支援內的單一遷移批次。如果您需要將多個公用資料夾對應至相同的 Office 365 群組，您可以完成這個動作執行不同的移轉批次，應該要執行連續、 之後彼此。您可以在每一個遷移批次中有最多 500 個項目。

某個公用資料夾應移轉至一個遷移批次中只有一個群組。

## 步驟 4： 啟動遷移要求

在此步驟中，您收集資訊從 Exchange 環境，而且再使用該資訊Exchange Online PowerShell中建立遷移批次。之後，您可以啟動移轉。

1.  在 Exchange 2013 伺服器上，尋找 MRS proxy 端點伺服器並記下其。當您執行遷移要求必須稍後此資訊。

2.  在Exchange Online PowerShell，使用步驟 1 到執行下列命令中上面所傳回的資訊。這些命令中的變數會是步驟 1 中的值。
    
    1.  在 Exchange 2013 環境的使用管理員權限的使用者認證傳遞至變數`$Source_Credential`中。當您最後執行遷移要求在 Exchange Online 時，您將會使用此認證來存取至 Exchange 2013 伺服器以一段的內容複製到 Exchange Online。
        
            $Source_Credential = Get-Credential
            <source_domain>\<PublicFolder_Administrator_Account>
    
    2.  使用您在上述步驟 1 中記下您 Exchange 2013 環境的 MRS proxy 伺服器資訊並將該值傳至變數`$Source_RemoteServer`。
        
            $Source_RemoteServer = "<MRS proxy endpoint>"

3.  在Exchange Online PowerShell，執行下列命令來建立遷移端點：
    
        $PfEndpoint = New-MigrationEndpoint -PublicFolderToUnifiedGroup -Name PFToGroupEndpoint -RemoteServer $Source_RemoteServer -Credentials $Source_Credential

4.  執行下列命令以建立新公用資料夾至 Office 365 群組遷移批次。在此命令：
    
      - **CSVData**是在上述建立的.csv 檔案*步驟 3： 建立.csv 檔案*。請務必提供此檔案的完整路徑。若檔案已移動有任何原因，請務必確認和使用新的位置。
    
      - **NotificationEmails**是選擇性的參數可以用來將會收到相關的狀態與進度移轉之通知的電子郵件地址。
    
      - **自動啟動**為選用參數它會使用時，請建立為啟動遷移批次。
    
      - **PublicFolderToUnifiedGroup**是表示它是 Office 365 群組遷移批次公用資料夾的參數。
    
    <!-- end list -->
    
        New-MigrationBatch -Name PublicFolderToGroupMigration -CSVData (Get-Content <path to .csv file> -Encoding Byte) -PublicFolderToUnifiedGroup -SourceEndpoint $PfEndpoint.Identity [-NotificationEmails <email addresses for migration notifications>] [-AutoStart]

5.  Exchange Online PowerShell中執行下列命令來啟動移轉。請注意這是必要步驟只有在`-AutoStart`參數已無法使用時在步驟 4 中建立的批次以上。
    
        Start-MigrationBatch PublicFolderToGroupMigration

雖然批次移轉需要建立Exchange Online PowerShell中使用`New-MigrationBatch`指令程式，可以檢視及Exchange 系統管理中心中受管理移轉的進度。您也可以藉由執行[Get-MigrationBatch](https://technet.microsoft.com/zh-tw/library/jj219164\(v=exchg.150\))和[Get-MigrationUser](https://technet.microsoft.com/zh-tw/library/jj218702\(v=exchg.150\))指令程式檢視移轉的進度。`New-MigrationBatch`指令程式會移轉使用者的每個 Office 365 群組信箱，且您可以檢視信箱移轉\] 頁面上使用這些要求的狀態。

若要檢視信箱移轉\] 頁面上：

1.  在 Exchange Online 中，開啟 \[ Exchange 系統管理中心\]。

2.  瀏覽至 \[**收件者**，然後再選取 \[**移轉**。

3.  選取剛建立的移轉要求，然後在**詳細資料**\] 窗格中，選取 \[**檢視詳細資料**。

**已完成**的批次狀態時，則可以移到上*步驟 5： 將成員新增至 Office 365 群組從公用資料夾*。

## 步驟 5： 將成員新增至 Office 365 群組從公用資料夾

您可以將成員新增至 Office 365 中手動所需的目標群組。不過，如果您想要新增成員至公用資料夾中的權限項目為基礎的群組，您需要藉由 Exchange 2013 伺服器上的指令碼`AddMembersToGroups.ps1`執行下列命令所示。使用者信箱必須同步處理至 Exchange Online 才能新增為 Office 365 群組的成員。 若要知道哪些公用資料夾權限所要新增為 Office 365 中群組的成員資格，請參閱本文稍後的移轉指令碼。

在下列命令：

  - **MappingCsv**是在上述建立的.csv 檔案*步驟 3： 建立.csv 檔案*。請務必提供此檔案的完整路徑。若檔案已移動有任何原因，請務必確認和使用新的位置。

  - **BackupDir**是移轉記錄檔會儲存所在的目錄。

  - **ArePublicFoldersOnPremises**是以指出公用資料夾是否位於內部部署或 Exchange Online 中的參數。

  - **Credential**是 Exchange Online 使用者名稱和密碼。

<!-- end list -->

    .\AddMembersToGroups.ps1 -MappingCsv <path to .csv file> -BackupDir <path to backup directory> -ArePublicFoldersOnPremises $true -Credential (Get-Credential)

一旦使用者已新增至 Office 365 中的群組，他們可以開始使用它。

## 步驟 6： 鎖定公用資料夾 （需公用資料夾停機）

當您的公用資料夾中的資料多數 」 已移轉至 Office 365 群組時，您可以執行指令碼`LockAndSavePublicFolderProperties.ps1`在 Exchange 2013 伺服器上以唯讀方式將公用資料夾。此步驟可確保沒有新的資料會新增至 \[公用資料夾移轉完成之前。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有擁有郵件功能的公用資料夾 (MEPFs) 之間的公用資料夾遷移，此步驟會將 MEPFs，例如 SMTP 位址的某些屬性複製到 Office 365 中的對應群組，然後停用郵件功能的公用資料夾。因為移轉 MEPFs 將會停用之後執行此指令碼的您會啟動看不到傳送至 MEPFs 改用相對應的群組中接收電子郵件。如需詳細資訊，請參閱本文稍後的移轉指令碼。</td>
</tr>
</tbody>
</table>


在下列命令：

  - **MappingCsv**是在上述建立的.csv 檔案*步驟 3： 建立.csv 檔案*。請務必提供此檔案的完整路徑。若檔案已移動有任何原因，請務必確認和使用新的位置。

  - **BackupDir**是儲存備份檔案的權限項目、 MEPF 屬性與移轉記錄檔的目錄。此備份會很有用以防您需要回復至 \[公用資料夾。

  - **ArePublicFoldersOnPremises**是以指出公用資料夾是否位於內部部署或 Exchange Online 中的參數。

  - **Credential**是 Exchange Online 使用者名稱和密碼。

<!-- end list -->

    .\LockAndSavePublicFolderProperties.ps1 -MappingCsv <path to .csv file> -BackupDir <path to backup directory> -ArePublicFoldersOnPremises $true -Credential (Get-Credential)

## 步驟 7： 完成公用資料夾至 Office 365 群組移轉

您的公用資料夾進行唯讀之後，您需要重新執行移轉。這是必要資料的最終累加複本。您可以執行一次移轉之前，您必須移除現有的批次，您可以執行下列命令：

    Remove-MigrationBatch <name of migration batch>

下一步\] 建立新的批次以相同的.csv 檔案執行下列命令。在此命令：

  - **CsvData**是在上述建立的.csv 檔案*步驟 3： 建立.csv 檔案*。請務必提供此檔案的完整路徑。若檔案已移動有任何原因，請務必確認和使用新的位置。

  - **NotificationEmails**是選擇性的參數可以用來將會收到相關的狀態與進度移轉之通知的電子郵件地址。

  - **自動啟動**為選用參數它會使用時，請建立為啟動遷移批次。

<!-- end list -->

    New-MigrationBatch -Name PublicFolderToGroupMigration -CSVData (Get-Content <path to .csv file> -Encoding Byte) -PublicFolderToUnifiedGroup -SourceEndpoint $PfEndpoint.Identity [-NotificationEmails <email addresses for migration notifications>] [-AutoStart]

建立新的批次之後，請Exchange Online PowerShell中執行下列命令來啟動移轉。請注意此步驟只需要是否`-AutoStart`參數是不在以上的命令。

    Start-MigrationBatch PublicFolderToGroupMigration

完成此步驟 （批次狀態為**\[已完成**） 之後，確認所有的資料有已複製到 Office 365 群組。屆時，您必須是滿意群組經驗，即可開始刪除已移轉的公用資料夾從 Exchange 2013 環境。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>雖然有支援回復移轉及傳回公用資料夾的程序，這不是可能之後已刪除的來源公用資料夾。 請參閱How do I 回復到公用資料夾從 Office 365 群組？如需詳細資訊。</td>
</tr>
</tbody>
</table>


## 已知問題

典型的公用資料夾可以發生下列已知的問題 Office 365 群組移轉。

  - 傳輸 SMTP 位址擁有郵件功能的公用資料夾從 Office 365 群組僅為次要電子郵件將地址的指令碼討論在 Exchange Online。因此，若您的環境中有 Exchange Online Protection (EOP) 或集中式郵件流程設定，就必須將電子郵件傳送至群組 （次要電子郵件地址） 移轉後的問題。

  - 如果.csv 對應檔案具有無效的公用資料夾路徑的項目，而不發生錯誤，遷移批次會顯示為 \[**已完成**並沒有進一步的資料複製。

## 移轉指令碼

供您參考本章節提供深入的三個移轉指令碼和其 Exchange 環境中執行的工作的描述。所有指令碼及支援檔案可以[從下列位置下載](https://www.microsoft.com/en-us/download/details.aspx?id=55985)。

## AddMembersToGroups.ps1

此指令碼會讀取遷移公用資料夾的權限並再新增成員及擁有者至 Office 365 群組，如下所示：

  - 具有下列權限角色的使用者將成員新增至 Office 365 中的群組。 **權限的角色：** 擁有者、 PublishingEditor、 編輯器、 PublishingAuthor、 作者

  - 在 \[除了下列最小的存取權，與上述的使用者權限也會新增成員至 Office 365 中的群組。 **存取權限：** ReadItems、 CreateItems、 FolderVisible、 EditOwnedItems、 DeleteOwnedItems

  - 右作為擁有者群組新增 「 擁有者 」 與其他的合格的存取權限的使用者將會加入為成員的存取權的使用者。

  - 安全性群組不能為成員新增至 Office 365 中的群組。因此他們會展開，且再個別使用者將會加入為成員或擁有者群組依據的存取權的安全性群組。

  - 當使用者在安全性群組中的存取權限一段的公用資料夾的使用權限自行明確透過相同的公用資料夾、 明確權限將會獲得喜好設定。 例如，請考慮安全性群組呼叫"SG1"案例不具 User1 和 User2 的成員。"PF1"的公用資料夾的權限項目如下所示：
    
    在 PF1 SG1： 作者
    
    在 PF1 User1： 擁有者
    
    在此例中使用者 1 將到 Office 365 中的群組新增為擁有者。

  - 要移轉的公用資料夾的 「 預設 」 權限時 'Author' 或超出指令碼將會建議設定相對應群組的隱私權設定為 '公用'。

此指令碼可以執行即使之後的公用資料夾鎖定向下參數設為` $true``ArePublicFoldersLocked` 。在此案例中，指令碼會從檔案鎖定關閉期間建立備份讀取權限。

## LockAndSavePublicFolderProperties.ps1

此指令碼進行遷移的公用資料夾唯讀屬性。擁有郵件功能的公用資料夾已移轉時，他們會先會停用和其 SMTP 位址會新增至 Office 365 中的個別群組。然後，使其唯讀屬性將會修改權限項目。在其上執行任何修改之前，將會複製備份之擁有郵件功能的公用資料夾的郵件屬性時的所有公用資料夾的權限項目。

如果有多個遷移批次，不同的備份目錄應該搭配每個對應.csv 檔案。

將儲存下列信箱內容，以及各自擁有郵件功能的公用資料夾和 Office 365 群組：

  - PrimarySMTPAddress

  - EmailAddresses

  - ExternalEmailAddress

  - EmailAddressPolicyEnabled

  - GrantSendOnBehalfTo

  - SendAs 者清單

上述的郵件內容會儲存在.csv 檔案中，可用於備份程序聯播 (如果想要傳回給使用的公用資料夾，請參閱How do I 回復到公用資料夾從 Office 365 群組？如需詳細資訊)。擁有郵件功能的公用資料夾的內容的快照也會儲存在名 PfMailProperties.csv 的檔案。這個檔案不需要聯播 （英文） back 程序，但仍可用於您參考 （英文）。

下列郵件屬性將會移轉至目標群組鎖定的一部分：

  - PrimarySMTPAddress

  - EmailAddresses

  - SendAs 者清單

  - GrantSendOnBehalfTo

指令碼可確保 PrimarySMTPAddress 和 EmailAddresses 移轉擁有郵件功能的公用資料夾會新增為次要 SMTP 位址的 Office 365 中相對應的群組。此外，SendAs 和 SendOnBehalfTo 權限的使用者擁有郵件功能的公用資料夾上將會獲得相等權限對應的目標群組中。

**允許的存取權限**

只有下列的存取權限允許使用者以確保公用資料夾所做的所有使用者唯讀的。這些都會儲存在**ListOfAccessRightsAllowed**。

  - ReadItems

  - CreateSubfolders

  - FolderContact

  - FolderVisible

會以下列方式修改權限項目：

1.  ###  
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>鎖定之前</th>
    <th>鎖定之後</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>無</p></td>
    <td><p>無</p></td>
    </tr>
    <tr class="even">
    <td><p>AvailabilityOnly</p></td>
    <td><p>AvailabilityOnly</p></td>
    </tr>
    <tr class="odd">
    <td><p>LimitedDetails</p></td>
    <td><p>LimitedDetails</p></td>
    </tr>
    <tr class="even">
    <td><p>投稿人</p></td>
    <td><p>FolderVisible</p></td>
    </tr>
    <tr class="odd">
    <td><p>檢閱者</p></td>
    <td><p>ReadItems, FolderVisible</p></td>
    </tr>
    <tr class="even">
    <td><p>NonEditingAuthor</p></td>
    <td><p>ReadItems, FolderVisible</p></td>
    </tr>
    <tr class="odd">
    <td><p>Aughor</p></td>
    <td><p>ReadItems, FolderVisible</p></td>
    </tr>
    <tr class="even">
    <td><p>編輯器</p></td>
    <td><p>ReadItems, FolderVisible</p></td>
    </tr>
    <tr class="odd">
    <td><p>PublishingAuthor</p></td>
    <td><p>ReadItems, CreateSubfolders, FolderVisible</p></td>
    </tr>
    <tr class="even">
    <td><p>PublishingEditor</p></td>
    <td><p>ReadItems, CreateSubfolders, FolderVisible</p></td>
    </tr>
    <tr class="odd">
    <td><p>擁有者</p></td>
    <td><p>ReadItems, CreateSubfolders, FolderContact, FolderVisible</p></td>
    </tr>
    </tbody>
    </table>


2.  無讀取權限之使用者的存取權限會向左不變，而且它們會繼續要封鎖與讀取權限。

3.  使用自訂角色的使用者，將會移除所有不在**ListOfAccessRightsAllowed**中的存取權。該篩選後的使用者沒有從允許清單的任何存取權，這些使用者的存取權限將設為 「 無 」。

可能的電子郵件時傳送給擁有郵件功能的公用資料夾的間隔時間期間之資料夾的郵件功能停用和其 SMTP 位址已新增至 Office 365 群組中斷。

## UnlockAndRestorePublicFolderProperties.ps1

此指令碼會重新指派回到依據 ＜ back up 檔案鎖定向下採取期間公用資料夾的公用資料夾的權限。此指令碼會也啟用郵件功能之有已停用的公用資料夾、 之後移除 Office 365 中其各自群組的資料夾的 SMTP 位址。此程序期間可能稍微停機時間。

## How do 我回復到公用資料夾從 Office 365 群組？

改變心意而想要使用的公用資料夾之後使用 Office 365 Groups 下, 面所列的命令會還原您的環境的狀態會傳回可行的移轉前與其。聯播 （英文） back 可以執行只要將備份檔案存在於和只要未刪除公用資料夾移轉後。

在 Exchange 2013 伺服器上，執行下列命令。在此命令：

  - **BackupDir**是儲存備份檔案的權限項目、 MEPF 屬性與移轉記錄檔的目錄。請確定您使用相同的位置中所指定*步驟 6： 鎖定剪下移轉至公用資料夾 （需公用資料夾停機）*。

  - **ArePublicFoldersOnPremises**是以指出公用資料夾是否位於內部部署或 Exchange Online 中的參數。

  - **Credential**是 Exchange Online 使用者名稱和密碼。

<!-- end list -->

    .\UnlockAndRestorePublicFolderProperties.ps1 -BackupDir <path to backup directory> -ArePublicFoldersOnPremises $true -Credential (Get-Credential)

請注意任何項目新增至 Office 365\] 群組中或在群組中執行任何編輯作業不複製回您的公用資料夾。因此會有資料遺失，假設新資料已時新增的公用資料夾群組。

請注意，即無法再還原所有的公用資料夾有已遷移這表示應該要還原的公用資料夾的子集。

Office 365 中的對應群組將不會刪除聯播 （英文） 備份程序的一部分。您必須清除或手動刪除這些群組。

