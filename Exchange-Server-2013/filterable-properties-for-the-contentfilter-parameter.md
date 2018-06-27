---
title: '-ContentFilter 參數的可篩選內容: Exchange 2013 Help'
TOCTitle: -ContentFilter 參數的可篩選內容
ms:assetid: cf504a59-1938-489c-bb48-b27b2ac3234e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ff601762(v=EXCHG.150)
ms:contentKeyID: 50554065
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# \-ContentFilter 參數的可篩選內容

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-09-10_

本主題列出 *ContentFilter* 參數的可篩選屬性。*ContentFilter* 參數用於將郵件匯出至符合篩選器的 .pst 檔案。[New-MailboxExportRequest](https://technet.microsoft.com/zh-tw/library/ff607299\(v=exchg.150\)) 指令程式中使用 *ContentFilter* 參數。

## 可篩選的內容

*ContentFilter* 參數的許多屬性接受萬用字元。如果您使用萬用字元，請使用 **-like** 運算子，而不要使用 **-eq** 運算子。**-like** 運算子是用來尋找各種類型 (例如字串) 的模式符合，而 **-eq** 運算子則是用來尋找完全相符的項目。

下表包含 *ContentFilter* 參數的可篩選屬性清單。此表格列出屬性的名稱、描述、可接受的值和語法範例。如需 OPATH 篩選器的相關資訊，請參閱[在 \[收件者的命令介面命令的篩選器](https://technet.microsoft.com/zh-tw/library/bb124268\(v=exchg.150\))。


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
<th>描述</th>
<th>值</th>
<th>範例語法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>All</p></td>
<td><p>此屬性會傳回在任何索引屬性中含有特定字串的所有郵件。例如，如果您要匯出以 &quot;Ayla&quot; 為收件者、寄件者或在郵件內文中提及此名稱的所有郵件，請使用此屬性。</p></td>
<td><p>字串</p>
<p>萬用字元</p></td>
<td><pre><code>-ContentFilter {All -like &#39;*Ayla*&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>Attachment</p></td>
<td><p>此屬性會傳回在附件內容或附件檔名中含有指定字串的郵件。</p></td>
<td><p>字串</p>
<p>萬用字元</p></td>
<td><pre><code>-ContentFilter {Attachment -like &#39;*.jpg&#39;}</code></pre></td>
</tr>
<tr class="odd">
<td><p>BCC</p></td>
<td><p>此屬性傳回在 [密件副本] 欄位中含有指定收件者的已傳送郵件。</p></td>
<td><p>顯示名稱</p>
<p>別名</p>
<p>SMTP 位址</p>
<p>LegacyDN</p>
<p>萬用字元</p></td>
<td><pre><code>-ContentFilter {(BCC -eq &#39;ayla@contoso.com&#39;) -or (BCC -eq &#39;tony@contoso.com&#39;)}</code></pre></td>
</tr>
<tr class="even">
<td><p>Body</p></td>
<td><p>此屬性會傳回在郵件內文含有指定字串的郵件。</p></td>
<td><p>字串</p>
<p>萬用字元</p></td>
<td><pre><code>-ContentFilter {Body -like &#39;*prospectus*&#39;}</code></pre></td>
</tr>
<tr class="odd">
<td><p>Category</p></td>
<td><p>此屬性會傳回具有相符類別的郵件。類別由使用者或 [收件匣] 規則設定。</p></td>
<td><p>字串</p>
<p>萬用字元</p></td>
<td><pre><code>-ContentFilter {Category -like &#39;*Blue*&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>CC</p></td>
<td><p>此屬性會傳回在 [副本] 欄位中含有指定收件者的已傳送郵件。</p></td>
<td><p>顯示名稱</p>
<p>別名</p>
<p>SMTP 位址</p>
<p>LegacyDN</p>
<p>萬用字元</p></td>
<td><pre><code>-ContentFilter {(CC -eq &#39;ayla@contoso.com&#39;) -or (CC -eq &#39;tony@contoso.com&#39;)}</code></pre></td>
</tr>
<tr class="odd">
<td><p>Expires</p></td>
<td><p>此屬性傳回具有指定到期時間戳記的郵件。</p></td>
<td><p>日期時間戳記</p></td>
<td><pre><code>-ContentFilter {Expires -lt &#39;01/01/2013&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>HasAttachment</p></td>
<td><p>此屬性會傳回包含或不含附件的郵件。</p></td>
<td><p>布林值</p>
<p><code>$true</code> 或<code>$false</code></p></td>
<td><pre><code>-ContentFilter {HasAttachment -eq $true}</code></pre></td>
</tr>
<tr class="odd">
<td><p>Importance</p></td>
<td><p>此屬性會傳回具有指定重要性層級的郵件。</p></td>
<td><p>0 或 &quot;Low&quot;</p>
<p>1 或 &quot;Normal&quot;</p>
<p>2 或 &quot;High&quot;</p></td>
<td><pre><code>-ContentFilter {Importance -eq &#39;high&#39;}</code></pre>
<pre><code>-ContentFilter {Importance -eq 2}</code></pre></td>
</tr>
<tr class="even">
<td><p>IsFlagged</p></td>
<td><p>此屬性會傳回已由使用者或 [收件匣] 規則加上標幟的郵件。</p></td>
<td><p>布林值</p>
<p><code>$true</code> 或<code>$false</code></p></td>
<td><pre><code>-ContentFilter {IsFlagged -eq $true}</code></pre></td>
</tr>
<tr class="odd">
<td><p>IsRead</p></td>
<td><p>此屬性會傳回使用者已閱讀或未閱讀的郵件。</p></td>
<td><p>布林值</p>
<p><code>$true</code> 或<code>$false</code></p></td>
<td><pre><code>-ContentFilter {IsRead -eq $true}</code></pre></td>
</tr>
<tr class="even">
<td><p>MessageKind</p></td>
<td><p>此屬性會傳回屬於指定類型的郵件。</p></td>
<td><p>行事曆</p>
<p>Contact</p>
<p>Doc</p>
<p>Email</p>
<p>傳真</p>
<p>InstantMessage</p>
<p>日誌</p>
<p>附註</p>
<p>Post</p>
<p>RSSFeed</p>
<p>工作</p>
<p>語音信箱</p></td>
<td><pre><code>-ContentFilter {MessageKind -eq &#39;Calendar&#39;}</code></pre>
<pre><code>-ContentFilter {MessageKind -ne &#39;Email&#39;}</code></pre></td>
</tr>
<tr class="odd">
<td><p>MessageLocalee</p></td>
<td><p>此屬性會傳回屬於指定地區設定的郵件。</p></td>
<td><p>CultureInfo</p></td>
<td><pre><code>-ContentFilter {MessageLocale -ne &#39;en-US&#39;}</code></pre>
<pre><code>-ContentFilter {MessageLocale -eq &#39;tr-TR&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>Participants</p></td>
<td><p>此屬性傳回在 [收件者]、[密件副本] 或 [副本] 欄位中含有指定收件者的郵件。</p></td>
<td><p>顯示名稱</p>
<p>別名</p>
<p>SMTP 位址</p>
<p>LegacyDN</p>
<p>萬用字元</p></td>
<td><pre><code>-ContentFilter {(Participants -eq &#39;ayla@contoso.com&#39;) -or (Participants -eq &#39;tony@contoso.com&#39;)}</code></pre></td>
</tr>
<tr class="odd">
<td><p>PolicyTag</p></td>
<td><p>此屬性會傳回具有原則標記的郵件。Exchange 存放區以 GUID 來保存原則標記。因此，字串可能包含明確 GUID 值，可依 PR_POLICY_TAG 或萬用字元字串來搜尋。</p>
<p>如果指定的值不是 GUID，此命令會使用 Active Directory 資訊將名稱解析為 GUID。</p></td>
<td><p>字串</p>
<p>萬用字元</p></td>
<td><pre><code>-ContentFilter {PolicyTag -ne &#39;00000000-0000-0000-0000-000000000000&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>Received</p></td>
<td><p>此屬性會傳回已收到且具有指定收件時間戳記的郵件。</p></td>
<td><p>日期時間戳記</p></td>
<td><pre><code>-ContentFilter {Received -lt &#39;01/01/2013 9:00&#39;}</code></pre>
<pre><code>-ContentFilter {(Received -lt &#39;01/01/2013&#39;) -and (Received -gt &#39;01/01/2012&#39;)}</code></pre></td>
</tr>
<tr class="odd">
<td><p>Sender</p></td>
<td><p>此屬性會傳回從指定寄件者所收到的郵件。</p></td>
<td><p>顯示名稱</p>
<p>別名</p>
<p>SMTP 位址</p>
<p>LegacyDN</p>
<p>萬用字元</p></td>
<td><pre><code>ContentFilter {Sender -eq &#39;tony&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>Sent</p></td>
<td><p>此屬性會傳回已傳送且具有指定傳送時間戳記的郵件。</p></td>
<td><p>日期時間戳記</p></td>
<td><pre><code>-ContentFilter {Sent -lt &#39;01/01/2013 9:00&#39;}</code></pre>
<pre><code>-ContentFilter {(Sent -lt &#39;01/01/2013&#39;) -and (Sent -gt &#39;01/01/2012&#39;)}</code></pre></td>
</tr>
<tr class="odd">
<td><p>Size</p></td>
<td><p>此屬性會傳回特定大小的郵件。</p></td>
<td><p>B (位元組)</p>
<p>KB (千位元組)</p>
<p>MB (百萬位元組)</p></td>
<td><pre><code>-ContentFilter {Size -gt &#39;10KB&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>Subject</p></td>
<td><p>此屬性會傳回在郵件主旨內含有指定字串的郵件。</p></td>
<td><p>字串</p>
<p>萬用字元</p></td>
<td><pre><code>-ContentFilter {Subject -like &#39;*meeting*&#39;}</code></pre></td>
</tr>
<tr class="odd">
<td><p>To</p></td>
<td><p>此屬性會傳回在 [收件者] 欄位中包含指定收件者的已傳送郵件。</p></td>
<td><p>顯示名稱</p>
<p>別名</p>
<p>SMTP 位址</p>
<p>LegacyDN</p>
<p>萬用字元</p></td>
<td><pre><code>-ContentFilter {To -eq &#39;aylakol&#39;}</code></pre></td>
</tr>
</tbody>
</table>

