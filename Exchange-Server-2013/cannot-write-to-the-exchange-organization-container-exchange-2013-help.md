---
title: '無法寫入至 Exchange 組織容器: Exchange 2013 Help'
TOCTitle: 無法寫入至 Exchange 組織容器
ms:assetid: 17c4667b-7db1-4e0a-b824-1f6d51d980a9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.globalserverinstall(v=EXCHG.150)
ms:contentKeyID: 50472703
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 無法寫入至 Exchange 組織容器

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2014-11-05_

安裝程式無法繼續 Microsoft Exchange Server 2013因為已登入使用者沒有寫入至 Active Directory 目錄服務中容器的組織所需的帳戶權限。

安裝程式要求在 Exchange 2013 安裝時，登入的使用者需擁有建立並修改 Active Directory 中物件的權限。若您第一次在組織中執行 Exchange 2013 安裝程式，您使用的帳戶需為 Schema Admins 與 Enterprise Admins 群組中的成員。需要這些權限的原因為，需在首次執行安裝程式時備妥 Exchange 2013 的 Active Directory。在 Active Directory 備妥後，您用於安裝額外 Exchange 2013 伺服器的帳戶需為 Organization Management 管理角色群組的成員。

若要解決此問題，請授與登入的使用者正確權限，或是使用具有那些權限的帳戶登入，然後重新執行 Exchange 2013 安裝程式。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>不支援 Exchange 2013 的跨樹系安裝。請使用您要在其中安裝 Exchange 2013 之 Active Directory 樹系的成員帳戶。</td>
</tr>
</tbody>
</table>


有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

找到您要的資訊了嗎？請撥冗[提供您的意見](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac)讓我們知道您需要什麼資訊。

