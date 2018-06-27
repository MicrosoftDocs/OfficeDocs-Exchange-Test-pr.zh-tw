---
title: 'UM 服務: Exchange 2013 Help'
TOCTitle: UM 服務
ms:assetid: f36835f2-1e5f-4e5a-88bc-0672af1e3498
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb125191(v=EXCHG.150)
ms:contentKeyID: 50554106
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# UM 服務

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2012-11-18_

執行 Microsoft Exchange 整合通訊呼叫路由器服務的用戶端存取伺服器和執行 Microsoft Exchange 整合通訊服務的信箱伺服器都可讓您為組織中的使用者部署整合通訊 (UM) 和語音信箱功能。

要尋找與 UM 服務相關的管理工作嗎？請參閱[UM 服務程序](um-services-procedures-exchange-2013-help.md)。

**目錄**

Client Access and Mailbox servers

Server configuration settings

Server operation

## Client Access Server 和信箱伺服器

在 Exchange 2013 中，Exchange 2007 和 Exchange 2010 伺服器角色結合為二種伺服器類型，而那些伺服器角色之所有元件或服務，都是在同一個實體伺服器或兩個個別伺服器 (稱為用戶端存取和信箱) 上執行。

在此新模型中，用戶端存取伺服器負責進行自動探索、 Secure Sockets Layer (SSL)、 驗證、 重新導向及代理。用戶端存取伺服器是針對任何撥入通話的進入點或整合通訊工作階段初始通訊協定 (SIP) 要求。路由邏輯和 SIP 重新導向會實作為自動包含在用戶端存取伺服器的服務。此服務會稱為 Microsoft Exchange Unified Messaging Call Router 服務。在組織中每個用戶端存取伺服器上執行。

當用戶端存取伺服器會接收 SIP INVITE 的來電時，Microsoft Exchange Unified Messaging Call Router 服務會重新導向的信箱伺服器的傳入呼叫。接著 VoIP 閘道、 IP PBX 或工作階段邊界控制器 (SBC) 與主控使用者的信箱的信箱伺服器之間建立的媒體通道 （RTP 或 SRTP）。雖然用戶端存取伺服器會作為 SIP 重新導向程式，它只會處理 VoIP 閘道、 IP Pbx 或 Sbc 的 SIP 要求。它不會收到任何媒體流量。使用 RTP 或 SRTP 的媒體流量只會傳遞 Mailbox server 和如 VoIP 閘道、 IP Pbx 或 Sbc 的 SIP 對等之間。當您部署Exchange 2013和 UM 時，您必須設定 VoIP 閘道、 IP Pbx 或指向您已安裝，以便讓來電會路由 um 傳送正確的 Client Access server 的 Sbc。

Exchange 2013，在 Mailbox server 會處理做為處理Exchange 2007和Exchange 2010中的整合通訊伺服器角色相同的程序。信箱伺服器在執行 Microsoft Exchange 整合通訊服務和 UM 工作者處理序。

如果您是安裝在用戶端存取和信箱伺服器部署整合通訊，您不需要建立關聯或新增用戶端存取或 Mailbox server 至 UM 撥號對應表。用戶端存取和信箱伺服器接聽所有來電，然後使用 UM 撥號對應表來尋找使用者。

不過，如果您正在整合通訊與整合 Microsoft Office Communications Server 2007 R2 或 Microsoft Lync Server、 SIP 和來電的 RTP 或 SRTP 媒體通道都是由處理 Lync server 和 Mailbox server。在 Lync 整合式環境中，您不需要 VoIP 閘道、 IP Pbx 或 Sbc。Lync，執行 Microsoft Exchange 整合通訊服務的信箱伺服器外觀就像是Exchange 2010 UM 伺服器。信箱伺服器與用戶端存取伺服器被視為信任的同儕因為這兩個伺服器必須加入至 SIP 撥號對應表。Lync 路由傳送來電使用輸入路由元件，它會使用 SIP 與用戶端存取伺服器進行通訊，然後路由傳送的信箱伺服器的呼叫。

回到頁首

## 伺服器組態設定

Exchange 2013、 在所有的 UM 元件和套用至執行 Unified Messaging server role Exchange 2010在單一電腦的組態設定是仍然可以使用。不過，某些這些元件與組態設定的用戶端存取伺服器上找到且其他人可在信箱伺服器上。在某些情況下，相同的設定值是位於兩者。下列清單顯示的參數和可用的 Client Access server 和 Mailbox server 上的設定。

  - \[-DialPlans \<MultiValuedProperty\>\]

  - \[-MaxCallsAllowed \<Int32\>\]

  - \[-SipTcpListeningPort \<Int32\>\]

  - \[-SipTlsListeningPort \<Int32\>\[

  - \[-Status \<Enabled | Disabled | NoNewCalls\>\]

  - \[-UMStartupMode \<TCP | TLS | Dual\>\]

Mailbox server，您將使用**Set-UMService**、 **Get-UMService**、 **Enable-UMService**及**Disable-UMService**指令程式來檢視或設定 Microsoft Exchange 整合通訊服務的 UM 內容。一組不同的指令程式、 **Set-UMCallRouterSettings**和**Get-UMCallRouterSettings**，可用來檢視或設定用戶端存取伺服器上的 Microsoft Exchange Unified Messaging Call Router 服務屬性。這可確保現有**Get-UMServer**、 Exchange 2007及Exchange 2010**Set-UMServer**、 **Enable-UMServer**，以及**Disable-UMServer**指令程式會在Exchange 2013 Mailbox server 的共存部署工作。這也可確保指令程式會運作時的相同或不同電腦上安裝 Mailbox 和 Client Access server。

回到頁首

## 伺服器作業

用戶端存取伺服器和信箱伺服器會在安裝時自動予以啟用，以便接聽傳入和撥出的語音信箱，並將語音訊息路由至 Exchange 中預定的收件者。

您可以讓信箱伺服器上的 Microsoft Exchange 整合通訊服務或接聽新來電 Client Access server 上的 Microsoft Exchange Unified Messaging Call Router 服務或防止能力。根據預設，Mailbox 或 Client Access server 已啟用狀態安裝後。當您正在設定為接受傳入的語音、 傳真、 自動語音應答以及 Outlook Voice Access 電話 Mailbox 或 Client Access server 時，您會使用**Set-ServerComponentState**指令程式。

在維護模式設定為Exchange 2013 Mailbox 或 Client Access server 可讓您需要停止服務的伺服器。信箱伺服器、 服務 （英文） 表示伺服器將不會主控任何使用中資料庫、 所有傳輸佇列都是空的且伺服器不接受任何來電從用戶端存取伺服器、 VoIP 閘道、 IP Pbx、 已啟用 SIP 的 Pbx 或 Sbc。用戶端存取伺服器、 服務 （英文） 表示伺服器不接受任何來電來自 VoIP 閘道、 IP Pbx、 已啟用 SIP 的 Pbx 或 Sbc。

在Exchange 2007和Exchange 2010，有無法用來控制的整合通訊伺服器的操作狀態的狀態參數。在Exchange 2013、 無狀態參數是提供該**Set-UMService** cmdlet 會在信箱伺服器或用戶端存取伺服器上的**Set-UMCallRouterSettings**指令程式上的目的。

儘管用戶端存取伺服器和信箱伺服器在安裝時都已設為啟用，但直到將 UM 撥號對應表連結到至少一個 UM IP 閘道之前，任一個伺服器都無法正確處理來電並路由至啟用 UM 的使用者。

撥號對應表連結與 UM IP 閘道之後，用戶端存取和信箱伺服器找出所有與 UM 撥號對應表和 VoIP 閘道、 IP Pbx 和 Sbc 相關聯的 UM IP 閘道。若要偵測並識別 UM 撥號對應表或 UM IP 閘道器上的任何設定變更，Client Access server 或信箱伺服器會檢查設定每隔 10 分鐘。

如果 UM IP 閘道器識別之設定的任何變更，Client Access server 或 Mailbox server 反應據以，並且會開始使用或停止使用適當的 VoIP 閘道、 IP PBX 或 SBC。接聽傳入的用戶端存取和信箱伺服器之後使用者的電話與 UM 撥號對應表連結及他們正在正確通訊的 VoIP 閘道、 IP Pbx 和 Sbc 您可以執行一組診斷操作來確認他們正在運作正確且 Exchange 伺服器與 VoIP 閘道、 IP Pbx 或 Sbc 之間的連線運作正常。

回到頁首

