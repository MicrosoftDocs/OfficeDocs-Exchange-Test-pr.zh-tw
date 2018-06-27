---
title: '更新公用資料夾階層: Exchange Online Help'
TOCTitle: 更新公用資料夾階層
ms:assetid: a7b2fb51-0207-4d7d-938d-466ae110bb90
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ945055(v=EXCHG.150)
ms:contentKeyID: 52062386
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 更新公用資料夾階層

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2014-04-03_

只有在您要手動叫用階層同步器和信箱助理員時，才需要更新公用資料夾階層。對於組織中的每一個公用資料夾信箱，這兩種至少要每 24 小時叫用一次。如果有任何使用者是透過 Microsoft Outlook 或 Microsoft Exchange Web 服務用戶端登入到次要信箱，則每 15 分鐘會叫用階層同步器一次。

如需與 Exchange Online 中公用資料夾相關的其他管理工作，請參閱 [Office 365 和 Exchange Online 中公用資料夾程序](https://technet.microsoft.com/zh-tw/library/jj966272\(v=exchg.150\))。

如需與 Exchange Server 2013 中公用資料夾相關的其他管理工作，請參閱[公用資料夾程序](public-folder-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [共用和協同作業的權限](sharing-and-collaboration-permissions-exchange-2013-help.md)主題中的「公用資料夾」項目。

  - 您無法在 EAC 中執行此程序。您必須使用命令介面。

  - 建議您在執行此命令並搭配 *InvokeSynchronizer* 參數時，採用 *SuppressStatus* 參數。如果您未在命令中使用此參數，輸出會每 3 秒顯示一次狀態訊息，長達 1 分鐘。在這一分鐘內，您都無法使用命令介面的執行個體。

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


## 更新公用資料夾階層

此範例會更新公用資料夾信箱 PF\_marketing 的公用資料夾階層，並隱藏命令輸出。

    Update-PublicFolderMailbox -Identity PF_marketing -InvokeSynchronizer -SuppressStatus

此範例會更新所有公用資料夾信箱，並隱藏命令輸出。

    Get-Mailbox -PublicFolder | Update-PublicFolderMailbox InvokeSynchronizer -SuppressStatus

