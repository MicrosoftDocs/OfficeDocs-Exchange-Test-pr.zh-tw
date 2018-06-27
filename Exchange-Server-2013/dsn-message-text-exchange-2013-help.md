---
title: 'DSN 郵件文字: Exchange 2013 Help'
TOCTitle: DSN 郵件文字
ms:assetid: eae4a050-5ecb-4c87-b377-74edb93a5995
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb125135(v=EXCHG.150)
ms:contentKeyID: 50474514
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# DSN 郵件文字

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

您可以在 Microsoft Exchange Server 2013 的自訂傳遞狀態通知 (DSN) 郵件中加入文字，並將該段文字格式化為 HTML。

您可以包含任何您想要顯示給 DSN 郵件的收件者的資訊。例如，您可以包含 DSN，您的服務台、 及支援部門的網站連結的連絡人資訊的詳細的說明。每個 DSN 郵件可以包含最大值為 512 個字元。

HTML 中可以顯示 DSN 郵件，因為您可以內嵌 HTML 格式中的 DSN 文字標籤。例如，如果您想要將 DSN 郵件的一些文字變成粗體、 括住 \< B \> 中的文字與 \< /B \> HTML 標籤。下表提供可用於 DSN 訊息文字的有效 HTML 標籤的一些範例。

### 適用於 DSN 訊息的有效 HTML 標記

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>HTML 標記</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>&lt;B&gt;</p></td>
<td><p>粗體開始</p></td>
</tr>
<tr class="even">
<td><p>&lt;/B&gt;</p></td>
<td><p>粗體結束</p></td>
</tr>
<tr class="odd">
<td><p>&lt;A HREF=&quot;url&quot;&gt;</p></td>
<td><p>超連結開始</p></td>
</tr>
<tr class="even">
<td><p>&lt;/A&gt;</p></td>
<td><p>超連結結束</p></td>
</tr>
<tr class="odd">
<td><p>&lt;BR&gt;</p></td>
<td><p>換行</p></td>
</tr>
<tr class="even">
<td><p>&lt;EM&gt;</p></td>
<td><p>斜體開始</p></td>
</tr>
<tr class="odd">
<td><p>&lt;/EM&gt;</p></td>
<td><p>斜體結束</p></td>
</tr>
<tr class="even">
<td><p>&lt;P&gt;</p></td>
<td><p>段落開始</p></td>
</tr>
<tr class="odd">
<td><p>&lt;/P&gt;</p></td>
<td><p>段落結束</p></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>根據預設，Exchange 會傳送 HTML DSN 郵件，但您可以設定是否 Exchange 會將 HTML DSN 郵件傳送給內部寄件者、 外部寄件者，或兩者。若要設定此表現方式，修改<em>InternalDsnSendHtml</em>參數和<em>ExternalDsnSendHtml</em>參數搭配<strong>Set-TransportService</strong>命令。<br />
如果<em>InternalDsnSendHtml</em>參數設為<code>$false</code>，Exchange 會隱藏內部的寄件者的 DSN 訊息中的 HTML 標籤。如果<em>ExternalDsnSendHtml</em>參數設為<code>$false</code>，Exchange 會隱藏在傳送給外部寄件者的 DSN 郵件的 HTML 標籤。</td>
</tr>
</tbody>
</table>


下列 Exchange 在 DSN 郵件文字中使用的字元，具有特別意義︰

  - 大於符號 (\>)

  - 小於符號 (\<)

  - 連字號 (&)

  - 引號 (")

這些字元可用來判斷出 HTML 標籤開始和結束應該給寄件者顯示的文字其中啟動和停止。如果您想要的 DSN 訊息中顯示這些字元，您必須使用下表中的逸出程式碼。

例如，若您想要顯示訊息 `"Please contact the Help Desk at <1234>."`，則必須將 `"Please contact the Help Desk at &lt;1234&gt;." ` 新增到 DSN 訊息文字。

### DSN 訊息字元跳出代碼

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>跳出代碼</th>
<th>字元</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>&amp;lt;</p></td>
<td><p>&lt;</p></td>
</tr>
<tr class="even">
<td><p>&amp;gt;</p></td>
<td><p>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>&amp;quot;</p></td>
<td><p>&quot;</p></td>
</tr>
<tr class="even">
<td><p>&amp;amp;</p></td>
<td><p>&amp;</p></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您在包含引號 （&quot;），例如<code>&lt;A HREF=&quot;url&quot;&gt;</code>您 DSN 訊息文字中包含 HTML 標籤，您必須使用單引號 （'） 整個 DSN 訊息文字周圍。如果您使用雙引號整個 DSN 訊息文字周圍與周圍的 HTML 標籤，將會收到錯誤訊息。</td>
</tr>
</tbody>
</table>

