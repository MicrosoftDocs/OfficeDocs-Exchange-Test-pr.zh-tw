---
title: '公用資料夾信箱移至不同信箱資料庫: Exchange 2013 Help'
TOCTitle: 公用資料夾信箱移至不同信箱資料庫
ms:assetid: 67601d45-4824-4ae6-9a7e-b645ec3af4d3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ906434(v=EXCHG.150)
ms:contentKeyID: 51409206
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 公用資料夾信箱移至不同信箱資料庫

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2015-07-21_

您可能需要將公用資料夾信箱移至不同信箱資料庫伺服器的負載平衡用途或將更接近資源移至其地理位置。類似移動一般信箱，您使用**MoveRequest**指令程式來移動公用資料夾信箱。如需移動信箱的詳細資訊，請參閱[在 Exchange 2013 移動信箱](mailbox-moves-in-exchange-2013-exchange-2013-help.md)。

如需與公用資料夾相關的其他管理工作，請參閱 [公用資料夾程序](public-folder-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間視公用資料夾信箱的大小而定。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「信箱移動與移轉權限」一節。

  - 您無法在 EAC 中執行此程序。您只可以在命令介面中執行此程序。

  - 視公用資料夾信箱的大小、 移動可能需要數小時才能完成。在該工作時，使用者將不能夠存取公用資料夾。使用者也無法存取公用資料夾簡短期間時資料夾是在 「 完成進行中 」 狀態。

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

## 建立移動要求

**New-MoveRequest**指令程式會將 Microsoft Exchange 信箱複寫服務佇列佇列公用資料夾信箱。使用 Microsoft Exchange 信箱複寫服務時，它會挑選的移動要求，並開始移動公用資料夾信箱。它會完成整個要求結束開始。

此範例會執行公用資料夾信箱 PF\_SanFrancisco 到信箱資料夾 MBX\_DB01 的移動要求。

    New-MoveRequest -Identity "PF_SanFrancisco" -TargetDatabase MBX_DB01

如需詳細的語法及參數資訊，請參閱 [New-MoveRequest](https://technet.microsoft.com/zh-tw/library/dd351123\(v=exchg.150\))。

## 建立稍後完成的移動要求

階段的移動要求最終時，它會在`CompletionInProgress`階段中，使用者可能會暫時鎖定公用資料夾信箱。必要時，您可以暫停的移動要求之前便該階段並恢復時將不會影響使用者一次。

此範例會執行公用資料夾信箱 PF\_SanFrancisco 到信箱資料庫 MBX\_DB01 的移動要求，並在移動要求準備完成時暫停。

    New-MoveRequest -Identity "PF_SanFrancisco" -TargetDatabase MBX_DB01 -SuspendWhenReadyToComplete

如需詳細的語法及參數資訊，請參閱 [New-MoveRequest](https://technet.microsoft.com/zh-tw/library/dd351123\(v=exchg.150\))。

此範例會擷取公用資料夾信箱 PF\_SanFrancisco 的進行中信箱移動狀態。

    Get-MoveRequest -Identity "PF_SanFrancisco"

如需詳細的語法及參數資訊，請參閱 [Get-MoveRequest](https://technet.microsoft.com/zh-tw/library/dd335227\(v=exchg.150\))。

當的移動要求達到暫停的狀態時，您可以繼續執行要求。此範例會繼續公用資料夾信箱 PF\_SanFrancisco 的移動要求。

    Resume-MoveRequest -Identity "PF_SanFrancisco"

如需詳細的語法及參數資訊，請參閱 [Resume-MoveRequest](https://technet.microsoft.com/zh-tw/library/ee332320\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要確認成功建立移動要求，請執行下列命令：

    Get-MoveRequestStatistics -Identity PF_SanFrancisco | Format-List Status

狀態 `Completed` 表示移動要求順利完成。

如果移動不成功，您可能需要還原公用資料夾。如需詳細資訊，請參閱[從失敗的移動還原公用資料夾和公用資料夾信箱](restore-public-folders-and-public-folder-mailboxes-from-failed-moves-exchange-2013-help.md)。

