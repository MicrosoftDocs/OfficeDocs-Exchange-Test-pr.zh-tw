---
title: '外部連接器: Exchange 2013 Help'
TOCTitle: 外部連接器
ms:assetid: 21c6a7a9-f4d2-4359-9ac9-930701b63a4e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa996779(v=EXCHG.150)
ms:contentKeyID: 50472816
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 外部連接器

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-09-25_

外部連接器將郵件傳遞至伺服器或不使用 SMTP 做為其主要傳輸機制的外部系統。此範例可傳真閘道伺服器。外部連接器會使用本機或共用的放置目錄藉由檔案傳輸、 外部系統來傳送外寄郵件。Microsoft Exchange Server 2013 Mailbox server 的傳輸服務中建立外部連接器。

外部閘道伺服器可以使用傳送郵件到Exchange 2013組織的信箱伺服器的傳輸服務中存在的收取\] 目錄或重新顯示目錄。正確地格式化您複製到每個目錄的檔案送進行傳遞至Exchange信箱的電子郵件訊息。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您必須將外寄郵件傳遞給非 SMTP 系統大多數的情況下，我們建議傳遞代理程式連接器，因為他們允許之訊息的佇列管理、 訊息沒有寫入檔案系統與其他優點。<a href="delivery-agents-and-delivery-agent-connectors-exchange-2013-help.md">傳遞代理程式及傳遞代理程式連接器</a>主題提供更多詳細資料。</td>
</tr>
</tbody>
</table>


## 相關資訊

[建立外部連接器將郵件傳送至非 SMTP 傳真閘道](create-a-foreign-connector-to-deliver-messages-to-a-non-smtp-fax-gateway-exchange-2013-help.md)

[傳遞代理程式及傳遞代理程式連接器](delivery-agents-and-delivery-agent-connectors-exchange-2013-help.md)

[New-ForeignConnector](https://technet.microsoft.com/zh-tw/library/aa996310\(v=exchg.150\))

[Set-ForeignConnector](https://technet.microsoft.com/zh-tw/library/bb123789\(v=exchg.150\))

