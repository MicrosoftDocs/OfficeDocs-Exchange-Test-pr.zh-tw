---
title: '修改封存原則: Exchange Online Help'
TOCTitle: 修改封存原則
ms:assetid: 1e3002c2-801a-43ea-ae00-52ab34d76b9c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh529919(v=EXCHG.150)
ms:contentKeyID: 50472784
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 修改封存原則

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2016-02-01_

在Exchange Server 2013和Exchange Online，您可以使用自動將信箱項目移至個人 （內部） 或雲端式封存的封存原則。封存原則是使用 \[**移至封存**\] 保留動作的保留標記。

Exchange 安裝程式會建立稱為 「**預設 MRM 原則**的保留原則。此原則具有預設原則標記 (DPT) 指派的兩個年度之後將項目移至封存信箱。原則也包含數個人標記的使用者可以自動套用至要採用資料夾或信箱項目移動或刪除的郵件。如果信箱都不會有保留原則指派啟用封存時，**預設 MRM 原則**會自動套用至其，由 Exchange。您也可以建立您自己的封存和保留原則並將其套用到信箱使用者。若要深入了解，請參閱[保留標記和保留原則](retention-tags-and-retention-policies-exchange-2013-help.md)。

您可以修改包含在預設原則來符合您的業務需求的保留標記。例如，您可以修改將項目移至封存而不是兩個三年後封存 DPT。您也可以建立額外的個人標記和 \[將其新增至保留原則，包括**預設 MRM 原則**，或允許使用者從Outlook Web App選項新增至其信箱的個人標記。

封存與相關的其他管理工作，請參閱：

  - **Exchange Server 2013:** [管理 Exchange 2013 中的就地封存](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md)

  - **Exchange Online:** [在 Exchange Online 中啟用或停用封存信箱](https://technet.microsoft.com/zh-tw/library/jj984357\(v=exchg.150\))

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您可以在Exchange混合式部署中，啟用雲端式封存信箱的內部部署主要信箱。如果您將封存原則指派給內部部署信箱，項目所移至雲端式封存。如果項目移至封存信箱時，其複本不保留在內部部署信箱。如果內部部署信箱處於保留狀態，封存原則仍會指定保留期間的保留位置的雲端式封存信箱移動項目。</td>
</tr>
</tbody>
</table>


## 開始之前有哪些須知？

  - 預估完成時間： 5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「通訊記錄管理」項目。

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

## 使用 EAC 修改預設封存原則

1.  瀏覽至 \[規範管理\] \> \[保留標記\]。

2.  在清單檢視中，選擇標記 \[預設 2 年移至封存\] 然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您可以按一下 [<strong>類型</strong>] 欄排序依類型的保留標記。預設封存原則會顯示為<strong>預設</strong>類型，且<strong>封存</strong>] 保留動作。或者，按一下要依名稱排序保留標記的<strong>名稱</strong>。</td>
    </tr>
    </tbody>
    </table>


3.  
    
    在 \[保留標記\]，檢視或修改下列設定，然後按一下 \[儲存\]：
    
      - \[名稱\]   使用頁面上方這個方塊，即可檢視或變更標記名稱。
    
      - \[保留標記類型\]   此唯讀欄位將顯示標記類型。
    
      - \[保留動作\]   不要為封存原則修改此欄位。
    
      - **保留期間**：選取下列其中一個選項：
        
          - **永不**  按一下此按鈕可停用標記。如果已停用 DPT，標記不再套用至信箱。
            
            <table>
            <thead>
            <tr class="header">
            <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
            </tr>
            </thead>
            <tbody>
            <tr class="odd">
            <td>已套用已停用的保留標記的項目未處理的信箱助理員。若要防止標籤套用到項目，則建議您停用標記而不是刪除它。當您刪除標記時、 標記設定會從 Active Directory、 刪除及信箱助理員處理所有訊息都要移除已刪除的標籤。</td>
            </tr>
            </tbody>
            </table>
            
            <table>
            <thead>
            <tr class="header">
            <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
            </tr>
            </thead>
            <tbody>
            <tr class="odd">
            <td>如果使用者將標記套用到項目，認為該項目永不會移動，則稍後啟用該標記可能會移動使用者原本想保留在主要信箱的項目。</td>
            </tr>
            </tbody>
            </table>
        
          - **當項目達到下列年齡 （天數）**  按一下此按鈕可指定項目要移至封存一段期間後。根據預設，此設定會設定為將郵件移至封存的兩個年度 （730 天） 後。若要修改此設定，在相對應的文字方塊中，輸入天數中的保留期間。值的範圍是從 1 到 24,855 天。
    
      - \[註解\]   使用這個方塊，輸入 Outlook 和 Outlook Web App 使用者會看到的註解。

## 使用命令介面修改封存原則

本範例將 `Default 2 year move to archive` 標記修改為 1095 天 (3 年) 後移動項目。

    Set-RetentionPolicyTag "Default 2 year move to archive" -Name "Default 3 year move to archive" -AgeLimitForRetention 1095

本範例會停用 `Default 2 year move to archive` 標記。

    Set-RetentionPolicyTag "Default 2 year move to archive" -RetentionEnabled $false

本範例擷取所有封存 DPT 與個人標記並予以停用。

    Get-RetentionPolicyTag | ? {$_.RetentionAction -eq "MoveToArchive"} | Set-RetentionPolicyTag -RetentionEnabled $false

如需詳細的語法及參數資訊，請參閱 [Set-RetentionPolicyTag](https://technet.microsoft.com/zh-tw/library/dd298042\(v=exchg.150\)) 與 [Get-RetentionPolicyTag](https://technet.microsoft.com/zh-tw/library/dd298009\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

使用 [Get-RetentionPolicyTag](https://technet.microsoft.com/zh-tw/library/dd298009\(v=exchg.150\)) 指令程式來擷取保留標記設定。

此指令擷取 `Default 2 year move to archive` 保留標記的屬性，並以管線傳輸輸出至 **Format-List** 指令程式以透過清單格式顯示所有屬性。

    Get-RetentionPolicyTag "Default 2 year move to archive" | Format-List

