---
title: '公用資料夾: Exchange 2013 Help'
TOCTitle: 公用資料夾
ms:assetid: 94c4fb69-9234-4b34-8c1c-da2a0a11da65
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ150538(v=EXCHG.150)
ms:contentKeyID: 50473766
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 公用資料夾

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2017-03-27_

公用資料夾的設計目的在於共用存取，並提供簡易有效率的方式來收集及組織資訊，以及與工作群組或組織中的其他人員共用資訊。公用資料夾有助於以易於瀏覽的深層階層來組織內容。使用者可在 Outlook 中看到完整階層，讓他們更容易瀏覽想找的內容。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>下列 Outlook 用戶端提供公用資料夾：Outlook Web App for Exchange 2013、Outlook 2007、Outlook 2010、Outlook 2013 和 Outlook for Mac。</td>
</tr>
</tbody>
</table>


公用資料夾也可作為通訊群組的封存方法。當您對公用資料夾啟用郵件功能並將其新增為通訊群組的成員，傳送給該群組的電子郵件都會自動加入公用資料夾，供日後參考。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您必須使用 Outlook 2007 或更新版本才能存取 Exchange 2013 伺服器上的公用資料夾。</td>
</tr>
</tbody>
</table>


公用資料夾不被設計來執行下列動作：

  - **資料封存**有時具有信箱限制使用者使用封存資料，而不是信箱的公用資料夾。此作法是不建議使用，因為它會影響公用資料夾中的儲存空間和思考的目標信箱限制。而是建議您使用[就地封存 in Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md)做為封存解決方案。

  - **文件共用和協同合作**公用資料夾不提供版本或其他文件管理功能，例如控制的存回及取出功能及自動通知內容變更。而是建議[SharePoint](https://go.microsoft.com/fwlink/?linkid=282474)作為您的文件共用解決方案。

若要深入了解 Exchange 2013 的公用資料夾和其他協同作業方法，請參閱[共同作業](collaboration-exchange-2013-help.md)。

若要瀏覽 Exchange 2013 公用資料夾的常見問題，請參閱[常見問題集：公用資料夾](faq-public-folders-exchange-2013-help.md)。

如需限制和公用資料夾配額的詳細資訊，請參閱[公用資料夾的限制](limits-for-public-folders-exchange-2013-help.md)。

如需公用資料夾管理工作的清單，請參閱[公用資料夾程序](public-folder-procedures-exchange-2013-help.md)。

尋找本主題的 Exchange Online 版本吗？請參閱[Office 365 與 Exchange Online 的公用資料夾](https://technet.microsoft.com/zh-tw/library/jj200758\(v=exchg.150\))。

**目錄**

Public folder architecture

將公用資料夾移轉

Public folder moves

Public folder quotas

Disaster recovery

## 公用資料夾架構

Exchange 2013 中的公用資料夾已使用信箱基礎結構重新設計，可善用信箱資料庫現有的高可用性和儲存技術。公用資料夾架構使用特殊設計的信箱，來儲存公用資料夾階層與內容。這也意味著再也沒有公用資料夾資料庫。公用資料夾信箱的高可用性是由資料庫可用性群組 (DAG) 提供。若要深入了解 DAG，請參閱[資料庫可用性群組 (DAGs)](database-availability-groups-dags-exchange-2013-help.md)。

公用資料夾的主要架構元件是公用資料夾信箱，這些信箱可以位在一或多個信箱資料庫中。

## 公用資料夾信箱

公用資料夾信箱有兩種類型：*主要階層信箱*和*次要階層信箱*。這兩種信箱類型都能包含內容：

  - **主要階層信箱**  主要階層信箱是公用資料夾階層的一個可寫入複本。公用資料夾階層複製到其他公用資料夾信箱，但是這些會是唯讀的複本。

  - **次要階層信箱**  次要階層信箱包含公用資料夾內容以及公用資料夾階層的唯讀複本。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>公用資料夾信箱不支援保留原則。</td>
</tr>
</tbody>
</table>


公用資料夾信箱有兩種管理方法：

  - 在 Exchange 系統管理中心 (EAC) 內，瀏覽至 **\[公用資料夾\]** \> **\[公用資料夾信箱\]**。

  - 在 Exchange 管理命令介面中，使用 **\*-Mailbox** 這組指令程式。已新增下列參數至 [New-Mailbox](https://technet.microsoft.com/zh-tw/library/aa997663\(v=exchg.150\)) 指令程式以支援公用資料夾信箱：
    
      - *PublicFolder*   此參數與 **New-Mailbox** 指令程式搭配使用可建立公用資料夾信箱。建立公用資料夾信箱時，會以 `PublicFolder` 信箱類型建立新信箱。如需詳細資訊，請參閱[建立公用資料夾信箱](create-a-public-folder-mailbox-exchange-2013-help.md)。
    
      - *HoldForMigration*   此參數僅適用於將公用資料夾從舊版遷移至 Exchange 2013。如需詳細資訊，請參閱本主題稍後的Migrate Public folders from previous versions。
    
      - *IsHierarchyReady*  此參數會指出是否已準備好要提供給使用者的公用資料夾階層公用資料夾信箱。它設為`$True`後已同步處理整個階層公用資料夾信箱。如果此參數設為 $False，使用者將不會使用它來存取階層。不過，如果您在特定的公用資料夾信箱使用者信箱上設定*DefaultPublicFolderMailbox*屬性、，使用者仍即使*IsHierarchyReady*參數設為`$False`存取指定的公用資料夾信箱。
    
      - *IsExcludedFromServingHierarchy*   此參數可避免使用者在指定的公用資料夾信箱上存取公用資料夾階層。針對負載平衡用途，根據設定使用者將平均分配於公用資料夾信箱中。當此參數設定於公用資料夾信箱上時，信箱未包含於此自動負載平衡中，且無法供使用者存取以擷取公用資料夾階層。但是，如果您將使用者信箱上的 *DefaultPublicFolderMailbox* 內容設定為特定的公用資料夾信箱，使用者將仍可存取指定的公用資料夾信箱，即便 *IsExcludedFromServingHierarchy* 參數已為該公用資料夾信箱設定。

如果明確指定在使用者的信箱使用*DefaultPublicFolderMailbox*屬性，或者符合下列條件的次要階層信箱會對使用者做僅公用資料夾階層資訊：

  - 公用資料夾信箱上的 \[ *IsHierarchyReady* \] 屬性設為`$True`。

  - 公用資料夾信箱的*IsExcludedFromServingHierarchy*屬性設為`$False`。

## 公用資料夾階層

公用資料夾階層包含了該資料夾的內容和組織資訊，包括樹狀結構。每個公用資料夾信箱都包含公用資料夾階層的副本。但只有一個可寫入的階層副本，其位置在主要公用資料夾信箱中。對於特定資料夾而言，階層資訊可用來識別下列事項：

  - 資料夾的權限

  - 公用資料夾樹狀目錄內資料夾的位置，包含其父項及子項資料夾

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>階層不會儲存已啟用郵件功能之公用資料夾的電子郵件地址相關資訊。電子郵件地址是儲存在 Active Directory 的目錄物件上。</td>
</tr>
</tbody>
</table>


## 階層同步

公用資料夾階層同步程序使用遞增值同步處理 (ICS)，此方法可提供監控和同步 Exchange 儲存區階層或內容之變更的機制。變更包括建立、修改和刪除資料夾及郵件。當使用者連線到內容信箱及使用內容信箱時，每 15 分鐘就會進行一次同步。如果沒有使用者連線到內容信箱，則觸發同步的頻率較低 (每 24 小時)。如果在主要階層執行寫入作業 (如建立資料夾)，則會立即 (同時) 觸發內容信箱的同步。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>因為只有一個可寫入的階層副本，資料夾建立程序會由使用者連線到的內容信箱透過 Proxy 傳送到階層信箱。</td>
</tr>
</tbody>
</table>


在大型組織中，當您建立新的公用資料夾信箱時，階層必須先同步至該公用資料夾，之後使用者才能與其連線。否則，使用者在連線到 Outlook 時可能會看到不完整的公用資料夾結構。若要在同步進行期間不讓使用者嘗試連線到新的公用資料夾信箱，在建立公用資料夾信箱時請對 **New-Mailbox** 指令程式設定 *IsExcludedFromServingHierarchy* 參數。此參數可防止使用者連線到新建立的公用資料夾信箱。同步完成後，執行 [Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\)) 指令程式並將 *IsExcludedFromServingHierarchy* 參數設為 `false`，表示該公用資料夾信箱已準備好可供連線。您也可以使用 [Get-PublicFolderMailboxDiagnostics](https://technet.microsoft.com/zh-tw/library/jj218720\(v=exchg.150\)) 指令程式，根據 *SyncInfo* 和 *AssistantInfo* 內容來檢視同步狀態。

如需詳細資訊，請參閱[建立公用資料夾](create-a-public-folder-exchange-2013-help.md)。

## 公用資料夾內容

公用資料夾內容可包含電子郵件、文章、文件和 eForms。這些內容儲存在公用資料夾信箱中，但不會複寫到多個公用資料夾信箱。所有使用者都是存取同一個公用資料夾信箱中的同一個內容集。您可以對公用資料夾內容執行全文搜尋，但無法在多個公用資料夾之間搜尋公用資料夾內容，Exchange 搜尋也未對內容編制索引。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Outlook Web App 支援，但有限制。您可以新增和移除我的最愛公用資料夾並執行項目層級作業，例如建立、 編輯、 刪除文章及回覆的文章。不過，您無法建立或刪除公用資料夾從 Outlook Web App。此外，唯一的電子郵件、 文章、 行事曆及連絡人公用資料夾可新增至 Outlook Web App 中的 [我的最愛] 清單。</td>
</tr>
</tbody>
</table>


## 移轉公用資料夾

您可以將公用資料夾移轉從放至 Exchange 2013 的 Exchange Server 版本或先前版本的 Exchange Server 至 Exchange Online。您也可以將 Exchange 2013 公用資料夾移轉至 Exchange Online。

如果您已安裝 Exchange 2013 之前在組織中 Exchange 2010 SP3 或 Exchange 2007 SP3 RU10 公用資料夾，您必須將這些公用資料夾移轉至 Exchange 2013。為達成此目的，使用**PublicFolderMigrationRequst**指令程式。如需詳細資訊，請參閱[使用批次移轉公用資料夾從舊版移轉至 Exchange 2013](use-batch-migration-to-migrate-public-folders-to-exchange-2013-from-previous-versions-exchange-2013-help.md)。如果您的組織移至 Exchange Online 時，您可以將公用資料夾移轉至雲端並加以升級，同時。如需詳細資訊，請參閱[使用批次移轉至 Office 365 和 Exchange Online 移轉舊版公用資料夾](use-batch-migration-to-migrate-legacy-public-folders-to-office-365-and-exchange-online-exchange-online-help.md)和[使用批次移轉至 Exchange 2013 公用資料夾移轉至 Exchange Online](use-batch-migration-to-migrate-exchange-2013-public-folders-to-exchange-online-exchange-online-help.md)。

由於公用資料夾的儲存方式產生變更，舊版 Exchange 信箱無法存取 Exchange 2013 伺服器或 Exchange Online 上的公用資料夾階層。不過，Exchange 2013 伺服器或 Exchange Online 上的使用者信箱可以連接至舊版公用資料夾。Exchange 2013 公用資料夾和舊版公用資料夾無法同時存在於您的 Exchange 組織中。這實際上表示不同版本無法共存。將公用資料夾遷移至 Exchange Server 2013 或 Exchange Online 目前是一次性轉換過程。

此原因，建議再移轉您的公用資料夾，您應該先在舊版將信箱遷移至 Exchange 2013 或 Exchange Online。如需移轉的詳細資訊的信箱，請參閱[在 Exchange 2013 移動信箱](mailbox-moves-in-exchange-2013-exchange-2013-help.md)、[執行轉換遷移至 Office 365 的電子郵件的](https://go.microsoft.com/fwlink/p/?linkid=536689)，以及[執行分段遷移至 Office 365 的電子郵件的](https://go.microsoft.com/fwlink/p/?linkid=536687)。

## 公用資料夾移動

您可將公用資料夾移動至其他公用資料夾信箱，也可以將公用資料夾信箱移動至其他信箱資料庫。若要將公用資料夾移動至其他公用資料夾信箱，請使用 **PublicFolderMoveRequest** 這組指令程式。依預設，要移動之公用資料夾下的子資料夾不會移動。如果您要移動公用資料夾分支，可以使用隨 Exchange 2013 預設安裝的 `Move-PublicFolderBranch.ps1` 指令碼。如需詳細資訊，請參閱[將公用資料夾移至不同的公用資料夾信箱](move-a-public-folder-to-a-different-public-folder-mailbox-exchange-2013-help.md)。

除了移動公用資料夾，您也可以使用 **MoveRequest** 這組指令程式將公用資料夾信箱移至其他信箱資料庫。這與用來移動一般信箱的指令程式是同一組指令程式。如需詳細資訊，請參閱[公用資料夾信箱移至不同信箱資料庫](move-a-public-folder-mailbox-to-a-different-mailbox-database-exchange-2013-help.md)。

**PublicFolderMoveRequest** 指令程式和 **MoveRequest** 指令程式使用信箱複寫服務，以非同步方式移動公用資料夾。這表示實際操作不是由指令程式執行的，而且在大部分移動過程中，使用者仍可使用公用資料夾和公用資料夾信箱。因為是由信箱複寫服務執行信箱移動、匯入和匯出要求以及公用資料夾移動要求，所以請務必考慮節流和工作負載管理。

## 公用資料夾配額

公用資料夾信箱在建立時，會自動繼承信箱資料庫大小限制預設值。因此，使用 [Get-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123685\(v=exchg.150\)) 指令程式時若想正確評估目前的儲存配額狀態，除了 *ProhibitSendQuota*、*ProhibitSendReceiveQuota* 和 *IssueWarningQuota* 內容之外，也必須查看 *UseDatabaseQuotaDefaults* 內容。如果 *UseDatabaseQuotaDefaults* 內容設為 `true`，表示會忽略每個信箱設定，並使用信箱資料庫限制。如果此內容設為 `true`，而 *ProhibitSendQuota*、*ProhibitSendReceiveQuota* 及 *IssueWarningQuota* 內容設為 `unlimited`，則信箱大小並非真的無限。您必須改用 **Get-MailboxDatabase** 指令程式並檢閱信箱資料庫儲存限制，以找出信箱的限制。如果 *UseDatabaseQuotaDefaults* 內容設為 `false`，則會使用每個信箱設定。Exchange 2013 的預設信箱資料庫配額限制如下：

  - *發出警告配額*：1.9 GB

  - *禁止傳送配額*：2 GB

  - *禁止接收配額*：2.3 GB

若想找出信箱資料庫配額，請執行 [Get-MailboxDatabase](https://technet.microsoft.com/zh-tw/library/bb124924\(v=exchg.150\)) 指令程式。

若要在公用資料夾信箱上設定配額，請使用 [Set-OrganizationConfig](https://technet.microsoft.com/zh-tw/library/aa997443\(v=exchg.150\)) 指令程式。

## 嚴重損壞修復

Exchange 2013 公用資料夾是建立在信箱基礎結構上，並使用相同的可用性和備援機制。每個公用資料夾信箱都能有多個複製檔以及自動容錯移轉功能，與一般信箱相同。若要深入了解，請參閱[高可用性和站台恢復](high-availability-and-site-resilience-exchange-2013-help.md)。

除了整體嚴重損壞修復案例，您也可以還原下列狀況中的公用資料夾：

  - **虛刪除公用資料夾還原**   公用資料夾已遭刪除，但仍在保留期間內。

  - **虛刪除公用資料夾信箱還原**   公用資料夾信箱已遭刪除，但仍在信箱保留期間內。

  - **從復原資料庫還原公用資料夾信箱**   已刪除的信箱超過保留期間時，您可以從備份復原個別的公用資料夾信箱。然後您可以從已還原信箱中擷取資料，並將資料複製到目標資料夾或合併至另一個信箱。

在上述所有情況中，公用資料夾和公用資料夾信箱都能使用 **MailboxRestoreRequest** 指令程式加以復原。

如需詳細資訊，請參閱[從失敗的移動還原公用資料夾和公用資料夾信箱](restore-public-folders-and-public-folder-mailboxes-from-failed-moves-exchange-2013-help.md)。

