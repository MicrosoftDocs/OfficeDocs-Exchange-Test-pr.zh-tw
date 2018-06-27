---
title: '將公用資料夾移至不同的公用資料夾信箱: Exchange 2013 Help'
TOCTitle: 將公用資料夾移至不同的公用資料夾信箱
ms:assetid: b8744934-a3cb-443e-acce-a9a6ca5d88f6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ906435(v=EXCHG.150)
ms:contentKeyID: 51409208
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 將公用資料夾移至不同的公用資料夾信箱

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2016-11-16_

如果超過信箱配額開頭的公用資料夾信箱的內容，您可能需要將公用資料夾移至不同的公用資料夾信箱。有幾種方式可以執行這項作業。若要移動一或多個公用資料夾不包含子資料夾，您可以使用**PublicFolderMoveRequest**指令程式。如果您需要移動整個公用資料夾分支下 （其中包括上層公用資料夾及所有子資料夾），您可以使用當您安裝 Exchange 2013 `Move-PublicFolderBranch.ps1`指令碼。

如需與公用資料夾相關的其他管理工作，請參閱[公用資料夾程序](public-folder-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 完成這項工作的預估時間取決於公用資料夾的大小。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [共用和協同作業的權限](sharing-and-collaboration-permissions-exchange-2013-help.md)主題中的「公用資料夾」項目。

  - 您無法使用 EAC 來執行這些程序。您必須使用命令介面。

  - 如果您正在移動之資料夾的子資料夾，則不會移動預設的這些子資料夾。如果您想要移動的公用資料夾及所有子資料夾，使用**Move-PublicFolderBranch.ps1**指令碼。

  - 移動公用資料夾時將只會移動公用資料夾的實體內容，而不會變更邏輯階層。

  - 視公用資料夾及其中包含的內容量的大小、 移動可能需要數小時才能完成。在該工作時，使用者將能夠存取公用資料夾。不過，使用者將無法存取簡短的期間內的公用資料夾時資料夾是在 「 完成進行中 」 狀態。

  - 您可以一次執行只有一個公用資料夾移動要求。您必須使用**Remove-PublicFolderMoveRequest**指令程式來完成後移除要求。

  - 若要檢查進行中之公用資料夾移動要求的狀態，請執行 [Get-PublicFolderMoveRequest](https://technet.microsoft.com/zh-tw/library/jj878076\(v=exchg.150\)) 指令程式。

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

## 移動單一公用資料夾

此範例會啟動將公用資料夾 \\CustomerEnagagements 從公用資料夾信箱 DeveloperReports 移至 DeveloperReports01 的要求

    New-PublicFolderMoveRequest -Folders \DeveloperReports\CustomerEngagements -TargetMailbox DeveloperReports01

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>作用中的移動要求時將會鎖定的目標公用資料夾信箱。</td>
</tr>
</tbody>
</table>


如需詳細的語法及參數資訊，請參閱 [New-PublicFolderMoveRequest](https://technet.microsoft.com/zh-tw/library/jj878081\(v=exchg.150\))。

## 移動多個公用資料夾

此範例一開始 \\Dev 公用資料夾分支下的目標公用資料夾信箱 DeveloperReports01 的公用資料夾移動要求。本範例會不會移動公用資料夾 \\Dev。

    New-PublicFolderMoveRequest -Folders \Dev\CustomerEngagements,\Dev\RequestsforChange,\Dev\Usability -TargetMailbox DeveloperReports01

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>作用中的移動要求時將會鎖定的目標公用資料夾信箱。</td>
</tr>
</tbody>
</table>


如需詳細的語法及參數資訊，請參閱 [New-PublicFolderMoveRequest](https://technet.microsoft.com/zh-tw/library/jj878081\(v=exchg.150\))。

## 移動公用資料夾的分支

此範例會使用`Move-PublicFolderBranch.ps1`指令碼來移動公用資料夾的分支。這會啟動公用資料夾 \\Dev 和所有子資料夾至公用資料夾信箱 DeveloperReports01 的移動要求。指令碼的 scripts 資料夾位於與必須從該位置執行。

    CD $env:ExchangeInstallPath\scripts
    
    .\Move-PublicFolderBranch.ps1 -FolderRoot \Dev -TargetPublicFolderMailbox DeveloperReports01

## 如何才能了解這是否正常運作？

若要確認公用資料夾移動要求成功，請執行下列命令：

    Get-PublicFolderMoveRequest | Format-List Status

當狀態為 `Completed` 時，表示移動要求成功。

如果不成功的移動要求，您可能需要還原公用資料夾或其內容。如需詳細資訊，請參閱[從失敗的移動還原公用資料夾和公用資料夾信箱](restore-public-folders-and-public-folder-mailboxes-from-failed-moves-exchange-2013-help.md)。

