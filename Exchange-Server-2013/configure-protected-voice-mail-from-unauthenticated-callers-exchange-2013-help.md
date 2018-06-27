---
title: '從未經過驗證的來電者設定受保護的語音信箱: Exchange Online Help'
TOCTitle: 從未經過驗證的來電者設定受保護的語音信箱
ms:assetid: 106bfa0a-a0fa-4a1b-bd59-4b6df1d0d61d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd335098(v=EXCHG.150)
ms:contentKeyID: 52062225
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 從未經過驗證的來電者設定受保護的語音信箱

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-22_

您可以設定整合通訊接聽來電，並再決定是否要套用保護到語音郵件訊息所使用的加密。語音信箱訊息受到保護時：

  - 郵件已標示為私人，Microsoft Outlook和Outlook Web App中。

  - 只有語音訊息的預期收件者才能開啟語音訊息。

  - 收件者可以回覆語音訊息，但是不能將該語音訊息轉寄給未包含在原始語音訊息中的人員。

此設定會套用到這些未接聽電話時傳送給啟用 UM 之使用者的語音訊息。此設定也適用於來電者使用 UM 自動語音應答時傳送給啟用 UM 之使用者的語音訊息。

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

## 使用 EAC 來設定未驗證來電者的受保護語音信箱

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。在清單檢視中，選取您要修改的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 **\[UM 撥號對應表\]** 頁面的 **\[UM 信箱原則\]** 下，選取您要管理的 UM 信箱原則，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 **\[UM 信箱原則\]** 頁面 \> **\[受保護的語音信箱\]** 的 **\[保護未驗證來電者的語音訊息\]** 下，選取下列其中一個選項：
    
      - **無**   當您不想要將保護套用至任何傳送至已啟用 UM 的使用者的語音訊息時，請使用此設定。
    
      - **私人**   如果您想要整合通訊僅對來電者標記為私人的語音訊息套用保護，請使用此設定。
    
      - **全部**   如果您想要整合通訊對所有語音訊息套用保護 (包括未標示為私人的語音訊息)，請使用此設定。

4.  按一下 **\[儲存\]**。

## 使用命令介面來設定未驗證來電者的受保護語音信箱

本範例會保護 UM 信箱原則 `MyUMMailboxPolicy` 上所有未驗證來電者的所有語音訊息。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -ProtectUnauthenticatedVoiceMail -All

