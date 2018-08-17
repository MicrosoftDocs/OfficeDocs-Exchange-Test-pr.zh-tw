---
title: 'World Wide Web Publishing 服務已停用或遺失'
TOCTitle: World Wide Web Publishing 服務已停用] 或 [missing_W3SVCDisabledOrNotInstalled
ms:assetid: 2d26d778-ddf1-4225-b5e2-f6b49d819c94
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.w3svcdisabledornotinstalled(v=EXCHG.150)
ms:contentKeyID: 50472896
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# World Wide Web Publishing 服務已停用\] 或 \[missing\_W3SVCDisabledOrNotInstalled

 

_<strong>適用版本：</strong> Exchange Server_

_<strong>上次修改主題的時間：</strong> 2012-06-05_

此主題中的內容尚未針對 Microsoft Exchange Server 2013 進行更新。在更新之前，可能還是適用於 Exchange 2013。如果您仍然需要幫助，請查看下方的社群資源。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft® Exchange Server 2007 安裝程式無法繼續因為嘗試安裝信箱伺服器或用戶端存取角色上找到的 World Wide Web Publishing 服務已停用或未安裝在這部電腦上。

Exchange 2007 的安裝程式會要求您安裝 Microsoft Exchange 移轉至已安裝並設定為以外停用的某個項目 World Wide Web Publishing 服務的電腦。

若要解決此問題，確認 World Wide Web Publishing 服務已安裝並不在本機電腦上已停用並再重新執行 Microsoft Exchange 安裝程式。

若要確認 World Wide Web Publishing 服務已安裝並不會停用

1.  <strong>「 我的電腦</strong>在桌面上按一下滑鼠右鍵並再按一下 \[<strong>管理</strong>。

2.  依序展開 \[<strong>服務及應用程式</strong>\] 節點，並再按一下 \[<strong>服務</strong>\] 節點。

3.  在右窗格中，尋找<strong>World Wide Web Publishing 服務\]</strong>。
    
    如果<strong>World Wide Web Publishing 服務</strong>不會顯示在已安裝的服務清單中，遵循下列程序中的步驟安裝方式。

4.  如果<strong>World Wide Web Publishing 服務</strong>會顯示但以外的<strong>啟動</strong>狀態，繼續執行下列步驟來啟動它。

5.  以滑鼠右鍵按一下 \[ <strong>World Wide Web Publishing 服務</strong>，並再按一下 \[<strong>內容</strong>。

6.  確認<strong>啟動類型</strong>是<strong>自動</strong>且<strong>服務狀態</strong>設為 \[<strong>已啟動</strong>。

7.  按一下 \[<strong>套用</strong>\]，然後按一下 \[<strong>確定</strong>\]。

若要安裝 World Wide Web Publishing 服務

1.  \[<strong>開始</strong>\] 功能表上選取 \[<strong>設定</strong>\] 的 \[<strong>控制台</strong>\] 和 \[<strong>新增或移除程式\]</strong>

2.  按一下 \[<strong>新增/移除 Windows 元件</strong>\]。

3.  \[<strong>元件</strong>\] 清單中選取<strong>應用程式伺服器</strong>\] 核取方塊，和 \[<strong>詳細資料</strong>。

4.  選取 \[<strong>網際網路資訊服務管理員</strong>\] 和 \[<strong>詳細資料</strong>。

5.  選取 \[ <strong>World Wide Web 服務</strong>\]，然後選取 \[核取方塊。

6.  若要返回 \[<strong>元件</strong>\] 清單中，按一下<strong>\[確定\]</strong>兩次並再按 \[<strong>下一步</strong>。

7.  安裝 IIS 服務時按一下 \[<strong>完成</strong>\]。

