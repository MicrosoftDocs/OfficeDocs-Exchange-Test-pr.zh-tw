---
title: 'Exchange 2013/Exchange 2010 混合式部署中的傳輸選項: Exchange 2013 Help'
TOCTitle: Exchange 2013/Exchange 2010 混合式部署中的傳輸選項
ms:assetid: 57f93b81-d153-4f0d-81f6-085130319803
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn393960(v=EXCHG.150)
ms:contentKeyID: 59634075
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013/Exchange 2010 混合式部署中的傳輸選項

本主題正在編輯中。  

_<strong>適用版本：</strong>Exchange Online, Exchange Server, Exchange Server 2013_

_<strong>上次修改主題的時間：</strong>2016-12-09_

在混合式部署中，您可以將信箱放在內部部署 Exchange 組織中，也可放在 Exchange Online 組織中。兩個不同的組織之所以能夠對使用者以及在其之間交換的郵件顯示為一個合併組織，其中一個重要元件就是混合式傳輸。在採用混合傳輸的情況下，任一組織中的收件者之間傳送的郵件都會使用傳輸層安全性 (TLS) 進行驗證、加密及傳輸，並對傳輸規則、日誌及反垃圾郵件原則等 Exchange 元件顯示為「內部�?」。混合傳輸是由混合組態精靈在 Exchange 2013 中自動設定。

為使混合傳輸組態能搭配混合組態精靈使用，接受 Microsoft Exchange Online Protection (EOP) 連線並處理 Exchange Online 組織之傳輸作業的內部部署 SMTP 端點，必須為 Exchange 2013 Client Access Server、Exchange 2013 Edge Transport Server 或 Exchange Server 2010 SP3 Edge Transport Server。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ906432.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>內部部署 Exchange 2013 Client Access Server 或 Exchange 2013/Exchange 2010 SP3 Edge Transport Server 與 EOP 之間可能沒有其他 SMTP 主機或服務。新增至可啟用混合傳輸功能的郵件資訊，會在通過非 Exchange 2013 伺服器、Exchange 2010 SP3 預備伺服器或 SMTP 主機時移除。如果您的組織部署了 Exchange 2010 SP2 Edge Transport Server，而您想將其用於混合傳輸，這些伺服器必須升級至 Exchange 2010 SP3。</td>
</tr>
</tbody>
</table>


從外部網際網路寄件者傳送到兩個組織收件者的內送郵件，會遵循通用內送路由。從組織傳送給外部網際網路收件者的外寄郵件，可遵循通用外寄路由，或可經由獨立路由傳送。

當您規劃及設定混合式部署時，需要選擇如何路由傳送內送和外寄郵件。內部部署和 Exchange Online 組織收件者傳送的內送與外寄郵件所使用的路由，取決於下列條件：

  - 您想要透過 Microsoft Office 365 和 EOP 或您的內部部署組織，路由傳送您內部部署與 Exchange Online 信箱的內送網際網路郵件嗎？
    
    您可以選擇透過內部部署組織或透過 EOP 和 Exchange Online 組織，為這兩個組織路由傳送內送網際網路郵件。這兩個組織的內送郵件採用的路由，取決於您是否啟用混合式部署中的集中式郵件傳輸。

  - 您想透過內部部署組織 (集中式郵件傳輸) 路由傳送 Exchange Online 組織的外寄郵件至外部收件者，還是要將郵件直接路由傳送到網際網路？
    
    利用所謂的集中式郵件傳輸，您可以先透過內部部署組織路由傳送 Exchange Online 組織中信箱的所有郵件，然後再傳遞到網際網路。這個方法用於規範案例中，因為所有傳送到及傳送自網際網路的郵件，都必須由內部部署伺服器處理。或者，您可以設定 Exchange Online 將外部收件者的郵件直接傳遞至網際網路。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ150559.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>對於有特定規範相關傳輸需求的組織，才建立使用集中式郵件傳輸。對於一般 Exchange 組織，建議不啟用集中式郵件傳輸。</td>
    </tr>
    </tbody>
    </table>


  - 您想要在內部部署組織中部署 Edge Transport Server 嗎？
    
    如果您不想讓加入網域的內部 Exchange 2013 伺服器直接暴露於網際網路，您可以在周邊網路中部署 Exchange 2013 Edge Transport Server 或 Exchange 2010 SP3 Edge Transport Server。如需新增 Edge Transport Server 至混合式部署的詳細資訊，請參閱[Exchange 2013/Exchange 2010 混合式部署中的 Edge Transport Server](edge-transport-servers-in-exchange-2013-exchange-2010-hybrid-deployments-exchange-2013-help.md)。

不論您如何將郵件路由傳送到網際網路，或從網際網路路由傳送郵件，所有在內部部署與 Exchange Online 組織之間傳送的郵件都會使用安全傳輸進行傳送。如需詳細資訊，請參閱本主題稍後的[Trusted communication](transport-options-in-exchange-hybrid-deployments-exchange-2013-help.md)。

若要深入了解這些選項如何影響組織中郵件遞送的方式，請參閱[Exchange 2013/Exchange 2010 混合式部署中的傳輸路由](transport-routing-in-exchange-2013-exchange-2010-hybrid-deployments-exchange-2013-help.md)。

## 混合式部署中的 Exchange Online Protection

EOP 是 Microsoft 提供的線上服務，許多公司皆利用它保護內部部署組織免於病毒、垃圾郵件、網路釣魚詐騙及原則違規情形。在 Office 365 中，也使用 EOP 保護 Exchange Online 組織不受相同威脅的侵害。註冊 Office 365 時，會自動建立一個連結至您 Exchange Online 組織的 EOP 公司。

EOP 公司包含數個可為您 Exchange Online 組織設定的郵件傳輸設定。您可以指定哪些 SMTP 網域必須來自特定 IP 位址、要求 TLS 與安全通訊端層 (SSL) 憑證、略過規範原則等等。EOP 是進入 Exchange Online 組織的前哨。不論郵件來源為何，所有郵件都必須通過 EOP 才能傳送到您 Exchange Online 組織中的信箱。而且，所有從您 Exchange Online 組織送出的郵件，都必須通過 EOP 才能傳送到網際網路。

使用混合組態精靈設定混合式部署時，所有傳輸設定都會自動在您的內部部署組織，以及在 Exchange Online 組織內含的 EOP 公司中設定。混合組態精靈會設定這個 EOP 公司中的所有內送和外寄連接器以及其他設定，以保護在內部部署與 Exchange Online 組織之間傳送的郵件安全，並將郵件路由傳送到正確的目的地。如果您想要為 Exchange Online 組織設定自訂傳輸設定，則也會在這個 EOP 公司中設定這些設定。

## 信任的通訊

為了協助保護在內部部署與 Exchange Online 組織中的收件者，並且協助確保組織之間傳送的郵件不會遭受攔截與讀取，內部部署組織與 EOP 之間的傳輸會設定為使用強制 TLS。TLS 傳輸會使用由信任的協力廠商憑證授權單位 (CA) 所提供的安全通訊端層 (SSL) 憑證。EOP 和 Exchange Online 組織之間的郵件也會使用 TLS。

使用強制執行的 TLS 傳輸時，傳送和接收伺服器會檢查另一部伺服器上設定的憑證。憑證上所設定的主體名稱或是其中一個主體替代名稱 (SAN)，必須符合系統管理員在另一部伺服器上明確指定的 FQDN。例如，若 EOP 設定為接受並保護傳送自 mail.contoso.com FQDN 的郵件，則負責傳送的內部部署 Client Access Server 或 Edge Transport Server，必須有主旨名稱或 SAN 內包含 mail.contoso.com 的 SSL 憑證。如果未符合此需求，則 EOP 會拒絕連線。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ150559.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用的 FQDN 不需要符合收件者的電子郵件網域名稱。唯一的需求是憑證主旨名稱或 SAN 中的 FQDN 必須符合負責接收或傳送的伺服器所設定要接受的 FQDN。</td>
</tr>
</tbody>
</table>


除了使用 TLS 以外，組織之間的郵件也被視為「內部�?」郵件。此方法允許郵件略過反垃圾郵件設定和其他服務。

若要深入了解 SSL 憑證和網域安全性，請參閱[混合部署的憑證需求](certificate-requirements-for-hybrid-deployments-exchange-2013-help.md)和[了解 TLS 憑證](http://go.microsoft.com/fwlink/p/?linkid=187237)。

