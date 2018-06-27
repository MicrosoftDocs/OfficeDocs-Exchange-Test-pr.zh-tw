---
title: '管理角色群組成員: Exchange 2013 Help'
TOCTitle: 管理角色群組成員
ms:assetid: c064729d-7cda-47fc-b105-acf4b300d430
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ657492(v=EXCHG.150)
ms:contentKeyID: 50474177
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理角色群組成員

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2012-10-08_

本主題顯示如何新增、 移除及檢視 Microsoft Exchange Server 2013中的管理角色群組的成員。如需Exchange 2013中的角色群組的詳細資訊，請參閱[了解管理角色群組](understanding-management-role-groups-exchange-2013-help.md)。

若欲瞭解更多與角色群組相關的管理工作，請參閱 [權限](permissions-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [角色管理權限](role-management-permissions-exchange-2013-help.md)主題中的「角色群組」項目。

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


## 您要執行的工作

## 將成員新增至角色群組

若要授與使用者由角色群組所授與的權限，您需要將該使用者、萬用安全性群組 (USG) 或該使用者為其成員的其他角色群組，新增為該角色群組的成員。

## 使用 EAC 將成員新增至角色群組

1.  在 Exchange 系統管理中心 (EAC) 中，導覽至 \[權限\] \> \[管理員角色\]。

2.  選取要新增成員的角色群組，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[成員\] 區段上，按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

4.  選取要新增至該角色群組的使用者、USG 或其他角色群組，按一下 \[新增\]，然後按一下 \[確定\]。

5.  按一下 \[儲存\]，將變更儲存到角色群組。

## 使用命令介面將成員新增至角色群組

若要新增角色群組成員，請參閱 [Add-RoleGroupMember](https://technet.microsoft.com/zh-tw/library/dd638207\(v=exchg.150\)) 中的[Examples](https://technet.microsoft.com/zh-tw/dd638207\(exchg.150\)#examples)區段。

若要新增多個角色群組成員或完全取代角色群組成員資格，請參閱 [Update-RoleGroupMember](https://technet.microsoft.com/zh-tw/library/dd638116\(v=exchg.150\)) 中的[Examples](https://technet.microsoft.com/zh-tw/dd638116\(exchg.150\)#examples)區段。

## 如何才能了解這是否正常運作？

若要確認是否已成功將一或多個成員新增至角色群組，請執行下列操作：

1.  在 EAC 中，瀏覽至 \[權限\] \> \[管理員角色\]。

2.  選取您在其中新增成員的角色群組。

3.  在角色群組詳細資料窗格中，確認您新增的成員已列出。

## 移除角色群組的成員

若要移除使用者透過角色群組所授與的權限，您必須從角色群組的成員資格中移除使用者，或使用者所屬的萬用安全性群組 (USG)。

## 使用 EAC 從角色群組中移除成員

1.  在 EAC 中，瀏覽至 \[權限\] \> \[管理員角色\]。

2.  選取要從中移除成員的角色群組，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[成員\] 區段中，選取您要移除的成員，按一下 \[移除\]![\[移除\] 圖示](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[移除] 圖示")，然後按一下 \[儲存\]。

## 使用命令介面從角色群組中移除成員

若要移除角色群組成員，請參閱 [Remove-RoleGroupMember](https://technet.microsoft.com/zh-tw/library/dd638208\(v=exchg.150\)) 中的[Examples](https://technet.microsoft.com/zh-tw/dd638208\(exchg.150\)#examples)區段。

若要移除多個角色群組成員或完全取代角色群組成員資格，請參閱 [Update-RoleGroupMember](https://technet.microsoft.com/zh-tw/library/dd638116\(v=exchg.150\)) 中的[Examples](https://technet.microsoft.com/zh-tw/dd638116\(exchg.150\)#examples)區段。

## 如何才能了解這是否正常運作？

若要確認是否已成功移除角色群組中的一或多個成員，請執行下列操作：

1.  在 EAC 中，瀏覽至 \[權限\] \> \[管理員角色\]。

2.  選取您已移除其中成員的角色群組。

3.  在角色群組詳細資料窗格中，確認不再列出您移除的成員。

## 檢視角色群組的成員

提供管理角色指派給角色群組的權限會授與角色群組的成員。您可以檢視依您指定的角色群組以查看哪些使用者、 萬用安全性群組 (USG) 或其他角色群組會授與權限角色群組的成員。

## 使用 EAC 檢視角色群組的成員

1.  在 EAC 中，瀏覽至 \[權限\] \> \[管理員角色\]。

2.  選取您想要檢視其成員的角色群組。

3.  在角色群組詳細資料窗格中，檢視角色群組詳細資料窗格中的成員。

## 使用命令介面檢視角色群組的成員

若要檢視角色群組的成員，請參閱 [Get-RoleGroupMember](https://technet.microsoft.com/zh-tw/library/dd638093\(v=exchg.150\)) 中的＜範例＞一節。

