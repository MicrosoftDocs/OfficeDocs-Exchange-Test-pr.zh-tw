---
title: '備份、還原和嚴重損壞修復: Exchange 2013 Help'
TOCTitle: 備份、還原和嚴重損壞修復
ms:assetid: 394fc4ed-fa02-41fa-9159-cc2754ff8875
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd876874(v=EXCHG.150)
ms:contentKeyID: 50472882
ms.date: 01/01/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 備份、還原和嚴重損壞修復

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

在您的資料保護規劃中，您必須了解可保護資料的方法，並判定哪個方法最適合您的組織需求。資料保護規劃是複雜的處理程序，需要您在部署的規劃階段進行許多決策。

傳統上，下列情況會使用備份：

  - **嚴重損壞修復**   當硬體或軟體故障時，DAG 中有多個資料庫副本能夠提供高可用性，可快速容錯轉移，而且只遺失少量資料，甚至完全不會遺失任何資料。如此就不會因為運作停擺而導致失去產能，這是從過去時間點備份復原到磁碟或磁帶時付出的重大代價。DAG 可以延伸到數個站台，能夠從磁碟、伺服器、網路和資料中心故障情況中恢復。

  - **復原意外刪除的項目**   一直以來，當使用者刪除了項目，之後又必須復原時，常常需要尋找儲存需還原資料的備份媒體，然後再設法取得所需的項目並提供給使用者。有了 Exchange 2013 嶄新的 \[可復原的項目\] 資料夾，以及套用資料夾上的「保留原則」，便可以將所有遭刪除與修改的資料保留一段指定的時間，讓復原這些項目變得更簡單、更快速。這可讓一般使用者自行復原不小心刪除的項目，而減少 Exchange 系統管理員與 IT 服務台人員的負擔，也因此減少復原單一項目的複雜度與管理成本。如需詳細資訊，請參閱[郵件原則及符合性](messaging-policy-and-compliance-exchange-2013-help.md)及[資料遺失防護](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)。

  - **長期資料儲存**   備份也做為封存用途，且依照法規需求，通常會使用磁帶長期保存資料的時間點快照。Exchange 2013 中新的封存、多信箱搜尋與訊息保留功能，提供了一種機制可有效率地以一般使用者可存取的方式來長期保存資料。這樣可避免從磁帶還原時付出的重大代價，因而提升產能。如需相關資訊，請參閱[就地封存 in Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md)、[就地 eDiscovery](in-place-ediscovery-exchange-2013-help.md)與[就地保留與訴訟暫止](in-place-hold-and-litigation-hold-exchange-2013-help.md)。

  - **時間點資料庫快照**   如果您的組織需要有信箱資料的過去時間點副本，則 Exchange 能夠在 DAG 環境中建立遲延資料庫副本。在非常少見的情況下，儲存邏輯損毀會複寫到 DAG 中的多個資料庫副本，導致需要回到過去的時間點，此時這項功能就很有用。如果系統管理員不小心刪除信箱或使用者資料，這也會很有幫助。從遲延副本復原會比從備份復原更加快速，因為遲延副本不需要從備份伺服器複製到 Exchange 伺服器上，這是相當耗時的程序。這可以藉由縮短停機時間來大幅降低擁有權總成本。

因為有原生的 Exchange 2013 功能可解決以上各種情況，不但有效率又符合成本效益，可讓您的環境中減少或不必使用傳統備份。

Exchange 原生資料保護

支援的備份技術

Exchange 2013 VSS 編寫器

Exchange Server 復原

整合連絡人儲存復原

復原資料庫

資料庫可攜性

撥號音可攜性

## Exchange 原生資料保護

Microsoft 的 Exchange Server 2013[建議架構](https://blogs.technet.com/b/exchange/archive/2014/04/21/the-preferred-architecture.aspx)採用所謂的 Exchange 原生資料保護概念。Exchange 原生資料保護依賴內建的 Exchange 功能來保護信箱資料，而不使用備份 (您仍然可以使用這些功能和建立備份)。Exchange 2013 中有許多新的功能和核心變更，只要正確地部署和設定，就能提供原生資料保護，而不需要對資料建立傳統備份。使用 Exchange 2013 內建的高可用性功能，在發生嚴重損壞的情况下，可使停機和資料遺失減到最小，還可以減少郵件系統的擁有權總成本。透過結合這些功能與其他內建功能 (例如合法持有)，您可以減少或不必使用傳統時間點備份，並減少相關的成本。

除了判斷 Exchange 2013 是否能使您脫離傳統的時間點備份以外，我們也建議您評估目前備份基礎結構的成本。當嘗試使用現有備份基礎結構從嚴重損壞還原時，請考量使用者停機和資料遺失的成本。此外，也要包含硬體、安裝及授權成本，還有復原資料和維護備份的相關管理成本。視您組織的需求而定，一個至少具備三個信箱資料庫副本的單純 Exchange 2013 環境，很可能會比具有備份的相同環境能提供較低的擁有權總成本。

使用建置到 Exchange 2013 中的功能取代傳統備份之前，有幾個問題需要考量。您的組織可能也有自身獨有的考量。請考慮下列問題，並請注意這並非詳盡清單：

  - 您應確認需要部署的資料庫副本數目。在取代傳統的資料庫保護形式 (例如獨立磁碟容錯陣列 (RAID) 或傳統 VSS 備份) 之前，強烈建議您至少部署三個信箱資料庫 (非延遲) 副本。

  - 您應清楚定義復原時間目標與復原點目標，且您應證明將一組內建的功能結合使用來取代傳統的備份，能讓您達成這些目標。

  - 您應決定每個資料庫需要多少副本，以涵蓋各種預定防護系統以避免發生的故障狀況。

  - 您應判斷如果不考慮使用 DAG 或其某些成員，是否能夠獲得充足的費用支援傳統的備份解決方案。如果是的話，您應判斷該解決方案是否能改善您的復原時間目標或複原點目標服務等級協議 (SLA)。

  - 您應判斷如果代管副本的 DAG 成員遇到故障，影響到副本或副本的完整性，您是否可負擔失去時間點副本造成的損失？

  - Exchange 2013 可讓您部署更大的信箱，建議信箱資料庫大小為 2TB（當有兩個或更高可用信箱資料庫複本正在使用時）。若採用大多數組織可能部署的大型信箱，您應判斷當啟用資料庫副本或延遲的資料庫副本時，如果您必須重現大量的記錄檔，您的復原點目標為何。

  - 您應決定如何偵測主動資料庫副本的邏輯損毀，並防止該損毀複寫到資料庫的被動副本。這包括卻摁發生此情況時的復原計劃，以及過去發生此情況的頻率。如果您的組織常常發生邏輯損毀，則建議您使用一或多個遲延副本將該狀況的因素包含到您的設計中，並有足夠的重現延遲時間，讓您能夠在發生邏輯損毀時，且在損毀複寫到其他資料庫副本之前，便偵測到該邏輯損毀並採取動作。

成功完整或增量備份結束時要執行的功能之一，就是將資料庫復原時不再需要的交易記錄檔截斷。如果未執行備份，就不會截斷記錄檔。為避免記錄檔增長，您可以為複寫的資料庫啟用循環記錄。當您將循環記錄結合連續複寫時，便有了一種新的循環記錄，稱做連續複寫循環記錄 (CRCL)，這與 可延伸儲存引擎 (ESE) 循環記錄不同。不同於 ESE 循環記錄是由 Microsoft Exchange Information Store 服務來執行和管理，CRCL 則是由 Microsoft Exchange 複寫服務來執行和管理。啟用 ESE 循環記錄時，不會產生其他記錄檔，而是會在需要時，覆寫目前的記錄檔。然而，在連續複寫環境中，需要有記錄檔來傳送及重新顯示記錄。因此，當您啟用 CRCL 時，不會覆寫目前的記錄檔，並且會針對記錄傳送及重新顯示處理程序來產生關閉的記錄檔。

具體而言，Microsoft Exchange 複寫服務會管理 CRCL，以維護記錄的連續性，而且如果仍需要這些記錄來進行複寫，也不會將其刪除。Microsoft Exchange 複寫服務和 Microsoft Exchange Information Store 服務會使用遠端程序呼叫 (PRC) 通訊，以判斷可以刪除哪些記錄檔。

若要讓高可用性 (非延遲) 信箱資料庫副本執行截斷，下列條件必須成立：

  - 記錄檔已備份或已啟用 CRCL。

  - 記錄檔是在檢查點下方。

  - 資料庫的其他非延遲副本同意刪除。

  - 記錄檔已由所有延遲的資料庫副本進行檢查。

若要讓延遲信箱資料庫副本執行截斷，下列條件必須成立：

  - 記錄檔是在檢查點下方。

  - 記錄檔比 ReplayLagTime + TruncationLagTime 更舊。

  - 記錄檔已在資料庫的主動副本上刪除。

Exchange 原生資料保護

## 支援的備份技術

Exchange 2013 僅支援 Exchange 感知 VSS 型備份。Exchange 2013 包含 Windows Server Backup 的外掛程式可讓您製作和還原 Exchange 資料的 VSS 型備份。若要備份和還原 Exchange 2013，您必須使用支援 Exchange 2013 VSS 編寫器的 Exchange 感知式應用程式，例如 Windows Server Backup (含 VSS 外掛程式)、Microsoft System Center 2012 - Data Protection Manager，或協力廠商 Exchange 感知式 VSS 應用程式。

如需如何使用 Windows Server Backup 備份和還原 Exchange 資料的詳細步驟，請參閱[使用 Windows Server Backup 備份及還原 Exchange 資料](using-windows-server-backup-to-back-up-and-restore-exchange-data-exchange-2013-help.md)。

Exchange 原生資料保護

## Exchange 2013 VSS 編寫器

Exchange 2013 從 Exchange 2010 與 Exchange 2007中使用的 VSS 編寫器架構引進了重大改變。這些舊版的Exchange包括兩個 VSS 編寫器：一個位於 Microsoft Exchange Information Store 服務 (store.exe) 內，而另一個位於 Microsoft Exchange Replication 服務內 (msexchangerepl.exe)。在 Exchange，先前曾於 Microsoft Exchange Information Store 服務找到的 VSS 編寫器已移至 Microsoft Exchange Replication 服務。新編寫器 Microsoft Exchange Writer 現已由 Exchange 感知 VSS 應用程式使用，以備份主動及被動資料庫副本，並還原備份資料庫副本。雖然新編寫器在 Microsoft Exchange Replication 服務中執行，但仍需要執行 Microsoft Exchange Information Store 服務，編寫器才能被公告。因此，需要兩個服務才能備份或還原 Exchange 資料庫。

Exchange 原生資料保護

## Exchange Server 復原

幾乎所有信箱及用戶端伺服器的組態設定皆儲存在 Active Directory。如同舊版的 Exchange，Exchange 2013 也包含可復原損毀伺服器的 Setup 參數。*/m:RecoverServer* 參數用於使用儲存在 Active Directory 中的設定與組態資訊，來重新建置與建立損毀的伺服器。不過，請注意有幾項設定不會還原，例如對 web.config 和其他組態檔所做的變更。此外，也不會還原自訂登錄項目。建議您使用可靠的變更管理程序來追蹤和重新建立這些變更。

如需如何執行損毀 Exchange 2013 伺服器的伺服器復原詳細步驟，請參閱[復原 Exchange Server](recover-an-exchange-server-exchange-2013-help.md)。如需如何復原屬於資料庫可用性群組成員 (DAG) 之損毀伺服器的詳細步驟，請參閱[復原資料庫可用性群組成員伺服器](recover-a-database-availability-group-member-server-exchange-2013-help.md)。

Exchange 原生資料保護

## 整合連絡人儲存復原

在 Exchange 2013 環境中使用 Microsoft Lync Server 2013 時，使用者的 Lync 連絡人資訊將儲存在使用者信箱的特殊連絡人資料夾中。這稱為整合連絡人儲存 (UCS)。若還原 UCS 遷移的信箱，目標使用者的立即訊息連絡清單可能會受影響。若使用者在上次備份後遷移，還原信箱將讓使用者的連絡清單完全遺失。少數嚴重的情況下，上次備份由使用者修改的連絡清單將會遺失。若要減這個輕潛在的資料遺失風險，請確認使用者在還原信箱前已遷移回立即訊息伺服器。

Exchange 原生資料保護

## 復原資料庫

復原資料庫是特殊種類的信箱資料庫，可讓您裝載還原的信箱資料庫，並在復原作業中從還原的資料庫擷取資料。您可以使用 [New-MailboxRestoreRequest](https://technet.microsoft.com/zh-tw/library/ff829875\(v=exchg.150\)) 指令程式從復原資料庫擷取資料。擷取完畢後，便可以匯出資料，或將資料合併至現有信箱中。復原資料庫可讓您從資料庫的備份或副本中復原資料，而不會干擾使用者存取目前的資料。

不支援使用任何舊版本的 Exchange 信箱資料庫作為復原資料庫。此外，用於資料合併與擷取作業的目標信箱必須與復原資料庫中裝載的資料庫位於同一個 Active Directory 樹系。

如需相關資訊，請參閱[復原資料庫](recovery-databases-exchange-2013-help.md)。如需如何建立復原資料庫的詳細步驟，請參閱[建立復原資料庫](create-a-recovery-database-exchange-2013-help.md)。如需如何使用復原資料庫的詳細步驟，請參閱[使用復原資料庫還原資料](restore-data-using-a-recovery-database-exchange-2013-help.md)。

Exchange 原生資料保護

## 資料庫可攜性

資料庫可攜性是一種可將 Exchange 2013 信箱資料庫移至並裝載在相同組織中任何其他 Exchange 2013 信箱伺服器上的功能。使用資料庫可攜性可從復原處理程序移除幾個容易造成錯誤的手動步驟，從而改善可靠性。此外，資料庫可攜性可減少各種失敗案例的整體復原時間。

如需詳細資訊，請參閱＜[資料庫可攜性](database-portability-exchange-2013-help.md)＞。如需使用資料庫可攜性的詳細步驟，請參閱[使用資料庫可攜性移動信箱資料庫](move-a-mailbox-database-using-database-portability-exchange-2013-help.md)。

Exchange 原生資料保護

## 撥號音可攜性

撥號音可攜性是一種功能，可為影響信箱資料庫、伺服器或整個站台的失敗情況，提供有限的永續營運解決方案。在還原或修復使用者的原始信箱期間，撥號音可攜性讓使用者有一個暫時信箱可用來傳送及接收電子郵件。暫時信箱可以位於同一部 Exchange 2013 信箱伺服器上，或位於組織中的任何其他 Exchange 2013 信箱伺服器上。這允許替代伺服器儲存先前位於無法再使用的伺服器上之使用者的信箱。支援自動探索的用戶端 (例如 Microsoft Outlook) 會自動重新導向新的伺服器，而不需手動更新使用者的桌面設定檔。在還原使用者的原始信箱資料之後，系統管理員可以將使用者已復原的信箱和使用者的撥號音信箱合併成最新的單一信箱。

使用撥號音可攜性的程序稱為「撥號音復原」。撥號音復原包括在信箱伺服器上建立空的資料庫，以取代失敗的資料庫。這個空的資料庫 (稱為「撥號音資料庫」) 可讓使用者在失敗的資料庫復原之前，傳送及接收電子郵件。在復原故障的資料庫後，撥號音資料庫與已復原的資料庫會交換，然後撥號音資料庫中的資料會合併到已復原的資料庫中。

如需詳細資訊，請參閱＜[撥號音可攜性](dial-tone-portability-exchange-2013-help.md)＞。如需執行撥號音復原的詳細步驟，請參閱＜[執行撥號音復原](perform-a-dial-tone-recovery-exchange-2013-help.md)＞。

Exchange 原生資料保護

