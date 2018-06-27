---
title: '若要準備 Active Directory_DomainPrepWithoutADUpdate 的權限不足: Exchange 2013 Help'
TOCTitle: 若要準備 Active Directory_DomainPrepWithoutADUpdate 的權限不足
ms:assetid: 4283c4b9-983f-460e-a5de-42b2772eae0d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.domainprepwithoutadupdate(v=EXCHG.150)
ms:contentKeyID: 50473115
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 若要準備 Active Directory\_DomainPrepWithoutADUpdate 的權限不足

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2016-12-09_

此主題中的內容尚未針對 Microsoft Exchange Server 2013 進行更新。在更新之前，可能還是適用於 Exchange 2013。如果您仍然需要幫助，請查看下方的社群資源。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft Exchange Server 2007 安裝程式無法繼續因為嘗試的網域準備作業失敗。

Exchange 安裝程式需要 Active Directory 目錄服務要修改的 Exchange Server 2007 之前可以準備 Active Directory 中的網域。

要用來執行**setup /PrepareAD**命令的帳戶已執行此命令即使它看起來屬於 Enterprise Admins 群組的權限不足。帳戶可能已經過期。

若要解決此問題，確認已登入使用者帳戶皆有效且屬於 Enterprise Admins 群組或記錄檔在一起擁有這些權限並重新執行**setup /PrepareAD**的帳戶。

如需如何執行 PrepareAD 程序的詳細資訊，查看 」 如何至準備 Active Directory 及網域 」 ([https://go.microsoft.com/fwlink/?LinkId=78453](https://go.microsoft.com/fwlink/?linkid=78453))。

如需與 Microsoft Exchange 所需的 Active Directory 權限的詳細資訊，請參閱 「 使用與 Active Directory 權限在 Exchange 伺服器 」 ([https://go.microsoft.com/fwlink/?LinkId=47592](https://go.microsoft.com/fwlink/?linkid=47592))。

