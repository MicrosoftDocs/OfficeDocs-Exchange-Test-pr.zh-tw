---
title: 'COM + 事件系統必須啟動服務之前安裝程式可以 continue_EventSystemStopped: Exchange 2013 Help'
TOCTitle: COM + 事件系統必須啟動服務之前安裝程式可以 continue_EventSystemStopped
ms:assetid: 3b8d2ba3-87fb-4749-b4d1-5dfec97e1ca4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.eventsystemstopped(v=EXCHG.150)
ms:contentKeyID: 50472921
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# COM + 事件系統必須啟動服務之前安裝程式可以 continue\_EventSystemStopped

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2012-06-05_

此主題中的內容尚未針對 Microsoft Exchange Server 2013 進行更新。在更新之前，可能還是適用於 Exchange 2013。如果您仍然需要幫助，請查看下方的社群資源。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft Exchange Server 2007 安裝程式無法繼續因為嘗試安裝 Client Access Server 或 Edge Transport server 角色失敗，因為在目標電腦上未啟動 COM + 事件系統服務。

Exchange 2007 的安裝程式需要安裝有 COM + 事件系統服務狀態設為 \[**已啟動**的 Microsoft Exchange 的電腦。

COM + 事件系統服務支援 COM + 元件提供自動發佈事件訂閱 COM 元件的系統事件通知。

Client Access Server 及 Edge Transport server role 上 COM + 訂閱 COM + 事件系統服務的元件有相依關係。

若要解決此問題，請確認 COM + 事件系統服務狀態已在本機電腦上設定為 \[**已啟動**並再重新執行 Microsoft Exchange 安裝程式。

若要設定為 \['已啟動' COM + 事件系統服務的狀態

1.  以滑鼠右鍵按一下 \[**我的電腦**，並再按一下 \[**管理**。

2.  依序展開 \[**服務及應用程式**\] 節點，並再按一下 \[**服務**\] 節點。

3.  在右窗格中，找出**Com + 事件系統**。

4.  以滑鼠右鍵按一下**Com + 事件系統**，並再按一下 \[**內容**。

5.  **啟動類型**設為**自動**進行且**服務狀態**為 \[**已啟動**。

6.  按一下 \[套用\]，然後按一下 \[確定\]。

