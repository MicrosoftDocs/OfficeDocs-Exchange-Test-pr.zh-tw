---
title: 'UM 通訊協定、 連接埠和服務: Exchange 2013 Help'
TOCTitle: UM 通訊協定、 連接埠和服務
ms:assetid: 5997ce29-1755-48bb-8ff4-b08da549482a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa998265(v=EXCHG.150)
ms:contentKeyID: 54652585
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# UM 通訊協定、 連接埠和服務

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2015-03-09_

Microsoft Exchange 2013整合通訊 (UM) 要求數個 TCP 及使用者資料包通訊協定 (UDP) 的連接埠用來建立伺服器執行Exchange 2013和其他裝置之間的通訊。藉由允許存取透過這些 IP 連接埠，您啟用整合通訊以正常運作。本主題討論Exchange 2013中所使用的 TCP 及 UDP 連接埠整合通訊。

## 整合的通訊的通訊協定和服務

Exchange 2013整合通訊功能與服務依賴靜態及動態 TCP 及 UDP 連接埠以確保正確作業執行 Microsoft Exchange Unified Messaging Call Router 服務的用戶端存取伺服器與執行 Microsoft Exchange 整合通訊服務的 Mailbox server。Exchange 2013安裝時，即會為Exchange新增靜態輸入的Windows防火牆規則。如果您變更用戶端存取和信箱伺服器所使用的 TCP 連接埠，則您可能需要重新設定Windows防火牆規則，以允許整合通訊才能正常運作。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在Exchange 2013用戶端存取和信箱執行 UM 元件和服務的伺服器、 Exchange 安裝程式會建立內送的防火牆規則的允許沒有任何 TCP 連接埠限制的輸入的通訊。新增 UM 服務的下列輸入的規則：</td>
</tr>
</tbody>
</table>


1.  **SESWorker (GFW) (TCP-In)**

2.  **UMCallRouter (GFW) (Tcp-in)**

3.  **UMCallRouter (Tcp-in)**

4.  **UMService (GFW) (TCP-In)**

5.  **Umservice 所 (Tcp-in)**

6.  **UMWorkerProcess – RPC (Tcp-in)**

7.  **UMWorkerProcess (GFW) (TCP-In)**

8.  **UMWorkerProcess (Tcp-in)**

## 工作階段初始通訊協定

工作階段初始通訊協定 (SIP) 是用於起始、 修改及結束涉及多媒體元素，例如視訊、 語音、 立即訊息、 線上遊戲及虛擬現實互動式使用者工作階段的通訊協定。它是其中一個語音訊號通訊協定 over IP (VoIP) 以及 H.323 前置字元。大部分 VoIP 標準為基礎的方案使用 H.323 或 SIP。不過，數種專屬的設計和通訊協定亦存在於。VoIP 通訊協定通常支援的功能，例如等待會議通話的電話和電話轉接。

如 VoIP 閘道和 IP 專用交換機 (Pbx) 的 SIP 用戶端可以連線至 SIP 伺服器，包括用戶端存取伺服器執行 Microsoft Exchange Unified Messaging Call Router 服務使用 TCP 及 UDP 連接埠 5060。SIP 僅用於設定及分裂向下語音或視訊通話。所有的語音和視訊通訊發生透過即時傳輸通訊協定 (RTP)。

## 即時傳輸通訊協定

RTP 定義透過特定的網路，例如網際網路傳遞音訊及視訊的標準封包格式。RTP 透過網路執行僅語音/視訊資料。通話設定與清除通常是由 SIP 執行。

RTP 不需要標準或靜態 TCP 或 UDP 連接埠與通訊。RTP 通訊發生偶數 UDP 連接埠上及下一個較高奇數號碼連接埠用於 TCP 通訊。雖然不標準的連接埠範圍指派 RTP 通常會設定為使用連接埠介於 1024年和 65535 並執行 \[Microsoft Exchange 整合通訊服務追蹤此慣例的信箱伺服器。很難的 RTP 周遊防火牆，因為它會使用動態連接埠範圍。

## 整合通訊的 Web 服務

在信箱伺服器上安裝整合通訊的 Web 服務使用 IP 的用戶端、 信箱伺服器與執行其他Exchange 2013伺服器角色的電腦之間的網路通訊。數個Exchange 2013Outlook Web App和Outlook 2013用戶端功能依賴正常運作的整合通訊的 Web 服務。

下列整合通訊用戶端功能依賴整合通訊的 Web 服務：

  - 語音郵件選項可用的Exchange 2013Outlook Web App，包括電話功能與能力重設 PIN 上的播放。

  - 在 Outlook 用戶端中找到的 Phone 功能上播放。

## UM 連接埠

用戶端存取伺服器上找到的 Microsoft Exchange Unified Messaging Call Router 服務會使用 SIP over 傳輸控制通訊協定 (TCP) 或共同通訊正在執行 Microsoft Exchange 整合通訊服務的 Mailbox server 的傳輸層安全性 (相互 TLS)。若要避免 TCP/使用者資料包通訊協定 (UDP) 連接埠衝突，Microsoft Exchange Unified Messaging Call Router 服務和 Microsoft Exchange 整合通訊服務預設值並在不同的 TCP 連接埠上接聽。它們可接受兩者不安全模式和安全連線\] 中，根據相互 TLS 是否用於 SIP 和 RTP 流量。根據預設，用戶端存取伺服器會接聽的這兩個 TCP 通訊埠 5060 不安全模式和 SIP 安全模式中的 TCP 連接埠 5061 上的 SIP 要求時使用相互 TLS。這些連接埠都可使用**Set-UMCallRouterSettings**指令程式。用戶端存取伺服器上的 Microsoft Exchange Unified Messaging Call Router 服務不會處理媒體 （RTP 或 SRTP） 流量，因此皆會使用唯一的 TCP 連接埠及 UDP 連接埠。根據預設，在信箱伺服器會接聽的這兩個 TCP 連接埠 5062 不安全模式和 TCP 連接埠 5063 SIP 安全模式中的 SIP 要求時相互 TLS 用。這些連接埠都可使用 Exchange 管理命令介面 cmdlet。Microsoft Exchange 整合通訊服務的 Mailbox server 上會接受來自 5062 和 5063 的 SIP 連接埠上的用戶端存取伺服器的連線。用戶端存取伺服器會 SIP 要求重新導向至信箱伺服器之後，使用 VoIP 閘道、 IP PBX 或 SBC，以及 Microsoft Exchange 整合通訊工作者處理序的信箱伺服器上建立 RTP 或 SRTP 媒體通道。

下列表格概述 Exchange 2013 埠及協定，以及這些連接埠是否能變更。

### UM 聽候連接埠

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>通訊協定</th>
<th>TCP 連接埠</th>
<th>UDP 連接埠</th>
<th>連接埠是否可以變更？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SIP （用戶端存取伺服器 – Microsoft Unified Messaging Call Router 服務）</p></td>
<td><p>5060 （不安全） 5061 （安全）。這兩個連接埠上接聽此服務。</p></td>
<td><p>不適用</p></td>
<td><p>是的，使用<strong>Set-UMCallRouterSettings</strong> 指令程式。</p></td>
</tr>
<tr class="even">
<td><p>SIP (信箱伺服器 — Microsoft Exchange Unified Messaging )</p></td>
<td><p>5062 （不安全） 5063 （安全）。這兩個連接埠上接聽此服務。</p></td>
<td><p>不適用</p></td>
<td><p>無法變更連接埠。</p></td>
</tr>
<tr class="odd">
<td><p>SIP (信箱伺服器-- UM 工作者處理程序)</p></td>
<td><p>5065 和 5067 tcp （無安全性）。5065 和 5067 的相互 TLS （安全）。如果您已將它設為雙模式 5066 而且也會用 5068。</p></td>
<td><p>不適用</p></td>
<td><p>無法變更連接埠。</p></td>
</tr>
<tr class="even">
<td><p>RTP (信箱箱伺服器 - UM 工作者處理程序)</p></td>
<td><p>不適用</p></td>
<td><p>1024 與 65535 之間的連接埠。</p></td>
<td><p>可以 msexchangeum.config 設定檔中變更連接埠。Msexchangeum.config 檔案位於 Exchange 2013 Unified Messaging server 上的 [\Program Files\Microsoft\Exchange\V15\bin] 資料夾。</p></td>
</tr>
</tbody>
</table>


## Lync Server 和 UM 連接埠

Exchange 2013整合的通訊支援網路位址轉譯 (NAT) 周遊和信箱伺服器的 RTP 媒體允許以透過 NAT 防火牆通道。不過，針對此工作，您也必須 Microsoft Office Communications Server 2007 R2 和 Microsoft Lync Server 2010 或Microsoft Lync 2013環境中部署。如果您要部署同時Exchange 2013和 Communications Server 2007 R2 或 Microsoft Lync Server 2010 或Lync 2013網路上，此部署可讓執行 Microsoft Exchange Unified Messaging 服務以通訊端點 NAT 防火牆外的 Mailbox server。信箱伺服器與 Communications Server 2007 R2、 Microsoft Lync Server 2010 或Lync 2013集區相關聯，並取得適當的驗證權杖從 A / V 驗證服務的電腦上提供該特定的 Communications Server 2007 或 Lync Server 集區。

A / V 驗證服務會用來允許 RTP 語音媒體周遊 NAT 裝置和防火牆。由於媒體閘道處理僅訊號和無法跨 NAT 裝置或防火牆安全地傳輸語音這是必要的。當您在 Communications Server 2007 R2\]、 \[Lync Server 2010\] 或 \[ Lync 2013設定中繼伺服器時，您會指定 A / V Edge server 上的 A / V 驗證服務執行使中繼伺服器將會了解將傳入的媒體封包的位置。

如需關於如何部署 Communications Server 2007 R2 或 Lync Server 2010 或 2013年和Exchange 2013整合通訊，請參閱下列：

  - [部署 Exchange 2013 UM 和 Lync Server 概觀 （英文）](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md)

  - [檢查清單： Lync Server 整合 Exchange 2013 UM](checklist-integrate-exchange-2013-um-with-lync-server-exchange-2013-help.md)

