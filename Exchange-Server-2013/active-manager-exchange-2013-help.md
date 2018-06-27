---
title: 'Active Manager: Exchange 2013 Help'
TOCTitle: Active Manager
ms:assetid: f4be27b7-1d7c-47b4-87ac-bfdfcc046f00
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd776123(v=EXCHG.150)
ms:contentKeyID: 50474596
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Active Manager

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-07_

Microsoft Exchange Server 2013 包含一個稱為 *Active Manager* 的元件，用於管理包含資料庫可用性群組 (DAG) 和信箱資料庫副本的高可用性平台。Active Manager 在所有信箱伺服器的 Microsoft Exchange 複寫服務 (MSExchangeRepl.exe) 中執行。在不是 DAG 成員的信箱伺服器上，有一個 Active Manager 角色：*「獨立 Active Manager」*。在隸屬於 DAG 成員的伺服器上，有兩個 Active Manager 角色：*主要 Active Manager* (PAM) 與*待機 Active Manager* (SAM)。PAM 是 DAG 中決定哪些副本為主動和被動的 Active Manager 角色。PAM 負責取得拓撲變更通知，並回應伺服器失敗。取得 PAM 角色的 DAG 成員，一律為目前擁有叢集仲裁資源的成員 (預設叢集群組)。如果擁有叢集仲裁資源的伺服器失敗，則 PAM 角色會自動移至取得叢集仲裁資源擁有權的剩餘伺服器。此外，如果您需要中斷主控叢集仲裁資源的伺服器連線，以便進行維護或升級，首先必須將 PAM 移至 DAG 中的另一台伺服器上。PAM 會控制資料庫副本之間主動委派的所有移動。(任何指定時間只能有一個主動副本，該副本可以是已裝載或已卸載。)PAM 同時會在本機系統上執行 SAM 角色功能，偵測本機資料庫與本機資訊儲存庫的失敗。

SAM 所提供的資訊，是關於哪一台伺服器會將信箱資料庫的主動副本裝載至執行 Active Manager 用戶端元件的其他 Exchange 元件 (例如，用戶端存取或傳輸服務)。SAM 會偵測到本機資料庫與本機資訊儲存庫的失敗。它會要求 PAM 初始化容錯移轉 (如果資料庫已複寫的話) 來回應失敗。SAM 無法決定容錯移轉目標，也無法更新 PAM 中資料庫的位置狀態。它會存取主動資料庫副本位置狀態，以回答所收到的主動資料庫副本查詢。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Exchange 2013 不是叢集式應用程式。它會使用 clusapi.dll 中實作的叢集程式庫功能，來執行叢集、群組、叢集網路 (活動訊號)、節點管理、叢集登錄與一些控制碼功能。此外，Active Manager 會將目前的信箱資料庫資訊 (例如，主動與被動資料以及裝載的資料) 儲存在叢集資料庫 (也稱為叢集登錄) 中。雖然這項資訊是直接儲存在叢集資料庫中，但卻無法由其他任何元件直接存取。</td>
</tr>
</tbody>
</table>


在 Exchange 2013 中，Microsoft Exchange 複寫服務會定期監視所有已裝載資料庫的健康狀態。此外，它還會監控可延伸儲存引擎呼 (ESE)，查看是否有任何 I/O 錯誤或失敗。當服務偵測到失敗時，會通知 Active Manager。這時 Active Manager 會判斷應該裝載那一個資料庫副本，以及裝載該資料庫需要哪些條件。此外，它會追蹤信箱資料庫的主動副本 (依據上次裝載的資料庫副本)，並將追蹤結果資訊提供給與該用戶端連線的用戶端存取伺服器。

## 最佳副本選擇

當發生失敗而無法存取已複寫信箱資料庫的主動副本時，Active Manager 會採取幾個步驟，透過選取要啟動之受影響資料庫的最佳可行被動副本，以便從失敗中復原。此處理程序在 Exchange 2010 中稱為最佳副本選擇 (BCS)，現在在 Exchange 2013 中則稱為最佳副本和伺服器選擇 (BCSS)。一般程序進行的順序如下：

1.  受管理的可用性或 Active Manager 偵測到失敗狀況，或由系統管理員啟動較不具目標的切換。

2.  PAM 執行 BCSS 內部演算法。

3.  發生名為「嘗試複製最後一個記錄檔」(ACLL) 的處理程序，它會嘗試從在容錯移轉或切換之前主控主動資料庫副本的伺服器上，複製所有遺失的記錄檔。

4.  ACLL 處理程序完成之後，會將主控資料庫副本之信箱伺服器的 *AutoDatabaseMountDial* 值，與被啟動之資料庫的複製佇列長度進行比較。此時：
    
      - 遺失記錄檔的數目等於或小於 *AutoDatabaseMountDial* 的值，此時將進行步驟 5。
    
      - 遺失記錄檔的數目大於 *AutoDatabaseMountDial* 的值，此時 Active Manager 將嘗試啟動下一個最佳可用副本 (若有)。

5.  PAM 透過遠端程序呼叫 (RPC)，向 Microsoft Exchange Information Store 發出裝載要求。此時：
    
      - 資料庫會裝載並供用戶端使用。
    
      - 資料庫不會裝載，而由 PAM 對下一個最佳副本 (若有) 執行步驟 3 和 4。

Exchange 2010、 BCS 程序評估來決定最佳的複製到啟動每個資料庫副本的數個層面。這些包括：

  - 複製佇列長度

  - 重新顯示佇列長度

  - 資料庫的狀態

  - 內容索引狀態

在 Exchange 2013 中，Active Manager 會執行所有相同的 BCS 檢查和階段，但現在還包括使用健全狀況狀態的降序條件約束。具體而言，BCSS 包含數個新的健全狀況檢查，這屬於 Exchange 2013 中內建之受管理可用性監控元件的一部分。Active Manager 執行四種新的額外檢查（以執行的順序記載）：

1.  \[全部正常\]**：**檢查在主控受影響資料庫副本的伺服器中，所有監控元件是否皆為健全狀態。

2.  \[接近一般正常\]**：**檢查在主控受影響資料庫副本的伺服器中，所有一般優先順序的監控元件是否皆為健全狀態。

3.  \[全部優於來源\]**：**檢查在主控受影響資料庫副本的伺服器中，監控元件的狀態是否皆優於目前主控受影響副本的伺服器。

4.  \[等同於來源\]**：**檢查在主控受影響資料庫副本的伺服器中，監控元件的狀態是否皆與目前主控受影響副本的伺服器相同。

如果 BCSS 是因監控元件觸發了容錯移轉而被叫用 (例如，透過容錯移轉回應程式)，則會實施另一個強制條件約束，也就是目標伺服器的元件健全狀態必須優於發生容錯移轉的伺服器。例如，如果是因 Microsoft Office Outlook Web App 失敗而透過容錯移轉回應程式觸發了容錯移轉，則 BCSS 必須選取主控受影響資料庫副本且其上之 Outlook Web App 狀況良好的伺服器。

## 最佳副本選擇程序

至於資料庫失敗 (不是通訊協定失敗)，Exchange 2013 中的 Active Manager 會執行與 Exchange 2010 相同的檢查。開始進行最佳副本選擇的程序時，Active Manager 會先建立一份可能啟動的資料庫副本清單。任何無法存取或被系統管理人員封鎖而無法啟動的資料庫副本都將被忽略，也不會用於選擇程序中。清單的順序是依據 *AutoDatabaseMountDial* 的值而定：

  - 如果主控資料庫副本之所有伺服器上的 *AutoDatabaseMountDial* 設定為 `Lossless` 以外的任何值，Active Manager 會使用複製佇列長度做為主要索引鍵，排序產生的清單。計算是根據 LastLogInspected (從副本的角度)，所以可能副本的清單是依 LastLogInspected 的最高值 (這將是複製佇列長度最低的副本) 來排序。如有必要，Active Manager 會使用「啟動喜好設定」的值做為次要索引鍵，再次排序清單，打破有兩個以上被動副本具有相同複製佇列長度的平手狀況。「啟動喜好設定」值最低的副本，在清單上具有較高優先順序。

  - 如果主控資料庫副本之任何伺服器上的 *AutoDatabaseMountDial* 設定為 `Lossless` 的值，則 Active Manager 會使用「啟動喜好設定」的值做為主要索引鍵，依遞增順序排序產生的清單。此外，如果系統管理員執行不失真伺服器或資料庫切換但未指定目標，Active Manager 也會使用「啟動喜好設定」的值做為主要索引鍵，依遞增順序排序產生的清單。

接下來，Active Manager 會嘗試在清單中尋找具有 Healthy、DisconnectedAndHealthy、DisconnectedAndResynchronizing 或 SeedingSource 狀態的信箱資料庫副本，然後再使用依序排列的十組準則來評估清單中每個副本啟動的可能性。Active Manager 會判斷是有任何可能啟動的副本符合第一組準則：

  - 它具有 Healthy 狀態的內容索引。

  - 它的副本佇列長度少於 10 個記錄檔。

  - 它的重新顯示佇列長度少於 50 個記錄檔。

如果沒有任何一個資料庫副本符合第一組準則，Active Manager 會嘗試尋找符合第二組準則的資料庫副本：

  - 它具有 Crawling 狀態的內容索引。

  - 它的副本佇列長度少於 10 個記錄檔。

  - 它的重新顯示佇列長度少於 50 個記錄檔。

如果沒有任何一個資料庫副本符合第二組準則，Active Manager 會嘗試尋找符合第三組準則的資料庫副本：

  - 它具有 Healthy 狀態的內容索引。

  - 它的重新顯示佇列長度少於 50 個記錄檔。

如果沒有任何一個資料庫副本符合第三組準則，Active Manager 會嘗試尋找符合第四組準則的資料庫副本：

  - 它具有 Crawling 狀態的內容索引。

  - 它的重新顯示佇列長度少於 50 個記錄檔。

如果沒有任何一個資料庫副本符合第四組準則，Active Manager 會嘗試尋找符合第五組準則的資料庫副本：

  - 它的重新顯示佇列長度少於 50 個記錄檔。

如果沒有任何一個資料庫副本符合第五組準則，Active Manager 會嘗試尋找符合第六組準則的資料庫副本：

  - 它具有 Healthy 狀態的內容索引。

  - 它的副本佇列長度少於 10 個記錄檔。

如果沒有任何一個資料庫副本符合第六組準則，Active Manager 會嘗試尋找符合第七組準則的資料庫副本：

  - 它具有 Crawling 狀態的內容索引。

  - 它的副本佇列長度少於 10 個記錄檔。

如果沒有任何一個資料庫副本符合第七組準則，Active Manager 會嘗試尋找符合第八組準則的資料庫副本：

  - 它具有 Healthy 狀態的內容索引。

如果沒有任何一個資料庫副本符合所有第八組準則，Active Manager 會嘗試尋找符合第九組準則的資料庫副本：

  - 它具有 Crawling 狀態的內容索引。

如果沒有任何一個資料庫副本符合第九組準則，Active Manager 會嘗試使用 Healthy、DisconnectedAndHealthy、DisconnectedAndResynchronizing 或是 SeedingSource (第十組準則) 來啟動任何一個資料庫副本。如果找不到任何符合第十組準則的資料庫副本，它就無法自動啟動資料庫副本。

找到符合一或多組準則的一或多個副本之後，便會執行 ACLL 處理程序，以便將任何記錄檔從原始來源複製到可能的新主動副本。在 ACLL 處理程序完成之後，PAM 會發出裝載要求，且資料庫會裝載並供用戶端使用，或者資料庫並不會裝載，而由 PAM 搜尋下一個最佳副本 (若有)。

