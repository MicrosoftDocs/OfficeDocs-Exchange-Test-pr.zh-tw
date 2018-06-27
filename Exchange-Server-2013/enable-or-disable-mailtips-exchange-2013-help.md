---
title: '啟用或停用郵件提示: Exchange 2013 Help'
TOCTitle: 啟用或停用郵件提示
ms:assetid: 11ad3848-f303-4ad5-a21d-9b0883db4bda
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ649321(v=EXCHG.150)
ms:contentKeyID: 50472595
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟用或停用郵件提示

 

_**適用版本：**Exchange Server 2013_

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


## 使用命令介面啟用或停用郵件提示

您可以使用**Set-OrganizationConfig**指令程式來啟用或停用組織中的郵件提示。當您安裝新的Exchange組織時依預設啟用的郵件提示。本範例會示範如何在組織中啟用 \[寄件提醒。

    Set-OrganizationConfig -MailTipsAllTipsEnabled $true

如需詳細的語法及參數資訊，請參閱 [Set-OrganizationConfig](https://technet.microsoft.com/zh-tw/library/aa997443\(v=exchg.150\))。

