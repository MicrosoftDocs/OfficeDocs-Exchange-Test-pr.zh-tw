---
title: '混合部署的憑證需求: Exchange 2013 Help'
TOCTitle: 混合部署的憑證需求
ms:assetid: 48d532cc-29f9-4009-9d2d-f19a9c13c320
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh563848(v=EXCHG.150)
ms:contentKeyID: 50474701
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 混合部署的憑證需求

 

_<strong>適用版本：</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>上次修改主題的時間：</strong>2016-12-09_

在混合式部署中，數位憑證是保護內部部署 Exchange 組織與 Office 365 之間通訊安全相當重要的一環。憑證可讓 Exchange 組織信任彼此的識別。憑證也有助於確認每一個 Exchange 組織與正確的來源進行通訊。

在混合式部署中，有許多服務會使用憑證：

  - **Azure Active Directory Connect (Azure AD Connect) 搭配 Active Directory Federation Services (AD FS)**   如果您選擇在混合式部署中部署 Azure AD Connect 搭配 AD FS，則使用受信任的協力廠商憑證授權單位 (CA) 所發行的憑證，在 Web 用戶端與同盟伺服器 Proxy 之間建立信任，以簽署安全性權杖及解密安全性權杖。
    
    若要深入了解，請參閱[憑證](http://go.microsoft.com/fwlink/p/?linkid=205993)。

  - **Exchange 同盟**   使用自我簽署憑證可在內部部署 Exchange 伺服器與 Azure Active Directory 驗證系統之間建立安全連線。
    
    若要深入了解，請參閱 [共用](https://technet.microsoft.com/zh-tw/library/dd638083\(v=exchg.150\))。

  - **Exchange 服務**   使用受信任的協力廠商 CA 所發行的憑證，協助確保在 Exchange 伺服器與用戶端之間進行安全的安全通訊端層 (SSL) 通訊。使用憑證的服務包括 網頁型 Outlook、Exchange ActiveSync、Outlook Anywhere 及郵件傳輸。

  - **現有 Exchange 伺服器**   您現有的 Exchange 伺服器可能會使用憑證，協助確保 網頁型 Outlook 通訊、郵件傳輸等等的安全。視您在 Exchange 伺服器上使用憑證的方式而定，可能會使用自我簽署憑證或受信任的協力廠商 CA 所發行的憑證。

## 混合式部署的憑證需求

設定混合式部署時，您必須針對您向信任的協力廠商 CA 所購買的憑證進行使用和設定。用於混合安全郵件傳輸的憑證必須安裝在所有內部部署信箱 (Exchange 2016 和更新版本) 以及信箱和用戶端存取 (Exchange 2013 和更舊版本) 伺服器上。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ906432.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>對於將 Exchange 伺服器部署在多個 Active Directory 樹系中的組織，當您在該組織中設定混合式部署時，必須在<em>每個</em> Active Directory 樹系中使用不同的協力廠商 CA 憑證。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/JJ150559.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果內部部署組織中已部署 Exchange Edge Transport Server，此憑證也必須安裝在所有 Edge Transport Server 上。每一部傳輸伺服器都必須使用共用相同發行 CA 與相同主旨的憑證，混合安全郵件才能正確運作。</td>
</tr>
</tbody>
</table>


像是 AD FS、Exchange 同盟、服務和 Exchange 等多項服務都需要憑證。視您的組織而定，您可以決定執行下列其中一項操作：

  - 使用由所有服務跨多部伺服器使用的協力廠商憑證。

  - 將協力廠商憑證用於提供服務的每部伺服器。

無論您選擇將相同的憑證用於所有服務，或是每項服務各有專用的憑證，都取決於您的組織以及您實作的服務。以下是每個選項要考量的事項：

  - **跨多部伺服器的協力廠商憑證**   由許多服務跨多部伺服器使用的協力廠商憑證在取得時可能較便宜，但是會使更新及更換作業變得複雜。發生複雜情況是因為當需要更換憑證時，必須為每部安裝憑證的伺服器進行更換。

  - **每部伺服器專用的協力廠商憑證**   針對每部主控服務的伺服器使用專用憑證，可讓您特別為該伺服器上的服務設定憑證。如果需要更換或更新憑證，只需要在安裝服務的伺服器上進行更換。其他伺服器不會受到影響。

建議您將專用的協力廠商憑證用於任何選用的 AD FS 伺服器，另一張憑證用於混合式部署的 Exchange 服務，並且視需要在 Exchange 伺服器上再將一張憑證用於其他需要的服務或功能。根據預設，設定作為混合式部署中同盟資訊共用一部分的內部部署同盟信任，會使用自我簽署憑證。除非您有特殊需求，否則不需要使用在其中將同盟信任設定作為混合式部署一部分的協力廠商憑證。

安裝在單一伺服器上的服務可能會要求您為伺服器設定多個完整網域名稱 (FQDN)。您應購買允許使用所需最大 FQDN 數目的憑證。憑證是由主旨名稱 (亦稱為主要名稱) 以及一個或多個主體別名 (SAN) 所組成。主旨名稱是作為憑證簽發目標的 FQDN，且應該使用內部部署與 Exchange Online 組織之間共用的主要 SMTP 網域。SAN 是除主旨名稱外可新增至憑證的其他 FQDN。如果您需要可支援五個 FQDN 的憑證，請購買允許將五個網域新增至憑證的憑證：一個主旨名稱和四個 SAN。

下表說明應包含在設定用於混合式部署中憑證上的建議 FQDN 數目下限。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>服務</th>
<th>建議的 FQDN</th>
<th>欄位</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>主要共用 SMTP 網域</p></td>
<td><p>contoso.com</p></td>
<td><p>主體名稱</p></td>
</tr>
<tr class="even">
<td><p>自動探索</p></td>
<td><p>符合 Exchange 2013 Client Access Server 的外部自動探索 FQDN 的標籤，例如 autodiscover.contoso.com</p></td>
<td><p>主體替代名稱</p></td>
</tr>
<tr class="odd">
<td><p>傳輸</p></td>
<td><p>符合 Edge Transport Server 的外部 FQDN 的標籤，例如 edge.contoso.com</p></td>
<td><p>主體替代名稱</p></td>
</tr>
</tbody>
</table>

