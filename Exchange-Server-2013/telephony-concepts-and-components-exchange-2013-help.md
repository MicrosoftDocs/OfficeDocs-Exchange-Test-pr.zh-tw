---
title: '電話語音概念及元件: Exchange 2013 Help'
TOCTitle: 電話語音概念及元件
ms:assetid: ce70bf6a-db85-411b-8b93-2987703963a9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124606(v=EXCHG.150)
ms:contentKeyID: 54652602
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 電話語音概念及元件

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-04-25_

如果您正在規劃及部署MicrosoftExchange 2013整合通訊 (UM) 網路上，您必須先了解整合通訊和電話語音的網路。本主題概述電話語音基礎結構概念及元件可協助您規劃及部署執行Exchange 2013伺服器整合通訊。

**目錄**

概觀

概念及元件

電路切換型網路

封包切換網路

PBX

IP PBX

已啟用 SIP 的 PBX

VoIP

IP 閘道器

## 概觀

在Microsoft ExchangeExchange Server 2007之前的版本、 Exchange系統管理員的主要責任已管理電子郵件訊息與，有時，管理網路基礎結構。舊版Exchange無須整合通訊功能。Exchange Server 5.5 版、 Exchange 2000 Server，與Exchange Server 2003管理員著重於Exchange環境和網路基礎結構，並倚賴管理其電話語音環境與基礎結構的電話語音顧問。

## 概念及元件

若要成功部署整合通訊中Exchange 2013，您必須基本的電話語音概念和電話語音元件的確實了解。您充分瞭解的電話語音基礎 （英文） 之後，您可以成功地整合Exchange 2013到Exchange 2013組織整合通訊。基本概念及元件包括：

  - 電路切換式與封包切換式網路

  - 專用交換機 (PBX)

  - IP PBX

  - 網際網路語音通訊協定 (VoIP)

  - VoIP 閘道

## 電路切換型網路

電路切換型網路，例如公用交換電話網路 (PSTN)，在多個通話傳送相同傳輸中型不同。常見問題、 用於 PSTN 中型是銅。不過，也可能使用光纖助讀纜線。

電路切換型網路位於網路中有存在的專用的連線。專用的連線為基礎的電路或設定兩個節點之間，讓他們可以彼此通訊通道。兩個節點之間建立撥號之後，可以使用連線只能由下列兩個節點。當通話會使用下列其中一個節點的結束時，會取消連線。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>PSTN 是一群的 world 公用電路切換型電話網路。此群組的格式類似於網際網路是一群的 world 公用 IP 架構封包切換網路的方式。</td>
</tr>
</tbody>
</table>


有兩種基本電路切換型網路 ︰ 類比和數位。針對語音傳輸設計旨在類比。許多年 PSTN 已僅類比，但今天，例如 PSTN 電路型網路而且轉換從類比成數位。若要支援類比語音傳輸信號透過數位網路、 類比傳輸訊號必須編碼或其進入電話語音 WAN 之前轉換成以數位格式。在接收結束連線時，必須解碼或回類比訊號格式轉換的數位訊號。

有優點和缺點電路切換型網路。電路切換型網路有幾項缺點。電路切換型網路可能較效率低，因為可以浪費頻寬。並非如此封包切換網路上使用 VoIP 時。VoIP 與所有其他網路應用程式共用的可用頻寬並使用可用頻寬更有效率。另一個缺點電路切換型網路是您必須佈建的電話通話將必要的尖峰使用量時間並再工資使用電路或電路支援通話數目上限數目上限。

電路切換具有透過封包切換網路的一個大優點。電路切換型網路中使用電路時您有完整的電路您使用沒有其他使用者從競爭電路的時間。這不是封包切換網路的大小寫。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>同步數位階層 (SDH) 已經成為大部分 PSTN 網路的主要的傳輸通訊協定。SDH 被遷光纖助讀網路。</td>
</tr>
</tbody>
</table>


回到頁首

## 封包切換網路

封包切換是將資料訊息分成較小的單位呼叫封包的技術。封包可用的最佳路由傳送至其目的地及接收結尾的重組然後。

在封包切換網路例如網際網路封包路由傳送給其目的地最有利的路由，但不是所有出差兩個主機之間的封包傳輸相同路由，甚至是那些從單一的郵件。這幾乎保證封包會送達在不同時間和照順序。封包切換網路中封包 （訊息或片段 （英文） 的訊息） 個別會透過資料連結可能會共用其他節點的節點之間路由傳送。使用不同於電路切換的封包切換多個連線至網路上的節點共用的可用頻寬。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>與基礎的電路切換，所有封包會移至受話方順序與單一路徑。</td>
</tr>
</tbody>
</table>


若要啟用整個全球網際網路上的資料通訊存在於封包切換網路。公用資料網路或封包切換網路是資料對應至 PSTN。

封包切換網路也會找到在這類網路環境中做為 LAN 和 WAN 網路。在 WAN 的封包切換環境依賴電話電路但電路排列使它們保留與其端點的永久性連線。在區域網路封包切換環境中，例如乙太網路，具有資料封包傳輸依賴封包切換、 路由器和 LAN 纜線。在 LAN 參數會長僅不夠傳送目前的封包的兩個區段之間的連線。傳入封包會儲存至暫時記憶體區域或緩衝區中的記憶體。在乙太網路型區域網路乙太網路圖文框包含封包及特殊的標頭包含的媒體存取控制 (MAC) 位址資訊的來源和目的地的封包的承載或資料部分。當封包到達其目的地時，他們會置回順序由封包組合程式。封包組合程式所需之不同的路由的封包可能會因為。

封包切換網路已進行可能的存在於網際網路與，同時，有進行資料網路 — 特別 LAN 型 IP 網路 — 更多可用和時遇到的普遍。

回到頁首

## PBX

舊版的 PBX 是做為切換通話的電話語音或電路切換型網路的交換器的電話語音裝置。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>舊版的 PBX 是無法傳遞 IP 封包 PBX。在許多企業中舊版的 Pbx 已取代為 IP Pbx。</td>
</tr>
</tbody>
</table>


PBX 是最 \[中等大小\] 與 \[較大的公司所使用的電話語音裝置。PBX 可讓使用者或訂閱者的 PBX 共用加速被視為外部的 PBX 電話通話的外部的行數。PBX 是比給予每位使用者在公司外部的專用的電話線的更加較不昂貴的解決方案。電話組另外至傳真機器、 數據機及許多其他通訊裝置可以被連接至 PBX。

PBX 設備通常公司的內部部署安裝並連接散位於與安裝在商務網站之間的通話。限制外部行數，又稱為主幹行、 一般會針對撥出及接聽通話的外部商務，來自 PSTN 等外部來源。

透過撥 9 或 0 後面接著外部號碼某些系統中進行內部商務撥打到使用 PBX 的外部電話號碼。完成將來電自動選取外寄的主幹線。相反地，公司內的使用者之間所撥打的電話通常不需要特殊撥號的數字或外部的主幹線的使用。這是因為內部的電話路由傳送或是由 PBX 電話的實際連接至 PBX 之間切換。

中等大小及較大的企業版，在下列的 PBX 設定為可能：

  - 支援的整個商務單一 PBX。

  - 分組的兩個或多個 Pbx 不網路或連線至彼此。

  - 一群的兩個或多個 Pbx 連接在一起或網路。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Exchange 2013 UM 撥號對應表可以跨多個 PBX 或 IP PBX。</td>
</tr>
</tbody>
</table>


回到頁首

## IP PBX

將 IP PBX 是 PBX 電話使用乙太網路或封包切換 LAN 連線的 IP 通訊協定的支援及 IP 封包中傳送其語音交談。混合式 IP PBX 支援 IP 通訊協定傳送語音交談中封包，但也會連接傳統類比和數位電路切換型時間部門多工 (TDM) 電話。將 IP PBX 是電話切換位於私用的營業，而不是電話公司的設備。

IP Pbx 較為經常管理比舊版的 pbx 設定，因為系統管理員可以輕易地設定其 IP PBX 服務使用網際網路瀏覽器或另一個 IP 型公用程式。加上，必須安裝任何其他電線、 纜線或修補程式面板。將 IP PBX、 移動 IP 型電話是拔除電話並再次將它插入新的位置，而不是從舊版的 PBX 廠商移電話昂貴服務的通話一樣簡單。此外，擁有 IP PBX 的企業版不需要維護與管理兩個不同電路切換型及封包切換網路所需的其他基礎結構成本。

## 啟用 SIP 的 Pbx

已啟用 SIP 的 PBX 是做為切換通話的電話語音或電路切換型網路的網路交換器的電話語音裝置。不過，已啟用 SIP 的 PBX 與傳統 PBX 之間的差異是已啟用 SIP 的 PBX 可以連線到網際網路和透過網際網路進行的通話使用 SIP 通訊協定。

啟用 SIP 的 Pbx 可針對包含包含全域的 E.164 號碼的 SIP URI 的電話使用格式和"user = phone"參數。例如： sip:+14255551234@contoso.com;user=phone

E164 號碼開頭為前置字元"+"並不會包含電話內容參數或任何分隔符號。 啟用 SIP 的 Pbx 支援 TCP 及 UDP。UDP 仍廣泛搭配舊版系統。啟用 SIP 的 Pbx 也支援相互傳輸層安全性 (相互 TLS) 和 DNS 查詢。

## VoIP

Voice over Internet Protocol (VoIP) 是一種可以包含硬體和軟體可讓使用者使用電話通話作為傳輸中型 IP 型網路技術。在 VoIP 語音資料傳送封包使用，而不是傳統電路傳輸 IP 或 PSTN 電路切換型電話行中。連線至確保 IP 網路 VoIP 閘道使用 VoIP 通訊協定來傳送語音Exchange 2013用戶端存取和信箱伺服器和 PBX 系統之間的資料封包。

## VoIP 閘道

VoIP 閘道是協力廠商硬體裝置或舊版的 PBX 連線至您的區域網路的產品。VoIP 閘道可讓與Exchange 2013信箱和用戶端存取伺服器執行 Microsoft Exchange Unified Messaging 和整合通訊呼叫路由器服務通訊的 PBX 系統。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>VoIP 閘道也可以連線到使用 VoIP 取代 PSTN 電路切換型通訊協定的 PBX 系統。</td>
</tr>
</tbody>
</table>


Exchange 2013整合的通訊依賴 VoIP 閘道的權限翻譯或轉換 TDM 或電路切換型電話語音基礎通訊協定 ISDN 和 PBX 從 QSIG 類似工作階段初始通訊協定 (SIP)、 即時傳輸通訊協定 (RTP) 或 T.38 IP 型或 VoIP 基礎通訊協定來進行即時傳真傳輸。VoIP 閘道是組成的功能和整合通訊的運作方式。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在您安裝 VoIP 閘道、 IP PBX 或已啟用 SIP 的 PBX、 之後必須建立 UM IP 閘道來代表實際的裝置。建立 UM IP 閘道器後，UM IP 閘道器與連結的用戶端存取和信箱伺服器會將 SIP OPTIONS 要求傳送給 VoIP 閘道、 IP PBX 或已啟用 SIP 的 PBX 以確保裝置有回應中。如果 VoIP 閘道不會從信箱伺服器回應 SIP OPTIONS 要求，Mailbox server 會記錄與識別碼 1088年說明事件的要求失敗。若要解決此問題，請確定 VoIP 閘道、 IP PBX 或可用且線上和整合通訊用戶端存取和信箱伺服器上的設定是否正確。</td>
</tr>
</tbody>
</table>


如需 IP PBX 和 PBX 組態的詳細資訊，請參閱[PBX 與 IP PBX 組態](pbx-and-ip-pbx-configurations-exchange-2013-help.md)。

回到頁首

## 相關資訊

[UM 通訊協定、 連接埠和服務](um-protocols-ports-and-services-exchange-2013-help.md)

[Exchange 2013 的電話語音 advisor](telephony-advisor-for-exchange-2013-exchange-2013-help.md)

