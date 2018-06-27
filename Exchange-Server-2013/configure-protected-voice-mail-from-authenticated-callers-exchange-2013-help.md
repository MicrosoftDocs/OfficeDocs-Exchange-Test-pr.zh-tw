---
title: '從已驗證的來電者設定受保護的語音信箱: Exchange Online Help'
TOCTitle: 從已驗證的來電者設定受保護的語音信箱
ms:assetid: f69e94a7-9768-4445-9ded-e78d732bd623
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee423560(v=EXCHG.150)
ms:contentKeyID: 52062442
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 從已驗證的來電者設定受保護的語音信箱

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-22_

您可以設定整合通訊接聽來電，並再決定是否要套用保護到語音郵件訊息所使用的加密。當受到保護的語音訊息：

  - 訊息在 Microsoft Outlook 和 Outlook Web App 中會標示為 \[私人\]。

  - 僅有預定的語音訊息收件者才能開啟語音訊息。

  - 收件者可以回覆語音訊息，但不可將其轉寄至未包含在原始語音訊息中的人員。

此設定會套用到這些未接聽電話時傳送給啟用 UM 之使用者的語音訊息。此設定也適用於當來電者登入使用Outlook語音存取其信箱並再建立及傳送語音訊息。

如需與「受保護的語音信箱」相關的其他管理工作，請參閱[受保護的語音信箱程序](protected-voice-mail-procedures-exchange-2013-help.md)。

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

## 使用 EAC 設定來自已驗證呼叫者的「受保護的語音信箱」

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。在清單檢視中，選取您要修改的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 **\[UM 撥號對應表\]** 頁面的 **\[UM 信箱原則\]** 下，選取您要管理的 UM 信箱原則，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 **\[UM 信箱原則\]** 頁面 \> **\[受保護的語音信箱\]** 的 **\[保護已驗證呼叫者的語音訊息\]** 下方，選取下列其中一個選項：
    
      - **無**   若不想為傳送給啟用 UM 之使用者的任何語音訊息套用保護，請使用此設定。
    
      - **私人**   若您希望「整合通訊」僅對來電者標示為私人的語音訊息套用保護，請使用此設定。
    
      - **全部**   若您希望「整合通訊」對所有語音訊息 (包含未標示為私人的語音訊息) 套用保護，請使用此設定。

4.  按一下 **\[儲存\]**。

## 使用命令介面設定來自已驗證呼叫者的「受保護的語音信箱」

此範例會保護來自 `MyUMMailboxPolicy` UM 信箱原則上所有已驗證呼叫者的語音訊息。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy ProtectAuthenticatedVoiceMail -All

