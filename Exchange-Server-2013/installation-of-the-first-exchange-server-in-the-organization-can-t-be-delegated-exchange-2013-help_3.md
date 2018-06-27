---
title: '安裝第一部 Exchange 組織中的伺服器無法受到委派: Exchange 2013 Help'
TOCTitle: 安裝第一部 Exchange 組織中的伺服器無法受到委派
ms:assetid: d451581b-6161-4e95-99f1-03dac8313fae
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.delegatedmailboxfirstinstall(v=EXCHG.150)
ms:contentKeyID: 50474327
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 安裝第一部 Exchange 組織中的伺服器無法受到委派

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2014-11-05_

因為登入的使用者沒有必要的帳戶權限，無法安裝組織中的第一台 Exchange 2013 伺服器，所以 Microsoft Exchange Server 2013 安裝程式無法繼續。

雖然 Exchange 2013 安裝程式允許使用委派來安裝後續的伺服器角色，但安裝程式要求在安裝組織中的第一台 Exchange 2013 伺服器時，登入使用者必須是 Enterprise Admins Windows 安全性群組的成員。這是因為 Exchange 2013 安裝程式在安裝期間需在 Active Directory 的 Exchange 組織容器中建立並設定物件。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若您先前尚未備妥 Exchange 2013 的 Active Directory 架構，則登入使用者也必須是 Schema Admins Windows 安全性群組的成員。或者，身為 Schema Admins Windows 群組成員的另一名使用者可以在安裝 Exchange 2013 前先備妥 Active Directory 架構。</td>
</tr>
</tbody>
</table>


若要解決此問題，請將登入使用者加入 Enterprise Admins 安全性群組。或是以 Enterprise Admins 安全性群組成員的帳戶登入。然後再次執行 Exchange 2013 安裝程式。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

找到您要的資訊了嗎？請撥冗[提供您的意見](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac)讓我們知道您需要什麼資訊。

