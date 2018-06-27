---
title: '為使用者啟用語音郵件預覽: Exchange Online Help'
TOCTitle: 為使用者啟用語音郵件預覽
ms:assetid: 206a5d2b-27c9-4e9b-a29a-6ddffaa07109
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ673514(v=EXCHG.150)
ms:contentKeyID: 51409164
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 為使用者啟用語音郵件預覽

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-21_

您可以啟用已停用與整合通訊 (UM) 信箱原則關聯的使用者的語音郵件預覽功能。啟用此設定可讓使用者接收電子郵件訊息本文中的語音信箱訊息或文字訊息的文字。會啟用預設設定。

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

## 使用 EAC 啟用語音信箱預覽

1.  在 EAC 中，瀏覽至 **\[整合通訊\]** \> **\[UM 撥號對應表\]**，選取要變更的 UM 撥號對應表，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 **\[UM 撥號對應表\]** 頁面的 **\[UM 信箱原則\]** 下，選取您要管理的 UM 信箱原則，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 **\[UM 信箱原則\]** 頁面 \> **\[一般\]**，選取 **\[允許語音信箱預覽\]** 旁的核取方塊。

4.  按一下 **\[儲存\]**。

## 使用命令介面啟用語音信箱預覽

此範例會允許與 UM 信箱原則 `MyUMMailboxPolicy` 關聯的使用者使用語音信箱預覽功能。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy - AllowVoiceMailPreview $true

