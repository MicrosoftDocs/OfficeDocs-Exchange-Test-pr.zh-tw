---
title: '接收傳真郵件時傳送的電子郵件訊息中包含的文字: Exchange Online Help'
TOCTitle: 接收傳真郵件時傳送的電子郵件訊息中包含的文字
ms:assetid: 48244e58-b7d6-4f0e-bbae-d22bf0fc11ff
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb201684(v=EXCHG.150)
ms:contentKeyID: 51409185
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 接收傳真郵件時傳送的電子郵件訊息中包含的文字

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2016-12-09_

您可以由誰整合通訊 (UM) 的語音信箱啟用與傳真功能且當 UM 信箱原則已正確設定以使用傳真協力廠商提供者的使用者接收傳真訊息時傳送電子郵件訊息中包含其他文字。根據預設，包含時已啟用 UM 的使用者接收傳真訊息的文字會指出僅使用者已收到傳真訊息。不過，您可以將文字新增 UM 信箱原則上**時使用者接收傳真訊息**方塊中建立的自訂訊息。例如，文字可以包含系統安全性原則的相關資訊及說明的正確的方式來處理您組織中的傳真訊息。新增文字後，它將會包含每個相關聯的 UM 信箱原則已啟用 UM 的使用者接收傳真訊息時傳送的電子郵件中。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>傳真訊息內含的自訂文字長度限制在 512 個字元內，其中可包括簡單的 HTML 文字。</td>
</tr>
</tbody>
</table>


如需傳真協力廠商的詳細資訊，請參閱[Microsoft PinPoint 傳真協力廠商](https://go.microsoft.com/fwlink/?linkid=190238)。

如需與傳真相關的其他管理工作，請參閱[傳真程序](faxing-procedures-exchange-2013-help.md)。

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

## 使用 EAC 變更傳真訊息包含的文字

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。在清單檢視中，選取您要變更的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 **\[UM 撥號對應表\]** 頁面的 **\[UM 信箱原則\]** 下，選取您要管理的 UM 信箱原則，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 **\[UM 信箱原則\]** 頁面 \> **\[郵件文字\]** 的 **\[當使用者收到傳真訊息時\]** 文字方塊中，輸入要加入使用者在信箱中收到傳真訊息時所傳送之電子郵件內的文字。

4.  按一下 **\[儲存\]**。

## 使用命令介面變更傳真訊息包含的文字

此範例可讓與 UM 信箱原則關聯並已啟用 UM 的使用者接收如何開啟信箱中所收到傳真訊息的其他指示。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -FaxMessageText "To open this fax message, double-click the file attachment."

