---
title: 'UM 連接至電話系統: Exchange 2013 Help'
TOCTitle: UM 連接至電話系統
ms:assetid: 92c3e029-f732-4d6d-b147-2b3006d5f088
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ673544(v=EXCHG.150)
ms:contentKeyID: 50554033
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# UM 連接至電話系統

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2012-11-30_

整合通訊 (UM) 結合語音訊息和電子郵件訊息到一個可從許多不同的裝置存取的信箱。使用者可以從其電子郵件收件匣或從任何電話使用 Outlook 語音存取聆聽其語音郵件訊息。

當您正在部署 UM 部署 Microsoft Exchange 組織中時，您必須安裝、 部署及設定單一或多個 Voice over IP (VoIP) 連線至專用交換機 (Pbx) 電話語音網路中或安裝、 部署及設定已啟用工作階段初始通訊協定 SIP 的 Pbx 或 IP Pbx 的閘道。如果您正在升級您目前的語音郵件系統，您將需要部署連線至您的電話語音網路裝置安裝 Exchange 用戶端存取和信箱伺服器，然後再建立所需的 UM 元件可讓您的電話語音網路連線至您資料的網路。這可讓與電話語音網路連線至您 VoIP 閘道、 IP Pbx 或已啟用 SIP 的 Pbx 與這些裝置連線至 Exchange 組織的傳入呼叫。

如果您是安裝、 部署及設定 Microsoft Office Communications Server 2007 R2 或 Microsoft Lync Server，您將不會使用 VoIP 閘道、 IP Pbx 或已啟用 SIP 的 Pbx 直接連線至 Exchange 整合通訊。而是 Lync 中繼伺服器與 VoIP 閘道或有中繼伺服器的功能的進階的 VoIP 閘道和 VoIP 閘道可讓您連線至 Exchange UM。針對 Enterprise Voice 啟用的 UM 使用者可以擷取、 收聽、 回覆語音郵件與撥出電話。他們也可以使用 Office Communicator 或 Lync 用戶端包括目前狀態和立即訊息 (IM) 其他 Lync 相關功能的存取權。

下列資訊可協助您設定及部署 UM 和啟用您組織中使用者的語音信箱功能：

  - [連線至 UM VoIP 閘道、 IP PBX 或工作階段邊界控制器](connect-a-voip-gateway-ip-pbx-or-session-border-controller-to-um-exchange-2013-help.md)  了解如何連接 VoIP 閘道或 IP Pbx to UM。

  - [Exchange 2013 的電話語音 advisor](telephony-advisor-for-exchange-2013-exchange-2013-help.md)  了解支援 VoIP 閘道、 IP Pbx 和 Pbx。

  - [支援 VoIP 閘道、 IP Pbx 和 Pbx 組態注意事項](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md) 了解如何設定 VoIP 閘道、 IP Pbx 和 Pbx。

