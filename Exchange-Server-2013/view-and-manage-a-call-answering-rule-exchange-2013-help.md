---
title: '檢視及管理自動答錄規則: Exchange Online Help'
TOCTitle: 檢視及管理自動答錄規則
ms:assetid: de6d9fa1-7878-49a9-bddb-e3317d94f4d8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn140251(v=EXCHG.150)
ms:contentKeyID: 54652569
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 檢視及管理自動答錄規則

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2015-04-08_

您可以使用命令介面來檢視或設定一個或多個使用者呼叫接聽規則。您也可以使用 Exchange 管理命令介面指令碼中的**Get-UMCallAnsweringRule**或**Set-UMCallAnsweringRule**指令程式來檢視或管理自動答錄規則的多個使用者。

自動答錄規則套用至來電的方式，類似於將收件匣規則套用至傳入電子郵件的方式。 根據預設，為使用者啟用整合通訊 (UM) 時，不會設定任何自動答錄規則。 即使如此，郵件系統仍會接聽來電，並提示來電者留下語音訊息。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>已啟用 UM 的使用者可以登入 Outlook Web App，以建立、管理及移除自動答錄規則。</td>
</tr>
</tbody>
</table>


如需與自動答錄規則相關的其他管理工作，請參閱[轉接通話程序](forwarding-calls-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 自動答錄規則」項目。

  - 執行此程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

  - 執行此程序之前，請確認已建立 UM 信箱原則。如需詳細步驟，請參閱[建立 UM 信箱原則](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 執行此程序之前，請確認有已啟用 UM 的使用者的信箱。如需詳細步驟，請參閱[啟用使用者的語音信箱](enable-a-user-for-voice-mail-exchange-2013-help.md)。

  - 您只能使用命令介面來執行此程序。 若要了解如何在內部部署 Exchange 組織中開啟 Exchange 管理命令介面，請參閱[開啟命令介面。](https://technet.microsoft.com/zh-tw/library/dd638134\(v=exchg.150\))。 若要了解如何使用 Windows PowerShell 連線到 Exchange Online，請參閱[連線到 Exchange Online Protection PowerShell](https://go.microsoft.com/fwlink/p/?linkid=396554)。

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

## 使用命令介面來檢視自動答錄規則

您可以擷取單一自動答錄規則的內容或清單啟用 UM 之使用者信箱中呼叫接聽規則。

此範例會傳回使用者已啟用 UM 的信箱中自動答錄規則的格式化清單。

    Get-UMCallAnsweringRule-Mailbox tonysmith | Format-List

本範例會顯示自動答錄規則`MyUMCallAnsweringRule`屬性。

    Get-UMCallAnsweringRule -Identity MyUMCallAnsweringRule

## 使用命令介面來設定的自動答錄規則

您可以設定或變更自動答錄規則會儲存在使用者的信箱。您可以指定下列條件：

  - 來電的發話者

  - 一天中的時間

  - 行事曆空閒/忙碌狀態

  - 是否開啟電子郵件的自動回覆功能

您也可以指定下列動作：

  - 尋找我

  - 將來電者轉接給他人

  - 留下語音訊息

本範例會將優先順序設定為 2 上呼叫自動答錄規則`MyCallAnsweringRule`存在於信箱中 Tony smith。

    Set-UMCallAnsweringRule -Mailbox tonysmith -Name MyCallAnsweringRule -Priority 2

本範例會執行下列動作上呼叫自動答錄規則`MyCallAnsweringRule`信箱中 Tony smith：

  - 將自動應答規則設為兩個來電顯示。

  - 將自動應答規則的優先度設為 2。

  - 將自動應答規則設為允許來電者中斷問候語。

<!-- end list -->

    Set-UMCallAnsweringRule -Name MyCallAnsweringRule -CallerIds "1,4255550100,,","1,4255550123,," -Priority 2 -CallersCanInterruptGreeting $true -Mailbox tonysmith

本範例會將空閒/忙碌狀態變更為離開上呼叫自動答錄規則`MyCallAnsweringRule`信箱中 Tony smith 並將優先順序設定為 2。

    Set-UMCallAnsweringRule -Name MyCallAnsweringRule -Priority 2 -Mailbox tonysmith@contoso.com -ScheduleStatus 0x8

