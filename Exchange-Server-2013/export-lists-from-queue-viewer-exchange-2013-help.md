---
title: '從佇列檢視器中匯出清單: Exchange 2013 Help'
TOCTitle: 從佇列檢視器中匯出清單
ms:assetid: dcb829cd-0ffd-4ea9-ac3e-eaac5a8d1194
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb691328(v=EXCHG.150)
ms:contentKeyID: 50474392
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 從佇列檢視器中匯出清單

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-09-25_

這個主題說明如何使用 Exchange 工具箱中的佇列檢視器匯出郵件或佇列的清單。

您可以將清單匯出至下列檔案格式：

  - 文字 (Tab 鍵分隔)

  - 文字 (逗號分隔)

  - Unicode 文字 (Tab 鍵分隔)

  - Unicode 文字 (逗號分隔)

## 開始之前有哪些須知？

  - 預估完成時間：10 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)中的「佇列」項目。

  - 根據預設，佇列檢視器中的 \[結果\] 窗格會顯示前 1000 的物件。若要變更此值，請參閱[設定佇列檢視器選項](set-queue-viewer-options-exchange-2013-help.md)。

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


## 從佇列檢視器的結果窗格中匯出清單

1.  按一下 \[開始\] \> \[所有程式\] \> \[Microsoft Exchange 2013\] \> \[Exchange 工具箱\]。

2.  在 \[郵件流程\] 區段中，連按兩下 \[佇列檢視器\] 。

3.  佇列檢視器中選取 \[**佇列**\] 索引標籤或 \[**訊息**\] 索引標籤。其中一個索引標籤上，您可以按一下 \[**建立篩選器**來限制結果。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果重新整理 [結果] 窗格不、 在 [動作] 窗格中，按一下 [<strong>重新整理</strong>]。較長清單可能需要數分鐘才能重新整理。</td>
    </tr>
    </tbody>
    </table>


4.  在 \[動作\] 窗格中，按一下 \[**匯出\] 清單中**。**匯出清單**\] 對話方塊隨即出現。

5.  在 \[匯出清單\] 的 \[檔案名稱\] 方塊中輸入檔案名稱，然後從 \[另存類型\] 清單中選取檔案格式。

6.  按一下 \[儲存\]。

