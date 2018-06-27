---
title: '依 Exchange 搜尋編製索引編製郵件內容: Exchange 2013 Help'
TOCTitle: 依 Exchange 搜尋編製索引編製郵件內容
ms:assetid: a9754dc1-44aa-4076-8b59-a5d39246d5b0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ983804(v=EXCHG.150)
ms:contentKeyID: 52062575
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 依 Exchange 搜尋編製索引編製郵件內容

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2015-04-17_

Exchange 搜尋可將許多項目內容編制為索引，包括電子郵件的寄件者、收件者、郵件內文和附件。

## 依 Exchange 搜尋編制索引的內容

下表包括依 Exchange 搜尋編制索引的所有項目內容清單。


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
<th>屬性</th>
<th>類型</th>
<th>可查詢</th>
<th>可搜尋</th>
<th>可擷取</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Account</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>Assistantname</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>Attachment</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>Attachmentfilenames</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>Attachmentmetaproperties</p></td>
<td><p>字串</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>Attachmentcount</p></td>
<td><p>整數</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>Bcc</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>Body</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>Businessaddress</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>Businessmainphone</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>Businessphonenumber</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>Carphonenumber</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>類別</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>Cc</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>Companyname</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>Compositeitemid</p></td>
<td><p>字串</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>Conversationid</p></td>
<td><p>整數</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>Conversationtopic</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>Departmentname</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>Displayname</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>Displaynameprefix</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>Documentid</p></td>
<td><p>整數</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>Emailaddress</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>Emaildisplayname</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>Emailoriginaldisplayname</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>Errorcode</p></td>
<td><p>整數</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>Fileas</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>Firstname</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>Folderid</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>From</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>Homeaddress</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>Homephone</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>Importance</p></td>
<td><p>整數</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>Ispartiallyprocessed</p></td>
<td><p>布林值</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>Ispermanentfailure</p></td>
<td><p>布林值</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>Itemclass</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>Kind</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>Lastattempttime</p></td>
<td><p>DateTime</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>Lastname</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>Mailboxguid</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>Manager</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>Meetinglocation</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>Middlename</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>Mobilephonenumber</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>Nickname</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>Officelocation</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>Otheraddress</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>Participants</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>Primarytelephonenumber</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>Received</p></td>
<td><p>DateTime</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>Receivedby</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>Receivedrepresenting</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>Recipients</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>Sent</p></td>
<td><p>DateTime</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>Sharinginfo</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>Size</p></td>
<td><p>整數</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>Subject</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>Tasktitle</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>Title</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>To</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>Umaudionotes</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>Watermark</p></td>
<td><p>整數</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>Yomicompanyname</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>Yomifirstname</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>Yomilastname</p></td>
<td><p>字串</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
</tbody>
</table>


**索引化內容的備註：**

  - **設為可查詢的屬性**可用於搜尋用戶端等Outlook Web App`property:value`成對，例如`from:bsuneja@cotoso.com`AQS 查詢。就地 ediscovery （英文） 也在搜尋查詢中使用上表所列的設為可查詢屬性的子集。如需這些屬性的清單，請參閱[郵件內容和搜尋運算子就地 ediscovery （英文）](message-properties-and-search-operators-for-in-place-ediscovery-exchange-2013-help.md)。

  - **可搜尋的內容**是不能在`property:value`配對中指定的屬性，但如果關鍵字搜尋會傳回值中任何可搜尋的屬性。例如，您無法使用`body:Contoso`搜尋字串`contoso`郵件本文中。不過，該字串的搜尋將傳回的所有項目任何可搜尋的屬性中找到的屬性。

  - **可擷取內容**，如 `documenteid` 和 `ispartiallyprocessed`，每次搜尋都會傳回。

