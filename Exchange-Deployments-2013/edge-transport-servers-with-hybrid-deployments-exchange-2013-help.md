---
title: 'Edge Transport server 與混合式部署: Exchange 2013 Help'
TOCTitle: Edge Transport server 與混合式部署
ms:assetid: 166b1490-5c56-40df-a17b-e8bb36224fd9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh134662(v=EXCHG.150)
ms:contentKeyID: 50474698
ms.date: 04/26/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Edge Transport server 與混合式部署

 

_<strong>適用版本：</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>上次修改主題的時間：</strong>2018-04-16_

Edge Transport server role 是選擇性角色，通常會部署在 Exchange 組織周邊網路中的電腦上，且會設計為將組織的攻擊面降到最低。Edge Transport server role 會處理所有網際網路對向郵件流程，這為您組織內部的內部部署 Exchange 伺服器提供 SMTP 轉送和智慧主機服務。

## 以 Exchange 為基礎的混合式部署組織中的 Edge Transport server

想要使用 Edge Transport server 的 Exchange 2016 組織可以選擇部署執行最新版 Exchange 2016、Exchange 2013 或 Exchange 2010 的 Edge Transport server。如果您不想要直接對網際網路公開內部 Exchange 伺服器，請使用 Edge Transport server。在混合式部署中部署 Edge Transport server 時，Exchange Online 會透過 Exchange Online Protection 服務連線到您的 Edge Transport server 以傳遞郵件。然後 Edge Transport server 會將傳遞郵件到收件者信箱所在的內部部署 Exchange 信箱伺服器。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ906432.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>請不要將任何伺服器、服務或裝置放在處理或修改 SMTP 流量的內部部署 Exchange 伺服器與 Office 365 之間。保護內部部署 Exchange 組織和 Office 365 之間郵件流程的安全，取決於組織之間傳送的郵件中所包含的資訊。支援允許 TCP 通訊埠 25 上通過未經修改之 SMTP 流量的防火牆。如果伺服器、服務或裝置會處理內部部署 Exchange 組織和 Office 365 之間傳送的郵件，就會移除這項資訊。如果發生這種情況，郵件將不會視為組織內部郵件，而會受制於反垃圾郵件篩選、傳輸和日誌規則及其他可能不適用的原則。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/JJ906432.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您在其他的位置擁有其他 Exchange Edge Transport server，但不會用於處理混合傳輸，則不需要將它們升級以支援混合式部署。不過，如果您希望在未來將 EOP 連接到其他的 Edge Transport server 以進行混合傳輸，則它們必須執行最新版的 Exchange 2016 (和更新版本)、Exchange 2010 或 Exchange 2013。</td>
</tr>
</tbody>
</table>


## 將 Edge Transport Server 新增至混合式部署

設定混合式部署時，在內部部署組織中部署 Edge Transport Server 是選擇性的。設定混合式部署時，混合式組態精靈可讓您選取一部或多部內部部署 Exchange 伺服器，或是選取一部或多部內部部署 Edge Transport Server 來處理和 Exchange Online 組織之間的混合郵件傳輸。

當您將 Edge Transport server 新增至混合式部署時，它會代表內部 Exchange 伺服器與 EOP 進行通訊。Edge Transport server 會當做內部 Exchange 伺服器與 EOP 之間的轉送伺服器，用於內部部署組織到 Exchange Online 組織的外寄郵件傳送。Edge Transport server 也會當做內部 Exchange 伺服器之間的轉送伺服器，用於 Exchange Online 組織到內部部署組織的內送郵件傳送。所有先前由內部 Exchange 伺服器所處理的連線安全性，現在則由 Edge Transport server 處理。收件者查閱、規範原則及其他郵件檢查，會繼續在內部 Exchange 伺服器上進行。

如果您將 Edge Transport server 新增至您的混合式部署，您不需要透過它路由傳送在內部部署使用者和網際網路收件者之間傳送的郵件。只有在內部部署和 Exchange Online 組織之間傳送的郵件才會透過 Edge Transport server 路由傳送。

## 無 Edge Transport Server 的郵件流程

下列程序與圖表描述在未部署 Edge Transport Server 的情況下，內部部署組織與 Exchange Online 之間郵件所採取的路徑：

1.  從內部部署組織傳送給 Exchange Online 組織收件者的外寄郵件，會從內部 Exchange 伺服器上的信箱傳送。

2.  Exchange 伺服器會將郵件直接傳送到 EOP。

3.  EOP 會將郵件傳遞到 Exchange Online 組織。

從 Exchange Online 組織傳送到內部部署組織收件者的郵件，則會遵循反向路由。

**未部署 Edge Transport Server 之混合式部署中的郵件流程**

![沒有 Edge Transport Server 的混合式郵件流程](images/Hh134662.a95b4d1e-fd4a-4952-b891-22f84c9e71a3(EXCHG.150).png "沒有 Edge Transport Server 的混合式郵件流程")

## 有 Edge Transport Server 的郵件流程

下列程序描述在部署 Edge Transport server 的情況下，內部部署組織與 Exchange Online 之間郵件所採取的路徑。從內部部署組織傳送到 Exchange Online 組織收件者的郵件是從內部 Exchange 伺服器傳送：

1.  從內部部署組織傳送給 Exchange Online 組織收件者的郵件，會從內部 Exchange 伺服器上的信箱傳送。

2.  Exchange 伺服器將郵件傳送到執行支援版本和 Exchange 版本的 Edge Transport server。

3.  Edge Transport server 會將郵件傳送到 EOP。

4.  EOP 會將郵件傳遞到 Exchange Online 組織。

從 Exchange Online 組織傳送到內部部署組織收件者的郵件，則會遵循反向路由。

**部署 Edge Transport Server 之混合部署中的郵件流程**

![有 Edge Transport Server 的混合式郵件流程](images/Hh134662.821fe099-56f5-4501-8e1a-e184ba07a653(EXCHG.150).png "有 Edge Transport Server 的混合式郵件流程")

