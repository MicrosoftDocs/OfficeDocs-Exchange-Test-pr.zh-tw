---
title: 'Active Directory 分割權限 不支援的網域控制站上安裝: Exchange 2013 Help'
TOCTitle: Active Directory 分割權限 不支援的網域控制站上安裝
ms:assetid: 977e3758-5e09-40a2-80c1-fe344b1d8a2a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.installondcinadsplitpermissionmode(v=EXCHG.150)
ms:contentKeyID: 50473782
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Active Directory 分割權限 不支援的網域控制站上安裝

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2012-11-12_

Microsoft Exchange Server 2013安裝程式偵測到您嘗試在 Active Directory 網域控制站上執行安裝程式與下列其中一項為真：

  - 部署 Exchange 組織已設定的 Active Directory 分割權限。

  - 選取 \[將 Active Directory 分割Exchange 2013安裝程式中的 \[權限\] 選項。

設定 Exchange 組織的 Active Directory 分割權限時不支援Exchange 2013網域控制站上的安裝。

如果您想要在網域控制站上安裝Exchange 2013 ，您必須設定 Exchange 組織的角色型存取控制 (RBAC) 分割權限或共用的權限。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>我們不建議在 Active Directory 網域控制站上安裝Exchange 2013 。如需詳細資訊，請參閱<a href="installing-exchange-on-a-domain-controller-is-not-recommended-exchange-2013-help.md">在網域控制站上安裝 Exchange 不建議使用</a>。</td>
</tr>
</tbody>
</table>


如果您想要繼續使用 Active Directory 分割權限，您必須安裝Exchange 2013成員伺服器。

如需分割和Exchange 2013中的共用權限的詳細資訊，請參閱下列主題：

[了解分割權限](understanding-split-permissions-exchange-2013-help.md)

[設定 Exchange 2013 分割權限](configure-exchange-2013-for-split-permissions-exchange-2013-help.md)

[如需共用權限設定 Exchange 2013](configure-exchange-2013-for-shared-permissions-exchange-2013-help.md)

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

找到您要的資訊了嗎？請撥冗[提供您的意見](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac)讓我們知道您需要什麼資訊。

