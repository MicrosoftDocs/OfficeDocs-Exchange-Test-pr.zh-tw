---
title: '啟用或停用 Outlook 語音存取使用者的自動語音辨識: Exchange Online Help'
TOCTitle: 啟用或停用 Outlook 語音存取使用者的自動語音辨識
ms:assetid: 58f41016-e725-432b-953e-415d61e0664c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb232062(v=EXCHG.150)
ms:contentKeyID: 50553995
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟用或停用 Outlook 語音存取使用者的自動語音辨識

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-22_

您可以設定已啟用整合通訊 (UM) 和語音信箱的使用者自動語音辨識 (ASR)。ASR Outlook語音存取使用者信箱啟用時，使用者可以移動到使用語音命令的信箱功能表。預設會啟用 ASR。如果停用 ASR 時，使用者必須使用複頻式訊號 (DTMF) 也稱為按鍵式輸入來瀏覽功能表。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您無法使用 EAC 來設定此功能。您必須使用命令介面啟用或停用語音郵件使用者的 ASR。</td>
</tr>
</tbody>
</table>


UM 或語音郵件使用者相關的其他管理工作，請參閱[擁有郵件功能的語音使用者程序](voice-mail-enabled-user-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 信箱」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

  - 執行這些程序之前，請確認已建立 UM 信箱原則。如需詳細步驟，請參閱[建立 UM 信箱原則](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 執行這些程序之前，請確認有已啟用 UM 的使用者的信箱。如需詳細步驟，請參閱[啟用使用者的語音信箱](enable-a-user-for-voice-mail-exchange-2013-help.md)。

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


## 使用命令介面為啟用 UM 的使用者啟用或停用 ASR

此範例會針對名為 `tonysmith` 之啟用 UM 的使用者啟用 ASR。

    Set-UMMailbox -Identity tonysmith@contoso.com -AutomaticSpeechRecognitionEnabled $true

此範例會針對名為 `tonysmith` 之啟用 UM 的使用者停用 ASR。

    Set-UMMailbox -Identity tonysmith@contoso.com -AutomaticSpeechRecognitionEnabled $false

