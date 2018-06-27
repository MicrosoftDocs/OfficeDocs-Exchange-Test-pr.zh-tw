---
title: 'IIS 6 相容性元件不 installed_LonghornIIS6MgmtConsoleNotInstalled: Exchange 2013 Help'
TOCTitle: IIS 6 相容性元件不 installed_LonghornIIS6MgmtConsoleNotInstalled
ms:assetid: 8358eafb-def7-4b8d-8fe1-623bc5a0e20e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.longhorniis6mgmtconsolenotinstalled(v=EXCHG.150)
ms:contentKeyID: 50473670
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# IIS 6 相容性元件不 installed\_LonghornIIS6MgmtConsoleNotInstalled

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2012-06-05_

此主題中的內容尚未針對 Microsoft Exchange Server 2013 進行更新。在更新之前，可能還是適用於 Exchange 2013。如果您仍然需要幫助，請查看下方的社群資源。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft®Exchange Server 2007 安裝程式無法繼續嘗試下列 Windows 作業系統上安裝 Client Access Server 的伺服器角色、 信箱伺服器角色或 Exchange 2007 系統管理工具：

  - Windows Server 2008 R2

  - Windows Server 2008

  - Windows 7 （僅限系統管理工具）

  - Windows Vista （僅限系統管理工具）

因為未安裝 Internet Information Server (IIS) 6 Metabase 相容性元件及 IIS 6 管理主控台元件會發生此問題。

Exchange 2007 的安裝程式需要您在安裝 Exchange 2007 用戶端存取伺服器角色、 信箱伺服器角色或 Exchange 2007 系統管理工具的電腦具有 \[IIS 6 Metabase 相容性元件和安裝 IIS 6 管理主控台元件。

若要解決這個問題、 目的地電腦上安裝 IIS 6 Metabase 相容性元件，然後重新執行 Microsoft Exchange 安裝程式。

使用 \[伺服器管理員工具在 Windows Server 2008 R2 或 Windows Server 安裝 IIS 6.0 管理相容性元件

1.  依序按一下 \[開始\]、\[系統管理工具\] 及 \[伺服器管理員\]。

2.  在功能窗格\] 中展開 \[**角色**、**網頁伺服器 (IIS)**\] 上按一下滑鼠右鍵並再按一下 \[**新增角色服務**。

3.  在 \[**選取角色服務**\] 窗格中，捲動至**IIS 6 管理相容性**。

4.  按一下以選取 \[ **IIS 6 Metabase 相容性**、 **IIS 6 WMI 相容性**、 及**IIS 6 管理主控台**\] 核取方塊。

5.  在 \[**選取角色服務**\] 窗格中，按一下 \[**下一步**\]。

6.  在 \[**確認安裝選項**\] 窗格中，按一下 \[**安裝**\]。

7.  按一下 \[**關閉**結束 \[新增角色服務精靈\]。

從 \[控制台\] 的 Windows Vista 或 Windows 7 中安裝 IIS 6.0 管理相容性元件

1.  按一下 \[**開始\]**、 \[**控制台\]**、 按一下 \[**程式和功能**\] 和 \[**開啟或關閉 Windows 功能**。

2.  開啟 \[**網際網路資訊服務**\]。

3.  開啟**Web 管理工具**。

4.  開啟 \[ **IIS 6.0 管理相容性**\]。

5.  按一下以選取 \[ **IIS 6 Metabase 及 IIS 6 設定相容性**、 **IIS 6 WMI 相容性**、 及**IIS 6 管理主控台**\] 核取方塊。

6.  按一下 **\[確定\]**。

