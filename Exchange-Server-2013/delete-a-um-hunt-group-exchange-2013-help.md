---
title: '刪除 UM 群組搜尋: Exchange Online Help'
TOCTitle: 刪除 UM 群組搜尋
ms:assetid: 11ac102d-b58d-486c-85b6-e096428e556d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa996318(v=EXCHG.150)
ms:contentKeyID: 50553937
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 刪除 UM 群組搜尋

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2012-11-05_

刪除整合通訊 (UM) 群組搜尋後，UM 群組搜尋相關聯的 UM IP 閘道將不再 service 或接聽來電。如果刪除的 UM 群組搜尋留下沒有任何剩餘的搜尋設定的群組的 UM IP 閘道、 UM IP 閘道器無法處理或 UM 呼叫。

如需與 UM IP 群組搜尋相關的其他管理工作，請參閱 [UM 群組搜尋的程序](um-hunt-group-procedures-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您要變更 UM 群組搜尋設定，則必須刪除該群組搜尋，然後再建立另一個具有適當設定值的群組搜尋。</td>
</tr>
</tbody>
</table>


## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 群組搜尋」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

  - 執行這些程序之前，請確認已建立 UM IP 閘道器。如需詳細步驟，請參閱[建立 UM IP 閘道器](create-a-um-ip-gateway-exchange-2013-help.md)。

  - 執行這些程序之前，請確認已建立 UM 群組搜尋。如需詳細步驟，請參閱[建立 UM 群組搜尋](create-a-um-hunt-group-exchange-2013-help.md)。

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

## 使用 EAC 刪除 UM 群組搜尋

1.  在 EAC 中，瀏覽至 \[**整合通訊**\> **UM 撥號對應表**。在清單檢視中，按一下您想要變更 UM 撥號對應表並在工具列上，按一下 \[**編輯**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 \[UM 撥號對應表\] 頁面的 \[UM 群組搜尋\] 下方，選取要刪除的群組搜尋，然後按一下工具列上的 \[刪除\]![刪除圖示](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "刪除圖示")。

3.  在 \[警告\] 頁面上按一下 \[是\]。

## 使用命令介面刪除 UM 群組搜尋

此範例會刪除名為 `MyUMHuntGroup` 的 UM 群組搜尋。

    Remove-UMHuntGroup -identity MyUMHuntGroup

