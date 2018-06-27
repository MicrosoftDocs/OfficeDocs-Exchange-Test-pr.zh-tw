---
title: '移除所有的伺服器 roles_CannotUninstallDelegatedServer 的權限不足: Exchange 2013 Help'
TOCTitle: 移除所有的伺服器 roles_CannotUninstallDelegatedServer 的權限不足
ms:assetid: 214ae6f3-15e7-4337-99e8-40f9547c8e0c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.cannotuninstalldelegatedserver(v=EXCHG.150)
ms:contentKeyID: 50472810
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 移除所有的伺服器 roles\_CannotUninstallDelegatedServer 的權限不足

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2016-12-09_

此主題中的內容尚未針對 Microsoft Exchange Server 2013 進行更新。在更新之前，可能還是適用於 Exchange 2013。如果您仍然需要幫助，請查看下方的社群資源。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft Exchange Server 2007 安裝程式無法繼續因為嘗試解除安裝所有伺服器角色失敗。

Exchange 2007 的安裝程式需要解除安裝所有伺服器角色時登入的使用者是 Exchange 組織系統管理員群組或 Enterprise Admins 群組的成員。

若要解決這個問題，授與登入使用者的 Exchange 組織系統管理員權限或其註冊 Enterprise Admins 群組中，或使用具有這些權限的帳戶登入並重新執行 Exchange 2007 的安裝程式。

如需與 Microsoft Exchange 的 Active Directory 權限的詳細資訊，請參閱 ＜ 」 工作與 Active Directory 權限在 Exchange 伺服器 」 ([https://go.microsoft.com/fwlink/?LinkId=47592](https://go.microsoft.com/fwlink/?linkid=47592))。

