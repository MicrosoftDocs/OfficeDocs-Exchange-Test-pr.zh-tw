---
title: '移除角色範圍: Exchange 2013 Help'
TOCTitle: 移除角色範圍
ms:assetid: ad17cba0-a8d3-4f40-b3c9-c37e6e5c3f36
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd351051(v=EXCHG.150)
ms:contentKeyID: 50473956
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 移除角色範圍

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-02_

管理角色範圍決定哪些物件會對可用的使用者，然後變更使用的指令程式和參數指派給使用者的物件。如果您不再使用的範圍，您可以予以移除。如需 Microsoft Exchange Server 2013中的管理角色範圍的詳細資訊，請參閱[了解管理角色範圍](understanding-management-role-scopes-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [角色管理權限](role-management-permissions-exchange-2013-help.md)主題中的「管理範圍」項目。

  - 您必須使用命令介面來執行這些程序。

  - 您可以移除範圍之前，您必須移除範圍從可能會使用它的任何管理角色指派。如需如何移除角色指派的範圍的詳細資訊，請參閱[變更角色指派](change-a-role-assignment-exchange-2013-help.md)。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 使用命令介面來移除範圍

若要移除範圍，請使用下列語法。

    Remove-ManagementScope <scope name>

例如，若要移除「Dublin Servers」範圍，請使用下列命令。

    Remove-ManagementScope "Dublin Servers"

