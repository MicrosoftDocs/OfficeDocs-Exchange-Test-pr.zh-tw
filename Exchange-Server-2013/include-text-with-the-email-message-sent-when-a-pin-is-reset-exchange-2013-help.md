---
title: '當 PIN 會重設時傳送電子郵件訊息中包含的文字: Exchange Online Help'
TOCTitle: 當 PIN 會重設時傳送電子郵件訊息中包含的文字
ms:assetid: f7a4d775-a588-412f-ac2c-11ab1a5c67eb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb201750(v=EXCHG.150)
ms:contentKeyID: 51409258
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 當 PIN 會重設時傳送電子郵件訊息中包含的文字

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-22_

您可以在他們的整合通訊 (UM) 或語音信箱 pin 碼重設時傳送給使用者的電子郵件訊息中包含其他文字。您這麼做**時重設使用者的 Outlook 語音存取 PIN** \] 方塊中輸入自訂文字在 UM 信箱原則。自訂的文字可以包含，例如已啟用 UM 之使用者的安全性相關資訊。

根據預設，Outlook 語音存取用來在重設 PIN 由整合通訊或語音信箱系統如果失敗的登入嘗試數目超過 5。使用者也可以重設其使用包含在Outlook Web App或 Outlook 2010 或更新版本，或使用Outlook語音存取從電話的 UM 功能的 Pin。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在此方塊中輸入文字的限制為 512 個字元，並可包含簡易 HTML 文字。</td>
</tr>
</tbody>
</table>


如需瞭解與 Outlook Voice Access PIN 碼安全性相關的其他工作，請參閱 [PIN 安全性程序](pin-security-procedures-exchange-2013-help.md)。

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

## 使用 EAC 以在重設使用者的 PIN 碼時，將文字加入傳送給使用者的電子郵件中

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。在清單檢視中，選取您要變更的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 **\[UM 撥號對應表\]** 頁面的 **\[UM 信箱原則\]** 下，選取您要管理的 UM 信箱原則，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 **\[UM 信箱原則\]** 頁面 \> **\[郵件文字\]** 的 **\[當使用者的 Outlook Voice Access PIN 碼重設時\]** 文字方塊中，輸入想要在重設使用者 PIN 碼時加入電子郵件中的文字。

4.  按一下 **\[儲存\]**。

## 使用命令介面以在重設使用者的 PIN 碼重設時，將文字加入傳送給使用者的電子郵件中

本範例會包含其他文字、"不要與其他使用者共用您的 PIN。這麼做讓可能會導致專業領域巨集指令"、 電子郵件中傳送到使用者與相關聯 UM 信箱原則`MyUMMailboxPolicy`時重設其 PIN。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -ResetPINText "Do not share your PIN with other users. Doing so may result in disciplinary action."

