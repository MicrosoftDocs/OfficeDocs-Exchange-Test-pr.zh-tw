---
title: '設定您的組織的大型對象大小: Exchange Online Help'
TOCTitle: 設定您的組織的大型對象大小
ms:assetid: 8a37911c-4339-4921-b5d3-0a5a774d4517
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ659068(v=EXCHG.150)
ms:contentKeyID: 50473691
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定您的組織的大型對象大小

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2015-04-08_

您可使用 Exchange 管理命令介面進行各種設定，以定義在組織中使用「寄件提醒」的方式。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「郵件提示」項目。

  - 您只能使用命令介面來執行此程序。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 使用命令介面設定您組織的大型對象大小

您可以使用**Set-OrganizationConfig**指令程式來設定您的組織的大型對象大小。當超過大小的多個收件者寄件者地址的郵件您設定、 顯示大型對象 」 郵件提示。大型對象大小預設會設為 25。此範例會設定在組織中的大型對象大小設為 50。

    Set-OrganizationConfig -MailTipsLargeAudienceThreshold 50

如需詳細的語法及參數資訊，請參閱 [Set-OrganizationConfig](https://technet.microsoft.com/zh-tw/library/aa997443\(v=exchg.150\))。

