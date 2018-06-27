---
title: '建立或移除就地保留: Exchange Online Help'
TOCTitle: 建立或移除就地保留
ms:assetid: 9d5d8d37-a053-4830-9cb1-6e1ede25e963
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd979797(v=EXCHG.150)
ms:contentKeyID: 50473850
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 建立或移除就地保留

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2017-01-18_

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>我們已延後 2017 年 7 月 1 日的期限以在 Exchange Online 中建立新的就地保留 (在 Office 365 和 Exchange Online 獨立計劃中)。但今年稍晚或明年初，您將無法在 Exchange Online 中建立新的就地保留。使用就地保留的替代方法是，您可以使用 <a href="https://go.microsoft.com/fwlink/?linkid=780738">eDiscovery 案例</a>或 Office 365 安全性和規範中心的<a href="https://go.microsoft.com/fwlink/?linkid=827811">保留原則</a>。在我們解除委任新就地保留後，您仍然可以修改現有的就地保留，而在 Exchange Server 2013 和 Exchange混合部署中建立新的就地保留仍會受到支援。而且，您依然能夠讓信箱處於「訴訟暫止」。</td>
</tr>
</tbody>
</table>


就地保留會保留所有信箱內容，包括已刪除的項目和已修改項目的原始版本。在[就地 eDiscovery](in-place-ediscovery-exchange-2013-help.md)搜尋會傳回所有這類信箱項目。 當您在使用者的信箱就地保留上放置時，相對應的封存信箱中的內容 （如果已啟用） 已也處於保留狀態，並傳回 eDiscovery 搜尋中。

## 開始之前有哪些須知？

  - 預估完成時間： 5 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「就地保留」項目。

  - 若要置於Exchange Online信箱就地保留功能，其必須被指派 Exchange Online (Plan 2) 授權。如果信箱指派 Exchange Online (計劃 1) 的授權，您必須將其放入個別 Exchange Online 封存授權保留指派。

  - 根據您的 Active Directory 拓撲和複寫延遲而定，就地保留的設定最長可能需要一小時後才會生效。

  - 如先前所述，當使用者的信箱上放置 \[就地保留使用者的封存信箱中的內容也處於保留狀態。如果您為 「 就地保留上放置Exchange混合部署的內部部署主要信箱、 雲端式封存信箱 （若啟用） 也被處於保留狀態。

  - 如果使用者處於多個就地保留，從任何查詢式保留搜尋查詢 （使用**OR**運算子） 結合。在此例中放置在信箱上所有查詢式保留的關鍵字數量上限為 500。如果有超過 500 個關鍵字，然後在信箱中的所有內容被處於保留狀態 （不只是符合搜尋準則的內容）。直到關鍵字的總數為 500 減少小於或等於會保留所有內容。

  - Exchange Online，在 \[可復原的項目\] 資料夾的配額自動增加為 100 GB 時您放在信箱上的 \[就地保留。可復原的項目\] 資料夾的預設大小為 30 GB。

  - 在Exchange Online，您可以在Office 365群組放置就地保留。當您保留上放置Office 365群組時，群組信箱處於保留狀態 ； 群組成員的信箱不處於保留狀態。 如需Office 365群組資訊，請參閱[了解 Office 365 群組](https://go.microsoft.com/fwlink/p/?linkid=724066)。

## 建立就地保留

**使用 EAC 建立就地保留**

1.  瀏覽至 \[規範管理\] \> \[就地 eDiscovery 和保留\]。

2.  按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

3.  在 \[就地 eDiscovery 和保留\] 中，\[名稱與描述\] 頁面，輸入一個搜尋名稱和選用描述，然後按一下 \[下一步\]。

4.  在 \[**信箱與公用資料夾**\] 頁面上選擇 \[您想要保留，然後按 \[**下一步\]**的內容位置\]。
    
    ![選擇要保留的內容位置](images/Dd979797.bbe76c50-a93b-4e5e-acd2-78e0d747ea19(EXCHG.150).png "選擇要保留的內容位置")  
    
    1.  **搜尋所有信箱**  您不能選取此選項可建立就地保留。您可以選取此選項就地 eDiscovery 搜尋，但您必須建立為 「 就地保留，選取您想要保留特定信箱。
    
    2.  **不要搜尋任何信箱**  當您建立的公用資料夾以獨佔模式就地保留選取此選項。
    
    3.  **指定信箱搜尋**  選取這個選項，然後按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")選取的信箱或您想要保留的通訊群組。中Exchange Online，也可以選取以保留Office 365群組。
    
    4.  **搜尋所有的公用資料夾**  您可以在Exchange Online、 選取此核取方塊可保留在組織中放置所有公用資料夾。如先前所述，若要建立僅適用於公用資料夾的就地保留，務必選取 \[**不要搜尋任何信箱**\] 選項。

5.  在 \[搜尋查詢\] 頁面，完成以下欄位，然後按一下 \[下一步\]：
    
      - \[包含所有使用者信箱內容\]   按一下這個按鈕將所有選定信箱中的內容設為保留。
    
      - **篩選依據準則**  按一下此按鈕可指定搜尋準則，包括關鍵字、 開始和結束日期、 寄件者和收件者的地址以及訊息類型。當您建立查詢式保留功能，只有符合的搜尋準則會保留的項目。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>當您將公用資料夾設就地保留時，也會保留與公用資料夾階層同步處理程序相關之電子郵件訊息。這可能會導致數千個階層同步處理相關電子郵件項目要保留。這些訊息可能會填滿儲存配額上公用資料夾信箱 [可復原的項目] 資料夾。若要避免此問題，您可以建立查詢式就地保留功能並將下列<code>property:value</code>配對新增至搜尋查詢：<br />
        <code>NOT(subject:HierarchySync*)</code><br />
        結果是 （的公用資料夾階層同步處理的相關） 包含片語&quot;HierarchySync&quot;主旨行中的並未圍繞在任何訊息保留。</td>
        </tr>
        </tbody>
        </table>


6.  在 \[就地保留設定\] 頁面上，勾選 \[將符合搜尋查詢的內容放入保留的所選信箱\] 核取方塊，然後選擇下列其中一個選項：
    
      - \[無限期保留\]   按一下此按鈕以將搜尋傳回項目設為無限期保留。 除非您從搜尋中移除信箱或移除搜尋，否則保留的項目會一直保存下來。
    
      - \[指定與項目收到日期相關的保留天數\] 按一下此按鈕將項目保留一段特定期間。 例如，若您的組織要求所有郵件都必須至少保存七年時，即可使用此選項。 您可使用「以時間為基礎」的就地保留和保留原則，以確保項目會在七年後受到刪除。 若要深入了解保留原則，請參閱[保留標記和保留原則](retention-tags-and-retention-policies-exchange-2013-help.md)。

**使用命令介面建立就地保留**

此範例會建立一個名為 Hold-CaseId012 的就地保留並新增 mailbox joe@contoso.com 到就地保留中。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若您未指定就地保留的搜尋參數，特定信箱的所有項目皆會被就地保留。 如果您未指定 <em>ItemHoldPeriod</em> 參數，所有項目都會被無限期保留，或者會被保留到該信箱從就地保留中移除或刪除就地保留時才終止保留。</td>
</tr>
</tbody>
</table>


    New-MailboxSearch "Hold-CaseId012"-SourceMailboxes "joe@contoso.com" -InPlaceHoldEnabled $true

如需詳細的語法及參數資訊，請參閱 [New-MailboxSearch](https://technet.microsoft.com/zh-tw/library/dd298064\(v=exchg.150\))。

**如何才能了解這是否正常運作？**

若要驗證是否成功建立就地保留，請執行以下其中一個操作：

  - 使用 EAC 驗證 \[就地 eDiscovery 和保留\] 索引標籤的清單檢視中是否列出該就地保留。

  - 使用 **Get-MailboxSearch** 指令程式 擷取信箱搜尋並查看搜尋參數。 如需如何擷取信箱搜尋的範例，請參閱 [Get-MailboxSearch](https://technet.microsoft.com/zh-tw/library/dd351021\(v=exchg.150\)) 中的範例。

返回頁首

## 刪除就地保留

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在 Exchange 2013 中，信箱搜尋可用於就地保留和就地 eDiscovery。 您無法移除就地保留所使用的信箱搜尋。 您必須先取消勾選 <strong>[就地保留設定]</strong> 頁面上的 <strong>[將符合搜尋查詢的內容放入保留的所選信箱]</strong> 核取方塊，或在命令介面中將 <em>InPlaceHoldEnabled</em> 參數設定為 <code>$false</code>，才能停用就地保留。 您也可以使用搜尋中所指定的 <em>SourceMailboxes</em> 參數來移除信箱。</td>
</tr>
</tbody>
</table>


**使用 EAC 移除就地保留**

1.  瀏覽至 \[規範管理\] \> \[就地 eDiscovery 和保留\]。

2.  在清單檢視中，選取您要移除的就地保留，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[就地 eDiscovery 和保留\] 屬性的 \[就地保留\] 頁面上，取消勾選 \[將符合搜尋查詢的內容放入保留的所選信箱\]，然後按一下 \[儲存\]。

4.  從清單檢視中再選擇一次就地保留，然後按一下 \[刪除\]![刪除圖示](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "刪除圖示")。

5.  在警告中，請按一下 \[是\] 移除搜尋。

**使用命令介面移除就地保留**

此範例會先停用名為 Hold-CaseId012 的就地保留，然後才移除信箱搜尋。

    Set-MailboxSearch "Hold-CaseId012"  -InPlaceHoldEnabled $false
    Remove-MailboxSearch "Hold-CaseId012"

如需詳細的語法及參數資訊，請參閱 [Set-MailboxSearch](https://technet.microsoft.com/zh-tw/library/dd335145\(v=exchg.150\))。

**如何才能了解這是否正常運作？**

若要驗證是否成功移除就地保留，請執行以下其中一個操作：

  - 使用 EAC，驗證 **\[就地 eDiscovery 和保留\]** 索引標籤的清單檢視中未列出該就地保留。

  - 使用 **Get-MailboxSearch** 指令程式擷取所有信箱搜尋並檢查您所移除的搜尋已不再列出。 如需如何擷取信箱搜尋的範例，請參閱 [Get-MailboxSearch](https://technet.microsoft.com/zh-tw/library/dd351021\(v=exchg.150\)) 中的範例。

返回頁首

