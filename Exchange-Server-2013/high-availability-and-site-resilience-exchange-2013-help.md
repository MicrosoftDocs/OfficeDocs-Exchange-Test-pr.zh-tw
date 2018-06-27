---
title: '高可用性和站台恢復: Exchange 2013 Help'
TOCTitle: 高可用性和站台恢復
ms:assetid: 6628285e-d07c-443d-866b-be784ad1ed1e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd638137(v=EXCHG.150)
ms:contentKeyID: 50473346
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 高可用性和站台恢復

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-15_

您可以設定信箱伺服器和資料庫的高可用性和站台恢復功能，以保護 Exchange Server 2013 信箱資料庫及其所包含的資料。Exchange 2013 可將部署高可用性和恢復通訊解決方案的成本和複雜度降到最低，同時還提供高度的服務和資料可用性，並支援非常大的信箱。

Exchange 2013 可讓所有規模和所有領域的客戶，根據 Exchange 2010 中引進的原生複寫功能和高可用性架構，在其組織中以經濟實惠的方式部署郵件持續性服務。如需有關對 Exchange 2010 和 Exchange 2007 所做變更的清單，請參閱＜[變更至與舊版不同的高可用性與站台回復性](changes-to-high-availability-and-site-resilience-over-previous-versions-exchange-2013-help.md)＞。

**目錄**

Key terminology

Database availability groups

Mailbox database copies

Active Manager

Site resilience

Third-party replication API

High availability and site resilience documentation

## 重要詞彙

下列重要術語對於了解高可用性或站台回復性相當重要：

  - *Active Manager*  
    在 Microsoft Exchange 複寫服務內部運作的一個內部 Exchange 元件，主要負責透過在資料庫可用性群組 (DAG) 中容錯移轉的失敗監視和修正動作。

<!-- end list -->

  - *AutoDatabaseMountDial*  
    信箱伺服器的內容設定，用以確定是否將被動資料庫副本自動裝載為新的主動副本，根據裝載副本所遺失的記錄檔數目而定。

<!-- end list -->

  - *連續複寫 - 區塊模式*  
    在區塊模式中，每項更新都會寫入到主動資料庫副本的主動記錄緩衝區，同時也會傳送到封鎖模式下每個被動信箱副本上的記錄緩衝區。當記錄緩衝區已滿時，每個資料庫副本會依產生順序建置、檢查和建立下一個記錄檔。

<!-- end list -->

  - *連續複寫 - 檔案模式*  
    在檔案模式中，會從主動資料庫副本推送已關閉交易記錄檔至一個或多個被動資料庫副本。

<!-- end list -->

  - *資料庫可用性群組*  
    最多 16 個 Exchange 2013 信箱伺服器的群組，主控一組已複寫的資料庫。

<!-- end list -->

  - *資料庫行動力*  
    複寫所在和掛接在其他 Exchange 2013 信箱伺服器上之 Exchange 2013 信箱資料庫的能力。

<!-- end list -->

  - *資料中心*  
    通常，這是指 Active Directory 站台，但是也可以指實體站台。在此文件的內容中，資料中心等同於 Active Directory 站台。

<!-- end list -->

  - *資料中心啟動協調模式*  
    DAG 設定的內容於啟用時會強制 Microsoft Exchange 複寫服務取得權限，以在啟動時裝載資料庫。

<!-- end list -->

  - *嚴重損壞修復*  
    用於以手動方式從失敗中復原的任何處理程序。可以是影響單一項目的失敗，或是影響整個實體位置的失敗。

<!-- end list -->

  - *交換協力廠商複寫 API*  
    Exchange 所提供的 API，可使用 DAG 的協力廠商同步複寫，來代替連續複寫。

<!-- end list -->

  - *高可用性*  
    提供影響服務或資料 (例如網路、儲存或伺服器失敗) 的服務可用性、資料可用性和故障自動復原之解決方案。

<!-- end list -->

  - *增量部署*  
    Exchange 2013 安裝後部署高可用性和站台回復性的能力。

<!-- end list -->

  - *延遲的信箱資料庫副本*  
    記錄檔重新執行延隔時間大於 0 的被動信箱資料庫副本。

<!-- end list -->

  - *信箱資料庫副本*  
    信箱資料庫 (.edb 檔和記錄檔) 為主動或被動。

<!-- end list -->

  - *信箱恢復功能*  
    Exchange 2013 中整合高可用性和站台回復性解決方案的名稱。

<!-- end list -->

  - *受管理的可用性*  
    由探查、監視和回應程式所組成的一組內部程序，結合了所有伺服器角色和所有通訊協定的監視與高可用性。

<!-- end list -->

  - *\[\*over\]* (讀成 "star over")  
    *\[switchovers\] (轉換)* 和 *\[failovers\] (容錯移轉)* 的簡寫。轉換是指一或多個資料庫副本的手動啟動。容錯移轉是指一或多個資料庫副本發生故障後的自動啟動。

<!-- end list -->

  - *安全網*  
    以前稱為傳輸暫放，這是傳輸服務的一項功能，可儲存所有郵件副本 *X* 天。預設值為 2 天。

<!-- end list -->

  - *陰影備援*  
    一種傳輸伺服器功能，在郵件的整個傳送過程中提供郵件備援。

<!-- end list -->

  - *站台回復性*  
    此組態可將郵件基礎結構擴充至多個 Active Directory 站台，當發生會影響任一站台的故障時，可為郵件系統提供運作持續性。

回到頁首

## 資料庫可用性群組

DAG 是建置於 Exchange 2013 的高可用性和站台回復性架構之基礎元件。DAG 是一組多達 16 個信箱伺服器的群組，可主控資料庫集，並提供從影響個別資料庫、網路或伺服器的失敗中自動進行資料庫層級復原的功能。DAG 中的任何伺服器都可以主控來自 DAG 中任何其他伺服器的信箱資料庫副本。當伺服器新增至 DAG 後，它即可與 DAG 中其他的伺服器搭配使用，以便針對影響信箱資料庫的失敗 (例如磁碟故障或伺服器失敗) 進行自動復原功能。如需 DAG 的詳細資訊，請參閱[資料庫可用性群組 (DAGs)](database-availability-groups-dags-exchange-2013-help.md)。

回到頁首

## 信箱資料庫副本

Exchange 2010 中第一次引進的高可用性和站台回復性功能用於 Exchange 2013，可建立和維護資料庫副本。Exchange 2013 還採用資料庫行動性的概念，是Exchange 受管的資料庫層級容錯移轉。

資料庫行動性可中斷資料庫與伺服器的連線，並新增對多達 16 份單一資料庫副本的支援。它還提供建立資料庫副本的原生體驗。

設定資料庫副本作為主動信箱資料庫，即稱為 *\[轉換\]*。當發生失敗影響資料庫或存取資料庫，且新資料庫成為主動副本時，此處理程序稱為 \[容錯移轉\]。此處理程序還涉及伺服器故障，一個或多個伺服器讓以前在故障伺服器上的線上資料庫處於線上狀態。當發生轉換或容錯移轉，其他 Exchange 2013 伺服器幾乎立即得知轉換，並將用戶端和通訊流量重新導向至新的主動資料庫。

例如，如果 DAG 的主動資料庫因基礎存放區故障而失敗，Active Manager 會自動復原，其方法是透過在 DAG 的另一個信箱資料庫上容錯移轉至資料庫副本。在 Exchange 2013，受管理的可用性會新增新的行為以恢復所喪失的對資料庫的通訊協定存取能力，包括回收應用程式工作者集區、重新啟動服務和伺服器，並啟動資料庫容錯移轉。

如需信箱資料庫副本的詳細資訊，請參閱[信箱資料庫副本](mailbox-database-copies-exchange-2013-help.md)。

回到頁首

## Active Manager

Exchange 2013 利用 Exchange 2010 中引進的 Active Manager 元件來管理資料庫和資料庫副本健康狀況、狀態、持續複寫和其他方面的信箱伺服器高可用性功能。如需 Active Manager 的相關資訊，請參閱 [Active Manager](active-manager-exchange-2013-help.md)。

回到頁首

## 站台回復性

雖然 Exchange 2013 持續將 DAG 和 Windows 容錯移轉叢集用於 Mailbox server role 高可用性和站台恢復，但與 Exchange 2013 中的站台恢復不同。因為已經過簡化，所以優於 Exchange 2013 中的站台恢復。Exchange 2013 中的基礎架構變更對站台恢復組態的復原層面有顯著影響。

在 Exchange 2010 中，信箱 (DAG) 和用戶端存取 (Client Access Server 陣列) 復原聯結在一起。如果您遺失所有 Client Access Server、陣列的 VIP 或大部分 DAG，則必須執行資料中心轉換。雖然此程序需要一定的時間來執行，並且需要人為介入才能開始，但它已有充分的文件記錄，而且眾所周知。

在 Exchange 2013 中，如果您因任何原因遺失 Client Access Server 陣列 (例如負載平衡器故障)，您不必執行資料中心轉換。使用適當組態，容錯移轉會在用戶端層級發生，並且用戶端會自動重新導向至操作 Client Access Server 的第二個資料中心，這些操作 Client Access Server Proxy 的通訊會返回使用者仍然不受中斷影響的信箱伺服器 (因為您沒有執行轉換)。不進行復原服務，服務本身會自行復原，您可以專注於修正核心問題 (例如，更換故障的負載平衡器)。

此外，透過命名空間簡化、伺服器角色合併、減少 Active Directory 站台伺服器角色需求、區隔 Client Access Server 陣列與 DAG 復原，以及負載平衡變更，Exchange 2013 中的變更如今能夠區隔 Client Access Server 和 DAG 復原並在站台間自動進行，因此可提供資料中心容錯移轉方案 (需具備三個地點)。

在 Exchange 2010 中，您可以跨兩個資料中心部署 DAG，並在第三個資料中心內主控見證，以及為任一個資料中心的 Mailbox Server Role 啟用容錯移轉。但您並未取得解決方案本身的容錯移轉，因為仍然需要針對非 Mailbox Server Role 手動變更命名空間。

在 Exchange 2013 中，命名空間不需要與 DAG 一起移動。Exchange 運用容錯移轉透過多重 IP 位址、負載平衡建立至命名空間 (如果需要的話，使用啟用伺服器和停用伺服器的功能)。現代 HTTP 用戶端會自動使用此備援。HTTP 堆疊接受多重 IP 位址作為完整網域名稱 (FQDN)，如果第一個 IP 位址嘗試硬故障 (亦即無法連接)，將嘗試清單中的下一個 IP 位址。軟故障 (連線在工作階段建立後遺失，或許是因為服務發生間歇性故障，例如，裝置丟棄封包並且必須停用) 期間，使用者可能需要重新整理其瀏覽器。

這意味著命名空間不再是單一失敗點，因為它是在 Exchange 2010 中。在 Exchange 2010 中，訊息系統上最大的單一失敗點或許是您提供給使用者的 FQDN，因為它會告訴使用者前往何處。在 Exchange 2010 範例中，變更 FQDN 前往的位置並不容易，因為您必須變更 DNS，然後處理 DNS 延遲，其中某些部分極具挑戰性。瀏覽器中的名稱快取通常需大約 30 分鐘或更多，也必須處理。

Exchange 2013 中的一項變更是讓用戶端有一個以上可以前往的地方。假設用戶端能夠使用一個以上可以前往的地方 (Exchange 2013 內幾乎所有的用戶端存取通訊協定都是以 HTTP 為基礎 (範例包括 Outlook、Outlook Anywhere、EAS、EWS、OWA 和 EAC)，所有支援的 HTTP 用戶端都可以使用多重 IP 位址)，因此可以提供用戶端容錯移轉。您可以設定 DNS 以在名稱解析期間處理至用戶端的多重 IP 位址。例如，用戶端要求 mail.contoso.com 並送回兩個 IP 位址或四個 IP 位址。然而，用戶端取回的許多 IP 位址會由用戶端確實使用。這讓用戶端的境況更好，因為如果其中一個 IP 位址失敗，用戶端可以嘗試連接一個或多個其他 IP 位址。如果用戶端嘗試其中一個並且失敗，會等候大約 20 秒，然後嘗試清單中的下一個。因此，如果您遺失 Client Access Server 陣列的 VIP，用戶端會自動復原，並在大約 21 秒內完成。

優點包括下列各項：

  - 在 Exchange 2010 中，如果您在主要資料中心中遺失負載平衡器，並且該站台上沒有其他負載平衡器，則必須執行資料中心轉換。在 Exchange 2013 中，如果您在主要站台中遺失負載平衡器，只需將它關閉 (或可能是關閉 VIP) 並修復或更換它。尚未在次要資料中心內使用 VIP 的用戶端會自動容錯移轉至次要 VIP，名稱空間和 DNS 都不會有任何變更。這不僅意味著您不再須要執行轉換，也意味著不須要執行通常與資料中心轉換復原相關的作業。在 Exchange 2010 中，您必須處理 DNS 延遲 (因此，建議將存留時間 (TTL) 設定為 5 分鐘，並使用容錯回復 URL)。在 Exchange 2013 中，您不需要執行這項作業，因為在 VIP (資料中心) 之間命名空間的容錯移轉速度相當快 (20 秒)。

  - 因為您可以容錯移轉資料中心之間的命名空間，達到資料中心容錯移轉時所需的所有跨資料中心是一種連線機制的 Mailbox server role 的容錯移轉。若要取得 DAG 自動容錯移轉，您可以只包括工程師平均兩個資料中心，之間分割 DAG 的解決方案，然後將見證伺服器放在第三個位置以便仲裁式它可以是其中一個資料中心，不論狀態包含 DAG 成員資料中心之間的網路的 DAG 成員。 如果您只有兩個資料中心及第三個實體位置無法使用，您可以將見證伺服器放在 Microsoft Azure 虛擬機器上。請參閱[使用 Microsoft Azure 虛擬機器為 DAG 見證伺服器](using-a-microsoft-azure-vm-as-a-dag-witness-server-exchange-2013-help.md)如需詳細資訊。

  - 在此案例中，系統管理員僅專注於修復問題，而不是花時間還原服務。您只需修復失敗項；儘管服務已經執行，仍會保持資料完整性。修復損壞裝置時的緊迫性和壓力程度與還原服務時的緊迫性和壓力不同。對一般使用者而言，壓力更適當；對系統管理員而言，壓力更小。

您可以允許容錯移轉，而不必執行轉換 (有時會誤稱為容錯回復)。如果您在主要資料中心內遺失 Client Access Server，並導致用戶端發生 20 秒中斷，您可能甚至不在乎容錯回復。此時，您應該專注在修復核心問題 (例如，更換故障的負載平衡器)。回復上線並正常運作後，部分用戶端將可開始使用，其他用戶端可能維持經由第二個資料中心作業。

Exchange 2013 也提供讓系統管理員處理間歇性故障的功能。間歇性故障表現為，例如，可進行初始 TCP 連線，但之後沒有任何反應。間歇性故障需要採取某種形式的額外管理動作，因為它可能是由於更換投入使用的裝置所造成。進行此修復程序時，裝置可能需要開機並接受一些要求，但必須在執行必要的設定步驟之後，才會確實準備好向用戶端提供服務。在此案例中，系統管理員只需從 DNS 針對被更換的裝置移除 VIP，即可執行命名空間轉換。在該服務期間，沒有用戶端可以嘗試與其連線。更換程序完成後，系統管理員可以將 VIP 新增回 DNS，用戶端才最終可以開始使用。

如需有關站台恢復規劃與部署的詳細資訊，請參閱[規劃高可用性及站台恢復](planning-for-high-availability-and-site-resilience-exchange-2013-help.md)和[部署高可用性和站台恢復](deploying-high-availability-and-site-resilience-exchange-2013-help.md)。

回到頁首

## 協力廠商複寫 API

Exchange 2013 還包含一個協力廠商複寫 API，它可讓組織使用協力廠商的同步複寫解決方案，代替內建的連續複寫功能。Microsoft 可支援使用此 API 的協力廠商解決方案，前提是解決方案需提供必要的功能來取代因為使用 API 而停用的所有原生連續複寫功能。只有當 DAG 在內部使用此 API 來管理及啟動信箱資料庫副本時，才支援解決方案。不支援在這些界限以外使用 API。此外，該解決方案必須滿足適用的 Windows 硬體支援要求。(支援不需要測試驗證)

部署時使用內建協力廠商複寫 API 的解決方案，請注意解決方案廠商負責主要支援的解決方案。Microsoft 支援 Exchange 資料的複寫與非複寫解決方案。Microsoft 知識庫文章 895847、 [Exchange server 支援多個網站資料複寫](https://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=895847)中所述資料複寫的 Microsoft 支援原則必須依照使用資料複寫的解決方案。此外，使用 Windows 容錯移轉叢集資源模型的解決方案必須符合 Windows 叢集支援能力需求 Microsoft 知識庫文章 943984， [Microsoft 支援原則的 Windows Server 2008 或 Windows Server 2008 R2 容錯移轉叢集](https://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=943984)或[Microsoft 支援原則的 Windows Server 2012 容錯移轉叢集](https://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=2775067)中所述。

Microsoft 對於使用協力廠商複寫 API 型解決方案之部署的備份與還原支援原則，與原生連續複寫部署相同。

如果您是尋找協力廠商 API 資訊的合作夥伴，請連絡您的 Microsoft 代表。

回到頁首

## 高可用性和站台回復性文件

下表包含可協助您了解並管理 DAG、信箱資料庫副本和 Exchange 2013 備份與儲存的主題連結。


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
<td><p><a href="database-availability-groups-dags-exchange-2013-help.md">資料庫可用性群組 (DAGs)</a></p></td>
<td><p>了解 DAG、Active Manager、資料中心啟動協調 (DAC) 模式和信箱資料庫副本。</p></td>
</tr>
<tr class="even">
<td><p><a href="planning-for-high-availability-and-site-resilience-exchange-2013-help.md">規劃高可用性及站台恢復</a></p></td>
<td><p>了解 DAG 的一般、硬體、網路、軟體、見證伺服器和其他需求與最佳作法。</p></td>
</tr>
<tr class="odd">
<td><p><a href="deploying-high-availability-and-site-resilience-exchange-2013-help.md">部署高可用性和站台恢復</a></p></td>
<td><p>探索部署和設定 DAG 的範例部署案例。</p></td>
</tr>
<tr class="even">
<td><p><a href="managing-high-availability-and-site-resilience-exchange-2013-help.md">管理高可用性和站台恢復</a></p></td>
<td><p>了解 DAG 管理工作、轉換和容錯移轉和維護模式。</p></td>
</tr>
<tr class="odd">
<td><p><a href="monitoring-database-availability-groups-exchange-2013-help.md">監視資料庫可用性群組</a></p></td>
<td><p>了解內建用於監控 DAG 和資料庫副本的指令程式和指令碼。</p></td>
</tr>
<tr class="even">
<td><p><a href="backup-restore-and-disaster-recovery-exchange-2013-help.md">備份、還原和嚴重損壞修復</a></p></td>
<td><p>了解備份和還原 Exchange 資料庫、復原資料庫和伺服器復原。</p></td>
</tr>
</tbody>
</table>


回到頁首

