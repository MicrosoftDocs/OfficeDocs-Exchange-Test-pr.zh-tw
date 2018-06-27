---
title: '從失敗的移動還原公用資料夾和公用資料夾信箱: Exchange 2013 Help'
TOCTitle: 從失敗的移動還原公用資料夾和公用資料夾信箱
ms:assetid: 2ade83c9-5f9b-4945-bf32-48fa8185b515
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ983802(v=EXCHG.150)
ms:contentKeyID: 52062525
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 從失敗的移動還原公用資料夾和公用資料夾信箱

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-13_

如果公用資料夾或公用資料夾信箱的移動要求失敗，只要符合下列條件就能還原資料夾或信箱：

  - **失敗的公用資料夾移動**   虛刪除的公用資料夾副本仍然存在於來源公用資料夾信箱，且仍在保留期間內。

  - **失敗的公用資料夾信箱移動**   虛刪除的公用資料夾信箱副本仍然存在於來源信箱資料庫，且仍在信箱保留期間內。

如果在經過信箱保留期間，您可以從備份復原的個別公用資料夾信箱。然後從還原的信箱擷取資料並將它複製到目標資料夾或合併與另一個信箱。如需詳細資訊，請參閱[使用復原資料庫還原資料](restore-data-using-a-recovery-database-exchange-2013-help.md)。

如需與公用資料夾相關的其他管理工作，請參閱 [公用資料夾程序](public-folder-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「信箱還原要求」項目。

  - 您無法使用 EAC 來執行此程序。您必須使用命令介面。

  - 若要建立還原要求，您必須為虛刪除的公用資料夾信箱提供 *DisplayName*、*LegacyDN* 或 *MailboxGUID* 參數的值。

  - 根據預設，暫放資料夾將會還原以及規則的資料夾。這可以避免使用*ExcludeDumpster*參數。

  - 還原公用資料夾信箱不同於還原一般信箱，若不存在的目標信箱中將不會建立資料夾。遺失的資料夾會顯示在結尾處的還原要求的警告訊息。

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


## 您要執行的工作

## 還原虛刪除的公用資料夾

此範例會將公用資料夾 \\Dev\\CustomerEnagagements 還原到目標公用資料夾信箱 Development01。

    New-MailboxRestoreRequest -SourceStoreMailbox Development -SourceDatabase MBX_DB01 -TargetMailbox Development01 -AllowLegacyDNMismatch -IncludeFolders \Dev\CustomerEngagements

如需詳細的語法及參數資訊，請參閱 [New-MailboxRestoreRequest](https://technet.microsoft.com/zh-tw/library/ff829875\(v=exchg.150\))。

## 還原虛刪除的公用資料夾信箱

此範例會將公用資料夾信箱 PF\_Singapore 還原到新的公用資料夾信箱 PF\_Singapore\_Restore。

    New-MailboxRestoreRequest -SourceStoreMailbox PF_Singapore -SourceDatabase MBX_DB01 -TargetMailbox PF_Singapore_Restore -AllowLegacyDNMismatch

如需詳細的語法及參數資訊，請參閱 [New-MailboxRestoreRequest](https://technet.microsoft.com/zh-tw/library/ff829875\(v=exchg.150\))。

