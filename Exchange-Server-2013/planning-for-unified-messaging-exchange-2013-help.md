---
title: '整合通訊的規劃: Exchange 2013 Help'
TOCTitle: 整合通訊的規劃
ms:assetid: 942788b1-b19d-40b3-a52e-2e1fef8df3f9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ674306(v=EXCHG.150)
ms:contentKeyID: 50473800
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 整合通訊的規劃

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2016-12-09_

當您規劃整合通訊 (UM) 部署時，有許多能夠順利部署 UM，您必須考慮的因素。您必須了解整合通訊和每個元件和功能的不同的元素，您可以適當地規劃整合通訊基礎架構與部署。配置時間規劃及完成這些問題可協助您部署在組織中的 \[整合通訊時防止發生的問題。

您可能會在新的 Exchange 組織中部署整合通訊或從舊版或協力廠商語音郵件解決方案升級。如果您正在升級，您需要決定是否要轉換之裝置的會接受使用 IP 資料網路的電話語音基礎的電路型通訊協定或是否要部署企業語音解決方案類似 Microsoft Lync Server。這是只的第一個步驟準備自行了解及部署 UM 您的組織。

## 規劃您的語音郵件系統

UM 提供語音信箱、 傳真及電子郵件可從電話、 使用者的電腦或行動裝置的一個存放區中。使用者可以存取語音訊息、 電子郵件、 行事曆資訊及位於Outlook Web AppOutlook等的電子郵件用戶端從 Exchange 信箱中的個人連絡人。

執行 Microsoft Exchange Unified Messaging Call Router 服務的用戶端存取伺服器與執行 Microsoft Exchange 整合通訊服務的 Mailbox server 的設計被用來為在組織中的使用者提供語音信箱功能。

Mailbox server 依賴用戶端存取伺服器轉送的 SIP 流量從來電然後建立與 VoIP 閘道、 IP PBX 或工作階段邊界控制器 (SBC) 的連線並接受 RTP/SRTP 媒體流量。所有的語音信箱和傳真訊息一起送出從傳遞至使用者信箱的信箱伺服器上的 Microsoft Exchange 整合通訊服務。若要使用的語音信箱功能整合通訊的使用者，他們必須具備 Exchange 信箱。

## 規劃 UM 部署

通常較簡單的整合通訊拓撲、 更輕鬆地 UM 是以部署及維護。安裝少用戶端存取和信箱伺服器，並建立最少的整合通訊元件-like 計劃、 自動語音應答和 UM 信箱原則的 UM 撥號對應表 — 視需要以支援您的業務與組織目標。與複雜網路和電話語音的環境、 多個業務單位或其他複雜性的大型企業將會需要較複雜的規劃較小型組織具有較簡單的整合通訊需求。

以下是一些規劃貴組織中的整合通訊時應該考量的區域：

  - **組織的需求**  評估您的業務需求、 部署語音郵件系統、 您實體網路和商務拓撲及貴組織的安全性需求的實用性。

  - **電話語音的需求**  檢閱您的現有電話語音、 電路切換型網路和語音郵件系統。

  - **網路需求**  分析您的網路拓撲，您目前封包切換 IP 網路設計包括您的 LAN 和 WAN 連線點和裝置。

  - **Active Directory （目錄服務）**  檢查您目前的實作和設計並考慮如何整合 UM。

  - **部署模型**  決定是否要有混合部署、 線上僅限，或內部部署 UM 部署。

  - **Exchange 需求**  決定下列項目：
    
      - 多少使用者將使用的語音信箱。
    
      - UM 功能 （英文） 及服務您想要部署，例如並行通話內部和外部使用者存取，傳入傳真語音郵件預覽，等等。
    
      - 您必須部署用戶端存取和信箱伺服器的數目。
    
      - 儲存需求及語音信箱使用者的配額。
    
      - 高可用性和站台恢復能力最佳的設計。這包括 UM 系統需求、 提供高度可用且擴充度佳的 UM 部署和系統以確保效能的硬體需求。

  - **與電話語音元件和裝置整合**  決定是否使用傳統的電話語音設備或 Microsoft Lync Server。請考慮要放置 VoIP 閘道、 電話語音設備及用戶端存取和信箱伺服器，以及是否要在組織中啟用 Enterprise Voice。

## 電話語音網路連接

整合的通訊會要求您與您現有的電話系統整合您的 Exchange Server 部署或整合 Microsoft Lync Server。必須小心分析您的現有電話語音基礎結構和 Microsoft Lync Server\]，然後依照正確的規劃步驟來部署和管理 UM 語音信箱已成功。

**VoIP 閘道器**選擇正確的 VoIP 閘道、 IP PBX、 已啟用 SIP 的 PBX 或 SBC 是只是第一個步驟中整合您的電話語音網路與 UM。您必須設定這些裝置能夠使用 UM、 部署所需的用戶端存取和信箱伺服器，並建立及設定所有必要的 UM 元件。這些元件可讓您進行電路為基礎的通訊協定網路 IP 資料網路的連線並啟用使用者的語音信箱。

**Microsoft Lync Server**  整合的通訊可用於 Microsoft Lync Server 的語音訊息、 立即訊息、 增強顯示狀態、 音訊/視訊會議和電子郵件合併為熟悉的整合通訊功能。整合 UM 和 Microsoft Lync Server 具有下列優點：

  - 各種應用程式的增強型平台服務通知，可以讓使用者得知連絡人的可用性。

  - 整合的立即訊息、 語音訊息、 會議、 電子郵件、 和其他通訊方法，可讓使用者選取任務最合適的方法。使用者也可以切換其中一種方法從至另一個視。

  - 從任何可取得網際網路連線的位置取得替代通訊方式。

  - 適用於電話語音、立即訊息和會議的智慧用戶端 (Microsoft Lync)。

  - 在多項裝置上的使用者經驗持續性。

如需 Microsoft Lync Server 的詳細資訊，查看[Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>規劃和部署整合通訊造成某些挑戰。根據您與 Exchange 和語音郵件系統的技術功能，可能會想要取得協助的整合通訊的專員。Exchange 整合通訊專家可協助確保已從舊版或協力廠商語音信箱系統順利地轉換到 Exchange 整合通訊。執行新部署或升級舊版的語音郵件系統要求 VoIP 閘道、 Pbx 和整合通訊相關的重要知識。如需如何連絡整合通訊的專員，請參閱<a href="http://go.microsoft.com/fwlink/p/?linkid=262708">Microsoft Exchange Server 2013 整合通訊 (UM) 專家</a>的詳細資訊。</td>
</tr>
</tbody>
</table>


## 部署步驟

可以使用整合通訊的許多部署選項。每個選項有幾個步驟中一般所建立的可擴充及高度可用的系統可支援大量的使用者。這些步驟如下所示：

1.  使用整合通訊部署和設定電話語音元件或 Microsoft Lync Server。

2.  確認您已正確安裝整合通訊所需的用戶端存取和信箱伺服器。

3.  建立並設定必要的整合通訊元件，包括 UM 撥號對應表、 UM IP 閘道器、 UM 群組搜尋和 UM 信箱原則。

4.  執行後期部署工作，包括取得的相互 TLS 憑證、 建立 UM 自動語音應答，以及設定傳真。

如需部署整合通訊的詳細資料，請參閱[部署 Exchange 2013 UM](deploy-exchange-2013-um-exchange-2013-help.md)。

整合您的整合通訊環境和 Microsoft Lync Server 時，還有一些額外的規劃考量。如需詳細資訊，請參閱[部署 Exchange 2013 UM 和 Lync Server 概觀 （英文）](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md)。

