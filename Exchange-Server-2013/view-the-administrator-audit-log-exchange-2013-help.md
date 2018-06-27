---
title: '檢視系統管理員稽核記錄: Exchange Online Help'
TOCTitle: 檢視系統管理員稽核記錄
ms:assetid: 5c62072a-556d-4fea-9973-d668c6b9fd57
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn342832(v=EXCHG.150)
ms:contentKeyID: 56269008
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 檢視系統管理員稽核記錄

 

_**適用版本：**Exchange Online, Exchange Online Protection, Exchange Server 2013_

_**上次修改主題的時間：**2016-05-03_

在 Microsoft Exchange Online Protection (EOP)、Microsoft Exchange Online 和 Microsoft Exchange 2013 中，您可以使用 Exchange 系統管理中心 (EAC) 搜尋並檢視*系統管理員稽核記錄*中的項目。系統管理員稽核記錄會按照 Exchange 管理命令介面 Cmdlet，記錄由系統管理員以及已被指派系統管理權限的使用者所執行的特定動作。系統管理員稽核記錄中的項目會提供執行的 Cmdlet、使用的參數、Cmdlet 的執行者，以及受影響的物件的相關資訊。

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>系統管理員稽核記錄已根據預設啟用。</p></li>
<li><p>系統管理員稽核記錄不會記錄以 Exchange 管理命令介面 Cmdlet 為基礎且以 <strong>Get</strong>、<strong>Search</strong> 或 <strong>Test</strong> 動詞命令為開頭的動作。</p></li>
<li><p>稽核記錄項目會保留 90 天的時間。超過 90 天的項目就會遭到刪除。</p></li>
</ul></td>
</tr>
</tbody>
</table>


## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [EOP 中的功能權限](https://technet.microsoft.com/zh-tw/library/jj723125\(v=exchg.150\))主題中的「檢視報告」項目。

  - 如同先前所述，系統管理員稽核記錄已根據預設啟用。 若要確認已啟用系統管理員稽核記錄，您可以執行下列命令。
    
        Get-AdminAuditLogConfig | FL AdminAuditLogEnabled
    
    在 Exchange 2013 中，如果已執行下列命令停用系統管理員稽核記錄，您可以將其啟用。
    
        Set-AdminAuditLogConfig -AdminAuditLogEnabled $True
    
    在 Exchange Online Protection 和 Exchange Online 中，系統管理員稽核記錄一律啟用。無法將其停用。

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


## 使用 EAC 檢視系統管理員稽核記錄

1.  在 EAC 中，移至 \[**規範管理**\] \> \[**稽核**\]，然後選擇 \[**執行系統管理員稽核記錄回報**\]。

2.  選擇 \[開始日期\] 和 \[結束日期\]，然後選擇 \[搜尋\]。在指定期間進行的所有組態變更都會顯示出來，而且可以使用下列資訊進行排序：
    
      - **日期**   進行組態變更的日期及時間。日期和時間會以格林威治標準時間 (UTC) 格式儲存。
    
      - **Cmdlet**   進行組態變更所用的 Cmdlet 名稱。
    
      - **使用者**   進行組態變更的使用者帳戶名稱。
    
    可在多個頁面上顯示最多 5000 個項目。如果需要縮小搜尋結果，請指定較小的日期範圍。如果您選取個別的搜尋結果，下列其他資訊會顯示在詳細資料窗格中：
    
      - **修改的物件**   Cmdlet 修改的物件。
    
      - **參數 (參數:值)**   使用的 Cmdlet 參數和參數指定的任何值。

3.  如果您要列印特定的稽核記錄項目，請選擇詳細資料窗格中的 \[**列印**\] 按鈕。

## 如何知道這是否正常運作？

如果您已成功執行系統管理員稽核記錄報告，在您指定的日期範圍內進行的組態變更會顯示在搜尋結果窗格中。如果沒有結果，請變更日期範圍，然後再次執行報告。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在組織中所進行的變更最長可能需要 15 分鐘才會出現在稽核記錄搜尋結果中。如果變更未出現在系統管理員稽核記錄中，請等待幾分鐘再重新執行搜尋。</td>
</tr>
</tbody>
</table>

