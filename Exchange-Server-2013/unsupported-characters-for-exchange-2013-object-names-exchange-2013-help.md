---
title: '不支援的字元的 Exchange 2013 物件名稱: Exchange 2013 Help'
TOCTitle: 不支援的字元的 Exchange 2013 物件名稱
ms:assetid: 76fa4e23-f0f6-473b-9227-70ded907578f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn169553(v=EXCHG.150)
ms:contentKeyID: 54652591
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 不支援的字元的 Exchange 2013 物件名稱

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

本文說明您無法在Exchange 2013中的物件或元件名稱中使用的字元。當您在Exchange 2013中建立的物件或元件的名稱時，名稱不能包含不支援的字元，即使您可以建立物件並使用不受支援的字元。此外，如果您嘗試匯入或連線至其名稱中含有不受支援的字元物件，您可能會收到錯誤訊息或發生未預期的行為。

## 不支援的字元

下表列出不支援使用於 Exchange 相關物件或元件名稱的字元。 該表格亦列出使用不支援的字元時可能發生問題的案例。 請注意，該表格列出的每一個物件的最大長度是 64 個字元。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange 物件或元件</th>
<th>Exchange 案例</th>
<th>不支援的字元</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>電子郵件網域名稱</p></td>
<td><p>簡易郵件傳送通訊協定 (SMTP) 連接器</p></td>
<td><p><code>~ ` ! @ # $ % ^ &amp; * ( ) + = { } | [ ] \ : &quot; ; &lt; &gt; , . ? /</code></p></td>
</tr>
<tr class="even">
<td><p>連接器位址空間的主機名稱</p></td>
<td><p>郵件流程</p></td>
<td><p><code>..</code> (兩個句點)</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server 的主機名稱</p></td>
<td><p>SMTP</p></td>
<td><p><code>_</code> (底線)</p></td>
</tr>
<tr class="even">
<td><p>組織或站台名稱</p></td>
<td><p>執行安裝程式或移動信箱</p></td>
<td><p><code>~ ` ! @ # $ % ^ &amp; * ( ) _ + = { } | [ ] \ : &quot; ; '  &lt; &gt; , . ? /</code></p></td>
</tr>
<tr class="odd">
<td><p>組織內部目錄名稱</p></td>
<td><p>Directory</p></td>
<td><p><code>~ ` ! @ # $ % ^ &amp; * ( ) _ + = { } | [ ] \ : &quot; ; '  &lt; &gt; , . ? /</code></p></td>
</tr>
<tr class="even">
<td><p>公用資料夾樹狀目錄名稱</p></td>
<td><p>檢視和建立公用資料夾</p></td>
<td><p><code>: ;</code></p></td>
</tr>
<tr class="odd">
<td><p>收件者名稱</p></td>
<td><p>SMTP</p></td>
<td><p><code>' &quot;</code></p></td>
</tr>
<tr class="even">
<td><p>收件者原則 SMTP 位址</p></td>
<td><p>檢視公用資料夾階層</p></td>
<td><p><code>~ ` ! @ # $ % ^ &amp; * ( ) + = { } | [ ] \ : &quot; ; &lt; &gt; , . ? /</code></p></td>
</tr>
<tr class="odd">
<td><p>收件者原則 SMTP 位址主機名稱</p></td>
<td><p>郵件流程</p></td>
<td><p><code>..</code> (兩個句點)</p></td>
</tr>
<tr class="even">
<td><p>站台內部目錄名稱</p></td>
<td><p>檢視公用資料夾階層</p></td>
<td><p><code>? ( ) *</code></p></td>
</tr>
<tr class="odd">
<td><p>智慧主機名稱</p></td>
<td><p>SMTP</p></td>
<td><p>前端或尾端空格</p></td>
</tr>
</tbody>
</table>

