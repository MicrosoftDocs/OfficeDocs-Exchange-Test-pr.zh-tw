---
title: 'Exchange 稽核報告: Exchange Online Help'
TOCTitle: Exchange 稽核報告
ms:assetid: 2b3e1529-1677-4564-be0b-ce22757ddc0d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ150497(v=EXCHG.150)
ms:contentKeyID: 50472299
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 稽核報告

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

您可以使用稽核記錄來追蹤系統管理員所做的特定變更，藉以疑難排解組態問題，以及協助您符合法規、規範符合性和訴訟需求。Microsoft Exchange 提供了兩種稽核記錄：

  - *系統管理員稽核記錄*會記錄任何根據 \[Exchange 管理命令介面指令程式，由管理員執行的動作。這可協助您疑難排解設定問題或識別與安全性或規範相關問題的原因。在Exchange Online、 動作執行 Microsoft 系統管理員和委派管理員，也記錄。

  - *信箱稽核記錄*記錄由系統管理員、 委派的使用者或擁有信箱的人存取信箱時。這可協助您決定誰存取過信箱和其已完成。

本主題將說明下列事項：

  - Export audit logs

  - Run auditing reports

  - Configure audit logging
    
      - Enable mailbox audit logging
    
      - Give users access to auditing reports
    
      - Configure Outlook Web App to allow XML attachments

## 匯出稽核記錄

\[**相符性管理**\>**稽核**\] 頁面上的 Exchange 系統管理中心 (EAC) 中，您可以搜尋並匯出項目從管理員稽核記錄和信箱稽核記錄。

  - **匯出系統管理員稽核記錄**  命令介面 cmdlet 為基礎且不會開頭的動詞**Get**、 **Search**或**Test**管理員執行任何動作會記錄在系統管理員稽核記錄。稽核記錄項目包含已執行，請使用此指令程式，以及時的作業已成功使用的值與參數指令程式。您可以搜尋並匯出系統管理員稽核記錄項目。當您匯出搜尋結果時，Microsoft Exchange 將它們儲存在 XML 檔案並將其附加至電子郵件訊息。如需詳細資訊，請參閱：
    
      - [搜尋角色群組變更或管理員稽核記錄檔](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md)
    
      - [檢視和匯出外部管理員稽核記錄](https://technet.microsoft.com/zh-tw/library/dn505728\(v=exchg.150\))
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>根據預設，管理員稽核記錄項目會保留期為 90 天。超過 90 天的項目時，會將它刪除。雲端架構組織中無法變更此設定。不過，就可以變更在內部部署 Exchange 組織中使用<strong>Set-AdminAuditLog</strong>指令程式。</td>
    </tr>
    </tbody>
    </table>


  - **匯出信箱稽核記錄**  信箱稽核時為信箱啟用記錄、 Microsoft Exchange 儲存動作所非擁有者信箱正在稽核中隱藏資料夾中儲存信箱稽核記錄檔中執行信箱資料的記錄。信箱稽核記錄也可以設定記錄擁有者動作。此記錄檔中的項目指出誰存取信箱以及何時、 執行動作，以及動作是否成功。中搜尋項目中的信箱稽核記錄和匯出其搜尋結果中的 XML 檔案及將它附加至電子郵件訊息的 Microsoft Exchange 儲存。如需詳細資訊，請參閱[匯出信箱稽核記錄](export-mailbox-audit-logs-exchange-2013-help.md)。

## 執行稽核報告

當您在 EAC 中的 \[**稽核**\] 頁面上執行任何下列報告時，結果會顯示在報告的詳細資料窗格中。

  - **執行非擁有者信箱存取報告**  使用這份報告找出已經由擁有信箱的人以外的某人來存取信箱。如需詳細資訊，請參閱[執行非擁有者信箱存取報告](run-a-non-owner-mailbox-access-report-exchange-online-help.md)。

  - **執行系統管理員角色群組報告**   使用這個報告將搜尋對於系統管理員角色群組所做的變更。如需詳細資訊，請參閱[搜尋角色群組變更或管理員稽核記錄檔](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md)。

  - **執行就地探索和保留報告**   使用這個報告可找出在就地保留中放入或移除的信箱。如需相關資訊，請參閱：
    
      - [就地保留與訴訟暫止](in-place-hold-and-litigation-hold-exchange-2013-help.md)
    
      - [就地 eDiscovery](in-place-ediscovery-exchange-2013-help.md)

  - **執行個別信箱訴訟資料暫留報告**  使用這份報告可以找出被放入或移除訴訟暫止的信箱。如需詳細資訊。
    
      - [執行個別信箱訴訟資料暫留報告](run-a-per-mailbox-litigation-hold-report-exchange-2013-help.md)
    
      - [將信箱設為訴訟暫止](place-a-mailbox-on-litigation-hold-exchange-2013-help.md)

  - **執行管理員稽核記錄報告**  使用這份報告可以檢視系統管理員稽核記錄項目。而不是匯出系統管理員稽核記錄，可能需要 24 小時的時間來接收電子郵件訊息中，您可以在 EAC 中執行這份報告。這份報告的記錄設定在組織中的系統管理員所做的變更。達 5000 項目將會顯示在多個頁面上。若要縮小搜尋，您可以指定日期範圍。如需詳細資訊，請參閱：
    
      - [檢視系統管理員稽核記錄](view-the-administrator-audit-log-exchange-2013-help.md)
    
      - [系統管理員稽核記錄](administrator-audit-logging-exchange-2013-help.md)

  - **執行外部系統稽核記錄報告**  這份報告只有Exchange Online和Exchange Online Protection中。Microsoft 系統管理員所執行的動作或委派的管理員已登入系統管理員稽核記錄。使用外部系統的稽核記錄報告搜尋及檢視您組織外部的系統管理員在 Exchange Online 組織的組態執行的動作。如需詳細資訊，請參閱[檢視和匯出外部管理員稽核記錄](https://technet.microsoft.com/zh-tw/library/dn505728\(v=exchg.150\))。

## 設定稽核記錄

您必須先設定組織的稽核記錄，然後才能執行稽核報告和匯出稽核記錄。

## 啟用信箱稽核記錄

您必須針對想要執行非擁有者信箱存取報告的每個信箱啟用信箱稽核記錄。如果未針對信箱啟用信箱稽核記錄，當您執行報告或是匯出信箱稽核記錄時，就不會得到任何結果。

若要針對單一信箱啟用信箱稽核記錄，請執行下列命令介面中的指令：

    Set-Mailbox <Identity> -AuditEnabled $true

若要針對組織內的所有使用者信箱啟用信箱稽核，請執行下列命令。

    $UserMailboxes = Get-mailbox -Filter {(RecipientTypeDetails -eq 'UserMailbox')}
    $UserMailboxes | ForEach {Set-Mailbox $_.Identity -AuditEnabled $true}

如需設定會記錄的動作的詳細資訊，請參閱：

  - **Exchange 2013**    [啟用或停用信箱稽核記錄功能信箱](enable-or-disable-mailbox-audit-logging-for-a-mailbox-exchange-2013-help.md)

  - **Exchange Online**    [啟用信箱稽核 Office 365 中](https://go.microsoft.com/fwlink/p/?linkid=626109)

## 讓使用者能夠存取稽核報告

根據預設，系統管理員可以在 EAC 的 \[稽核\] 頁面上存取並執行任何報告。不過，其他使用者 (例如記錄管理員或法律人員) 則必須被指派必要的權限。

授與使用者存取最簡單的方法是將它們新增至記錄管理角色群組。您也可以使用命令介面來授與使用者存取 EAC 中的 \[**稽核**\] 頁面來將 「 稽核記錄 」 角色指派給使用者。

## 將使用者新增至記錄管理角色群組

1.  前往 **\[權限\]** \> **\[管理員角色\]**。

2.  在角色群組的清單中，按一下 \[記錄管理\]，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[成員\]底下，按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

4.  在 \[選取成員\] 對話方塊中，選取使用者。您可以輸入完整或部分顯示名稱，然後按一下 \[搜尋\]![搜尋圖示](images/Dn624163.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "搜尋圖示")，藉此搜尋使用者。您也可以透過按一下 \[名稱\] 或 \[顯示名稱\] 欄位標題來排序清單。

5.  按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")，然後按一下 \[確定\]，返回角色群組頁面。

6.  按一下 \[儲存\]，將變更儲存到角色群組。

在 \[詳細資料\] 窗格中，使用者已列在 \[成員\] 底下，而且可以存取 EAC 中的 \[稽核\] 頁面、執行稽核報告和匯出稽核記錄。

## 將稽核記錄角色指派給使用者

若要將「稽核記錄」角色指派給使用者，請執行下列命令。

    New-ManagementRoleAssignment -Role "Audit Logs" -User <Identity>

此動作可讓使用者選擇 EAC 中的 \[規範管理\] \> \[稽核\] 以執行任何報告。使用者也可以匯出信箱稽核記錄，並匯出和檢視系統管理員稽核記錄。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>注意：若要允許使用者執行稽核報告，但不允許匯出稽核記錄，請使用前一個命令來指派「僅檢視稽核記錄」角色。</td>
</tr>
</tbody>
</table>


## 設定 Outlook Web App 允許 XML 附件

當您匯出信箱稽核記錄或系統管理員稽核記錄時，Microsoft Exchange 會將稽核記錄 (也就是 XML 檔案) 附加到電子郵件。不過，Outlook Web App 預設會封鎖 XML 附件。若您想要使用 Outlook Web App 來存取這些稽核記錄，需將 Outlook Web App 設定為允許 XML 附件。

執行下列命令，在 Outlook Web App 中允許 XML 附件。

    Set-OwaMailboxPolicy -Identity Default -AllowedFileTypes '.rpmsg','.xlsx','.xlsm','.xlsb','.tiff','.pptx','.pptm','.ppsx','.ppsm','.docx','.docm','.zip','.xls','.wmv','.wma','.wav','.vsd','.txt','.tif','.rtf','.pub','.ppt','.png','.pdf','.one','.mp3','.jpg','.gif','.doc','.bmp','.avi','.xml'

