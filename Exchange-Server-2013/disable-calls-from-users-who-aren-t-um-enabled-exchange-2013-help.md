---
title: '停用未啟用 UM 之使用者的電話: Exchange Online Help'
TOCTitle: 停用未啟用 UM 之使用者的電話
ms:assetid: 272ff4ab-b4d9-4647-98e2-7c171f9dfc3f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ673516(v=EXCHG.150)
ms:contentKeyID: 50472738
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 停用未啟用 UM 之使用者的電話

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2012-11-05_

您可以啟用或停用使用者未啟用的整合通訊 (UM) 的來電。根據預設，整合通訊可讓來電轉接至已啟用 UM 的使用者透過自動語音應答未經過驗證的來電者。啟用此設定，與組織外部的使用者可以將來電轉接至已啟用 UM 的使用者。

如果已啟用 UM 之使用者的已停用此設定，仍可位於使用目錄搜尋使用者的信箱。不過，如果外部呼叫者嘗試傳送給使用者，表示系統、"我已經很抱歉，I am 無法轉接至這位使用者。 」如果已設定運算子上的自動語音應答來電者然後轉接到運算子。如果沒有運算子的自動語音應答上設定、 轉接至撥號對應表操作員，如果其中已設定。如果已啟用語音的自動語音應答、 雙音多頻 (dtmf) 後援自動語音應答或撥號對應表上不設定任何操作員分機，系統會回應由預警"抱歉。運算子和按鍵式服務都是可用。

如需與啟用語音信箱之使用者相關的其他管理工作，請參閱[擁有郵件功能的語音使用者程序](voice-mail-enabled-user-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

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


## 使用命令程式禁用來自未啟用 UM 之使用者的來電

此範例會讓 Tony Smith 無法接收未啟用 UM 之來電者的語音來電。

    Set UMMailbox -Identity tony@contoso.com -AllowUMCallsFromNonUsers None

