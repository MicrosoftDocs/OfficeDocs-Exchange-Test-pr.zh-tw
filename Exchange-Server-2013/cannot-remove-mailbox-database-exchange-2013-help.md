---
title: '無法移除信箱資料庫: Exchange 2013 Help'
TOCTitle: 無法移除信箱資料庫
ms:assetid: 5881e4c0-c2e2-48db-84b4-7f9ce3cf46a7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.unwillingtoremovemailboxdatabase(v=EXCHG.150)
ms:contentKeyID: 50473249
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 無法移除信箱資料庫

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2012-11-08_

Microsoft Exchange Server 2013安裝程式無法繼續因為它無法從本機伺服器移除使用者信箱資料庫不產生可能遺失資料。

Exchange 2013安裝程式會判斷是否所有信箱資料庫已都移除從伺服器都移除 Mailbox server role 之前。不過，使用者信箱可能仍維持在伺服器上。

若要解決此問題，請將所有信箱伺服器上都移至另一部 Exchange 伺服器或信箱和中其所包含的資料不再是必要的如果停用信箱。然後重新執行Exchange 2013安裝程式。

  - 如需如何識別在資料庫中的信箱的詳細資訊，請參閱[Get-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123685\(v=exchg.150\))。

  - 如需如何移動信箱的詳細資訊，請參閱[在 Exchange 2013 移動信箱](mailbox-moves-in-exchange-2013-exchange-2013-help.md)。

  - 如需如何停用信箱的詳細資訊，請參閱[Disable-Mailbox](https://technet.microsoft.com/zh-tw/library/aa997210\(v=exchg.150\))。

  - 如需如何移除信箱資料庫的詳細資訊，請參閱[管理 Exchange 2013 中的信箱資料庫](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md)。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

找到您要的資訊了嗎？請撥冗[提供您的意見](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac)讓我們知道您需要什麼資訊。

