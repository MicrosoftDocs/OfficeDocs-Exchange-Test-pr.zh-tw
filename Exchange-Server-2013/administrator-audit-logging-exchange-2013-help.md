---
title: '系統管理員稽核記錄: Exchange 2013 Help'
TOCTitle: 系統管理員稽核記錄
ms:assetid: 22b17eb8-d8ee-4599-b202-d6a7928c20d9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd335144(v=EXCHG.150)
ms:contentKeyID: 50553950
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 系統管理員稽核記錄

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2018-03-05_

您可以使用系統管理員稽核記錄中 Microsoft Exchange Server 2013至使用者或管理員在組織中，進行變更時登入。依保持所做的變更記錄檔，您可以追蹤變更、 已實作增強詳細記錄的變更與您變更記錄、 符合法規需求並徵求探索與其他人的變更。

根據預設，新安裝的 Exchange 2013 會啟用稽核記錄。

**目錄**

What gets audited

Audit logging configuration

Audit logs

Manual audit log entries

Active Directory replication

Admin Audit Log agent

## 稽核內容

您可以直接在Exchange管理命令介面中執行的指令程式稽核。此外，使用 Exchange 系統管理中心 (EAC) 執行的作業也會記錄因為這些作業在背景執行 cmdlet。

指令程式，不論執行之所在稽核如果指令程式在稽核清單和一個指令程式，或該指令程式上的多個參數的參數稽核清單上。稽核記錄用來顯示已修改Exchange組織中的物件採取的動作而不是已檢視哪些物件。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果此 cmdlet 會呼叫管理員稽核記錄指令程式延伸代理程式之前會發生錯誤可能不會記錄指令程式。如果呼叫管理員稽核記錄代理程式之後會發生錯誤，指令程式會記錄以及相關聯的錯誤。如需詳細資訊，請參閱本主題稍後的管理員稽核記錄代理程式一節。<br />
系統會記錄使用 Microsoft Exchange Server 2010 管理工具進行的變更，不過，使用 Microsoft Exchange Server 2007 管理工具所進行的變更則不會記錄。<br />
稽核記錄檔設定的變更會重新整理已進行組態變更次開啟命令介面的電腦上每隔 60 分鐘。如果您想要套用所做的變更立即、 關閉，然後開啟 [命令介面中的每部電腦上一次。<br />
命令可能會需要最多 15 分鐘後會出現在稽核記錄搜尋結果中執行。這是因為之前可搜尋稽核記錄項目必須編製索引。如果命令不會出現在系統管理員稽核記錄，請稍候幾分鐘然後重新執行搜尋。</td>
</tr>
</tbody>
</table>


## 稽核記錄設定

根據預設，如果啟用稽核記錄的記錄項目建立每次執行任何指令程式。如果您不想以稽核在執行的每個指令程式，您可以設定稽核記錄稽核只有 cmdlet 和您感興趣的參數。您可以設定稽核記錄功能與**Set-AdminAuditLogConfig**指令程式。下列各節中所參照的參數會搭配這個指令程式。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>不論受稽核的指令程式清單中是否包含 <strong>Set-AdministratorAuditLog</strong> 指令程式，且不論稽核記錄是否啟用或停用，對管理員稽核記錄組態所做的變更會一律予以記錄。</td>
</tr>
</tbody>
</table>


執行命令時， Exchange會檢查所用的 cmdlet。如果已執行此指令程式符合任何*AdminAuditLogConfigCmdlets*參數所提供的 cmdlet， Exchange接著會檢查*AdminAuditLogConfigParameters*參數中指定的參數。如果 \[參數\] 清單中的至少一或多個參數的比對， Exchange記錄檔中使用*AdminAuditLogMailbox*參數所指定的信箱已執行此指令程式。下列各節包含稽核記錄組態的各方面的詳細資訊。

如需管理稽核記錄設定的詳細資訊，請參閱[管理系統管理員稽核記錄](manage-administrator-audit-logging-exchange-2013-help.md)。

回到頁首

## 指令程式

您可以控制哪些 cmdlet 稽核所提供的指令程式，以及其參數，您想要記錄的清單。當您設定稽核記錄時，您可以指定以稽核在每個指令程式，或您可以指定您想要使用*AdminAuditLogConfigCmdlets*參數稽核的 cmdlet。您可以指定完整的 cmdlet 名稱，例如**New-Mailbox**，或者您可以指定部分的 cmdlet 名稱以及之類的萬用字元，星號 (`*`) 括住這些名稱。例如，如果您想要記錄包含字串`Transport`任何指令程式執行時，您可以指定`*Transport*`的值。您可用於混合的完整指令程式名稱及部分指令程式名稱，同時針對稽核記錄設定至您的需求，量身設定。

## 參數

除了指定您想要記錄的 cmdlet，您也可以指示指令程式只是否指令程式上的特定參數都使用記錄。使用*AdminAuditLogConfigParameters*參數指定應記錄的參數。為使用 cmdlet，您可以指定完整的參數名稱，例如`Database`或部分的參數名稱括住萬用字元 (`*`)，例如`*Address*`或兩者的組合。

## 稽核記錄檔保留限制

根據預設，稽核記錄設定為 90 天儲存稽核記錄項目。90 天後刪除稽核記錄項目。您可以變更稽核記錄保留限制使用*AdminAuditLogAgeLimit*參數。您可以指定天數、 小時、 分鐘和稽核的記錄項目應保留的秒的數。若要指定一個值，請使用格式`dd.hh:mm:ss`出下列適用於：

  - **dd**   保留稽核記錄項目的天數。

  - **hh**   保留稽核記錄項目的時數。

  - **mm**   保留稽核記錄項目的分鐘數。

  - **ss**   保留稽核記錄項目的秒數。

您必須指定多個 years 使用`dd` \] 欄位。例如，365 天等於一年以上;730 天等於兩個年度;913 天等於兩年六個月。例如，將稽核記錄保留限制設定為兩個 years 六個月，使用語法`913.00:00:00`。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您可以將稽核記錄保留限制設為小於比目前保留天數的值。如果您這樣做，會刪除其存留期超過新保留天數任何稽核記錄項目。<br />
如果您將保留限制設為 0，則 Exchange 會刪除稽核記錄中的所有項目。<br />
建議您僅將設定稽核記錄保留限制的權限授予您非常信任的使用者。</td>
</tr>
</tbody>
</table>


## 詳細資訊記錄

根據預設，系統管理員稽核記錄會記錄僅指令程式名稱、 cmdlet 參數 （及指定的值），可修改、 誰執行此指令程式，此 cmdlet 所執行，並在哪些伺服器上執行此指令程式時的物件。系統管理員稽核記錄不會記錄哪些屬性已修改的物件上。如果您想要還包含物件中所修改的屬性的稽核記錄，您可以啟用詳細資訊記錄*LogLevel*參數設為`Verbose`。當您啟用詳細資訊記錄，除了預設所記錄的資訊之外的稽核記錄中所包含上的物件，包括其舊的和新的值，修改屬性。

## 測試指令程式

開頭為動詞**Test**指令程式不預設記錄。您可以指出應該記錄*TestCmdletLoggingEnabled*參數設為`$true`的**Test**指令程式。雖然您可以啟用記錄的測試指令程式，我們建議您採用這僅適用於短時間內的因為測試 cmdlet 可以產生大量的資訊。

## 稽核記錄

指令程式會記錄，每次建立稽核記錄項目。稽核記錄檔會儲存在僅可使用 EAC 或**Search-AdminAuditLog**或**New-AdminAuditLogSearch**指令程式隱藏、 專用的仲裁信箱。無法開啟使用 Microsoft Outlook Web App或 Microsoft Outlook。下列各節提供下列資訊：

  - 在記錄檔中包含的項目

  - EAC \[稽核\] 頁面上可用的報告

  - 稽核記錄檔搜尋指令程式

## 稽核記錄內容

每個稽核記錄項目包含下表所述的資訊。稽核記錄檔包含一或多個稽核記錄項目。稽核記錄項目數目是由使用**Set-AdminAuditLogConfig**指令程式指定稽核記錄保留限制所控制。會刪除超過存留期限制任何稽核記錄項目。

### 稽核記錄檔輸入欄位

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>欄位</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>RunspaceId</code></p></td>
<td><p>此欄位僅供 Exchange 內部使用。</p></td>
</tr>
<tr class="even">
<td><p><code>ObjectModified</code></p></td>
<td><p>此欄位中包含的物件是由 <code>CmdletName</code> 欄位中指定的指令程式所修改。</p></td>
</tr>
<tr class="odd">
<td><p><code>CmdletName</code></p></td>
<td><p>此欄位包含的指令程式名稱是由 <code>Caller</code> 欄位中的使用者所執行。</p></td>
</tr>
<tr class="even">
<td><p><code>CmdletParameters</code></p></td>
<td><p>此欄位會包含<code>CmdletName</code>欄位中的 cmdlet 所執行時所指定的參數。也儲存在此欄位中，但在預設的輸出中不可見，為指定的值與參數，如果有任何。如需如何存取此欄位中的其他資訊，請參閱<a href="search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md">搜尋角色群組變更或管理員稽核記錄檔</a>的詳細資訊。</p></td>
</tr>
<tr class="odd">
<td><p><code>ModifiedProperties</code></p></td>
<td><p>此欄位會包含在<code>ObjectModified</code> ] 欄位中的物件所修改的屬性。也儲存在此欄位中，但不是可見的預設輸出中，且舊屬性的值已儲存的新值。如需如何存取此欄位中的其他資訊，請參閱<a href="search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md">搜尋角色群組變更或管理員稽核記錄檔</a>的詳細資訊。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>只有在 <strong>Set-AdminAuditLogConfig</strong>指令程式上的 <em>LogLevel</em> 參數設定為 <code>Verbose</code> 時，才會填入此欄位。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p><code>Caller</code></p></td>
<td><p>此欄位包含在 <code>CmdletName</code> 欄位中執行該指令程式的使用者所屬的使用者帳戶。</p></td>
</tr>
<tr class="odd">
<td><p><code>Succeeded</code></p></td>
<td><p>此欄位會指定指令程式<code>CmdletName</code>欄位中的是否已順利執行。此值為<code>True</code>或<code>False</code>。</p></td>
</tr>
<tr class="even">
<td><p><code>Error</code></p></td>
<td><p>如果 <code>CmdletName</code> 欄位中的指令程式無法順利完成，則此欄位會包含所產生的錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><code>RunDate</code></p></td>
<td><p>此欄位包含的日期和時間<code>CmdletName</code>欄位中的指令程式執行的時間。以國際標準時間 (UTC) 格式儲存的日期和時間。</p></td>
</tr>
<tr class="even">
<td><p><code>OriginatingServer</code></p></td>
<td><p>此欄位會指出執行 <code>CmdletName</code> 欄位中指定的指令程式的伺服器。</p></td>
</tr>
<tr class="odd">
<td><p><code>Identity</code></p></td>
<td><p>此欄位僅供 Exchange 內部使用。</p></td>
</tr>
<tr class="even">
<td><p><code>IsValid</code></p></td>
<td><p>此欄位僅供 Exchange 內部使用。</p></td>
</tr>
<tr class="odd">
<td><p><code>ObjectState</code></p></td>
<td><p>此欄位僅供 Exchange 內部使用。</p></td>
</tr>
</tbody>
</table>


回到頁首

## EAC 稽核報告

在 EAC 中的 \[**稽核**\] 頁面具有數個報告，提供各種類型的規範與系統管理組態變更的相關資訊。下列報告提供組織中的組態變更的相關資訊：

  - **系統管理員角色群組報告**  這份報告可讓您變更至您指定在指定的時間範圍內的管理角色群組搜尋。會傳回包含已變更的角色群組、 誰已變更及進行時機以及有什麼變更結果。可以傳回最大值為 3000 項目。如果您的搜尋可能會傳回 3000 個以上的項目，請使用**系統管理員稽核記錄**報告或**Search-AdminAuditLog**指令程式。

  - **系統管理員稽核記錄**  您指定此報告可讓您匯出稽核記錄所記錄至 XML 檔案的指定時間範圍內的項目並再將透過電子郵件檔案傳送給收件者。XML 檔案的內容的相關資訊，請參閱[系統管理員稽核記錄檔結構](administrator-audit-log-structure-exchange-2013-help.md)。

如需如何使用報告的詳細資訊，請參閱[搜尋角色群組變更或管理員稽核記錄檔](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md)。

如需 **\[稽核\]** 頁面上所包含其他報告的詳細資訊，請參閱[Exchange 稽核報告](exchange-auditing-reports-exchange-2013-help.md)。

## Search-AdminAuditLog 指令程式

當您執行**Search-AdminAuditLog**指令程式時，則會傳回所有稽核記錄項目符合您指定的搜尋準則。您可以指定下列搜尋準則：

  - **指令程式**   指定您要在系統管理員稽核記錄中搜尋的指令程式。

  - **參數**  指定的參數，以逗號分隔您想要搜尋的系統管理員稽核記錄中。如果您指定要搜尋指令程式僅可搜尋的參數。

  - **結束日期**   將管理員稽核記錄結果的範圍設定為在指定日期當天或之前發生的記錄項目。

  - **開始日期**   將管理員稽核記錄結果的範圍設定為在指定日期當天或之後發生的記錄項目。

  - **物件識別碼**   指定只應傳回包含所指定已變更物件的系統管理員稽核記錄項目

  - **使用者識別碼**   指定只應在系統管理員稽核記錄項目包含指定的使用者識別碼 (此使用者為當初執行指令程式的使用者) 時，才傳回系統管理員稽核記錄項目。

  - **成功完成**   指定是否只應傳回指出成功或失敗的系統管理員稽核記錄項目。

傳回每個稽核記錄項目包含在稽核記錄檔目錄中的表格中所述的資訊。根據預設，會傳回只的前 1000 日誌項目符合您指定的準則。不過，您可以覆寫此預設值並傳回*ResultSize*參數的更多或更少項目。您可以指定的值為`Unlimited`*ResultSize*參數來傳回所有符合指定的準則的記錄項目。

如需如何使用 **Search-AdminAuditLog**指令程式的詳細資訊，請參閱[搜尋角色群組變更或管理員稽核記錄檔](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md)。

## New-AdminAuditLogSearch 指令程式

**New-AdminAuditLogSearch**指令程式搜尋稽核記錄檔就像是**Search-AdminAuditLog**指令程式。不過，而不是在命令介面中顯示搜尋結果的稽核記錄檔， **New-AdminAuditLogSearch**指令程式會執行搜尋，然後將結果傳送給收件者的搜尋您指定透過電子郵件訊息。結果是當做電子郵件訊息的 XML 附件。

您可以透過**New-AdminAuditLogSearch**指令程式用**Search-AdminAuditLog**指令程式上使用相同的搜尋準則。如需搜尋準則的清單，請參閱Search-adminauditlog 指令程式。

執行**New-AdminAuditLogSearch**指令程式之後， Exchange可能需要 15 分鐘的時間將傳送至指定的收件者的報表。XML 檔附加報告可以為最大值為 10 mb (MB)。XML 檔案包含稽核記錄檔目錄中的表格中所述的相同資訊。如需 XML 檔案結構的詳細資訊，請參閱[系統管理員稽核記錄檔結構](administrator-audit-log-structure-exchange-2013-help.md)。

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


如需如何使用 **New-AdminAuditLogSearch**指令程式的詳細資訊，請參閱[搜尋角色群組變更或管理員稽核記錄檔](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md)。

回到頁首

## 手動稽核記錄項目

除了記錄Exchange指令程式正在執行時， Exchange 2013可讓您手動將記錄項目寫入稽核記錄。Exchange 2013支援此**Write-AdminAuditLog** 指令程式。有時您可能需要新增手動記錄項目包括：

  - 自訂指令碼項目並結束

  - 變更控制項資訊

  - 維護開始和結束時間

使用**Write-AdminAuditLog** 指令程式，您指定要使用*Comment*參數的稽核記錄中包含的文字字串。*Comment*參數可接受最多 500 個字元的英數字元字串。包含在手動稽核記錄項目以及註解字串為 all 擷取記錄Exchange指令程式時的相同資訊。稽核記錄中包含的每個欄位的說明，請參閱稽核記錄檔目錄中的表格。

您可以使用與其他記錄項目相同的方法擷取手動稽核記錄項目，方法是使用 EAC \[稽核\] 頁面或使用 **Search-AdminAuditLog** 或 **New-AdminAuditLogSearch** 指令程式。

若要檢視手動稽核記錄項目中 **Write-AdminAuditLog**指令程式上的 *Comment* 參數內容，請參閱[搜尋角色群組變更或管理員稽核記錄檔](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md)。

## Active Directory 複寫

系統管理員稽核記錄依賴Active Directory複寫來複寫到網域控制站您組織中您指定的組態設定。根據您的複寫設定所做的變更可能不會立即套用到執行Exchange 2013或Exchange 2010您組織中的所有伺服器。

## 管理稽核記錄代理程式

管理員稽核記錄內建指令程式延伸代理程式會執行系統管理員稽核記錄中Exchange 2013指令程式作業。此代理程式讀取稽核記錄檔設定並再執行評估組織中執行每個指令程式。如果您已指定稽核準則記錄設定相符項目正在執行此指令程式，代理程式會產生的稽核記錄。

管理員稽核記錄代理程式會啟用根據預設，這是必要的稽核記錄功能運作。它不能停用，且無法變更其優先順序。如需指令程式延伸代理程式的詳細資訊，請參閱[Cmdlet 延伸代理程式](cmdlet-extension-agents-exchange-2013-help.md)。

