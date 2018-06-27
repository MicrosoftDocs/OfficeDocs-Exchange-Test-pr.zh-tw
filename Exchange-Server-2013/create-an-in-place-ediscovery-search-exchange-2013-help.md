---
title: '建立就地 eDiscovery 搜尋: Exchange Online Help'
TOCTitle: 建立就地 eDiscovery 搜尋
ms:assetid: feedc0c9-4a44-4bb2-8520-cc29d66d4fc3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd353189(v=EXCHG.150)
ms:contentKeyID: 50474690
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 建立就地 eDiscovery 搜尋

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2017-01-17_

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>我們已延後 2017 年 7 月 1 日的期限以在 Exchange Online 中建立新的就地 eDiscovery 搜尋 (在 Office 365 和 Exchange Online 獨立計劃中)。但今年稍晚或明年初，您將無法在 Exchange Online 中建立新的搜尋。若要建立 eDiscovery 搜尋，請開始在 Office 365 安全與規範中心中使用 [<a href="https://go.microsoft.com/fwlink/?linkid=847843">內容搜尋</a>]。在我們解除委任新就地 eDiscovery 搜尋後，您仍然可以修改現有的就地搜尋，而在 Exchange Server 2013 和 Exchange 混合部署中建立新的就地 eDiscovery 搜尋仍會受到支援。</td>
</tr>
</tbody>
</table>


使用[就地 eDiscovery](in-place-ediscovery-exchange-2013-help.md) 可搜尋所有信箱內容，包括使用者放入[就地保留與訴訟暫止](in-place-hold-and-litigation-hold-exchange-2013-help.md)的已刪除項目和已修改項目的原始版本。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「就地 eDiscovery」項目。

  - 若要建立 eDiscovery 搜尋，您有您正在建立中的搜尋組織中有 SMTP 位址。因此，在Exchange Online，必須已獲授權的 Exchange Online (Plan 2) 信箱建立 eDiscovery 搜尋。在 Exchange 混合式部署組織中您的內部部署 Exchange 信箱必須對應的郵件使用者帳戶貴組織中有Office 365 ，讓您可以搜尋Exchange Online信箱。或者，如果您使用只存在於Office 365，例如租用戶系統管理員帳戶\] 中的帳戶登入該帳戶必須具有的 Exchange Online (Plan 2) 授權。

  - Exchange 2013 安裝程式會建立名為 \[探索搜尋信箱\] 的探索信箱，用以複製搜尋結果。\[探索搜尋信箱\] 預設也會建立在 Exchange Online 中。您可以建立額外的探索信箱。如需詳細資訊，請參閱[建立探索信箱](create-a-discovery-mailbox-exchange-2013-help.md)。

  - 當您建立就地 eDiscovery 搜尋時，搜尋結果傳回的郵件並不會自動複製到探索信箱。在您建立搜尋後，可以使用 Exchange 系統管理中心 (EAC) 來預估及預覽搜尋結果，或將搜尋結果複製到探索信箱。如需詳細資訊，請參閱：
    
      - Estimate or preview search results (本主題稍後說明)
    
      - [將 eDiscovery 搜尋結果複製到探索信箱](copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md)

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


## 使用 EAC 建立就地 eDiscovery 搜尋

如先前所述，若要建立 eDiscovery 搜尋，您必須登入在您的組織中有 SMTP 位址的使用者帳戶。

1.  移至 \[規範管理\] \> \[就地 eDiscovery 和保留\]。

2.  按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

3.  在 \[就地 eDiscovery 和保留\] 中，於 \[名稱與描述\] 頁面上輸入搜尋的名稱，新增選用描述，然後按一下 \[下一步\]。

4.  在 \[**信箱**\] 頁面上選取的信箱搜尋。您可以搜尋所有信箱或選取要都搜尋的特定錯誤。在Exchange Online，您也可以選取Office 365群組以進行搜尋的內容來源。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>不可使用 [搜尋所有信箱] 選項將所有信箱設為保留。若要建立 In-Place Hold，需選擇 [指定信箱進行搜尋]。如需詳細資訊，請參閱<a href="create-or-remove-an-in-place-hold-exchange-2013-help.md">建立或移除就地保留</a>。</td>
    </tr>
    </tbody>
    </table>


5.  在 \[搜尋查詢\] 頁面上，填入下列欄位：
    
      - \[包含所有使用者信箱內容\]   選擇這個選項以將所有選定信箱中的內容設為保留。如果選取這個選項，便無法指定其他搜尋準則。
    
      - \[篩選依據準則\]   選擇這個選項以指定搜尋準則，包含關鍵字、開始與結束日期、寄件人與收件人地址以及訊息類型。
        
        ![設定 eDiscovery 搜尋查詢](images/Dd298021.a3626569-8700-421e-8b4e-7ec520b28272(EXCHG.150).png "設定 eDiscovery 搜尋查詢")  
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><strong>從︰</strong>和<strong>至 / [副本] / [密件副本︰</strong>欄位連線來執行搜尋時建立搜尋查詢中<strong>或</strong>運算子。這表示在搜尋結果中包含任何訊息傳送或接收的任何指定的使用者 （與符合項目的其他搜尋條件）。<br />
    由<strong>AND</strong>運算子連線的日期。</td>
    </tr>
    </tbody>
    </table>


6.  在 \[就地保留設定\] 頁面上，您可以選取 \[將符合搜尋查詢的內容放入保留的所選信箱\] 核取方塊，然後選取下列其中一個選項，用以將項目放入 \[就地保留\]：
    
      - \[無限期保留\]   選擇這個選項以將傳回項目設為無限期保留。除非您從搜尋中移除信箱或移除搜尋，否則保留的項目會一直保存下來。
    
      - \[指定與項目收到日期相關的保留天數\] 使用這個選項將項目保留一段特定期間。例如，若您的組織要求所有郵件都必須至少保存七年時，即可使用此選項。您可使用「以時間為基礎」的就地保留和保留原則，以確保項目會在七年後受到刪除。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>當為法律目的進行信箱或項目的 In-Place Hold 保留時，一般建議無限期保留項目並於案件或調查完成時移除保留。</td>
        </tr>
        </tbody>
        </table>


7.  按一下 \[完成\]，可儲存搜尋並傳回根據您指定之準則而進行的搜尋將傳回的預估總大小和項目數。估計結果會顯示在詳細資料窗格中。按一下 \[重新整理\]![重新整理圖示](images/Dn624163.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "重新整理圖示") 以更新在詳細資料窗格中顯示的資訊。

返回頁首

## 使用命令介面來建立就地 eDiscovery 搜尋

此範例會建立名為-CaseId012 可搜尋的項目包含關鍵字 Contoso 和 ProjectA 並也符合下列準則的就地 eDiscovery 搜尋：

  - 開始日期：1/1/2009

  - 結束日期：12/31/2011

  - 來源信箱：DG-Finance

  - 目標信箱：探索搜尋信箱

  - 郵件類型：Email

  - 包含無法搜尋的項目中的搜尋統計資料

  - 記錄層級：完整

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果不指定執行就地 eDiscovery 搜尋時的其他搜尋參數，則結果會傳回所指定來源信箱中的所有項目。如果不指定要搜尋的信箱，則會搜尋 Exchange 或 Exchange Online 組織中的所有信箱。</td>
</tr>
</tbody>
</table>


    New-MailboxSearch "Discovery-CaseId012" -StartDate "01/01/2009" -EndDate "12/31/2011" -SourceMailboxes "DG-Finance" -TargetMailbox "Discovery Search Mailbox" -SearchQuery '"Contoso" AND "Project A"' -MessageTypes Email -IncludeUnsearchableItems -LogLevel Full

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用 <em>StartDate</em> 和 <em>EndDate</em> 參數時，即使本機電腦設定已設為使用不同的日期格式 (如 dd/mm/yyyy)，您仍必須使用日期格式 mm/dd/yyyy。例如，若要搜尋在 2013 年 4 月 1 日與 2013 年 7 月 1 日之間傳送的郵件，您會使用 <strong>04/01/2013</strong> 和 <strong>07/01/2013</strong> 作為開始和結束日期。</td>
</tr>
</tbody>
</table>


此範例會建立名為電子郵件以 2015年傳送由 Alex Darrow Sara Davis HRCase090116 可以搜尋的就地 eDiscovery 搜尋。

    New-MailboxSearch "HRCase090116" -StartDate "01/01/2015" -EndDate "12/31/2015" -SourceMailboxes  alexd,sarad -SearchQuery 'From:alexd@contoso.com AND To:sarad@contoso.com' -MessageTypes Email -TargetMailbox "Discovery Search Mailbox" -IncludeUnsearchableItems -LogLevel Full

使用命令介面建立就地 eDiscovery 搜尋後，您必須使用 **Start-MailboxSearch** Cmdlet 開始搜尋，以將郵件複製到在 *TargetMailbox* 參數中指定的探索信箱。如需詳細資訊，請參閱[將 eDiscovery 搜尋結果複製到探索信箱](copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md)。

如需詳細的語法及參數資訊，請參閱 [New-MailboxSearch](https://technet.microsoft.com/zh-tw/library/dd298064\(v=exchg.150\))。

返回頁首

## 使用 EAC 預估或預覽搜尋結果

建立就地 eDiscovery 搜尋之後，您可以使用 EAC 取得搜尋結果的預估和預覽。如果您使用了 **New-MailboxSearch** Cmdlet 建立新搜尋，即可使用命令介面開始搜尋，以取得預估搜尋結果。您不能使用命令介面來預覽搜尋結果中傳回的郵件。

1.  瀏覽至 \[規範管理\] \> \[就地 eDiscovery 和保留\]。

2.  在清單檢視中，選取就地 eDiscovery 搜尋，並再執行下列其中一項：
    
      - 按一下 \[**搜尋**![搜尋圖示](images/Dn624163.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "搜尋圖示") \>**預估搜尋結果**傳回的估計項目總大小和搜尋將傳回的項目數根據您指定的準則。選取此選項，重新啟動搜尋並進行評估。
        
        預估搜尋結果會顯示在詳細資料窗格中。按一下 \[重新整理\]![重新整理圖示](images/Dn624163.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "重新整理圖示") 以更新在詳細資料窗格中顯示的資訊。
    
      - 按一下 \[**預覽搜尋結果**的詳細資訊窗格中預覽搜尋評估完成後的結果。選取此選項會開啟 \[ **eDiscovery 搜尋預覽**\] 視窗。會顯示所搜尋的信箱所傳回的所有郵件。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>所搜尋的信箱會列在 [eDiscovery 搜尋預覽] 視窗的右窗格中。針對每個信箱，也會顯示傳回的項目數目以及這些項目的總大小。搜尋傳回的所有項目都會列在右窗格中，並可依照最新或最舊的日期排序。按一下左窗格中的信箱，並無法讓各信箱中的項目顯示在右窗格中。若要檢視從特定信箱傳回的項目，您可以複製搜尋結果及檢視探索信箱中的項目。</td>
        </tr>
        </tbody>
        </table>
    
    ![預估或預覽搜尋結果](images/Dd353189.57e0fc2d-71bf-42aa-aa4b-4a77148f2b43(EXCHG.150).gif "預估或預覽搜尋結果")  

返回頁首

## 使用命令介面預估搜尋結果

您可以使用 *EstimateOnly* 參數，僅傳回預估搜尋結果，但不將結果複製到探索信箱。您必須利用 **Start-MailboxSearch** Cmdlet 來啟動僅限預估的搜尋。接著可使用 **Get-MailboxSearch** Cmdlet，擷取預估搜尋結果。

例如，您可執行下列命令來建立新的 eDiscovery 搜尋，然後顯示預估搜尋結果。

    New-MailboxSearch "FY13 Q2 Financial Results" -StartDate "04/01/2013" -EndDate "06/30/2013" -SourceMailboxes "DG-Finance" -SearchQuery '"Financial" AND "Fabrikam"' -EstimateOnly -IncludeKeywordStatistics

    Start-MailboxSearch "FY13 Q2 Financial Results"

    Get-MailboxSearch "FY13 Q2 Financial Results"

若要顯示先前範例中有關預估搜尋結果的特定資訊，您可以執行下列命令：

    Get-MailboxSearch "FY13 Q2 Financial Results" | FL Name,Status,LastRunBy,LastStartTime,LastEndTime,Sources,SearchQuery,ResultSizeEstimate,ResultNumberEstimate,Errors,KeywordHits

返回頁首

## eDiscovery 搜尋的詳細資訊

  - 建立新的 eDiscovery 搜尋後，即可將搜尋結果複製到探索信箱並將這些搜尋結果複製到 PST 檔案。如需詳細資訊，請參閱：
    
      - [將 eDiscovery 搜尋結果複製到探索信箱](copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md)
    
      - [將 eDiscovery 搜尋結果匯出至 PST 檔](export-ediscovery-search-results-to-a-pst-file-exchange-2013-help.md)

  - 執行 eDiscovery 搜尋評估 （其中包含關鍵字中的搜尋準則） 之後，您可以藉由選取搜尋的詳細資料窗格中按一下 \[**檢視關鍵字統計資料**檢視關鍵字統計資料。這些統計資料顯示詳細資料相關的每個關鍵字搜尋查詢中使用傳回的項目數。不過，如果在搜尋中包含 100 個以上的來源信箱，將會傳回錯誤如果您嘗試檢視關鍵字統計資料。若要檢視關鍵字統計資料，可以包含不超過 100 個來源信箱中搜尋。

  - 如果您使用**Get-MailboxSearch**Exchange Online中擷取的 eDiscovery 搜尋的相關資訊，您必須指定搜尋以返回搜尋屬性 ； 的完整清單的名稱例如， `Get-MailboxSearch "Contoso Legal Case"`。如果您執行**Get-MailboxSearch**指令程式不使用任何參數時，不傳回下列屬性：
    
      - SourceMailboxes
    
      - Sources
    
      - SearchQuery
    
      - ResultsLink
    
      - PreviewResultsLink
    
      - Errors
    
    原因是它需要大量的資源以傳回組織中所有的 eDiscovery 搜尋這些屬性。

返回頁首

