---
title: '設定佇列檢視器選項: Exchange 2013 Help'
TOCTitle: 設定佇列檢視器選項
ms:assetid: 03a9134c-0714-4c13-b286-92bccc7ec05e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa995934(v=EXCHG.150)
ms:contentKeyID: 50472474
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定佇列檢視器選項

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-03_

您可以調整的頁面顯示的項目數的佇列檢視器中設定選項，並調整自動重新整理的間隔。自動重新整理的間隔會決定在佇列檢視器結果更新的頻率。

## 開始之前有哪些須知？

  - 預估完成時間：10 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「佇列」項目。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 使用 \[Exchange 工具箱\] 設定佇列檢視器選項

1.  按一下 \[開始\] \> \[所有程式\] \> \[Microsoft Exchange Server 2013\] \> \[Exchange 工具箱\]。

2.  在 \[郵件流程工具\] 區段中，按兩下 \[佇列檢視器\]。

3.  在佇列檢視器中，按一下 \[檢視\] \> \[選項\] 來設定 \[佇列檢視器選項\] 對話方塊中的以下設定：
    
    1.  在 \[重新整理間隔 (秒)\] 欄位中輸入佇列檢視器應該更新顯示的頻率。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>預設自動重新整理的間隔為 30 秒，因此無法設定較短時間。如果您停用自動重新整理功能清除 [<strong>佇列檢視器選項</strong>] 頁面上的 [<strong>自動重新整理畫面</strong>] 核取方塊，您必須手動更新依序按一下 [<strong>重新整理</strong>佇列檢視器中顯示的結果。</td>
        </tr>
        </tbody>
        </table>
    
    2.  **若要在每一頁上顯示的項目數**\] 欄位中輸入佇列檢視器中顯示的項的目數上限。此號碼必須是介於 1 到 10000。如果您有多個項目大於此限制，您會看到的項目數上限的群組中的項目。例如下, 圖顯示與設定為 10 個項目顯示在每一頁上的佇列檢視器中 14 郵件的佇列。頁面上物件的數目會顯示在右上方。在頁面的底端，您可以看到佇列中的項目的總數。您可以查看佇列中的其他項目使用的導覽控制項。

4.  完成後，請按一下 \[確定\]。
    
    **佇列檢視器**
    
    ![含有比項目限制更多項目的佇列檢視器](images/Aa995934.e82196e6-002a-4e9e-823d-b244b0bd25e2(EXCHG.150).gif "含有比項目限制更多項目的佇列檢視器")  

## 如何才能了解這是否正常運作？

當佇列檢視器使用重新整理的間隔與每頁項目數量等設定時，即可知道此程序是否正確執行。

