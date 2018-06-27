---
title: '整合通訊中的 IPv6 支援: Exchange 2013 Help'
TOCTitle: 整合通訊中的 IPv6 支援
ms:assetid: 91242c85-ce4e-422a-954e-ab623d3d6939
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ150536(v=EXCHG.150)
ms:contentKeyID: 50473733
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 整合通訊中的 IPv6 支援

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2015-04-07_

網際網路通訊協定第 6 版 (IPv6) 是最新版本的網際網路通訊協定 (IP)。若要更正許多 IPv4，已 IP 的前一版的缺點適合 IPv6。在 Microsoft Exchange Server 2010，只有時也會使用 IPv4 支援 IPv6。完全 IPv6 Exchange 環境不支援。只有當執行Exchange 2010之電腦上啟用 IPv4 和 IPv6 和網路支援兩個 IP 位址版本時才支援使用 IPv6 位址和 IP 位址範圍。但是，由於 IPv4 和 IPv6 不完全不同的通訊協定，所以 IPv4 網路無法通訊直接與 IPv6 網路，反之亦然。若要處理這個缺點，網路管理員部署所需等路由器可路由資訊的網路 IPv4 與 IPv6 網路間的裝置。如果同時使用 IPv4 和 IPv6 部署Exchange 2010 、 所有伺服器角色除了整合通訊 (UM) 可以資料從傳送和接收資料裝置、 伺服器和用戶端使用 IPv6 位址。使用Exchange 2013、 整合通訊不再類似 Exchange 2007 和 Exchange 2010 中的傳輸、 用戶端存取和信箱伺服器角色個別的伺服器角色。僅用戶端存取和信箱的伺服器上執行 UM 相關的元件和語音服務。

在 Exchange 2013 中，由於 UM 架構已變更，所以現在需要 Unified Communications Managed API (UCMA) v4.0 才能支援 IPv4 和 IPv6 以及其他功能，具有整合通訊元件和服務的用戶端存取和信箱伺服器兩者都將支援 IPv6 網路。

## IPv6 支援

啟動與Exchange 2010 Service Pack 1 (SP1) 的整合通訊伺服器角色所依賴的 UCMA 2.0 其基礎工作階段初始通訊協定 (SIP) 訊號和語音處理。UCMA 2.0 是在 UM 語音功能的主要元件。UCMA 2.0 包含 SIP 堆疊、 媒體堆疊和語音引擎的自動語音辨識 (ASR)，除了語音合成所產生的文字轉換語音 (TTS)。

在Exchange 2010、 執行雙重堆疊 （IPv4 和 IPv6） 已所需但不包括 UM 的所有伺服器角色因為 UM 所都需 UCMA 2.0 但支援僅限 IPv4，沒有 IPv6。針對Exchange 2013、 UCMA 4.0 由 UM 與需要在用戶端存取和信箱伺服器上安裝Exchange 2013 。UCMA 4.0 所支援的新功能和支援 IPv6。

UM 現在會使用 UCMA 4.0 的其中一些理由是為了在 Exchange 2013 中支援的以下新功能 (包括 IPv6)：

  - 一些公家單位需要 IPv6 以支援他們使用的產品。

  - UM 現在需要與執行雙重堆疊 (IPv4 和 IPv6) 或僅執行 IPv6 的路由器、IP 閘道、IP PBX 和工作階段邊界控制器 (SBC) 等硬體裝置相容。

  - Exchange 2013，在 Mailbox server 上執行 Microsoft Exchange 整合通訊服務和用戶端存取伺服器上執行 Microsoft Exchange Unified Messaging Call Router 服務。Exchange 2013的信箱與用戶端存取伺服器角色需要 IPv4 和 IPv6。

  - 線上服務允許用戶端使用 IPv4 或 IPv6 連線他們的服務。

  - 公用 IPv4 位址空間正在執行。針對Exchange Server 2013 Enterprise，這不是真正 um，發生問題自 UM 一律會與個私用的 IPv4 位址空間可以部署的內部 SIP 對等通訊。不過，為裝載的 Exchange UM，客戶的設備必須支援使用 IPv4 和 IPv6 的裝載的 UM。

除了 UM 和傳輸小部分、 Exchange 2013可以連線到組織中的Exchange 2010伺服器時使用 IPv4 和 IPv6 啟用雙重堆疊模式中執行的用戶端存取 」 或 「 Mailbox server。這表示客戶可以使用 IPv4 和 IPv6 堆疊位址設定執行的電腦上安裝Exchange 2013 。這可讓 IPv6 用戶端和其他 Exchange 伺服器，包括Exchange Server 2010，直接連接到Exchange 2013。

雙重堆疊模式中執行的 Windows 伺服器上的 UM 運作。這是因為等 HTTP 通訊協定搜尋時忽略的傳輸類型，而且 UM 使用 voice over IP (VoIP) 通訊協定 （包括 SIP/RTP/STUN/TURN/ICE），其取決於其他位置。這包括媒體交涉 (RTP/SRTP) UM 通告和 SIP 等項目，例如 IP 閘道、 IP Pbx 或 Sbc 會的 IP 位址清單。

## UM 支援 IPv6 意味著什麼？

若要啟用Exchange 2013 UM 以支援 IPv6，企業版及 online UM 系統管理員必須能夠利用 IPv6 連線支援 IPv6 的裝置，包括裝置例如路由器、 IP 閘道、 IP Pbx 及 Office Communications Server 2007 R2 和 Microsoft Lync server 至 UM 時。不過，如果 IPv6 不適用於互通性與舊版 Exchange 的回溯相容性，系統管理員不需要進行其他設定變更，並 IPv4 可改用。

針對Exchange 2013 Enterprise、 UM 必須直接與 SIP 對等 （IP 閘道、 IP Pbx 和 Sbc） 可能不支援 IPv6 其軟體或韌體中的通訊。因此，UM 必須能夠直接與支援 IPv4 的 SIP 對等通訊和、 更重要、 使用 IPv6。針對主控Exchange 2013、 UM 會透過 Sbc 或 Lync Server 2010 或 Lync Server 15 客戶設備與通訊。在主控Exchange 2013環境、 IPv6 注意 SIP 用戶端如 Sbc 和 Lync 伺服器可能可以部署與因此處理 IPv6-IPv4 轉換程序。

## 支援 IPv6 的 UM 裝置

因為執行 UM 元件和服務的Exchange 2013 Mailbox 和 Client Access server 支援 IPv6，IP 閘道、 IP PBX 和 SBC 廠商也必須能夠支援 IPv6。有數個問題影響裝置支援的 IPv6：

  - 有 IP 閘道、 IP Pbx 和 Sbc 可能可支援 IPv6 但尚未尚未使用 IPv6 和 UM 測試。可能會新增此支援未來，但取決於硬體廠商。

  - 有些 IP 閘道目前不支援 IPv6。

  - 有些 SBC 具有 IPv4-IPv6 功能，但現在並無法供 UM 使用，因為它們不支援 SRTP (安全即時傳遞通訊協定)/SDES (工作階段描述通訊協定安全)。

  - 另外，也有不支援雙重堆疊和單純 IPv6 的 IP PBX，但這些裝置搭配 Exchange 2013 一起使用則未經測試。

目前 UCMA 4.0 是啟用 IPv6，這表示它可以接受 IPv6 連線，但該 IPv4 也可接受、 操作雙重模式或時進行輸出連線。雙模式中執行允許 IPv4 連線來連線至舊版的 Exchange UM 正在需要進行。Lync 安裝的做法是 Lync Server\] 會版本資訊從 Active Directory 取得 Exchange Server 的最新版本。傳統的電話語音裝置 — 包括 IP 閘道、 IP Pbx 和 Sbc--若要支援 IPv4 及 IPv6 連線，他們必須聆聽的這兩種類型的連線。這是因為每個 SIP 對等裝置必須能夠接受這兩種類型的連線與舊版的 Exchange UM 的回溯相容性。這也是必要支援撥出這兩種類型的連線。

## 支援 IPv6 的 UM 設定

安裝用戶端存取和信箱伺服器之後，您需要建立整合通訊撥號對應表、 自動語音應答、 IP 閘道及搜尋群組。若要允許 UM 以支援 IPv6，您必須：

  - 建立新的 UM IP 閘道或網路上為每個 IP 閘道、 IP Pbx 或 Sbc 設定現有的 UM IP 閘道器使用 IPv6 位址。當您建立並設定必要的 UM IP 閘道器時，您必須新增 IPv6 位址\] 或 \[完全完整網域名稱 (FQDN) 的 UM IP 閘道。如果您正在將 FQDN 新增至 UM IP 閘道，您必須建立 UM IP 閘道 FQDN 解析為 IPv6 位址正確的 DNS 記錄。如果您有現有的 UM IP 閘道器，您可以使用**Set-UMIPgateway**指令程式來設定 IPv6 位址或 FQDN。建立或設定 UM IP 閘道之後，您可以使用**Get-UMIPgateway**指令程式來檢視以確保 IPv6 設定正確的 UM IP 閘道的屬性。

  - 在每個 UM IP 閘道設定*IPAddressFamily*參數。若要啟用 IP 閘道接受 IPv6 封包，您必須設定 UM IP 閘道接受 IPv4 與 IPv6 連線，或接受僅 IPv6 連線使用**Set-UMIPgateway**指令程式並將*IPAddressFamily*參數設定為下列其中一項：
    
      - *IPv4* – 預設設定，在未設定其他值時使用。
    
      - *IPv6* -這會讓使用 IPv6。不過，不會使用 IPv4。
    
      - *Any* – 這個允許使用 IPv6，但如果裝置不支援 IPv6，就可以改為使用 IPv4。

  - 您已設定 UM IP 閘道器之後，也必須支援 IPv6 網路上設定的 IP 閘道、 IP Pbx 和 Sbc。如需詳細資訊，請參閱您的硬體廠商的支援 IPv6 及正確地設定方式的裝置清單。

  - （選用） 您可能需要設定的用戶端存取和信箱伺服器以接受 IPv6 流量其中一個伺服器只能設定為接收 IPv4 流量。不過，預設值是執行 Microsoft Exchange Unified Messaging Call Router 服務的 Client Access server 和 Mailbox server 執行 Microsoft Exchange Unified Messaging 服務以接受 IPv4 與 IPv6 的流量。如需在用戶端存取和信箱伺服器上設定 IPv6 設定的詳細資訊，請參閱[Set-UMCallRouterSettings](https://technet.microsoft.com/zh-tw/library/jj215758\(v=exchg.150\))和[Set-UMService](https://technet.microsoft.com/zh-tw/library/jj552412\(v=exchg.150\))。
    
    有可能需要設定來支援 IPv6 的用戶端存取和信箱伺服器上的兩個參數： *IPAddressFamily*和*IPAddressFamilyConfigurable*。若要啟用用戶端存取和信箱伺服器以接受 IPv6 封包，您必須設定用戶端存取和信箱伺服器，以接受 IPv4 與 IPv6 連線，或接受僅 IPv6 連線。若要設定*IPAddressFamily*參數， *IPAddressFamilyConfigurable*參數必須設`$true`。

## UM IP 定址邏輯

Exchange 2013 中 UM 的 IPv6 支援邏輯如下：

  - 用戶端存取和信箱伺服器聆聽 IPv4 和 IPv6 介面上啟用雙重堆疊和用戶端存取和信箱伺服器已設為*IPv6*或*Any*時。否則即須僅限 IPv4。

  - 針對撥出電話 UM 如果 UM IP 閘道器、 Client Access server 和 Mailbox server 的*IPAddressFamily*參數設為*IPv6*或*Any*使用雙重模式。否則即須僅限 IPv4。

在雙重模式下撥出電話時，如果 *IPAddressFamily* 參數設定為 *IPv6* 或 *Any*：

  - UCMA 將取得 SIP 對等嘗試存取的 FQDN 位址清單。

  - 如有的話，UCMA 將嘗試存取所有的 IPv6 位址。

  - 如果 UCMA 判斷位址無法使用，它將會包含在清單中的位址並不嘗試再次根據設定的時間間隔。這會防止 UM 其實不重試中已知的不正確地址。

  - 如果沒有 IPv6 位址可以存取，UCMA 會將 SIP 對等的清單位址回復為 IPv4 位址。

