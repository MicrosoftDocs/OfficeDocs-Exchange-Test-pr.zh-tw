---
title: '啟用或停用受保護的語音訊息的多媒體播放: Exchange Online Help'
TOCTitle: 啟用或停用受保護的語音訊息的多媒體播放
ms:assetid: 3c33370c-4262-42b1-8d83-d61fc7c426cd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee423543(v=EXCHG.150)
ms:contentKeyID: 52062284
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟用或停用受保護的語音訊息的多媒體播放

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-22_

您可以強制使用者會收到受保護的語音郵件訊息，以其訊息接聽電話的功能上使用 \[播放。或者，如果用戶端軟體不支援版權管理，使用者必須使用Outlook語音存取聆聽的郵件。

若要聆聽語音訊息、 已啟用整合通訊 UM 的使用者可以電話的功能上使用 \[播放或電腦或行動裝置上使用多媒體軟體。多媒體播放可讓已啟用 UM 的使用者電腦的喇叭透過使用媒體播放或行動裝置上使用媒體播放聽到語音訊息。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>只有在使用Outlook支援版權管理的版本的用戶端上使用受保護的語音信箱。如果用戶端軟體不支援版權管理，使用者必須使用Outlook語音存取其電話接聽。</td>
</tr>
</tbody>
</table>


根據預設，UM 信箱原則上**RequireProtectedPlayOnPhone**屬性的值設為 false。這表示已啟用 UM 的使用者相關聯的 UM 信箱原則可以收聽由受保護的語音訊息：

  - 使用 Outlook 語音存取。

  - 使用內建媒體播放器或 Outlook 2010 或更新版本中的 \[在電話上播放\] 按鈕。

  - 使用內建媒體播放器或 Outlook Web App 中的 \[在電話上播放\] 按鈕。

如果此值設為不允許的受保護的語音信箱，則為 true、 多媒體播放。此值設為 true 可以在其的 UM 信箱原則相關聯的已啟用 UM 的使用者只能由收聽受保護的語音訊息：

  - 使用 Outlook 語音存取。

  - 使用 Outlook 2010 或更新版本中的 \[在電話上播放\] 按鈕。

  - 使用 Outlook Web App 中的 \[在電話上播放\] 按鈕。

當已啟用 UM 的使用者使用公用電腦、公共地點中的筆記型電腦，或其行動裝置的媒體播放器來接聽可能包含私人資訊之受保護的語音郵件時，此設定就特別有幫助。

如需其他與受保護的語音信箱程序相關的管理工作，請參閱[受保護的語音信箱程序](protected-voice-mail-procedures-exchange-2013-help.md)。

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

## 使用 EAC 來啟用或停用受保護之語音訊息的多媒體播放

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。在清單檢視中，選取您要變更的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 \[UM 信箱原則\] 下，選取您要管理的 UM 信箱原則，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[ **UM 信箱原則**\] 頁面上 \>**受保護的語音信箱**、 選取啟用此設定**需要在受保護的語音訊息的電話上播放**\] 旁的核取方塊。清除核取方塊停用此設定。

4.  按一下 **\[儲存\]**。

## 使用命令介面來啟用或停用受保護之語音訊息的多媒體播放

此範例可讓與名為 `MyUMMailboxPolicy` 之 UM 信箱原則相關聯的使用者使用媒體播放器播放受保護的語音訊息。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -RequireProtectedPlayOnPhone $false

此範例可禁止與名為 `MyUMMailboxPolicy` 之 UM 信箱原則相關聯的使用者使用媒體播放器播放受保護的語音訊息。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -RequireProtectedPlayOnPhone $true

