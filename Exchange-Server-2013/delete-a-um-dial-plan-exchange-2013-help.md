---
title: '刪除 UM 撥號對應表: Exchange Online Help'
TOCTitle: 刪除 UM 撥號對應表
ms:assetid: c9b32ef6-432c-45ca-b94c-31bbcc973128
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124546(v=EXCHG.150)
ms:contentKeyID: 50474193
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 刪除 UM 撥號對應表

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2012-11-11_

您可以刪除現有的整合通訊 (UM) 撥號。當您刪除 UM 撥號對應表、 它將不再提供的 UM IP 閘道器、 UM 信箱原則，及 UM 群組搜尋。您無法刪除 UM 撥號對應表，則它已由參照或與 UM 信箱原則、 UM 自動語音應答、 UM IP 閘道相關聯 UM 群組搜尋。

如需與 UM 撥號對應表相關的其他管理工作，請參閱 [UM 撥號對應表規劃程序](um-dial-plan-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 撥號對應表」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。 如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

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

## 使用 EAC 來刪除現有的撥號

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。

2.  在清單檢視中，選取您要刪除的 UM 撥號\] 和 \[**刪除**![刪除圖示](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "刪除圖示")。

3.  在 \[警告\] 頁面上按一下 \[**是**\]。

## 使用命令介面來刪除現有的撥號

此範例會刪除名為`MyUMDialPlan`UM 撥號對應表。

    RemoveUMDialplan -identity MyUMDialPlan

