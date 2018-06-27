---
title: 'Connect a VoIP 閘道與 PBX 通訊: Exchange 2013 Help'
TOCTitle: Connect a VoIP 閘道與 PBX 通訊
ms:assetid: 76bcdc54-3ec2-408a-bdbe-37826580dd62
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa998872(v=EXCHG.150)
ms:contentKeyID: 50554011
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Connect a VoIP 閘道與 PBX 通訊

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2016-12-15_

當您設定電話語音和資料網路的整合通訊 (UM) Microsoft Exchange Server 2013中時，您必須設定 VoIP 閘道讓他們與執行 Microsoft Exchange Unified Messaging Call Router 服務的用戶端存取伺服器與執行 Microsoft Exchange 整合通訊服務的 Mailbox server 通訊。您也必須設定與專用交換機 (Pbx) 您組織中進行通訊的 VoIP 閘道器。您可以使用 \[本主題中的資訊和連結，設定 VoIP 閘道與 PBX 通訊。

## 設定 VoIP 閘道

當您設定 VoIP 閘道時，您必須考量 VoIP 閘道裝置是否類比、 數位或類比和數位。如果類比連接至 PBX 的 VoIP 閘道介面，您必須正確設定以啟用 VoIP 閘道與 PBX 通訊適當的設定。連接至 PBX 的 VoIP 閘道介面是否數位，則可能需要啟用與 PBX 通訊的數位介面進行其他設定。

下的建議的資源 Exchange TechCenter 中提供可協助您正確設定 VoIP 閘道及 Pbx 的資訊：

  - **支援 VoIP 閘道、 IP PBX 和 PBX 文件**   [Exchange 2013 的電話語音 advisor](telephony-advisor-for-exchange-2013-exchange-2013-help.md)包括組態檔以及您可以使用當您設定 VoIP 閘道及 Pbx 的安裝程式資訊。

  - **設定與技術的附註**   [支援 VoIP 閘道、 IP Pbx 和 Pbx 組態注意事項](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)包含設定檔及設定 VoIP 閘道和 Pbx 時您可以使用的設定資訊。

  - **設定 AudioCodes 式 VoIP 閘道** [Microsoft Exchange Server 資源頁面](https://www.audiocodes.com/solutions/microsoft/exchange-server)提供可協助您設定為使用 AudioCodes 式 VoIP 閘道與整合通訊的最新支援和組態資訊。

  - **設定 Dialogic 型 VoIP 閘道**  [Dialogic 網站](https://www.dialogic.com/)提供 Dialogic 型 VoIP 閘道器最新的支援和組態資訊。

建議您打算部署整合通訊的所有客戶都取得協助的整合通訊的專員。Exchange 整合通訊專家可協助確保有順利升級至 \[整合通訊從舊版或協力廠商語音郵件系統並協助您規劃及部署與 Exchange 整合通訊的新語音郵件系統。 部署新的語音郵件系統或升級舊版的語音一需要 VoIP 閘道、 Pbx 和整合通訊相關的重要知識。如需如何連絡整合通訊專家的詳細資訊，請參閱[Microsoft Exchange Server 2013 整合通訊 (UM) 專家](http://go.microsoft.com/fwlink/p/?linkid=262708)或在[Microsoft Pinpoint](https://go.microsoft.com/fwlink/p/?linkid=261951)認證的 UM 夥伴。

## 相關資訊

[支援 VoIP 閘道、 IP Pbx 和 Pbx 組態注意事項](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)

[連線至受支援的 VoIP 閘道的 UM](connect-um-to-a-supported-voip-gateway-exchange-2013-help.md)

