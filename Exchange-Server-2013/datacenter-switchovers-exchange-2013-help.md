---
title: '資料中心轉換: Exchange 2013 Help'
TOCTitle: 資料中心轉換
ms:assetid: ac208c12-04d0-4809-bacd-72478ff14983
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd351049(v=EXCHG.150)
ms:contentKeyID: 62523863
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 資料中心轉換

 

_**適用版本：**Exchange Server 2013 SP1_

_**上次修改主題的時間：**2016-03-17_

在站台恢復組態中，站台層級失敗之後的自動復原可能在 DAG 內進行，可讓郵件系統維持在正常運作狀態。此組態至少需要三個位置，因為需要將 DAG 成員部署在兩個位置，而 DAG 的見證伺服器在第三個位置。

如果您沒有三個位置，或者，即使有三個位置，但想要控制資料中心層級復原動作，您可以設定 DAG 以便在站台層級失敗時手動復原。在此情況下，您需要執行所謂的*「資料中心轉換」*程序。和許多災難復原案例一樣，資料中心轉換的優先規劃和準備可以簡化復原程序，並縮短中斷的持續時間。

最初決定啟動次要資料中心之後，要完成四個基本步驟才能執行資料中心轉換：

1.  **終止部份執行的資料中心**   此步驟包括終止主要資料中心的 Exchange 服務 (如果有任何服務仍在執行)。這對於 Mailbox server role 來說特別重要，因爲它會使用主動/被動高可用性模型。如果不停止部份失敗的資料中心中的服務，則轉換回主要資料中心時，部份失敗的資料中心的問題可能會對這些服務產生不良影響。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果網路或 Active Directory 基礎結構的可靠性已因主要資料中心失敗而遭到破壞，則建議關閉所有通訊服務，直到這些相依性都還原為狀況良好的服務為止。</td>
    </tr>
    </tbody>
    </table>


2.  **驗證並確認次要資料中心的必要條件**   此步驟可與步驟 1 同時執行，因爲驗證次要資料中心的基礎結構相依性健康狀況，與第一個資料中心服務並無直接關係。每個組織通常都需要以自己的方法執行這個步驟。例如，您可以決定透過檢視監控應用程式之基礎結構所收集和篩選的健康狀況資訊來完成此步驟，或是使用組織基礎結構的獨有工具來完成此步驟。這是重要步驟，因為在次要資料中心的基礎結構狀況不良且不穩定時加以啟用，可能會產生不良結果。

3.  **啟動 Mailbox Server**   此步驟會開始啟動次要資料中心的處理程序。此步驟可與步驟 4 同時執行，因爲 Microsoft Exchange 服務可以處理資料庫中斷以及進行復原。啟動 Mailbox Server 包括在啟動次要資料中心的伺服器之後，將主要資料中心的失敗伺服器標記為無法使用。信箱伺服器的啟動程序，取決於 DAG 是否處於資料庫啟動協調 (DAC) 模式。如需資料庫啟動協調模式的相關資訊，請參閱[資料中心啟動協調模式](datacenter-activation-coordination-mode-exchange-2013-help.md)。
    
    如果 DAG 是處於 DAC 模式，便可以使用 Exchange 站台回復性指令程式，來終止部分失敗的資料中心 (如有必要)，並啟動信箱伺服器。例如，在 DAC 模式中，您可以使用 [Stop-DatabaseAvailabilityGroup](https://technet.microsoft.com/zh-tw/library/dd335133\(v=exchg.150\)) 指令程式來執行此步驟。在某些情況下，伺服器必須兩次 (每一個資料中心中一次) 標記爲無法使用。接著，執行 [Restore-DatabaseAvailabilityGroup](https://technet.microsoft.com/zh-tw/library/dd351169\(v=exchg.150\)) 指令程式，來還原次要資料中心的資料庫可用性群組 (DAG) 的剩餘成員，方法是將 DAG 成員減少到仍可操作的成員，進而重新建立仲裁。如果 DAG 不是處於 DAC 模式，則必須使用 Windows 容錯移轉叢集工具來啟動信箱伺服器。在每一項處理程序都完成之後，先前在次要資料中心是被動模式的資料庫副本，就可以變成主動並進行裝載。此時，信箱伺服器復原已完成。

4.  **啟動 Client Access Server**   這包括使用 URL 對應資訊及網域名稱系統 (DNS) 變更方法來執行所有必要的 DNS 更新。對應資訊會描述要執行的 DNS 變更。完成更新所需的時間量取決於所使用的方法及 DNS 記錄上的存留時間 (TTL) 設定 (以及部署基礎結構是否遵循 TTL)。

在完成步驟 3 和 4 之後，使用者就應該能夠存取通訊服務。本主題稍後將詳述步驟 3 和 4。

**目錄**

Terminating a Partially Failed Datacenter

Activating Mailbox Servers

Activating Other Server Roles

Restoring Service to the Primary Datacenter

Reestablishing Site Resilience

## 終止部份失敗的資料中心

如果失敗的資料中心有任何 DAG 成員仍在執行，則應該終止。

當 DAG 處於 DAC 模式時，下列為要終止主要資料中心內所有存在之 DAG 成員的特定行動：

1.  在主要資料中心中，主要資料中心的 DAG 成員必須標記為停止。*「已停止」*是阻止裝載資料庫的 Active Manager 的狀態，而使用 [Stop-DatabaseAvailabilityGroup](https://technet.microsoft.com/zh-tw/library/dd335133\(v=exchg.150\)) 指令程式可以將失敗資料中心的每台伺服器上的 Active Manager 設定為此狀態。此指令程式的 *ActiveDirectorySite* 參數可以透過單一命令，將主要資料中心的所有伺服器標記為已停止。視失敗狀況而定，此步驟可能無法進行。如果資料中心的狀態允許，則應該執行此步驟。應該對主要資料中心的所有伺服器執行 **Stop-DatabaseAvailabilityGroup** 指令程式。如果 Mailbox Server 無法使用，但 Active Directory 正在主要資料中心中作業，則必須針對主要資料中心中處於此狀態的所有伺服器，執行含 *ConfigurationOnly* 參數的 **Stop-DatabaseAvailabilityGroup** 命令，或是關閉 Mailbox Server。如果無法關閉失敗資料中心的 Mailbox Server，或是無法順利對伺服器執行 **Stop-DatabaseAvailabilityGroup** 命令，則兩個資料中心之間就有可能發生核心分裂的狀況。您可能需要透過電源管理裝置個別關閉電腦，以滿足此需求。

2.  現在必須更新次要資料中心，才能顯示哪個主要資料中心伺服器已停止。使用相同 *ActiveDirectorySite* 參數並指定失敗主要資料中心的 Active Directory 站台名稱，來執行含 *ConfigurationOnly* 參數的相同 **Stop-DatabaseAvailabilityGroup** 命令，即可完成此動作。此步驟的目的是在還原服務時，通知次要資料中心的伺服器可以使用哪些信箱伺服器。

當 DAG 不處於 DAC 模式時，下列為要終止主要資料中心內所有存活之 DAG 成員器特定行動：

1.  您必須針對主要資料中心裡的每一台 DAG 成員執行下列命令，強制將它們從 DAG 的基礎叢集收回：
    
        net stop clussvc
        cluster <DAGName> node <DAGMemberName> /forcecleanup

2.  次要資料中心的 DAG 成員現在必須重新啟動，然後再用來完成來自次要資料中心的收回處理程序。在每一台成員上執行下列命令，以便停止次要資料中心每一台 DAG 成員上的叢集服務：
    
        net stop clussvc

3.  在次要資料中心裡的某台 DAG 成員上，執行下列命令以強制進行叢集服務的仲裁啟動：
    
        net start clussvc /forcequorum

4.  開啟容錯移轉叢集管理工具，並連線至 DAG 的基礎叢集。展開叢集，然後展開 \[節點\]。在主要資料中心的每個節點上按一下滑鼠右鍵，並依序選取 \[其他動作\] 及 \[收回\]。收回主要資料中心的 DAG 成員之後，請關閉容錯移轉叢集管理工具。

回到頁首

## 啟動 Mailbox Server

在資料中心轉換期間啟動信箱伺服器所需的步驟，同樣取決於 DAG 是否處於 DAC 模式。在啟動次要資料中心的 DAG 成員之前，建議您驗證次要資料中心的基礎結構服務是否就緒並可供啟動通訊服務。

當 DAG 處於 DAC 模式時，在次要資料中心完成啟動信箱伺服器的步驟，如下所示：

1.  次要資料中心的每個 DAG 成員的叢集服務都必須停止。您可以使用 **Stop-Service** 指令程式來停止服務 (例如，`Stop-Service ClusSvc`)，或從提升權限的命令提示字元使用 `net stop clussvc`。

2.  使用 [Restore-DatabaseAvailabilityGroup](https://technet.microsoft.com/zh-tw/library/dd351169\(v=exchg.150\)) 指令程式，待命資料中心的信箱伺服器就會啟動。待命資料中心的 Active Directory 站台會傳遞到 **Restore-DatabaseAvailabilityGroup** 指令程式，以識別要使用哪些伺服器來還原服務，以及設定 DAG 來使用替代的見證伺服器。如果先前替代見證伺服器，您可以使用 [Restore-DatabaseAvailabilityGroup](https://technet.microsoft.com/zh-tw/library/dd351169\(v=exchg.150\)) 指令程式的 *AlternateWitnessServer* 和 *AlternateWitnessDirectory* 參數來進行設定。如果此命令成功，則仲裁條件會縮小為待命資料中心的伺服器。如果該資料中心的伺服器數目是偶數，則 DAG 將轉成使用由 DAG 物件的設定所識別的替代見證伺服器。

3.  現在可以啟動資料庫。根據組織使用的特定組態，此動作可能不會自動進行。如果待命資料中心的伺服器設定會阻止啟動，系統就不會從主要資料中心自動容錯移轉到任何資料庫的待命資料中心。如果待命資料中心的所有資料庫副本都沒有容錯移轉限制，系統就會假設次要資料中心的副本狀況良好並加以啟動。如果以阻止啟動的設定 (需要明確手動的動作) 來設定資料庫，則有兩種動作可選：
    
    1.  清除會阻止啟動的設定。這樣會使系統回到其預設行為，也就是啟動任一個可用的副本。
    
    2.  保持設定不變，並使用 [Move-ActiveMailboxDatabase](https://technet.microsoft.com/zh-tw/library/dd298068\(v=exchg.150\)) 指令程式來完成次要資料中心的資料庫啟動。若要在設定為阻止啟動時使用 **Move-ActiveMailboxDatabase** 指令程式完成此步驟，則必須明確識別此動作的目標。

4.  最後一個步驟是檢閱來自工作的所有錯誤及警告訊息。所有已指明的警告都應該加以處理和修正。這些命令的工作設計模型如果無法達到其設計的基礎目標，就算是失敗。例如，如果 **Restore-DatabaseAvailabilityGroup** 指令程式無法縮小 DAG 仲裁，並在不造成仲裁中斷的情況下，讓次要資料中心的伺服器重新啟動以提供服務，則該指令程式就會失敗。但是，也會使用每個工作的輸出，來識別需要管理員進行後續處理的問題。強烈建議您儲存所有工作輸出，並檢閱是否需要後續處理動作。

當 DAG 不處於 DAC 模式時，在次要資料中心完成啟動信箱伺服器的步驟，如下所示：

1.  仲裁必須依據次要資料中心的 DAG 成員數量來進行修改。
    
    1.  如果 DAG 成員數量為奇數，請執行下列命令將 DAG 仲裁模型從節點及檔案共用多數仲裁，變更為多數節點仲裁：
        
            cluster <DAGName> /quorum /nodemajority
    
    2.  如果 DAG 成員數量為偶數，則在 Exchange 管理命令介面中執行下列命令，重新設定見證伺服器與目錄：
        
            Set-DatabaseAvailabilityGroup <DAGName> -WitnessServer <ServerName>

2.  執行下列命令，在次要資料中心任何剩下的 DAG 成員上啟動叢集服務：
    
        net start clussvc

3.  針對每一台 DAG 成員執行下列命令，執行伺服器轉換作業以啟動 DAG 中的信箱資料庫：
    
        Move-ActiveMailboxDatabase -Server <DAGMemberinPrimarySite> -ActivateOnServer <DAGMemberinSecondSite>

4.  執行下列命令，將每一台 DAG 成員上的信箱資料庫裝載到次要站台：
    
        Get-MailboxDatabase <DAGMemberinSecondSite> | Mount-Database

回到頁首

## 啟動 Client Access Server

用戶端會連接到服務端點 (例如，Outlook Web App、自動探索、Exchange ActiveSync、Outlook Anywhere、POP3、IMAP4 和 RPC Client Access 陣列) 來存取 Exchange 服務和資料。因此，啟動 Client Access Server 涉及變更這些服務端點的 DNS 記錄對應 (從主要資料中心的 IP 位址變更為次要資料中心的 IP 位址)，而次要資料中心的 IP 位址會設定為新的服務端點。視 DNS 組態而定，需要修改的 DNS 記錄不一定會在相同的 DNS 區域中。

## 啟動 Client Access Server

接著，用戶端將會以下列其中一個方式自動連接到新服務端點：

  - 用戶端將繼續嘗試連接，而且應該會在原始 DSN 項目的 TTL 過期之後自動連接，以及在用戶端 DNS 快取的項目過期之後自動連接。使用者還可以從命令提示字元執行 `ipconfig /flushdns` 命令，手動清除其 DNS 快取。

  - 用戶端啟動或重新啟動時，會執行 DNS 查閱並取得服務端點的新 IP 位址；而此端點將是次要資料中心的 Client Access Server 或陣列。

假設用來定義和設定次要資料中心之服務 (使其運作方式與在主要資料中心的運作方式相同) 的所有適當組態變更均已完成，並假設已建立的 DNS 組態正確，則啟動 Client Access Server 時，應該不需要進行任何進一步的變更。

## 啟動傳輸服務

提交郵件的用戶端和其他伺服器通常都會使用 DNS 來識別這些伺服器。在次要資料中心啟動傳輸服務包括變更 DNS記錄，以指向次要資料中心裡的信箱伺服器 IP 位址。接著，用戶端和傳送伺服器就會以下列其中一個方式，自動連接到次要資料中心裡的伺服器：

  - 用戶端將繼續嘗試連接，而且應該會在原始 DSN 項目的 TTL 過期之後自動連接，以及在用戶端 DNS 快取的項目過期之後自動連接。使用者還可以從命令提示字元執行 `ipconfig /flushdns` 命令，手動清除其 DNS 快取。

  - 用戶端啟動或重新啟動時會執行 DNS 查閱，並取得 SMTP 端點的新 IP 位址，也就是次要資料中心裡的信箱伺服器。

假設已完成所有適當的組態變更，將次要資料中心裡的服務定義並設定為如同在主要資料中心裡運作一樣，並假設已建立的 DNS 組態正確，則不需要進一步的變更即可啟動傳輸服務。

## 啟動整合通訊服務

整合通訊 (UM) 服務會連接到組織的 PBX 系統和電話線路。PBX 系統與整合通訊服務之間的邏輯連線是由 IP 閘道提供。IP 閘道包含高可用性功能，且能在偵測到失敗時，於多個整合通訊服務之間切換。

如果次要資料中心裡有因爲專用於站台恢復解決方案而處於停用狀態的整合通訊服務，您可以使用 [Enable-UMService](https://technet.microsoft.com/zh-tw/library/jj552411\(v=exchg.150\)) 指令程式 (例如，`Enable-UMService EX4`) 加以啟用。

假設 IP 閘道透過 DNS 伺服器而與整合通訊服務產生關聯，則啟動整合通訊服務就包括變更 DNS 記錄，以指向將針對次要資料中心裡的整合通訊服務而設定的新 IP 位址。假設已完成所有適當的組態變更，將次要資料中心裡的服務定義並設定為如同在主要資料中心裡運作一樣，並假設已建立的 DNS 組態正確，則不需要進一步的變更即可啟動整合通訊服務。

如果使用中的 IP 閘道不支援使用 DNS 名稱來解析整合通訊服務，則必須進行其他設定步驟，以手動將 IP 閘道指向次要資料中心裡的整合通訊服務 IP 位址。

## 啟動 Edge Transport Server

啟動 Edge Transport server role 的步驟視特定組態而有所不同。兩個資料中心的 Edge Transport Server 都可以設定為主動/被動或主動/主動組態。在主動/被動組態中，除非啟動次要資料中心，否則次要資料中心的 Edge Transport Server 會維持閒置。在主動/主動組態中，兩個資料中心的 Edge Transport Server 會一直傳送郵件。

在主動/主動組態中，不需要任何步驟即可啟動次要資料中心的 Edge Transport Server，因爲它們已在執行。在主動/被動組態中，每個 SMTP 網域的 DNS MX 資源記錄都必須在轉換過程中，從主要資料中心更新到待命資料中心。雖然主動/主動組態提供了簡單的資料中心轉換解決方案，但缺點是必須小心監控負載，以確認資料中心轉換之後，次要資料中心的 Edge Transport Server 有足夠容量可支援現在通過它的新增負載 (因為主要資料中心的 Edge Transport Server 無法使用)。

即使在主動/主動組態中，也可以在資料中心轉換期間，更新 Edge Transport Server 的 MX 資源記錄。允許失敗資料中心的 MX 資源記錄繼續指向失敗的資料中心，表示資料中心開始復原時，就能夠開始嘗試連線到它的 Edge Transport Server。當 Edge Transport 服務處於不穩定狀態時 (例如因爲正在還原資料中心的依存服務)，就可能發生此狀況。hzwxtu

假設 DNS 記錄受到組織控制，則啟動 Edge Transport Server 就包括更新由伺服器主控之每個 SMTP 網域的 MX 資源記錄。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果組織使用的 MX 資源記錄不是在組織的控制下由 DNS 伺服器主控，則您可以考慮參照 MX 資源記錄中的 CNAME 記錄，並在組織的控制下使用可以更新的 CNAME 記錄。</td>
</tr>
</tbody>
</table>


DNS 更新會啟用內送流量，而啟動站台 (含有操作中的 Edge Transport Server) 的信箱資料庫時，則會處理外寄流量：

  - 如果傳入 SMTP 連線是使用更新過的名稱解析資訊來起始，則 SMTP 用戶端會連接到次要資料中心的 Edge Transport Server。流量將由 Edge Transport Server 適當地路由，不需要進一步變更。

  - 起始外寄 SMTP 連線時，會嘗試本機可用的 Edge Transport Server，而郵件將根據接收伺服器的狀態進入佇列或立即傳送。

回到頁首

## 將服務還原至主要資料中心

一般而言，資料中心失敗不是暫時性就是永久性。如果是永久性失敗 (例如，事件已經造成主要資料中心的永久損壞)，則不必期望啟動主要資料中心。不過，如果是暫時性失敗 (例如，長時間斷電或廣泛但可修復的損害)，則可以期待主要資料中心最後能夠還原至完整服務。

將服務還原至先前失敗之資料中心的處理程序稱爲*「容錯回復」*。執行資料中心容錯回復的步驟與執行資料中心轉換的步驟類似。其中的顯著差別在於，資料中心容錯回復是經過排程的動作，而且中斷的持續時間通常較短。

重要的是，除非 Exchange 的基礎結構相依性已經重新啟動、正在穩定操作且已經過驗證，否則不會執行容錯回復。如果這些相依性無法使用或狀況不良，容錯回復的處理程序就會比必要的中斷時間更久，且程序有可能會完全失敗。

## 信箱伺服器角色容錯回復

信箱伺服器角色應該是容錯回復到主要資料中心的第一個角色。下列步驟詳細說明信箱伺服器角色容錯回復處理程序：

1.  主要資料中心的 Mailbox Server 會在資料中心轉換的處理程序中，進入已停止狀態。當環境 (例如主要資料中心、Exchange 相依性及廣域網路 (WAN) 連線) 就緒時，第一步就是讓已還原的主要資料中心的 Mailbox Server 進入啟動狀態，並將其合併到 DAG。其實作方式取決於 DAG 是否處於 DAC 模式。
    
    1.  如果 DAG 處於 DAC 模式，您可以使用 [Start-DatabaseAvailabilityGroup](https://technet.microsoft.com/zh-tw/library/dd335076\(v=exchg.150\)) 指令程式，將 DAG 成員重新合併至主要站台。接著，若要確定 DAG 已使用適當的仲裁模型，請對 DAG 執行 [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/zh-tw/library/dd297934\(v=exchg.150\)) 指令程式，而不指定任何參數。
    
    2.  如果 DAG 不處於 DAC 模式，您可以使用 [Add-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/zh-tw/library/dd298049\(v=exchg.150\)) 指令程式，重新合併 DAG 成員。

2.  當主要資料中心的 Mailbox Server 合併到 DAG 之後，這些 Mailbox Server 需要一些時間才能同步處理其資料庫副本。視失敗的性質、中斷的長度及管理員在中斷期間採取的動作而定，可能需要重新植入資料庫副本。例如，如果您在中斷期間，從失敗的主要資料中心移除資料庫副本，讓次要資料中心的剩餘主動副本發生記錄檔截斷，則需要重新植入。每個資料庫都能夠個別從這個點繼續下去。如果主要資料中心的複寫資料庫副本狀況良好，就可以繼續進行下一個步驟。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>此處理程序不需要同時移動所有資料庫。雖然您應該同時移動組織的大多數資料庫，但是如果主要資料中心的資料庫副本產生問題，有些資料庫就可能存留在次要資料中心。</td>
    </tr>
    </tbody>
    </table>


3.  如果主要資料中心的大多數資料庫狀況良好，就可以排定容錯回復中斷。達到排定的時間時，必須採取下列步驟：
    
    1.  在資料中心轉換過程中，DAG 會設定為使用替代見證伺服器。DAG 必須重新設定，才能使用主要資料中心的見證伺服器。如果您使用的是在主要資料中心中斷之前所使用的相同見證伺服器及見證目錄，則可以執行 `Set-DatabaseAvailabilityGroup -Identity DAGName` 命令。如果打算使用與原始見證伺服器和目錄不同的見證伺服器或見證目錄，請使用 [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/zh-tw/library/dd297934\(v=exchg.150\)) 命令並搭配適當的值，來設定見證伺服器和見證目錄參數。
    
    2.  應該從次要資料中心卸載已在主要資料中心重新啟動的資料庫。您可以使用 [Dismount-Database](https://technet.microsoft.com/zh-tw/library/bb124936\(v=exchg.150\)) 指令程式卸載資料庫。
    
    3.  卸載資料庫之後，Client Access Server URL 就應該從次要資料中心移到主要資料中心。變更 DNS 記錄，讓 URL 指向主要資料中心的 Client Access Server 或陣列，即可完成此動作。這樣會導致系統行為就像每個移動的資料庫都發生資料庫容錯移轉一樣。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>除非 Client Access Server URL 已移動，且 DNS TTL 及快取項目都已過期，否則請勿繼續進行下一個步驟。如果在 Client Access Server URL 移到主要資料中心之前，就啟動主要資料中心的資料庫，則會導致組態無效 (例如，裝載伺服器在自己的 Active Directory 站台中沒有 Client Access Server)。</td>
        </tr>
        </tbody>
        </table>
    
    4.  因爲主要資料中心的每個資料庫都狀況良好，所以只要執行資料庫轉換，就可以在主要資料中心啟動這些資料庫。針對每個要啟動的資料庫使用 [Move-ActiveMailboxDatabase](https://technet.microsoft.com/zh-tw/library/dd298068\(v=exchg.150\)) 指令程式，即可完成此動作。
    
    5.  在每個資料庫都移到主要資料中心之後，就可以使用 [Mount-Database](https://technet.microsoft.com/zh-tw/library/aa998871\(v=exchg.150\)) 指令程式加以裝載。

當主要資料中心的一或多個資料庫成為主動且已裝載之後，就可以執行其他伺服器角色的容錯回復程序。

## Client Access Server 容錯回復

由用戶端、其他伺服器及 IP 閘道用來解析 Client Access Server、傳輸和整合通訊服務及 Edge Transport Server 之服務端點的內部和外部 DNS 記錄，都已在轉換過程中修改，以指向次要資料中心裡對應的端點。其他伺服器角色的容錯回復處理程序包括修改這些記錄，以指向主要資料中心的已還原服務端點。

與轉換至次要資料中心時進行的 DNS 變更一樣，用戶端、伺服器及 IP 閘道都會繼續嘗試連接，而且應該會在原始 DNS 項目的 TTL 到期之後自動連接，以及在 DNS 快取的項目到期之後自動連接。

回到頁首

## 重新建立站台恢復

成功完成容錯回復到主要資料中心之後，您就可以驗證次要資料中心的每個信箱資料庫副本的健康狀況及狀態，以重新建立主要資料中心的站台恢復。此外，如果次要資料中心有任何資料庫副本已設為阻止啟動，您也可以在此時重新設定。

回到頁首

