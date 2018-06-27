---
title: '通訊群組命名原則會覆寫: Exchange Online Help'
TOCTitle: 通訊群組命名原則會覆寫
ms:assetid: 9eb23fc9-3f59-4d09-9077-85c89a051ee0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ218685(v=EXCHG.150)
ms:contentKeyID: 50472345
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 通訊群組命名原則會覆寫

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2012-10-13_

群組的通訊群組命名原則只會套用到使用者所建立的群組。當您或其他管理員使用 Exchange 系統管理中心 (EAC) 來建立通訊群組時、 群組命名原則會忽略並不會套用到的群組名稱。

不過，如果您使用 Exchange 管理命令介面來建立或重新命名通訊群組，除非使用 *IgnoreNamingPolicy* 參數覆寫群組命名原則，否則群組命名原則會套用至系統管理員所建立的群組。

## 開始之前有哪些須知？

  - 預估完成時間： 2 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「通訊群組」項目。

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

## 使用命令介面在您建立新的群組時覆寫群組命名原則

若要複寫群組命名原則，請執行以下命令。

    New-DistributionGroup -Name <Group Name> -IgnoreNamingPolicy

例如，如果組織的群組命名原則是**DG\_\<Group Name\>\_Users**，請執行下列命令建立名為 **All Administrators** 的群組。

    New-DistributionGroup -Name "All Administrators" -IgnoreNamingPolicy

當 Microsoft Exchange 建立此群組時，它會將 **All Administrators** 同時用於 *Name* 和 *DisplayName* 參數。

## 使用命令介面在您重新命名群組時覆寫群組命名原則

若要在命令介面中重新命名現有群組時覆寫群組命名原則，請執行下列命令：

    Set-DistributionGroup -Identity <Old Group Name> -Name <New Group Name> -DisplayName <New Group Name> -IgnoreNamingPolicy

例如，假設您建立群組命名原則落後一個夜間與您下一步早上實現拼錯的前置字中的文字字串。下一個晨曦 」，您會看到新的群組已建立與拼錯的字首。您可以修正群組命名原則在 EAC 中，但是您必須使用命令介面來重新命名群組拼錯的名稱。執行下列命令。

    Set-DistributionGroup -Identity "Goverment_Contracts_NWRegion" -Name "Government_ContractEstimates_NWRegion" -DisplayName "Government_ContractEstimates_NWRegion" -IgnoreNamingPolicy

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>請務必包含<em>DisplayName</em>參數時重新命名群組。如果您不要的舊名稱仍會顯示在 [收件者共用的通訊錄中:、 [副本 ︰，以及從 ︰ 電子郵件訊息中的行。</td>
</tr>
</tbody>
</table>


## 如何才能了解這是否正常運作？

若要驗證您是否已成功建立或重新命令忽略了群組命名原則之通訊群組，請執行下列命令。

    Get-DistributionGroup <Name> | FL DisplayName

    Get-OrganizationConfig | FL DistributionGroupNamingPolicy

如果群組的顯示名稱格式與組織的群組命名原則強制提供的顯示名稱格式不同，表示設定成功。

