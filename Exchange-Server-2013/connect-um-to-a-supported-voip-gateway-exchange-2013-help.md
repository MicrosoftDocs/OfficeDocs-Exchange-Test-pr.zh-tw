---
title: '連線至受支援的 VoIP 閘道的 UM: Exchange 2013 Help'
TOCTitle: 連線至受支援的 VoIP 閘道的 UM
ms:assetid: b8dfc8bd-2ee5-418d-b0a4-4fa2ec7e2a2e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124360(v=EXCHG.150)
ms:contentKeyID: 50554088
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 連線至受支援的 VoIP 閘道的 UM

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-04-19_

您正在設定設定整合通訊 (UM)，您必須設定語音 over IP (VoIP) 閘道、 IP Pbx、 已啟用 SIP 的 Pbx 或工作階段邊界控制器 (Sbc) 與執行 Microsoft Exchange Unified Messaging Call Router 服務的 Client Access server 和 Mailbox server Exchange組織中執行 Microsoft Exchange 整合通訊服務通訊網路上。您也必須設定的用戶端存取和信箱伺服器與 VoIP 閘道、 IP Pbx、 已啟用 SIP 的 Pbx 或 Sbc 通訊。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>將用戶端存取伺服器和信箱伺服器連線到您資料網路上的 VoIP 閘道、IP PBX、啟用 SIP 的 PBX 或 SBC 之後，您必須建立需要的 UM 元件並為使用者啟用整合通訊，讓他們能夠使用語音信箱系統。</td>
</tr>
</tbody>
</table>


## 步驟

下列是將 VoIP 閘道、IP PBX、啟用 SIP 的 PBX 或 SBC 連線至用戶端存取伺服器和信箱伺服器的基本步驟：

步驟 1： 安裝在組織中的用戶端存取和信箱伺服器。

步驟 2： 建立及設定電話分機號碼、 SIP URI 或 E.164 UM 撥號對應表。

步驟 3： 建立並設定 UM IP 閘道。您必須建立並設定 UM IP 閘道的每個 VoIP 閘道、 IP PBX、 已啟用 SIP 的 PBX、 或會接受傳入呼叫並傳送的撥出電話的 SBC。

步驟 4： 在必要時建立新的 UM 群組搜尋。如果您建立 UM IP 閘道器並沒有指定 UM 撥號對應表，將會自動建立 UM 群組搜尋。

請參閱下列各節以取得每個步驟的相關資訊。

## 步驟 1： 安裝用戶端存取和信箱伺服器

當您正在您組織中部署 Exchange 伺服器時，您可以在同一部電腦上安裝 Client Access 與 Mailbox server 或從信箱伺服器在個別電腦上安裝 Client Access server。若要安裝的用戶端存取伺服器，請從安裝媒體執行 Setup.exe。您使用同一個命令是從信箱伺服器在個別電腦上安裝 Client Access server 或安裝在同一部電腦上時。如需詳細資訊，請參閱[使用安裝精靈安裝 Exchange 2013](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)。如果您想要新增至現有的 Exchange server 的特性和功能，您可以使用**\[程式和功能**或 Setup.exe。

## 步驟 2： 建立並設定 UM 撥號對應表

您已安裝所需的伺服器之後，您必須先建立 UM 撥號對應表。UM 撥號對應表包含可讓您連線至您的電話語音網路連結至單一或多個 UM IP 閘道器的組態設定。UM IP 閘道和 UM 群組搜尋直接連結至 UM 撥號對應表和也會需要。如需詳細資訊，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

UM 撥號對應表建立已啟用 UM 的信箱中之使用者的電話分機號碼的連結。當您建立 UM 撥號對應表時，您可以設定的位數的分機號碼、 統一資源識別元 (URI) 類型和 VoIP 安全性設定的撥號對應表。

有三種類型的撥號對應表： 電話分機號碼、 工作階段初始通訊協定 (SIP) URI 和 E.164。當您建立及設定 UM 撥號對應表時，您必須判斷已寄件者 IP PBX、 已啟用 SIP 的 PBX 或 PBX 與電話是否要傳送至電話分機號碼或 E.164 格式中的 Client Access server 或信箱伺服器的資訊類型。如果您正在部署 Microsoft Office Communications Server 2007 R2 或 Microsoft Lync Server，您必須建立及設定的 SIP URI 撥號對應表。

## 步驟 3： 建立並設定 UM IP 閘道器

建立之後 UM 撥號對應表，您必須建立 UM IP 閘道來代表每個 VoIP 閘道、 IP PBX 或 SBC 網路上。當您建立 UM IP 閘道時，您可以將其設定為使用 IP 位址或完整的網域名稱 (FQDN)。如果您使用 FQDN，您必須確定讓主機名稱正確解析為 IP 位址已正確設定 IP 閘道的 DNS 主機記錄。

安裝 VoIP 閘道、 IP PBX 或 SBC 之後，您必須建立 UM IP 閘道來代表實體硬體裝置。您已建立 UM IP 閘道器之後，請使用 UM IP 閘道的用戶端存取伺服器會將 SIP OPTIONS 要求傳送給 VoIP 閘道、 IP PBX 或 SBC 可確保回應中。VoIP 閘道、 IP PBX、 已啟用 SIP 的 PBX 或 SBC 沒有回應，如果用戶端存取伺服器會記錄與識別碼 1088年說明事件的要求失敗。若要解決此問題，請確定 VoIP 閘道、 IP PBX 或 SBC 會提供與線上和整合通訊設定正確。

僅限 VoIP 閘道、 IP PBX 或已列為信任的 SIP 對等的 SBC 要通訊用戶端存取和信箱伺服器。在某些情況下，如果兩個 VoIP 閘道、 IP Pbx 或 Sbc 設定為使用相同的 IP 位址，將記錄與識別碼 1175年事件。如果您已在網路上與 VoIP 閘道的完整的網域名稱 (Fqdn) 設定 DNS 區域，可能會發生此事件。Unified Messaging 提供保護，避免未經授權的要求，以擷取信箱伺服器上的整合通訊的 Web 服務虛擬目錄的內部 URL，然後使用 URL 建立清單的 Fqdn 為受信任的 SIP 對等。兩個 Fqdn 解析為相同的 IP 位址之後，就會記錄此事件。

您必須重新啟動MicrosoftExchange整合通訊服務的 UM IP 閘道設定成使用 FQDN 及 UM IP 閘道的 DNS 記錄變更之後啟動服務。如果您不重新啟動服務，Mailbox server 將無法找到的 UM IP 閘道。因為在信箱伺服器會保留在記憶體中的所有 UM IP 閘道器快取且僅時重新啟動服務執行 DNS 解析或已變更的 VoIP 閘道、 IP PBX 或 SBC 設定這時發生。

Exchange Unified Messaging 支援各種 VoIP 閘道廠商與 IP Pbx、 已啟用 SIP 的 Pbx 和 Sbc 的其他廠商。每個支援的 VoIP 閘道器的設計目的連線至各種協力廠商 PBX 系統。

如需 VoIP 閘道的詳細資訊，請參閱下列主題：

  - [建立 UM IP 閘道器](create-a-um-ip-gateway-exchange-2013-help.md)

  - [支援 VoIP 閘道、 IP Pbx 和 Pbx 組態注意事項](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)

  - [連線至 UM VoIP 閘道、 IP PBX 或工作階段邊界控制器](connect-a-voip-gateway-ip-pbx-or-session-border-controller-to-um-exchange-2013-help.md)

如需詳細資訊，請參閱[連線至您的電話網路的語音郵件系統](connect-your-voice-mail-system-to-your-telephone-network-exchange-2013-help.md)。

## 步驟 4： 建立新的 UM 群組搜尋 （如果需要）

群組搜尋是用來描述一群專用交換機 (PBX) 字詞或 IP PBX 副檔名數字的共用的使用者。群組搜尋可用來快速分散移入或移出特定業務單位的通話。建立及定義群組搜尋最小化時接到電話時來電 places 來電者會收到忙線訊號的機會。

UM 群組搜尋鏡像 Pbx 與 IP Pbx 上所使用的群組搜尋。當您設定 Pbx 或 IP Pbx 時，您必須建立並設定一個或多個 UM 群組搜尋。UM 群組搜尋作為 UM IP 閘道和 UM 撥號對應表之間的連結。

根據如何建立 UM IP 閘道器，您可能必須建立一或多個新的 UM 群組搜尋。如果您不連結撥號對應表與 UM IP 閘道器建立 UM IP 閘道時，預設會建立單一的 UM 群組搜尋。連結時 UM IP 閘道 um 撥號對應表建立 UM IP 閘道器、 所有來電將會都傳送到 UM IP 閘道器與這些通話將會接受用戶端存取和信箱伺服器所時。如果您不連結至 UM 撥號對應表 UM IP 閘道器當您建立 UM IP 閘道器，必須使用正確的引導識別碼的來電轉接至撥號對應表的 UM IP 閘道建立 UM 群組搜尋。

如果您有多個 Outlook Voice Access 和自動語音應答號碼並已連結至撥號對應表 UM IP 閘道器，您需要刪除 UM 群組搜尋之預設已建立並建立多個 UM 群組搜尋。如需詳細資訊如何建立 UM 群組搜尋，請參閱[建立 UM 群組搜尋](create-a-um-hunt-group-exchange-2013-help.md)。

