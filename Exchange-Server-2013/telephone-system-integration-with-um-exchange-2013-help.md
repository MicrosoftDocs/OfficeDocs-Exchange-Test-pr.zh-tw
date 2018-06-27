---
title: 'UM 電話系統整合: Exchange Online Help'
TOCTitle: UM 電話系統整合
ms:assetid: b8790117-b040-4c84-9d34-005c75088e76
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ673558(v=EXCHG.150)
ms:contentKeyID: 50554057
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# UM 電話系統整合

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2016-12-09_

順利部署整合通訊 (UM)，您必須使用基本的電話語音概念和電話語音元件的確實了解。了解電話語音基礎後，UM 可以整合至 Exchange 組織。基本概念及元件包括：

  - 電路切換式與封包切換式網路

  - 專用交換機 (PBX)

  - IP PBX

  - 網際網路語音通訊協定 (VoIP)

  - VoIP 閘道

在內部部署、 混合部署、 或Office 365環境中，連接並設定必要的電話語音元件是使用或不 Lync Server Enterprise Voice 順利部署 UM、 最複雜且重要步驟。您將需要連線並設定 VoIP 閘道、 進階 VoIP 閘道、 Pbx、 IP Pbx 與傳統電話語音網路的工作階段邊界控制器 (Sbc) 並連線至電話語音網路如果您將會使用 Microsoft Lync Server 和 UM。

規劃和部署新的 UM 部署或升級舊版的語音郵件系統造成組織的挑戰。需要 VoIP 閘道、 Pbx、 IP Pbx、 Microsoft Lync 伺服器和整合通訊相關的重要知識。根據您與 Exchange 和語音郵件系統的技術功能，可能會想要取得協助的整合通訊的專員。Exchange 整合通訊專家可協助確保已從舊版或協力廠商語音信箱系統順利地轉換到 Exchange 整合通訊。如需如何連絡整合通訊的專員，請參閱[Microsoft Exchange Server 2013 整合通訊 (UM) 專家](http://go.microsoft.com/fwlink/p/?linkid=262708)的詳細資訊。

## 整合您的電話語音網路

整合的通訊需要您整合您的 Exchange Server 部署您現有的電話語音網路或組織的 Microsoft Lync Server 整合 UM。若要順利部署及管理 UM 語音信箱您需要請小心分析的現有電話語音基礎結構或 Microsoft Lync Server 企業語音部署並完成所需的規劃步驟。

## VoIP 閘道

當您在 Exchange 組織中部署 UM 時，您必須安裝、部署及設定一或多個 VoIP 閘道來連接電話語音網路中的 PBX，或是安裝、部署及設定已啟用工作階段初始通訊協定 (SIP) 的 PBX 或 IP PBX。

VoIP 閘道是舊版的 PBX 連線到您的 LAN 協力廠商硬體裝置。VoIP 閘道可讓與您組織中的 Exchange 伺服器進行通訊的 PBX 系統。

UM 依賴翻譯或轉換階段部門多工 (TDM) 或 ISDN 和 QSIG 電路切換型根據通訊協定從 PBX 例如 SIP、 即時傳輸通訊協定 (RTP) 或 T.38 IP 型或 VoIP 基礎通訊協定進行即時傳真傳輸的 VoIP 閘道的能力。VoIP 閘道是組成的功能和 UM 的運作方式。VoIP 閘道也可以使用 VoIP，而不是公用交換的電話網路 (PSTN) 電路切換型通訊協定的 PBX 系統連線。

選擇正確的 VoIP 閘道、 IP PBX、 已啟用 SIP 的 PBX 或 SBC 會的第一個部分整合您的電話語音網路與 UM。您必須設定為與 UM 搭配使用這些裝置。在內部部署和混合式部署中，您就需要部署所需的用戶端存取和信箱伺服器，並建立及設定所有必要的 UM 元件。為裝載的語音信箱與Office 365您正在不需要安裝及設定的任何伺服器。元件可讓您對您的 IP 資料網路進行連線從您的電話語音、 電路切換型網路和啟用語音信箱貴組織中的使用者。如需詳細資訊及支援的電話語音裝置，請參閱下列資源：

  - [Exchange 2013 的電話語音 advisor](telephony-advisor-for-exchange-2013-exchange-2013-help.md)

  - [支援 VoIP 閘道、 IP Pbx 和 Pbx 組態注意事項](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)

  - [支援工作階段邊界控制器的組態注意事項](configuration-notes-for-supported-session-border-controllers-exchange-2013-help.md)

## Microsoft Lync Server

整合的通訊可用於 Microsoft Lync Server 的語音訊息、 立即訊息、 增強顯示狀態、 音訊/視訊會議和電子郵件合併為熟悉的整合通訊功能。提供給您組織中使用者的企業語音功能整合 UM 和 Microsoft Lync Server 具有下列優點：

  - 各種應用程式的增強型平台服務通知，可以讓使用者得知連絡人的可用性。

  - 整合的立即訊息、 語音訊息、 會議、 電子郵件、 和其他通訊模式，可讓使用者選取任務的最適當的模式。使用者也可以切換從一個模式至另一個視。

  - 從任何可取得網際網路連線的位置取得替代通訊方式。

  - 適用於電話語音、立即訊息和會議的智慧用戶端 (Microsoft Lync)。

  - 在多項裝置上的使用者經驗持續性。

Exchange UM 路由元件會處理語音郵件路由之間 Lync Server 與 Exchange 整合通訊功能整合 Lync Server 的伺服器。Lync Server 中找到的 Exchange UM 路由元件也會處理重新路由語音信箱透過 PSTN 若都無法提供 Exchange 伺服器。如果您有企業語音部署在分支網站，且這些網站沒有可恢復的 WAN 連結至中央網站，請在分支網站部署 Survivable Branch Appliance 提供語音信箱為分支使用者如果 WAN 連結下降。WAN 連結無法使用時，Survivable Branch Appliance 會執行下列動作：

  - 透過 PSTN，將未接聽的電話重新路由至中央站台的 Exchange 伺服器。

  - 讓使用者能夠透過 PSTN 擷取語音訊息。

  - 將未接來電通知排入佇列中，然後在 WAN 連結恢復時將它們上傳至 Exchange 伺服器。

如需 Microsoft Lync Server 的詳細資訊，查看[Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您正在將 Unified Messaging 和 Lync Server 整合在內部部署或混合式部署中，未接來電通知都無法提供使用者沒有信箱位於 Exchange 2007 或 Exchange 2010 信箱伺服器。當使用者中斷通話傳送至信箱伺服器之前，會產生未接的來電通知。</td>
</tr>
</tbody>
</table>

