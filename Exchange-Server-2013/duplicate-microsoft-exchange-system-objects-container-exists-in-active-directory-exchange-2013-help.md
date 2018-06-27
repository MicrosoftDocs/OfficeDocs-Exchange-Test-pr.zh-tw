---
title: '在 Active Directory 中存在重複的 Microsoft Exchange 系統物件容器: Exchange 2013 Help'
TOCTitle: 在 Active Directory 中存在重複的 Microsoft Exchange 系統物件容器
ms:assetid: cd0f45ab-89de-4653-b50d-c1157c2329d5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.adiniterrorrule(v=EXCHG.150)
ms:contentKeyID: 50474272
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 在 Active Directory 中存在重複的 Microsoft Exchange 系統物件容器

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2013-02-18_

Microsoft Exchange Server 2013安裝程式無法繼續因為它找到重複的 Microsoft Exchange 系統物件容器中的 Active Directory 網域命名內容\]。當安裝程式會找出重複的 Microsoft Exchange 系統物件容器時，您必須刪除重複容器才可以繼續安裝程式。當存在重複的 Microsoft Exchange 系統物件容器中時，您無法再次執行**DomainPrep**來解決問題。您必須找出並刪除重複的 Microsoft Exchange 系統物件容器。

若要解決這個問題，請執行下列動作：

1.  使用系統管理認證登入網域控制站

2.  在 **\[系統管理工具\]** 中，按一下 **\[Active Directory 使用者和電腦\]**。

3.  在 **\[Active Directory 使用者和電腦\]** 管理主控台窗格中，按一下位於工具列功能表中的 **\[檢視\]**，然後選取 **\[進階功能\]**。

4.  找出重複的 Microsoft Exchange 系統物件容器。

5.  確認重複的 Microsoft Exchange 系統物件容器未包含有效的 Active Directory 物件。

6.  以滑鼠右鍵按一下重複的 Microsoft Exchange 系統物件容器，然後按一下 **\[刪除\]**。

7.  在 Active Directory 對話方塊中按一下 \[是\]，確認刪除。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您要立即複寫變更，則必須手動初始化網域控制站之間的複寫。</td>
</tr>
</tbody>
</table>


有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

找到您要的資訊了嗎？請撥冗[提供您的意見](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac)讓我們知道您需要什麼資訊。

