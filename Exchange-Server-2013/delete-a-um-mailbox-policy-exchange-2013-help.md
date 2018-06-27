---
title: '刪除 UM 信箱原則: Exchange Online Help'
TOCTitle: 刪除 UM 信箱原則
ms:assetid: c8758464-3c52-4dd3-b2a6-142a99bb0628
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124536(v=EXCHG.150)
ms:contentKeyID: 50554061
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 刪除 UM 信箱原則

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2012-11-05_

當您刪除整合通訊 (UM) 信箱原則時，UM 信箱原則將不再提供要與已正在啟用 UM 之收件者相關聯。如果它參照任何已啟用 UM 的信箱，且您無法刪除 UM 撥號對應表與它相關聯的 UM 信箱原則時，您無法刪除 UM 信箱原則。

如需其他與 UM 信箱原則相關的管理工作，請參閱 [UM 信箱原則程序](um-mailbox-policy-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 信箱原則」項目。

  - 執行這些程序之前，請確認已建立 UM 信箱原則。如需詳細步驟，請參閱[建立 UM 信箱原則](create-a-um-mailbox-policy-exchange-2013-help.md)。

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

## 使用 EAC 來刪除 UM 信箱原則

1.  
    
    在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。在清單檢視中，選取您要修改的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在**UM 撥號對應表**\] 頁面上 \[ **UM 信箱原則**，在工具列上，按一下 \[**刪除**![刪除圖示](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "刪除圖示")。

## 使用命令介面來刪除 UM 信箱原則

此範例會刪除名為`MyUMMailboxPolicy`的 UM 信箱原則。

    Remove-UMMailboxPolicy -Identity MyUMMailboxPolicy

