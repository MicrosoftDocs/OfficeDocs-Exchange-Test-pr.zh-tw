---
title: 'Exchange 2013/Exchange 2007 混合部署中的伺服器角色: Exchange 2013 Help'
TOCTitle: Exchange 2013/Exchange 2007 混合部署中的伺服器角色
ms:assetid: d7104efe-6d2a-4260-bc4e-f05da477e30b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn151302(v=EXCHG.150)
ms:contentKeyID: 54651474
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013/Exchange 2007 混合部署中的伺服器角色

本主題正在編輯中。  

_<strong>適用版本：</strong>Exchange Online, Exchange Server, Exchange Server 2013_

_<strong>上次修改主題的時間：</strong>2016-12-09_

當您在 Exchange 2007 組織中設定混合部署時，必須至少安裝一個 Exchange 2013 伺服器，讓它具有現有 Exchange 2007 組織中的 Client Access 和 Mailbox server role。Exchange 2013 Client Access Server 和 Mailbox Server 會協調現有 Exchange 2007 內部部署組織與 Exchange Online 組織之間的通訊。此通訊包括內部部署與 Exchange Online 組織之間的郵件傳輸與訊息傳送功能。

我們強烈建議您在內部部署組織中安裝多個 Exchange 2013 伺服器，以協助增進混合部署功能的可靠性與可用性。

## 混合部署中的伺服器角色

以下是混合式部署中的 Exchange 2013 伺服器角色的快速概觀：

  - **Client Access server role**   Exchange 2013 Client Access server role 會繼續在您組織中提供 Exchange 2007 Client Access Server 通常會提供的許多相同功能，並附加一些支援混合部署及與 Exchange 2007 共存所需的功能。Client Access Server 還會處理從 Exchange Online 組織傳送至內部部署組織的安全郵件，並且處理傳輸規則、日誌原則，以及對混合式部署中的 Mailbox Server 傳遞的郵件。Client Access Server 上預設會設定專用的接收連接器，以支援安全的混合郵件傳輸。所有的用戶端連線 (包含 Outlook 用戶端存取)、Outlook Web App 和 Outlook 無所不在，現在都透過用戶端存取伺服器角色進行。內部部署與 Exchange Online 組織之間的組織關聯性功能 (例如，空閒/忙碌共用)，也是由 Client Access server role 進行處理。
    
    若要深入了解，請參閱 [Client Access server](https://technet.microsoft.com/zh-tw/library/dd298114\(v=exchg.150\))。

  - **Mailbox server role**   Exchange 2013 Mailbox server role 會處理從內部部署組織傳送至 Exchange Online 組織的安全郵件。它也可以裝載內部部署收件者信箱，並且藉由 Proxy 透過內部部署 Client Access Server 來與 Exchange Online 組織進行通訊，只是這些用法並不常見。根據預設，Mailbox server role 上會設定專用的傳送連接器，以支援安全的混合郵件傳輸。
    
    若要深入了解，請參閱 [信箱伺服器](https://technet.microsoft.com/zh-tw/library/jj150491\(v=exchg.150\))。

根據您所希望的混合部署組態而定，Exchange 2013 伺服器上需要安裝下列兩種伺服器角色的其中一種，或兩種都安裝：

  - **單一 Exchange 伺服器**   若您選擇在內部部署組織中安裝單一 Exchange 伺服器，則需要在單一伺服器上同時安裝 Client Access server role 和 Mailbox server role。

  - **多個 Exchange 伺服器**   若您選擇在內部部署組織中安裝一個以上的 Exchange 伺服器，可在內部部署伺服器中多個不同伺服器上安裝伺服器角色。例如，您可以安裝一部已安裝 Mailbox role 和 Client Access role 的 Exchange 2013 伺服器，並且安裝另一部只安裝 Client Access server role 的 Exchange 伺服器。但是，最佳作法與建議的伺服器組態，是在內部部署組織中部署的「每一部」Exchange 2013 伺服器上，同時安裝 Client Access server role 和 Mailbox server role。

可於 [瞭解容量規劃中的多重伺服器角色組態](http://go.microsoft.com/fwlink/?linkid=266576)，瞭解更多關於 Exchange 容量規劃的資訊。

## 混合部署中的 Exchange 伺服器功能

Exchange 伺服器可在混合部署中，為您的內部部署組織提供幾項重要功能：

  - **同盟**   Exchange 2013 伺服器可讓您使用 Microsoft Federation Gateway，為您的內部部署組織建立同盟信任。Microsoft Federation Gateway 是 Microsoft 所提供的免費雲端式服務，做為內部部署組織與 Office 365 租用戶組織之間的信任代理。若要在內部部署與 Exchange Online 組織之間的建立組織關聯性，同盟是必要條件。
    
    若要深入了解，請參閱 [同盟](https://technet.microsoft.com/zh-tw/library/dd335047\(v=exchg.150\))。

  - **組織關係**   具有 Client Access server role 的 Exchange 2013 伺服器，可協助在內部部署與 Exchange Online 組織之間建立組織關係。混合式部署中的其他許多服務都需要組織關聯性，包括內部部署與 Exchange Online 組織之間的行事曆空閒/忙碌資訊共用、郵件追蹤以及信箱移動。
    
    若要深入了解，請參閱 [共用](https://technet.microsoft.com/zh-tw/library/dd638083\(v=exchg.150\))。

  - **郵件傳輸**   具有 Client Access server role 和 Mailbox server role 的 Exchange 2013 伺服器，會負責混合部署中的郵件傳輸。透過使用傳送及接收連接器，其會做為內送外部郵件的連線端點，而且還為網際網路和 Exchange Online 組織提供外寄郵件傳遞。
    
    若要深入了解，請參閱 [Exchange 2013/Exchange 2007 混合式部署中的傳輸選項](transport-options-in-exchange-2013-exchange-2007-hybrid-deployments-exchange-2013-help.md)。

  - **郵件傳輸安全性**   具有 Client Access server role 和 Mailbox server role 的 Exchange 2013 伺服器會使用 Exchange 2013 中的 \[網域安全性\] 功能，協助確保內部部署與 Exchange Online 組織之間的郵件通訊安全。使用相互傳輸層安全性驗證及郵件通訊加密，可以提高安全性。
    
    若要深入了解，請參閱[了解網域安全性](http://go.microsoft.com/fwlink/p/?linkid=266581)。

  - **Outlook Web App**   具有 Client Access server role 的 Exchange 2013 伺服器支援為內部部署信箱和 Exchange Online 信箱的外部連線，設定單一 URL 端點。針對內部部署信箱，Client Access Server 的設定是為 Outlook Web App 要求提供服務。針對 Exchange Online 組織信箱，會將用戶端存取伺服器設定為自動顯示連結，且該連結會連至 Exchange Online 組織上的Outlook Web App 端點。
    
    若要深入了解，請參閱 [Outlook Web App](https://technet.microsoft.com/zh-tw/library/jj657718\(v=exchg.150\))。

## Exchange 伺服器拓撲

若您選擇新增額外的 Exchange 2013 伺服器來支援混合部署，則將 Exchange 伺服器部署至現有 Exchange 2007 組織的方式，會與部署任何其他 Exchange Server 的方式十分類似。為混合部署設定現有的內部部署 Exchange 2007 組織，並不需要任何特殊的 Exchange 伺服器拓撲。不過，您必須在 Exchange 2007 伺服器上安裝 Exchange 2007 Service Pack 3 (SP3) 更新彙總套件 10，並且也安裝 Exchange 2013 累計更新 1 (CU1) 或更新版本，才能啟用與 Office 365 的相容性和完整混合功能。

下表簡要說明設定混合部署後的服務變更。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>服務</th>
<th>混合部署前</th>
<th>混合部署後</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>郵件傳輸 (內送和外寄)</p></td>
<td><p>Exchange 2007 Client Access Server</p></td>
<td><p>Office 365 隨附的 Exchange 2013 Client Access Server 或 Exchange Online Protection (EOP)</p></td>
<td><p>網域的 MX (郵件交換程式) 記錄會保持不變或是更新為指向 EOP。</p></td>
</tr>
<tr class="even">
<td><p>Outlook Web App 公用 URL</p></td>
<td><p>Exchange 2007 Client Access Server</p></td>
<td><p>Exchange 2013 Client Access Server</p></td>
<td><p>Exchange 2013 Client Access Server 會代理 Outlook Web App 對 Exchange 2007 Client Access Server 提出的內部部署信箱存取要求。Outlook Web App 如果要求存取位在 Exchange Online 上的信箱，就會得到 Exchange Online Outlook Web App URL 的連結。</p></td>
</tr>
</tbody>
</table>


## Exchange 伺服器軟體

Exchange 2013 CU1 或更新版本會使用 \[混合組態精靈\] 來啟用混合部署功能。您可以在安裝額外的 Exchange 2013 伺服器時使用任何 Exchange 2013 CU1 或更新版本媒體。

如需有關如何下載最新版 Exchange 2013 的相關資訊，請參閱＜[更新 Exchange 2013](http://technet.microsoft.com/library/jj907309)＞。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ906432.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>設定具有 Exchange 2013 或 2010 和 Office 365 的混合部署時，需要授權混合伺服器。您可以利用 <a href="https://aka.ms/hybridkey">Hybrid Edition 產品金鑰工具</a>，取得用於設定混合部署的免費 Exchange Server 產品金鑰。</td>
</tr>
</tbody>
</table>

