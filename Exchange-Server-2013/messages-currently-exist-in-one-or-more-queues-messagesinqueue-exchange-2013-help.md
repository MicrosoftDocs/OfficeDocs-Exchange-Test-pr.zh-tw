---
title: '一或多個 queues_MessagesInQueue 中目前存在的郵件: Exchange 2013 Help'
TOCTitle: 一或多個 queues_MessagesInQueue 中目前存在的郵件
ms:assetid: 3ffcdc7e-c1b7-49a7-8e5f-b30c0397908d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.messagesinqueue(v=EXCHG.150)
ms:contentKeyID: 50473034
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 一或多個 queues\_MessagesInQueue 中目前存在的郵件

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2012-06-05_

此主題中的內容尚未針對 Microsoft Exchange Server 2013 進行更新。在更新之前，可能還是適用於 Exchange 2013。如果您仍然需要幫助，請查看下方的社群資源。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft® Exchange Server 2007 安裝程式會顯示這個警告因為嘗試解除安裝傳輸角色可能導致資料遺失從傳輸佇列。

Exchange 2007 的安裝程式進行檢查以確認傳輸佇列是空的之前它會移除管理那些佇列相關聯的角色。

如果您仍在傳輸佇列中移除傳輸角色之前傳送的訊息，可能會無限期保留這些訊息。

若要解決此問題，檢查以確認其空白的郵件才可繼續安裝程式所參照的佇列。

若要檢視佇列的內容

1.  開啟 Exchange 管理主控台。

2.  在主控台樹狀目錄中，按一下 **\[工具箱\]**。

3.  在 \[結果\] 窗格中，按一下 \[ **Exchange 佇列檢視器**\]。

4.  在執行窗格中，按一下 \[開啟工具\]。

5.  在佇列檢視器中，按一下 \[**佇列**\] 索引標籤。您已連線的伺服器上的所有佇列清單隨即顯示。

6.  以滑鼠右鍵按一下您想要並選取要檢視佇列的內容**屬性**的佇列。

若要檢視佇列中的郵件

1.  請依照下列步驟 1 到 4。

2.  在佇列檢視器中，按一下 \[**訊息**\] 索引標籤。您已連線的伺服器上的所有郵件清單隨即顯示。以調整檢視以單一佇列、 按一下 \[**佇列**\] 索引標籤、 連按兩下 \[佇列名稱，然後按一下 \[出現 \[Server\\Queue\] 索引標籤。

3.  若要檢視郵件的詳細的資訊，請選取郵件，然後按一下 \[動作\] 窗格中的**內容**。

