---
title: '管理信箱資料庫副本: Exchange 2013 Help'
TOCTitle: 管理信箱資料庫副本
ms:assetid: 28cedf1d-365a-4e36-b2ba-6bf81af8684f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd335158(v=EXCHG.150)
ms:contentKeyID: 50472872
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理信箱資料庫副本

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-08-26_

在資料庫可用性群組 (DAG) 已建立、設定並填入信箱伺服器成員後，您可以使用 Exchange 系統管理中心 (EAC) 或 Exchange 管理命令介面，透過彈性且精細的方式新增信箱資料庫副本。

## 管理資料庫副本

建立資料庫的多個副本之後，您可以使用 EAC 或命令介面，監視每個副本的健康狀況和狀態，並執行與資料庫副本關聯的其他管理工作。可能需要執行的一些管理工作包含暫停或繼續資料庫副本、植入資料庫副本、監視資料庫副本、設定資料庫副本設定和移除資料庫副本。

## 暫停及繼續資料庫副本

基於各種原因 (例如執行已規劃的維護)，您可能需要暫停及繼續資料庫副本的連續複寫活動。此外，某些系統管理工作 (例如植入) 需要先暫停資料庫副本。我們建議您在變更資料庫或其記錄檔的路徑時，先暫停所有複寫活動。您可以使用 EMC 或在命令介面中執行 **Suspend-MailboxDatabaseCopy** 與 **Resume-MailboxDatabaseCopy** Cmdlet 來暫停與繼續資料庫副本活動。如需如何暫停或繼續資料庫副本之連續複寫活動的詳細步驟，請參閱[擱置或恢復信箱資料庫副本](suspend-or-resume-a-mailbox-database-copy-exchange-2013-help.md)。

## 植入資料庫副本

「植入」 (也稱為「更新」) 是將空白資料庫或實際執行資料庫的副本新增至相同 DAG 中另一個信箱伺服器上的目標副本位置，作為作用中的資料庫。這會成為由該伺服器維護之副本的基準線資料庫。

根據不同的情況而定，植入可以是自動的處理程序，也可以是您所初始的手動處理程序。假設目標伺服器及其儲存設定正確，新增資料庫副本時，將自動植入副本。如果您要手動植入資料庫副本，而且不希望在建立副本時發生自動植入，則可以在執行 [Add-MailboxDatabaseCopy](https://technet.microsoft.com/zh-tw/library/dd298105\(v=exchg.150\)) 指令程式時使用 *SeedingPostponed* 參數。

初始植入進行之後，很少需要重新植入資料庫副本。但如果必須重新植入，或您想要手動植入資料庫副本而非讓系統自動植入副本，您可以使用 EAC 中的「更新信箱資料庫副本」精靈或命令介面中的 [Update-MailboxDatabaseCopy](https://technet.microsoft.com/zh-tw/library/dd335201\(v=exchg.150\)) Cmdlet 來執行這些工作。植入資料庫副本之前，您必須先暫停信箱資料庫副本。如需如何植入資料庫副本的詳細步驟，請參閱[更新信箱資料庫副本](update-a-mailbox-database-copy-exchange-2013-help.md)。

手動植入作業完成之後，會自動繼續已植入之信箱資料庫副本的複寫。如果您不想讓複寫自動繼續，您可以在執行 [Update-MailboxDatabaseCopy](https://technet.microsoft.com/zh-tw/library/dd335201\(v=exchg.150\)) 指令程式時使用 *ManualResume* 參數。

## 選擇要植入的項目

當執行植入作業時，您可以選擇植入信箱資料庫副本的信箱資料庫副本，或同時資料庫副本和內容索引類別目錄複製的內容索引類別目錄。

更新信箱資料庫副本精靈和[Update-MailboxDatabaseCopy](https://technet.microsoft.com/zh-tw/library/dd335201\(v=exchg.150\))指令程式的預設行為是植入信箱資料庫副本和內容索引類別目錄複製。若要只植入信箱資料庫副本沒有植入內容索引類別目錄*DatabaseOnly*參數使用時執行[Update-MailboxDatabaseCopy](https://technet.microsoft.com/zh-tw/library/dd335201\(v=exchg.150\))指令程式。若要植入剛才的內容索引類別目錄複本，請執行[Update-MailboxDatabaseCopy](https://technet.microsoft.com/zh-tw/library/dd335201\(v=exchg.150\))指令程式時使用*CatalogOnly*參數。

## 選取植入來源

任何健全狀況良好的資料庫副本都可以作為該資料庫之其他副本的植入來源使用。當您的 DAG 遍佈多個實體位置時，此功能特別有用。例如，假設有一個四個成員的 DAG 部署，其中兩個成員 (MBX1 和 MBX2) 位於奧勒崗州的波特蘭，而另兩個成員 (MBX3 和 MBX4) 位於紐約州的紐約市。名爲 DB1 的信箱資料庫在 MBX1 上使用中，而在 MBX2 和 MBX3 上有 DB1 的被動副本。將 DB1 的副本新增至 MBX4 時，您可以選擇使用 MBX3 上的副本作為植入來源。這麼做，您可以避免植入超出 Portland 和 New York 之間的廣域網路 (WAN) 連結。

若要在新增資料庫副本時使用特定副本作為植入來源，您應該執行下列動作：

  - 執行 [Add-MailboxDatabaseCopy](https://technet.microsoft.com/zh-tw/library/dd298105\(v=exchg.150\)) 指令程式以新增資料庫副本時，請使用 *SeedingPostponed* 參數。如果不使用 *SeedingPostponed* 參數，則會使用資料庫的使用中副本作爲來源，明確地植入資料庫副本。

  - 您可以指定想要作為 EAC 中更新信箱資料庫副本精靈一部分的來源伺服器，或可以在執行 [Update-MailboxDatabaseCopy](https://technet.microsoft.com/zh-tw/library/dd335201\(v=exchg.150\)) Cmdlet 時，使用 *SourceServer* 參數以指定想要用於植入的來源伺服器。在先前的範例中，您應該將 MBX3 指定為來源伺服器。如果不使用 *SourceServer* 參數，則會從資料庫的使用中副本明確地植入資料庫副本。

## 植入和網路

除了選取植入信箱資料庫副本的特定來源伺服器之外，您也可以使用命令介面指定要使用的 DAG 網路，並在植入作業期間選擇性地覆寫 DAG 網路的壓縮和加密設定。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>植入內容索引類別目錄才有可能透過 MAPI 網路。即使您可以將 Update-mailboxdatabasecopy 指令程式<code>-Network</code>參數也是如此。</td>
</tr>
</tbody>
</table>


若要指定要用於植入的網路，請在執行 [Update-MailboxDatabaseCopy](https://technet.microsoft.com/zh-tw/library/dd335201\(v=exchg.150\)) 指令程式時使用 *Network* 參數，並指定要使用的 DAG 網路。如果您不使用 *Network* 參數，系統會使用下列在植入作業時用於選取要使用之網路的預設行為：

  - 如果來源伺服器和目標伺服器位於相同的子網路上，已設定包含該子網路的複寫網路，則會使用該複寫網路。

  - 如果來源伺服器和目標伺服器位於不同的子網路上，即使已設定包含這些子網路的複寫網路，仍將使用用戶端 (MAPI) 網路進行植入。

  - 如果來源伺服器和目標伺服器位於不同的資料中心，則會使用用戶端 (MAPI) 網路進行植入。

DAG 網路的加密和壓縮是在 DAG 層級中設定。預設設定為僅針對不同子網路的通訊使用加密和壓縮。如果來源和目標位於不同的子網路上，而 DAG 是使用 *NetworkCompression* 和 *NetworkEncryption* 的預設值進行設定，您可以在執行 [Update-MailboxDatabaseCopy](https://technet.microsoft.com/zh-tw/library/dd335201\(v=exchg.150\)) 指令程式時，分別使用 *NetworkCompressionOverride* 和 *NetworkEncryptionOverride* 參數來覆寫這些值。

## 植入程序

當您使用 [Add-MailboxDatabaseCopy](https://technet.microsoft.com/zh-tw/library/dd298105\(v=exchg.150\)) 或 [Update-MailboxDatabaseCopy](https://technet.microsoft.com/zh-tw/library/dd335201\(v=exchg.150\)) 指令程式起始植入程序時，會執行以下工作：

1.  讀取來自 Active Directory 的資料庫內容以驗證指定的資料庫和伺服器，並驗證來源和目標伺服器執行的是 Exchange 2013、它們是相同 DAG 的成員，以及指定的資料庫不是復原資料庫。也會讀取資料庫檔案路徑。

2.  準備從目標伺服器上的 Microsoft Exchange 複寫服務重新植入檢查。

3.  目標伺服器上的 Microsoft Exchange 複寫服務會檢查步驟 1 中 Active Directory 檢查所讀取的檔案目錄中是否有資料庫和交易記錄檔。

4.  Microsoft Exchange 複寫服務會將狀態資訊從目標伺服器傳回到從其執行指令程式的系統管理介面。

5.  如果所有初步檢查都已通過，則會在繼續之前提示您確認作業。如果您確認該作業，程序就會繼續進行。如果在初步檢查期間發生錯誤，則會回報錯誤，而作業也會失敗。

6.  植入作業是從目標伺服器上的 Microsoft Exchange 複寫服務啟動。

7.  Microsoft Exchange 複寫服務會暫停使用中資料庫副本的資料庫複寫。

8.  Microsoft Exchange 複寫服務會更新資料庫的狀態資訊，以反映植入的狀態。

9.  如果目標伺服器上還沒有用於目標資料庫和記錄檔的目錄，則會建立這些目錄。

10. 植入資料庫的要求是使用 TCP 從目標伺服器上的 Microsoft Exchange 複寫服務傳遞至來源伺服器上的 Microsoft Exchange 複寫服務。植入資料庫的這個要求和後續的通訊會在設定為複寫網路的 DAG 網路上進行。

11. 來源伺服器上的 Microsoft Exchange 複寫服務會透過 Microsoft Exchange 資訊儲存庫服務介面起始可延伸儲存引擎 (ESE) 資料流備份。

12. Microsoft Exchange 資訊儲存庫服務會將資料庫資料串流傳送至 Microsoft Exchange 複寫服務。

13. 資料庫資料會從來源伺服器的 Microsoft Exchange 複寫服務移至目標伺服器的 Microsoft Exchange 複寫服務。

14. 目標伺服器上的 Microsoft Exchange 複寫服務會將資料庫副本寫入位於名爲 *\[temp-seeding\]* 的主要資料庫目錄中的暫存目錄。

15. 當達到資料庫的結尾時，來源伺服器上的資料流備份作業便會結束。

16. 目標伺服器上的寫入作業完成後，資料庫會從 temp-seeding 目錄移至最終位置。該 temp-seeding 目錄隨即遭到刪除。

17. 在目標伺服器上，Microsoft Exchange 複寫服務會代理 Microsoft Exchange 搜尋服務的要求，以裝載資料庫副本的內容索引類別目錄 (如果存在)。如果在資料庫副本的先前執行個體中，有現有的過期類別目錄檔案，裝載作業便會失敗，這會觸發從來源伺服器複寫的需求。同樣地，如果類別目錄不存在於目標伺服器上資料庫副本的新執行個體上，則需要類別目錄的副本。在從來源複製新類別目錄時，Microsoft Exchange 複寫服務會引導 Microsoft Exchange 搜尋服務暫停資料庫副本的索引。

18. 目標伺服器上的 Microsoft Exchange 複寫服務會將植入類別目錄要求傳送至來源伺服器上的 Microsoft Exchange 複寫服務。

19. 在來源伺服器上，Microsoft Exchange 複寫服務會從 Microsoft Exchange 搜尋服務要求目錄資訊，並要求暫停索引。

20. 來源伺服器上的 Microsoft Exchange 搜尋服務會將搜尋類別目錄目錄資訊傳回到 Microsoft Exchange 複寫服務。

21. 來源伺服器上的 Microsoft Exchange 複寫服務會從目錄讀取類別目錄檔案。

22. 來源伺服器上的 Microsoft Exchange 複寫服務會使用跨複寫網路的連線，將類別目錄資料移至目標伺服器上的 Microsoft Exchange 複寫服務。讀取完成之後，Microsoft Exchange 複寫服務會傳送一個要求到 Microsoft Exchange 搜尋服務以繼續來源資料庫的索引。

23. 如果目標伺服器的目錄中有任何現有的類別目錄檔案，目標伺服器上的 Microsoft Exchange 複寫服務會將其刪除。

24. 目標伺服器上的 Microsoft Exchange 複寫服務會將類別目錄資料寫入名爲 *\[CiSeed.Temp\]* 的暫存目錄，直到資料已完整傳輸為止。

25. Microsoft Exchange 複寫服務會將完整的類別目錄資料移至最終位置。

26. 目標伺服器上的 Microsoft Exchange 複寫服務會繼續搜尋目標資料庫的索引。

27. 目標伺服器上的 Microsoft Exchange 複寫服務會傳回完成狀態。

28. 作業的最終結果會傳遞到從其呼叫指令程式的系統管理介面。

## 設定資料庫副本

建立資料庫副本之後，您可以在需要時檢視和修改其組態。您可以針對 EAC 中的資料庫副本檢查 \[屬性\] 頁面，以檢視部分組態資訊。您也可以在命令介面中使用 [Get-MailboxDatabase](https://technet.microsoft.com/zh-tw/library/bb124924\(v=exchg.150\)) 和 [Set-MailboxDatabaseCopy](https://technet.microsoft.com/zh-tw/library/dd298104\(v=exchg.150\)) 指令程式以檢視和設定資料庫副本設定，例如重新顯示延遲時間、截斷延遲時間和啟動喜好設定順序。如需如何檢視和設定資料庫副本設定的詳細步驟，請參閱[設定信箱資料庫副本屬性](configure-mailbox-database-copy-properties-exchange-2013-help.md)。

## 使用重新顯示延遲和截斷延遲選項

信箱資料庫副本支援使用*重新顯示延遲時間*和*截斷延遲時間*，兩者的設定都以分鐘為單位。設定重新顯示延遲時間可讓您將資料庫副本還原至特定的時間點。設定截斷延遲時間可讓您使用被動資料庫副本上的記錄檔，從使用中資料庫副本上的記錄檔遺失進行復原。由於這兩個功能會導致暫時的記錄檔增多，因此使用任一功能都會影響您的儲存設計。

## 重新顯示延遲時間

重新顯示延遲時間是信箱資料庫副本的內容，其中指定所需的時間 (以分鐘為單位)，以延遲資料庫副本的記錄重新顯示。當記錄檔已複寫到被動副本並已順利通過檢查後，重新顯示延遲計時器便會啟動。透過延遲資料庫副本記錄檔的重新顯示，您就可以將資料庫復原至過去的特定時間點。重新執行延隔時間設定成大於 0 的信箱資料庫副本稱為*延遲的信箱資料庫副本*，或簡稱為*延遲副本*。

在 Exchange 2013 中使用資料庫副本和訴訟保留功能的策略，可對通常會造成資料遺失的失敗範圍提供保護。不過，這些功能無法在發生邏輯損毀時針對資料遺失提供保護，雖然這種情況很罕見，但會導致資料遺失。延遲副本的設計是用於發生邏輯損毀時，避免資料遺失。通常有兩種類型的邏輯損毀：

  - **資料庫邏輯損毀**  資料庫頁面總和檢查碼相符，但頁面上的資料邏輯錯誤。這可能會在 ESE 嘗試寫入資料庫頁面時發生，即使作業系統傳回成功訊息時，資料仍永不寫入磁碟，或是寫入到錯誤的位置。這稱為*遺失清除*。為避免遺失清除遺失資料，ESE 在資料庫中包含遺失清除偵測機制以及頁面修補功能 (單一頁面還原)。

  - **儲存邏輯損毀**  資料是以使用者非預期的方式新增、刪除或處理。這些情況通常是由協力廠商應用程式所造成。它通常只是因為使用者看起來像損毀而被視為損毀。Exchange 存放區會將產生邏輯損毀的交易視為一系列有效的 MAPI 作業。Exchange 2013 中的訴訟資料暫留功能可避免儲存邏輯損毀 (因為它可以防止內容被使用者或應用程式永久刪除)。不過，也有可能是使用者信箱變成嚴重損毀的情況下，使其更容易將資料庫還原至損毀之前的特定時間點，然後匯出使用者信箱以擷取未損毀的資料。

資料庫副本、保留原則和 ESE 單一頁面還原的組合還原只會保留罕見但嚴重的儲存邏輯損毀情況。您對於是否要搭配重新顯示延遲 (延遲副本) 使用資料庫副本的決定，將取決於您所使用的協力廠商應用程式，以及組織使用儲存邏輯損毀的歷程記錄。

延遲的副本可以該注意自己的 Exchange 2013 時呼叫自動記錄重新顯示來減少記錄檔在特定情況下：

  - 達到低磁碟空間閾值時

  - 當延遲副本具有實體損毀，需要進行頁面修補時

  - 當超過 24 小時少於三個可用的正常副本 (僅限主動或被動，不計算延遲資料庫副本)。

使用透過功能此自動減少延遲副本修補頁面。如果系統偵測認為修補頁面需要延遲的副本，記錄會自動重新顯示到執行修補頁面延遲的副本。延遲的副本也叫用這個自動重新顯示功能及特定的一段時間的延遲的副本偵測為唯一可用的副本時已達到低磁碟空間閾值。

遲延副本減少行為預設為停用，並可透過執行下列命令來予以啟用。

    Set-DatabaseAvailabilityGroup <DAGName> -ReplayLagManagerEnabled $true

啟用之後，當副本少於三個時便會發生減少行為。您可以修改下列 DWORD 登錄值來變更預設值 3。

**HKLM\\Software\\Microsoft\\ExchangeServer\\v15\\Replay\\Parameters\\ReplayLagManagerNumAvailableCopies**

若要啟用磁碟空間過低閾值的減少功能，您必須設定下列登錄項目。

**HKLM\\Software\\Microsoft\\ExchangeServer\\v15\\Replay\\Parameters\\ReplayLagLowSpacePlaydownThresholdInMB**

設定上述任何登錄設定之後，重新啟動 Microsoft Exchange DAG 管理服務，讓變更生效。

例如，假設環境中的特定資料庫有 4 個副本 (3 個高可用性副本，1 個延遲副本)，且 ReplayLagManagerNumAvailableCopies 使用預設設定。如果非延遲副本因故而停止運作 (例如，因為暫停)，則延遲副本會在 24 小時內自動播放其記錄檔。

如果您不啟用`ReplayLagManagerEnabled`參數選擇使用延遲的副本，請注意下列隱含意義：

  - 重新顯示延遲時間是一個由系統管理員設定的值，且預設為停用。

  - 重新顯示延遲時間的預設設定為 0 天，最大設定為 14 天。

  - 延遲的副本不會被視為高可用性的副本。它們的設計是用於嚴重損壞復原，以防止儲存邏輯損毀。

  - 重新顯示延遲時間設定越大，資料庫復原程序所需的時間就越長。根據復原期間需要重新顯示之記錄檔的數目，以及硬體重新顯示的速度，復原資料庫可能需花費數小時或更久。

  - 建議您判斷延遲的副本對於您的整體嚴重損壞復原策略是否重要。如果使用它們對策略來說很重要，建議您使用多個延遲的副本；如果您沒有多個延遲的副本，請使用獨立磁碟容錯陣列 (RAID) 來保護單一延遲的副本。如果您遺失磁碟，或者如果發生損毀，就不會遺失延遲時間點。

  - 延遲的副本不能使用 ESE 單一頁面還原功能進行修補。如果延遲的副本發生資料庫頁面損毀 (例如，-1018 錯誤)，則必須將其重新植入 (將會失去副本的延遲層面)。

如果您希望資料庫重新顯示所有記錄檔，並使資料庫副本保持在最新狀態，啟動及復原延遲的信箱資料庫副本是很簡單的程序。如果您要重新顯示截至某一個特定時間點的記錄檔，這會是較困難的作業，因爲您必須手動操作記錄檔並執行 Exchange Server 資料庫公用程式 (Eseutil.exe)。

如需如何啟動延遲信箱資料庫副本的詳細步驟，請參閱[啟動延遲的信箱資料庫副本](activate-a-lagged-mailbox-database-copy-exchange-2013-help.md)。

## 截斷延遲時間

截斷延遲時間是信箱資料庫副本的內容，其中指定記錄檔已重新顯示至資料庫副本後，延遲資料庫副本的記錄檔刪除的時間 (以分鐘為單位)。當記錄檔已被複寫到被動副本、成功通過檢查，並且成功重新顯示至資料庫副本時，截斷延遲計時器便會啟動。透過延遲資料庫副本記錄檔的截斷，您可以從影響資料庫使用中副本之記錄檔的失敗中復原。

## 資料庫副本和記錄檔截斷

記錄截斷相同中運作Exchange 2013Exchange 2010中一樣。截斷行為是由重新顯示延遲時間和截斷延遲時間設定複本所決定。

延遲設定保留為其預設值 0 (停用) 時，必須符合下列條件，才會截斷資料庫副本的記錄檔：

  - 必須已成功備份記錄檔，或者必須啟用循環記錄。

  - 記錄檔必須在資料庫的檢查點 (復原所需的最小記錄檔) 之下。

  - 其他所有延遲的副本必須已檢查記錄檔。

  - 其他所有副本 (非延遲的副本) 必須已重新顯示該記錄檔。

必須符合下列條件，延遲的資料庫副本才會發生截斷：

  - 記錄檔必須位於資料庫的檢查點之下。

  - 記錄檔必須比 ReplayLagTime + TruncationLagTime 更舊。

  - 必須已在使用中的副本上截斷記錄檔。

在 Exchange 2013 中，有一或多個被動副本暫停時，主動信箱資料庫副本上並不會發生記錄截斷。如果規劃好的維護活動執行時間長 (例如數天)，則可能會累積相當長的記錄檔。若要避免記錄磁碟機填滿了交易記錄，您可以將受影響的被動資料庫副本移除，而非暫停它。完成規劃的維護後，您可以重新新增被動資料庫副本。

Exchange 2013 Service Pack 1 (SP1) 引進稱為「鬆散截斷」(預設予以停用) 的新功能。正常作業期間，在資料庫的所有副本皆確認已重新顯示 (被動副本) 或接收到 (遲延副本) 記錄檔之前，每個資料庫副本都會保留需要傳送至其他資料庫副本的記錄。這是預設記錄截斷行為。如果資料庫副本因某個原因而離線，則記錄檔會始累積於資料庫的其他副本所使用的磁碟上。如果受影響的資料庫副本長時間離線，則可能會導致其他資料庫副本的磁碟空間不足。

啟用鬆散截斷時，截斷行為將會不同。每個資料庫副本都會追蹤本身的可用磁碟空間，並在可用空間偏低時套用鬆散截斷行為。就主動副本而言，最舊的落後副本 (在記錄重新顯示中最落後的被動資料庫副本) 會被忽略，而會從其餘最舊的被動副本開始截斷。全域截斷會在主動資料庫副本中計算。被動副本會嘗試依循主動副本的既定截斷決策。撇開 MinCopiesToProtect 這個名稱隱含的意義，Exchange 將只會忽略執行截斷時已知的最舊落後副本。就被動副本而言，當可用空間偏低時，其記錄檔將會根據以下說明的設定參數個別截斷。

離線資料庫重新連線時，將會遺漏已從其他狀況良好副本中刪除的記錄檔，而其狀況良好副本狀態會是 FailedAndSuspended。在此情況下，如果設定 Autoreseed，則會自動重新植入受影響的副本。如果未設定 Autoreseed，則系統管理員需要手動植入資料庫副本。

必要的狀況良好副本數目、可用磁碟空間閾值以及要保留的記錄數目都是可設定的參數。根據預設，可用磁碟空間閾值為 204800 MB (200 GB)、為被動副本保留的記錄數目為 100,000 個 (100 GB)，主動副本則為 10,000 個 (10 GB)。

編輯每個 DAG 成員上的 Windows 登錄，即可執行啟用鬆散截斷以及設定鬆散截斷參數。有三個可設定的登錄值都是儲存在 HKLM\\Software\\Microsoft\\ExchangeServer\\v15\\BackupInformation 下方。在預設情況下，具有下列 DWORD 值的 BackupInformation 機碼並不存在，而必須手動建立。下表說明 BackupInformation 下的 DWORD 登錄值：


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>登錄值</th>
<th>描述</th>
<th>預設值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>LooseTruncation_MinCopiesToProtect</p></td>
<td><p>此機碼可用來啟用鬆散截斷。它代表在資料庫的主動副本上要受到保護而不進行鬆散截斷的被動副本數目。將這個機碼的值設定為 0，即會停用鬆散截斷。</p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p>LooseTruncation_MinDiskFreeSpaceThresholdInMB</p></td>
<td><p>觸發鬆散截斷的可用磁碟空間 (MB) 閾值。如果可用磁碟空間低於這個值，則會觸發鬆散截斷。</p></td>
<td><p>如果未設定此登錄值，則鬆散截斷會使用預設值 200 GB。</p></td>
</tr>
<tr class="odd">
<td><p>LooseTruncation_MinLogsToProtect</p></td>
<td><p>要截斷記錄的狀況良好副本上所要保留的記錄檔數目下限。如果設定了此登錄值，則會同時對主動和被動副本套用此設定值。</p></td>
<td><p>如果未設定此登錄值，則會使用被動資料庫副本的預設值 100,000 和主動資料庫副本的預設值 10,000。</p></td>
</tr>
</tbody>
</table>


使用 LooseTruncation\_MinLogsToProtect 登錄值時，請留意主動和被動資料庫副本的行為並不相同。在主動資料庫副本上，這是在受保護的被動副本和必要範圍內的主動副本所需要的數目以外事先另行保留的記錄數目。在被動資料庫副本上，這則是從最新的可用記錄中保留的記錄數目。此外，此數目有十分之一會用來在此被動副本的必要範圍以外事先保留記錄。之所以設定這兩項限制，是為了確保延遲的資料庫副本不會佔用太多空間，因為其必要範圍通常很大。

## 資料庫啟動原則

有時候您可能想要建立信箱資料庫副本，並在失敗發生時，防止系統自動啟動該副本，例如：

  - 如果您將一或多個信箱資料庫副本部署至另一個或待命的資料中心。

  - 如果您將延遲的資料庫副本設定為用於復原用途。

  - 如果您正在執行伺服器維護或升級。

在先前的每個案例中，您有幾個不想要讓系統自動啟動的資料庫副本。若要防止系統自動啟動信箱資料庫副本，您可以將副本設定為阻止 (暫停) 啟動。這可讓系統透過記錄檔傳送和重新顯示，使副本維持在最新狀態，但防止系統自動啟動與使用該副本。阻止啟動的副本必須由系統管理員手動啟動。您可以對整個伺服器使用 [Set-MailboxServer](https://technet.microsoft.com/zh-tw/library/aa998651\(v=exchg.150\)) Cmdlet 或對個別資料庫副本使用 [Set-MailboxDatabaseCopy](https://technet.microsoft.com/zh-tw/library/dd298104\(v=exchg.150\)) Cmdlet 設定資料庫啟動原則，以將 *DatabaseCopyAutoActivationPolicy* 參數設定為「封鎖」。

如需設定資料庫啟動原則的詳細資訊，請參閱[設定信箱資料庫複本的啟動原則](configure-activation-policy-for-a-mailbox-database-copy-exchange-2013-help.md)。

## 在連續複寫上移動信箱的影響

在高記錄檔產生率的忙碌信箱資料庫中，如果複寫至被動資料庫副本無法與記錄檔產生保持同步，則很有可能會造成資料遺失。有一個情況可推動高記錄檔產生率，即為信箱移動。Exchange 2013 包含服務所使用的「資料保證 API」(如 Microsoft Exchange 信箱複寫服務 (MRS))，可根據由系統或管理原設定之 *DataMoveReplicationConstraint* 參數的值檢查資料庫副本架構的健康狀況。具體而言，「資料保證 API」可用於：

  - **檢查複寫健康狀況** 確認資料庫副本的必要條件數為可用。

  - **檢查複寫清除** 確認必要的記錄檔已對應資料庫副本的必要條件數重新顯示。

執行時，API 會將以下狀態資訊傳回呼叫應用程式：

  - \[重試\] 表示有暫時性錯誤，導致無法對應資料庫檢查條件。

  - \[滿意\] 表示資料庫符合必要條件或資料庫未複寫。

  - \[不滿意\] 表示資料庫不符合必要條件。此外，傳回 \[不滿意\] 回應之原因的相關資訊已提供給呼叫應用程式。

適用於信箱資料庫的 *DataMoveReplicationConstraint* 參數的值可決定有多少資料庫副本應評估為要求的一部分。*DataMoveReplicationConstraint* 參數有以下可能的值：

  - `None`  當您建立信箱資料庫時，應該依預設設定此值。當此值已設定時，會忽略「資料保證 API」條件。此值應該僅用於未複寫的信箱資料庫。

  - `SecondCopy`  這是當您新增第二個信箱資料庫副本時的預設值。當此值已設定時，至少有一個被動資料庫副本必須符合「資料保證 API」條件。

  - `SecondDatacenter`  當此值已設定時，另一個 Active Directory 站台中至少有一個被動資料庫副本必須符合「資料保證 API」條件。

  - `AllDatacenters`  當此值已設定時，每一個 Active Directory 站台中至少有一個被動資料庫副本必須符合「資料保證 API」條件。

  - `AllCopies`  當此值已設定時，信箱資料庫的所有副本皆必須符合「資料保證 API」條件。

**檢查複寫健康狀況**

當執行「資料保證 API」以評估資料庫副本基礎架構的健康狀況時，會評估幾個項目。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>如果 <em>DataMoveReplicationConstraint</em> 參數設定為…</th>
<th>那麼，對於給定的資料庫...</th>
<th>條件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>SecondCopy</code></p></td>
<td><p>對於複寫的資料庫，至少有一個被動資料庫副本必須符合下一欄中的條件。</p></td>
<td><p>被動資料庫副本必須：</p>
<ul>
<li><p>健康狀況良好。</p></li>
<li><p>在 10 分鐘的重新顯示延遲時間內重新顯示佇列。</p></li>
<li><p>少於 10 筆記錄的複製佇列長度。</p></li>
<li><p>平均複製佇列長度少於 10 筆記錄。平均複製佇列長度根據應用程式已查詢資料庫狀態的次數而計算。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code>SecondDatacenter</code></p></td>
<td><p>另一個 Active Directory 站台中至少有一個被動資料庫副本必須符合下一欄中的條件。</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>AllDatacenters</code></p></td>
<td><p>必須裝載作用中副本，而且每一個 Active Directory 站台中的被動資料庫副本必須符合下一欄中的條件。</p></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>AllCopies</code></p></td>
<td><p>必須裝載作用中副本，而且所有被動資料庫副本必須符合下一欄中的條件。</p></td>
<td></td>
</tr>
</tbody>
</table>


**檢查複寫清除**

「資料保證 API」也可用來驗證資料庫副本的必要條件數已重新顯示必要的交易記錄。這是藉由比較最後記錄重新顯示時間戳記與呼叫服務的認可時間戳記 (大部分情況下，這是包含必要資料之最後記錄檔的時間戳記) 來進行驗證，再另外加上五秒鐘 (處理系統時間偏移或漂移)。如果重新顯示時間戳記晚於認可時間戳記，則會滿足 *DataMoveReplicationConstraint* 參數。如果重新顯示戳記早於認可時間戳記，則不會滿足 *DataMoveReplicationConstraint* 參數。

將大量信箱移進或移出 DAG 中的複寫資料庫之前，建議根據以下事項在每一個信箱資料庫設定 *DataMoveReplicationConstraint* 參數：


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>如果您正在部署...</th>
<th>將 DataMoveReplicationConstraint 設定…</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>沒有任何資料庫副本的信箱資料庫</p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p>單一 Active Directory 站台內的 DAG</p></td>
<td><p><code>SecondCopy</code></p></td>
</tr>
<tr class="odd">
<td><p>使用延伸 Active Directory 站台的多個資料中心中的 DAG</p></td>
<td><p><code>SecondCopy</code></p></td>
</tr>
<tr class="even">
<td><p>跨兩個 Active Directory 站台的 DAG，而且您對每一個站台中的資料庫副本有高可用性</p></td>
<td><p><code>SecondDatacenter</code></p></td>
</tr>
<tr class="odd">
<td><p>跨兩個 Active Directory 站台的 DAG，而且您在第二個站台中只有一個延遲資料庫副本</p></td>
<td><p><code>SecondCopy</code></p>
<p>這是因為記錄檔在重新顯示至資料庫副本之前，「資料保證 API」不保證待認可的資料，而且由於待延遲的資料庫副本的性質，此限制將造成無法移動要求，除非延遲資料庫副本 ReplayLagTime 值低於 30 分鐘。</p></td>
</tr>
<tr class="even">
<td><p>跨三個或三個以上 Active Directory 站台的 DAG，每一個站台將包含高可用性的資料庫副本</p></td>
<td><p><code>AllDatacenters</code></p></td>
</tr>
</tbody>
</table>


## 平衡資料庫副本

由於 DAG 的固有性質 (因為資料庫轉換或容錯移轉)，使用中信箱資料庫副本會在整個 DAG 的存留時間內多次變更主機。因此，DAG 在使用中信箱資料庫副本散發方面可能變得不平衡。下表顯示 DAG 的範例，該 DAG 具有四個資料庫，每個資料庫各有四份副本 (每部伺服器上共有 16 個資料庫)，且使用中資料庫副本的散發不平均。

### 具有不平衡的使用中副本散發的 DAG

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>伺服器</th>
<th>主動資料庫數目</th>
<th>被動資料庫數目</th>
<th>裝載的資料庫數目</th>
<th>卸載的資料庫數目</th>
<th>喜好設定計數清單</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EX1</p></td>
<td><p>5</p></td>
<td><p>11</p></td>
<td><p>5</p></td>
<td><p>0</p></td>
<td><p>4, 4, 3, 5</p></td>
</tr>
<tr class="even">
<td><p>EX2</p></td>
<td><p>1</p></td>
<td><p>15</p></td>
<td><p>1</p></td>
<td><p>0</p></td>
<td><p>1, 8, 6, 1</p></td>
</tr>
<tr class="odd">
<td><p>EX3</p></td>
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>12</p></td>
<td><p>0</p></td>
<td><p>13, 2, 1, 0</p></td>
</tr>
<tr class="even">
<td><p>EX4</p></td>
<td><p>1</p></td>
<td><p>15</p></td>
<td><p>1</p></td>
<td><p>0</p></td>
<td><p>1, 1, 5, 9</p></td>
</tr>
</tbody>
</table>


在先前的範例中，每個資料庫有四份副本，因此，只有四個啟動喜好設定的可能值 (1、2、3 或 4)。**\[喜好設定計數清單\]** 欄位顯示具有每一個這些值之資料庫數目的計數。例如，在 EX3 上，有 13 份資料庫副本的啟動喜好設定為 1、兩份副本的啟動喜好設定為 2、一份副本的啟動喜好設定為 3，而沒有任何副本的啟動喜好設定為 4。

如您所見，在每個 DAG 成員所主控的使用中資料庫數目、每個 DAG 成員所主控的被動資料庫數目，或主控之資料庫的啟動喜好設定計數等方面，此 DAG 並不平衡。

您可以使用 RedistributeActiveDatabases.ps1 指令碼，以平衡跨 DAG 的使用中信箱資料庫副本。此指令碼會在資料庫副本之間移動資料庫，嘗試讓 DAG 中的每一部伺服器上擁有相等的裝載資料庫數目。如有需要，此指令碼還會嘗試跨站台平衡使用中資料庫。

指令碼提供兩個用來在 DAG 中平衡使用中資料庫副本的選項：

  - **BalanceDbsByActivationPreference**  指定此選項時，無論 Active Directory 站台為何，指令碼都會嘗試將資料庫移至最慣用的副本 (根據 \[啟動喜好設定\])。

  - **BalanceDbsBySiteAndActivationPreference**  指定此選項時，指令碼會嘗試將使用中資料庫移至最慣用的副本，同時嘗試平衡每個 Active Directory 站台中的使用中資料庫。

使用第一個選項執行指令碼之後，先前不平衡的 DAG 會變成平衡，如下表所示。

### 具有平衡的使用中副本散發的 DAG

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>伺服器</th>
<th>主動資料庫數目</th>
<th>被動資料庫數目</th>
<th>裝載的資料庫數目</th>
<th>卸載的資料庫數目</th>
<th>喜好設定計數清單</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EX1</p></td>
<td><p>4</p></td>
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>0</p></td>
<td><p>4, 4, 4, 4</p></td>
</tr>
<tr class="even">
<td><p>EX2</p></td>
<td><p>4</p></td>
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>0</p></td>
<td><p>4, 4, 4, 4</p></td>
</tr>
<tr class="odd">
<td><p>EX3</p></td>
<td><p>4</p></td>
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>0</p></td>
<td><p>4, 4, 4, 4</p></td>
</tr>
<tr class="even">
<td><p>EX4</p></td>
<td><p>4</p></td>
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>0</p></td>
<td><p>4, 4, 4, 4</p></td>
</tr>
</tbody>
</table>


如上表所示，在每部伺服器上的使用中和被動資料庫數目方面，以及跨伺服器的啟動喜好設定方面，此 DAG 目前已平衡。

下表列出 RedistributeActiveDatabases.ps1 指令檔的可用參數。

### RedistributeActiveDatabases.ps1 指令碼參數

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>參數</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>DagName</em></p></td>
<td><p>指定要重新平衡的 DAG 名稱。若省略此參數，會使用本機伺服器為其成員的 DAG。</p></td>
</tr>
<tr class="even">
<td><p><em>BalanceDbsByActivationPreference</em></p></td>
<td><p>指定無論 Active Directory 站台為何，指令碼都應該將資料庫移至最慣用的副本。</p></td>
</tr>
<tr class="odd">
<td><p><em>BalanceDbsBySiteAndActivationPreference</em></p></td>
<td><p>指定指令碼應該嘗試將使用中資料庫移至最慣用的副本，同時嘗試平衡每個 Active Directory 站台中的使用中資料庫。</p></td>
</tr>
<tr class="even">
<td><p><em>ShowFinalDatabaseDistribution</em></p></td>
<td><p>指定在轉散發完成之後，顯示目前資料庫散發的報告。</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowedDeviationFromMeanPercentage</em></p></td>
<td><p>指定允許跨站台的使用中資料庫變化，並以百分比表示。預設值為 20%。例如，如果有 99 個資料庫在三個站台之間散發，則理想的散發應該是每個站台 33 個資料庫。如果允許的偏差為 20%，則指令碼會嘗試平衡資料庫，以便每個站台不會高於或低於此數字超過 10%。33 的 10% 為 3.3，且會進位至 4。因此，指令碼會嘗試讓每個站台有 29 到 37 個資料庫。</p></td>
</tr>
<tr class="even">
<td><p><em>ShowDatabaseCurrentActives</em></p></td>
<td><p>指定指令碼針對每個資料庫產生一份報告，其中詳細說明資料庫的移動方式，以及資料庫目前在其最慣用的副本上是否為使用中。</p></td>
</tr>
<tr class="odd">
<td><p><em>ShowDatabaseDistributionByServer</em></p></td>
<td><p>指定指令碼針對每部伺服器產生一份報告，其中顯示其資料庫散發。</p></td>
</tr>
<tr class="even">
<td><p><em>RunOnlyOnPAM</em></p></td>
<td><p>指定指令碼只在目前擁有 PAM 角色的 DAG 成員上執行。指令碼會確認它是從 PAM 執行。如果它不是從 PAM 執行，則指令碼會結束。</p></td>
</tr>
<tr class="odd">
<td><p><em>LogEvents</em></p></td>
<td><p>指定指令碼應記錄包含動作摘要的事件 (MsExchangeRepl event 4115)。</p></td>
</tr>
<tr class="even">
<td><p><em>IncludeNonReplicatedDatabases</em></p></td>
<td><p>指定指令碼在決定如何轉散發使用中資料庫時，應納入非複寫的資料庫 (未包含副本的資料庫)。雖然非複寫的資料庫無法移動，但是可能會影響複寫資料庫的散發。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Confirm 參數可用來隱藏執行命令檔時依預設出現的確認提示。若要隱藏確認提示，請使用語法 -Confirm:$False。您必須在語法中加入冒號 ( :)。</p></td>
</tr>
</tbody>
</table>


## RedistributeActiveDatabases.ps1 範例

此範例顯示 DAG 目前的資料庫散發，包括喜好設定計數清單。

    RedistributeActiveDatabases.ps1 -DagName DAG1 -ShowDatabaseDistributionByServer | Format-Table

此範例會使用啟動喜好設定來轉散發及平衡 DAG 中的使用中信箱資料庫副本。

    RedistributeActiveDatabases.ps1 -DagName DAG1 -BalanceDbsByActivationPreference -Confirm:$False

此範例會使用啟動喜好設定來轉散發及平衡 DAG 中的使用中信箱資料庫副本，並產生散發的摘要。

    RedistributeActiveDatabases.ps1 -DagName DAG1 -BalanceDbsByActivationPreference -ShowFinalDatabaseDistribution

## 監視資料庫副本

如果發生會影響資料庫使用中副本的失敗，資料庫副本是第一道防線。因此，監視資料庫副本的健全狀況和狀態，以確保它們在需要時可供使用十分重要。您可以藉由檢查 EAC 中資料庫副本的詳細資料，檢視各種資訊，包含副本佇列長度、重新顯示佇列長度、狀態，以及索引狀態資訊。您也可以在命令介面中使用 **Get-MailboxDatabaseCopyStatus** 指令程式以檢視資料庫副本的各種狀態資訊。

如需監視資料庫副本的詳細資訊，請參閱[監視資料庫可用性群組](monitoring-database-availability-groups-exchange-2013-help.md)。

## 移除資料庫副本

您可以使用 EMC 或命令介面的 **Remove-MailboxDatabaseCopy** Cmdlet，隨時移除資料庫副本。在移除資料庫副本之後，必須手動刪除所移除資料庫副本所在伺服器上的任何資料庫和交易記錄檔。如需如何移除資料庫副本的詳細步驟，請參閱[移除信箱資料庫副本](remove-a-mailbox-database-copy-exchange-2013-help.md)。

## 資料庫轉換

主控資料庫作用中副本的信箱伺服器稱為信箱資料庫主機。啟動被動資料庫副本的程序會變更資料庫的信箱資料庫主機，並將被動副本變成新的使用中副本。這個程序稱為資料庫轉換。在資料庫轉換中，資料庫的使用中副本會從信箱伺服器上卸載，而且該資料庫的被動副本會掛載為另一個信箱伺服器上新的使用中信箱資料庫。執行轉換時，您可以選擇性地覆寫新信箱資料庫主機上的資料庫裝載撥號設定。

您可以在 EAC 中的 \[資料庫副本\] 索引標籤下檢閱右側欄，快速識別哪個信箱伺服器是目前的信箱資料庫主機。您可以使用 EAC 中的 \[啟動\] 連結，或使用命令介面中的 **Move-ActiveMailboxDatabase** Cmdlet 來執行轉換。

在啟動被動副本之前，有幾個需要執行的內部檢查：

  - 檢查資料庫副本的狀態。如果資料庫副本的狀態為失敗，則會阻止轉換。您可以使用 **Move-ActiveMailboxDatabase** 指令程式的 *SkipHealthChecks* 參數來覆寫此行為，並略過健全狀況檢查。此參數可讓您在失敗狀態下，將使用中的副本移至資料庫副本。

  - 主動資料庫副本會查看其目前是否為任何資料庫被動副本的植入來源。如果作用中副本目前作為植入來源，則會封鎖轉換。您可以使用 **Move-ActiveMailboxDatabase** Cmdlet 中的 *SkipActiveCopyChecks* 參數來覆寫此行為，並略過植入來源檢查。此參數可讓您移動要作為植入來源的主動副本。使用此參數將造成植入作業取消，並視為失敗。

  - 檢查資料庫副本的副本佇列和重新顯示佇列長度，以確定其值在設定條件內。同時，驗證資料庫副本以確定它目前並未當做植入的來源使用。如果佇列長度的值在設定的條件以外，或如果資料庫目前當做植入的來源使用，則會阻止轉換。您可以使用 **Move-ActiveMailboxDatabase** 指令程式的 *SkipLagChecks* 參數來覆寫此行為，並略過這些檢查。此參數會允許啟動在所設定條件之外重新顯示及複製佇列的副本。

  - 檢查資料庫副本的搜尋類別目錄 (內容索引) 的狀態。如果搜尋類別目錄不是最新的、處於不正常的狀態或已損毀，則會阻止轉換。您可以使用 **Move-ActiveMailboxDatabase** 指令程式的 *SkipClientExperienceChecks* 參數來覆寫此行為，並略過搜尋類別目錄檢查。這個參數會造成此搜尋略過類別目錄健全狀況檢查。如果您在啟動之資料庫副本的搜尋類別目錄處於不正常或無法使用的狀態，而您使用此參數略過類別目錄健全狀況檢查並啟動資料庫副本，您將需要再次對搜尋類別目錄進行編目，或是再次植入搜尋類別目錄。

執行資料庫轉換時，您也可以選擇覆寫為主控要啟動之被動資料庫副本的伺服器設定的裝載撥號設定。使用 **Move-ActiveMailboxDatabase** 指令程式的 *MountDialOverride* 參數指示目標伺服器覆寫其自己的裝載撥號設定， 並使用由 *MountDialOverride* 參數指定的內容。

如需執行資料庫副本轉換的詳細步驟，請參閱[啟動信箱資料庫副本](activate-a-mailbox-database-copy-exchange-2013-help.md)。

