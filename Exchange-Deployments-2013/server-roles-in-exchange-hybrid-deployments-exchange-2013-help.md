---
title: 'Exchange 混合式部署中的伺服器角色: Exchange 2013 Help'
TOCTitle: Exchange 混合式部署中的伺服器角色
ms:assetid: 7a7eaf17-d2b0-4d62-90a2-45a0d2faca54
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ659051(v=EXCHG.150)
ms:contentKeyID: 50474705
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 混合式部署中的伺服器角色

 

_<strong>適用版本：</strong>Exchange Server 2013, Exchange Server 2016_

_<strong>上次修改主題的時間：</strong>2016-12-09_

您可以根據 Exchange 2013 和 Exchange 2016 設定混合式部署。需要設定哪些角色才能支援混合式部署，視您正在使用的 Exchange 而定。

## Exchange 2016 混合部署

當設定 Exchange 2016 組織中的混合部署時，您不需要在現有的 Exchange 組織中安裝任何額外的 Exchange 伺服器。您的信箱伺服器會協調現有 Exchange 2016 組織與 Exchange Online 組織之間的通訊。此通訊包括內部部署與 Exchange Online 組織之間的郵件傳輸與訊息傳送功能。我們強烈建議您在內部部署組織中安裝多個 Exchange 伺服器，以協助增進混合部署功能的可靠性與可用性。

Exchange 2016 僅有一個必要的伺服器角色，亦即信箱角色。除了裝載內部部署收件者信箱，信箱角色也會執行所有支援 Exchange Online 混合式部署所需的功能。這包含處理在內部部署和 Exchange Online 組織之間的所有安全郵件，以及處理混合部署中對使用者信箱的傳輸規則、日誌原則和郵件傳遞。所有用戶端連線和組織關係功能，例如空閒/忙碌共用，皆由信箱伺服器所處理。

若要深入了解 Exchange 2016 容量規劃，請參閱[決定 Exchange 2016 部署規模](http://go.microsoft.com/fwlink/p/?linkid=301990)。

## Exchange 2013 混合部署

當設定 Exchange 2013 組織中的混合部署時，您不需要在現有的 Exchange 組織中安裝任何額外的 Exchange 伺服器。您的 Client Access Server 和信箱伺服器會協調現有 Exchange 2013 組織與 Exchange Online 組織之間的通訊。此通訊包括內部部署與 Exchange Online 組織之間的郵件傳輸與訊息傳送功能。我們強烈建議您在內部部署組織中安裝多個 Exchange 伺服器，以協助增進混合部署功能的可靠性與可用性。

以下是混合式部署中的 Exchange 2013 伺服器角色的快速概觀：

  - **用戶端存取伺服器角色**   對於 Exchange 2013 組織上其他用戶端存取伺服器一般提供的功能，此用戶端存取伺服器角色可持續提供基本上相同的功能，並附加支援混合部署所需要的一些新增功能。Client Access Server 還會處理在內部部署和 Exchange Online 組織之間傳送的所有安全郵件，以及處理混合部署中對使用者信箱的傳輸規則、日誌原則和郵件傳遞。根據預設，Client Access Server 上設定了專用的接收連接器，可支援安全的混合郵件傳輸。所有的用戶端連線 (包含 Outlook 用戶端存取)、Outlook Web App 和 Outlook 無所不在，現在都透過用戶端存取伺服器角色進行。內部部署與 Exchange Online 組織之間的組織關聯性功能 (例如，空閒/忙碌共用)，也是由 Client Access server role 進行處理。
    
    若要深入了解，請參閱 [Client Access server](https://technet.microsoft.com/zh-tw/library/dd298114\(v=exchg.150\))。

  - **Mailbox server role**   Mailbox server role 主控內部部署收件者信箱，並且藉由 Proxy 透過內部部署 Client Access Server 與 Exchange Online 組織進行通訊。根據預設，Mailbox server role 上會設定專用的傳送連接器，以支援安全的混合郵件傳輸。
    
    若要深入了解，請參閱 [信箱伺服器](https://technet.microsoft.com/zh-tw/library/jj150491\(v=exchg.150\))。

根據您所希望的混合部署組態而定，Exchange 2013 伺服器上需要安裝下列兩種伺服器角色的其中一種，或兩種都安裝：

  - **單一 Exchange 伺服器**   若您選擇在內部部署組織中安裝單一 Exchange 伺服器，則需要在單一伺服器上同時安裝 Client Access server role 和 Mailbox server role。

  - **多個 Exchange 伺服器**   若您選擇在內部部署組織中安裝一個以上的 Exchange 伺服器，可在內部部署伺服器中多個不同伺服器上安裝伺服器角色。例如，您可以安裝一部已安裝 Mailbox role 和 Client Access role 的 Exchange 伺服器，並且安裝另一部只安裝 Client Access server role 的 Exchange 伺服器。但是，最佳作法與建議的伺服器組態，是在內部部署組織中部署的*每一部*伺服器上同時安裝 Client Access server role 和 Mailbox server role。

可於 [瞭解容量規劃中的多重伺服器角色組態](http://go.microsoft.com/fwlink/?linkid=266576)，瞭解更多關於 Exchange 2013 容量規劃的資訊。

## 混合部署中的 Exchange 伺服器功能

Exchange 伺服器可在混合部署中，為您的內部部署組織提供幾項重要功能：

  - **同盟**Exchange 伺服器可讓您使用 Microsoft 同盟閘道，為您的內部部署組織建立同盟信任。Microsoft Federation Gateway 是 Microsoft 所提供的免費雲端式服務，做為內部部署組織與 Office 365 組織之間的信任代理。若要在內部部署與 Exchange Online 組織之間的建立組織關聯性，同盟是必要條件。
    
    若要深入了解，請參閱 [同盟](https://technet.microsoft.com/zh-tw/library/dd335047\(v=exchg.150\))。

  - **組織關係**具有用戶端存取角色的 Exchange 2013 伺服器以及具有信箱角色的 Exchange 2016 伺服器，可協助在內部部署與 Exchange Online 組織之間建立組織關係。混合式部署中的其他許多服務都需要組織關聯性，包括內部部署與 Exchange Online 組織之間的行事曆空閒/忙碌資訊共用、郵件追蹤以及信箱移動。
    
    若要深入了解，請參閱 [共用](https://technet.microsoft.com/zh-tw/library/dd638083\(v=exchg.150\))。

  - **郵件傳輸**   具有 Client Access server role 和 Mailbox server role 的 Exchange 伺服器負責混合部署中的郵件傳輸。透過使用傳送及接收連接器，其會做為內送外部郵件的連線端點，而且還為網際網路和 Exchange Online 組織提供外寄郵件傳遞。
    
    若要深入了解，請參閱 [Exchange 混合式部署中的傳輸選項](transport-options-in-exchange-hybrid-deployments-exchange-2013-help.md)。

  - **郵件傳輸安全性**   具有 Client Access server role 和 Mailbox server role 的 Exchange 伺服器會使用 Exchange 中的 \[網域安全性\] 功能，協助確保內部部署與 Exchange Online 組織之間的郵件通訊安全。使用相互傳輸層安全性驗證及郵件通訊加密，可以提高安全性。
    
    若要深入了解，請參閱[了解網域安全性](http://go.microsoft.com/fwlink/p/?linkid=266581)。

  - **Outlook 網頁版 (在 Exchange 2013 中也稱為 Outlook Web App)**   具有用戶端存取角色的 Exchange 2013 伺服器以及具有信箱角色的 Exchange 2016 伺服器，支援為內部部署信箱和 Exchange Online 信箱的外部連線，設定單一 URL 端點。針對內部部署信箱，Exchange 伺服器的設定是為 網頁型 Outlook 要求提供服務。針對 Exchange Online 組織信箱，會將 Exchange 伺服器設定為自動顯示連結，且該連結會連至 Exchange Online 組織上的 網頁型 Outlook 端點。
    
    若要深入了解，請參閱 [Outlook Web App](https://technet.microsoft.com/zh-tw/library/jj657718\(v=exchg.150\))。

