---
title: '防止來電者沒有來電者識別碼留下語音訊息: Exchange Online Help'
TOCTitle: 防止來電者沒有來電者識別碼留下語音訊息
ms:assetid: dd5dad32-2f69-4bf4-8ff0-545c413d395a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ673571(v=EXCHG.150)
ms:contentKeyID: 50474395
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 防止來電者沒有來電者識別碼留下語音訊息

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-22_

您可以讓已啟用 UM 的使用者接收匿名來電者的語音訊息或防止能力。根據預設，當使用者已啟用整合通訊 (UM) 和語音信箱可以接聽電話匿名且不含來電者識別碼資訊。

在大多數的情況下接收到 Exchange 伺服器的電話會包含可用來判斷來電的來源來電者識別碼。不過，來電可能不基於下列原因包括來電者識別碼資訊：

  - 您組織的電話設備設定為不含來電者識別碼資訊。

  - 來電是來自行動或外部電話。

  - 來電者已停用其電話的本機號碼。

預設會啟用*AnonymousCallersCanLeaveMessages*參數，因為已啟用 UM 的使用者可以接收語音訊息即使來電者識別碼資訊不包含在內。如果*AnonymousCallersCanLeaveMessages*已停用此選項，並已啟用 UM 的使用者會收到不包括來電者識別碼的通話，通話會識別為匿名，並已啟用 UM 的使用者將不會收到語音訊息。

如需與啟用語音信箱之使用者相關的其他管理工作，請參閱[擁有郵件功能的語音使用者程序](voice-mail-enabled-user-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 2 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 信箱」項目。

  - 執行此程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

  - 執行此程序之前，請確認已建立 UM 信箱原則。如需詳細步驟，請參閱[建立 UM 信箱原則](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 執行此程序之前，請確認有已啟用 UM 的使用者的信箱。如需詳細步驟，請參閱[啟用使用者的語音信箱](enable-a-user-for-voice-mail-exchange-2013-help.md)。

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


## 使用命令介面拒絕匿名來電者的語音訊息

此範例可防止已啟用 UM 的使用者 onysmith@contoso.com 從未包含來電者識別碼資訊的來電接收語音訊息。

    Set-UMMailbox -Identity tonysmith@contoso.com -AnonymousCallersCanLeaveMessages $false

