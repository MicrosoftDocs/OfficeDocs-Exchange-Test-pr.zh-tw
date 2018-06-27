---
title: '網域準備 required_DomainPrepRequired: Exchange 2013 Help'
TOCTitle: 網域準備 required_DomainPrepRequired
ms:assetid: f6feae6f-7404-4b1f-887f-ed63c26a6bcd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.domainpreprequired(v=EXCHG.150)
ms:contentKeyID: 50474609
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 網域準備 required\_DomainPrepRequired

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2016-12-09_

此主題中的內容尚未針對 Microsoft Exchange Server 2013 進行更新。在更新之前，可能還是適用於 Exchange 2013。如果您仍然需要幫助，請查看下方的社群資源。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft Exchange Server 2007 安裝程式無法繼續因為嘗試安裝伺服器角色失敗。

Microsoft Exchange 安裝程式需要特定伺服器角色，才能安裝，為 Exchange Server 2007 準備本機網域。

Exchange Server 2007 的網域準備包含下列工作：

  - Exchange Server、 Exchange 組織系統管理員、 經過驗證的使用者及 Exchange 信箱管理員的網域容器上設定權限。

  - 如果不存在，建立的 Microsoft Exchange 系統物件容器與此容器上設定權限的 Exchange 伺服器、 Exchange 組織系統管理員及經過驗證的使用者。

  - 在目前的網域中建立新的網域全域群組呼叫 Exchange Install Domain Servers。

  - 將 Exchange Install Domain Servers 群組新增至根網域中 Exchange Servers USG。

若要解決此問題，請執行**setup /PrepareDomain**準備本機網域和重試伺服器角色安裝。

如需如何執行 PrepareDomain 程序，請參閱"方式來準備 Active Directory 及網域 」 ([https://go.microsoft.com/fwlink/?LinkId=78453](https://go.microsoft.com/fwlink/?linkid=78453)) 的詳細資訊。

