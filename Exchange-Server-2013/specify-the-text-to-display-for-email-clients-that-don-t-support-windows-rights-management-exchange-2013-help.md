---
title: '指定要顯示的電子郵件用戶端不支援 Windows Rights Management 的文字: Exchange Online Help'
TOCTitle: 指定要顯示的電子郵件用戶端不支援 Windows Rights Management 的文字
ms:assetid: a9b2238a-b534-469c-a0c3-2768bc3d005b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee423552(v=EXCHG.150)
ms:contentKeyID: 52062389
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 指定要顯示的電子郵件用戶端不支援 Windows Rights Management 的文字

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-22_

您可以指定當使用者收到受保護的語音訊息但其電子郵件用戶端不支援資訊版權管理 (IRM) 或 Windows Rights Management 時，要傳送給該使用者的文字。

只有支援 Windows Rights Management 的電子郵件用戶端可以存取受保護的語音信箱，或者已啟用 UM 的使用者也能利用 Outlook 語音存取來存取受保護的語音訊息。

受保護的語音信箱已加密。當受到保護的語音訊息：

  - 訊息會在 Microsoft Outlook 及 Outlook Web App 中標示為「私人」。

  - 只有語音訊息的預期收件者才能開啟語音訊息。

  - 收件人可以答复语音邮件，但是不能将该语音邮件转发给未包含在原始语音邮件中的人员。

如果受保護的語音訊息傳送給某人其電子郵件用戶端不支援 Windows Rights Management 並不存取使用Outlook語音存取郵件、 電子郵件訊息會傳送給他們，其中包含您指定的文字。這段文字應該包含能夠將會收到受保護的語音訊息稱為的廠商應執行的動作的相關指示。

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

## 使用 EAC 指定要顯示給不支援 Windows Rights Management 之電子郵件用戶端的文字

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。在清單檢視中，選取您要變更的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 **\[UM 撥號對應表\]** 頁面的 **\[UM 信箱原則\]** 下，選取您要管理的 UM 信箱原則，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 **\[UM 信箱原則\]** 頁面 \> **\[受保護的語音信箱\]** 中，於 **\[要傳送給沒有 Windows Rights Management 支援之使用者的郵件\]** 下方的文字方塊中輸入訊息文字。

4.  按一下 **\[儲存\]**。

## 使用命令介面指定要顯示給不支援 Windows Rights Management 之電子郵件用戶端的文字

此範例指定要顯示給與名為 `MyUMMailboxPolicy` 之 UM 信箱原則關聯的使用者 (且其電子郵件用戶端不支援 Windows Rights Management) 的文字。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -ProtectedVoiceMailText "Your email client software does not support Protected Voice Mail. Please contact the Help Desk."

