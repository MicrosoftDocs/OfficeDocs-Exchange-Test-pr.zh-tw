---
title: '郵件編碼選項: Exchange 2013 Help'
TOCTitle: 郵件編碼選項
ms:assetid: c1d9edbb-d87c-41e5-881b-cd612d83d7e4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb310794(v=EXCHG.150)
ms:contentKeyID: 50474188
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 郵件編碼選項

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

Exchange 中的郵件編碼選項指定郵件特性，例如 MIME 和非 MIME 字元集、二進位編碼和附件格式。您可以在下列位置指定郵件編碼選項：

  - 遠端網域設定

  - 郵件使用者和郵件連絡人設定

  - Microsoft Outlook 設定
    
      - 郵件格式
    
      - 網際網路郵件格式
    
      - 網際網路收件者郵件格式
    
      - 郵件字元集編碼選項

**內容**

Message encoding options for messages sent to remote domains

Message encoding options for mail users and mail contacts

Message encoding options available in Outlook

郵件編碼選項可在 Outlook Web App

Order of precedence for message encoding options

如需詳細資訊

## 傳送至遠端網域之郵件的郵件編碼選項

當您設定遠端網域的郵件編碼選項時，傳送到該網域的所有郵件都適用特定設定。如果是組織中的遠端網域，則郵件編碼具有下列組態選項。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>設定</strong></p></td>
<td><p><strong>可在 Exchange Online Dedicated 的 EAC 中使用</strong></p></td>
<td><p><strong>可在命令介面中使用</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>MIME 字元集</strong>  您指定的字元集將只供本身沒有指定字元集的 MIME 郵件使用。設定此參數不會覆寫外寄郵件中已經指定的字元集。</p>
<p><strong>非 MIME 字元集</strong>  如果滿足下列任意一個條件，則使用此設定：</p>
<ul>
<li><p>來自遠端網域的內送郵件遺失了位於 MIME Content-Type 中的 <em>charset=</em> 設定值：標頭欄位。</p></li>
<li><p>送至遠端網域的外寄郵件遺失 MIME 字元集的值。</p></li>
</ul>
<p></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><strong>內容類型</strong>  您可以針對傳送到遠端網域之收件者的 MIME 郵件指定內容類型。您可以使用下列設定：</p>
<ul>
<li><p><strong>MimeHtmlText</strong>  除非原始郵件是文字郵件，否則所有郵件都會轉換成使用 HTML 格式的 MIME 郵件。如果原始郵件是文字郵件，則外寄郵件就會是使用文字格式的 MIME 郵件。這是預設設定。</p></li>
<li><p><strong>MimeText</strong>  所有郵件都會轉換成使用文字格式的 MIME 郵件。</p></li>
<li><p><strong>MimeHtml</strong>  所有郵件都會轉換成使用 HTML 格式的 MIME 郵件。</p></li>
</ul></td>
<td><p>否</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><strong>自動換行大小</strong>  您可以指定電子郵件內文中一行文字的字元數上限。較舊的電子郵件用戶端應用程式可能偏好一行 78 個字元。此選項只能透過命令介面使用。</p>
<p></p></td>
<td><p>否</p></td>
<td><p>是</p></td>
</tr>
</tbody>
</table>


回到頁首

## 郵件使用者與郵件連絡人的郵件編碼選項

當您設定郵件連絡人或郵件使用者的郵件編碼選項時，該選項會套用到所有傳送給該特定收件者的郵件。如果是組織中的郵件連絡人及郵件使用者，則郵件編碼有下列組態選項：

  - **UsePreferMessageFormat**  此參數會指定是否以針對郵件連絡人所設定的郵件格式設定，覆寫針對遠端網域所設定的全域設定。如果您停用該設定，Exchange 將忽略此收件者的其他郵件編碼選項，而郵件編碼將由遠端網域的組態或郵件寄件者的設定進行判斷。

  - **MessageFormat**  此參數會指定郵件格式。您可以將 Text 或 Mime 指定為郵件格式。此設定的值取決於 *MessageBodyFormat* 參數。如果郵件內文格式是 Html 或 TextAndHtml，則此參數必須設為 Mime。

  - **MessageBodyFormat**  此參數會指定郵件內文格式。您可以指定 Text、Html 或 TextAndHtml。此設定的值取決於 *MessageFormat* 參數。如果郵件格式是 Text，則此參數也必須設為 Text。

  - **MacAttachmentFormat**  此參數會針對郵件指定 Apple Macintosh 作業系統附件格式。您可以指定 BinHex、UuEncode、AppleSingle 或 AppleDouble。此設定的值取決於 *MessageFormat* 參數。如果郵件格式設為 Text，則此參數必須設為 BinHex 或 UuEncode。如果郵件格式設為 Mime，則此參數必須設為 BinHex、AppleSingle 或 AppleDouble。

您需要使用 Exchange 管理命令介面中的上述參數，以設定郵件使用者與郵件連絡人的郵件編碼選項。如需詳細資訊，請參閱下列主題：

  - [Enable-MailContact](https://technet.microsoft.com/zh-tw/library/aa996001\(v=exchg.150\))

  - [New-MailContact](https://technet.microsoft.com/zh-tw/library/bb124519\(v=exchg.150\))

  - [Set-MailContact](https://technet.microsoft.com/zh-tw/library/aa995950\(v=exchg.150\))

  - [Enable-MailUser](https://technet.microsoft.com/zh-tw/library/aa996549\(v=exchg.150\))

  - [New-MailUser](https://technet.microsoft.com/zh-tw/library/aa996335\(v=exchg.150\))

  - [Set-MailUser](https://technet.microsoft.com/zh-tw/library/aa995971\(v=exchg.150\))

回到頁首

## 在 Outlook 中可用的郵件編碼選項

作為寄件者，您可以在下列任意階段從 Outlook 中指定郵件編碼選項：

  - 將預設郵件格式設定為純文字或 HTML。

  - 使用 \[選項\] 索引標籤的 \[格式\] 區域，將您正在撰寫的郵件格式設為純文字或 HTML。

  - 為傳送至 Exchange 組織外之所有收件者的郵件設定郵件編碼選項。這些選項稱為*網際網路郵件格式*選項。這些選項只適用於遠端收件者，不適用於 Exchange 組織內的收件者。

  - 為傳送至 Exchange 組織外之特定收件者的郵件設定郵件編碼選項。這些選項稱為*網際網路收件者郵件格式*選項。這些選項只適用於 \[連絡人\] 資料夾中的遠端收件者，不適用於 Exchange 組織內的收件者。

Outlook 預設會使用自動字元集郵件編碼，其作法為掃描外寄郵件全文以決定要用於郵件的適當編碼。此設定會套用至您傳送至網際網路收件者及 Exchange 組織收件者的郵件。不過，您可以略過此動作，並針對外寄郵件指定慣用編碼。

回到頁首

## 在 Outlook Web App 中可用的郵件編碼選項

作為寄件者，您可以在下列任意階段從 Outlook Web App 中指定郵件編碼選項：

  - 在 \[設定\] \> \[選項\] \> \[設定\] 頁面的 \[郵件格式\] 區段中，將預設郵件格式設定為純文字或 HTML。

  - 使用 \[更多選項\] (…) 功能表，並選取 \[切換至純文字\] 或 \[切換至 HTML\]，將您正在撰寫的郵件格式設為純文字或 HTML。

回到頁首

## 郵件編碼選項的優先順序

Exchange 會使用下列清單所述的優先順序，決定傳送至 Exchange 組織外收件者之外寄郵件的郵件編碼選項：

1.  遠端網域設定

2.  Outlook 或 Outlook Web App 設定

3.  郵件使用者或郵件連絡人設定

此清單由低至高指定優先順序。較高等級的設定可覆寫較低等級的設定。

下表說明郵件字元集編碼選項的優先順序，從最低優先順序到最高優先順序。

### 郵件字元集編碼選項的優先順序，從最低優先順序到最高優先順序

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>來源</th>
<th>參數</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>使用 EAC 或 <strong>Set-RemoteDomain</strong> 進行遠端網域項目設定</p></td>
<td><p><em>CharacterSet</em></p></td>
<td><p>已指定</p></td>
</tr>
<tr class="even">
<td><p>使用 EAC 或 <strong>Set-RemoteDomain</strong> 進行遠端網域項目設定</p></td>
<td><p><em>NonMimeCharacterSet</em></p></td>
<td><p>已指定</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 設定</p></td>
<td><p>郵件字元集編碼</p></td>
<td><ul>
<li><p>自動選取</p></li>
<li><p>已指定</p></li>
</ul></td>
</tr>
</tbody>
</table>


當您為遠端網域設定非 MIME 字元集時，系統會將該字元集指派給下列類型的郵件：

  - 送至所設定之遠端網域且不含指定字元集的外寄郵件。

  - 來自所設定之遠端網域且不含指定字元集的內送郵件。

傳輸伺服器之 Windows ANSI 字碼頁的值可用於指定下列郵件類型的字元集：

  - 不含指定字元集的內部郵件。

  - 含有指定字元集但不含指定伺服器字碼頁的內部郵件。

如果郵件含有的指定字元集無效，則傳輸伺服器會嘗試以有效的字元集來取代無效的字元集。

下表說明純文字郵件編碼選項的優先順序，從最低優先順序到最高優先順序。

### 純文字郵件編碼選項的優先順序，從最低優先順序到最高優先順序

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>來源</th>
<th>參數</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-RemoteDomain</strong></p></td>
<td><p><em>LineWrapSize</em></p></td>
<td><ul>
<li><p>從 0 到 132</p></li>
<li><p>不限</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Outlook 設定</p></td>
<td><p>郵件格式</p></td>
<td><p>純文字</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 設定</p></td>
<td><p>網際網路郵件格式</p></td>
<td><p>純文字選項：</p>
<ul>
<li><p>傳送純文字郵件時使用 UuEncode 格式將附件編碼</p></li>
<li><p>以 <em>nn</em> 個字元自動進行文字換行</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Outlook 設定</p></td>
<td><p>網際網路收件者郵件格式</p></td>
<td><p>純文字格式：</p>
<ul>
<li><p>使用 UuEncode 附件格式將附件編碼</p></li>
<li><p>使用 BinHex Mac 附件格式</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>UsePreferMessageFormat</em></p></td>
<td><ul>
<li><p><code>$true</code></p></li>
<li><p><code>$false</code></p></li>
</ul>
<p>若值為 <code>$false</code> 或者若收件者並未定義為 Exchange 組織中的郵件使用者或郵件連絡人，則會忽略郵件使用者或郵件連絡人設定。</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MessageFormat</em></p></td>
<td><p>文字</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MessageBodyFormat</em></p></td>
<td><p>文字</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MacAttachmentFormat</em></p></td>
<td><ul>
<li><p>BinHex</p></li>
<li><p>UuEncode</p></li>
</ul></td>
</tr>
</tbody>
</table>


下表說明 MIME 郵件編碼選項的優先順序，從最低優先順序到最高優先順序。

### MIME 郵件編碼選項的優先順序，從最低優先順序到最高優先順序

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>來源</th>
<th>參數</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-RemoteDomain</strong></p></td>
<td><p><em>ContentType</em></p></td>
<td><ul>
<li><p><code>MimeHtmlText</code></p></li>
<li><p><code>MimeText</code></p></li>
<li><p><code>MimeHtml</code></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Outlook 或 Outlook Web App 設定</p></td>
<td><p>郵件格式</p></td>
<td><ul>
<li><p>純文字</p></li>
<li><p>HTML</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Outlook 設定</p></td>
<td><p>網際網路收件者郵件格式</p></td>
<td><p>MIME 郵件格式</p>
<ul>
<li><p>純文字</p></li>
<li><p>同時包含純文字與 HTML</p></li>
<li><p>HTML</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>UsePreferMessageFormat</em></p></td>
<td><p><code>$true</code></p>
<p><code>$false</code></p>
<p>若值為 <code>$false</code> 或者若收件者並未定義為 Exchange 組織中的郵件使用者或郵件連絡人，則會忽略郵件使用者或郵件連絡人設定。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MessageFormat</em></p></td>
<td><ul>
<li><p>文字</p></li>
<li><p>MIME</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MessageBodyFormat</em></p></td>
<td><ul>
<li><p><code>Text</code></p></li>
<li><p><code>Html</code></p></li>
<li><p><code>TextAndHtml</code></p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MacAttachmentFormat</em></p></td>
<td><ul>
<li><p>BinHex</p></li>
<li><p>AppleSingle</p></li>
<li><p>AppleDouble</p></li>
</ul></td>
</tr>
</tbody>
</table>


回到頁首

## 相關資訊

[郵件編碼選項](message-encoding-options-exchange-2013-help.md)

[TNEF 轉換選項](tnef-conversion-options-exchange-2013-help.md)

[遠端網域](remote-domains-exchange-2013-help.md)

[Exchange Online 中的遠端網域](https://technet.microsoft.com/zh-tw/library/jj966211\(v=exchg.150\))

[管理郵件使用者](manage-mail-users-exchange-2013-help.md)

[管理郵件連絡人](manage-mail-contacts-exchange-2013-help.md)

[在 Outlook 中的郵件格式變更](https://go.microsoft.com/fwlink/p/?linkid=397890)

