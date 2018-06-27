---
title: '搜尋信箱的信箱稽核記錄: Exchange 2013 Help'
TOCTitle: 搜尋信箱的信箱稽核記錄
ms:assetid: 5b518a08-3b51-4ba3-bfbd-0e35cc5ff374
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ff461930(v=EXCHG.150)
ms:contentKeyID: 50473271
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 搜尋信箱的信箱稽核記錄

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-03_

您可以在信箱稽核記錄項目中同步搜尋信箱，並在命令介面中顯示搜尋結果。

如果您想要搜尋多個信箱的信箱稽核記錄並將結果傳送至指定的地址，您必須改用建立信箱稽核記錄搜尋。如需詳細資訊，請參閱[建立信箱稽核記錄搜尋](create-a-mailbox-audit-log-search-exchange-2013-help.md)。

如需與信箱稽核記錄相關的其他管理工作，請參閱[信箱稽核記錄程序](mailbox-audit-logging-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「信箱稽核記錄」項目。

  - 根據預設，信箱稽核記錄已停用所有的信箱。您想要稽核的信箱，您必須啟用稽核記錄功能並指定您想要稽核的信箱擁有者、 委派、 或系統管理員動作。如需詳細資訊，請參閱[啟用或停用信箱稽核記錄功能信箱](enable-or-disable-mailbox-audit-logging-for-a-mailbox-exchange-2013-help.md)。

  - 您無法使用 EAC 來搜尋信箱的信箱稽核記錄。不過，您可以使用 EAC 來執行或搜尋並匯出非擁有者信箱存取報告。

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


## 使用命令介面在信箱稽核記錄中搜尋信箱

若需使用命令介面來搜尋信箱稽核記錄的範例，請參閱 [Search-MailboxAuditLog](https://technet.microsoft.com/zh-tw/library/ff522360\(v=exchg.150\)) 中的 [Examples](https://technet.microsoft.com/zh-tw/ff522360\(exchg.150\)#examples)。

