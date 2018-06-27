---
title: '移除組織關係: Exchange 2013 Help'
TOCTitle: 移除組織關係
ms:assetid: ff211394-f58b-4da7-bb3a-df6abcb5950e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ657513(v=EXCHG.150)
ms:contentKeyID: 50474667
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 移除組織關係

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-01-04_

組織關係可讓 Exchange 組織中的使用者將行事曆空閒/忙碌資訊與 Office 365 組織或其他 Exchange 內部部署組織共用。您可以移除組織關係，以停用與其他組織的行事曆共用。

您可以與其他組織共用行事曆之前，您都必須設定與Azure Active Directory驗證系統 （又稱為 「 同盟 」） 的驗證關係及必須符合最低軟體需求。若要深入了解同盟共用，請參閱[共用](sharing-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「行事曆和共用權限」一節。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

## 您要執行的工作

## 使用 EAC 移除組織關係

1.  在內部部署組織中的 Exchange 2013 伺服器上，瀏覽至 \[組織\] \> \[共用\]。

2.  在 \[組織共用\] 下選取組織關係，然後按一下 \[刪除\]![刪除圖示](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "刪除圖示")，移除組織關係。

3.  在出現的警告中，按一下 \[是\]。

## 使用命令介面移除組織關係

此範例會從 Exchange 組織移除組織關係 Contoso

    Remove-OrganizationRelationship -Identity "Contoso"

如需詳細的語法及參數資訊，請參閱 [Remove-OrganizationRelationship](https://technet.microsoft.com/zh-tw/library/ee332362\(v=exchg.150\))。

## 如何知道這是否正常運作？

若要確認您是否已成功移除組織關係，請執行下列其中一項操作：

  - 在 EAC 中，瀏覽至 **\[組織\]** \> **\[共用\]** 並確認該組織關係未顯示在 **\[組織共用\]** 下方的清單檢視中。

  - 執行下列命令介面命令，確認組織關係資訊已移除。
    
        Get-OrganizationRelationship | Format-List

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

