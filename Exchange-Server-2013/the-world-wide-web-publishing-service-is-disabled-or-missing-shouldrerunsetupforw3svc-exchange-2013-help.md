---
title: 'World Wide Web Publishing 服務已停用] 或 [missing_ShouldReRunSetupForW3SVC: Exchange 2013 Help'
TOCTitle: World Wide Web Publishing 服務已停用] 或 [missing_ShouldReRunSetupForW3SVC
ms:assetid: f1815a6d-d16b-4271-9fab-84087465529e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.shouldrerunsetupforw3svc(v=EXCHG.150)
ms:contentKeyID: 50474569
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# World Wide Web Publishing 服務已停用\] 或 \[missing\_ShouldReRunSetupForW3SVC

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2012-06-05_

此主題中的內容尚未針對 Microsoft Exchange Server 2013 進行更新。在更新之前，可能還是適用於 Exchange 2013。如果您仍然需要幫助，請查看下方的社群資源。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft® Exchange Server 2007 安裝程式無法繼續因為嘗試安裝信箱伺服器或用戶端存取角色上找到的 World Wide Web Publishing 服務已停用或未安裝在這部電腦上。

Exchange 2007 的安裝程式會要求您安裝 Microsoft Exchange 移轉至已安裝並設定為以外停用的某個項目 World Wide Web Publishing 服務的電腦。

若要解決此問題，確認 World Wide Web Publishing 服務已安裝並不在本機電腦上已停用並再重新執行 Microsoft Exchange 安裝程式。

若要確認 World Wide Web Publishing 服務已安裝並不會停用

1.  **「 我的電腦**在桌面上按一下滑鼠右鍵並再按一下 \[**管理**。

2.  依序展開 \[**服務及應用程式**\] 節點，並再按一下 \[**服務**\] 節點。

3.  在右窗格中，尋找**World Wide Web Publishing 服務\]**。
    
    如果**World Wide Web Publishing 服務**不會顯示在已安裝的服務清單中，遵循下列程序中的步驟安裝方式。

4.  如果**World Wide Web Publishing 服務**會顯示但以外的**啟動**狀態，繼續執行下列步驟來啟動它。

5.  以滑鼠右鍵按一下 \[ **World Wide Web Publishing 服務**，並再按一下 \[**內容**。

6.  確認**啟動類型**是**自動**且**服務狀態**設為 \[**已啟動**。

7.  按一下 \[**套用**\]，然後按一下 \[**確定**\]。

若要安裝 World Wide Web Publishing 服務

1.  \[**開始**\] 功能表上選取 \[**設定**\] 的 \[**控制台**\] 和 \[**新增或移除程式\]**

2.  按一下 \[**新增/移除 Windows 元件**\]。

3.  \[**元件**\] 清單中選取**應用程式伺服器**\] 核取方塊，和 \[**詳細資料**。

4.  選取 \[**網際網路資訊服務管理員**\] 和 \[**詳細資料**。

5.  選取 \[ **World Wide Web 服務**\]，然後選取 \[核取方塊。

6.  若要返回 \[**元件**\] 清單中，按一下**\[確定\]**兩次並再按 \[**下一步**。

7.  安裝 IIS 服務時按一下 \[**完成**\]。

