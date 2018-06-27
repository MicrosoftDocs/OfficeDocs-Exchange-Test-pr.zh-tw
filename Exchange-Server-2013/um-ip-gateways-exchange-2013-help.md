---
title: 'UM IP 閘道: Exchange Online Help'
TOCTitle: UM IP 閘道
ms:assetid: 991d77e0-3995-44ab-bedf-52ff7a0301ab
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb123890(v=EXCHG.150)
ms:contentKeyID: 50473834
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# UM IP 閘道

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2014-06-24_

整合通訊 (UM) IP 閘道可代替 VoIP (Voice over IP) 閘道、IP 專用交換機 (PBX) 或工作階段邊界控制器 (SBC) 硬體裝置。在 VoIP 閘道、IP PBX 或 SBC 可以用來接聽來電並為語音信箱使用者傳送撥出號碼前，必須在目錄服務中建立 UM IP。

**目錄**

Overview of UM IP gateways

UM IP gateways

IPv6 support for UM IP gateways

Enabling and disabling a UM IP gateway

## UM IP 閘道概觀

一般而言，*「閘道」*是描述連線兩個不相容網路之實體裝置的術語。使用 Exchange 整合通訊及其他整合通訊解決方案時，會使用 VoIP 閘道轉譯公用交換電話網路 (PSTN)/分時多工 (TDM)，或電路切換型電話語音網路及 IP 或封包切換型資料網路。IP PBX 也會在 PSTN 網路和封包切換型網路之間進行轉譯，所以使用 IP PBX 時，就需要 VoIP 閘道。VoIP 閘道只有在連接傳統 PBX 硬體裝置與 UM 部署時需要使用。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>封包切換型網路是指封包 (郵件或郵件片段) 在 VoIP 閘道、IP PBX 和 SBC 等裝置之間個別路由的網路。這與電路切換網路相反，此網路會設定兩個節點間的專用連線，以在通訊期間獨佔使用。</td>
</tr>
</tbody>
</table>


Exchange 整合通訊依賴 VoIP 閘道的功能，將 TDM 或電話語音電路切換型的通訊協定 (例如整合服務數位網路 (ISDN) 或 QSIG) 從 PBX 轉譯成以 VoIP 或 IP 為基礎的通訊協定 (例如工作階段初始通訊協定 (SIP)、即時傳輸通訊協定 (RTP) 或進行即時傳真傳輸的 T.38)。

IP PBX 也會在連接電路切換型電話網路與資料或封包切換型網路時使用。它們也常用來轉譯電路切換型通訊協定與以 VoIP 或 IP (如 SIP、RTP 和 Secure RTPC (SRTP)) 為基礎的通訊協定。

工作階段邊界控制器 (SBC) 與 VoIP 閘道和 IP PBX 稍有不同。它們正好與連接電路切換型網路與封包切換型網路相反，是使用公用網路 (如網際網路) 或透過私人 WAN 連線來連接兩個資料網路。在整合通訊中，SBC 是在 UM 混合式部署中使用，而其中 UM 會使用位在內部部署或其他位置 (如雲端中的信箱) 的元件。

## VoIP 裝置組態

雖然 PBX、VoIP 閘道、IP PBX 和 SBC 的類型及製造商很多，但是基本上有三種類型的 VoIP 裝置組態：

  - **IP PBX**   在 PSTN/TDM 或以電話網路為基礎的電路切換型網路和 IP 或封包切換型資料網路之間進行轉譯的單一裝置。

  - **PBX (傳統) 和 VoIP 閘道**   兩個一起在 PSTN/TDM 或電路切換型電話網路和 IP 或封包切換型資料網路之間進行轉譯的不同元件。

  - **SBC**   連接兩種 IP 型網路 (如 LAN 和資料中心) 的一台或多台裝置。

為了支援整合通訊，連接電話網路基礎結構與資料網路基礎結構，或連接內部部署與雲端中的 UM 部署時，會使用一或兩種類型的 IP/VoIP 裝置組態。

## UM IP 閘道

UM IP 閘道含有一或多個 UM 群組搜尋和組態設定。UM 群組搜尋是用來連結 UM IP 閘道與 UM 撥號對應表。結合 UM IP 閘道與 UM 群組搜尋，可在 VoIP 閘道、IP PBX 或 SBC 與 UM 撥號對應表之間建立連結。透過建立多個 UM 群組搜尋，您可以將單一 UM IP 閘道與多個 UM 撥號對應表產生關聯。

當您建立 UM IP 閘道後，連結 UM IP 閘道的 Exchange 伺服器將傳送 SIP OPTIONS 要求給 VoIP 閘道、IP PBX 或 SBC，以確保裝置可以回應。如果 VoIP 閘道、IP PBX 或 SBC 未回應要求，Exchange 伺服器將會記錄識別碼 1400 的事件，說明要求失敗。發生此問題時，請確定 VoIP 閘道、IP PBX 或 SBC 可供使用且為連線狀態，而且整合通訊組態正確無誤。

信箱伺服器只會與列入信任 SIP 對等的 VoIP 閘道、IP PBX 或 SBC 通訊。在某些情況下，如果有兩個 VoIP 閘道、IP PBX 或 SBC 設定為使用相同的 IP 位址，將會記錄識別碼 1175 的事件。整合通訊會擷取整合通訊 Web 服務虛擬目錄的內部 URL，然後使用 URL 建立受信任 SIP 對等的 FQDN 清單，以避免未經授權的要求。當兩個 FQDN 都解析成相同 IP 位址時，將會記錄此事件。

## 為 UM IP 閘道提供 IPv6 支援

網際網路通訊協定第 6 版 (IPv6) 是最新版的網際網路通訊協定 (IP)。IPv6 旨在修正舊版 IP 的 IPv4 本身許多缺點。在 Microsoft Exchange Server 2010 內部部署和混合部署中，只有在同時使用 IPv4 時才支援 IPv6。

在 Exchange 2013 內部部署和混合部署中，UM 相關元件和語音服務只能在用戶端存取和信箱伺服器上執行。由於 UM 架構已變更，所以現在需要 Unified Communications Managed API (UCMA) v4.0 才能支援 IPv4 和 IPv6 以及其他功能，具有整合通訊元件和服務的用戶端存取和信箱伺服器兩者都將支援 IPv6 網路且不需要 IPv4。

在內部部署、混合和 Exchange Online 部署中，當企業和 Exchange Online UM 系統管理員連線 UM 與具 IPv6 功能的裝置 (包括路由器、IP 閘道、IP PBX 和 Microsoft Office Communications Server 2007 R2 與 Microsoft Lync Server) 時，都可以使用 IPv6。不過，對於交互操作性和回溯相容性，如果 UM IP 閘道上的 *IPAddressFamily* 參數設定為 `Any`，就可以在不需要變更其他組態的情況下，使用 IPv4。

Exchange UM 仍必須直接與可能在其軟體或韌體支援 IPv6 的 SIP 對等 (VoIP 閘道、IP PBX 和 SBC) 通訊。如果它們不支援 IPv6，UM 必須可以直接與使用 IPv4 的 SIP 對等通訊。對於託管的語音信箱，UM 會透過 SBC 或 Lync Server 2010 或 Lync Server 2013 與客戶設備通訊，在託管的環境中，可以部署諸如 SBC 和 Lync 伺服器等 IPv6 SIP 感知用戶端來處理 IPv6-to-IPv4 轉換程序。

針對您安裝 Client Access Server 和 Mailbox Server 後的內部部署和混合部署，以及 Exchange Online UM 部署，您需要建立 UM IP 閘道。如果您需要 UM IP 閘道支援 IPv6，您還必須︰

1.  建立一個新 UM IP 閘道或以 IPv6 位址為網路上每個 IP 閘道、IP PBX 或 SBC 設定 UM IP 閘道。建立並設定要求的 UM IP 閘道時，必須新增 IPv6 位址或 UM IP 閘道的完整網域名稱 (FQDN)。若您將 FQDN 新增至 UM IP 閘道中，必須建立正確的 DNS 記錄以將 UM IP 閘道解析至 IPv6 位址。若您已有 UM IP 閘道，可使用 **Set-UMIPgateway** 指令程式來設定 IPv6 位址或 FQDN。

2.  在每個 UM IP 閘道上設定*IPAddressFamily*參數。若要啟用 VoIP 閘道接受 IPv6 封包，您必須將 UM IP 閘道設定為接受 IPv4 和 IPv6 兩種連線，或僅接受 IPv6 的連線，方法是透過使用 **Set-UMIPgateway** 指令程式設定。

3.  當您設定 UM IP 閘道後，您也必須在網路上設定 VoIP 閘道、IP PBX 和 SBC 以支援 IPv6。詳細資料可參閱您硬體廠商所提供支援 IPv6 的裝置清單以及如何正確設定的方式。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>每個撥號對應表最多有 200 個 UM IP 閘道。如果建立超過 200 個，則 UM 服務不會啟動。</td>
</tr>
</tbody>
</table>


## 啟用及停用 UM IP 閘道

根據預設，UM IP 閘道建立之後會保持啟用狀態。然而，您仍然可以啟用或停用 UM IP 閘道。如果您停用了某個 UM IP 閘道，您可以設定它強制所有 Exchange 伺服器中斷現有的呼叫。另外，您可將它設定為強制所有與 UM IP 閘道相關聯的 Exchange 伺服器停止處理任何 VoIP 閘道、IP PBX 或 SBC 提出的新呼叫。

如果您將整合通訊與 Office Communications Server R2 或 Microsoft Lync Server 整合，您必須允許只有一個 UM IP 閘道可以為使用者撥出呼叫，並停用與 SIP URI 撥號對應表相關聯之其他所有 UM IP 閘道的輸出呼叫。使用命令介面或 EAC 停用輸出呼叫。

當您選擇透過 UM IP 閘道允許內部部署和混合部署的撥出呼叫時，請選擇一個可能用來處理大部分流量的 UM IP。不可允許透過連接 Lync Server Director 集區的 UM IP 閘道撥出流量。這是為了確保由執行 Microsoft Exchange 整合通訊服務 (例如，「在電話上播放」的情況) 的信箱伺服器所放置的外部使用者輸出呼叫可確實周遊到公司的防火牆。

