---
title: 'Windows 處理程序啟用 Service-程序模型元件是 required_LonghornWASProcessModelInstalled: Exchange 2013 Help'
TOCTitle: Windows 處理程序啟用 Service-程序模型元件是 required_LonghornWASProcessModelInstalled
ms:assetid: 8cc13dbb-4921-4c07-8602-d26613d7730a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.longhornwasprocessmodelinstalled(v=EXCHG.150)
ms:contentKeyID: 50473697
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Windows 處理程序啟用 Service-程序模型元件是 required\_LonghornWASProcessModelInstalled

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2015-04-07_

此主題中的內容尚未針對 Microsoft Exchange Server 2013 進行更新。在更新之前，可能還是適用於 Exchange 2013。如果您仍然需要幫助，請查看下方的社群資源。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Exchange Server 2010安裝程式無法繼續安裝在Windows Server 2008-或Windows Server 2008 R2 型電腦因為伺服器上未安裝 Windows 程序啟用 Service-程序模型功能。

Windows 處理程序啟用服務可以產生網際網路資訊服務 (IIS) 程序模型中，移除 HTTP 上的相依性。現在可供使用非 HTTP 通訊協定來裝載 Windows Communication Foundation (WCF) 服務的應用程式的已先前僅適用於 HTTP 應用程式的 IIS 的所有功能。IIS 7.0 也會使用訊息型啟用 Windows 程序啟用服務 over HTTP。

程序模型主控 Web 及 WCF 服務。最早出現在 IIS 6.0、 程序模型是新的架構該功能快速失敗保護、 健康狀況監控與回收。

若要解決此問題，請安裝 Windows 程序啟用服務位在此伺服器上的程序模型功能，然後重新執行Exchange 2010安裝程式。

安裝 Windows 程序啟用服務-使用 \[伺服器管理員工具的程序模型功能

1.  按一下 \[**開始\]**、 \[**系統管理工具\]**及 \[**伺服器管理員**。

2.  在左側的導覽窗格中，以滑鼠右鍵按一下**功能**和 \[**新增功能\]**。

3.  在 \[**選取功能**窗格中，捲動到**Windows 程序啟動服務**。

4.  選取核取方塊的**程序模型**。

5.  從 \[**選取功能**\] 窗格中，按一下 \[**下一步**\] 和 \[**安裝**在 \[**確認安裝選項**\] 窗格。

6.  按一下 \[**關閉**保留 \[新增角色服務精靈\]。

