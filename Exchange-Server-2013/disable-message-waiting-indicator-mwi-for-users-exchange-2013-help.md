---
title: '停用使用者訊息等待指示器 (MWI): Exchange Online Help'
TOCTitle: 停用使用者訊息等待指示器 (MWI)
ms:assetid: 51cd6dc4-11d1-4eb9-a6c6-1965fcd24267
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ673525(v=EXCHG.150)
ms:contentKeyID: 50553985
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 停用使用者訊息等待指示器 (MWI)

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-21_

您可以啟用或停用使用者的整合通訊 (UM) 信箱原則相關聯訊息等待指示器。訊息等待指示器是最舊版的語音信箱系統中找到的功能。在其最常見的表單中，它會指出新的語音郵件訊息的顯示狀態的語音郵件訂閱者的電話上 lights 燈。訊息等待指示器也可以傳送文字郵件給已啟用 UM 之使用者的行動電話。會啟用預設設定。

如果在 UM IP 閘道上停用訊息等待指示器，則與 UM 信箱原則相關聯之已啟用 UM 的使用者，無法使用這項功能。

如需其他與 UM 信箱原則相關的管理工作，請參閱 [UM 信箱原則程序](um-mailbox-policy-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 信箱原則」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

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

## 使用 EAC 停用訊息等待指示器

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。在清單檢視中，選取您要變更的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 \[UM 信箱原則\] 下，選取您要管理的 UM 信箱原則，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[UM 信箱原則\] 頁面上，清除 \[允許郵件等待指示器\] 旁的核取方塊。

4.  按一下 \[儲存\]。

## 使用命令介面停用訊息等待指示器

此範例會針對與名為 `MyUMMailboxPolicy` 的 UM 信箱原則相關聯的使用者停用訊息等待指示器。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowMessageWaitingIndicator $false

