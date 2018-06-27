---
title: '建立角色: Exchange 2013 Help'
TOCTitle: 建立角色
ms:assetid: e614ad8f-5946-4135-b130-89ea626afcd4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd351214(v=EXCHG.150)
ms:contentKeyID: 50474470
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 建立角色

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-17_

您可以建立管理角色、 變更管理角色項目，則需要，然後將角色指派給角色受託人可將新增範圍。您應該幾乎不需要執行此程序。我們建議您檢查是否可以使用內建管理角色，而不是建立管理角色。如需內建管理角色的清單，請參閱[內建管理角色](built-in-management-roles-exchange-2013-help.md)。

如需 Microsoft Exchange Server 2013 中管理角色的相關資訊，請參閱[了解管理角色](understanding-management-roles-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>本主題不會討論如何建立未限定範圍的管理角色。如需如何建立未限定範圍的管理角色的資訊，請參閱<a href="create-an-unscoped-role-exchange-2013-help.md">建立未限定範圍的角色</a>。</td>
</tr>
</tbody>
</table>


要尋找與角色相關的其他管理工作嗎？請參閱[進階權限](advanced-permissions-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 此程序預估完成時間：10 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [角色管理權限](role-management-permissions-exchange-2013-help.md)主題中的「管理角色」項目。

  - 您必須使用命令介面來執行這些程序。

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


## 該怎麼做？

## 步驟 1： 建立管理角色

新的管理角色根據現有的角色。當您建立角色時，現有的角色和其管理角色項目都會複製到新的角色。現有的角色會成為新的子角色父。您必須一律選擇包含的所有 cmdlet 和參數則需要使用、 角色，然後移除您不想的過。子系角色不能有不存在於父系角色的管理角色項目。

使用下列語法建立新角色。

    New-ManagementRole -Parent <existing role to copy> -Name <name of new role>

此範例會將「郵件收件者」角色及其管理角色項目複製到「西雅圖收件者管理員」角色。

    New-ManagementRole -Parent "Mail Recipients" -Name "Seattle Mail Recipients"

如需詳細的語法及參數資訊，請參閱 [New-ManagementRole](https://technet.microsoft.com/zh-tw/library/dd298073\(v=exchg.150\))。

## 步驟 2： 變更新角色的管理角色項目

建立您的角色之後，您需要變更的角色項目。您可以移除整個角色項目，以完全移除相關聯的指令程式的存取。或者，您可以從來移除這些特定的參數相關聯的指令程式上存取的角色項目移除參數。

您無法新增新角色項目或參數角色項目上除非它們存在於父系角色。因為您只是從父系角色在步驟 1 中建立角色，所以您無法新增任何其他角色項目或參數角色項目上因為它們不存在於父系角色。

在變更角色的角色項目時，您可以進行下列其中一項動作：

  - 移除單一、整個角色項目。

  - 移除多個、整個角色項目。

  - 從角色項目移除參數。

若要從新角色移除角色項目，請參閱[從角色移除角色項目](remove-a-role-entry-from-a-role-exchange-2013-help.md)。

## 步驟 3： 建立自訂管理角色範圍，如有需要

管理角色範圍決定可讓使用者檢視或變更使用步驟 2 中所設定的角色項目使用的物件。新的管理角色會繼承讀取及寫入管理其父系角色的角色範圍。這些被呼叫*隱含的範圍*。不過，可能會想要變更寫入範圍以符合您的業務需求的新角色的情況。當您建立自訂範圍時，您覆寫隱含寫入範圍的角色。隱含讀取的範圍的角色不會變更。如需管理角色範圍的詳細資訊，請參閱[了解管理角色範圍](understanding-management-role-scopes-exchange-2013-help.md)。

您可以建立自訂範圍、 建立獨佔範圍、 使用預先定義的範圍或範圍指派給組織單位 (OU)。新的範圍必須是 「 角色隱含讀取範圍內。若要使用預先定義的範圍或指定組織單位，請跳至步驟 4。

若要將自訂範圍新增至新的角色，請參閱[建立規則或獨佔範圍](create-a-regular-or-exclusive-scope-exchange-2013-help.md)。

## 步驟 4： 將新的管理角色指派

建立與設定角色的最後一個步驟是將其指派給角色指派者。

當您建立角色指派時，可以選擇執行下列其中一個動作：

  - 建立沒有範圍的角色指派。

  - 使用預先定義的範圍建立角色指派。

  - 使用 OU 建立角色指派，但不使用網域限制篩選器。

  - 使用您在步驟 3 建立的自訂或獨佔範圍來建立角色指派。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>當您建立角色與管理角色指派原則之間的指派時，不能指定範圍。</td>
    </tr>
    </tbody>
    </table>


您可以將新的角色指派給角色群組、 角色指派原則、 使用者或萬用安全性群組 (USG)。如需詳細資訊，請參閱下列主題：

  - [管理角色群組](manage-role-groups-exchange-2013-help.md)

  - [管理角色指派原則](manage-role-assignment-policies-exchange-2013-help.md)

  - [將角色新增至使用者或 USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

