---
title: '佇列篩選器: Exchange 2013 Help'
TOCTitle: 佇列篩選器
ms:assetid: fbfbdcab-e0d2-4ed9-8f7f-e5fa2c87360d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb125237(v=EXCHG.150)
ms:contentKeyID: 50474646
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 佇列篩選器

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

篩選會產生佇列的不同的檢視。您可以使用的佇列屬性做為篩選選項。藉由指定篩選準則，您可以快速找出佇列，並採取動作。下列案例是您如何使用佇列篩選來管理郵件流程的範例：

  - 您會收到一則訊息來自 Microsoft System Center Operations Manager 表示佇列長度超過建立臨界值。您想要調查全伺服器的郵件流程問題是否存在。
    
    您可以建立篩選器來檢視郵件計數超過考慮典型的所有佇列。如果在指定的郵件流程問題，您可以在篩選結果中選取的所有佇列並而繼續調查擱置佇列。

  - 您暫停數個佇列調查郵件流程問題的原因。您判斷問題所造成的不正確的連接器組態和現在固定。
    
    您可以建立篩選來檢視狀態為「已擱置」的所有佇列，然後選取篩選結果內的所有佇列，並繼續進行這些佇列的活動。

## 篩選佇列時所用的佇列內容

您可以使用佇列內容來建立篩選和尋找符合指定的條件的佇列。您可以在佇列檢視器，或使用*Filter*參數的佇列管理指令程式來建立篩選器。請注意佇列管理指令程式支援多個比佇列檢視器可篩選的內容。下表列出依佇列屬性的可篩選與這些屬性的有效值。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>佇列檢視器佇列內容</th>
<th>命令介面佇列屬性</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>不適用</p></td>
<td><p><code>DeferredMessageCount</code></p></td>
<td><p>此屬性會識別因收件者解析期間所發生暫時性錯誤傳回至提交佇列的訊息數。如需延期郵件的詳細資訊，請參閱<a href="recipient-resolution-exchange-2013-help.md">收件者的解決方法</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>傳遞類型</strong></p></td>
<td><p><code>DeliveryType</code></p></td>
<td><p>在 <a href="queues-exchange-2013-help.md">佇列</a> 主題的「NextHopSolutionKey」一節當中，會說明 <strong>DeliveryType</strong> 的有效值。</p></td>
</tr>
<tr class="odd">
<td><p>不適用</p></td>
<td><p><code>Identity</code></p></td>
<td><p>此屬性是格式為<em>&lt;Server&gt;\&lt;Queue&gt;</em>佇列的識別。如需詳細資訊請參閱<a href="queues-exchange-2013-help.md">佇列</a>主題的 「 佇列身分識別 」 一節。</p></td>
</tr>
<tr class="even">
<td><p>不適用</p></td>
<td><p><code>IncomingRate</code></p></td>
<td><p>此屬性為計算的數字表示郵件會進入佇列的速度。如需詳細資訊，請參閱<a href="queues-exchange-2013-help.md">佇列</a>主題中的 「 IncomingRate、 OutgoingRate 以及 Velocity 」 一節。</p></td>
</tr>
<tr class="odd">
<td><p><strong>上個錯誤</strong></p></td>
<td><p><code>LastError</code></p></td>
<td><p>此內容指出文字字串，記錄佇列的上個錯誤。</p></td>
</tr>
<tr class="even">
<td><p><strong>上次重試時間</strong></p></td>
<td><p><code>LastRetryTime</code></p></td>
<td><p>此內容指出狀態為 <code>Retry</code> 之佇列的上次嘗試進行連線日期/時間。</p></td>
</tr>
<tr class="odd">
<td><p>不適用</p></td>
<td><p><code>LockedMessageCount</code></p></td>
<td><p>此內容保留供 Microsoft 內部使用，而不會用於內部部署的 Exchange 2013 組織。</p></td>
</tr>
<tr class="even">
<td><p><strong>郵件計數</strong></p></td>
<td><p><code>MessageCount</code></p></td>
<td><p>此內容指出佇列中的郵件數目。</p></td>
</tr>
<tr class="odd">
<td><p>不適用</p></td>
<td><p><code>NextHopCategory</code></p></td>
<td><p>此屬性為<code>Internal</code>或<code>External</code>會指定佇列的下一個躍點，並根據佇列<strong>DeliveryType</strong>屬性的值。如需詳細資訊，請參閱<a href="queues-exchange-2013-help.md">佇列</a>主題的 「 NextHopSolutionKey 」 一節。</p></td>
</tr>
<tr class="even">
<td><p>不適用</p></td>
<td><p><code>NextHopConnector</code></p></td>
<td><p>此屬性是下一個躍點的 GUID，並根據佇列<strong>DeliveryType</strong>屬性的值。如需詳細資訊，請參閱<a href="queues-exchange-2013-help.md">佇列</a>主題的 「 NextHopSolutionKey 」 一節。</p></td>
</tr>
<tr class="odd">
<td><p><strong>下一個躍點網域</strong></p></td>
<td><p><code>NextHopDomain</code></p></td>
<td><p>此屬性為下一個躍點的名稱，並根據佇列<strong>DeliveryType</strong>屬性的值。如需詳細資訊，請參閱<a href="queues-exchange-2013-help.md">佇列</a>主題的 「 NextHopSolutionKey 」 一節。</p></td>
</tr>
<tr class="even">
<td><p><strong>下一次重試時間</strong></p></td>
<td><p><code>NextRetryTime</code></p></td>
<td><p>此內容指出狀態為 <code>Retry</code> 之佇列的下次嘗試進行連線日期/時間。</p></td>
</tr>
<tr class="odd">
<td><p>不適用</p></td>
<td><p><code>OutgoingRate</code></p></td>
<td><p>此屬性會指出如何快速訊息離開佇列的度量數字。如需詳細資訊，請參閱<a href="queues-exchange-2013-help.md">佇列</a>主題中的 「 IncomingRate、 OutgoingRate 以及 Velocity 」 一節。</p></td>
</tr>
<tr class="even">
<td><p>不適用</p></td>
<td><p><code>RiskLevel</code></p></td>
<td><p>此內容保留供 Microsoft 內部使用，而不會用於內部部署的 Exchange 2013 組織。</p></td>
</tr>
<tr class="odd">
<td><p><strong>狀態</strong></p></td>
<td><p><code>Status</code></p></td>
<td><p>此屬性會指出目前的佇列狀態。佇列可以有一個下的 [狀態] 值使用中] 連線，None、 暫停、 準備、 或重試。如需詳細資訊，請參閱<a href="queues-exchange-2013-help.md">佇列</a>主題的 「 佇列狀態 」 一節。</p></td>
</tr>
<tr class="even">
<td><p>不適用</p></td>
<td><p><code>TlsDomain</code></p></td>
<td><p>若為「網域安全性」設定網域，則此內容會包含目的地網域的 FQDN。</p></td>
</tr>
<tr class="odd">
<td><p>不適用</p></td>
<td><p><code>Velocity</code></p></td>
<td><p>此屬性包含計算的數字表示佇列已清空如何有效率地。如需詳細資訊，請參閱<a href="queues-exchange-2013-help.md">佇列</a>主題中的 「 IncomingRate、 OutgoingRate 以及 Velocity 」 一節。</p></td>
</tr>
</tbody>
</table>

