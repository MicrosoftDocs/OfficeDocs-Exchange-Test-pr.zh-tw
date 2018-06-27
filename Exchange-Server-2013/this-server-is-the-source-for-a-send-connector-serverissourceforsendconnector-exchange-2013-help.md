---
title: '此伺服器為傳送 Connector_ServerIsSourceForSendConnector 的來源: Exchange 2013 Help'
TOCTitle: 此伺服器為傳送 Connector_ServerIsSourceForSendConnector 的來源
ms:assetid: 151c0014-c90c-4c52-8e74-4b3f1bc7aaf1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.serverissourceforsendconnector(v=EXCHG.150)
ms:contentKeyID: 50472669
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 此伺服器為傳送 Connector\_ServerIsSourceForSendConnector 的來源

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2016-12-09_

此主題中的內容尚未針對 Microsoft Exchange Server 2013 進行更新。在更新之前，可能還是適用於 Exchange 2013。如果您仍然需要幫助，請查看下方的社群資源。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft Exchange Server 2007 安裝程式無法繼續因為嘗試移除 Hub Transport server role 失敗。本機電腦為 Exchange 組織中的一或多個傳送連接器的來源。

傳送連接器代表透過傳送輸出郵件的邏輯閘道。

Exchange 2007 的安裝程式需要為 Exchange 組織的所有傳送連接器即將移動或刪除集線傳輸伺服器電腦的伺服器角色可以刪除之前。

若要解決此問題，移動或刪除本機電腦的所有傳送連接器，然後重新執行安裝程式。

如需修改或移除傳送連接器的詳細資訊，請參閱 Exchange Server 2007 產品文件中的下列主題：

  - 「 如何移除的傳送連接器 」 ([https://go.microsoft.com/fwlink/?LinkId=86655](https://go.microsoft.com/fwlink/?linkid=86655))。

  - "How to 修改的傳送連接器組態 」 ([https://go.microsoft.com/fwlink/?LinkId=86656](https://go.microsoft.com/fwlink/?linkid=86656))。

