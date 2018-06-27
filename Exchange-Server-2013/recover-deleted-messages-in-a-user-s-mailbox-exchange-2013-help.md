---
title: '復原刪除的郵件使用者的信箱: Exchange Online Help'
TOCTitle: 復原刪除的郵件使用者的信箱
ms:assetid: 9e0e34ce-efc5-454e-8d15-57b4da867f12
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ff660637(v=EXCHG.150)
ms:contentKeyID: 50554039
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 復原刪除的郵件使用者的信箱

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

（此主題適用於Exchange系統管理員的）。

系統管理員可以搜尋並復原已刪除的電子郵件訊息中使用者的信箱。這例如指派給使用者信箱的保留原則包含項目永久刪除 （清除） 的人員 （藉由使用Outlook或Outlook Web App中復原刪除的郵件功能），或自動化程序所刪除的項目。 在下列情況下，無法由使用者復原已清除的項目。 但系統管理員可以使用若尚未到期的項目刪除項目保留期間復原已清除的郵件。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>除了可以使用此程序來搜尋和復原刪除的項目 (在啟用單一項目復原或訴訟保留的情況下，這些項目會被移至 [可復原的項目]\[清除] 資料夾中) 之外，您也可以使用此程序來搜尋信箱內其他資料夾中的項目，並從來源信箱刪除項目 (又稱為「搜尋與摧毀」)。</td>
</tr>
</tbody>
</table>


## 開始之前您必須瞭解的資訊

  - 預估完成時間： 15-30 分鐘。

  - 本主題中的程序需要特定權限。請查看每個程序以取得權限資訊。

  - 要復原的項目會在刪除之前單一項目復原必須啟用信箱。 在Exchange Online、 單一項目復原預設會啟用時建立新的信箱。在Exchange 2013、 單一項目復原已停用信箱建立時。 如需詳細資訊，請參閱[啟用或停用單一項目復原的信箱](enable-or-disable-single-item-recovery-for-a-mailbox-exchange-2013-help.md)。

  - 若要搜尋和復原項目，您必須具備下列資訊：
    
      - **來源信箱**   這是要搜尋的信箱。
    
      - **目標信箱**  這是在其中將復原的郵件的探索信箱。Exchange安裝程式會建立預設探索信箱。在Exchange Online，預設也會建立探索信箱。如有需要，您可以建立其他探索信箱。如需詳細資訊，請參閱[建立探索信箱](create-a-discovery-mailbox-exchange-2013-help.md)。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>當使用<strong>Search-Mailbox</strong>指令程式，您也可以指定不是探索信箱的目標信箱。不過，您無法指定相同的信箱為來源和目標信箱。</td>
        </tr>
        </tbody>
        </table>
    
      - **搜尋準則**   準則包括寄件者或收件者，或郵件中的關鍵字 (字詞或片語)。

  - 此主題著重於使用 PowerShell 復原已刪除的項目在使用者的信箱。您也可以使用 GUI 型就地 eDiscovery 工具找到並已刪除的項目匯出至 PST 檔案。使用者會使用此 PST 檔案還原至其信箱已刪除的郵件。 如需詳細指示，請參閱[復原已刪除的使用者的信箱位管理員說明中的項目](https://go.microsoft.com/fwlink/p/?linkid=722928)。

## （選用）步驟 1： 連線至 Exchange Online 使用遠端 PowerShell

您只須有Exchange Online或Office 365組織執行此步驟。 如果您有Exchange 2013組織移至下一個步驟並Exchange 管理命令介面中執行命令。

1.  在您的本機電腦上開啟 Windows PowerShell 並執行下列命令。
    
        $UserCredential = Get-Credential
    
    在 **\[Windows PowerShell 認證要求\]** 對話方塊中，輸入 Office 365 全域管理員帳戶的使用者名稱和密碼，然後按一下 **\[確定\]**。

2.  執行下列命令。
    
        $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $UserCredential -Authentication Basic -AllowRedirection

3.  執行下列命令。
    
        Import-PSSession $Session

4.  若要確認您要連線至Exchange Online組織，請執行下列命令以取得組織中的所有信箱的清單。
    
        Get-Mailbox

如需詳細資訊或如果您有連線至Exchange Online組織的問題，請參閱 ＜ [Connect to Exchange Online 使用遠端 PowerShell](https://go.microsoft.com/fwlink/p/?linkid=517283)。

## 步驟 2： 搜尋並復原遺失的項目

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「就地 eDiscovery」項目。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您可以使用 Exchange 系統管理中心 (EAC) 中的就地 eDiscovery 搜尋遺失的項目。不過，當使用 EAC 中，您不能限制搜尋可復原的項目] 資料夾。即使他們不會刪除將會傳回郵件符合您的搜尋參數。他們復原到指定的探索信箱後，您可能需要檢閱搜尋結果，並移除不必要的訊息之前剩餘的郵件至使用者信箱的復原或匯出至.pst 檔案。<br />
如需有關如何使用 EAC 以執行就地復原搜尋的詳細資料，請參閱 <a href="create-an-in-place-ediscovery-search-exchange-2013-help.md">建立就地 eDiscovery 搜尋</a>。</td>
</tr>
</tbody>
</table>


在復原過程中的第一個步驟是搜尋中來源信箱的郵件。使用下列方法之一來搜尋使用者信箱，並將郵件複製到探索信箱。

此範例會在 April Stewart 的信箱中搜尋符合下列準則的郵件：

  - 寄件者︰ Ken Kwok

  - 關鍵字： Seattle

<!-- end list -->

    Search-Mailbox "April Stewart" -SearchQuery "from:'Ken Kwok' AND seattle" -TargetMailbox "Discovery Search Mailbox" -TargetFolder "April Stewart Recovery" -LogLevel Full

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用時<strong>Search-Mailbox</strong>指令程式，您可使用<em>SearchQuery</em>參數來指定使用關鍵字查詢語言 (KQL) 格式化的查詢範圍搜尋。您也可以使用<em>SearchDumpsterOnly</em>參數來搜尋只有項目可復原的項目] 資料夾中。</td>
</tr>
</tbody>
</table>


如需詳細的語法及參數資訊，請參閱 [Search-Mailbox](https://technet.microsoft.com/zh-tw/library/dd298173\(v=exchg.150\))。

**如何才能了解這是否正常運作？**

若要驗證您已經成功搜尋到您想要復原的訊息，登入您選為目標信箱的探索信箱並檢閱搜尋結果。

## 步驟 3： 如何還原已復原的項目

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「就地 eDiscovery」項目。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您無法使用 EAC 以還原復原項目。</td>
</tr>
</tbody>
</table>


郵件已復原到探索信箱後，您可以還原至使用者的信箱使用**Search-Mailbox**指令程式。在Exchange 2013，您也可以使用**New-MailboxExportRequest**及**New-MailboxImportRequest**指令程式來匯出至訊息或匯入訊息從.pst 檔案。

## 使用命令介面還原郵件

以下範例將郵件還原至 April Stewart 的信箱，並將這些郵件從探索搜尋信箱中刪除。

    Search-Mailbox "Discovery Search Mailbox" -SearchQuery "from:'Ken Kwok' AND seattle" -TargetMailbox "April Stewart" -TargetFolder "Recovered Messages" -LogLevel Full -DeleteContent

如需詳細的語法及參數資訊，請參閱 [Search-Mailbox](https://technet.microsoft.com/zh-tw/library/dd298173\(v=exchg.150\))。

**如何才能了解這是否正常運作？**

若要驗證您已經成功將訊息復原至使用者信箱，將您在目標資料夾中指定的使用者檢閱訊息放進上述指令中。

## (Exchange 2013)使用命令介面匯出及匯入訊息從.pst 檔案

Exchange 2013，在您可以從信箱的內容匯出至.pst 檔案和.pst 檔案的內容匯入至信箱。若要深入了解信箱匯入與匯出，請參閱[信箱匯入及匯出要求](mailbox-import-and-export-requests-exchange-2013-help.md)。您無法在Exchange Online執行這項工作。

此範例使用下列設定將郵件從探索搜尋信箱的 \[April Stewart Recovery\] 資料夾中匯出至 .pst 檔案。

  - **信箱**   探索搜尋信箱

  - **來源資料夾**   April Stewart Recovery

  - **ContentFilter**   四月旅行計畫

  - **PST 檔案路徑**   \\\\MYSERVER\\HelpDeskPst\\AprilStewartRecovery.pst

<!-- end list -->

    New-MailboxExportRequest -Mailbox "Discovery Search Mailbox" -SourceRootFolder "April Stewart Recovery" -ContentFilter {Subject -eq "April travel plans"} -FilePath \\MYSERVER\HelpDeskPst\AprilStewartRecovery.pst

如需詳細的語法及參數資訊，請參閱 [New-MailboxExportRequest](https://technet.microsoft.com/zh-tw/library/ff607299\(v=exchg.150\))。

此範例使用下列設定將郵件從 .pst 檔案匯入至 April Stewart 信箱中的 \[Recovered By Helpdesk\] 資料夾中。

  - **信箱**   April Stewart

  - **目標資料夾**   Recovered By Helpdesk

  - **PST 檔案路徑**   \\\\MYSERVER\\HelpDeskPst\\AprilStewartRecovery.pst

<!-- end list -->

    New-MailboxImportRequest -Mailbox "April Stewart" -TargetRootFolder "Recovered By Helpdesk" -FilePath \\MYSERVER\HelpDeskPst\AprilStewartRecovery.pst 

如需詳細的語法及參數資訊，請參閱 [New-MailboxImportRequest](https://technet.microsoft.com/zh-tw/library/ff607310\(v=exchg.150\))。

**如何才能了解這是否正常運作？**

若要確認您已成功匯出的郵件的.pst 檔案，請使用Outlook開啟的.pst 檔案並檢查其內容。若要確認您已成功匯入的郵件從.pst 檔案，也請使用者檢查您在上述命令中指定的目標資料夾的內容。

## 其他資訊

  - 能夠復原已刪除的項目會啟用*單一項目復原*，可讓管理員復原一則訊息，已將清除由使用者或保留原則已刪除的項目保留期間尚未過期的項目如下。若要深入了解單一項目復原，請參閱[可復原的項目資料夾](recoverable-items-folder-exchange-2013-help.md)。

  - Exchange Online信箱會依預設設定為 14 天內，保留已刪除的項目。您可以變更此設定最大值為 30 天。 在Exchange 2013、 信箱資料庫被設定為 14 天內，保留已刪除的項目預設。您可以設定信箱或信箱資料庫刪除項目保留設定。如需詳細資訊，請參閱：
    
      - [Exchange Online 信箱之保留時間變更多久永久刪除項目](https://technet.microsoft.com/zh-tw/library/dn163584\(v=exchg.150\))
    
      - [設定已刪除的項目保留及可復原的項目配額](configure-deleted-item-retention-and-recoverable-items-quotas-exchange-2013-help.md)

  - 如先前所述，您也可以使用就地 eDiscovery 工具找到並已刪除的項目匯出至 PST 檔案。使用者會使用此 PST 檔案還原至其信箱已刪除的郵件。 如需詳細指示，請參閱[復原已刪除的使用者的信箱位管理員說明中的項目](https://go.microsoft.com/fwlink/p/?linkid=722928)。

  - 如果尚未被清除，如果尚未過期的項目已刪除的項目保留期間的使用者可以復原刪除的項目。如果使用者需要從可復原項目資料夾中復原刪除的項目，請將其指向下列主題：
    
      - [復原已刪除的 Outlook 2010 中的項目](https://go.microsoft.com/fwlink/p/?linkid=524923)
    
      - [復原已刪除的在 Outlook 2013 中的項目](https://go.microsoft.com/fwlink/p/?linkid=624829)
    
      - [復原刪除的項目或 Outlook Web App 中的電子郵件](https://go.microsoft.com/fwlink/p/?linkid=524924)

  - 本主題顯示如何使用**Search-Mailbox**指令程式來搜尋並復原遺失的項目。如果您使用此指令程式，可以同時搜尋只有一個信箱。如果您想要同時搜尋多個信箱，您就可以使用[就地 eDiscovery](in-place-ediscovery-exchange-2013-help.md)在 Exchange 系統管理中心 (EAC) 或在Windows PowerShell[New-MailboxSearch](https://technet.microsoft.com/zh-tw/library/dd298064\(v=exchg.150\))指令程式。

  - 除了使用此程序可搜尋並復原已刪除的項目，您也可以使用類似的程序來搜尋使用者信箱中的項目並再從來源信箱刪除這些項目。如需詳細資訊，請參閱[搜尋並刪除郵件 - 管理中心說明](search-for-and-delete-messages-admin-help-exchange-2013-help.md)。

