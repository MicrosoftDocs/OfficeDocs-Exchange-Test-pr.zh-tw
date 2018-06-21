---
title: '混合移轉的效能因素和最佳作法: Exchange 2013 Help'
TOCTitle: 混合移轉的效能因素和最佳作法
ms:assetid: 120a7832-d2d3-47d7-b305-918360c2ef66
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Mt483789(v=EXCHG.150)
ms:contentKeyID: 70118327
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 混合移轉的效能因素和最佳作法

 

_<strong>適用版本：</strong>Exchange Server 2016_

_<strong>上次修改主題的時間：</strong>2016-12-09_

有許多方法可以將資料從內部部署電子郵件組織移轉至 Office 365 中。規劃移轉至 Office 365 時，常見的問題是如何提升資料移轉效能並最佳化移轉速度。本文討論 Exchange 混合式部署的移轉效能。如需有關其他移轉方法的效能資訊，請參閱 [Office 365 移轉效能和最佳作法](http://go.microsoft.com/fwlink/p/?linkid=623651)。

## 混合移轉的效能因素和最佳作法

混合部署移轉支援在內部部署 Exchange 伺服器與 Office 365 中的 Exchange Online 之間順利移轉。

混合部署移轉是目前為止將信箱資料移轉至 Office 365 最快的移轉方法。在實際客戶部署期間，每小時輸送量最多可達 100 GB。下表提供適用於原生 Office 365 混合移轉案例的因素清單。

如果您的內部部署環境包含地理位置分散的多個網站，您可以透過建立地理位置相近的移轉端點來改善移轉效能。這是因為在這個案例下是使用 Microsoft 的網路進行移轉，而非使用內部部署網路的集中式移轉端點。

## 因素 1：資料來源 (Exchange Server)


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>檢查清單</th>
<th>描述</th>
<th>最佳作法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>系統效能</p></td>
<td><p>資料擷取是相當耗用資料的工作。來源系統必須有足夠的資源 (例如 CPU 時間和記憶體)，才能提供更高的移轉效能。移轉期間，來源系統通常會接近日常一般使用者工作量的滿載程度，有時甚至因為有額外的移轉工作量造成系統資源缺乏，而導致使用者無法存取。</p></td>
<td><p>在試驗移轉測試期間監視系統效能。若系統忙碌，基於移轉可能變慢及潛在的服務可用性問題，建議不要對特定系統進行積極的移轉排程。如有可能的話，請提升來源系統效能，您可以增加硬體資源，以及將工作和使用者移至其他未參與移轉的伺服器以降低系統負載。</p>
<p>如需詳細資訊，請參閱：</p>
<ul>
<li><p><a href="http://go.microsoft.com/fwlink/?linkid=723566">詢問 Perf Guy︰決定 Exchange 2016 部署規模</a></p></li>
<li><p><a href="https://technet.microsoft.com/zh-tw/library/jj150551(v=exchg.150)">伺服器健康狀況與效能</a></p></li>
<li><p><a href="http://technet.microsoft.com/zh-tw/library/dd351192.aspx">了解 Exchange 2010 效能</a></p></li>
</ul>
<p>從含有多部信箱伺服器和多個資料庫的內部部署 Exchange 組織移轉時，建議您建立移轉使用者清單，以平均分配至不同的信箱伺服器和資料庫。根據個別伺服器效能，可以更進一步微調清單以增加輸送量。</p>
<p>例如，若伺服器 A 的資源可用性比伺服器 B 高出 50%，理所當然在相同的移轉批次中，來自伺服器 A 的使用者會多出 50%。類似作法也可套用至其他來源系統。</p>
<p>請在伺服器擁有最大資源可用性時執行移轉，例如下班後、週末及假日。</p></td>
</tr>
<tr class="even">
<td><p>後端工作</p></td>
<td><p>在移轉期間執行的其他後端工作。由於最好在下班後執行移轉，因此移轉常會與內部部署伺服器上所執行的其他維護工作發生衝突，例如資料備份。</p></td>
<td><p>請檢閱移轉期間可能執行的其他系統工作。建議您在其他耗用大量資源的工作未執行時，才執行資料移轉。</p>
<p><strong>注意</strong>  若為使用內部部署 Microsoft Exchange 的客戶，常見的後端工作是備份解決方案和 <a href="http://technet.microsoft.com/zh-tw/library/aa996226(exchg.65).aspx">Exchange 儲存區維護</a>。</p></td>
</tr>
</tbody>
</table>


## 因素 2：移轉伺服器

混合部署移轉是雲端啟動的提取/推送資料移轉方法，而且 Exchange 混合伺服器會作為移轉伺服器。這一點經常遭到忽略，且客戶會使用低階虛擬機器來作為混合伺服器。因而導致移轉效能低落。

**最佳作法**

除了套用先前所述的最佳作法之外，我們還測試下列最佳作法，可提升實際客戶移轉時的移轉效能：

  - 使用強大的伺服器類別實體機器作為 Exchange 混合伺服器，而非虛擬機器。

  - 在客戶的網路負載平衡器後方使用多部混合伺服器。

例如，在實際客戶移轉中，我們使用下列設定，可達到每小時 30 GB 的一致輸送量：

  - **網路** 以管道輸出 500 MB 至網際網路；內部網路為 1 GB 加上 10 GB 光纖骨幹。

  - **硬體**  兩部用戶端存取/中樞 (實體) 伺服器的規格：
    
      - CPU：Intel® Xeon® CPU E5520 @ 2.27 GHz 2.26 GHz (2 個處理器)。
    
      - RAM：24 GB。
    
      - 磁碟：八個，每個磁碟 146 GB。RAID 5 組態 = 960 GB 原始空間總計。

  - **MRSProxy**   以並行數目 100 進行設定。

## 因素 3：移轉引擎

混合部署移轉使用原生 Office 365 工具。它適用於 Office 365 移轉服務節流。

**Exchange 2003 與更新版本的 Exchange**

從 Exchange 2003 移轉時，使用者經驗會有顯著不同。不同於更新版本的 Exchange，Exchange 2003 的使用者無法在移轉資料時存取其信箱。因此，Exchange 2003 客戶通常比較關心排程移轉的時機以及移轉所需的時間，特別是當移轉效能因大型信箱或低速網路而降低時。

Exchange 2003 移轉對於中斷也很敏感。例如，在實際客戶移轉中，若移轉 10 GB 信箱，而在信箱移轉完成 50% 時發生服務事件。您必須重新啟動處理資料移轉的 Office 365 用戶端存取伺服器，才能解決此問題。在此情況下，必須重新開始移轉該信箱，這表示客戶必須重新移轉所有 10 GB 資料。移轉無法從停止的時間點繼續。但是，Exchange 2010 和更新版本的 Exchange 則可以在中斷後繼續移轉。

**最佳作法**

某些客戶會選擇針對大型且敏感的 Exchange 2003 信箱執行兩個躍點的移轉：

  - **第一個躍點**   將信箱從 Exchange 2003 移轉至 Exchange 2010 或更新版本的伺服器，通常是混合伺服器。第一個躍點為離線移動，而通常是透過區域網路進行的超高速移轉。

  - **第二個躍點**   將信箱從 Exchange 2010 或更新版本移轉至 Office 365。

第二個躍點為線上移動，可提供更佳的使用者經驗和容錯能力。此兩個躍點的方法需要暫時內部部署使用者信箱的 Exchange 授權。

**信箱複寫服務 Proxy (MRSProxy)**

MRS Proxy 為內部部署移轉功能，可搭配在 Office 365 端執行的信箱複寫服務使用。如需詳細資訊，請參閱[了解移動要求](http://technet.microsoft.com/zh-tw/library/dd298174.aspx)。

**最佳作法**

您可以設定內部部署 Exchange 混合伺服器的最大 MRSProxy 連線數目。請執行下列 Windows PowerShell 命令。

    Set-WebServicesVirtualDirectory -Identity "EWS (Default Web Site)" -MRSMaxConnections <number between 0 and unlimited; default is 100>

<table>
<thead>
<tr class="header">
<th><img src="images/JJ150559.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>大多數客戶的移轉不需變更預設 MRSMaxConnections 值。若需要保護來源伺服器，以免移轉負載造成負荷過高，客戶可以減少連線數目。此設定是根據 MRSProxy 伺服器。若客戶擁有兩部 MRSProxy 伺服器，每部伺服器設為 10 個連線，則會取得 20 (2 x 10) 個 MRSProxy 連線總數。如需在內部部署 Exchange 2010 組織中設定 MRSProxy 服務的詳細資訊，請參閱<a href="http://technet.microsoft.com/zh-tw/library/ee732395.aspx">啟動遠端用戶端存取伺服器上的 MRSProxy 服務</a>。</td>
</tr>
</tbody>
</table>


## 因素 4：網路

**驗證測試**

若為執行 Exchange 2010 或更新版本的客戶，可透過執行多個測試信箱移轉來完成混合移轉的網路效能測試。或者，您可使用 -SuspendWhenReadyToComplete 選項移轉實際使用者信箱，以取得移轉效能的指示。測試完成之後，請移除該移動要求以避免影響使用者。

如需移動要求的相關資訊，請參閱[New-MoveRequest](https://technet.microsoft.com/zh-tw/library/dd351123\(v=exchg.150\))。

## 因素 5：Office 365 服務

Office 365 資源狀況節流會影響使用 Office 365 混合部署移轉執行的移轉。如需詳細資訊，請參閱以上的「Office 365 資源狀況節流」一節。

