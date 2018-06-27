---
title: '信箱稽核記錄: Exchange 2013 Help'
TOCTitle: 信箱稽核記錄
ms:assetid: 29b67d58-eef9-4ad4-863f-562405ea8794
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ff459237(v=EXCHG.150)
ms:contentKeyID: 50472878
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 信箱稽核記錄

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

由於信箱會包含敏感、高度業務影響 (HBI) 資訊和個人識別資訊 (PII)，因此追蹤哪些人登入組織中的信箱以及執行哪些動作是相當重要的。追蹤信箱擁有者以外的使用者存取信箱則更為重要。這些使用者稱為*代理使用者*。

使用*信箱稽核記錄*，您就可以依信箱擁有者、代理人 (包括具有完整信箱存取權限的系統管理員) 和系統管理員記錄信箱存取。

啟用信箱的稽核記錄時，可指定針對哪種登入類型 (系統管理員、代理使用者或擁有者) 將記錄哪些使用者動作 (例如存取、移動或刪除郵件)。稽核記錄項目還包含一些重要資訊，例如用戶端 IP 位址、主機名稱，以及用來存取信箱的程序或用戶端。針對移動的項目，記錄中還包含目的資料夾的名稱。

## 信箱稽核記錄

每個啟用信箱稽核記錄功能的信箱都會產生信箱稽核記錄。記錄項目會儲存在稽核信箱 \[可復原的項目\] 資料夾的 \[稽核\] 子資料夾中。因此，無論是使用哪種用戶端存取方法來存取信箱，或系統管理員使用哪個伺服器或工作站來存取信箱稽核記錄，這都可確保所有的稽核記錄項目都能從單一位置取得。如果您將信箱移至其他信箱伺服器，該信箱的信箱稽核記錄也會隨之移動，因為這些記錄皆位於信箱中。

依預設，信箱稽核記錄項目會先保留在信箱中 90 天再刪除。您可以使用 *AuditLogAgeLimit* 參數與 [Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\)) 指令程式來修改保留期間。如果信箱處於就地保留或訴訟暫止狀態，則稽核記錄項目只會保存到信箱的稽核記錄保留期間期滿為止。若要將稽核記錄項目保留更久的時間，您必須變更 *AuditLogAgeLimit* 參數值來加長保留期間。您也可以在保留期間期滿前匯出稽核記錄項目。如需相關資訊，請參閱：

  - [匯出信箱稽核記錄](export-mailbox-audit-logs-exchange-2013-help.md)

  - [建立信箱稽核記錄搜尋](create-a-mailbox-audit-log-search-exchange-2013-help.md)

## 啟用信箱稽核記錄

啟用每個信箱的信箱稽核記錄。使用 **Set-Mailbox** 指令程式來啟用或停用信箱稽核記錄。如需詳細資料，請參閱[啟用或停用信箱稽核記錄功能信箱](enable-or-disable-mailbox-audit-logging-for-a-mailbox-exchange-2013-help.md)。

啟用信箱的信箱稽核記錄時，預設會記錄信箱的存取和某些系統管理員與代理人動作。若要記錄信箱擁有者執行的動作，您必須指定要稽核的擁有者動作。

## 信箱稽核記錄所記錄的信箱動作

下表列出信箱稽核記錄所記錄的動作，包括可記錄動作的登入類型。


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>動作</th>
<th>描述</th>
<th>系統管理員</th>
<th>代理人</th>
<th>擁有者</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Copy</p></td>
<td><p>將項目複製到其他資料夾。</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>Create</p></td>
<td><p>在信箱的 [行事曆]、[連絡人]、[記事] 或 [工作] 資料夾中建立了項目，例如，建立了新的會議邀請。請注意，郵件或資料夾建立將不予稽核。</p></td>
<td><p>是*</p></td>
<td><p>是*</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>FolderBind</p></td>
<td><p>存取信箱資料夾。</p></td>
<td><p>是*</p></td>
<td><p>是**</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>HardDelete</p></td>
<td><p>永久刪除 [可復原的項目] 資料夾中的項目。</p></td>
<td><p>是*</p></td>
<td><p>是*</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>MessageBind</p></td>
<td><p>在讀取窗格存取或開啟項目。</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>Move</p></td>
<td><p>將項目移至其他資料夾。</p></td>
<td><p>是*</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>MoveToDeletedItems</p></td>
<td><p>將項目移至 [刪除的郵件] 資料夾。</p></td>
<td><p>是*</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>SendAs</p></td>
<td><p>使用「以下列傳送」權限傳送郵件。</p></td>
<td><p>是*</p></td>
<td><p>是*</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="odd">
<td><p>SendOnBehalf</p></td>
<td><p>使用「代理傳送者」權限傳送郵件。</p></td>
<td><p>是*</p></td>
<td><p>是</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="even">
<td><p>SoftDelete</p></td>
<td><p>將項目從 [刪除的郵件] 資料夾刪除。</p></td>
<td><p>是*</p></td>
<td><p>是*</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>Update</p></td>
<td><p>更新項目的屬性。</p></td>
<td><p>是*</p></td>
<td><p>是*</p></td>
<td><p>是</p></td>
</tr>
</tbody>
</table>


\* 在啟用信箱的稽核時依預設稽核。

\* \* 資料夾繫結動作委派所執行的項目已合併。24 小時的時間範圍內的個別資料夾存取產生一個日誌項目。

如果您不再需要稽核某些信箱動作類型，您應修改信箱的稽核記錄組態以停用這些動作。在達到稽核記錄項目的保留天數之前，不會清除現有的記錄項目。

## 搜尋信箱稽核記錄項目

您可以使用下列方法來搜尋稽核記錄項目：

  - **同步搜尋單一信箱** 您可以使用 [Search-MailboxAuditLog](https://technet.microsoft.com/zh-tw/library/ff522360\(v=exchg.150\)) 指令程式同步搜尋單一信箱的信箱稽核記錄項目。指令程式會在 Exchange 管理命令介面視窗顯示搜尋結果。如需詳細資料，請參閱[搜尋信箱的信箱稽核記錄](search-the-mailbox-audit-log-for-a-mailbox-exchange-2013-help.md)。

  - **同步搜尋一個或多個信箱** 您可以建立信箱稽核記錄搜尋以同步搜尋一個或多個信箱的搜尋信箱稽核記錄，然後將搜尋結果傳送到指定的電子郵件地址。搜尋結果會以 XML 附件的形式傳送。若要建立搜尋，請使用 [New-MailboxAuditLogSearch](https://technet.microsoft.com/zh-tw/library/ff522362\(v=exchg.150\)) 指令程式。如需相關資訊，請參閱[建立信箱稽核記錄搜尋](create-a-mailbox-audit-log-search-exchange-2013-help.md)。

  - **使用 Exchange 系統管理中心 (EAC) 中的稽核報告**   您可以使用 EAC 中的 \[稽核\] 索引標籤來執行非擁有者信箱存取報告，或從信箱稽核記錄中匯出項目。如需詳細資訊，請參閱：
    
      - [執行非擁有者信箱存取報告](run-a-non-owner-mailbox-access-report-exchange-online-help.md)
    
      - [匯出信箱稽核記錄](export-mailbox-audit-logs-exchange-2013-help.md)

## 信箱稽核記錄項目

下表說明在信箱稽核記錄項目中記錄的欄位。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>欄位</th>
<th>填入</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Operation</strong></p></td>
<td><p>下列其中一個動作：</p>
<ul>
<li><p>Copy</p></li>
<li><p>Create</p></li>
<li><p>FolderBind</p></li>
<li><p>HardDelete</p></li>
<li><p>MessageBind</p></li>
<li><p>Move</p></li>
<li><p>MoveToDeletedItems</p></li>
<li><p>SendAs</p></li>
<li><p>SendOnBehalf</p></li>
<li><p>SoftDelete</p></li>
<li><p>Update</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>OperationResult</strong></p></td>
<td><p>下列其中一個結果：</p>
<ul>
<li><p>Failed</p></li>
<li><p>PartiallySucceeded</p></li>
<li><p>Succeeded</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>LogonType</strong></p></td>
<td><p>執行作業的使用者登入類型。登入類型包括：</p>
<ul>
<li><p>擁有者</p></li>
<li><p>代理人</p></li>
<li><p>管理</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>DestFolderId</strong></p></td>
<td><p>移動作業的目的資料夾 GUID。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DestFolderPathName</strong></p></td>
<td><p>移動作業的目的資料夾路徑。</p></td>
</tr>
<tr class="even">
<td><p><strong>FolderId</strong></p></td>
<td><p>資料夾 GUID。</p></td>
</tr>
<tr class="odd">
<td><p><strong>FolderPathName</strong></p></td>
<td><p>資料夾路徑。</p></td>
</tr>
<tr class="even">
<td><p><strong>ClientInfoString</strong></p></td>
<td><p>用於識別哪個用戶端或 Exchange 元件執行作業的相關資訊。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ClientIPAddress</strong></p></td>
<td><p>用戶端電腦 IP 位址。</p></td>
</tr>
<tr class="even">
<td><p><strong>ClientMachineName</strong></p></td>
<td><p>用戶端電腦名稱。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ClientProcessName</strong></p></td>
<td><p>應用程式處理程序的名稱。</p></td>
</tr>
<tr class="even">
<td><p><strong>ClientVersion</strong></p></td>
<td><p>用戶端應用程式版本。</p></td>
</tr>
<tr class="odd">
<td><p><strong>InternalLogonType</strong></p></td>
<td><p>執行作業的使用者登入類型。登入類型包括：</p>
<ul>
<li><p>擁有者</p></li>
<li><p>代理人</p></li>
<li><p>管理</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>MailboxOwnerUPN</strong></p></td>
<td><p>信箱擁有者使用者主要名稱 (UPN)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MailboxOwnerSid</strong></p></td>
<td><p>信箱擁有者安全性識別碼 (SID)。</p></td>
</tr>
<tr class="even">
<td><p><strong>DestMailboxOwnerUPN</strong></p></td>
<td><p>針對跨信箱作業記錄的目的信箱擁有者 UPN。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DestMailboxOwnerSid</strong></p></td>
<td><p>針對跨信箱作業記錄的目的信箱擁有者 SID。</p></td>
</tr>
<tr class="even">
<td><p><strong>DestMailboxOwnerGuid</strong></p></td>
<td><p>目的信箱擁有者 GUID。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CrossMailboxOperation</strong></p></td>
<td><p>關於記錄的作業是否為跨信箱作業的資訊 (例如，在信箱之間複製或移動郵件)。</p></td>
</tr>
<tr class="even">
<td><p><strong>LogonUserDisplayName</strong></p></td>
<td><p>顯示登入的使用者名稱。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DelegateUserDisplayName</strong></p></td>
<td><p>代理使用者顯示名稱。</p></td>
</tr>
<tr class="even">
<td><p><strong>LogonUserSid</strong></p></td>
<td><p>登入的使用者 SID。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SourceItems</strong></p></td>
<td><p>執行記錄動作 (例如移動或刪除) 的信箱項目 ItemID。針對在數個項目上執行的作業，此欄位會傳回項目組合。</p></td>
</tr>
<tr class="even">
<td><p><strong>SourceFolders</strong></p></td>
<td><p>來源資料夾 GUID。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ItemId</strong></p></td>
<td><p>項目 ID。</p></td>
</tr>
<tr class="even">
<td><p><strong>ItemSubject</strong></p></td>
<td><p>項目主旨。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MailboxGuid</strong></p></td>
<td><p>信箱 GUID。</p></td>
</tr>
<tr class="even">
<td><p><strong>MailboxResolvedOwnerName</strong></p></td>
<td><p><em>DOMAIN</em>\<em>SamAccountName</em> 格式的信箱使用者解析名稱。</p></td>
</tr>
<tr class="odd">
<td><p><strong>LastAccessed</strong></p></td>
<td><p>作業的執行時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>Identity</strong></p></td>
<td><p>稽核記錄項目 ID。</p></td>
</tr>
</tbody>
</table>


## 其他資訊

  - **信箱的系統管理員存取權**   在下列案例中，信箱會被視為只能由系統管理員存取：
    
      - 使用 [就地 eDiscovery](in-place-ediscovery-exchange-2013-help.md) 來搜尋信箱。
    
      - 使用 [New-MailboxExportRequest](https://technet.microsoft.com/zh-tw/library/ff607299\(v=exchg.150\)) 指令程式來匯出信箱。
    
      - [Microsoft Exchange Server MAPI 編輯器](https://go.microsoft.com/fwlink/p/?linkid=204086)用來存取信箱。

  - **略過信箱稽核記錄**   某些已授權自動化處理程序 (例如協力廠商工具所用的帳戶或用於法律監視的帳戶) 進行的信箱存取會建立大量的信箱稽核記錄項目，但組織對這些項目可能並無興趣。您可以設定這些帳戶略過信箱稽核記錄。如需詳細資料，請參閱[使用者帳戶從信箱稽核記錄略過](bypass-a-user-account-from-mailbox-audit-logging-exchange-2013-help.md)。

  - **記錄信箱擁有者動作**   對於探索搜尋信箱等可能包含敏感資訊的信箱來說，則應考慮針對郵件刪除等信箱擁有者動作啟用信箱稽核記錄。

回到頁首

