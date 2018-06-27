---
title: '必須是 updated_LocalDomainPrep 本機網域: Exchange 2013 Help'
TOCTitle: 必須是 updated_LocalDomainPrep 本機網域
ms:assetid: f33e6785-e85a-495e-a124-ebcb2b763e75
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.localdomainprep(v=EXCHG.150)
ms:contentKeyID: 50474578
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 必須是 updated\_LocalDomainPrep 本機網域

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2016-12-09_

此主題中的內容尚未針對 Microsoft Exchange Server 2013 進行更新。在更新之前，可能還是適用於 Exchange 2013。如果您仍然需要幫助，請查看下方的社群資源。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft Exchange Server 2007 安裝程式無法繼續因為沒有無法登入的使用者帳戶所需的網域準備作業的權限。

Exchange 安裝程式需要時執行**Setup /PrepareDomain**登入的使用者是網域系統管理員及 Exchange 組織系統管理員群組或 Enterprise Admins 群組的成員。

要解決這個問題，授予登入使用者以 Domain Admins 和 Exchange 組織系統管理員權限、 Enterprise Admins 群組中，將其註冊或登入帳戶擁有這些權限並重新執行 Exchange 2007 的安裝程式。

如需與 Microsoft Exchange 所需的 Active Directory 權限的詳細資訊，請參閱 「 使用與 Active Directory 權限在 Exchange 伺服器 」 ([https://go.microsoft.com/fwlink/?LinkId=47592](https://go.microsoft.com/fwlink/?linkid=47592))。

