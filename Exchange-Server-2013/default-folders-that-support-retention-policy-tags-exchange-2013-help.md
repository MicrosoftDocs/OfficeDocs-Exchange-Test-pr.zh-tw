---
title: '支援保留原則標記的預設資料夾: Exchange Online Help'
TOCTitle: 支援保留原則標記的預設資料夾
ms:assetid: d2e2064f-4102-4018-b688-504d09da6d39
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn783294(v=EXCHG.150)
ms:contentKeyID: 62835941
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 支援保留原則標記的預設資料夾

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2017-04-20_

您可以使用[保留標記和保留原則](retention-tags-and-retention-policies-exchange-2013-help.md)來管理電子郵件生命週期。保留原則包含保留標記是可用來指定封存或應刪除訊息自動要移動時設定。

保留原則標記 （印） 是一種可以套用至信箱，例如**收件匣**和**已刪除的項目**中的預設資料夾的保留標記。

![建立保留原則標記 (RPT)](images/Dn783294.b59a96fd-94e1-4c9b-bff6-97a1bd98dfe7(EXCHG.150).png "建立保留原則標記 (RPT)")

## 支援的預設資料夾

您可以在下表所示的預設資料夾建立 Rpt。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>資料夾名稱</th>
<th>詳細資料</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>封存</p></td>
<td><p>這個資料夾是預設目的地之郵件封存與 Outlook 的 [封存] 按鈕。封存功能快速程式提供方法來移除郵件而不刪除其收件匣的使用者。</p>
<p>此印為僅可用於Exchange Online。</p></td>
</tr>
<tr class="even">
<td><p>行事曆</p></td>
<td><p>此預設資料夾用於儲存會議和約會。</p></td>
</tr>
<tr class="odd">
<td><p>雜亂資料</p></td>
<td><p>這個資料夾包含低優先順序電子郵件訊息。雜亂會查看您已完成過去來判斷您是很有可能搜尋時忽略的訊息。然後將那些郵件移至 [<strong>雜亂</strong>] 資料夾。</p></td>
</tr>
<tr class="even">
<td><p>交談歷程記錄</p></td>
<td><p>此資料夾是由 Microsoft Lync (先前的 Microsoft Office Communicator) 所建立。雖然 Outlook 未將它視為預設資料夾，但 Exchange 將它視為特殊資料夾且可以套用 RPT。</p></td>
</tr>
<tr class="odd">
<td><p>刪除的郵件</p></td>
<td><p>此預設資料夾是用來儲存從信箱中其他資料夾刪除的項目。Outlook 和 Outlook Web App 使用者可以手動清空此資料夾。使用者也可以設定 Outlook，以在關閉 Outlook 時清空資料夾。</p></td>
</tr>
<tr class="even">
<td><p>草稿</p></td>
<td><p>此預設資料夾是用來儲存使用者尚未傳送的草稿郵件。Outlook Web App 也會使用此資料夾來儲存已由使用者傳送但尚未提交至 Hub Transport Server 的郵件。</p></td>
</tr>
<tr class="odd">
<td><p>收件匣</p></td>
<td><p>此預設資料夾是用來儲存傳遞至信箱的郵件。</p></td>
</tr>
<tr class="even">
<td><p>Journal</p></td>
<td><p>此預設資料夾包含使用者選取的動作。這些動作會自動由 Outlook 記錄並放在時間表檢視中。</p></td>
</tr>
<tr class="odd">
<td><p>垃圾郵件</p></td>
<td><p>此預設資料夾是用來儲存由 Exchange 伺服器上的內容篩選器，或由 Outlook 中的反垃圾郵件篩選器，標記為垃圾電子郵件的郵件。</p></td>
</tr>
<tr class="even">
<td><p>記事</p></td>
<td><p>此資料夾包含使用者在 Outlook 中所建立的記事。這些記事在 Outlook Web App 中也可看到。</p></td>
</tr>
<tr class="odd">
<td><p>寄件匣</p></td>
<td><p>此預設資料夾是用來暫時儲存使用者所傳送的郵件，直到將郵件提交至 Hub Transport Server 為止。已傳送的郵件副本會儲存在 [寄件備份] 預設資料夾中。由於郵件通常只會保留在此資料夾中一小段時間，因此不必為此資料夾建立 RPT。</p></td>
</tr>
<tr class="even">
<td><p>RSS 摘要</p></td>
<td><p>此預設資料夾包含 RSS 摘要。</p></td>
</tr>
<tr class="odd">
<td><p>可復原的項目</p></td>
<td><p>這是在非 IPM 子樹狀目錄中隱藏的資料夾。包含刪除、 版本、 清除、 DiscoveryHolds、 及稽核個子資料夾。此資料夾的保留標記會將項目從 [可復原的項目] 資料夾中使用者的主要信箱移至使用者封存信箱中的 [可復原的郵件] 資料夾。您可以將僅 [<strong>移至封存</strong>] 保留動作指派給此資料夾的標籤。若要深入了解，請參閱<a href="recoverable-items-folder-exchange-2013-help.md">可復原的項目資料夾</a>。</p></td>
</tr>
<tr class="even">
<td><p>寄件備份</p></td>
<td><p>此預設資料夾是用來儲存提交至 Hub Transport Server 的郵件。</p></td>
</tr>
<tr class="odd">
<td><p>同步問題</p></td>
<td><p>這個資料夾包含同步處理記錄檔。若要深入了解，請參閱<a href="https://go.microsoft.com/fwlink/p/?linkid=198215">同步處理錯誤資料夾</a>。</p></td>
</tr>
<tr class="even">
<td><p>工作</p></td>
<td><p>此預設資料夾用來儲存工作。若要建立 rpt，適用於 [工作] 資料夾，您必須使用Exchange 管理命令介面。如需詳細資訊，請參閱<a href="https://technet.microsoft.com/zh-tw/library/dd335226(v=exchg.150)">New-RetentionPolicyTag</a>。建立工作資料夾印之後，您可以使用 Exchange 系統管理中心來管理。</p></td>
</tr>
</tbody>
</table>


## 更多資訊

  - Rpt 是預設資料夾的保留標記。您只能選取刪除動作的 Rpt – \[**刪除並允許復原**\] 或 \[**永久刪除**。

  - 您無法建立將郵件移至封存印。若要移至封存舊的項目，您可以建立*預設原則標記*(DPT)，它會套用至整個信箱或*個人標記*，其顯示在 Outlook 和 Outlook Web App (OWA) 設定為封存原則。您的使用者可以套用至要採用資料夾或個別的郵件。

  - 您無法將 RPT 套用至 \[連絡人\] 資料夾。

  - 您只可以將特殊預設資料夾 RPT 新增至保留原則。例如，如果保留原則有一個收件匣標籤，您無法新增類型收件匣的另一個印至該保留原則。

  - 若要了解如何建立 Rpt 或其他類型的保留標記並將其新增至保留原則，請參閱[建立保留原則](create-a-retention-policy-exchange-2013-help.md)。

  - 在Exchange 2013和Exchange Online，DPT 也適用於**行事曆**及**工作**的預設資料夾。這可能會導致被刪除或移至封存 DPT 設定為基礎的項目。若要防止在刪除這些資料夾中的項目中的 DPT 設定，請使用保留已停用建立 Rpt。若要防止移動項目中的預設資料夾的 DPT 設定，您可以搭配移至封存巨集指令、 將其新增至保留原則，且然後套用至預設資料夾的使用者建立已停用的個人標記。如需詳細資訊，請參閱[防止在 Exchange 2010 中的預設資料夾中的項目封存](https://go.microsoft.com/fwlink/?linkid=511071)。

