---
title: 'Exchange  混合式部署中的傳輸路由: Exchange 2013 Help'
TOCTitle: Exchange  混合式部署中的傳輸路由
ms:assetid: 36c2cea3-2e2f-40ac-88bd-7e1b6bd27828
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ659050(v=EXCHG.150)
ms:contentKeyID: 50474707
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 混合式部署中的傳輸路由

 

_**適用版本：** Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：** 2016-07-29_


本主題討論來回於網際網路之內送和外寄郵件的路由傳送選項。

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
<th><img src="images/JJ150559.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>本主題中的範例，並不包含將 Edge Transport Server 新增至混合式部署中。郵件在內部部署組織、Exchange Online 組織以及網際網路之間所採取的路由，不會因為 Edge Transport Server 的增加而變更。路由只會在內部部署組織內變更。如需有關新增 Edge Transport Server 至混合式部署的詳細資訊，請參閱<a href="edge-transport-servers-with-hybrid-deployments-exchange-2013-help.md">Edge Transport server 與混合式部署</a>。</td>
</tr>
</tbody>
</table>


## 網際網路的內送郵件

在規劃和設定混合式部署的過程中，您需要決定是否讓來自網際網路寄件者的所有郵件透過 Exchange Online 或是您的內部部署組織進行路由傳送。所有來自網際網路寄件者的郵件，最初都會傳遞至您所選取的組織，然後會根據收件者信箱的所在位置進行路由傳送。選擇要讓郵件透過 Exchange Online 或是您的內部部署組織路由傳送，受許多因素影響，這些因素包括您是否要將規範原則套用到傳送到這兩個組織的所有郵件、每個組織有多少信箱，以及其他因素。

傳送到內部部署與 Exchange Online 組織收件者的郵件所使用的路徑，取決於您決定設定混合式部署中 MX 記錄的方式。偏好的方法是設定您的 MX 記錄以在 Office 365 中指向 Exchange Online Protection (EOP)，因為此組態提供最準確的垃圾郵件篩選。混合組態精靈不會設定內部部署或 Exchange Online 組織的內送網際網路郵件的路由。如果您想要變更傳遞內送網際網路郵件的方式，則必須手動設定 MX 記錄。

  - **如果您決定將 MX 記錄變更為指向 Office 365 中的 Exchange Online Protection 服務**   這是對於混合式部署的建議組態。傳送至任一組織中任何收件者的所有郵件都會先透過 Exchange Online 組織路由傳送。收件者地址位於內部部署組織中的郵件，將先透過 Exchange Online 組織路由傳送，然後再傳遞給內部部署組織中的收件者。如果 Exchange Online 組織中的收件者多於內部部署組織中的收件者，則建議您使用此路由。此組態選項對於 Exchange Online Protection 提供掃描和封鎖垃圾郵件是必要選項。

  - **如果您決定讓 MX 記錄繼續指向內部部署組織**   傳送至任一組織中任何收件者的所有郵件都會先透過內部部署組織路由傳送。收件者地址位於 Exchange Online 中的郵件，將先透過內部部署組織路由傳送，然後再傳遞給 Exchange Online 中的收件者。如果組織訂有規範原則，要求傳送到組織及從組織送出的郵件都要由日誌解決方案檢查，這個路由就很有用。如果您選取此選項，Exchange Online Protection 無法有效地掃描垃圾郵件。

如需詳細資訊，請參閱 [Exchange Online 與 Office 365 （概觀） 的郵件流程最佳作法](https://technet.microsoft.com/zh-tw/library/jj937232\(v=exchg.150\))。

請閱讀下一節，了解如何規劃將來自網際網路收件者的郵件，路由傳送到您的內部部署與 Exchange Online 收件者。在每個區段中，「內部部署 Exchange 伺服器」可以是 Exchange 2013 用戶端存取伺服器或 Exchange 2016 信箱伺服器。

## 透過 Exchange Online 組織路由傳送內送網際網路郵件

下列步驟與圖表說明當您決定讓 MX 記錄指向 Office 365 組織中的 EOP 服務時，在您的混合式部署中發生的內送郵件路徑。郵件路徑會因為您選擇啟用集中式郵件傳輸與否而有所不同。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ906432.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您可能需要為每個內部部署信箱購買 EOP 授權，這些信箱接收的郵件會先傳遞到 EOP，然後透過 Exchange Online 組織進行路由傳送。如需詳細資訊，請連絡您的 Microsoft 轉銷商。</td>
</tr>
</tbody>
</table>


若集中式郵件傳輸為 **「停用」** (Disabled) (預設組態) 狀態，內送網際網路郵件會依下述方式在混合式部署中路由傳送：

1.  內送郵件是從網際網路件寄件者傳送到收件者 julie@contoso.com 與 david@contoso.com。Julie 的信箱位於內部部署組織的 Exchange Mailbox Server 上。David 的信箱位於 Exchange Online 中。

2.  由於這兩位收件者都有 contoso.com 電子郵件地址，而且 contoso.com 的 MX 記錄指向 EOP，因此郵件會傳遞至 EOP。

3.  EOP 會將兩位收件者的郵件路由傳送到 Exchange Online。

4.  Exchange Online 會掃描郵件是否有病毒，並為每個收件者執行查閱。透過查閱可以判斷 Julie 的信箱位於內部部署組織中，而 David 的信箱則位於 Exchange Online 組織中。

5.  Exchange Online 會將郵件分割為兩個副本。郵件的其中一個副本會傳遞到 David 的信箱。

6.  第二個副本會從 Exchange Online 傳回 EOP。

7.  EOP 會將郵件傳送至內部部署組織中的內部部署 Exchange 伺服器。

8.  Exchange 會將郵件傳送至 Exchange 信箱伺服器，並會從該處將其傳遞至 Julie 的信箱。

**在集中式郵件傳輸停用 (預設組態) 的情況下，透過 Exchange Online 組織路由傳送內部部署和 Exchange Online 組織的郵件**

![集中輸入至 EXO](images/JJ659050.f98341e0-088d-49f0-bf8e-09f35255bf9e(EXCHG.150).png "集中輸入至 EXO")

若集中式郵件傳輸為 **「啟用」** (Enabled) 狀態，內送網際網路郵件會依下述方式在混合式部署中路由傳送：

1.  內送郵件是從網際網路件寄件者傳送到收件者 julie@contoso.com 與 david@contoso.com。Julie 的信箱位於內部部署組織的 Exchange Mailbox Server 上。David 的信箱位於 Exchange Online 中。

2.  由於這兩位收件者都有 contoso.com 電子郵件地址，而且 contoso.com 的 MX 記錄指向 EOP，因此郵件會傳遞至 EOP 並進行病毒掃描。

3.  由於集中式郵件傳輸為啟用狀態，因此 EOP 會將這兩位收件者的郵件路由傳送至內部部署 Exchange 伺服器。

4.  內部部署 Exchange 伺服器會為每一位收件者執行查閱。透過查閱可以判斷 Julie 的信箱位於內部部署組織中，而 David 的信箱則位於 Exchange Online 組織中。

5.  內部部署 Exchange 伺服器將郵件分割為兩個副本。郵件的其中一個副本會傳送到 Julie 在內部部署 Exchange 信箱伺服器中的信箱。

6.  第二個副本會從內部部署 Exchange 伺服器傳回 EOP。

7.  EOP 會將郵件傳送到 Exchange Online。

8.  Exchange 會將郵件傳遞至 David 的信箱。

**在集中式郵件傳輸啟用的情況下，透過 Exchange Online 組織路由傳送內部部署和 Exchange Online 組織的郵件**

![輸入 EXO，啟用集中式](images/JJ659050.062422d5-9cb6-42c2-9ec0-31962cd7ada6(EXCHG.150).png "輸入 EXO，啟用集中式")

## 透過內部部署組織路由傳送內送網際網路郵件

下列步驟與圖表說明當您決定讓 MX 記錄繼續指向內部部署組織時，將在您的混合式部署中發生的內送網際網路郵件路徑。

1.  內送郵件是從網際網路件寄件者傳送到收件者 julie@contoso.com 與 david@contoso.com。Julie 的信箱位於內部部署組織的 Exchange Mailbox Server 上。David 的信箱位於 Exchange Online 中。

2.  由於這兩位收件者都擁有 contoso.com 電子郵件地址，而且 contoso.com 的 MX 記錄指向內部部署組織，因此郵件會傳遞至內部部署 Exchange 伺服器。

3.  內部部署 Exchange 伺服器會使用內部部署通用類別目錄伺服器查閱每一位收件者。藉由通用類別目錄查閱，就能判斷出 Julie 的信箱位於內部部署 Exchange 信箱伺服器上，而 David 的信箱位於 Exchange Online 組織且混合式路由位址為 david@contoso.mail.onmicrosoft.com。

4.  內部部署 Exchange 伺服器將郵件分割為兩個副本。郵件的其中一個副本會傳送到內部部署 Exchange 信箱伺服器，然後傳遞到 Julie 的信箱。

5.  郵件的第二個副本會由內部部署 Exchange 伺服器使用設定為使用 TLS 的傳送連接器傳送到 EOP (其會接收傳送至 Exchange Online 組織的郵件)。

6.  EOP 會將郵件傳送到 Exchange Online 組織，其中會先掃描郵件是否有病毒，再傳遞到 David 的信箱。

**透過內部部署組織路由傳送內部部署和 Exchange Online 組織的郵件**

![集中式輸入郵件，內部部署](images/JJ659050.a246a1e2-7593-4d13-9426-73622a545c9a(EXCHG.150).png "集中式輸入郵件，內部部署")

## 傳送到網際網路的外寄郵件

除了選擇如何路由傳送寄給您組織內收件者的內送郵件之外，您還可以選擇如何路由傳送 Exchange Online 收件者所傳送的外寄郵件。執行混合組態精靈時，您可以選取兩個選項的其中一個：

  - **不啟用集中式郵件傳輸**   此為混合組態精靈中的預設選項，會將從 Exchange Online 組織傳送的外寄郵件直接路由傳送到網際網路。如果您不需要對 Exchange Online 組織收件者送出的郵件套用任何內部部署規範原則或其他處理規則，請使用此選項。

  - **啟用集中式郵件傳輸**   選取這個選項會經由您的內部部署組織路由傳送從 Exchange Online 組織傳送的外寄郵件。除了傳送給相同 Exchange Online 組織中其他收件者的郵件以外，Exchange Online 組織中收件者送出的所有郵件，都會經由內部部署組織傳送。這樣一來，無論收件者位於 Exchange Online 組織還是內部部署組織，您都可以對這些郵件以及必須套用至所有收件者的其他程序或需求套用規範規則。
    
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


不論您在混合組態精靈中選取哪個選項，內部部署收件者送出的郵件一律會使用 DNS 直接傳送給網際網路收件者。

下列步驟與圖表說明內部部署收件者送出之郵件的外寄郵件路徑。

1.  Julie 在內部部署 Exchange Mailbox Server 上有個信箱，他將郵件傳送給外部網際網路收件者 erin@cpandl.com。

2.  Exchange 伺服器會查閱 MX 記錄中的 cpandl.com，並且將郵件傳送到位於網際網路的 cpandl.com 郵件伺服器。

**內部部署寄件者寄給網際網路收件者的郵件**

![從內部部署輸出郵件](images/JJ659050.71f287d6-b814-4820-a0dc-575f17d13894(EXCHG.150).png "從內部部署輸出郵件")

請閱讀下一節，了解如何規劃將 Exchange Online 組織收件者送出的郵件，路由傳送給網際網路收件者。

## 使用 DNS 從 Exchange Online 傳遞要送至網際網路的郵件 (集中式郵件傳輸已停用)

下列步驟與圖表說明未選取混合組態精靈中的 \[啟用集中式郵件傳輸\] (預設組態) 時，Exchange Online 收件者傳送至網際網路收件者之郵件的外寄郵件路徑。

1.  David 在 Exchange Online 組織中有個信箱，他將郵件傳送給外部網際網路收件者 erin@cpandl.com。

2.  Exchange Online 會對郵件進行病毒掃描，然後將郵件傳送到 Exchange Online EOP 公司。

3.  EOP 會查閱 cpandl.com 的 MX 記錄，並且將郵件傳送到位於網際網路的 cpandl.com 郵件伺服器。

**在集中式郵件傳輸停用 (預設組織) 的情況下，將 Exchange Online 寄件者的郵件直接路由傳送至網際網路**

![EXO 直接輸出郵件](images/JJ659050.fe1c4241-0d6e-47bf-b61d-5af732d2dbbc(EXCHG.150).png "EXO 直接輸出郵件")

## 透過內部部署組織從 Exchange Online 路由傳送要送到網際網路的郵件 (集中式郵件傳輸已啟用)

下列步驟與圖表說明當您選取混合組態精靈中的 \[啟用集中式郵件傳輸\] 時，Exchange Online 收件者傳送至網際網路收件者之郵件的外寄郵件路徑。

1.  David 在 Exchange Online 組織中有個信箱，他將郵件傳送給外部網際網路收件者 erin@cpandl.com。

2.  Exchange Online 會對郵件進行病毒掃描，然後將郵件傳送到 EOP。

3.  EOP 設定為將所有要送至網際網路的郵件傳送到內部部署伺服器，因此郵件會路由傳送至內部部署 Exchange 伺服器。郵件使用 TLS 傳送。

4.  內部部署 Exchange 伺服器會對 David 的郵件執行系統管理員設定的規範、防毒和任何其他程序。

5.  內部部署 Exchange 伺服器會查閱 MX 記錄中的 cpandl.com，並且將郵件傳送到位於網際網路的 cpandl.com 郵件伺服器。

**在啟用集中式郵件傳輸的情況下，透過內部部署組織路由傳送 Exchange Online 寄件者的郵件**

![透過內部部署輸出 EXO](images/JJ659050.7ea9ffee-944b-45ae-ba4d-c3484100399b(EXCHG.150).png "透過內部部署輸出 EXO")

