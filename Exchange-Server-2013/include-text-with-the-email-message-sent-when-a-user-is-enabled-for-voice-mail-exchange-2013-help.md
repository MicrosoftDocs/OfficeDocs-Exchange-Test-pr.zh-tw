---
title: '當使用者已啟用語音信箱時傳送電子郵件訊息中包含的文字: Exchange Online Help'
TOCTitle: 當使用者已啟用語音信箱時傳送電子郵件訊息中包含的文字
ms:assetid: 3e8292fb-0cdb-445d-8048-a59af7c38d63
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb201679(v=EXCHG.150)
ms:contentKeyID: 51409173
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 當使用者已啟用語音信箱時傳送電子郵件訊息中包含的文字

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2012-12-16_

當使用者的信箱已啟用整合通訊 (UM) 的語音信箱時、 電子郵件訊息會傳送之歡迎至 \[整合通訊的使用者。此訊息包含使用者將會使用第一次存取語音信箱系統的 PIN 資訊。

您可以自訂在 UM 信箱原則的**使用者啟用整合通訊時**\] 方塊中新增文字傳送歡迎電子郵件訊息中的文字。您可以包含為 UM 技術支援電話號碼或其他 Outlook 語音存取號碼這類資訊。新增文字後，它將會包含在關聯的 UM 信箱原則的使用者啟用整合通訊時傳送的電子郵件訊息。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>加入歡迎使用郵件中的自訂文字最多為 512 個字元，其中可包括簡單的 HTML 文字。</td>
</tr>
</tbody>
</table>


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

## 使用 EAC 自訂為信箱啟用整合通訊時傳送的文字

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。在清單檢視中，選取您要變更的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 **\[UM 撥號對應表\]** 頁面的 **\[UM 信箱原則\]** 下，選取您要管理的 UM 信箱原則，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 **\[UM 信箱原則\]** 頁面 \> **\[郵件文字\]** 的 **\[使用者啟用整合通訊時\]** 文字方塊中，輸入要加入使用者啟用整合通訊語音信箱時傳送之電子郵件的文字。

4.  按一下 **\[儲存\]**。

## 使用命令介面自訂為信箱啟用整合通訊時傳送的文字

此範例可以讓與 UM 信箱原則關聯並已啟用 UM 的使用者收到關於 UM 的其他指示，以及他們可用來透過電話存取其信箱的 Outlook 語音存取號碼。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -UMEnabledText "You've been enabled for Unified Messaging voice mail. To access your Exchange mailbox, call your internal telephone extension number. From outside your office, call 425-555-1234."

