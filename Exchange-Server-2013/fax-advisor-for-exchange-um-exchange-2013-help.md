---
title: '傳真 advisor Exchange UM: Exchange Online Help'
TOCTitle: 傳真 advisor Exchange UM
ms:assetid: 928a466d-cc0c-4160-bd4c-f0fc76b038d4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee364747(v=EXCHG.150)
ms:contentKeyID: 52062372
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 傳真 advisor Exchange UM

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2016-12-09_

Microsoft整合通訊 (UM) 依賴認證的傳真協力廠商解決方案的增強的傳真功能，例如外寄傳真或傳真路由。根據預設，使用者未設定為允許傳遞給已啟用 UM 之使用者的傳入傳真訊息。Exchange 伺服器會將傳真要求傳送到認證的傳真協力廠商解決方案。傳真協力程式伺服器會接收傳真資料，然後傳送給電子郵件中的收件者的信箱與為.tif 附件包含傳真。如需詳細資訊，請參閱[啟用語音信箱使用者接收傳真](enable-voice-mail-users-to-receive-faxes-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>我們建議在規劃部署整合通訊的所有客戶都取得協助的整合通訊的專員。整合通訊的專員可協助您確保已順利地轉換至 [整合通訊從舊版的語音郵件系統。執行新部署或升級舊版的語音郵件系統需要 Pbx 和整合通訊相關的重要知識。更多如何連絡 Unified Messaging 專員的相關資訊，如<a href="http://go.microsoft.com/fwlink/p/?linkid=262708">Microsoft Exchange Server 2013 整合通訊 (UM) 專家</a>或<a href="https://go.microsoft.com/fwlink/p/?linkid=261951">Microsoft Pinpoint 整合通訊</a>。</td>
</tr>
</tbody>
</table>


## Exchange 整合通訊傳真協力程式

若要成為傳真協力程式認證的交互操作必須使用與 Exchange UM、 協力廠商必須實作傳真協力廠商的互通性規格中所包含的需求和獨立的憑證廠商必須認證的傳真解決方案。如需認證傳真產品使用 Exchange Unified Messaging 的詳細資訊，要求提交至[傳真協力廠商的整合通訊](mailto:fax-part@microsoft.com)。

## 通過與整合通訊交互操作認證的傳真協力程式解決方案

如果您已將部署 Exchange 整合通訊並尋找傳真協力程式可讓您的組織的傳入傳真\]，請參閱[Microsoft Pinpoint 傳真協力廠商](https://go.microsoft.com/fwlink/p/?linkid=190238)。這些軟體廠商已為互通與 Exchange Server 已認證並整合通訊的認證的軟體解決方案。

## VoIP、媒體閘道和 IP PBX 支援

正確設定貴組織如 VoIP 閘道是必須先完成已成功部署 Exchange 整合通訊與傳入傳真很難部署工作。若要協助回答問題並取得最新的 VoIP 閘道組態資訊，請參閱[Exchange 2013 的電話語音 advisor](telephony-advisor-for-exchange-2013-exchange-2013-help.md)。[支援 VoIP 閘道、 IP Pbx 和 Pbx 組態注意事項](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)提供 VoIP 閘道組態注意事項和您必須正確設定貴組織的 VoIP 閘道、 IP Pbx 和 Sbc 使用 Exchange 整合通訊的檔案。

現在已與Microsoft Unified Communications 開啟互通性計劃與 VoIP 閘道的 Exchange 整合通訊互通性測試。如需詳細資訊，請參閱[Microsoft Unified Communications 開啟互通性計劃](http://go.microsoft.com/fwlink/p/?linkid=140722)。

適用 VoIP 閘道和 IP PBX 的 [Microsoft Unified Communications Open Interoperability Program](http://go.microsoft.com/fwlink/p/?linkid=140722) 資格計畫，確保客戶在搭配使用合格的電話語音閘道和 IP-PBX 與 Microsoft Unified Communications 軟體時，擁有完美無缺的安裝和支援體驗。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在整合了整合通訊和 Communications Server 2007 R2 或 Microsoft Lync Server 的環境中，不支援使用 T.38 或 G.711 來傳送及接收傳真。</td>
</tr>
</tbody>
</table>


## 部署和設定傳真

UM 轉寄至專用的傳真協力廠商解決方案，然後建立傳真寄件者的傳真呼叫並接收代表已啟用 UM 之使用者的傳真傳入傳真呼叫。不過，若要允許已啟用 UM 的使用者接收傳真訊息在他們的信箱，必須設定傳真協力廠商伺服器上，及則設定 UM 撥號對應表、 UM 信箱原則，並啟用 UM 功能的使用者接收傳真\]。如需詳細資訊，請參閱[設定傳入傳真](setting-up-incoming-faxing-exchange-2013-help.md)。

