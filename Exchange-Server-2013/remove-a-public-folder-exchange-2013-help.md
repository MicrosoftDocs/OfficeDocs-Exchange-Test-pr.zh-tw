---
title: '移除公用資料夾: Exchange Online Help'
TOCTitle: 移除公用資料夾
ms:assetid: 334b831d-e372-4d85-a407-5c8a5d0e78de
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa997202(v=EXCHG.150)
ms:contentKeyID: 50472940
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 移除公用資料夾

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2016-11-16_

您可能需要在組織中移除不再使用的公用資料夾。若要協助您決定應該移除公用資料夾，請參閱[公用資料夾和公用資料夾項目的檢視統計資料](view-statistics-for-public-folders-and-public-folder-items-exchange-2013-help.md)。

如需與管理公用資料夾相關的其他管理工作，請參閱[公用資料夾程序](public-folder-procedures-exchange-2013-help.md)。

如需與公用資料夾相關的其他管理工作，請參閱 [Office 365 和 Exchange Online 中公用資料夾程序](https://technet.microsoft.com/zh-tw/library/jj966272\(v=exchg.150\))。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [共用和協同作業的權限](sharing-and-collaboration-permissions-exchange-2013-help.md)主題中的「公用資料夾」項目。

  - 您無法刪除擁有郵件功能的公用資料夾。您也可以將其刪除之前，您必須先停用公用資料夾的電子郵件。如需詳細資訊，請參閱[郵件啟用或停用郵件功能的公用資料夾](mail-enable-or-mail-disable-a-public-folder-exchange-2013-help.md)。

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

## 使用 EAC 移除共用資料夾

1.  瀏覽至 \[公用資料夾\] \> \[公用資料夾\]。

2.  在清單檢視中，選取您想要刪除的公用資料夾。請注意到的資料夾名稱上按一下 \[將會顯示該資料夾內的子資料夾如果有任何。在那個時候您可以按一下以選取要移除的特定子資料夾。
    
    若要刪除資料夾或子資料夾，請按一下任何地方上資料夾的資料列加上底線名稱以外的資料夾，然後按一下 \[**刪除**![刪除圖示](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "刪除圖示")。 如果您按一下加底線的資料夾名稱，將無法使用選取 \[**刪除**\] 選項。
    
    ![選取要移除的公用資料夾](images/Aa997202.8666290d-3f19-4c70-afe3-45569762718b(EXCHG.150).png "選取要移除的公用資料夾")  

3.  警告\] 方塊中顯示詢問您是否確定要刪除公用資料夾。按一下 \[**是\]**繼續。

## 使用命令介面刪除公用資料夾

此範例會刪除公用資料夾協助 Desk\\Resolved。此命令會假設已解決公用資料夾都不會有任何子資料夾。

    Remove-PublicFolder -Identity "\Help Desk\Resolved"

此範例會測試上述命令，而不進行任何修改。

    Remove-PublicFolder -Identity "\HelpDesk\Resolved" -WhatIf

此範例會移除公用資料夾 Marketing 及其所有子資料夾，因為命令會以遞迴方式執行。

    Remove-PublicFolder -Identity "\Marketing" -Recurse:$True

如需詳細的語法及參數資訊，請參閱 [Remove-PublicFolder](https://technet.microsoft.com/zh-tw/library/bb124894\(v=exchg.150\))。

