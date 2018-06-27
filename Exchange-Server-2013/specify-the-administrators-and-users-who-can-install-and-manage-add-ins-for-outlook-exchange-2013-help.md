---
title: '指定系統管理員和使用者可安裝和管理適用於 Outlook 增益集: Exchange Online Help'
TOCTitle: 指定系統管理員和使用者可安裝和管理適用於 Outlook 增益集
ms:assetid: 7ee4302d-b8bb-40a0-9810-10d3a0271bcb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ943754(v=EXCHG.150)
ms:contentKeyID: 52062562
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 指定系統管理員和使用者可安裝和管理適用於 Outlook 增益集

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2017-02-08_

您可以指定哪些系統管理員在組織中的已安裝和管理適用於 Outlook 增益集的權限。您也可以指定哪些使用者在組織中的已安裝和管理自己使用的增益集的權限。

做法是指派或移除增益集的特定的管理角色。有五個您可以使用的內建角色。

系統管理角色

  - **Org 市集應用程式**  可讓管理員能夠安裝及管理增益集所能使用來自 Office 市集的組織。

  - **Org 自訂應用程式**  可讓管理員能夠安裝及管理自訂增益集的組織。

使用者角色

  - **我市集應用程式**  可讓使用者安裝及管理 Office 市集的增益集自己使用。

  - **「 我的自訂應用程式**  可讓使用者安裝和管理自訂增益集供自己使用。

  - **我 ReadWriteMailbox 應用程式**  可讓使用者安裝和管理增益集，要求在其資訊清單中的 ReadWriteMailbox 權限層級。

根據預設，所有系統管理員**組織管理**角色群組擁有兩個以上的管理角色啟用。也根據預設，使用者可以啟用上述使用者角色。

如需這些角色的資訊，請參閱[Org 市集應用程式角色](org-marketplace-apps-role-exchange-2013-help.md)、 [Org 自訂應用程式角色](org-custom-apps-role-exchange-2013-help.md)、 [我市集應用程式的角色](my-marketplace-apps-role-exchange-2013-help.md)、 [我自訂應用程式的角色](my-custom-apps-role-exchange-2013-help.md)及[我 ReadWriteMailbox 應用程式的角色](my-readwritemailbox-apps-role-exchange-2013-help.md)。

如需增益集的資訊，請參閱[適用於 Outlook 的應用程式](add-ins-for-outlook-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此指令程式。雖然這個指令程式的所有參數都已列於本主題中，不過，如果某些參數並未包含在指派給您的權限中，您可能就無法存取這些參數。若要查看您需要的權限，請參閱 [角色管理權限](role-management-permissions-exchange-2013-help.md)主題中的 「 角色指派 」 項目。

  - 存取 Office 存放區不支援信箱或組織中特定區域 （英文）。如果您沒有看到**新增來自 Office 市集Exchange 系統管理中心**底下**組織**中的選項 \>**增益集**\> ![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")，您可以從 URL 或檔案的位置的 outlook 安裝增益集。如需詳細資訊，請連絡您的服務提供者。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 您要執行的工作

## 指派管理員安裝及管理組織的增益集所需的權限

## 使用 EAC 指派權限給系統管理員

您可以使用 EAC 來指派安裝和管理增益集也可用來自 Office 市集的組織所需的權限的管理員。如需如何執行這項作業的詳細資訊，請參閱[管理角色群組](manage-role-groups-exchange-2013-help.md)。

## 將使用者指派至安裝和管理自己使用的增益集所需的權限

## 使用 EAC 指派權限給使用者

您可以使用 EAC 來將使用者指派至檢視和修改自訂增益集供自己使用所需的權限。如需如何執行這項作業的詳細資訊，請參閱[管理角色群組](manage-role-groups-exchange-2013-help.md)。

## 如何才能了解這是否正常運作？

若要驗證您已成功指派給使用者的權限，請執行採用 `Get-ManagementRoleAssignment -Role <Role Name> -GetEffectiveUsers` 格式的命令介面命令，其中 `Role Name` 是您要驗證受指派權限的角色。

本範例會顯示如何確認您是否已指派其安裝的增益集來自 Office 市集的組織權限。

1.  執行 `Get-ManagementRoleAssignment -Role "Org Marketplace Apps" -GetEffectiveUsers`。

2.  在結果中，檢閱 **\[有效使用者\]** 欄中的項目。

如需語法及參數的相關資訊，請參閱 [Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd351024\(v=exchg.150\))。

