---
title: '未偵測到本機 site_ClientAccessRoleNotPresentInSite 的用戶端存取角色: Exchange 2013 Help'
TOCTitle: 未偵測到本機 site_ClientAccessRoleNotPresentInSite 的用戶端存取角色
ms:assetid: b5bfc6af-9c55-46c0-a293-6078b64e87dd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.clientaccessrolenotpresentinsite(v=EXCHG.150)
ms:contentKeyID: 50474065
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 未偵測到本機 site\_ClientAccessRoleNotPresentInSite 的用戶端存取角色

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2012-06-05_

此主題中的內容尚未針對 Microsoft Exchange Server 2013 進行更新。在更新之前，可能還是適用於 Exchange 2013。如果您仍然需要幫助，請查看下方的社群資源。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

因為本機 Active Directory® 目錄服務網站中偵測不到現有的用戶端存取角色 Microsoft® Exchange Server 2007 安裝程式會顯示這個警告。

您選擇要安裝之前的執行個體的用戶端存取角色的角色安裝在 Active Directory 站台信箱伺服器。

用戶端存取伺服器角色會接受來自各種不同的用戶端到您的 Exchange 2007 伺服器的連線。例如 Microsoft Outlook Express 和 Eudora 軟體用戶端使用 POP3 或 IMAP4 連線與 Exchange 伺服器進行通訊。硬體的用戶端，例如行動裝置會使用 ActiveSync、 POP3 或 IMAP4 與 Exchange 伺服器進行通訊。

如果使用者使用 Microsoft Office Outlook® 以外的任何用戶端存取其收件匣，您必須部署 Exchange 組織中安裝的用戶端存取伺服器角色。

使用者將能夠登入至 outlook 信箱，但是不能使用 Outlook Web Access 或行動裝置對相同的信箱直到出現在本機 Active Directory 站台的用戶端存取角色。

