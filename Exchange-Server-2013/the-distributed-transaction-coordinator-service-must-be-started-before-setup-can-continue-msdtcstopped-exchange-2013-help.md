---
title: '安裝程式可以 continue_MSDTCStopped 之前必須啟動分散式交易協調器服務: Exchange 2013 Help'
TOCTitle: 安裝程式可以 continue_MSDTCStopped 之前必須啟動分散式交易協調器服務
ms:assetid: 96e33c94-348e-4a0b-9585-9bee81be4355
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.msdtcstopped(v=EXCHG.150)
ms:contentKeyID: 50473781
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 安裝程式可以 continue\_MSDTCStopped 之前必須啟動分散式交易協調器服務

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2012-06-05_

此主題中的內容尚未針對 Microsoft Exchange Server 2013 進行更新。在更新之前，可能還是適用於 Exchange 2013。如果您仍然需要幫助，請查看下方的社群資源。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft Exchange Server 2007 安裝程式無法繼續因為嘗試安裝用戶端存取伺服器或 Unified Messaging server 角色失敗，因為在目標電腦上未啟動分散式交易協調器服務。

Exchange 2007 的安裝程式需要安裝有 Dtc 服務狀態設為 \[**已啟動**的 Microsoft Exchange 的電腦。

Dtc 服務提供服務的設計用來確保成功且完整的交易，甚至是系統失敗、 與程序失敗的通訊失敗。

參與分散式交易每一部電腦管理自己的資源與資料並運作與交易中其他電腦也有作用。高於所有分散式的交易必須認可或中止完全參與的所有電腦上其工作。Dtc 所執行的交易協調角色的相關的元件和做為管理交易的每部電腦的交易管理員。

Client Access Server 和整合通訊伺服器角色上的分散式交易協調器服務有相依關係。

若要解決此問題，請確認 Dtc 服務狀態已在本機電腦上設定為 \[**已啟動**並再重新執行 Microsoft Exchange 安裝程式。

若要設定為 \['已啟動' Dtc 服務的狀態

1.  以滑鼠右鍵按一下 \[**我的電腦**，並再按一下 \[**管理**。

2.  依序展開 \[**服務及應用程式**\] 節點，並再按一下 \[**服務**\] 節點。

3.  在右窗格中，找出**Dtc**。

4.  以滑鼠右鍵按一下**Dtc**，並再按一下 \[**內容**。

5.  **啟動類型**設為**自動**進行且**服務狀態**為 \[**已啟動**。

6.  按一下 \[套用\]，然後按一下 \[確定\]。

