---
title: '郵件內容和搜尋運算子就地 ediscovery （英文）: Exchange Online Help'
TOCTitle: 郵件內容和搜尋運算子就地 ediscovery （英文）
ms:assetid: 402b74e4-8853-4c51-9737-1a9c19f8e3dd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn774955(v=EXCHG.150)
ms:contentKeyID: 62623016
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 郵件內容和搜尋運算子就地 ediscovery （英文）

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

本主題說明您可以使用就地 eDiscovery 和保留搜尋的Exchange電子郵件的內容Exchange Server 2013和Exchange Online中。主題也會說明搜尋布林運算子和其他可用來調整 eDiscovery 搜尋結果的搜尋查詢技術。

就地 eDiscovery 使用關鍵字查詢語言 (KQL)。如需詳細資訊，請參閱[關鍵字查詢語言語法參考 （英文)](https://go.microsoft.com/fwlink/?linkid=269603)。

## 在 Exchange 中的可搜尋屬性

下表列出使用就地 eDiscovery 搜尋可搜尋的電子郵件內容或使用**New-MailboxSearch**或**Set-MailboxSearch**指令程式。表格包含每個屬性並由範例傳回的搜尋結果的描述*property:value*語法範例。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>屬性</th>
<th>屬性描述</th>
<th>範例</th>
<th>範例所傳回的搜尋結果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>附件</p></td>
<td><p>附加到電子郵件的檔案名稱。</p></td>
<td><p>attachment:annualreport.ppt</p>
<p>attachment:annual*</p></td>
<td><p>郵件已附加的檔案命名為 annualreport.ppt。</p>
<p>在第二個範例中，使用萬用字元傳回郵件的字&quot;年度&quot;中的附件檔案名稱。</p></td>
</tr>
<tr class="even">
<td><p>密件副本</p></td>
<td><p>電子郵件訊息的 [密件副本] 欄位。1</p></td>
<td><p>bcc:pilarp@contoso.com</p>
<p>bcc:pilarp</p>
<p>bcc:&quot;Pilar Pinilla&quot;</p></td>
<td><p>所有的範例會傳回包含在密件副本欄位中具有 Pilar Pinilla 的郵件。</p></td>
</tr>
<tr class="odd">
<td><p>類別</p></td>
<td><p>要搜尋的類別。使用者可以使用 Outlook 或 Outlook Web App 定義類別。可能的值為：</p>
<ul>
<li><p>藍色</p></li>
<li><p>綠色</p></li>
<li><p>橙色</p></li>
<li><p>紫色</p></li>
<li><p>紅色</p></li>
<li><p>黃色</p></li>
</ul></td>
<td><p>category:&quot;Red Category&quot;</p></td>
<td><p>來源信箱中已指派紅色類別的郵件。</p></td>
</tr>
<tr class="even">
<td><p>副本</p></td>
<td><p>電子郵件訊息的 [副本] 欄位。1</p></td>
<td><p>cc:pilarp@contoso.com</p>
<p>cc:&quot;Pilar Pinilla&quot;</p></td>
<td><p>在這兩個範例中，具有在 [副本] 欄位中指定 Pilar Pinilla 的郵件。</p></td>
</tr>
<tr class="odd">
<td><p>寄件者</p></td>
<td><p>電子郵件訊息的寄件者。1</p></td>
<td><p>from:pilarp@contoso.com</p>
<p>from:contoso.com</p></td>
<td><p>指定的使用者或從指定的網域傳送的郵件。</p></td>
</tr>
<tr class="even">
<td><p>重要性</p></td>
<td><p>電子郵件訊息的重要性，寄件者在傳送郵件時可以指定。根據預設，郵件會以一般重要性傳送，除非寄件者將重要性設定為 [高] 或 [低]。</p></td>
<td><p>importance:high</p>
<p>importance:medium</p>
<p>importance:low</p></td>
<td><p>標示為高重要性、中重要性或低重要性的郵件。</p></td>
</tr>
<tr class="odd">
<td><p>類型</p></td>
<td><p>要搜尋的郵件類型。可能值：</p>
<ul>
<li><p>連絡人</p></li>
<li><p>文件</p></li>
<li><p>電子郵件</p></li>
<li><p>傳真</p></li>
<li><p>IM</p></li>
<li><p>日誌</p></li>
<li><p>會議</p></li>
<li><p>附註</p></li>
<li><p>張貼</p></li>
<li><p>rssfeeds</p></li>
<li><p>工作</p></li>
<li><p>語音信箱</p></li>
</ul></td>
<td><p>kind:email</p>
<p>kind:email 或 kind:im 或 kind:voicemail</p></td>
<td><p>符合搜尋準則的電子郵件。第二個範例會傳回電子郵件、立即訊息交談，以及符合搜尋準則的語音訊息。</p></td>
</tr>
<tr class="even">
<td><p>參與者</p></td>
<td><p>電子郵件中所有的人員欄位；這些欄位為 [寄件者]、[收件者]、[副本] 及 [密件副本]。1</p></td>
<td><p>participants:garthf@contoso.com</p>
<p>participants:contoso.com</p></td>
<td><p>傳送至 garthf@contoso.com 或傳送的訊息。</p>
<p>第二個範例會傳回所有訊息所傳送或傳送至 contoso.com 網域中的使用者。</p></td>
</tr>
<tr class="odd">
<td><p>已收到</p></td>
<td><p>收件者收到電子郵件的日期。</p></td>
<td><p>received:04/15/2014</p>
<p>received&gt;=01/01/2014 AND received&lt;=03/31/2014</p></td>
<td><p>在 2014 年 4 月 15 日收到的郵件。第二個範例會傳回 2014 年 1 月 1 日到 2014 年 3 月 31 之間所收到的所有郵件。</p></td>
</tr>
<tr class="even">
<td><p>收件者</p></td>
<td><p>電子郵件中所有的收件者欄位；這些欄位為 [收件者]、[副本] 及 [密件副本]。1</p></td>
<td><p>recipients:garthf@contoso.com</p>
<p>recipients:contoso.com</p></td>
<td><p>傳送至 garthf@contoso.com 的郵件。</p>
<p>在第二個範例傳回傳送給任何收 contoso.com 網域中的郵件。</p></td>
</tr>
<tr class="odd">
<td><p>寄件日期</p></td>
<td><p>寄件者傳送電子郵件的日期。</p></td>
<td><p>sent:07/01/2014</p>
<p>sent&gt;=06/01/2014 AND sent&lt;=07/01/2014</p></td>
<td><p>在特定日期傳送或指定的日期範圍內所傳送的郵件。</p></td>
</tr>
<tr class="even">
<td><p>大小</p></td>
<td><p>項目的大小 (以位元組為單位)。</p></td>
<td><p>size&gt;26214400</p>
<p>size:1..1048576</p></td>
<td><p>大於 25 MB 的郵件。</p>
<p>第二個範例會傳回介於 1 到 1048576 位元組 (1 MB) 的大小的郵件。</p></td>
</tr>
<tr class="odd">
<td><p>主旨</p></td>
<td><p>電子郵件的主旨行中的文字。</p></td>
<td><p>主旨:&quot;Quarterly Financials&quot;</p>
<p>subject:northwind</p></td>
<td><p>郵件包含 「 Quarterly financials 」&quot;anywhere 中的主旨行文字。</p>
<p>第二個範例會傳回包含 word northwind 主旨行中的所有郵件。</p></td>
</tr>
<tr class="even">
<td><p>收件者</p></td>
<td><p>電子郵件的 [收件者] 欄位。1</p></td>
<td><p>to:annb@contoso.com</p>
<p>to:annb</p>
<p>收件者:&quot;Ann Beebe&quot;</p></td>
<td><p>所有範例會傳回在 [收件者:] 行中指定 Ann Beebe 的郵件。</p></td>
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
<td>1   如需收件者的屬性值，您可以使用 SMTP 位址、顯示名稱或別名來指定使用者。例如，您可以使用 annb@contoso.com、annb 或「Ann Beebe」來指定使用者 Ann Beebe。</td>
</tr>
</tbody>
</table>


## 支援的搜尋運算子

布林值搜尋運算子，例如**AND**、 **OR**，可協助您藉由包括或排除搜尋查詢中的特定字詞定義更精確的信箱搜尋。其他技術，例如使用屬性運算子 (例如 \> = 或..)、 引號括號，且萬用字元，協助您調整 eDiscovery 搜尋查詢。下表列出您可以使用縮小或擴大搜尋結果的運算子。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您必須在搜尋查詢中使用大寫布林運算子。例如，使用<strong>AND</strong>;請勿使用<strong>and</strong>。在搜尋查詢中使用小寫運算子會傳回錯誤。</td>
</tr>
</tbody>
</table>



<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>運算子</th>
<th>使用量</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AND</p></td>
<td><p>keyword1 AND keyword2</p></td>
<td><p>會傳回包含所有指定的關鍵字或<code>property:value</code>運算式的郵件。</p></td>
</tr>
<tr class="even">
<td><p>+</p></td>
<td><p>keyword1 + keyword2 + keyword3</p></td>
<td><p>會傳回包含<em><code>keyword2 </code>或<code>keyword3</code><em>及</em></em>包含的項目也<code>keyword1</code>。因此，此範例相當於查詢<code>(keyword2 OR keyword3) AND keyword1</code>。</p>
<p>請注意，查詢<code>keyword1 + keyword2</code> ( <strong>+</strong>之後空白符號) 不是使用<strong>AND</strong>運算子相同。此查詢就會等於<code>&quot;keyword1 + keyword2&quot;</code>並傳回完全階段<code>&quot;keyword1 + keyword2&quot;</code>項目。</p></td>
</tr>
<tr class="odd">
<td><p>OR</p></td>
<td><p>keyword1 OR keyword2</p></td>
<td><p>會傳回包含一或多個指定的關鍵字或<code>property:value</code>運算式的郵件。</p></td>
</tr>
<tr class="even">
<td><p>NOT</p></td>
<td><p>keyword1 NOT keyword2</p>
<p>NOT from:&quot;Ann Beebe&quot;</p></td>
<td><p>排除關鍵字或<code>property:value</code> expression 所指定的郵件。例如， <code>NOT from:&quot;Ann Beebe&quot;</code>排除 Ann Beebe 所傳送的郵件。</p></td>
</tr>
<tr class="odd">
<td><p>-</p></td>
<td><p>keyword1 -keyword2</p></td>
<td><p>相同<strong>不</strong>運算子。 此查詢會傳回含有<code>keyword1</code>的項目並排除包含<code>keyword2</code>的項目。</p></td>
</tr>
<tr class="even">
<td><p>NEAR</p></td>
<td><p>keyword1 NEAR(n) keyword2</p></td>
<td><p>會傳回其中 n 等於字數分開靠近彼此的單字的郵件。例如<code>best NEAR(5) worst</code>會傳回郵件其中單字&quot;百分比顯示&quot;是內的&quot;最佳&quot;的五個單字。如果未不指定任何數字，則預設距離是八個單字。</p></td>
</tr>
<tr class="odd">
<td><p>:</p></td>
<td><p>property:value</p></td>
<td><p>在<code>property:value</code>語法冒號 （:） 指定要搜尋的屬性值等於指定的值。例如， <code>recipients:garthf@contoso.com</code>會傳回任何訊息傳送到 garthf@contoso.com。</p></td>
</tr>
<tr class="even">
<td><p>&lt;</p></td>
<td><p>property&lt;value</p></td>
<td><p>代表所搜尋的屬性小於指定的值。 1</p></td>
</tr>
<tr class="odd">
<td><p>&gt;</p></td>
<td><p>property&gt;value</p></td>
<td><p>代表所搜尋的屬性大於指定的值。1</p></td>
</tr>
<tr class="even">
<td><p>&lt;=</p></td>
<td><p>property&lt;=value</p></td>
<td><p>代表所搜尋的屬性小於或等於指定的值。1</p></td>
</tr>
<tr class="odd">
<td><p>&gt;=</p></td>
<td><p>property&gt;=value</p></td>
<td><p>代表所搜尋的屬性大於或等於指定的值。1</p></td>
</tr>
<tr class="even">
<td><p>..</p></td>
<td><p>property:value1..value2</p></td>
<td><p>代表所搜尋的屬性大於或等於 value1 且小於或等於 value2。1</p></td>
</tr>
<tr class="odd">
<td><p>&quot; &quot;</p></td>
<td><p>&quot;fair value&quot;</p>
<p>主旨:&quot;Quarterly Financials&quot;</p></td>
<td><p>使用雙引號 (&quot; &quot;) 來搜尋關鍵字中的精準字詞或詞彙和 <code>property:value</code> 搜尋查詢。</p></td>
</tr>
<tr class="even">
<td><p>*</p></td>
<td><p>cat*</p>
<p>subject:set*</p></td>
<td><p>零或多個字元的關鍵字或<code>property:value</code>查詢比對前置詞萬用字元搜尋 （星號放置一個字結尾處）。例如， <code>subject:set*</code>會傳回包含字組、 設定和設定 （與其他單字&quot;集&quot;開頭） 的郵件主旨行中。</p></td>
</tr>
<tr class="odd">
<td><p>( )</p></td>
<td><p>（普通或空閒）與 from:contoso.com</p>
<p>(IPO OR initial) AND (stock OR shares)</p>
<p>(quarterly financials)</p></td>
<td><p>括號將布林片語、<code>property:value</code> 項目和關鍵字群組在一起。例如，<code>(quarterly financials)</code> 會傳回包含文字「quarterly」和「financials」的項目。</p></td>
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
<td>1   對具有日期或數值的屬性使用這個運算子。</td>
</tr>
</tbody>
</table>


## 在搜尋查詢中不支援的字元

在搜尋查詢中的不支援的字元通常是搜尋錯誤或傳回非預期的結果。通常會隱藏不受支援的字元與它們通常新增到查詢當您從其他應用程式 （例如 Microsoft Word 或 Microsoft Excel） 複製的查詢的組件並將它複製到 \[查詢\] 頁面上的就地 eDiscovery 搜尋關鍵字\] 方塊。

以下是不支援字元的就地 eDiscovery 搜尋查詢的清單。

  - **智慧引號**  不支援智慧單一及雙引號 （也稱為 「*智慧引號*」）。僅限直線引號可用於搜尋查詢。

  - **非列印和控制字元**  非列印和控制字元不代表書寫的符號，例如英數字元。範例的非列印和控制字元加入格式化文字或個別行文字的字元。

  - **左到右和從右至左標記**  這些是的控制字元用來指出 （例如英文和西班牙文） 以從左至右語言和從右至左語言 （如阿拉伯文和希伯來文） 的文字方向。

  - **小寫布林值運算元**  成先前所述，您必須使用大寫布林運算子，例如**AND**和**或者**、 搜尋查詢中。請注意，查詢語法通常會表示布林運算子正在使用的即使可能會使用小寫運算子;例如， `(WordA or WordB) and (WordC or WordD)`。

**如何防止在搜尋查詢中的不支援的字元？**若要防止不支援的字元的最佳方式是只需要輸入關鍵字\] 方塊中的查詢。或者，您可以將查詢複製從 Word 或 Excel 並再將它的純文字編輯器，例如 Microsoft \[記事本\] 中的檔案貼。然後將文字檔儲存並選取 \[**編碼**\] 下拉式清單中的**ANSI** 。這會移除任何格式設定與不支援的字元。然後您可以複製並貼到該關鍵字查詢\] 方塊的查詢文字檔案中。

## 搜尋秘訣與技巧

  - 關鍵字搜尋不區分大小寫。例如，**cat** 和 **CAT** 得到的結果一樣。

  - 兩個關鍵字或兩個`property:value`運算式之間的空間並使用**與**相同。例如， `from:"Sara Davis" subject:reorganization`會傳回所有所傳送的郵件 Sara Davis 包含主旨行中 word**重組**。

  - 使用符合`property:value`格式的語法。值不區分大小寫，以及它們不能有空格之後操作員。如果有空格、 預定的值只會全文檢索搜尋。例如**至︰ pilarp**搜尋的"pilarp"為關鍵字，而不是以 pilarp 所傳送的郵件。

  - 當您搜尋收件者屬性時 (例如 To、From、Cc 或 Recipients)，可以使用 SMTP 地址、別名或顯示名稱以代表收件者。例如，您可以使用 pilarp@contoso.com、pilarp 或「Pilar Pinilla」。

  - 您可以使用前置詞萬用字元搜尋 — 例如**cat \***或**組 \***。尾碼萬用字元搜尋 (\* cat) 或子字串搜尋萬用字元 (\* cat \*) 不受支援。

  - 搜尋屬性時使用雙引號 ("") 如果搜尋的值包含多個單字。例如**subject︰ 預算 Q1**會傳回包含**預算**中的郵件的主旨行且包含**Q1**無所不在郵件或中的任何郵件屬性。使用**主旨:"預算 Q1"**會傳回包含**預算 Q1**的主旨行中的任何位置的所有郵件。

