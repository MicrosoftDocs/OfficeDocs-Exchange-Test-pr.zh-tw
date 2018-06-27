---
title: '接收連接器的權限: Exchange 2013 Help'
TOCTitle: 接收連接器的權限
ms:assetid: 31af7139-6823-411b-81b3-e42edd83ee6c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ673053(v=EXCHG.150)
ms:contentKeyID: 50472803
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 接收連接器的權限

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-07_

下表列出權限類型以及每個類型的描述。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>接收連接器權限</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ms-Exch-SMTP-Submit</p></td>
<td><p>工作階段必須授與此權限或就無法提交郵件到這個接收連接器。如果工作階段都不會有此權限，MAIL FROM 及驗證命令將會失敗。</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-SMTP-Accept-Any-Recipient</p></td>
<td><p>此權限允許透過此連接器轉送訊息工作階段。如果不授與此權限，此連接器可接受定址給公認的網域中的收件者的郵件。</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-SMTP-Accept-Any-Sender</p></td>
<td><p>此權限允許工作階段略過寄件者地址詐騙檢查。</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-SMTP-Accept-Authoritative-Domain-Sender</p></td>
<td><p>此權限允許電子郵件地址位於授權網域的寄件者建立到此接收連接器的工作階段。</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-SMTP-Accept-Authentication-Flag</p></td>
<td><p>此權限可讓Exchange 2003伺服器來送出來自內部寄件者的郵件。Exchange 2010會看到郵件為 internal。寄件者可以宣告為受信任的郵件。輸入Exchange系統透過匿名送出的郵件將轉送到Exchange組織與此旗標不受信任的狀態。</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Accept-Headers-Routing</p></td>
<td><p>此權限允許送出有所有接收標頭不變的郵件工作階段。如果不授與此權限，伺服器會除去所有接收標頭。</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Accept-Headers-Organization</p></td>
<td><p>此權限允許送出有所有組織標頭不變的郵件工作階段。所有開頭<strong>X-MS-Exchange-Organization-</strong>組織標頭。如果不授與此權限，接收伺服器會刪除所有組織標頭。</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Accept-Headers-Forest</p></td>
<td><p>此權限允許送出有所有樹系標頭不變的郵件工作階段。所有開頭<strong>X-MS-Exchange-Forest-</strong>樹系標頭。如果不授與此權限，接收伺服器會刪除所有樹系標頭。</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Accept-Exch50</p></td>
<td><p>此權限可讓工作階段提交含有 XEXCH50 命令的訊息。此命令需要與Exchange 2003的互通性。XEXCH50 命令提供郵件資料如垃圾郵件信賴等級 (SCL)。</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Bypass-Message-Size-Limit</p></td>
<td><p>此權限允許工作階段提交超過為連接器設定之郵件大小限制的郵件。</p></td>
</tr>
<tr class="odd">
<td><p>Ms-Exch-Bypass-Anti-Spam</p></td>
<td><p>此權限允許工作階段略過反垃圾郵件篩選。</p></td>
</tr>
</tbody>
</table>

