---
title: '受管理的可用性: Exchange 2013 Help'
TOCTitle: 受管理的可用性
ms:assetid: ceb99e6f-6dca-446d-abfb-3e6fc6a72704
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn482056(v=EXCHG.150)
ms:contentKeyID: 59889058
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 受管理的可用性

 

_**適用版本：**Exchange Online, Exchange Server 2013 SP1_

_**上次修改主題的時間：**2017-03-29_

確保使用者具有良好的電子郵件經驗一直是郵件系統管理員的主要目標。為了協助確保 Microsoft Exchange Server 2013 組織的可用性和可靠性，您必須主動監控系統的各個層面，並快速解決任何偵測到的問題。在舊版 Exchange 中，監控重要系統元件通常包括使用外部應用程式 (例如 Microsoft System Center 2012 Operations Manager) 來收集資料，以及針對因分析所收集資料而偵測到的問題提供復原動作。Exchange 2010 及舊版已在管理組件中包含了健康情況資訊清單及關聯性引擎。這些元件讓 Operations Manager 能做出有關特定元件健康情況是否良好的判斷。此外，Operations Manager 也使用內建於 Exchange 2010 的診斷 Cmdlet 基礎結構，對系統的各個層面執行綜合交易。

Exchange 2013 採取新的方法，原生地使用一項稱為*受管理的可用性*的功能監控及維護使用者經驗，這項功能提供了內建的監控和復原動作。

## 受管理的可用性

受管理的可用性也稱為*主動式監控*或*本機主動式監控*，此功能將內建的監控和復原動作整合至 Exchange 高可用性平台。設計目的為在問題發生且被系統發現後，盡速加以偵測並進行復原。與舊版 Exchange 的外部監控解決方案及技術不同的是，受管理的可用性不會嘗試識別或溝通問題的根本原因，而是著重於復原層面，處理三個使用者體驗的主要領域：

  - \[可用性\]**：**使用者可以存取服務嗎？

  - \[延遲\]**：**使用者感受如何？

  - \[錯誤\]**：**使用者能夠完成他們想要進行的事項嗎？

要在 Exchange 2013 中進行伺服器角色合併及其他架構變更，需要有新的方法來處理舊版 Exchange 中使用的監控方法和健康情況模型。受管理的可用性就是設計來因應這些改變，其方式是提供原生的健康情況監控及復原解決方案。它不再只是監控個別系統切片，而是監控端對端使用者經驗，並透過復原導向的動作來保護使用者經驗。

受管理的可用性是在每部 Exchange 2013 伺服器上執行的內部處理程序，它每秒會輪詢並分析數百個健康情況度量資訊。如果發現有錯誤，大多數情況下會自動加以修正。但永遠都會有問題是受管理的可用性無法自行修正的。在這些情況下，受管理的可用性會將問題透過事件記錄呈報給系統管理員。

受管理的可用性以下列兩種服務形式實作：

  - Exchange 健全狀況管理員服務 (MSExchangeHMHost.exe)**：**這是控制器處理程序，用於管理工作者處理程序。用途視需要分為建立、執行以及啟動與停止工作者處理程序。也可用於復原工作者處理程序，以於處理程序失敗時避免工作者處理程序成為單一失敗點。

  - **Exchange 健全狀況管理員工作者處理序 (MSExchangeHMWorker.exe)**  這是負責執行執行階段中的受管理的可用性架構工作者處理序。

受管理的可用性使用持續性儲存空間以執行其功能：

  - \\bin\\Monitoring\\config 資料夾中的 XML 檔案可用來儲存某些探查和監視器工作項目的組態設定。

  - Active Directory 可用來儲存全域覆寫。

  - Windows 登錄可用來儲存執行階段資料 (例如書籤) 以及本機 (伺服器特定) 覆寫。

  - Windows Crimson Channel 事件記錄檔基礎結構用於儲存工作項目結果。

  - 健康情況信箱可用於探查活動。位於伺服器上的每個信箱資料庫上，將會建立多個健康情況信箱。

如下圖所示，受管理的可用性包括三個主要的非同步元件，這些元件會持續不斷地運作。

**受管理的可用性元件**

![Exchange Server 2013 中受管理的可用性](images/Dn482056.7a54dcb5-1e28-4bd4-87e6-0d496b4ab796(EXCHG.150).gif "Exchange Server 2013 中受管理的可用性")

第一個元件會呼叫的*探查*。探查負責在伺服器上進行測量和收集資料。這些測量結果流入的第二個元件*的監視器*。監視包含所有的項目會視為正常上收集的資料為基礎的系統所使用的商務邏輯。類似圖樣辨識引擎，監視器會尋找所有收集的度量值，在各種不同模式並再決定是否某個項目會被視為狀況良好。最後，有*回應程式*，這是負責復原和呈報動作。當某個項目為狀況不良時的第一個巨集指令會嘗試復原該元件。這可能包含多階段復原動作 ；例如，第一次嘗試可能會重新啟動應用程式集區、 第二個可能會重新啟動服務、 第三個嘗試可能會重新啟動伺服器，及後續的嘗試可能會使伺服器離線，讓它不會再接受流量。如果復原動作成功，則系統會程式以透過事件記錄通知人力資源問題。

有三個主要的類別的探查： 週期性的探查、 通知和檢查。週期性探查是所要測試的端對端使用者經驗的系統執行綜合交易。檢查所執行的效能資料，包括使用者流量集合的基礎結構與對臨界值設定為決定暴增中使用者失敗的測量收集的資料。這可讓使用者發生問題時成為注意檢查基礎結構。最後，通知邏輯可讓系統立即根據緊急事件\]，而不需等待的探查所收集資料結果採取動作。這些通常是例外狀況或可偵測到並沒有一組大型範例可辨識的條件。

週期性探查執行每隔幾分鐘，並檢查服務健康狀況的一些層面。這些探查可能會傳送至監控信箱透過 Exchange ActiveSync 電子郵件、 它們可能會連線至 RPC 結束點或時可能會驗證用戶端存取-信箱的連線。

所有探查都定義 Microsoft.Exchange.ActiveMonitoring\\ProbeDefinition crimson 通道中的健全狀況管理員服務啟動。每個探查定義有許多屬性，但最相關的屬性：

  - **名稱** 探查、 開頭為探查監視器*SampleMask*名稱。

  - **TypeName** 包含探查邏輯探查的程式碼物件類型。

  - **ServiceName** 包含此探查健全設定的名稱。

  - **TargetResource** 會驗證物件探查。這會變成探查結果*ResultName*執行時附加至探查的名稱

  - **RecurrenceIntervalSeconds** 探查的執行頻率。

  - **TimeoutSeconds** 長探查等候失敗。

有數百個週期性的探查。有許多這些探查是每個資料庫，所以為數資料庫個數增加所以沒有探查的數目。大部分的探查程式碼中所定義與因此不是直接可供搜尋。

以下是週期性探查的基本知識： 啟動每個*RecurrenceIntervalSeconds*並檢查 （或探查） 某些方面的狀況。如果元件是狀況良好，探查會傳遞和資訊性事件寫入 3 *ResultType* Microsoft.Exchange.ActiveMonitoring\\ProbeResult 通道。如果核取失敗或逾時，探查失敗，並將 error 事件寫入至相同的通道。4 *ResultType*表示無法檢查和其逾時的 1 表示*ResultType* 。如果重新執行許多探查他們逾時，最多個*MaxRetryAttempts*屬性的值。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>附註</strong> Crimson 通道可以取得非常忙碌數百 ProbeResult 探查執行每隔幾分鐘，並記錄事件，因此可以有實際影響的 Exchange 伺服器的效能如果您嘗試對實際執行環境中的事件記錄檔的高成本查詢。</td>
</tr>
</tbody>
</table>


通知是未執行狀況管理員 framework，但一些其他服務的伺服器的探查。這些服務執行他們自己的監控，並再送入其資料的受管理的可用性架構直接編寫探查結果。當此通道僅說明將受管理的可用性 framework 執行的探查就無法看到這些探查 ProbeDefinition 通道中。例如，就會由 MSExchangeDAGMgmt 服務所撰寫的探查結果觸發 ServerOneCopyMonitor 監視器。此服務會執行它自己的監控、 會決定是否有問題及記錄檔的探查結果。大部分的通知探查有開啟監視器的狀況不良的紅色事件及進行監視狀況良好再次綠色事件記錄的功能。

檢查都只記錄事件時的效能計數器通過高於或低於已定義的臨界值的探查。他們是真正特殊案例的通知探查、 監視伺服器上的效能計數器及設定的臨界值時，記錄事件 ProbeResult 通道服務時。

若要尋找的效能計數器和會被視為不健康的臨界值，您可以查看此核取監視器。監視器類型*Microsoft.Office.Datacenter.ActiveMonitoring.OverallConsecutiveSampleValueAboveThresholdMonitor*或*Microsoft.Office.Datacenter.ActiveMonitoring.OverallConsecutiveSampleValueBelowThresholdMonitor*意義的探查他們觀賞為\] 核取探查

監視器會查詢透過探查所收集的資料，根據預先定義的規則集，判斷是否需採取動作。依規則或問題本質而定，監視器可以啟動回應程式，或透過事件記錄檔項目將問題呈報給人員。此外，監視器也定義失敗過後多久應執行回應程式，以及復原動作的工作流程。監視器具有多種狀態。從系統狀態的角度來看，監視器有兩種狀態：

  - **狀況良好** 監視器運作正常，所有收集的計量都在正常的作業參數範圍內

  - **狀況不良：**監視器的狀況不良，已透過回應程式啟動復原動作或是已透過呈報流程通知系統管理員。

從系統管理員的角度來看，監視器會在命令介面中顯示其他狀態：

  - 降級**：**監視器有 0 到 60 秒處於不良狀態時，便視為「降級」。如果監視器的不良狀態超過 60 秒，則視為「狀況不良」。

  - **已停用** 系統管理員已明確停用監視器。

  - **無法使用** Microsoft Exchange 健全狀況服務會定期查詢每個監視器的狀態。如果查詢無法取得回應，監視器狀態就會成為「無法使用」。

  - 正在修復**：**系統管理員設定「正在修復」狀態，向系統指出目前正由人員進行修正動作，如此可讓系統及人員區別在進行修正同時發生的其他失敗 (例如資料庫副本重新植入作業)。

每個監視器及其定義中具有*SampleMask*屬性。當監視器執行，則它會 ProbeResult 通道中有相符的監視器*SampleMaskResultName*的事件。這些事件可能是從週期性的探查、 通知或檢查。如果已達到的監視器臨界值，它會變成 Unhealthy。從監視器的觀點來看，所有三個探查類型都是相同為每個登 ProbeResult 通道。

它是值得注意的單一探查失敗不一定指出某個項目會與伺服器錯誤。它是監視器正確識別實際需要修正的問題時的設計。這就是為什麼許多監視器會臨界值的多個探查失敗之前變成 Unhealthy。即使然後這些問題的許多可以被修正自動回應程式，所以尋找需要手動介入的問題的最佳位置是在 Microsoft.Exchange.ManagedAvailability\\Monitoring crimson 通道。這將會包含最新的探查時發生錯誤。

顧名思義，回應程式會對監視器產生的警示執行某種回應。回應程式會採取各種復原動作，例如重設應用程式工作者集區以重新啟動伺服器。回應程式有多種類型：

  - **重新啟動回應程式** 終止並重新啟動服務

  - **重設 AppPool 回應程式** 在網際網路資訊服務 (IIS) 中停止並重新啟動應用程式集區

  - **容錯移轉回應程式** 起始資料庫或伺服器容錯移轉

  - **檢查錯誤回應程式** 起始伺服器的檢查錯誤作業，進而使伺服器重新開機

  - **離線回應程式** 讓伺服器上的通訊協定停止服務 (拒絕用戶端要求)

  - **線上回應程式** 讓伺服器上的通訊協定恢復實際執行 (接受用戶端要求)

  - **呈報回應程式** 透過事件記錄將問題呈報給系統管理員

除了上述所列的回應程式，某些元件也有獨有的專用回應程式。

所有回應程式都包含節流行為，可提供內建的排序機制來控制回應程式的動作。節流行為的設計目的是要確保系統不會因為回應程式的復原動作而洩漏資料或惡化。所有回應程式都以某種方式節流。節流發生時，可能會略過或延遲回應程式的復原動作 (視回應程式的動作而定)。例如，對檢查錯誤回應程式執行節流時，會略過其動作，但不會延遲。

## 健全設定

從報告的觀點來看，受管理的可用性有兩個健康情況檢視，一個內部，一個外部。內部檢視會使用*健全設定*。Exchange 2013 中的每個元件 (例如 Outlook Web App、Exchange ActiveSync、Information Store 服務、內容索引、傳輸服務等等) 是由受管理的可用性使用探查、監視器及回應程式來監控。所指定元件之探查、監視器及回應程式的群組即稱為*健全設定*。健全設定是探查、監視器及回應程式的群組，可判斷該元件健康情況是否良好。健全設定的目前狀態 (例如，健康情況是否良好) 是使用健全設定的監視器狀態來判斷。如果健全設定的監視器健康情況全都良好，則健全設定便是處於良好狀態。如果有任何監視器不在良好狀態，則健全設定的狀態會以健康情況最差的監視器來決定。

如需檢視伺服器健康情況或健全設定狀態的詳細步驟，請參閱[管理健全設定與伺服器健康情況](manage-health-sets-and-server-health-exchange-2013-help.md)。

## 健康情況群組

受管理可用性的外部檢視是由*健康情況群組*所組成。健康情況群組會公開給 System Center Operations Manager 2007 R2 和 System Center Operations Manager 2012。

有四個主要的健康情況群組：

  - **客戶接觸點** 影響即時使用者互動的元件，例如通訊協定或資訊儲存庫

  - **服務元件** 沒有直接、即時使用者互動的元件，例如 Microsoft Exchange Mailbox Replication 服務，或離線通訊錄產生程序 (OABGen)

  - **伺服器元件** 伺服器的實體資源，例如磁碟空間、記憶體和網路

  - **依存項目可用性** 伺服器存取必要依存項目 (例如 Active Directory、DNS 等等) 的能力。

Exchange 管理組件安裝時，System Center Operations Manager (SCOM) 會做為狀況入口網站以供檢視Exchange環境相關的資訊。SCOM 儀表板包含三個檢視的Exchange伺服器健康情況：

  - **作用中警示** 呈報回應程式會將事件寫入 Windows 事件記錄檔，由 SCOM 內的監視器使用。這些項目會顯示為 \[作用中警示\] 檢視中的警示。

  - **組織健康情況** 此檢視中會顯示 Exchange 組織健康情況的整體健康情況彙總摘要。這些彙總內容包括顯示個別資料庫可用性群組的健康情況，以及特定 Active Directory 網站內的健康情況。

  - **伺服器健康情況** 相關的健全設定會結合成健康情況群組，並摘錄在此檢視中。

## 覆寫

覆寫讓系統管理員能夠設定受管理可用性的探查、監視器及回應程式的某些方面。覆寫可用來微調某些受管理可用性所使用的臨界值。覆寫也可用來為可能需要與現成可用預設值不同之組態設定的未預期事件啟用緊急動作。

覆寫可以建立並套用到單一伺服器 (這稱為*伺服器覆寫*)，或是套用到一群伺服器 (這稱為*全域覆寫*)。伺服器覆寫組態資料會儲存在套用覆寫的伺服器 Windows 登錄中。全域覆寫組態資料則儲存在 Active Directory 中。

覆寫可以設定為無限期地執行下去，或是設定為在特定持續時間內執行。此外，全域覆寫可以設定為套用到所有伺服器，或是只套用到執行特定 Exchange 版本的伺服器。

當您設定覆寫時，它不會立即生效。Microsoft Exchange 健全狀況管理員服務每 10 分鐘會檢查一次是否有更新的組態資料。此外，全域覆寫會依存於 Active Directory 複寫延遲。

如需檢視或設定伺服器覆寫或全域覆寫的詳細步驟，請參閱[設定受管理的可用性覆寫](configure-managed-availability-overrides-exchange-2013-help.md)。

## 管理工作和 Cmdlet

關於受管理的可用性，系統管理員通常會執行三個主要的操作工作：

  - 擷取或檢視系統健康情況

  - 檢視健全設定以及關於探查、監視器及回應程式的詳細資料

  - 管理覆寫

受管理可用性的兩個主要管理工具分別是 Windows 事件記錄檔和命令介面。受管理可用性會在 Exchange ActiveMonitoring 和 ManagedAvailability Crimson 通道事件記錄檔中記錄大量資訊，例如：

  - 探查、監視器及回應程式的定義，這些資訊記錄在個別的 \*Definition 事件記錄檔中。

  - 探查、監視器及回應程式的結果，這些資訊記錄在個別的 \*Results 事件記錄檔中。

  - 關於回應程式復原動作的詳細資料，包括復原動作的啟動時間，以及視為完成 (不論成功與否)，這些資訊記錄在 RecoveryActionResults 事件記錄檔中。

有 12 個 Cmdlet 用於受管理的可用性，如下表所述。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>指令程式</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/zh-tw/library/jj218703(v=exchg.150)">Get-ServerHealth</a></p></td>
<td><p>用來取得原始的伺服器健康情況資訊，例如健全設定及其目前狀態 (健康情況是否良好)、健全設定監視器、伺服器元件、探查的目標資源、與探查或監視器之啟動或停止時間相關的時間戳記，以及狀態轉換時間。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/zh-tw/library/jj218724(v=exchg.150)">Get-HealthReport</a></p></td>
<td><p>用來取得包含健全設定及其目前狀態的摘要健康情況檢視。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/zh-tw/library/jj218668(v=exchg.150)">Get-MonitoringItemIdentity</a></p></td>
<td><p>用來檢視與特定健全設定相關聯的探查、監視器及回應程式。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/zh-tw/library/jj218642(v=exchg.150)">Get-MonitoringItemHelp</a></p></td>
<td><p>用來檢視關於某些探查、監視器及回應程式內容的描述。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/zh-tw/library/jj218628(v=exchg.150)">Add-ServerMonitoringOverride</a></p></td>
<td><p>用來建立探查、監視器或回應程式的本機、伺服器特定覆寫。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/zh-tw/library/jj218664(v=exchg.150)">Get-ServerMonitoringOverride</a></p></td>
<td><p>用來檢視指定伺服器上的本機覆寫清單。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/zh-tw/library/dn482411(v=exchg.150)">Remove-ServerMonitoringOverride</a></p></td>
<td><p>用來從特定伺服器移除本機覆寫。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/zh-tw/library/jj218683(v=exchg.150)">Add-GlobalMonitoringOverride</a></p></td>
<td><p>用來建立伺服器群組的全域覆寫。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/zh-tw/library/jj218627(v=exchg.150)">Get-GlobalMonitoringOverride</a></p></td>
<td><p>用來檢視在組織中設定的全域覆寫清單。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/zh-tw/library/jj218675(v=exchg.150)">Remove-GlobalMonitoringOverride</a></p></td>
<td><p>用來移除全域覆寫。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/zh-tw/library/jj218699(v=exchg.150)">Set-ServerComponentState</a></p></td>
<td><p>用來設定一或多個伺服器元件的狀態。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/zh-tw/library/jj218713(v=exchg.150)">Get-ServerComponentState</a></p></td>
<td><p>用來檢視一或多個伺服器元件的狀態。</p></td>
</tr>
</tbody>
</table>

