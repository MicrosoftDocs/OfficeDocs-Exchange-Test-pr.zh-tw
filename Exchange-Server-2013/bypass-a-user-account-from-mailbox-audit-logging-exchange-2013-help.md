---
title: '使用者帳戶從信箱稽核記錄略過: Exchange 2013 Help'
TOCTitle: 使用者帳戶從信箱稽核記錄略過
ms:assetid: 98a87071-fe31-4b67-beb8-a73799e54df2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ff461934(v=EXCHG.150)
ms:contentKeyID: 50473786
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用者帳戶從信箱稽核記錄略過

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2013-05-21_

當您啟用信箱稽核記錄功能信箱時，會記錄指定的信箱的存取事件 （例如存取資料夾或訊息，或永久刪除郵件）。不過，某些存取授權帳戶、 例如協力廠商工具或 lawful 監控、 所使用的帳戶所使用的帳戶可以建立大量的信箱稽核記錄項目與可能不是您組織的感興趣。

您可以設定的使用者或電腦帳戶若要略過信箱稽核記錄，因此不記錄或帳戶的所有信箱的使用者所採取的動作。藉由略過受信任的使用者或電腦帳戶需要經常存取信箱，您可以減少雜訊信箱稽核記錄檔中。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您使用信箱稽核記錄稽核信箱存取和動作，您必須在固定間隔監視信箱稽核略過關聯。如果信箱稽核略過關聯性會新增帳戶、 帳戶可以存取之已被指派權限，而這類存取或 （例如郵件刪除） 採取任何動作所產生任何信箱稽核記錄項目不在組織中的所有信箱。</td>
</tr>
</tbody>
</table>


如需與信箱稽核記錄相關的其他管理工作，請參閱[信箱稽核記錄程序](mailbox-audit-logging-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「信箱稽核記錄」項目。

  - 當帳戶設定要略過信箱稽核記錄時，將不會登任何由該帳戶的信箱存取權。您無法設定帳戶略過特定信箱的存取權的記錄。

  - 您無法使用 Exchange 系統管理中心 (EAC) 來啟用或停用信箱稽核記錄略過的帳戶。您必須使用命令介面。

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


## 使用命令介面啟用或停用帳戶的信箱稽核記錄略過

若欲瞭解啟用帳號信箱稽核登入旁路的範例，請參閱 [Set-MailboxAuditBypassAssociation](https://technet.microsoft.com/zh-tw/library/ff696758\(v=exchg.150\)) 中的 [Examples](https://technet.microsoft.com/zh-tw/ff696758\(exchg.150\)#examples)。

若欲了解停用帳號信箱稽核登入旁路的範例，請參閱 [Set-MailboxAuditBypassAssociation](https://technet.microsoft.com/zh-tw/library/ff696758\(v=exchg.150\)) 中的[Examples](https://technet.microsoft.com/zh-tw/ff696758\(exchg.150\)#examples)。

## 如何才能了解這是否正常運作？

在您略過使用者帳戶的信箱稽核記錄後，您可以執行 [Get-MailboxAuditBypassAssociation](https://technet.microsoft.com/zh-tw/library/ff696741\(v=exchg.150\)) 指令程式查看略過設定。

若欲了解如何查看信箱稽核略過關聯，請參閱 [Get-MailboxAuditBypassAssociation](https://technet.microsoft.com/zh-tw/library/ff696741\(v=exchg.150\)) 中的[Examples](https://technet.microsoft.com/zh-tw/ff696741\(exchg.150\)#examples)。

