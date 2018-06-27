---
title: '傳送連接器: Exchange 2013 Help'
TOCTitle: 傳送連接器
ms:assetid: 6aa19a12-c7b2-4eac-a8dc-9a4d26919ac5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa998662(v=EXCHG.150)
ms:contentKeyID: 50473396
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 傳送連接器

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-15_

在 Microsoft Exchange Server 2013、 傳送連接器會控制來接收伺服器的輸出郵件流程。他們是執行的傳輸服務的 Mailbox server 上設定。最常您設定傳送到智慧主機或直接使用 DNS 其收件者的外寄電子郵件的傳送連接器。

Exchange 2013執行的傳輸服務的 mailbox server 需要傳送連接器將郵件傳送至其目的地的方式在下一個躍點。傳送連接器在信箱伺服器上建立儲存在Active Directory以及可用來在組織中執行的傳輸服務的所有信箱伺服器。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您部署Exchange 2013時，輸出郵件流程不可以設定路由外寄郵件傳送至網際網路的傳送連接器之前發生。如需詳細資訊，請參閱<a href="create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md">建立電子郵件傳送至網際網路的傳送連接器</a>。</td>
</tr>
</tbody>
</table>


## 選取 \[傳送連接器類型

通常您建立的傳送連接器的**郵件流程**\] 區段中的 Exchange 系統管理中心 (EAC)。當您建立新的傳送連接器時，您可以選擇適用於您連線的案例提供**類型**。此類型會決定連接器已指派的預設權限組與這些權限授與信任的安全性主體。安全性主體包括使用者、 電腦和安全性群組。

說明特定**類型**的選項的程序包括[建立傳送連接器路由傳送到智慧主機的外寄電子郵件](create-a-send-connector-to-route-outbound-email-through-a-smart-host-exchange-2013-help.md)和[建立協力廠商，套用傳輸層安全性 (TLS) 傳送電子郵件的傳送連接器](create-a-send-connector-to-send-email-to-a-partner-with-transport-layer-security-tls-applied-exchange-2013-help.md)。

在您偏好使用Exchange eac 管理命令介面，您可以建立的傳送連接器與使用[New-SendConnector](https://technet.microsoft.com/zh-tw/library/aa998936\(v=exchg.150\))指令程式來指定類型。

## Exchange 2013中新的傳送連接器功能

具有 Client Access server 上的 Front End Transport 服務和傳輸之間的關係Exchange 2013中的信箱伺服器上的服務會開始新的傳送連接器的行為。首先，您可以設定的傳送連接器路由傳送輸出郵件透過前端傳輸伺服器中本機的 Active Directory 站台，藉由[Set-SendConnector](https://technet.microsoft.com/zh-tw/library/aa998294\(v=exchg.150\))指令程式的*FrontEndProxyEnabled*參數的信箱伺服器傳輸服務中因此中的電子郵件路由的傳輸服務中的如何合併。[郵件路由](mail-routing-exchange-2013-help.md)提供傳輸服務、 路由行為和Exchange 2013中的目的地的詳細資訊。[郵件流程](mail-flow-exchange-2013-help.md)提供傳輸管線概觀和每個傳輸服務的說明。

*IsCoexistenceConnector*參數已被取代。在大多數情況下，當您想要設定混合式環境，您的信箱部分裝載在哪裡內部和部分裝載在雲端中，我們建議您使用混合組態精靈\]。

*LinkedReceiveConnector*已被取代。此參數用來建立無法郵件路由傳送至協力廠商反垃圾郵件服務，例如的連接器。現在，在大多數情況下，您路由傳送郵件到您的反垃圾郵件服務藉由您的 MX 記錄和連結連接器行為不需要。

預設值的郵件大小上限， *MaxMessageSize*參數所指定具有從 10 MB 增加到 25 MB。[Set-SendConnector](https://technet.microsoft.com/zh-tw/library/aa998294\(v=exchg.150\))提供如何設定參數的傳送連接器的詳細資訊。

已新增*TlsCertificateName* 。它用來驗證本機憑證用於輸出連線和詐騙憑證的風險降至最低。

