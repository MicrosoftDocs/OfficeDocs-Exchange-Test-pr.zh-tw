---
title: '仍 installed_SMTPSvcInstalled 簡易郵件傳輸通訊協定。: Exchange 2013 Help'
TOCTitle: 仍 installed_SMTPSvcInstalled 簡易郵件傳輸通訊協定。
ms:assetid: f786a93c-876d-4f4e-adb6-4dfea3d820d1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.smtpsvcinstalled(v=EXCHG.150)
ms:contentKeyID: 50474618
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 仍 installed\_SMTPSvcInstalled 簡易郵件傳輸通訊協定。

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2012-06-05_

此主題中的內容尚未針對 Microsoft Exchange Server 2013 進行更新。在更新之前，可能還是適用於 Exchange 2013。如果您仍然需要幫助，請查看下方的社群資源。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft® Exchange Server 2007 安裝程式無法繼續因為在這部電腦上安裝 Microsoft Windows Server™ 2003年簡易郵件傳送通訊協定 (SMTP) 服務。

Microsoft Exchange 安裝程式需要用於 Exchange 2007 伺服器上未安裝 SMTP 服務。

若要解決此問題，請解除安裝 SMTP 服務並重新執行 Microsoft Exchange 安裝程式。

若要使用新增解除安裝 SMTP 服務或在 \[控制台\] 中移除 Windows 元件

1.  在 \[開始\] 功能表上，按一下 \[控制台\]。

2.  按兩下 \[新增或移除程式\]。

3.  按一下 \[**新增/移除 Windows 元件**\]。

4.  \[**元件**\] 清單中選取**應用程式伺服器**\] 核取方塊和 \[**詳細資料**。

5.  選取 \[**網際網路資訊服務管理員**和 \[**詳細資料**。

6.  選取 \[ **SMTP Service** \] 和 \[清除\] 核取方塊。

7.  按兩次**\[確定\]**返回 \[**元件**\] 清單，然後按 \[**下一步**。

8.  解除安裝 SMTP 服務時按一下 \[**完成**\]。

