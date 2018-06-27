---
title: '語音的結構變更: Exchange 2013 Help'
TOCTitle: 語音的結構變更
ms:assetid: 55d5ca4a-b0cd-45f1-9f47-e745ef208698
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ150516(v=EXCHG.150)
ms:contentKeyID: 50473129
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 語音的結構變更

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2015-03-09_

Microsoft Exchange Server 2013架構是不同於Exchange Server 2007和Exchange Server 2010的架構。在Exchange 2007和Exchange 2010，類型的伺服器已分為多個伺服器角色： Client Access、 Mailbox、 集線傳輸和整合通訊。在Exchange 2013、 伺服器角色會結合成兩種類型的伺服器，然後的同一部實體伺服器或用戶端存取和信箱的兩個不同伺服器上執行所有的元件或伺服器角色中的服務。在新模型中，執行 Microsoft Exchange Unified Messaging Call Router 服務之用戶端存取伺服器會重新導向至信箱伺服器之傳入呼叫產生的工作階段初始化通訊協定 (SIP) 流量。然後媒體 （即時傳輸通訊協定 (RTP) 或安全 RTP (SRTP)） 通道 VoIP 閘道或 IP 專用交換機 (PBX) 建立以主控使用者的信箱的信箱伺服器。在Exchange 2013、 信箱伺服器具有相同的程序為 Unified Messaging server role Exchange 2007和Exchange 2010中。信箱伺服器在執行 Microsoft Exchange 整合通訊服務和 UM 工作者處理序。用戶端存取伺服器會執行 Microsoft Exchange Unified Messaging Call Router 服務，會收到來電並將其轉寄到信箱伺服器。

**目錄**

Support for the new Exchange architecture

UM ports

UM dial plans

UM Call Router performance counters

## 支援新的 Exchange 架構

在Exchange 2013、 用戶端存取伺服器負責進行自動探索、 Secure Sockets Layer (SSL)、 驗證、 重新導向及 proxy。用戶端存取伺服器會針對任何撥入通話的進入點或 SIP 要求的整合通訊 (UM)。路由邏輯和 SIP 重新導向會實作為自動包含在用戶端存取伺服器的服務。此服務會稱為 Microsoft Exchange Unified Messaging Call Router 服務。它會安裝並在組織中每個用戶端存取伺服器上執行。當用戶端存取伺服器會接收 SIP INVITE 的來電時，Microsoft Exchange Unified Messaging Call Router 服務會重新導向的信箱伺服器的傳入呼叫。接著 VoIP 閘道、 IP PBX 或工作階段邊界控制器 (SBC) 與 Mailbox server 之間建立的媒體通道 （RTP 或 SRTP）。雖然用戶端存取伺服器會作為 SIP 重新導向程式，它只會處理 VoIP 閘道、 IP Pbx 或 Sbc 的 SIP 要求。它不會收到任何媒體流量。使用 RTP 或 SRTP 的媒體流量只傳遞 Mailbox server 和如 VoIP 閘道、 IP Pbx 或 Sbc 的 SIP 對等之間 — 未提供給用戶端存取伺服器。當您部署Exchange 2013和 UM 時，您必須設定 VoIP 閘道、 IP Pbx 或指向您已安裝，以便讓來電會路由 um 傳送正確的 Client Access server 的 Sbc。

在某些情況下，部署多個用戶端存取伺服器會是必要項，與 Client Access server 部署分開在不同的實體硬體從信箱伺服器。可使用 4 或 5 硬體或軟體負載平衡器以分組用戶端存取伺服器陣列中。但沒有 Active Directory Exchange 物件型用戶端存取伺服器陣列。較大的 Exchange 部署中公認的作法是使用前面用戶端存取伺服器的硬體或軟體負載平衡。

在安裝用戶端存取伺服器時正在執行 Microsoft Exchange Unified Messaging Call Router 服務。此服務會執行下列動作：

  - 在初始化時，它會讀取一個名為 msexchangeumcallrouter.config 的本地設定檔。

  - 運用組織的系統信箱進行語音語法生成。

  - 支援傳輸控制通訊協定 (TCP) 和/或傳輸層安全性 (TLS) 連線。此設定為可設定。

  - 只有在出現設定錯誤或無法註冊必要連接埠時，程序才會停止。

在Exchange 2013、 信箱伺服器不是負責接聽來電的 SIP 要求。只有負責從用戶端存取伺服器接收 SIP 流量和再並建立 VoIP 閘道、 IP PBX 或 SBC RTP 或 SRTP 連線。

用戶端存取伺服器會重新導向來電至信箱伺服器之後，VoIP 閘道、 IP PBX 或 SBC 與 Mailbox server 之間建立的媒體通道。建立的媒體通道之後，Microsoft Exchange 整合通訊服務的 Mailbox server 上播放使用者的語音信箱問候語，處理自動答錄規則的使用者，並邀請來電者留下語音訊息。Mailbox server 然後記錄語音訊息、 建立之郵件的記錄並 deposits 在使用者的信箱。不過，如果您正在整合Exchange與 Office Communications Server 2007 R2 或 Lync 伺服器，這兩個的 SIP 和 RTP 或 SRTP 媒體通道的傳入呼叫都是由處理 Lync server 和 Mailbox server。在 Lync 整合式環境中，您不需要 VoIP 閘道、 IP Pbx 或 Sbc。Lync，執行 Microsoft Exchange 整合通訊服務的信箱伺服器外觀就像是Exchange 2010 UM 伺服器。信箱伺服器和用戶端存取伺服器執行 Microsoft Exchange Unified Messaging Call Router 服務之被視為信任的同儕因為這兩個伺服器必須加入至 SIP 撥號對應表。Lync 路由傳送來電使用輸入路由元件，它會使用 SIP 與用戶端存取伺服器進行通訊，然後路由傳送的信箱伺服器的呼叫。

Exchange 2010UM 管理員可以設定一組屬性整合通訊的每個 UM 伺服器上。Exchange 2013、 UM 元件和設定 um 找到的用戶端存取和信箱伺服器上。套用至單一電腦執行 Unified Messaging server role Exchange 2010中的所有組態設定都是仍然可以使用。不過，這些內容與組態設定的一些設定執行 Microsoft Exchange Unified Messaging Call Router 服務、 用戶端存取伺服器上且其他人可在執行 Microsoft Exchange 整合通訊服務的信箱伺服器上。在某些情況下，相同的設定值是位於兩者。下列清單顯示 cmdlet 和參數都可使用 Client Access server 和 Mailbox server 上與位置進行變更指令程式以支援與舊版的整合通訊的部署案例。

  - **Set-UMService -DialPlans \<MultiValuedProperty\>**    適用於 Exchange 2013 信箱伺服器，並可在 Exchange 2007 和 Exchange 2010 整合通訊伺服器上使用。

  - **Set-UMCallRouterSettings -DialPlans \<MultiValuedProperty\>**    適用於 Exchange 2013 用戶端存取伺服器，但無法用於 Exchange 2007 和 Exchange 2010 整合通訊伺服器。

  - **Set-UMService -MaxCallsAllowed \<Int32\>**    適用於 Exchange 2013 信箱伺服器，並可在 Exchange 2007 和 Exchange 2010 整合通訊伺服器上使用。

  - **Set-UMCallRouterSettings -MaxCallsAllowed \<Int32\>**   無法用於 Exchange 2013 用戶端存取伺服器，且無法用於 Exchange 2007 和 Exchange 2010 整合通訊伺服器。

  - **Set-UMService -SipTcpListeningPort \<Int32\>**    無法在 Exchange 2013 信箱伺服器上設定，但可以在 Exchange 2007 和 Exchange 2010 整合通訊伺服器上使用。

  - **Set-UMService -SipTlsListeningPort \<Int32\>**    無法在 Exchange 2013 信箱伺服器上設定，但可以在 Exchange 2007 和 Exchange 2010 整合通訊伺服器上使用。

  - **Set-UMCallRouterSettings -SipTcpListeningPort \<Int32\>**    適用於 Exchange 2013 用戶端存取伺服器，但無法在 Exchange 2007 和 Exchange 2010 整合通訊伺服器上使用。

  - **Set-UMCallRouterSettings -SipTlsListeningPort \<Int32\>**    適用於 Exchange 2013 用戶端存取伺服器，但無法在 Exchange 2007 和 Exchange 2010 整合通訊伺服器上使用。

  - **Set-UMService - Status \<Enabled | Disabled | NoNewCalls\>**   無法用於 Exchange 2013 信箱伺服器，但可在 Exchange 2007 和 Exchange 2010 整合通訊伺服器上使用。

  - **Set-UMCallRouterSettings - Status \<Enabled | Disabled | NoNewCalls\>**    無法用於 Exchange 2013 用戶端存取伺服器，而且無法在 Exchange 2007 和 Exchange 2010 整合通訊伺服器上使用。

  - **Set-UMService -UMStartupMode \<TCP | TLS | Dual\>**   適用於 Exchange 2013 信箱伺服器，並可在 Exchange 2007 和 Exchange 2010 整合通訊伺服器上使用。

  - **Set-UMCallRouterSettings - UMStartupMode \<TCP | TLS | Dual\>**    適用於 Exchange 2013 用戶端存取伺服器，但無法在 Exchange 2007 和 Exchange 2010 整合通訊伺服器上使用。

  - **Enable-UMService**    無法用於 Exchange 2013 信箱伺服器，但可以在 Exchange 2007 和 Exchange 2010 整合通訊伺服器上使用。

  - **Disable-UMService**    無法用於 Exchange 2013 信箱伺服器，但可以在 Exchange 2007 和 Exchange 2010 整合通訊伺服器上使用。

Mailbox server，您將使用**Set/Get/Enable/Disable-UMService**指令程式來檢視或設定 Exchange 2013 Mailbox server 或 Exchange 2007 或 Exchange 2010 Unified Messaging 的伺服器上的 Microsoft Exchange 整合通訊服務的 UM 內容。一組不同的指令程式， **Set/Get-UMCallRouterSettings**，可用來檢視或設定用戶端存取伺服器上的 Microsoft Exchange Unified Messaging Call Router 服務屬性。這可確保現有**Get-UMServer**、 Exchange 2007及Exchange 2010**Set-UMServer**、 **Enable-UMServer**，以及**Disable-UMServer**指令程式會在Exchange 2013 Mailbox server 的共存部署工作。這也可確保指令程式會運作時的相同或不同的伺服器上安裝 Mailbox 和 Client Access server。

回到頁首

## UM 連接埠

用戶端存取伺服器上找到的 Microsoft Exchange Unified Messaging Call Router 服務會使用 SIP over 傳輸控制通訊協定 (TCP) 或共同通訊正在執行 Microsoft Exchange 整合通訊服務的 Mailbox server 的傳輸層安全性 (相互 TLS)。若要避免 TCP/使用者資料包通訊協定 (UDP) 連接埠衝突，Microsoft Exchange Unified Messaging Call Router 服務和 Microsoft Exchange 整合通訊服務預設值與不同的 TCP 連接埠上接聽。它們可接受兩者不安全模式和安全連線\] 中，根據相互 TLS 是否用於 SIP 和 RTP 流量。根據預設，用戶端存取伺服器會接聽的這兩個 TCP 通訊埠 5060 不安全模式和 SIP 安全模式中的 TCP 連接埠 5061 上的 SIP 要求時使用相互 TLS。這些連接埠都可使用**Set-UMCallRouterSettings**指令程式。用戶端存取伺服器上的 Microsoft Exchange Unified Messaging Call Router 服務不會處理媒體 （RTP 或 SRTP） 流量，因此皆會使用唯一的 TCP 連接埠及 UDP 連接埠。根據預設，在信箱伺服器會接聽的這兩個 TCP 連接埠 5062 不安全模式和 TCP 連接埠 5063 SIP 安全模式中的 SIP 要求時相互 TLS 用。這些連接埠都可使用 Exchange 管理命令介面 cmdlet。在執行 Microsoft Exchange 整合通訊服務的 Mailbox server 上 TCP 連接埠無法設定 Exchange server 上使用命令介面或在登錄中進行設定。Microsoft Exchange 整合通訊服務的 Mailbox server 上會接受來自 5062 和 5063 的 SIP 連接埠上的用戶端存取伺服器的連線。用戶端存取伺服器會 SIP 要求重新導向至信箱伺服器之後，使用 VoIP 閘道、 IP PBX 或 SBC，以及 Microsoft Exchange 整合通訊工作者處理序的信箱伺服器上建立 RTP 或 SRTP 媒體通道。

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
<td><p>SIP (用戶端存取伺服器 — Microsoft Exchange 整合通訊通話路由器服務)</p></td>
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
<td><p>5065 和 5067 tcp （無安全性）。5066 和 5068 的相互 TLS （安全）。當<em>UMStartupMode</em>設為<em>Dual</em>是這樣。如果<em>UMStartUpMode</em>設為<em>TCP</em>或<em>TLS</em>，會使用連接埠 5065 和 5066。預設<em>UMStartupMode</em>是<em>TCP</em>。</p></td>
<td><p>不適用</p></td>
<td><p>無法變更連接埠。</p></td>
</tr>
<tr class="even">
<td><p>RTP (信箱箱伺服器 - UM 工作者處理程序)</p></td>
<td><p>不適用</p></td>
<td><p>1024 與 65535 之間的連接埠。</p></td>
<td><p>連接埠範圍可透過系統登錄變更（不過，這並非受支援的組態）。</p>
<p>HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Speech Server\2.0\AudioConnectionMinPort</p>
<p>HKLM\SOFTWARE\Microsoft\Microsoft Speech Server\2.0\AudioConnectionMaxPort</p></td>
</tr>
</tbody>
</table>


回到頁首

## UM 撥號對應表

對應或建立關聯的 UM 撥號對應至 UM 伺服器不是中需要Exchange 2013與其Exchange 2007和Exchange 2010中的方式。因為用戶端存取和信箱的所有伺服器都能如都預期 VoIP 閘道、 IP Pbx 或 SBCs 接收所有來電連結至撥號對應表不需要執行 UM 服務的 client Access server 或信箱伺服器。例外是 SIP 撥號對應表就會搭配Lync 2013、 Lync Server 2010 和 Office Communications Server 2007 R2 必須已部署的用戶端存取和信箱伺服器和相關聯。這兩種類型的Exchange伺服器必須新增至每個 SIP 撥號對應表是作為信任的同儕從 Communications Server 2007 R2 或 Lync Server。否則，Communications Server 2007 R2 或 Lync Server 會拒絕使用者的撥出電話。

下列表格概述用戶端存取伺服器、信箱伺服器，以及 UM 撥號對應表之關係。

### 連結 UM 撥號對應表

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>拓撲</th>
<th>撥號對應表</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>用戶端存取伺服器及信箱伺服器在同一個伺服器上 (沒有 Communications Server 2007 R2 或 Lync Server 2010 非 SIP 撥號對應表)</p></td>
<td><p>撥號對應表已不再需要與用戶端存取或信箱伺服器產生關聯。您不可以將用戶端存取或信箱伺服器新增至撥號對應表。如果您執行<strong>Set-UMService</strong>指令程式，它將會產生錯誤如果您嘗試建立與非 SIP 撥號對應表關聯的信箱伺服器。</p></td>
</tr>
<tr class="even">
<td><p>用戶端存取伺服器及信箱伺服器在不同的伺服器上 (沒有 Communications Server 2007 R2 或 Lync Server 2010 非 SIP 撥號對應表)</p></td>
<td><p>撥號對應表已不再需要與用戶端存取或信箱伺服器產生關聯。您不可以將用戶端存取或信箱伺服器新增至撥號對應表。如果您執行<strong>Set-UMService</strong>指令程式，它將會產生錯誤如果您嘗試建立與非 SIP 撥號對應表關聯的信箱伺服器。</p></td>
</tr>
<tr class="odd">
<td><p>用戶端存取伺服器及信箱伺服器在同一個實體伺服器上 (有 Communications Server 2007 R2 及 Lync Server 2010 附加 SIP 撥號對應表)</p></td>
<td><p>針對單一 SIP 撥號對應表，將新增至 SIP 撥號對應表的所有用戶端存取和信箱伺服器。為多個 SIP 撥號對應表、 新增撥號對應表為每個 SIP 的所有用戶端存取和信箱伺服器。這會使這兩個伺服器信任的同儕的 Office Communications Server 2007 R2 或 Lync Server。您必須在 Office Communications Server 2007 R2 或 Lync Server 部署中使用相同的憑證當您在每個用戶端存取和信箱伺服器上執行動作。</p></td>
</tr>
<tr class="even">
<td><p>用戶端存取伺服器及信箱伺服器在不同的實體伺服器上 (有 Communications Server 2007 R2 及 Lync Server 2010 附加 SIP 撥號對應表)</p></td>
<td><p>針對單一 SIP 撥號對應表，將新增至 SIP 撥號對應表的所有用戶端存取和信箱伺服器。為多個 SIP 撥號對應表、 新增撥號對應表為每個 SIP 的所有用戶端存取和信箱伺服器。這會使這兩個伺服器信任的同儕的 Office Communications Server 2007 R2 或 Lync Server。如果要使用的用戶端存取和信箱伺服器上的憑證不同，您必須如同您所做的每個用戶端存取和信箱伺服器上您組織中使用 [Office Communications Server 2007 R2 或 Lync Server 部署上的相同的憑證。</p></td>
</tr>
</tbody>
</table>


回到頁首

## UM 呼叫路由器的效能計數器

過去版本的 Exchange 包含整合通訊伺服器角色，負責執行 Microsoft Exchange 整合通訊服務。因為Exchange 2013的架構變更、 用戶端存取伺服器執行 Microsoft Exchange Unified Messaging Call Router 服務和信箱伺服器執行 Microsoft Exchange 整合通訊服務。就如同舊版的 Exchange UM 一樣的系統管理員可用的 Microsoft Exchange 整合通訊服務的相同的效能計數器。但有也額外的效能計數器您可以使用用戶端存取伺服器上以確認狀態的 Microsoft Exchange Unified Messaging Call Router 服務及進行疑難排解。

為支援新 Exchange 2013 中的 Client Access Unified Messaging Call Router 服務，有下列效能計數器可使用。

### 效能計數器

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>效能計數器類別</th>
<th>計數器名稱</th>
<th>描述</th>
<th>閾值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>% 內部來電在過去一小時內遭到 Microsoft Exchange Unified Messaging Call Router Service 拒絕。</p></td>
<td><p>顯示 Microsoft Exchange Unified Messaging Call router 服務最近一小時所拒絕的內部來電所佔的百分比。</p></td>
<td><p>應該總是少於百分之五，但是應該保持為 0。</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>來電中斷，Microsoft Exchange Unified Messaging Call Router 服務出現無法復原之錯誤。</p></td>
<td><p>顯示發生內部系統錯誤之後，中斷連線的來電數目。</p></td>
<td><p>應該永遠為 0。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>Microsoft Exchange Unified Messaging Call router 服務所拒絕的內部來電總數。</p></td>
<td><p>顯示 Microsoft Exchange Unified Messaging Call Router 自服務啟動之後拒絕的內部來電總數。</p></td>
<td><p>應該永遠為 0。</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>Microsoft Exchange Unified Messaging Call router 服務所接答的來電總數。</p></td>
<td><p>顯示 Microsoft Exchange Unified Messaging Call Router 自服務啟動之後接答的內部來電總數。</p></td>
<td><p>應大於或等於 0。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>% 內部來電在過去一小時內遭到 Microsoft Exchange Unified Messaging Call Router Service 拒絕。</p></td>
<td><p>顯示 Microsoft Exchange Unified Messaging Call router 服務最近一小時所拒絕的內部來電所佔的百分比。</p></td>
<td><p>應該小於百分之五。</p></td>
</tr>
</tbody>
</table>


回到頁首

