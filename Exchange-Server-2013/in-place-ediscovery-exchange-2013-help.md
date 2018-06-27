---
title: '就地 eDiscovery: Exchange Online Help'
TOCTitle: 就地 eDiscovery
ms:assetid: 6377cb7a-3416-4e15-8571-c45d2160fc6f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd298021(v=EXCHG.150)
ms:contentKeyID: 50473341
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 就地 eDiscovery

 

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


如果您的組織遵守法律調查需求 （相關機構政策、 規範、 或訴訟）、 Microsoft Exchange Server 2013和Exchange Online中的就地 eDiscovery 可協助您執行探索搜尋信箱內的相關內容。Exchange 2013和Exchange Online也提供同盟的搜尋功能，與Microsoft SharePoint 2013和Microsoft SharePoint Online整合。使用 SharePoint eDiscovery 中心，您可以搜尋並保留案例，包括SharePoint 2013和SharePoint Online網站、 文件、 SharePoint (SharePoint 2013只)，以編製索引的檔案共用中Exchange、 信箱內容和封存的Lync 2013內容相關的所有內容。您也可以使用 Exchange 混合式環境中的就地 eDiscovery 來搜尋中相同的搜尋內部部署和雲端架構信箱。

**目錄**

How In-Place eDiscovery works

Exchange Search

Discovery Management role group and management roles

Custom management scopes for In-Place eDiscovery

Integration with SharePoint Server 2013 and SharePoint Online

eDiscovery in an Exchange hybrid deployment

Discovery mailboxes

Using In-Place eDiscovery

Estimate, preview, and copy search results

Export search results to a PST file

Different search results

Logging for In-Place eDiscovery searches

In-Place eDiscovery and In-Place Hold

Preserving mailboxes for In-Place eDiscovery

In-Place eDiscovery limits and throttling policies

In-Place eDiscovery documentation

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>就地 eDiscovery 是一個強大的功能，可讓具有正確權限的使用者得以存取整個 Exchange 2013 或 Exchange Online 組織中所儲存的所有通訊記錄。這對於控制與監視探索活動而言很重要，包括將成員新增至探索管理角色群組、指派信箱搜尋管理角色，以及指派探索信箱的信箱存取權限。</td>
</tr>
</tbody>
</table>


## 就地 eDiscovery 運作方式

就地 eDiscovery 使用 Exchange 搜尋所建立的內容索引。角色存取控制 (RBAC) 可提供 [探索管理](discovery-management-exchange-2013-help.md) 角色群組，以便將探索工作委派給非技術人員，但不會提供較高的權限讓使用者能對 Exchange 組態進行任何作業上的變更。Exchange 系統管理中心 (EAC) 針對非技術人員，例如法務人員、記錄管理員與人力資源 (HR) 專業人員，提供一個簡單易用的搜尋介面。

授權的使用者若要執行就地 eDiscovery 搜尋，可先選取信箱，再指定搜尋準則，例如關鍵字、開始和結束日期、寄件者和收件者地址，以及郵件類型。搜尋完成之後，授權的使用者接著可再選取下列其中一個動作：

  - **估計搜尋結果**   此選項可傳回根據您指定之準則而進行的搜尋將傳回的估計項目總大小和項目數。

  - **預覽搜尋結果**   此選項可預覽結果。並顯示從每個搜尋信箱所傳回的郵件。

  - **複製搜尋結果：**此選項可將郵件複製到探索信箱。

  - **匯出搜尋結果**  搜尋結果複製到探索信箱後，您可以將其匯出至 PST 檔案。

![預估、預覽、複製和匯出搜尋結果](images/Dd298021.6356971a-34ed-4586-8229-030448d4fe2d(EXCHG.150).gif "預估、預覽、複製和匯出搜尋結果")

## Exchange 搜尋

就地 eDiscovery 使用 Exchange 搜尋所建立的內容索引。Exchange 搜尋經過改良，可使用 Microsoft Search Foundation。這是一個豐富的搜尋平台，已大幅提升索引和查詢效能，並改善搜尋功能。因為其他 Office 產品也使用 Microsoft Search Foundation，包括 SharePoint 2013，它能讓這些產品有更好的互通性，並使用相似的查詢語法。

透過使用單一內容索引引擎，當 IT 部門收到 eDiscovery 要求時，不需使用任何額外的資源即可針對就地 eDiscovery 進行信箱資料庫的編目與索引建立工作。

就地 eDiscovery 使用關鍵字查詢語法 (KQL)，此查詢語法與 Microsoft Outlook 和 Outlook Web App 中的立即搜尋功能所用的進階查詢語法 (AQS) 相似。熟悉 KQL 的使用者能夠輕鬆的建構強大的搜尋查詢來搜尋內容索引。

如需 Exchange 搜尋可編製索引的檔案格式的相關資訊，請參閱[依 Exchange 搜尋編製索引的檔案格式](file-formats-indexed-by-exchange-search-exchange-2013-help.md)。

## 探索管理角色群組和管理角色

為了讓經過授權的使用者執行就地 eDiscovery，您必須將他們新增至[探索管理](discovery-management-exchange-2013-help.md)角色群組。此角色群組包含兩個管理角色，一個是[信箱搜尋角色](mailbox-search-role-exchange-2013-help.md)，它允許使用者執行就地 eDiscovery，另一個是[法律保留角色](legal-hold-role-exchange-2013-help.md)，它允許使用者將信箱設為就地保留或訴訟暫止狀態。

依預設，執行就地 eDiscovery 相關工作的權限未指派給任何使用者或 Exchange 系統管理員。Exchange 系統管理員為組織管理群組的成員，能將使用者新增至探索管理角色群組，並建立自訂角色群組，將探索管理員的範圍縮小到一部分使用者。若要深入了解將使用者新增至探索管理角色群組，請參閱[Exchange 中指派 eDiscovery 權限](assign-ediscovery-permissions-in-exchange-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果使用者尚未新增至探索管理角色群組，或未被指派信箱搜尋角色，則 EAC 中不會顯示 <strong>[就地 eDiscovery &amp; 保留]</strong> 使用者介面，在 Exchange 管理命令介面中也無法使用就地 eDiscovery 指令程式。</td>
</tr>
</tbody>
</table>


稽核 RBAC 角色的改變 (預設為啟用)，可確保保有充足的記錄可供追蹤探索管理角色群組的指派。您可以利用系統管理員角色群組報告來搜尋系統管理員角色群組的變更。如需詳細資訊，請參閱 [搜尋角色群組變更或管理員稽核記錄檔](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md)。

回到頁首

## 就地 eDiscovery 的自訂管理範圍

您可以使用自訂管理範圍讓特定人員或群組使用「就地 eDiscovery」，在您的 Exchange 2013 或 Exchange Online 組織中搜尋信箱子集。例如，您可以讓探索管理員只在特定位置或部門中搜尋使用者的信箱。若要這麼做，您可以建立自訂管理範圍，利用自訂的收件者篩選器來控制可搜尋的信箱。收件者篩選器範圍使用篩選器，根據收件者類型或其他收件者屬性，鎖定以特定的收件者為目標。

在「就地 eDiscovery」中，使用者信箱上只有通訊群組成員資格這個屬性可用來建立自訂範圍的收件者篩選器。如果您使用其他屬性 (例如 *CustomAttributeN*、*Department* 或 *PostalCode*)，則獲指派自訂範圍的角色群組成員執行搜尋時會失敗。如需詳細資訊，請參閱 [建立就地 eDiscovery 搜尋的自訂管理範圍](create-a-custom-management-scope-for-in-place-ediscovery-searches-exchange-2013-help.md)。

## 與 SharePoint Server 2013 和 SharePoint Online 整合

Exchange 2013 和 Exchange Online 提供與 SharePoint 2013 和 SharePoint Online 整合功能，允許探索管理員使用 SharePoint 中的 eDiscovery 中心來執行下列工作：

  - **從單一位置搜尋並保存內容**授權的探索管理員能透過 SharePoint 與 Exchange 搜尋並保存內容，包括 Lync 內容，如立即訊息交談和在 Exchange 信箱中所封存的共用會議文件。

  - **專案管理** eDiscovery 中心使用 eDiscovery 的專案管理方式，讓您建立專案，並針對每件專案在不同內容存放庫間搜尋並保存內容。

  - **匯出搜尋結果**探索管理員可使用 eDiscovery 中心來匯出搜尋結果。將包含在搜尋結果中的信箱內容匯出至 PST 檔案。

SharePoint 也使用 Microsoft Search Foundation 進行內容索引和查詢。不論探索管理員使用的是 EAC 或 eDiscovery 中心搜尋 Exchange 內容，皆會傳回相同的信箱內容。

在內部部署中，您必須在兩個應用程式之間建立信任，才能使用 SharePoint 中的 eDiscovery 中心搜尋 Exchange 信箱。在 Exchange 2013 和 SharePoint 2013 之中，是透過使用 OAuth 驗證來完成。如需詳細資料，請參閱[設定 Exchange for SharePoint eDiscovery Center](configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md)。從 SharePoint 執行的 eDiscovery 搜尋由 Exchange 使用 RBAC 進行授權。SharePoint 使用者必須在 Exchange 中獲指派委派的探索管理權限，才能夠執行 Exchange 信箱的 eDiscovery 搜尋。探索管理員必須在相同的 Exchange 組織中擁有信箱，才能預覽以 SharePoint eDiscovery 中心執行 eDiscovery 搜尋所傳回的信箱內容。

步驟逐步指示中設定 eDiscovery 中心的 Office 365 組織中的設定，請參閱[設定 SharePoint Online 中的 eDiscovery 中心](https://go.microsoft.com/fwlink/p/?linkid=331600)。

## Exchange 混合部署中的 eDiscovery

若要在 Exchange 2013 混合組織中順利執行跨單位 eDiscovery 搜尋，您必須在您的 Exchange 內部部署組織與 Exchange Online 組織之間設定 OAuth (Open Authorization)，以便能使用就地 eDiscovery 搜尋內部部署與雲端信箱。OAuth 驗證是伺服器對伺服器的驗證通訊協定，可讓應用程式相互驗證。

OAuth 驗證在 Exchange 混合部署支援下列的 eDiscovery 案例：

  - 搜尋將「Exchange Online 封存」用於雲端封存信箱的內部部署信箱。

  - 在相同的 eDiscovery 搜尋中，搜尋內部部署和雲端信箱。

  - 在 SharePoint Online 中使用 eDiscovery 中心搜尋內部部署信箱。

若想進一步了解必須在 Exchange 混合部署中設定 OAuth 驗證的 eDiscovery 案例，請參閱[在 Exchange 混合式部署中使用 OAuth 驗證來支援 eDiscovery](using-oauth-authentication-to-support-ediscovery-in-an-exchange-hybrid-deployment-exchange-2013-help.md)。如需設定 OAuth 驗證以支援 eDiscovery 的逐步指示，請參閱[設定 Exchange 與 Exchange Online 組織之間的 OAuth 驗證](configure-oauth-authentication-between-exchange-and-exchange-online-organizations-exchange-2013-help.md)。

## 探索信箱

建立就地 eDiscovery 搜尋之後，您可以將搜尋結果複製到目標信箱。EAC 允許您選取探索信箱作為目標信箱。探索信箱是特殊類型的信箱，可提供下列功能：

  - **更容易且安全地選擇目標信箱：**當您使用 EAC 複製就地 eDiscovery 搜尋結果時，只會提供探索信箱作為儲存搜尋結果的存放庫。您不需要在一長串的組織可用信箱清單中分類整理，探索管理員也不會不小心選取其他使用者的信箱或是不安全的信箱來儲存機密的郵件。

  - **信箱儲存配額大：**目標信箱應能夠儲存大量由就地 eDiscovery 搜尋傳回的郵件資料。依預設，探索信箱擁有 50 GB 的信箱儲存配額。無法增加此儲存配額。

  - **預設更安全的保護**  就像所有類型的信箱一樣，探索信箱也有相關聯的 Active Directory 使用者帳戶。但這個帳戶預設為停用，只有獲得明確授權存取探索信箱的使用者能夠存取該帳戶。探索管理角色群組的成員都會獲得預設探索信箱的完整存取權限。任何您建立的其他探索信箱皆未有已指派給任何使用者的信箱存取權限。

  - **停用電子郵件傳遞：**雖然使用者會出現在 Exchange 通訊清單中，但無法將電子郵件傳送至探索信箱。使用傳遞限制可禁止將電子郵件傳遞至探索信箱，這可保留複製到探索信箱的搜尋結果的完整性。

Exchange 2013 安裝程式會建立一個探索信箱，其顯示名稱為 **\[探索搜尋信箱\]**。您可以使用命令介面建立其他的探索信箱。依預設，您建立的探索信箱不會指派任何信箱存取權限。您可以指派完整存取權限給探索管理員，以存取複製到探索信箱的郵件。如需詳細資訊，請參閱[建立探索信箱](create-a-discovery-mailbox-exchange-2013-help.md)。

就地 eDiscovery 也會使用顯示名稱為 **SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}** 的系統信箱，以保存就地 eDiscovery 中繼資料。系統信箱在 EMC 或 Exchange 通訊清單中不會顯示。在內部部署組織中，在移除就地 eDiscovery 系統信箱所在的信箱資料庫之前，您必須先將信箱移至其他信箱資料庫。如果信箱已移除或已損壞，則在重新建立信箱之前，探索管理員將無法執行 eDiscovery 搜尋。如需詳細資訊，請參閱[重新建立探索系統信箱](re-create-the-discovery-system-mailbox-exchange-2013-help.md)。

回到頁首

## 使用就地 eDiscovery

已新增至探索管理角色群組的使用者可執行就地 eDiscovery 搜尋。您能使用 EAC 中的 Web 介面來執行搜尋。這會讓如記錄管理員、法務人員，或法律與人力資源專家等非技術使用者更容易使用就地 eDiscovery。您也可以使用命令介面來執行搜尋。如需詳細資訊，請參閱[建立就地 eDiscovery 搜尋](create-an-in-place-ediscovery-search-exchange-2013-help.md)

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在內部部署組織中，您可以使用就地 eDiscovery 來搜尋位於 Exchange 2013 Mailbox Server 上的信箱。若要搜尋位於 Exchange 2010 Mailbox Server 的信箱，請使用 Exchange 2010 伺服器上的多信箱搜尋。<br />
對於部分信箱存在於您內部部署信箱伺服器，而部分信箱則是存在於雲端式組織中的混合部署而言，您能使用您內部部署組織裡的 EAC 去執行雲端式信箱的就地 eDiscovery 搜尋。若您想將郵件複製到一個探索信箱，您必須選取一個內部部署探索信箱。在雲端式信箱中，自搜尋結果傳回的郵件會被複製到指定的內部部署探索信箱。若要深入了解混合部署，請參閱<a href="https://technet.microsoft.com/zh-tw/library/jj200581(v=exchg.150)">Exchange Server 混合部署</a>。</td>
</tr>
</tbody>
</table>


EAC 中的 **\[就地 eDiscovery & 保留\]** 精靈讓您能建立就地 eDiscovery 搜尋，也能使用就地保留功能將搜尋結果設為保留狀態。當您建立就地 eDiscovery 搜尋時，就地 eDiscovery 系統信箱中會建立搜尋物件。使用者可操控此物件來開始、停止、修改與移除搜尋，建立搜尋後，您可以選擇預估搜尋結果，包括可判斷查詢效率的關鍵字統計資料。您也能即時預覽搜尋傳回的項目，讓您能檢視郵件內容、從每個來源信箱傳回的郵件數和郵件總數。如有需要，您能使用此資訊進一步微調查詢。

對搜尋結果感到滿意時，您能將其複製到探索信箱。您也能使用 EAC 或 Outlook 匯出探索信箱或部分內容至 PST 檔案。

建立就地 eDiscovery 搜尋時，您必須指定下列參數：

  - **名稱** 用來識別搜尋的搜尋名稱。當您複製搜尋結果至探索信箱時，將使用該搜尋名稱和時戳，在探索信箱中建立一個資料夾，以在探索信箱中唯一性地識別搜尋結果。

  - **信箱**  您可以選擇搜尋Exchange 2013或Exchange Online在組織中所有信箱，或指定要都搜尋的信箱。 使用者的主要和封存信箱都包含在搜尋。如果您也想要使用相同的搜尋項目放入保留，您必須指定信箱。您可以指定要包含該群組之成員的信箱使用者的通訊群組。建立搜尋時一次計算群組的成員資格與群組成員資格的後續變更不會自動反映在搜尋\]。
    
    在Exchange Online，您也可以指定Office 365群組作為內容來源以便群組信箱是搜尋 （或處於保留狀態）。當您新增Office 365群組的就地 eDiscovery 搜尋時，只群組信箱搜尋 ；群組成員的信箱不搜尋。

  - **搜尋查詢** 您可從指定信箱中包含所有信箱內容或是使用搜尋查詢來傳回與專案或調查更為相關的項目。您可以在搜尋查詢中指定下列參數：
    
      - **關鍵字** 您可以指定用於搜尋訊息內容的關鍵字與片語。您也可以使用邏輯運算子 **AND**、**OR** 和 **NOT**。而且，Exchange 2013 也支援 **NEAR** 運算子，讓您能搜尋與其他字或片語相近的字或片語。
        
        若要搜尋完全符合的多字片語，則必須用引號括住片語。例如，若搜尋片語 \&quot;plan and competition\&quot;，則會將其中有完全符合片語的郵件傳回，若是指定 **plan AND competition**，則會將郵件中任何一處有 **plan** 與 **competition** 的郵件傳回。
        
        Exchange 2013 也支援就地 eDiscovery 搜尋的關鍵字查詢語言 (KQL) 語法。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>就地 eDiscovery 不支援規則運算式。</td>
        </tr>
        </tbody>
        </table>
        
        邏輯運算子必須使用大寫字母，例如 **AND** 和 **OR**，系統才會將它們視為運算子，而非關鍵字。建議您在任何混合邏輯運算子的查詢中明確使用括號，以避免錯誤或誤解。例如，如果要搜尋包含 WordA 或 WordB 以及 WordC 或 WordD 的訊息，您必須使用 **(WordA OR WordB) AND (WordC OR WordD)**。
    
      - **開始和結束日期：**依預設，就地 eDiscovery 並不限制依日期範圍進行搜尋。若要搜尋在指定日期範圍期間寄出的郵件，您可以指定開始與結束日期來縮小搜尋範圍。如果您未指定結束日期，則搜尋會傳回每次您重新開始搜尋時的最新結果。
    
      - **寄件者與收件者：**若要縮小搜尋範圍，您可以指定郵件的寄件者或收件者。您可以使用電子郵件地址、顯示名稱或網域名稱，搜尋寄給或寄自網域中所有人的郵件。例如，若要尋找來自或寄往 Contoso, Ltd 人員的電子郵件，請在 EAC 的 **\[寄件者\]** 或 **\[收件者/副本\]** 欄位中指定 **@contoso.com**。您也可以在命令介面的 *Senders* 或 *Recipients* 參數中指定 **@contoso.com**。
    
      - **訊息類型：**依預設會搜尋所有郵件類型。您可以藉由選擇特定郵件類型來限制搜尋，例如電子郵件、連絡人、文件、日誌、會議、記事、Lync 內容等。

下列螢幕擷取畫面顯示 EAC 中的搜尋查詢範例。

![設定 eDiscovery 搜尋查詢](images/Dd298021.a3626569-8700-421e-8b4e-7ec520b28272(EXCHG.150).png "設定 eDiscovery 搜尋查詢")

使用就地 eDiscovery 時，也考量以下事項：

  - **附件** 就地 eDiscovery 會搜尋由 Exchange 搜尋所支援的附件。如需詳細資訊，請參閱[依 Exchange 搜尋編製索引的檔案格式](file-formats-indexed-by-exchange-search-exchange-2013-help.md)。在內部部署中，您可在 Mailbox Server 上安裝檔案類型的搜尋篩選器 (也稱做 iFilter)，以新增對其他檔案類型的支援。

  - **無法搜尋的項目：**無法搜尋的項目是指 Exchange 搜尋無法建立索引的信箱項目。無法索引的原因包括缺少附件檔案的搜尋篩選器、篩選器發生錯誤，或是郵件已加密。若要成功進行 eDiscovery 搜尋，您的組織可能需要包含這些檢閱項目。將搜尋結果複製到探索信箱時，或是將搜尋結果匯出至 PST 檔案時，可以包含無法搜尋的項目。如需詳細資訊，請參閱[Exchange eDiscovery 中項目\] 無法搜尋](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md)。

  - **加密項目：**因為 Exchange 搜尋不會將使用 S/MIME 加密的郵件建立索引，所以就地 eDiscovery 不會搜尋這些郵件。如果您選取選項在搜尋結果中包含無法搜尋的項目，則會將這些 S/MIME 加密的郵件複製到探索信箱。

  - **受 IRM 保護的項目：**使用資訊版權管理 (IRM) 保護的郵件會由 Exchange 搜尋建立索引，因此如果符合查詢參數，便會將它們納入搜尋結果。必須使用與 Mailbox Server 位於相同 Active Directory 樹系中的 Active Directory Rights Management Services (AD RMS) 叢集來保護郵件。如需詳細資訊，請參閱 [資訊版權管理](information-rights-management-exchange-2013-help.md)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Exchange 搜尋無法將受 IRM 保護的郵件建立索引時，則會因為解密失敗，或因為 IRM 停用，而使受保護的郵件不會新增至失敗項目清單中。如果您選取選項在搜尋結果中包含無法搜尋的項目，則結果中可能不會包含無法解密的受 IRM 保護郵件。<br />
    若要在搜尋中包含受 IRM 保護的郵件，您可以建立另一個搜尋，以納入含 .rpmsg 附件的郵件。不論是否成功建立索引，您都可以使用查詢字串 <code>attachment:rpmsg</code> 來搜尋指定信箱中所有受 IRM 保護的郵件。在某個搜尋傳回符合搜尋條件的郵件時，包括已成功建立索引的受 IRM 保護郵件時，這可能會造成某些重複的搜尋結果。搜尋不會傳回無法建立索引的受 IRM 保護郵件。<br />
    為所有受 IRM 保護的郵件執行第二次搜尋時，也會包含已成功建立索引並於第一次搜尋傳回的受 IRM 保護郵件。此外，第二次搜尋傳回的受 IRM 保護郵件，可能不符合如第一次搜尋時所使用關鍵字等搜尋條件。</td>
    </tr>
    </tbody>
    </table>


  - **刪除重複項目** 複製搜尋結果至探索信箱時，您可以啟用探索搜尋結果的*刪除重複項目*功能僅將唯一郵件的一項執行個體複製到探索信箱。刪除重複項目功能具有下列好處：
    
      - 由於複製的訊息數目變少而能降低儲存需求並減少探索信箱大小。
    
      - 減少探索管理員、法律顧問或是其他需檢閱搜尋結果之人員的工作量。
    
      - 降低 eDiscovery 成本 (視排除於搜尋結果之外的重複項目數目而定)。

回到頁首

## 預估、預覽並複製搜尋結果

完成就地 eDiscovery 搜尋後，您便能在 EAC 中的 \[詳細資料\] 窗格中檢視搜尋結果預估。預估包括所傳回的項目數和那些項目的總大小。您也能檢視關鍵字統計資料，該資料傳回的詳細資料，是關於每個用於搜尋查詢的關鍵字所傳回的項目數。此資訊在確定查詢效率方面十分實用。如果查詢太廣，有可能會傳回較大的資料集，進行檢視時可能會需要更多資源並因此提高 eDiscovery 成本。如果查詢太狹隘，可能會大幅減少傳回的記錄數目，或完全未傳回記錄。您能使用預估和關鍵字統計資料來微調查詢，使其達到您的需求。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在 Exchange 2013 中，關鍵字統計資料也包括非關鍵字內容的統計資料，例如在搜尋查詢中所指定的日期、郵件類型和寄件者/收件者。</td>
</tr>
</tbody>
</table>


您也能預覽搜尋結果，以進一步確認傳回的郵件包含您所搜尋的內容，並視需求進一步微調查詢。eDiscovery 搜尋預覽功能會顯示從每個搜尋的信箱所傳回的郵件數，以及搜尋所傳回的郵件總數。很快就會產生預覽，不需要複製郵件至探索信箱。

當您滿意搜尋結果的數量與品質後，您便能將其複製到探索信箱中。複製郵件時，您具有下列選項：

  - **包含無法搜尋的項目** 如欲取得有關被視為無法搜尋之項目的類型之相關詳細資訊，請參閱上一節中的 eDiscovery 搜尋考量事項。

  - **啟用刪除重複項目** 如果在一個或多個搜尋過的信箱中找到多個執行個體的話，刪除重複項目功能便會透過僅納入唯一記錄的單一執行個體來減少資料集。

  - **啟用完整記錄：**依預設，複製項目時僅會啟用基本記錄功能。您可以選取完整記錄功能來納入所有經由搜尋所傳回記錄的相關資訊。

  - **當複製完成時傳送郵件給我：**就地 eDiscovery 搜尋可能會傳回大量記錄。複製傳回的郵件至探索信箱可能要花很長的時間。使用此選項即可在複製程序完成時取得電子郵件通知。為使透過 Outlook Web App 能更輕鬆地進行存取，此通知會包含已複製郵件所在的探索信箱之位置連結。

如需詳細資訊，請參閱 [將 eDiscovery 搜尋結果複製到探索信箱](copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md)。

回到頁首

## 將搜尋結果匯出至 PST 檔案

搜尋結果複製到探索信箱後，您可以將其匯出至 PST 檔案。

![將 eDiscovery 搜尋結果匯出至 PST 檔案](images/Dd298021.4ddca8af-1af5-4cb2-852c-e3a292099a58(EXCHG.150).gif "將 eDiscovery 搜尋結果匯出至 PST 檔案")

將搜尋結果匯出成 PST 檔案之後，您或其他使用者可以在 Outlook 中開啟這些結果，以檢閱或列印搜尋結果中傳回的訊息。如需詳細資訊，請參閱[將 eDiscovery 搜尋結果匯出至 PST 檔](export-ediscovery-search-results-to-a-pst-file-exchange-2013-help.md)。

## 不同的搜尋結果

因為就地 eDiscovery 會對即時資料執行搜尋，內容來源相同並使用相同搜尋查詢的兩個搜尋可能會傳回不同的結果。預估搜尋結果也可能與複製到探索信箱的實際搜尋結果不同。即使在短時間內重新執行相同搜尋也有可能會發生此情況。有幾個因素可能會影響搜尋結果的一致性：

  - 不斷建立內送電子郵件的索引，因為 Exchange 搜尋持續地建立組織信箱資料庫和傳輸管線的編目與索引。

  - 使用者或自動化程序將電子郵件刪除。

  - 大量匯入需要一些時間建立索引的大量電子郵件。

如果您遇到相同搜尋但有不同結果的情形，請考慮將信箱設定為保留以保存內容、在離峰時間執行搜尋，並讓系統在匯入大量電子郵件之後有時間建立索引。

## 記錄就地 eDiscovery 搜尋

就地 eDiscovery 搜尋具有兩種記錄類型：

  - **基本記錄** 所有的就地 eDiscovery 搜尋預設為啟用基本記錄功能。記錄中包含了搜尋和執行者的相關資訊。基本記錄所擷取的資訊會出現在電子郵件的內文中，此電子郵件會寄到儲存搜尋結果的信箱中。此郵件位於建立用於儲存搜尋結果的資料夾中。

  - **完整記錄** 完整記錄包含搜尋所傳回所有訊息的相關資訊。系統會在包含基本記錄資訊的電子郵件中附加一個以逗號分隔值 (.csv) 的檔案來提供此資訊，該 .csv 檔案的名稱則使用該搜尋的名稱。您可能需要此資訊以供遵循法規或保持記錄之用。若要啟用完整記錄功能，當在 EAC 中將搜尋結果複製到探索信箱時，請務必選取 **\[啟用完整記錄\]** 選項。如果您正在使用命令介面，請使用 *LogLevel* 參數來指定完整記錄選項。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用命令介面建立或修改就地 eDiscovery 搜尋時，您也可以停用記錄。</td>
</tr>
</tbody>
</table>


複製搜尋結果至探索信箱時，除了包含了搜尋記錄，Exchange 也記錄了由 EAC 或命令介面用於建立、修改或移除就地 eDiscovery 搜尋的指令程式。此資訊會記錄在管理稽核記錄項目中。如需詳細資訊，請參閱[系統管理員稽核記錄](administrator-audit-logging-exchange-2013-help.md)。

回到頁首

## 就地 eDiscovery 和就地保留

作為 eDiscovery 要求的一部分，您可能會被要求保留信箱內容，直到訴訟或調查已進行處分為止。信箱使用者所刪除或更改的郵件或任何程序也必須一併保留。在 Exchange 2013 中，透過使用就地保留完成這項動作。如需詳細資訊，請參閱[就地保留與訴訟暫止](in-place-hold-and-litigation-hold-exchange-2013-help.md)。

在 Exchange 2013 中，您可以使用新的 **\[就地 eDiscovery & 保留\]** 精靈來搜尋項目，並依 eDiscovery 要求或為符合其他業務需求而保留一段時間。當就地 eDiscovery 和就地保留使用相同的搜尋時，請注意下列事項：

  - 您無法使用此選項來搜尋所有信箱。您必須選取該信箱或通訊群組。

  - 如果就地 eDiscovery 搜尋也用於就地保留，則您無法移除就地 eDiscovery 搜尋。您必須先在搜尋中停用 \[就地保留\] 選項，然後移除該搜尋。

## 保留用於就地 eDiscovery 的信箱

當員工離開組織時，停用或移除其信箱是常見的做法。在您停用信箱之後，就會中斷與使用者帳戶的連線，但會保留在信箱裡一段時間，預設值為 30 天。受管理的資料夾助理員不會處理中斷連線的信箱，且在這段期間，均不會套用任何保留原則。您無法搜尋中斷連線的信箱之內容。一旦達到信箱資料庫已設定之刪除的信箱保留期限時，便會將該信箱從信箱資料庫中清除。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在 Exchange Online 中，就地 eDiscovery 可搜尋非作用中信箱中的內容。非使用中的信箱是指設為就地保留或訴訟資料暫留狀態然後移除的信箱。非作用中的信箱在暫停使用期間會一直保留。當非使用中的信箱從就地保留中移除或當訴訟資料暫留停用時，就會永久刪除信箱。如需詳細資訊，請參閱<a href="https://technet.microsoft.com/zh-tw/library/dn144876(v=exchg.150)">管理 Exchange Online 中的非使用中信箱</a>。</td>
</tr>
</tbody>
</table>


在內部部署中，如果您的組織要求在已不在組織裡的員工之郵件上套用保留設定，或是如果您可能必須保留前任員工的信箱，用於目前的或未來的 eDiscovery 搜尋之用途，請勿停用或移除該信箱。您可以採取下列步驟，以確保無法存取該信箱，且不會傳遞新的郵件到該信箱。

1.  使用 **\[Active Directory 使用者和電腦\]** 或其他的 Active Directory 或帳戶佈建工具或指令碼停用 Active Directory 使用者帳戶。這可防止使用關聯的使用者帳戶登入信箱。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>擁有完整存取信箱權限的使用者仍然能夠存取該信箱。若要避免他人存取，您必須從該信箱移除他們的完整存取權限。如需如何移除信箱的完整存取信箱權限的詳細資訊，請參閱<a href="manage-permissions-for-recipients-exchange-online-help.md">管理收件者的權限</a>。</td>
    </tr>
    </tbody>
    </table>


2.  將會由該信箱使用者寄送或接收的郵件之郵件大小限制設定在非常低的值，例如 1 KB。這能防止該信箱接收或傳送新郵件。如需詳細資訊，請參閱[設定信箱的郵件大小上限](configure-message-size-limits-for-a-mailbox-exchange-2013-help.md)。

3.  設定信箱的傳遞限制，如此無人能寄送郵件至該信箱。如需詳細資訊，請參閱[設定信箱的郵件傳遞限制](configure-message-delivery-restrictions-for-a-mailbox-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您必須採取以上步驟及任何其他由您組織所要求的帳戶管理程序，但卻不停用或移除信箱或移除關聯的使用者帳戶。</td>
</tr>
</tbody>
</table>


當您規劃為郵件保留管理 (MRM) 或就地 eDiscovery 而實施信箱保留時，您必須考慮員工的流動率。長期保留前任員工的信箱將必須在信箱伺服器上具備額外的儲存空間，而且也會導致 Active Directory 資料庫的增加，因為這必須在相同期間內保留關聯的使用者帳戶。此外，這可能也會要求變更您組織的帳戶佈建與管理程序。

回到頁首

## 就地 eDiscovery 限制和節流原則

在 Exchange 2013 和 Exchange Online 中，就地 eDiscovery 可耗用的資源是透過節流原則進行控制的。

預設的節流原則包含下列節流參數。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>參數</th>
<th>描述</th>
<th>預設值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DiscoveryMaxConcurrency</p></td>
<td><p>可以在組織中的同一時間執行的就地 eDiscovery 搜尋的數目上限。</p></td>
<td><p>2</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果啟動 eDiscovery 搜尋時仍執行兩個先前搜尋時，第三個搜尋不會排入佇列並將會改用失敗。您必須等到其中一個舊版搜尋完成時才能成功啟動新的搜尋。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p>DiscoveryMaxMailboxes</p></td>
<td><p>可在單一就地 eDiscovery 搜尋中搜尋到的信箱數量上限。</p></td>
<td><p>Exchange Online: 10,0001</p>
<p>Exchange 2013: 5,000</p></td>
</tr>
<tr class="odd">
<td><p>DiscoveryMaxStatsSearchMailboxes</p></td>
<td><p>可搜尋仍可讓您檢視關鍵字統計資料在單一就地 eDiscovery 搜尋中的信箱數目上限。</p></td>
<td><p>100</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>執行 eDiscovery 搜尋估計值之後，您可以檢視關鍵字統計資料。這些統計資料顯示詳細資料相關的每個關鍵字搜尋查詢中使用傳回的項目數。如果在搜尋中包含 100 個以上的來源信箱，如果您嘗試檢視關鍵字統計資料會傳回錯誤。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p>DiscoveryMaxKeywords</p></td>
<td><p>可在單一就地 eDiscovery 搜尋中指定的關鍵字數量上限。</p></td>
<td><p>500</p></td>
</tr>
<tr class="odd">
<td><p>DiscoveryMaxSearchResultsPageSize</p></td>
<td><p>預覽就地 eDiscovery 搜尋結果時，可在單一頁面上顯示的項目數量上限。</p></td>
<td><p>200</p></td>
</tr>
<tr class="even">
<td><p>DiscoverySearchTimeoutPeriod</p></td>
<td><p>就地 eDiscovery 搜尋在逾時之前會執行的分鐘數。</p></td>
<td><p>10 分鐘</p></td>
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
<td>1如果您起始的 eDiscovery 搜尋中SharePoint OnlineOffice 365組織中的 eDiscovery 中心從，您可以搜尋 1500 個信箱的最大值在單一搜尋。</td>
</tr>
</tbody>
</table>


在 Exchange Server 2013 中，您可以變更這些參數的預設值來配合您的需求，或建立其他節流原則，並將它們指派給具備委派探索管理權限的使用者。在 Exchange Online 中，您無法變更這些節流參數的預設值。

## 就地 eDiscovery 文件

下列表格包含可協助您了解並管理就地 eDiscovery 的主題連結。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>主題</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="assign-ediscovery-permissions-in-exchange-exchange-2013-help.md">Exchange 中指派 eDiscovery 權限</a></p></td>
<td><p>了解如何授權讓使用者在 EAC 中使用就地 eDiscovery 來搜尋 Exchange 信箱。若將使用者加入探索管理角色群組，則此人也可以使用 SharePoint 2013 和 SharePoint Online 的 eDiscovery 中心來搜尋 Exchange 信箱。</p></td>
</tr>
<tr class="even">
<td><p><a href="create-a-discovery-mailbox-exchange-2013-help.md">建立探索信箱</a></p></td>
<td><p>了解如何使用命令介面來建立探索信箱和指派存取權限。</p></td>
</tr>
<tr class="odd">
<td><p><a href="create-an-in-place-ediscovery-search-exchange-2013-help.md">建立就地 eDiscovery 搜尋</a></p></td>
<td><p>了解如何建立就地 eDiscovery 搜尋，以及如何估計和預覽 eDiscovery 搜尋結果。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=506799">編製郵件內容和搜尋運算子就地 ediscovery （英文）</a></p></td>
<td><p>了解可以使用「就地 eDiscovery」搜尋哪些電子郵件訊息內容。本主題提供每個內容的語法範例、<strong>AND</strong> 和 <strong>OR</strong> 之類搜尋運算子的相關資訊，以及其他搜尋查詢技巧 (例如使用雙引號 (&quot; &quot;) 和前置萬用字元) 的相關資訊。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/zh-tw/library/dn798915(v=exchg.150)">Exchange Online 中的就地 ediscovery 搜尋限制</a></p></td>
<td><p>了解就地 eDiscovery 限制在Exchange Online為協助維護的健康狀況和 Office 365 組織的 eDiscovery 服務的品質。</p></td>
</tr>
<tr class="even">
<td><p><a href="start-or-stop-an-in-place-ediscovery-search-exchange-2013-help.md">啟動或停止就地 eDiscovery 搜尋</a></p></td>
<td><p>了解如何開始、停止和重新開始 eDiscovery 搜尋。</p></td>
</tr>
<tr class="odd">
<td><p><a href="modify-an-in-place-ediscovery-search-exchange-2013-help.md">修改就地 eDiscovery 搜尋</a></p></td>
<td><p>了解如何修改現有的 eDiscovery 搜尋。</p></td>
</tr>
<tr class="even">
<td><p><a href="copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md">將 eDiscovery 搜尋結果複製到探索信箱</a></p></td>
<td><p>了解如何將 eDiscovery 搜尋結果複製到探索信箱。</p></td>
</tr>
<tr class="odd">
<td><p><a href="export-ediscovery-search-results-to-a-pst-file-exchange-2013-help.md">將 eDiscovery 搜尋結果匯出至 PST 檔</a></p></td>
<td><p>了解如何將 eDiscovery 搜尋結果匯出至 PST 檔案。</p></td>
</tr>
<tr class="even">
<td><p><a href="create-a-custom-management-scope-for-in-place-ediscovery-searches-exchange-2013-help.md">建立就地 eDiscovery 搜尋的自訂管理範圍</a></p></td>
<td><p>了解如何使用自訂的管理範圍來限制探索管理員可搜尋的信箱。</p></td>
</tr>
<tr class="odd">
<td><p><a href="remove-an-in-place-ediscovery-search-exchange-2013-help.md">移除就地 eDiscovery 搜尋</a></p></td>
<td><p>了解如何刪除 eDiscovery 搜尋。</p></td>
</tr>
<tr class="even">
<td><p><a href="search-for-and-delete-messages-admin-help-exchange-2013-help.md">搜尋並刪除郵件 - 管理中心說明</a></p></td>
<td><p>了解如何使用<strong>Search-Mailbox</strong>指令程式來搜尋並再刪除電子郵件訊息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="reduce-the-size-of-a-discovery-mailbox-in-exchange-exchange-2013-help.md">降低探索 Exchange 中信箱的大小</a></p></td>
<td><p>如果探索信箱大於 50 GB，使用此程序縮減它的大小。</p></td>
</tr>
<tr class="even">
<td><p><a href="delete-and-re-create-the-default-discovery-mailbox-in-exchange-exchange-2013-help.md">刪除並重新建立 Exchange 中預設的探索信箱</a></p></td>
<td><p>了解如何刪除預設的探索信箱、重新建立以及對其重新指派權限。如果信箱超過 50 GB 的限制，而且您並不需要這些搜尋結果，可以使用此程序。</p></td>
</tr>
<tr class="odd">
<td><p><a href="re-create-the-discovery-system-mailbox-exchange-2013-help.md">重新建立探索系統信箱</a></p></td>
<td><p>了解如何重新建立探索系統信箱。此工作僅用於 Exchange 2013 組織。</p></td>
</tr>
<tr class="even">
<td><p><a href="using-oauth-authentication-to-support-ediscovery-in-an-exchange-hybrid-deployment-exchange-2013-help.md">在 Exchange 混合式部署中使用 OAuth 驗證來支援 eDiscovery</a></p></td>
<td><p>了解 Exchange 混合部署中需要設定 OAuth 驗證的 eDiscovery 案例。</p></td>
</tr>
<tr class="odd">
<td><p><a href="configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md">設定 Exchange for SharePoint eDiscovery Center</a></p></td>
<td><p>了解如何設定 Exchange 2013，讓您能夠使用 SharePoint 2013 的 eDiscovery 中心來搜尋 Exchange 信箱。</p></td>
</tr>
<tr class="even">
<td><p><a href="unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md">Exchange eDiscovery 中項目] 無法搜尋</a></p></td>
<td><p>了解 Exchange 搜尋無法編製索引的信箱項目，而在 eDiscovery 搜尋結果中以無法搜尋的項目傳回。</p></td>
</tr>
</tbody>
</table>


如需在 Office 365、 Exchange 2013、 SharePoint 2013 和 Lync 2013 的 eDiscovery 的詳細資訊，請參閱 ＜ [eDiscovery 常見問題集](https://go.microsoft.com/fwlink/p/?linkid=386633)。

回到頁首

