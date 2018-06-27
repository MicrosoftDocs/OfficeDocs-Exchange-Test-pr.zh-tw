---
title: 'UM 信箱原則指派: Exchange Online Help'
TOCTitle: UM 信箱原則指派
ms:assetid: c8da6cbe-3d22-4fff-8b5a-416b1c8adb6c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb201728(v=EXCHG.150)
ms:contentKeyID: 50474218
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# UM 信箱原則指派

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2012-11-30_

當您啟用使用者的整合通訊 (UM) 和語音信箱時，您必須選取要與使用者的信箱建立關聯的 UM 信箱原則。您可以變更之後已啟用 um 的使用者與使用者的信箱關聯的 UM 信箱原則。

您建立 UM 信箱原則套用至一組已啟用 UM 之使用者的信箱的一組通用原則\] 或 \[安全性設定。您可以使用 UM 信箱原則套用設定如下所示：

  - PIN 碼原則

  - 撥號限制

  - 其他一般 UM 信箱原則屬性

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>每次您建立 UM 撥號對應表建立預設的 UM 信箱原則。您可以刪除預設的 UM 信箱原則或建立額外的 UM 信箱原則根據組織的需求。</td>
</tr>
</tbody>
</table>


如需與啟用語音信箱之使用者相關的其他管理工作，請參閱[擁有郵件功能的語音使用者程序](voice-mail-enabled-user-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 2 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 信箱原則」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

  - 執行這些程序之前，請確認已建立 UM 信箱原則。如需詳細步驟，請參閱[建立 UM 信箱原則](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 執行這些程序之前，請確認使用者已啟用整合通訊。如需詳細步驟，請參閱[啟用使用者的語音信箱](enable-a-user-for-voice-mail-exchange-2013-help.md)。

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

## 使用 EAC 來變更指派給啟用 UM 功能之使用者的 UM 信箱原則

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[信箱\]。

2.  在清單檢視中，選擇您要變更 UM 信箱原則的信箱。

3.  在詳細資料窗格中的 \[電話與語音功能\] \> \[整合通訊\] 下方，按一下 \[檢視詳細資料\]。

4.  在 \[UM 信箱\] 頁面上，按一下 \[UM 信箱設定\]，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

5.  在 \[UM 信箱\] 頁面上，按一下 \[UM 信箱原則\] 旁邊的 \[瀏覽\] 以尋找使用者的 UM 信箱原則。

6.  按一下 \[儲存\]。

## 使用命令介面來變更指派給啟用 UM 功能之使用者的 UM 信箱原則

此範例會建立啟用 UM 功能之使用者 Tony Smith 與 UM 信箱原則 `MyUMMailboxPolicy` 的關聯。

    Set-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy

