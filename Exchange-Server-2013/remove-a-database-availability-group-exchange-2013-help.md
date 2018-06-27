---
title: '移除資料庫可用性群組: Exchange 2013 Help'
TOCTitle: 移除資料庫可用性群組
ms:assetid: 071296e9-31b0-40f4-9a02-177d97486ebd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd335069(v=EXCHG.150)
ms:contentKeyID: 50472505
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 移除資料庫可用性群組

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-11-16_

移除資料庫可用性群組 (DAG) 為快速又簡單的工作。您可以使用 EAC 或命令介面來移除 DAG。

要尋找與 DAG 相關的其他管理工作嗎？請參閱[管理資料庫可用性群組](managing-database-availability-groups-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：1 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [高可用性和站台回復性權限](high-availability-and-site-resilience-permissions-exchange-2013-help.md) 主題中的「資料庫可用性群組」項目。

  - 您可以移除 DAG 之前，DAG 必須是空的。如果您想要移除的 DAG 包含任何 Mailbox server，您必須先從 DAG 中移除伺服器。如需如何從 DAG 移除信箱伺服器的詳細步驟，請參閱[管理資料庫可用性群組成員資格](manage-database-availability-group-membership-exchange-2013-help.md)。

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

## 使用 EAC 移除資料庫可用性群組

1.  導航到\[伺服器\] \> \[資料庫可用性組\]。

2.  選取要變更的 DAG，然後按一下 \[刪除\]![刪除圖示](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "刪除圖示")。

3.  按一下\[是\] 以確認警告並移除 DAG。

## 使用命令介面移除資料庫可用性群組

本範例會移除 DAG DAG1。

    Remove-DatabaseAvailabilityGroup -Identity DAG1

## 如何才能了解這是否正常運作？

若要驗證您是否已成功移除 DAG，請執行下列其中一項操作：

  - 在 EAC 中，前往 \[伺服器\] \>\[資料庫可用性群組\] ，然後查看 DAG 是否仍顯示。

  - 在命令介面中執行下列命令以查看 DAG 是否仍存在：
    
        Get-DatabaseAvailabilityGroup <DAGName>
    
    若成功刪除 DAG，先前的命令將產生一則錯誤訊息表示找不到物件。

