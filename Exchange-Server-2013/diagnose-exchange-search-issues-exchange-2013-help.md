---
title: '診斷 Exchange 搜尋問題: Exchange 2013 Help'
TOCTitle: 診斷 Exchange 搜尋問題
ms:assetid: 8cfa26f4-ccf0-42dd-8570-67018188b4e8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb123701(v=EXCHG.150)
ms:contentKeyID: 52062571
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 診斷 Exchange 搜尋問題

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

Exchange搜尋索引的信箱與支援Exchange信箱中的附件。增加磁碟區的電子郵件、 信箱大小與儲存配額，佈建封存信箱的使用者，以及執行探索搜尋的就地 eDiscovery 增加Exchange搜尋是 Microsoft Exchange Server 2013組織中的信箱伺服器的重要元件。問題Exchange搜尋可以影響使用者產能及影響就地 eDiscovery 功能。

若要深入了解 Exchange 搜尋，請參閱[Exchange 搜尋](exchange-search-exchange-2013-help.md)。

要尋找有關管理 Exchange 搜尋的管理工作嗎？請參閱[Exchange 搜尋程序](exchange-search-procedures-exchange-2013-help.md)。

## 使用 Test-ExchangeSearch 指令程式

本主題程序的步驟 5 說明執行 **Test-ExchangeSearch** 指令程式來協助診斷 Exchange 搜尋問題。您可以使用 **Test-ExchangeSearch** 指令程式來測試信箱伺服器、信箱資料庫或特定信箱的 Exchange 搜尋功能。此指令程式會將測試郵件傳送至指定的信箱 (如果未指定信箱，則傳送至資料庫的系統信箱)，然後執行搜尋來決定是否編製郵件的索引，包括編製索引所需的時間。在正常情況下，Exchange 搜尋會在郵件建立或傳遞至信箱之後大約 10 秒內編製郵件的索引。測試後會自動刪除測試郵件。

如需詳細的語法及參數資訊，請參閱 [Test-ExchangeSearch](https://technet.microsoft.com/zh-tw/library/bb124733\(v=exchg.150\))。

## 擷取無法搜尋的項目

您可以使用[Get-FailedContentIndexDocuments](https://technet.microsoft.com/zh-tw/library/dd351154\(v=exchg.150\))指令程式來擷取無法成功索引Exchange搜尋無法搜尋之信箱項目清單。您可以針對信箱伺服器、 信箱資料庫或特定信箱執行此指令程式。此指令程式會傳回無法建立搜尋每個項目的詳細資訊。原因有幾個為何無法搜尋的信箱項目 ；例如，電子郵件訊息可能包含無法編製索引的搜尋的附件檔案類型或因為未安裝或已停用搜尋篩選。使用該檔案類型的搜尋篩選時，您可以Exchange伺服器上安裝它。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Microsoft 所提供的搜尋篩選器皆會進行測試，且受到 Microsoft 的支援。將任何協力廠商搜尋篩選器安裝到生產環境中的 Exchange 伺服器之前，建議先在測試環境中進行測試。</td>
</tr>
</tbody>
</table>


如需無法搜尋之項目的詳細資訊，請參閱：

  - [依 Exchange 搜尋編製索引的檔案格式](file-formats-indexed-by-exchange-search-exchange-2013-help.md)

  - [Exchange eDiscovery 中項目\] 無法搜尋](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md)

## 診斷 Exchange 搜尋問題

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「Exchange 搜尋」項目。

1.  **檢查服務狀態**   信箱伺服器上已啟動 Microsoft Exchange 搜尋 (MSExchangeFastSearch) 服務嗎？如果是，請移至步驟 2。如果不是，請使用 \[服務\] MMC 嵌入式管理單元來驗證 MSExchangeFastSearch 服務在執行中，如下所示：
    
    1.  按一下 \[開始\]、指向 \[系統管理工具\]，然後按一下 \[服務\]。
    
    2.  在 **\[服務\]** 中，確認 **Microsoft Exchange Search** 服務列出的 **\[狀態\]** 為 **\[已啟動\]**。

2.  **檢查信箱資料庫的組態**   是否已將使用者信箱資料庫的 *IndexEnabled* 參數設定為 True？如果是，請跳至步驟 3。否則，請在命令介面中執行下列命令來確認 *IndexEnabled* 旗標是否設為 True。
    
        Get-MailboxDatabase | Format-Table Name,IndexEnabled
    
    如需詳細語法及參數的資訊，請參閱 [Get-MailboxDatabase](https://technet.microsoft.com/zh-tw/library/bb124924\(v=exchg.150\))。

3.  **檢查信箱資料庫編目狀態**   Exchange 資料庫已編目嗎？如果是，請移至步驟 4。如果不是，請使用可靠性和效能監視器來檢查 **MSExchange Search Indexes** 效能物件的 **Crawler: Mailboxes Remaining** 計數器。執行下列步驟：
    
    1.  開啟 \[**效能監視器**(perfmon.exe)。
    
    2.  在主控台樹狀目錄中，按一下 \[監視工具\] 下的 \[效能監視器\]。
    
    3.  在 \[效能監視器\] 窗格中，按一下 \[新增\] (綠色加號)。
    
    4.  在 \[新增計數器\] 的 \[從電腦選取計數器\] 清單中，選取您要監視之信箱資料庫所在的伺服器。
    
    5.  在 **\[從下列電腦選取計數器\]** 清單下方無標籤的方塊中，選取 **\[MSExchange Search Indexes\]** 效能物件。
    
    6.  在 \[所選物件的執行個體\] 方塊中，選取使用者的信箱資料庫的執行個體。
    
    7.  按一下 \[新增\]，然後按一下 \[確定\]。
        
        在 \[效能監視器\] 窗格中，**MSExchange Search Indexes** 效能物件會列在 **\[物件\]** 欄中，而其各種計數器會列在 **\[計數器\]** 欄中。
    
    8.  檢視 **Crawler:Mailboxes Remaining** 計數器。1 或更高的任何值表示資料庫中的信箱仍在編目中。編目完成時，其值為 \[0\]。
    
    使用 \[效能監視器的相關資訊，請參閱[效能與可靠性監控快速入門指南 for Windows Server 2008](https://go.microsoft.com/fwlink/p/?linkid=178005)

4.  **檢查資料庫副本索引的健康狀況**   內容索引是否正常？使用 **Get-MailboxDatabaseCopyStatus** 指令程式來檢查資料庫副本的內容索引健康狀況。
    
        Get-MailboxDatabaseCopyStatus -Server $env:ComputerName | Format-Table Name,Status,ContentIndex* -Auto
    
    如需詳細的語法及參數資訊，請參閱 [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/zh-tw/library/dd298044\(v=exchg.150\))。

5.  **執行 Test-ExchangeSearch 指令程式**   如果已對信箱資料庫進行編目，則可以針對信箱資料庫或特定信箱執行 **Test-ExchangeSearch** 指令程式。
    
        Test-ExchangeSearch -Identity AlanBrewer@contoso.com
    
    如需詳細的語法及參數資訊，請參閱 [Test-ExchangeSearch](https://technet.microsoft.com/zh-tw/library/bb124733\(v=exchg.150\))。

6.  **檢查應用程式事件記錄檔**  使用事件檢視器或命令介面來檢查應用程式事件記錄檔中搜尋相關的錯誤訊息。檢查下列事件的來源。
    
      - **MSExchangeFastSearch**
    
      - **MSExchangeIS**
    
    如需詳細資訊，請依照下列事件日誌項目中的連結。

7.  **重新啟動 Microsoft Exchange 搜尋服務**   使用 \[服務\] MMC 嵌入式管理單元或命令介面來停止再重新啟動 MicrosoftExchange 搜尋 (MSExchangeFastSearch) 服務：
    
    1.  按一下 \[**開始**\]、指向 \[**系統管理工具**\]，然後按一下 \[**服務**\]。
    
    2.  在 **\[服務\]** 中，在 **\[Microsoft Exchange Search\]** 上按一下滑鼠右鍵，然後按一下 **\[停止\]**。在服務停止後，重新在該服務上按一下滑鼠右鍵，然後按一下 \[啟動\]。

8.  **重新植入搜尋類別目錄**   在某些情況下 (例如搜尋類別目錄損毀時)，可能需要重新植入類別目錄。需要重新植入搜尋類別目錄時，Exchange 搜尋會在應用程式事件記錄檔中記錄項目來通知您。如需重新植入搜尋類別目錄的詳細資訊，請參閱[重新植入搜尋類別目錄](reseed-the-search-catalog-exchange-2013-help.md)。

