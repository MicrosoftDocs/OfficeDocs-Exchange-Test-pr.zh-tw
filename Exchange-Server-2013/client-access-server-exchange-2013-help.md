---
title: 'Client Access server: Exchange 2013 Help'
TOCTitle: Client Access server
ms:assetid: 87e206ab-7a7b-4b4f-be1a-5035713c74d2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd298114(v=EXCHG.150)
ms:contentKeyID: 50473634
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Client Access server

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-07-02_

針對 Microsoft Exchange 2013，Exchange 伺服器角色的架構有一些重大改變。有別於 Exchange 2010 和 Exchange 2007 中出現的五個伺服器角色，在 Exchange 2013 中，伺服器的角色已減至三個：Client Access Server 和 Mailbox Server，以及裝上 Service Pack 1 之後的 Edge Transport server role。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Exchange 2013 也可以與 Exchange 2010 Edge Transport server role 一起使用。</td>
</tr>
</tbody>
</table>


Exchange 2013 Mailbox Server 包含 Exchange 2010 中的許多伺服器元件：用戶端存取通訊協定、傳輸服務、信箱資料庫及整合通訊服務 (Client Access Server 會將傳入呼叫所產生的 SIP 流量重新導向至 Mailbox Server)。如需 Exchange 2013 信箱伺服器的相關資訊，請參閱 [信箱伺服器](mailbox-server-exchange-2013-help.md)。

Client Access Server 提供驗證、Proxy 和有限重新導服務，也提供所有常用的用戶端存取通訊協定：HTTP、POP、IMAP 及 SMTP。Client Access Server 是精簡且不留狀態的伺服器，完全不留任何資料記錄。戶端存取伺服器上永遠不會佇列或儲存任何東西。如需 Exchange 2013 架構的相關資訊，請參閱 [Exchange 2013 的新功能](what-s-new-in-exchange-2013-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>周邊網路中不支援 Client Access Server，必須部署在內部 Active Directory 環境內。每一個含有信箱伺服器的 Active Directory 站台也必須含有用戶端伺服器。</td>
</tr>
</tbody>
</table>


架構性變更會導致用戶端連接性也有部分變更。首先，RPC/TCP 不再是支援的直接存取通訊協定。這表示所有 Outlook 連線必須利用 RPC over HTTPS (也稱為 Outlook 無所不在) 進行，或者，搭配 Exchange 2013 SP1 和 Outlook 2013 SP1 時，必須利用 MAPI over HTTP 進行。由於有這些變更，Client Access Server 上不需要有 RPC Client Access 服務。此外，站台恢復解決方案所需的命名空間比 Exchange 2010 中所需的數目更少，而且再也不必為 RPC Client Access 服務提供親和性。此外，Outlook 用戶端不必再像所有舊版 Exchange 一樣，得連線到伺服器完整格式的網域名稱 (FQDN)。使用自動探索，Outlook 找到一個新的連線點，此連線點是由 GUID + @ + 使用者主要 SMTP 位址的網域部分組成。這項變更讓使用者比較不會收到「管理員已變更您的信箱」這麼嚴重的訊息。只有 Outlook 2007 和更高版本支援 Exchange 2013。

## 用戶端存取伺服器功能

Exchange 2013 中用戶端存取伺服器的功能如同前哨站一般，可接收所有用戶端的請求並將它們路由到正確且使用中的信箱資料庫。用戶端存取伺服器提供安全通訊端層 (SSL) 和用戶端驗證等網路安全性功能，可透過重新導向和 Proxy 功能管理用戶端連線。用戶端存取伺服器會驗證用戶端的連線，大部分情況下，還會向目前使用中含有使用者信箱之資料庫副本的信箱伺服器發出代理要求。有些時候，用戶端存取伺服器可能會將要求重新導向給更適合的用戶端存取伺服器，該伺服器可能位在不同的位置或其 Exchange 伺服器版本較新。

用戶端存取伺服器具有以下功能：

  - **不留狀態的伺服器** 在舊版 Exchange 中，許多用戶端存取通訊協定需要工作階段親和性。例如，Outlook Web App 要求所有來自特定用戶端的要求，需由用戶端存取伺服器負載平衡陣列內的特定用戶端存取伺服器處理。在 Exchange 2013 中，用戶端存取伺服器是無狀態的。換句話說，由於所有信箱作業的處理都是發生在信箱伺服器上，所以由用戶端存取伺服器陣列中的哪個用戶端存取伺服器來接收每個個別用戶端要求都沒有關係。這項功能變更代表在負載平衡層級時不再需要工作階段親和性。這讓用戶端存取伺服器的傳入連線可以採用 DNS round-robin 這類負載平衡技術的簡單技巧來進行平衡。它也可以讓硬體負載平衡裝置所支援的同時連線數大幅增加。

  - **連線共用** 用戶端存取伺服器會處理用戶端驗證並傳送 AuthN 資料到信箱伺服器。用戶端存取伺服器用來連線信箱伺服器的帳戶是 Exchange 伺服器群組成員的一個權限帳戶。這讓用戶端存取伺服器可以有效共用信箱伺服器的連線。用戶端存取伺服器陣列可以處理數百萬個網際網路用戶端連線，但其向信箱伺服器發出代理要求的連線數比舊版 Exchange 少得多。 這提高了處理效率和端對端的延遲時間。

## 在用戶端存取伺服器上的管理工作

在 Exchange 2013 中，您可以在用戶端存取伺服器上執行一些主要工作。數位憑證的管理就是在用戶端存取伺服器上執行的主要工作之一，另外，用戶端存取伺服器也可以處理 Exchange ActiveSync、POP3 和 IMAP4 等用戶端通訊協定管理。

