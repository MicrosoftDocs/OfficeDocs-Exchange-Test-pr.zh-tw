---
title: 'Exchange 2013/Exchange 2010 混合式部署中的 Edge Transport Server: Exchange 2013 Help'
TOCTitle: Exchange 2013/Exchange 2010 混合式部署中的 Edge Transport Server
ms:assetid: 924f895e-5987-48d0-b113-9d26dcbcdae0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn393965(v=EXCHG.150)
ms:contentKeyID: 59634081
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013/Exchange 2010 混合式部署中的 Edge Transport Server

本主題正在編輯中。  

_<strong>適用版本：</strong>Exchange Online, Exchange Server, Exchange Server 2013_

_<strong>上次修改主題的時間：</strong>2016-12-09_

Microsoft Exchange 中的 Edge Transport Server 會部署在組織的內部部署周邊網路。這些非加入網域的電腦會處理網際網路對向郵件流程，並充當您內部網路中 Exchange 伺服器的 SMTP 轉送與智慧主機。

Exchange 2013 想要使用 Edge Transport server 的組織可以選擇部署 Exchange Server 2013 Edge Transport server 或執行 Service Pack 3 (SP3) for Exchange 2010 的 Exchange 2010 Edge Transport server。如果您不想要直接對網際網路公開內部 Exchange 2013 用戶端存取或信箱伺服器，請使用 Edge Transport server。

若要深入了解 Exchange 2013 Edge Transport server role，請參閱 [Edge Transport Server](https://technet.microsoft.com/zh-tw/library/bb124701\(v=exchg.150\))。

若要深入了解 Exchange 2010 Edge Transport server role，請參閱 [Edge Transport Server Role 概觀](http://go.microsoft.com/fwlink/p/?linkid=183473)。

## Exchange 2013 型混合式部署組織中的 Edge Transport server

在混合式部署中的內部部署和 Exchange Online 組織之間路由傳送的郵件，需要使用 Microsoft Exchange Online Protection (EOP) 服務代表 Exchange Online，直接連接至執行 Exchange 2013 或 Exchange 2010 SP3 的 Edge Transport Server。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ906432.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您在其他的位置擁有其他 Exchange 2010 Edge Transport server，但不會用於處理混合傳輸，則不需要將它們升級到 Exchange 2010 SP3。不過，如果您希望在未來將 EOP 連接到其他的 Edge Transport server 以進行混合傳輸，則必須將它們升級到 Exchange 2010 SP3 或升級到 Exchange 2013 Edge Transport server。</td>
</tr>
</tbody>
</table>


## 將 Edge Transport Server 新增至混合式部署

設定混合式部署時，在內部部署組織中部署 Edge Transport Server 是選擇性的。設定混合式部署時，混合組態精靈可讓您選取一部或多部 Client Access Server 和信箱伺服器，以進行混合郵件傳輸，或是選取一部或多部內部部署 Edge Transport Server 透過 Exchange Online 組織處理混合郵件傳輸。

當您將 Edge Transport Server 新增至混合式部署時，它會代表內部 Exchange 2013 Client Access Server 和 Mailbox Server 與 EOP 進行通訊。Edge Transport Server 會當做內部部署 Mailbox Server 與 EOP 之間的轉送伺服器，用於內部部署組織到 Exchange Online 的外寄郵件傳送。Edge Transport Server 也會當做內部部署 Client Access Server 之間的轉送伺服器，用於 Exchange Online 組織到內部部署組織的內送郵件傳送。所有先前由 Client Access Server 所處理的連線安全性，現在則由 Edge Transport Server 處理。收件者查閱、規範原則及其他郵件檢查，會繼續在 Client Access Server 上進行。

## 無 Edge Transport Server 的郵件流程

下列程序與圖表描述在未部署 Edge Transport Server 的情況下，內部部署組織與 Exchange Online 之間郵件所採取的路徑：

1.  從內部部署組織傳送給 Exchange Online 組織收件者的輸出郵件，會從 Exchange 2010 信箱伺服器上的信箱傳送到 Exchange 2010 Hub Transport Server。

2.  Exchange 2010 Hub Transport Server 會將郵件傳送到 Exchange 2013 信箱伺服器。

3.  Exchange 2013 Mailbox Server 會直接將郵件傳送到 Exchange Online EOP 公司。

4.  EOP 會將郵件傳遞到 Exchange Online 組織。在此範例中，Client Access 及 Mailbox Server Role 安裝於相同的 Exchange 2013 Server。

從 Exchange Online 組織傳送到內部部署組織收件者的郵件，則會遵循反向路由。

**未部署 Edge Transport Server 之混合式部署中的郵件流程**

![沒有 Edge Transport Server 的內部部署](images/Dn393965.37bbe430-b157-4f52-83da-6d44f4459425(EXCHG.150).png "沒有 Edge Transport Server 的內部部署")

## 有 Edge Transport Server 的郵件流程

下列程序描述在部署 Edge Transport Server 的情況下，內部部署組織與 Exchange Online 之間郵件所採取的路徑。從內部部署組織傳送至 Exchange Online 組織收件者的郵件是從 Exchange 2010 信箱伺服器傳送：

1.  從內部部署組織傳送給 Exchange Online 組織收件者的輸出郵件，會從 Exchange 2010 信箱伺服器上的信箱傳送到 Exchange 2010 Hub Transport Server。

2.  Exchange 2010 Hub Transport Server 會將郵件傳送到 Exchange 2013 信箱伺服器。

3.  Exchange 2013 信箱伺服器會將郵件傳送到 Exchange 2013 或 Exchange 2010 SP3 Edge Transport Server。

4.  Edge Transport server 會將郵件傳送至 Exchange Online EOP 公司。

5.  EOP 會將郵件傳遞到 Exchange Online 組織。在此範例中，Client Access 及 Mailbox Server Role 安裝於相同的 Exchange 2013 Server。

從 Exchange Online 組織傳送到內部部署組織收件者的郵件，則會遵循反向路由。

**部署 Exchange 2013 或 2010 SP3 Edge Transport server 之混合式部署中的郵件流程**

![具有 Edge Transport Server 的內部部署](images/Dn393965.f1039133-249b-401d-bd39-3672442a06c9(EXCHG.150).png "具有 Edge Transport Server 的內部部署")

