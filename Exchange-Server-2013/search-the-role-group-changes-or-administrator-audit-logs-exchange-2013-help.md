---
title: '搜尋角色群組變更或管理員稽核記錄檔: Exchange Online Help'
TOCTitle: 搜尋角色群組變更或管理員稽核記錄檔
ms:assetid: c7188d53-e672-492b-b57d-cd711379ddb3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ff459262(v=EXCHG.150)
ms:contentKeyID: 50553890
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 搜尋角色群組變更或管理員稽核記錄檔

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2013-12-02_

您可以搜尋系統管理員稽核記錄，以查明是誰變更組織、伺服器和收件者組態。在嘗試追蹤意外行為的原因時，這有助於識別惡意的系統管理員，或驗證是否符合規範需求。如需有關系統管理員稽核記錄的詳細資訊，請參閱[系統管理員稽核記錄](administrator-audit-logging-exchange-2013-help.md)。

如果您要搜尋信箱稽核記錄，請參閱[信箱稽核記錄](mailbox-audit-logging-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在 Exchange Online 中，您可以使用 EAC 來檢視系統管理員稽核記錄中的項目。如需詳細資訊，請參閱 <a href="view-the-administrator-audit-log-exchange-2013-help.md">檢視系統管理員稽核記錄</a>。</td>
</tr>
</tbody>
</table>


## 開始之前有哪些須知？

  - 每項程序的預估完成時間：不到 5 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [Exchange 及命令介面基礎結構權限](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)主題中的「僅檢視系統管理員稽核記錄」項目。

  - 系統管理員稽核記錄依預設已啟用。若要驗證是否已將其啟用，請執行下列命令：
    
        Get-AdminAuditLogConfig | FL AdminAuditLogEnabled
    
    `True` 值表示已啟用系統管理員稽核記錄。`False` 值表示已停用。如果您需要啟用內部部署 Exchange 組織的系統管理員稽核記錄，請執行下列命令：
    
        Set-AdminAuditLogConfig -AdminAuditLogEnabled $true
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><strong>Set-AdminAuditLogConfig</strong> Cmdlet 不適用於 Exchange Online。</td>
    </tr>
    </tbody>
    </table>
    
    如需詳細資訊，請參閱 [管理系統管理員稽核記錄](manage-administrator-audit-logging-exchange-2013-help.md)。

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


## 您要執行的工作

## 使用 EAC 執行管理角色群組變更報告

如果您想要了解組織中角色群組的管理角色群組成員資格有何變更，您可以在 Exchange 系統管理中心 (EAC) 中使用「系統管理員角色群組」報告。您可以使用「系統管理員角色群組」報告來檢視指定日期範圍內已變更的角色群組清單。您也可以選取想要檢視變更的特定角色群組。

1.  在 EAC 中，選取 \[相符性管理\] \> \[稽核\]，然後按一下 \[執行系統管理員角色群組報告\]。

2.  使用 \[開始日期\] 和 \[結束日期\] 欄位來選取日期範圍。

3.  按一下 \[選取角色群組\]，然後選取您要顯示變更的角色群組，或者將此欄位留白以搜尋所有角色群組中的變更。

4.  按一下 \[搜尋\]。

如果使用您指定的準則找到任何變更，結果窗格中會顯示變更清單。按一下角色群組會在詳細資料窗格中顯示角色群組的變更。

## 使用 EAC 匯出系統管理員稽核記錄

如果您要建立 XML 檔案，其中包含組織的變更，您可以在 ECP 中使用 \[匯出系統管理員稽核記錄\] 報告。您可以使用 \[匯出系統管理員稽核記錄\] 報告來指定日期範圍，以搜尋包含您指定之使用者所做變更的稽核記錄項目。然後，XML 檔案會以電子郵件附件形式傳送給收件者。XML 檔案的大小上限為 10 MB。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>根據預設，Outlook Web App 不允許您在開啟 XML 附件。您可以設定 Exchange 以允許使用 Outlook Web App 檢視 XML 附件，或是使用其他電子郵件用戶端 (如 Microsoft Outlook) 來檢視附件。如需如何設定 Outlook Web App 以允許檢視 XML 附件的相關資訊，請參閱<a href="view-or-configure-outlook-web-app-virtual-directories-exchange-2013-help.md">檢視或設定 Outlook Web App 虛擬目錄</a>。</td>
</tr>
</tbody>
</table>


1.  在 EAC 中，選取 \[相符性管理\] \> \[稽核\]，然後按一下 \[匯出系統管理員稽核記錄\]。

2.  使用 \[開始日期\] 和 \[結束日期\] 欄位來選取日期範圍。

3.  在 \[傳送稽核報告給\] 欄位中，按一下 \[選取使用者\]，然後選取您要傳送報告給他的收件者。

4.  按一下 \[匯出\]。

如果使用您指定的準則找到任何記錄項目，將會建立 XML 檔案，並以電子郵件附件形式傳送給您指定的收件者。

## 使用命令介面來搜尋稽核記錄項目

您可以使用命令介面來搜尋符合指定準則的稽核記錄項目。如需搜尋準則的清單，請參閱[系統管理員稽核記錄](administrator-audit-logging-exchange-2013-help.md)。此程序使用 **Search-AdminAuditLog** 指令程式並在命令介面中顯示搜尋結果。當您需要傳回的一組結果超過 **New-AdminAuditLogSearch** Cmdlet 或 EAC「稽核報告」報告中所定義的限制時，就可以使用這個 Cmdlet。

如果您要以電子郵件附件形式將稽核記錄搜尋結果傳送給收件者，請參閱本主題稍後的Use the Shell to search for audit log entries and send results to a recipient。

若要搜尋指定準則的稽核記錄，請使用下列語法。

    Search-AdminAuditLog - Cmdlets <cmdlet 1, cmdlet 2, ...> -Parameters <parameter 1, parameter 2, ...> -StartDate <start date> -EndDate <end date> -UserIds <user IDs> -ObjectIds <object IDs> -IsSuccess <$True | $False >

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>根據預設，<strong>Search-AdminAuditLog</strong> 指令程式最多會傳回 1,000 個記錄項目。請使用 <em>ResultSize</em> 參數指定最多 250,000 個記錄檔項目。或者，使用 <code>Unlimited</code> 值傳回所有項目。</td>
</tr>
</tbody>
</table>


此範例使用下列準則，執行所有稽核記錄項目的搜尋：

  - **開始日期**   2012/8/4

  - **結束日期**   2012/10/3

  - **使用者識別碼**   davids、chrisd、kima

  - **Cmdlets**   **Set-Mailbox**

  - **參數**   *ProhibitSendQuota*、*ProhibitSendReceiveQuota*、*IssueWarningQuota*、*MaxSendSize*、*MaxReceiveSize*

<!-- end list -->

    Search-AdminAuditLog -Cmdlets Set-Mailbox -Parameters ProhibitSendQuota, ProhibitSendReceiveQuota, IssueWarningQuota, MaxSendSize, MaxReceiveSize -StartDate 08/04/2012 -EndDate 10/03/2012 -UserIds davids, chrisd, kima

此範例搜尋特定信箱的變更。如果您在進行疑難排解或需要提供調查的資訊，這會很有用。使用下列準則：

  - **開始日期**   2012/5/1

  - **結束日期**   2012/10/3

  - **物件識別碼**   contoso.com/Users/DavidS

<!-- end list -->

    Search-AdminAuditLog -StartDate 05/01/2012 -EndDate 10/03/2012 -ObjectID contoso.com/Users/DavidS

如果搜尋傳回許多記錄項目，建議您使用本主題稍後的Use the Shell to search for audit log entries and send results to a recipient中提供的程序。該章節中的程序會以電子郵件附件形式將 XML 檔案傳送給您指定的收件者，讓您更輕鬆擷取感興趣的資料。

如需詳細的語法及參數資訊，請參閱 [Search-AdminAuditLog](https://technet.microsoft.com/zh-tw/library/ff459250\(v=exchg.150\))。

## 檢視稽核記錄項目的詳細資料

**Search-AdminAuditLog** Cmdlet 會傳回[系統管理員稽核記錄](administrator-audit-logging-exchange-2013-help.md)的「稽核記錄內容」一節所描述的欄位。在此指令程式傳回的欄位中，**CmdletParameters** 和 **ModifiedProperties** 兩個欄位包含依預設無法檢視的其他資訊。

若要檢視 **CmdletParameters** 和 **ModifiedProperties** 欄位的內容，請使用下列步驟。或者，您可以使用本主題稍後的Use the Shell to search for audit log entries and send results to a recipient中的程序來建立 XML 檔案。

此程序採用下列概念：

  - [陣列](https://technet.microsoft.com/zh-tw/library/aa998267\(v=exchg.150\))

  - [使用者定義的變數](https://technet.microsoft.com/zh-tw/library/bb123690\(v=exchg.150\))

<!-- end list -->

1.  決定您要搜尋的準則、執行 **Search-AdminAuditLog** 指令程式，然後使用下列命令將結果儲存在變數中。
    
        $Results = Search-AdminAuditLog <search criteria>

2.  每一個稽核記錄項目都儲存為變數 `$Results` 中的陣列元素。您可以指定陣列項目索引來選取陣列元素。陣列元素索引從零 (0) 開始，表示第一個陣列元素。例如，若要擷取第 5 個陣列元素，其索引為 4，請使用下列命令。
    
        $Results[4]

3.  上一個命令會傳回儲存在陣列元素 4 中的記錄項目。若要查看此記錄項目的 **CmdletParameters** 和 **ModifiedProperties** 欄位的內容，請使用下列命令。
    
        $Results[4].CmdletParameters
        $Results[4].ModifiedProperties

4.  若要檢視另一個記錄項目的 **CmdletParameters** 或 **ModifiedParameters** 欄位，請變更陣列元素索引。

## 使用命令介面搜尋稽核記錄項目並將結果傳送給收件者

您可以使用命令介面來搜尋符合指定準則的稽核記錄項目，然後以 XML 檔案附件形式將這些結果傳送給您指定的收件者。結果會在 15 分鐘內傳送給收件者。如需搜尋準則的清單，請參閱[系統管理員稽核記錄](administrator-audit-logging-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>根據預設，Outlook Web App 不允許您在開啟 XML 附件。您可以設定 Exchange 以允許使用 Outlook Web App 檢視 XML 附件，或是使用其他電子郵件用戶端 (如 Microsoft Outlook) 來檢視附件。如需如何設定 Outlook Web App 以允許檢視 XML 附件的相關資訊，請參閱<a href="view-or-configure-outlook-web-app-virtual-directories-exchange-2013-help.md">檢視或設定 Outlook Web App 虛擬目錄</a>。</td>
</tr>
</tbody>
</table>


若要搜尋指定準則的稽核記錄，請使用下列語法。

    New-AdminAuditLogSearch -Cmdlets <cmdlet 1, cmdlet 2, ...> -Parameters <parameter 1, parameter 2, ...> -StartDate <start date> -EndDate <end date> -UserIds <user IDs> -ObjectIds <object IDs> -IsSuccess <$True | $False > -StatusMailRecipients <recipient 1, recipient 2, ...> -Name <string to include in subject>

此範例使用下列準則，執行所有稽核記錄項目的搜尋：

  - **開始日期**   2012/8/4

  - **結束日期**   2012/10/3

  - **使用者識別碼**   davids、chrisd、kima

  - **Cmdlets**   **Set-Mailbox**

  - **參數**   *ProhibitSendQuota*、*ProhibitSendReceiveQuota*、*IssueWarningQuota*、*MaxSendSize*、*MaxReceiveSize*

此命令會將結果傳送至 davids@contoso.com SMTP 位址，郵件主旨行包含 "Mailbox limit changes"。

    New-AdminAuditLogSearch -Cmdlets Set-Mailbox -Parameters ProhibitSendQuota, ProhibitSendReceiveQuota, IssueWarningQuota, MaxSendSize, MaxReceiveSize -StartDate 08/04/2012 -EndDate 10/03/2012 -UserIds davids, chrisd, kima -StatusMailRecipients davids@contoso.com -Name "Mailbox limit changes"

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>New-AdminAuditLogSearch</strong> 指令程式產生的報告以 10 MB 為大小上限。如果您執行的搜尋傳回大於 10 MB 的報告，請變更您指定的搜尋準則。例如，縮小日期範圍並執行多個報告，各報告為原始日期範圍的一部分。</td>
</tr>
</tbody>
</table>


如需 XML 檔案格式的相關資訊，請參閱[系統管理員稽核記錄檔結構](administrator-audit-log-structure-exchange-2013-help.md)。

如需詳細的語法及參數資訊，請參閱 [New-AdminAuditLogSearch](https://technet.microsoft.com/zh-tw/library/ff459243\(v=exchg.150\))。

