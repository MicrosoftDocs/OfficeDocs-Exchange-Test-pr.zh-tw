---
title: '本機電腦是子 domain_LocalComputerIsDCInChildDomain 的網域控制站: Exchange 2013 Help'
TOCTitle: 本機電腦是子 domain_LocalComputerIsDCInChildDomain 的網域控制站
ms:assetid: 7db1dcc0-d953-41b8-b081-2a47a70950c4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.localcomputerisdcinchilddomain(v=EXCHG.150)
ms:contentKeyID: 50473589
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 本機電腦是子 domain\_LocalComputerIsDCInChildDomain 的網域控制站

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2012-06-05_

此主題中的內容尚未針對 Microsoft Exchange Server 2013 進行更新。在更新之前，可能還是適用於 Exchange 2013。如果您仍然需要幫助，請查看下方的社群資源。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft® Exchange Server 2007 安裝程式無法繼續因為本機電腦是子網域的網域控制站。

Exchange 2007 的安裝程式會安裝登入到子網域的網域控制站的網域控制站為通用類別目錄伺服器。

若要解決此問題，提升的通用類別目錄伺服器之網域控制站或 Exchange 2007 安裝至非網域控制站中子網域的成員伺服器，然後重新執行 Microsoft Exchange 安裝程式。

若要更正此警告所進行之 Exchange 伺服器的通用類別目錄伺服器

1.  在網域控制站上按一下 \[**開始\]**、 指向 \[**程式\]**、 \[**系統管理工具**\] 及 \[ **Active Directory 站台及服務**。

2.  在主控台樹狀目錄中，連按兩下 \[**網站**、 網站的名稱上按兩下和連按兩下 \[**伺服器**。

3.  按兩下 \[目標網域控制站。

4.  在 \[結果\] 窗格中，以滑鼠右鍵按一下**NTDS 設定**\] 和 \[**屬性**。

5.  在 \[**一般**\] 索引標籤上按一下以選取 \[**通用類別目錄**\] 核取方塊。

6.  重新啟動之網域控制站。

