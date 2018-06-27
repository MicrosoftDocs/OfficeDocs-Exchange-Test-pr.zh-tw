---
title: '連線至 UM VoIP 閘道、 IP PBX 或工作階段邊界控制器: Exchange 2013 Help'
TOCTitle: 連線至 UM VoIP 閘道、 IP PBX 或工作階段邊界控制器
ms:assetid: a7cecf59-b93a-413b-bb88-29f2669ef2cf
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124084(v=EXCHG.150)
ms:contentKeyID: 50554046
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 連線至 UM VoIP 閘道、 IP PBX 或工作階段邊界控制器

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2016-12-09_

您必須設定 Voice over IP (VoIP) 閘道與 IP 專用交換機進行交換 (Pbx) 的正確當您部署整合通訊 (UM) 的組織。如果您正在部署 UM 在混合環境中，您也需要正確設定您的工作階段邊界控制器 (Sbc)。為達成此目的，您需要設定的介面或 VoIP 閘道、 IP Pbx 和 Sbc 與執行 Microsoft Exchange Unified Messaging Call Router 服務的用戶端存取伺服器與執行 Microsoft Exchange 整合通訊服務的 Mailbox server 通訊的介面。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您執行管理工作如 VoIP 閘道、 IP PBX 或 SBC 使用網頁瀏覽器中時，未加密的 HTTP 要求透過網路傳送。若要增加 VoIP 閘道、 IP Pbx 或 Sbc 您網路上的安全性層級使用網際網路通訊協定安全性 (IPsec) 或 Secure Sockets Layer (SSL) 可協助保護系統管理認證和透過網路傳送的資料。也建議您使用的強式驗證機制模式和複雜的管理密碼來保護裝置的系統管理認證。</td>
</tr>
</tbody>
</table>


## 電話語音 IP 裝置介面

有數種類型的連接埠或您必須設定啟用 PBX、 VoIP 閘道、 IP PBX 或 SBC 及網路上的用戶端存取和信箱伺服器之間的通訊的介面。當您設定 VoIP 閘道、 IP PBX 或 SBC 時，您必須考慮裝置是否類比、 數位或類比和數位。

如果類比連接至 PBX 的 VoIP 閘道介面，您必須正確設定適當設定，以啟用 VoIP 閘道與用戶端存取和信箱伺服器進行通訊。IP Pbx 和 Sbc 您必須也正確設定 IP 介面讓這些裝置與用戶端存取和信箱伺服器進行通訊。所有這些裝置具有不同類型的連線或裝置型號與廠商根據可用的連接埠。

若要啟用與網路上的用戶端存取和信箱伺服器之間的通訊：

  - 如 VoIP 閘道器\] 中，您必須設定與您 Pbx 通訊的電話語音介面和您必須設定裝置的 IP 介面。

  - 如 IP Pbx，必須設定電路型並網路或 IP 為基礎的連線。

  - Sbc 的您必須設定兩個 IP 介面，一個適用於您的網路，透過網際網路或專用的 WAN 連線所連線的其他介面。

以下是 Exchange TechCenter 上找到的資源提供可協助您正確設定 VoIP 閘道、 IP Pbx 和 Sbc 的資訊清單：

  - **支援 IP 閘道、 IP PBX 和 PBX 文件**   [Exchange 2013 的電話語音 advisor](telephony-advisor-for-exchange-2013-exchange-2013-help.md)包含設定檔及設定 VoIP 閘道、 IP Pbx、 Pbx 和 Sbc 時，您可以使用的設定資訊。

  - **設定與技術的附註**   [支援 VoIP 閘道、 IP Pbx 和 Pbx 組態注意事項](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)包含設定檔及設定 VoIP 閘道、 IP Pbx 和 Pbx 時您可以使用的設定資訊。

  - **針對 Exchange UM online 組態注意事項**   [支援工作階段邊界控制器的組態注意事項](configuration-notes-for-supported-session-border-controllers-exchange-2013-help.md)包含設定檔及設定 Sbc 時，您可以使用的設定資訊。

整合的通訊專家可用來協助您在設定電話語音與 IP 型網路裝置。整合通訊專家可協助確保有順利地轉換到整合通訊從舊版或協力廠商語音信箱系統或協助您規劃及部署新的語音信箱系統與 Exchange 整合通訊。部署新的語音郵件系統或升級舊版的其中一個需要 VoIP 閘道、 IP Pbx、 Pbx 和整合通訊相關的重要知識。更多如何連絡 Unified Messaging 專員的相關資訊，如[Microsoft Exchange Server 2013 整合通訊 (UM) 專家](http://go.microsoft.com/fwlink/p/?linkid=262708)或在[Microsoft Pinpoint](https://go.microsoft.com/fwlink/p/?linkid=261951)的認證的 UM 協力廠商。

設定 VoIP 閘道、 IP PBX 或 SBC IP 介面之後，您必須建立並設定 UM IP 閘道來代表您已部署了每個裝置。如需如何建立 UM IP 閘道器，請參閱[建立 UM IP 閘道器](create-a-um-ip-gateway-exchange-2013-help.md)的詳細資訊。

建立 UM IP 閘道器後，UM IP 閘道相關聯的用戶端存取和信箱伺服器會將 SIP OPTIONS 要求傳送給 VoIP 閘道、 IP PBX 或 SBC 可確保有回應。如果不會回應 VoIP 閘道、 IP PBX 或 SBC，Mailbox server 將記錄與 ID 1088 表示事件要求失敗。若要解決此問題，請確定 VoIP 閘道、 IP PBX 或 SBC 會提供與線上和整合通訊設定正確。

在 Client Access server 和信箱伺服器將只與 VoIP 閘道、 IP PBX 或已列為信任的工作階段初始通訊協定 (SIP) 對等的 SBC 通訊。當多個 DNS 主機共用相同的 IP 位址會記錄與識別碼 1175年事件。如果您已設定 DNS 區域 fqdn 為 VoIP 閘道網路上，可能會發生此事件。Unified Messaging 提供保護，避免未經授權的要求，以擷取信箱伺服器上的整合通訊的 Web 服務虛擬目錄的內部 URL，然後使用 URL 建立清單的 Fqdn 為受信任的 SIP 對等。兩個 Fqdn 解析為相同的 IP 位址之後，就會記錄此事件。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您必須重新啟動MicrosoftExchange整合通訊服務如果在 VoIP 閘道、 IP PBX、 SBC 設定為具有 FQDN 和 DNS 記錄之 VoIP 閘道、 IP PBX 或 SBC 變更之後啟動服務。如果您不重新啟動服務，Mailbox server 將無法找到 VoIP 閘道、 IP PBX 或 SBC。因為在信箱伺服器維護所有 VoIP 閘道、 IP Pbx 或 Sbc 在記憶體中的快取且僅時重新啟動服務執行 DNS 解析或已變更的 VoIP 閘道、 IP PBX 或 SBC 設定這時發生。</td>
</tr>
</tbody>
</table>

