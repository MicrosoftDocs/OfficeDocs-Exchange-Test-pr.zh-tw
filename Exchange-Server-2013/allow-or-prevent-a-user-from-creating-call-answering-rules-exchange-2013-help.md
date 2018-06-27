---
title: '允許或防止使用者建立通話自動答錄服務規則: Exchange Online Help'
TOCTitle: 允許或防止使用者建立通話自動答錄服務規則
ms:assetid: 81863440-8b21-4523-bdab-6a2311889a0d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd298097(v=EXCHG.150)
ms:contentKeyID: 50554017
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 允許或防止使用者建立通話自動答錄服務規則

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-22_

您可以指定是否要讓個別使用者可以建立和管理自己自動答錄規則來設定其信箱內容。根據預設，他們可以建立自動答錄規則。

您可以在 UM 撥號對應表或 UM 信箱原則中設定自動答錄規則，針對整合通訊 (UM) 啟用的多位使用者啟用或停用自動答錄規則。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您無法使用 EAC 來設定此功能。您必須使用命令介面啟用或停用語音郵件使用者的通話自動答錄服務規則。</td>
</tr>
</tbody>
</table>


若要瞭解其他與允許使用者轉接電話相關的管理工作，請參閱[轉接通話程序](forwarding-calls-procedures-exchange-2013-help.md)。

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


## 使用命令介面為已啟用 UM 的使用者啟用或停用自動答錄規則

本範例會啟用使用者 tony@contoso.com 的自動答錄規則。

    Set-UMMailbox -Identity tony@contoso.com -CallAnsweringRulesEnabled $true

本範例會停用使用者 tony@contoso.com 的自動答錄規則。

    Set-UMMailbox -Identity tony@contoso.com -CallAnsweringRulesEnabled $false

