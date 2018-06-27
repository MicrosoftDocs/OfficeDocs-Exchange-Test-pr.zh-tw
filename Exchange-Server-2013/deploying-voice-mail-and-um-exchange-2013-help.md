---
title: '部署語音信箱和 UM: Exchange 2013 Help'
TOCTitle: 部署語音信箱和 UM
ms:assetid: 3df61b62-a1e4-41fb-969c-319189ae4e42
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ673519(v=EXCHG.150)
ms:contentKeyID: 50472941
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 部署語音信箱和 UM

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2016-12-09_

Exchange 整合通訊 (UM) 可讓您提供語音信箱服務給組織內的使用者。當您部署整合通訊時，必須將 Exchange 伺服器部署與您組織現有的電話語音系統或 Microsoft Lync Server 整合。成功的部署需要仔細分析您現有的電話基礎結構，並執行正確的規劃步驟以部署和管理整合通訊中的語音信箱。若您將 Exchange 與 Lync Server 整合，也需熟悉該產品：

當您部署整合通訊時，根據組織內找到的電話語音硬體而定，會有多個選項提供給您。如果您要將 UM 連線到電話語音網路，組織可以採用下列其中一種電話語音組態：

  - 含有一或多個 PBX 的一或多個 VoIP 閘道

  - 一或多個 IP PBX

  - 一或多個啟用 SIP 的 PBX

  - Microsoft Office Communications Server 2007 R2 或 Microsoft Lync Server 2010 或 2013

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您在託管或混合環境中部署 Exchange UM 時，必須部署工作階段邊界控制器 (SBC)。SBC 不會啟用 UM 連接到電話語音網路，或為組織提供撥號音。不過，它們確實會使用公用或私有 WAN 上的 IP 通訊協定，將您的內部部署 UM 部署連接到資料中心。</td>
</tr>
</tbody>
</table>


**電話語音硬體**   選擇正確的 VoIP 閘道、IP PBX 或 SBC 是整合電話語音網路與 UM 的第一步。需設定那些裝置與 UM 配合、部署需要的用戶端存取與信箱伺服器、以及建立並設定所有必要的 UM 元件。這些元件可讓您將電路通訊協定網路與 IP 資料網路連接，並為組織中的使用者啟用語音信箱。如需詳細資訊，請參閱 [Exchange 2013 的電話語音 advisor](telephony-advisor-for-exchange-2013-exchange-2013-help.md)。

**Microsoft Lync Server**   整合通訊可以使用 Microsoft Lync Server，將語音訊息、立即訊息、增強型平台服務、影音會議和電子郵件合併成令人熟悉的整合式通訊體驗。整合 UM 與 Lync Server 具有下列優點：

  - 各種應用程式的增強型平台服務通知，可以讓使用者得知連絡人的可用性。

  - 整合立即訊息、語音訊息、會議、電子郵件及其他通訊方法，可讓使用者選取工作上最適合的方法。使用者也可以視需要從某個方法切換為另一個方法。

  - 從任何可取得網際網路連線的位置取得替代通訊方式。

  - 適用於電話語音、立即訊息和會議的智慧用戶端 (Microsoft Lync)。

  - 在多項裝置上的使用者經驗持續性。

如需 Lync Server 的詳細資訊，請參閱[Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752)。

## 部署步驟

整合通訊有許多部署選項可用。每個選項都有幾個共通步驟，以建立可擴充和高度可用的系統來支援大量的使用者。這些步驟如下：

1.  使用整合通訊部署和設定電話語音元件或 Microsoft Lync Server。

2.  確認您已正確安裝整合通訊所需的用戶端存取和信箱伺服器。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb125224.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您必須先至少在組織中部署一個 Exchange 2013 Mailbox Server，才能將 VoIP 閘道或 IP PBX 設定為將 UM SIP 和 RTP 流量傳送至 Exchange 2013 Client Access Server。</td>
    </tr>
    </tbody>
    </table>


3.  建立並設定所需的整合通訊 元件，包括 UM 撥號對應表、UM IP 閘道器、UM 群組搜尋和 UM 信箱原則。

4.  執行後期部署工作，包括部署 mutual TLS 憑證、建立 UM 自動語音應答和用戶端功能。

如需部署整合通訊的詳細資料，請參閱[部署 Exchange 2013 UM](deploy-exchange-2013-um-exchange-2013-help.md)。

整合您的整合通訊環境和 Microsoft Lync Server 時，還有一些額外的規劃考量。如需詳細資訊，請參閱[部署 Exchange 2013 UM 和 Lync Server 概觀 （英文）](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md)。

