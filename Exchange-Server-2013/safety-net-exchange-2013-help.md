---
title: '安全網: Exchange 2013 Help'
TOCTitle: 安全網
ms:assetid: d0abb807-3b12-4c7d-bc7e-769b87c84ccb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ657495(v=EXCHG.150)
ms:contentKeyID: 50474309
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 安全網

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

在 Microsoft Exchange Server 2013、 信箱高可用性的主要機制是資料庫可用性群組 (DAG)。如需 Dag 的詳細資訊，請參閱[管理資料庫可用性群組](managing-database-availability-groups-exchange-2013-help.md)。*傳輸暫放*首度推出的Exchange 2007，且進一步已獲得改善Exchange 2010之後他們正在成功傳遞至信箱的 Dag 提供多餘郵件複本中。在Exchange 2010、 傳輸暫放有助於防止資料遺失所維護還沒有複寫至 DAG 中的被動信箱資料庫副本的已成功傳遞郵件的佇列。當失敗的信箱資料庫或伺服器所需的升級過期複本的信箱資料庫、 傳輸規則中的訊息暫放自動已提交至新的作用中信箱資料庫複本。

傳輸暫存經過 Exchange 2013 改進，現在稱為 *Safety Net*。

以下說明 Safety Net 與 Exchange 2010 中的傳輸暫放兩者類似之處。

  - 安全網是具有相關聯的信箱伺服器上的傳輸服務中的佇列。此佇列會儲存郵件已成功處理的伺服器複本。

  - 您可以指定他們到期與自動刪除之前安全網長儲存成功處理郵件的複本。預設值為 2 天。

Exchange 2013 的 Safety Net 有如下的差異：

  - 安全網不需要 Dag。不屬於 Dag 的信箱伺服器，安全網會儲存在本機 Active Directory 站台其他信箱伺服器上已傳遞郵件的複本。

  - 安全網本身現在已設為備援，且不再單一失敗點。這介紹*主要 Safety Net*與*陰影 Safety Net*的概念。如果主要 Safety Net 無法使用 12 小時以上，重新提交要求成為陰影重新提交要求，並從陰影 Safety Net 重新傳遞郵件。

  - 安全網會從 DAG 環境中的陰影備援一些責任。陰影備援不需要讓另一個已傳遞郵件的副本陰影佇列中等待複寫至 DAG 中的其他信箱伺服器上的信箱資料庫的被動副本已傳遞郵件。已傳遞郵件的複本已儲存在 Safety Net 讓郵件可以從 Safety Net 重新提交，必要時。

  - 在Exchange 2013、 傳輸高可用性是超過剛最佳郵件備援能力。Exchange 2013嘗試保證郵件備援。因此，您無法 Safety Net 的指定大小上限。您只能指定自動刪除之前安全網儲存郵件的時間。

**目錄**

How Safety Net works

Message resubmission from Safety Net

Message resubmission from Shadow Safety Net

## Safety Net 的運作方式

陰影備援都會保留郵件的重複複本中傳輸訊息時。安全網保留郵件的重複複本之後成功處理郵件。因此，安全網開始陰影備援的結束處。陰影備援，包括傳輸高可用性界限、 主要訊息、 主要伺服器、 陰影郵件及陰影伺服器還需相同的概念適用於安全網。如需詳細資訊，請參閱[陰影備援](shadow-redundancy-exchange-2013-help.md)。

郵件已成功處理的傳輸服務之前，保留主要郵件的信箱伺服器上有主要 Safety Net。這可能表示郵件已傳遞至目的地 Mailbox server 上的信箱傳輸服務。或郵件可能已轉送到 Active Directory 站台中的指定為中樞站台上的目的地 DAG 或 Active Directory 站台中的方式中的信箱伺服器。主要伺服器會處理主要訊息之後，郵件是從移動作用中的佇列到主要 Safety Net 的同一部伺服器。

保留陰影郵件的信箱伺服器上有陰影 Safety Net。陰影伺服器會決定主要伺服器已成功處理主要訊息之後，陰影 server 陰影會將郵件移陰影佇列從到陰影 Safety Net 的同一部伺服器。雖然可能看起來顯而易見、 存在的陰影 Safety Net 需要陰影備援若要啟用，且在Exchange 2013預設會啟用陰影備援。

Safety Net 使用的參數如下表所述。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>參數</th>
<th>預設值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>SafetyNetHoldTime</em> 位於 <strong>Set-TransportConfig</strong></p></td>
<td><p>2 天</p></td>
<td><p>成功處理的主要郵件時間長度儲存於主要 Safety Net，而認可的陰影郵件儲存於陰影 Safety Net。</p>
<p>您也可以在 [郵件流程] &gt; [接收連接器] &gt; [更多選項]<img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="更多選項圖示" alt="更多選項圖示" /> &gt; [組織傳輸設定] &gt; [Safety Net] &gt; [Safety Net 保留時間] 的 Exchange 系統管理中心 (EAC) 中指定此值。</p>
<p>未認可的陰影郵件最終將在 <strong>Set-TransportService</strong> 的 <em>SafetyNetHoldTime</em> 與 <em>MessageExpirationTimeout</em> 兩者的加總後從陰影 Safety Net 過期。</p>
<p>若要避免 Safety Net 重新提交期間發生資料遺失，<em>SafetyNetHoldTime</em> 的值必須大於或等於信箱資料庫延遲副本 <strong>Set-MailboxDatabaseCopy</strong> 上 <em>ReplayLagTime</em> 的值。</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-MailboxDatabaseCopy</strong> 上的 <em>ReplayLagTime</em></p></td>
<td><p>未設定</p></td>
<td><p>Microsoft Exchange 複寫服務應重新已複製到被動資料庫副本的記錄檔之前應該等待的時間量。將此參數設為值大於 0 會建立延遲的資料庫副本的信箱。最大值為 14 天。</p>
<p>若要避免 Safety Net 重新提交期間發生資料遺失，<em>ReplayLagTime</em> 的值必須小於或等於信箱資料庫延遲副本 <strong>Set-TransportConfig</strong> 上 <em>SafetyNetHoldTime</em> 的值。</p></td>
</tr>
<tr class="odd">
<td><p><em>MessageExpirationTimeout</em> 位於 <strong>Set-TransportService</strong></p></td>
<td><p>2 天</p></td>
<td><p>訊息在過期前可停留於佇列中停留多長時間。</p></td>
</tr>
<tr class="even">
<td><p><em>ShadowRedundancyEnabled</em> 位於 <strong>Set-TransportConfig</strong></p></td>
<td><p><code>$true</code></p></td>
<td><ul>
<li><p><code>$true</code> 於組織中的所有傳輸伺服器上啟動陰影備援。</p></li>
<li><p><code>$false</code> 於組織中的所有傳輸伺服器上停動陰影備援。</p></li>
</ul>
<p>備援 Safety Net 需要啟用陰影備援。</p></td>
</tr>
</tbody>
</table>


回到頁首

## 郵件從 Safety Net 重新傳遞

從 Safety Net 的訊息 resubmissions 所啟動的 Microsoft Exchange 複寫服務的管理 Dag 和信箱 Active Manager 元件所資料庫副本。若要重新提交郵件從 Safety Net 時不需要任何手動執行動作。如需 Active Manager 的詳細資訊，請參閱[Active Manager](active-manager-exchange-2013-help.md)。

有兩種基本的 Safety Net 郵件重新傳遞情況：

  - DAG 的信箱資料庫完成自動或手動容錯移轉後。

  - 啟動信箱資料庫的延遲副本後。

*延遲的信箱資料庫副本*或*延遲的副本*是信箱資料庫的被動副本所在之資料庫的更新刻意延遲以防止邏輯損毀的信箱資料庫。如需詳細資訊，請參閱[管理信箱資料庫副本](managing-mailbox-database-copies-exchange-2013-help.md)。

兩個案例的僅限重大差異最回復為移至重新提交郵件從 Safety Net 的時間。通常 DAG 中的 \[容錯移轉的信箱資料庫的新主動副本是通常數分鐘才能背後的舊作用中的數個小時複製。延遲的信箱資料庫複本通常是幾天背後的舊的主動副本。

成功重新送出從 Safety Net 延遲副本的主要需求是時間的的郵件會儲存在 Safety Net 長度必須大於或等於延遲信箱資料庫副本的延遲時間。換句話說， *SafetyNetHoldTime***Set-TransportConfig**上的值必須大於或等於*ReplayLagTime***Set-MailboxDatabaseCopy**延遲的副本上的值。

回到頁首

## 郵件從陰影 Safety Net 重新傳遞

與郵件從主要 Safety Net 重新傳遞一樣，郵件從陰影 Safety Net 重新傳遞完全自動化進行，不需要任何人工介入。

當 Active Manager 要求訊息重新送出從 Safety Net 透過特定時段時，要求會移到的傳輸服務 Mailbox server 上主要 Safety Net 其中所需的時間期間保留郵件的副本。在大型的 Exchange 組織中，很可能需要的郵件存在安全網中多個信箱伺服器上，特別是若所需的時間期間大型。

最佳化，而重新提交郵件從 Safety Net 會導致可能大量重複的傳遞。Exchange 組織內的重複傳遞都有問題，因為重複訊息偵測防止在信箱使用者看不到郵件的重複複本。但重複的郵件傳遞至 Exchange 組織外部收件者會導致郵件的重複複本。幸運地是，郵件從 Safety Net 重新送出已最佳化來減少重複的郵件傳遞Exchange 2013中。

如果主要 Safety Net 最初回應或訊息重新送出期間會變成沒有回應，Active Manager 會嘗試連絡放棄之前 12 小時繼續。12 小時之後廣播傳送給所有的傳輸服務中傳輸高可用性的信箱伺服器所需的信箱資料庫所需的時間間隔從 Safety Net 結合要求重新送出的郵件。當陰影 Safety Net 回應時，它重新提交僅為所需的時間間隔期間所需的信箱資料庫的訊息。

對於陰影 Safety Net 中儲存的陰影郵件有一些重要考量：

  - 陰影 Safety Net 不知道主要伺服器將主要郵件傳遞到何處。

  - 陰影郵件的陰影 Safety Net 只包含原始郵件信封收件者未實際收件者的主要郵件已傳遞位置。例如，郵件信封收件者可能需要展開的通訊群組。

  - 陰影 Safety net 中的訊息不需要的任何郵件更新發生之後的主要伺服器處理郵件。例如，郵件編碼或內容轉換。

從陰影 Safety Net 重新提交的陰影郵件需要完整的分類和透過 Mailbox server 上的傳輸服務的處理。大量陰影郵件的陰影 Safety Net 重新送出可能昂貴就 Mailbox server 資源。幸運地是，陰影郵件的陰影 Safety Net 重新送出也最佳化因此唯一郵件的陰影 Safety Net 針對所要求的時間間隔，而且會重新提交要求的信箱資料庫。

主要 Safety Net 與陰影 Safety Net 在郵件重新傳遞期間進行的互動如下所述。

1.  Active Manager 要求重新送出的郵件從 Safety Net 的信箱資料庫的時間間隔 5:00 到 9:00。不過，保留主要 Safety Net 的 Mailbox server 已損毀由於硬體故障。Active Manager 會重複嘗試連絡主要 Safety Net 的 12 個小時。

2.  經過 12 小時後，Active Manger 將向傳輸高可用性界限中所有信箱伺服器的傳輸服務發出廣播郵件，在時間間隔 5:00 到 9:00 內針對目標信箱資料庫尋找其他包含郵件的 Safety Net。陰影 Safety Net 回應是在時間間隔 5:00 到 9:00 內針對信箱資料庫重新傳遞的郵件。

如果主要 Safety Net 在如下所述的必要重新傳遞間隔內離線，將出現特別的互動情況。

1.  保留主要 Safety Net 的信箱伺服器上的佇列資料庫損毀，且新的佇列資料庫建立 7:00。所有主要的郵件儲存在主要 Safety Net 從 1:00 到 7:00 遺失，但伺服器能夠儲存已成功傳遞郵件的複本中安全網起始位置 7:00。

2.  Active Manager 要求在 1:00 到 9:00 的時間間隔內，從 Safety Net 針對信箱資料庫重新傳遞郵件。

3.  主要 Safety Net 在 7:00 到 9:00 的時間間隔內重新傳遞郵件。

4.  主要 Safety Net 將廣播的訊息傳送至傳輸高可用性邊界尋找包含目標信箱資料庫的郵件的時間間隔 1:00 到 7:00 主要 Safety Net 有無訊息其他安全網路中的所有信箱伺服器上的傳輸服務。陰影 Safety Net 產生第二個重新提交要求代表主要 Safety Net 的重新提交的目標信箱資料庫陰影郵件的時間間隔 1:00 到 7:00。

從 Safety Net 重新傳遞郵件時，有一些問題必須考量。

1.  所有的傳遞狀態通知 (Dsn) 和未傳遞回報 （ndr） 並非被隱藏的 Safety Net 重新提交。例如，如果主要郵件因為 NDR 所造成，將不會傳遞重新提交郵件的 NDR。

2.  當陰影 Safety Net 重新提交郵件從通訊群組中移除的使用者不可能會收到重新提交的郵件。例如將郵件傳送至含有使用者 A 」 和 「 使用者 B 的群組和兩個收件者會收到訊息。使用者 B 後續移除群組。稍後，從主要 Safety Net 重新提交要求是由主控使用者 B 的信箱的信箱資料庫。不過，主要 Safety Net 是無法使用 12 小時以上，因此陰影 Safety Net 伺服器會回應及重新提交受影響的郵件。重新送出期間擴充通訊群組時，使用者 B 不是群組的成員，將不會收到重新提交郵件的複本。

3.  新增至通訊群組的新使用者可能會收到舊的重新提交的郵件時陰影 Safety Net 重新提交郵件。例如將郵件傳送至含有使用者 A 」 和 「 使用者 B 的群組和兩個收件者會收到訊息。使用者 C 後續新增至群組。稍後，從主要 Safety Net 重新提交要求是由主控使用者 C 信箱的信箱資料庫。不過，主要 Safety Net 伺服器是無法使用 12 小時以上，因此陰影 Safety Net 伺服器會回應及重新提交受影響的郵件。重新送出期間擴充通訊群組時，使用者 C 是群組的成員，也會收到重新提交郵件的複本。

回到頁首

