---
title: '若要執行 /PrepareDomain_PrepareDomainNotAdmin 的權限不足: Exchange 2013 Help'
TOCTitle: 若要執行 /PrepareDomain_PrepareDomainNotAdmin 的權限不足
ms:assetid: c33a2bc0-5b07-49b8-a1c1-53baa4933d44
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.preparedomainnotadmin(v=EXCHG.150)
ms:contentKeyID: 50474133
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 若要執行 /PrepareDomain\_PrepareDomainNotAdmin 的權限不足

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2016-12-09_

此主題中的內容尚未針對 Microsoft Exchange Server 2013 進行更新。在更新之前，可能還是適用於 Exchange 2013。如果您仍然需要幫助，請查看下方的社群資源。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft Exchange Server 2007 安裝程式無法繼續因為嘗試執行**/PrepareDomain**程序失敗。登入使用者具有執行**/PrepareDomain**程序的權限不足。

Exchange 2007 的安裝程式會要求執行**/PrepareDomain**程序時登入的使用者必須要準備之網域的 Domain Admins 群組的成員，以及 Enterprise Admins 群組的成員。

若要解決此問題，授與登入使用者 Domain Admins 做準備之網域的權限群組及註冊它們在 Enterprise Admins 群組中，或使用這些權限並重新執行 Exchange 2007 的安裝程式的帳戶登入。

如需與 Microsoft Exchange 所需的 Active Directory 權限的詳細資訊，請參閱 「 使用與 Active Directory 權限在 Exchange 伺服器 」 ([https://go.microsoft.com/fwlink/?LinkId=47592](https://go.microsoft.com/fwlink/?linkid=47592))。

