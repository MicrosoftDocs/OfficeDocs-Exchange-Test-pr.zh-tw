---
title: 'IIS 7.NET 擴充性元件是 required_LonghornIIS7NetExt: Exchange 2013 Help'
TOCTitle: IIS 7.NET 擴充性元件是 required_LonghornIIS7NetExt
ms:assetid: 8b481626-b68a-4fba-b66e-a02c03856bfd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.longhorniis7netext(v=EXCHG.150)
ms:contentKeyID: 50473694
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# IIS 7.NET 擴充性元件是 required\_LonghornIIS7NetExt

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2012-06-05_

此主題中的內容尚未針對 Microsoft Exchange Server 2013 進行更新。在更新之前，可能還是適用於 Exchange 2013。如果您仍然需要幫助，請查看下方的社群資源。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft®Exchange Server 2010 安裝程式無法繼續因為目標伺服器上未安裝必要的 Internet Information Server (IIS) 7.NET 擴充性元件。

Exchange 2010 可以使用 Windows PowerShell 遠端功能之前，必須在目標伺服器上安裝 IIS 7.NET 擴充性元件。

若要解決此錯誤，可使用伺服器管理員在此伺服器上安裝 IIS 7.NET 擴充性元件，然後重新執行 Exchange 2010 安裝程式。

使用 \[伺服器管理員工具在 Windows Server 2008 或 Windows Server 2008 R2 安裝 IIS 7.NET 擴充性元件

1.  按一下 \[**開始\]**、 \[**系統管理工具\]**及 \[**伺服器管理員**。

2.  在左側的功能窗格中，展開 \[角色\]，然後在 \[網頁伺服器 (IIS)\] 上按一下滑鼠右鍵，再選取 \[新增角色服務\]。

3.  在 \[**選取角色服務**\] 窗格中，捲動至**應用程式開發**。

4.  選取 \[ **.NET 擴充性**\] 核取方塊。

5.  從 \[**選取角色服務**\] 窗格中，按一下 \[**下一步**\] 和 \[**安裝**在 \[**確認安裝選項**\] 窗格。

6.  按一下 \[**關閉**結束 \[新增角色服務精靈\]。

