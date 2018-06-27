---
title: 'Exchange 中指派 eDiscovery 權限: Exchange Online Help'
TOCTitle: Exchange 中指派 eDiscovery 權限
ms:assetid: 729e09d8-614b-431f-ae04-ae41fb4c628e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd298059(v=EXCHG.150)
ms:contentKeyID: 50473480
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 中指派 eDiscovery 權限

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2014-10-02_

如果您想讓使用者能夠使用 Microsoft Exchange Server 2013就地 eDiscovery，必須先將其授權透過將它們新增至探索管理角色群組。探索管理角色群組的成員有Exchange安裝程式會建立探索信箱的完整存取信箱權限。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>探索管理角色群組的成員可存取機密訊息內容。主要是針對這些成員可以使用<a href="in-place-ediscovery-exchange-2013-help.md">就地 eDiscovery</a>搜尋所有信箱在 Exchange 組織、 預覽郵件 （和其他信箱項目）、 將其複製到探索信箱並複製的郵件匯出至.pst 檔案。在大多數的組織，此權限會授與法律、 規範、 或人力資源人員。<br />
</td>
</tr>
</tbody>
</table>


若要深入了解 「 探索管理角色群組，請參閱[探索管理](discovery-management-exchange-2013-help.md)。若要深入了解角色存取控制 (RBAC)，請參閱[了解角色型存取控制](understanding-role-based-access-control-exchange-2013-help.md)。

對於案例感興趣一角與使用此程序？請參閱下列主題：

  - [建立就地 eDiscovery 搜尋](create-an-in-place-ediscovery-search-exchange-2013-help.md)

  - [建立或移除就地保留](create-or-remove-an-in-place-hold-exchange-2013-help.md)

## 開始之前有哪些須知？

  - 預估完成時間： 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [角色管理權限](role-management-permissions-exchange-2013-help.md)主題中的 「 角色群組 」 項目。

  - 根據預設， 探索管理角色群組不包含任何成員。與組織管理角色的系統管理員也包含無法建立或探索搜尋管理不被新增至探索管理角色群組。

  - 在Exchange 2013、 組織管理角色群組的成員可以建立[就地保留與訴訟暫止](in-place-hold-and-litigation-hold-exchange-2013-help.md)保留上放置信箱的所有內容。不過，若要建立查詢式就地保留功能，使用者必須探索管理角色群組的成員或具有信箱搜尋角色指派。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

## 使用 EAC 來將使用者新增至探索管理角色群組

1.  移至 \[**權限**\>**系統管理員角色**。

2.  在清單檢視中，選取 \[**探索管理**和 \[**編輯**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")

3.  在**角色群組**中的 \[**成員**、 按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

4.  在 \[**選取成員\]**中，選取一或多個使用者、 按一下 \[**新增**\] 及 \[**確定\]**。

5.  在**角色群組**中，按一下 \[**儲存**\]。

## 使用命令介面將使用者新增至探索管理角色群組

本範例會將使用者 Bsuneja 新增至探索管理角色群組。

    Add-RoleGroupMember -Identity "Discovery Management" -Member Bsuneja

如需詳細的語法及參數資訊，請參閱 [Add-RoleGroupMember](https://technet.microsoft.com/zh-tw/library/dd638207\(v=exchg.150\))。

## 如何知道這是否正常運作？

若要確認您是否已新增使用者至探索管理角色群組，請執行下列動作：

1.  在 EAC 中，移至 \[**權限**\>**系統管理員角色**。

2.  在清單檢視中，選取 \[**探索管理**。

3.  在 \[詳細資料\] 窗格中，確認使用者已列於 \[**成員**\] 底下。

您也可以執行此命令以列出探索管理角色群組的成員。

    Get-RoleGroupMember -Identity "Discovery Management"

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

