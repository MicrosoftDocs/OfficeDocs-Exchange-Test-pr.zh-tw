---
title: '使用 Exchange 管理命令介面管理佇列: Exchange 2013 Help'
TOCTitle: 使用 Exchange 管理命令介面管理佇列
ms:assetid: 5433c1d3-ad2e-4f82-b50d-b67964b32f26
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa998047(v=EXCHG.150)
ms:contentKeyID: 51409179
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用 Exchange 管理命令介面管理佇列

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

與舊版的 Exchange 一樣，您可以在 Exchange Server 2013 中使用 Exchange 管理命令介面，來檢視佇列和佇列中郵件的相關資訊，以及對佇列和郵件執行管理動作。在 Exchange 2013 中，佇列位於 Mailbox Server 和 Edge Transport Server 上。本主題將這些伺服器稱為 *Transport Server*。

當您使用命令介面來檢視及管理 Transport Server 上的佇列和佇列中的郵件時，請務必了解如何識別要管理的佇列或郵件。在一般的情況下，Transport Server 含有大量佇列和待傳遞的郵件。您可以使用佇列和郵件管理指令程式上的篩選參數，識別要檢視或管理的佇列或郵件。

請注意，您也可以使用 Exchange 工具箱內的佇列檢視器來管理佇列和佇列中的郵件。不過，佇列和郵件檢視指令程式支援的可篩選內容和篩選選項比佇列檢視器還多。如需使用佇列檢視器的詳細資訊，請參閱[佇列檢視器](queue-viewer-exchange-2013-help.md)。

**目錄**

  - Queue filtering parameters
    
      - Queue identity
    
      - Queue Filter parameter
    
      - Include and Exclude parameters

  - Get-QueueDigest

  - Message filtering parameters
    
      - Message identity
    
      - Message Filter parameter
    
      - Queue parameter

  - Comparison operators to use when filtering queues or messages

  - Advanced paging parameters

## 佇列篩選參數

下表說明佇列管理指令程式提供的篩選參數。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>指令程式</th>
<th>篩選參數</th>
<th>註解</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Get-Queue</strong></p></td>
<td><p><em>Identity</em></p>
<p><em>Filter</em></p>
<p><em>Include</em></p>
<p><em>Exclude</em></p></td>
<td><p>您不能在同一個命令中同時使用 <em>Identity</em> 參數和 <em>Filter</em> 參數。您可以在同一個命令中同時使用 <em>Include</em> 和 <em>Exclude</em> 參數及 <em>Filter</em> 參數。</p></td>
</tr>
<tr class="even">
<td><p><strong>Resume-Queue</strong></p>
<p><strong>Retry-Queue</strong></p>
<p><strong>Suspend-Queue</strong></p></td>
<td><p><em>Identity</em></p>
<p><em>Filter</em></p></td>
<td><p>您需要擇一使用 <em>Identity</em> 參數或 <em>Filter</em> 參數，不過不能在同一個命令中同時使用。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Get-QueueDigest</strong></p></td>
<td><p><em>Server</em></p>
<p><em>Dag</em></p>
<p><em>Site</em></p>
<p><em>Forest</em></p>
<p><em>Filter</em></p></td>
<td><p>您需要使用 <em>Server</em>、<em>Dag</em>、<em>Site</em> 或 <em>Forest</em> 參數，不過不能在同一個命令中搭配使用。您可以使用 <em>Filter</em> 參數來搭配其他任何篩選參數。</p></td>
</tr>
</tbody>
</table>


請注意，所有佇列管理指令程式均提供 *Server* 參數。在 **Get-QueueDigest**指令程式上，*Server* 參數是指定要檢視佇列摘要資訊之伺服器的範圍參數。在其他所有佇列管理指令程式上，您可以使用 *Server* 參數來連接特定的伺服器，以及在該伺服器上執行佇列管理命令。當您使用 *Server* 參數時，不一定要搭配 *Filter* 參數，不過 *Server* 參數不能搭配 *Identity* 參數。您可以使用 Transport Server 的主機名稱或 FQDN 來搭配 *Server* 參數。

回到頁首

## 佇列識別碼

佇列管理指令程式上的 *Identity* 參數能識別特定的佇列。使用 *Identity* 參數時，不能指定其他任何佇列篩選參數，因為您已唯一識別佇列。*Identity* 參數使用基本語法 *\<Server\>*\\*\<Queue\>*。

*\<Server\>* 預留位置是 Exchange 伺服器的主機名稱或 FQDN (如 `mailbox01` 或 `mailbox01.contoso.com`)。省略 *\<Server\>* 限定詞即意指本機伺服器。

\<*Queue*\> 預留位置接受以下任一值：

  - **持續佇列名稱**   所有 Mailbox Server 或 Edge Transport Server 上的持續佇列擁有唯一而一致的名稱。持續佇列名稱包括：
    
      - **提交**   此佇列含有待分類程式處理的郵件。
    
      - **無法存取**   此佇列含有無法路由傳送的郵件。若未將郵件放入佇列，此佇列便不存在。
    
      - **毒藥**   此佇列含有經判定為對 Exchange 伺服器有害的郵件。若未將郵件放入佇列，此佇列便不存在。

  - **傳遞佇列名稱**   傳遞佇列的名稱是佇列之 **NextHopDomain** 內容的值。例如，佇列名稱可以是傳送連接器的位址空間、Active Directory 站台的名稱或 DAG 的名稱。如需詳細資訊，請參閱[佇列](queues-exchange-2013-help.md)主題的「NextHopSolutionKey」一節。

  - **佇列整數**   在佇列資料庫中，系統會將唯一的整數值指派給傳遞佇列和陰影佇列。然而，您需要執行 **Get-Queue** 指令程式，以在 **Identity** 或 **QueueIdentity** 內容中尋找佇列的整數值。

  - **陰影佇列名稱**   陰影佇列使用 `Shadow\`*\<QueueInteger\>* 語法

下表摘要列出可用來在佇列管理指令程式上與 *Identity* 參數搭配的語法。在所有值中，*\<Server\>* 是主機名稱或伺服器的 FQDN。

### 佇列識別碼格式

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Identity 參數值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>&lt;Server&gt;\&lt;PersistentQueueName&gt;</code> 或<code>&lt;PersistentQueueName&gt;</code></p></td>
<td><p>指定之伺服器或本機伺服器上的持續佇列。</p>
<p><em>&lt;PersistentQueueName&gt;</em> 是 <code>Submission</code>、<code>Unreachable</code> 或 <code>Poison</code>。</p></td>
</tr>
<tr class="even">
<td><p><code>&lt;Server&gt;\&lt;NextHopDomain&gt;</code> 或<code>&lt;NextHopDomain&gt;</code></p></td>
<td><p>指定之伺服器或本機伺服器上的傳遞佇列。</p>
<p><em>&lt;NextHopDomain&gt;</em> 是佇列中郵件的路由目的地或傳遞群組。如需詳細資訊，請參閱<a href="queues-exchange-2013-help.md">佇列</a>主題的「NextHopSolutionKey」一節。</p></td>
</tr>
<tr class="odd">
<td><p><code>&lt;Server&gt;\&lt;QueueInteger&gt;</code> 或<code>&lt;QueueInteger&gt;</code></p></td>
<td><p>指定之伺服器或本機伺服器上的傳遞佇列。</p>
<p><em>&lt;QueueInteger&gt;</em> 是顯示於 <strong>Get-Queue</strong>指令程式之 <strong>Identity</strong> 內容中佇列的唯一整數值。</p></td>
</tr>
<tr class="even">
<td><p><code>&lt;Server&gt;\Shadow\&lt;QueueInteger&gt;</code> 或<code>Shadow\&lt;QueueInteger&gt;</code></p></td>
<td><p>指定之伺服器或本機伺服器上的陰影佇列。</p></td>
</tr>
<tr class="odd">
<td><p><code>&lt;Server&gt;\*</code> 或<code>*</code></p></td>
<td><p>指定之伺服器或本機伺服器上的所有佇列。請注意，這些值只能搭配 <strong>Get-Queue</strong> 指令程式。</p></td>
</tr>
</tbody>
</table>


回到頁首

## 佇列篩選參數

在所有佇列管理指令程式上，您可以使用 *Filter* 參數來根據佇列內容指定要檢視或管理的佇列。*Filter* 參數會建立含有比較運算子的運算式，這些運算子會將佇列作業限制為滿足篩選準則的佇列。您可以使用 `-and` 邏輯運算子指定結果必須符合的多個條件。

如需可搭配 *Filter* 參數的完整佇列內容清單，請參閱[佇列](queues-exchange-2013-help.md)。

如需可搭配 *Filter* 參數的比較運算子清單，請參閱本主題的Comparison operators to use when filtering queues or messages一節。

如需使用 *Filter* 參數來檢視及管理佇列的程序範例，請參閱[管理佇列](manage-queues-exchange-2013-help.md)。

回到頁首

## Include 和 Exclude 參數

Exchange 2013 的 `Get-Queue` 指令程式含有 *Include* 和 *Exclude* 參數。這兩個參數可以個別使用、同時使用，以及與 *Filter* 參數搭配使用，以便在本機或指定之 Transport Server 上微調佇列結果。例如，您可以：

  - 排除結果中空白的佇列。

  - 排除結果中前往外部目的地的佇列。

  - 在結果中包含具有特定 **DeliveryType** 值的佇列。

*Include* 和 *Exclude* 參數使用以下佇列內容來篩選佇列：


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
<th>描述</th>
<th>命令介面程式碼範例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>DeliveryType</code></p></td>
<td><p>此值會根據 <strong>DeliveryType</strong> 內容來包含或排除佇列。您可以指定多個以逗號分隔的值。<a href="queues-exchange-2013-help.md">佇列</a>主題的「NextHopSolutionKey」一節有 <strong>DeliveryType</strong> 之有效值的說明。</p></td>
<td><p>對於下一個躍點是已針對智慧主機路由進行設定之本機伺服器上的傳送連接器，以下範例會傳回符合此情況之本機伺服器上的所有傳遞佇列：</p>
<p><code>Get-Queue -Include SmartHostConnectorDelivery</code></p></td>
</tr>
<tr class="even">
<td><p><code>Empty</code></p></td>
<td><p>此值可包含或排除空白的佇列。空白佇列的 <strong>MessageCount</strong> 內容值為 <code>0</code>。</p></td>
<td><p>此範例會傳回含有郵件之本機伺服器上的所有佇列</p>
<p><code>Get-Queue -Exclude Empty</code></p></td>
</tr>
<tr class="odd">
<td><p><code>External</code></p></td>
<td><p>此值可包含或排除 <strong>NextHopCategory</strong> 內容值為 <code>External</code> 的佇列。</p>
<p>外部佇列的 <strong>DeliveryType</strong> 值一律為以下任一項：</p>
<ul>
<li><p><code>DeliveryAgent</code></p></li>
<li><p><code>DnsConnectorDelivery</code></p></li>
<li><p><code>NonSmtpGatewayDelivery</code></p></li>
<li><p><code>SmartHostConnectorDelivery</code></p></li>
</ul>
<p>如需詳細資訊，請參閱<a href="queues-exchange-2013-help.md">佇列</a>主題的「NextHopSolutionKey」一節。</p></td>
<td><p>此範例會傳回本機伺服器上的所有內部佇列</p>
<p><code>Get-Queue -Exclude External</code></p></td>
</tr>
<tr class="even">
<td><p><code>Internal</code></p></td>
<td><p>此值可包含或排除 <strong>NextHopCategory</strong> 內容值為 <code>Internal</code> 的佇列。如需詳細資訊，請參閱<a href="queues-exchange-2013-help.md">佇列</a>主題的「NextHopSolutionKey」一節。</p></td>
<td><p>此範例會傳回本機伺服器上的所有內部佇列。</p>
<p><code>Get-Queue -Include Internal</code></p></td>
</tr>
</tbody>
</table>


請注意，您可以使用 *Filter* 參數來複製 *Include* 和 *Exclude* 參數的功能。例如，`Get-Queue -Exclude Empty` 命令會產生與 `Get-Queue -Filter {MessageCount -gt 0}` 相同的結果。不過，*Include* 和 *Exclude* 參數的語法比較簡單，也比較容易記住。

回到頁首

## Get-QueueDigest

Exchange 2013 新增了名為 **Get-QueueDigest** 的佇列指令程式。此指令程式能讓您使用單一命令檢視 Exchange 組織中部分或全部佇列的相關資訊。具體來說，**Get-QueueDigest** 指令程式可讓您根據佇列在伺服器、DAG、Active Directory 站台或整個 Active Directory 樹系中的位置，來檢視佇列的相關資訊。請注意，結果中不會包含周邊網路中已訂閱的 Edge Transport Server 上的佇列。此外，**Get-QueueDigest** 也可在 Edge Transport Server 上使用，但結果只會顯示 Edge Transport Server 上的佇列。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>依預設，<strong>Get-QueueDigest</strong> 指令程式會顯示包含十封郵件以上的傳遞佇列，而且會是一到二分鐘之前的結果。如需如何變更這些預設值的指示，請參閱<a href="configure-get-queuedigest-exchange-2013-help.md">設定 Get-QueueDigest</a>。</td>
</tr>
</tbody>
</table>


下表說明可用來搭配 **Get-QueueDigest**指令程式的篩選和排序參數。


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
<td><p><em>Dag</em>、<em>Server</em> 或 <em>Site</em></p></td>
<td><p>這些參數會互斥，而且能設定指令程式的範圍。您需要指定這些參數中的其中一個參數，或指定 <em>Forest</em> 參數。在一般的情況下，您會使用伺服器、DAG 或 Active Directory 站台的名稱，不過您可以使用任何可唯一識別伺服器、DAG 或站台的值。您可以指定多個伺服器、DAG 或站台，並以逗號加以分隔。</p></td>
</tr>
<tr class="even">
<td><p><em>Forest</em></p></td>
<td><p>如果您不是使用 <em>Dag</em>、<em>Server</em> 或 <em>Site</em> 參數，便必須使用此參數。您不需要為此參數指定任何值。此參數能讓您取得 Active Directory 樹系中所有 Exchange 2013 Mailbox Server 的佇列。您不能使用 <em>Forest</em> 參數來檢視遠端 Active Directory 樹系中的佇列。</p></td>
</tr>
<tr class="odd">
<td><p><em>DetailsLevel</em></p></td>
<td><p>此參數接受的值為 <code>None</code>、<code>Normal</code> 及 <code>Verbose</code>。預設值為 <code>Normal</code>。使用 <code>None</code> 值時，結果之 <strong>[詳細資料]</strong> 欄中的佇列名稱會遭到省略。</p></td>
</tr>
<tr class="even">
<td><p><em>Filter</em></p></td>
<td><p>此參數可讓您根據佇列內容篩選佇列。您可以使用任何可篩選的佇列內容，如<a href="queue-filters-exchange-2013-help.md">佇列篩選器</a>主題所述。</p></td>
</tr>
<tr class="odd">
<td><p><em>GroupBy</em></p></td>
<td><p>此參數會為佇列結果分組。您可以根據以下任一內容為結果分組：</p>
<ul>
<li><p>DeliveryType</p></li>
<li><p>LastError</p></li>
<li><p>NextHopCategory</p></li>
<li><p>NextHopDomain</p></li>
<li><p>NextHopKey</p></li>
<li><p>狀態</p></li>
<li><p>ServerName</p></li>
</ul>
<p>依預設，系統會根據 <code>NextHopDomain</code> 為結果分組。如需這些佇列內容的相關資訊，請參閱<a href="queue-filters-exchange-2013-help.md">佇列篩選器</a>。</p></td>
</tr>
<tr class="even">
<td><p><em>ResultSize</em></p></td>
<td><p>此參數能將佇列結果限制為您指定的值。系統會根據佇列中的郵件數目以遞減順序為佇列排序，並且會根據 <em>GroupBy</em> 參數指定的值分組。預設值為 1000。這代表依預設此命令會顯示前 1000 個根據 <strong>NextHopDomain</strong> 分組的佇例，並根據包含最多郵件的佇列到包含最少郵件的佇列的順序進行排序。</p></td>
</tr>
<tr class="odd">
<td><p><em>Timeout</em></p></td>
<td><p>此參數可指定作業逾時前的秒數。預設值是 <code>00:00:10</code> 或 10 秒。</p></td>
</tr>
</tbody>
</table>


此範例會傳回名為 Mailbox01、Mailbox02 及 Mailbox03 等 Exchange 2013 Mailbox Server 上所有非空白的外部佇列。

    Get-QueueDigest -Server Mailbox01,Mailbox02,Mailbox03 -Include External -Exclude Empty

回到頁首

## 郵件篩選參數

下表說明郵件管理指令程式提供的篩選參數。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>指令程式</th>
<th>篩選參數</th>
<th>註解</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Get-Message</strong></p></td>
<td><p><em>Identity</em></p>
<p><em>Filter</em></p>
<p><em>Queue</em></p></td>
<td><p>所有篩選參數均會互斥，而您可以在同一個命令中搭配使用。</p></td>
</tr>
<tr class="even">
<td><p><strong>Remove-Message</strong></p>
<p><strong>Resume-Message</strong></p>
<p><strong>Suspend-Message</strong></p></td>
<td><p><em>Identity</em></p>
<p><em>Filter</em></p></td>
<td><p>您需要擇一使用 <em>Identity</em> 參數或 <em>Filter</em> 參數，不過不能在同一個命令中同時使用。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Export-Message</strong></p></td>
<td><p><em>Identity</em></p></td>
<td><p><em>Identity</em> 參數是必要的。</p></td>
</tr>
</tbody>
</table>


請注意，除了 **Export-Message**指令程式之外，所有郵件管理指令程式均提供 *Server* 參數。您可以使用 *Server* 參數來連接特定的伺服器，以及在該伺服器上執行郵件管理命令。當您使用 *Server* 參數時，不一定要搭配 *Filter* 參數，不過 *Server* 參數不能搭配 *Identity* 參數。您可以使用 Transport Server 的主機名稱或 FQDN 來搭配 *Server* 參數。

回到頁首

## 郵件識別碼

郵件管理指令程式上的 *Identity* 參數能識別一或多個佇列中的特定郵件。使用 *Identity* 參數時，不能指定其他任何郵件篩選參數，因為您已唯一識別郵件。*Identity* 參數使用基本語法 *\<Server\>*\\*\<Queue\>*\\*\<MessageInteger\>*。

*\<Server\>* 預留位置是 Exchange 伺服器的主機名稱或 FQDN (如 `mailbox01` 或 `mailbox01.contoso.com`)。省略 *\<Server\>* 限定詞即意指本機伺服器。

\<*Queue*\> 預留位置接受佇列的識別碼，如本主題的＜佇列識別碼＞一節所述。例如，您可以使用持續佇列名稱、**NextHopDomain** 值或佇列資料庫中佇列的唯一整數值。

*\<MessageInteger\>* 預留位置代表當郵件最初進入伺服器的佇列資料庫時，指派給郵件的唯一整數值。如果要將郵件傳送給需要多個佇列的多位收件者，該郵件的所有副本在佇列資料庫的所有佇列中均擁有相同的整數值。然而，您需要執行 **Get-Message** 指令程式，以在 **Identity** 或 **MessageIdentity** 內容中尋找郵件的整數值。

下表摘要列出可用來在郵件管理指令程式上與 *Identity* 參數搭配的語法。在所有值中，*\<Server\>* 是主機名稱或伺服器的 FQDN。

### 郵件識別碼格式

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Identity 參數值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>&lt;Server&gt;\&lt;Queue&gt;\&lt;MessageInteger&gt;</code> 或<code>&lt;Queue&gt;\&lt;MessageInteger&gt;</code></p></td>
<td><p>指定之伺服器或本機伺服器上特定佇列中的郵件。</p>
<p><em>&lt;MessageInteger&gt;</em> 是顯示於 <strong>Get-Message</strong>指令程式之 <strong>Identity</strong> 內容中郵件的唯一整數值。</p>
<p><em>&lt;Queue&gt;</em> 代表下列其中一個值：</p>
<ul>
<li><p><strong>持續佇列名稱</strong>   <code>Submission</code>、<code>Unreachable</code> 或 <code>Poison</code> 值。</p></li>
<li><p><strong>傳遞佇列名稱</strong>   佇列之 <strong>NextHopDomain</strong> 內容的值，實際上是佇列的名稱。此值可以是路由目的地或傳遞群組。如需詳細資訊，請參閱<a href="queues-exchange-2013-help.md">佇列</a>主題的「NextHopSolutionKey」一節。</p></li>
<li><p><strong>佇列整數</strong>   顯示於 <strong>Get-Message</strong> 或 <strong>Get-Queue</strong>指令程式之 <strong>Identity</strong> 內容中傳遞佇列或陰影佇列的唯一整數值。</p></li>
<li><p><strong>陰影佇列識別碼</strong>   陰影佇列識別碼使用 <code>Shadow\&lt;QueueInteger&gt;</code> 語法</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code>&lt;Server&gt;\*\&lt;MessageInteger&gt;</code> 或 <code>*\&lt;MessageInteger&gt;</code> 或 <code>&lt;MessageInteger&gt;</code></p></td>
<td><p>在指定伺服器或本機伺服器上，佇列資料庫之所有佇列中的所有郵件副本。</p></td>
</tr>
</tbody>
</table>


回到頁首

## 郵件篩選參數

您可以在 **Get-Message**、**Remove-Message**、**Resume-Message** 及 **Suspend-Message**指令程式上使用 *Filter* 參數來根據郵件的內容指定要檢視或管理的郵件。*Filter* 參數會建立含有比較運算子的運算式，這些運算子會將郵件作業限制為滿足篩選準則的郵件。您可以使用 `-and` 邏輯運算子指定結果必須符合的多個條件。

如需可搭配 *Filter* 參數的完整郵件內容清單，請參閱[佇列](queues-exchange-2013-help.md)。

如需可搭配 *Filter* 參數的比較運算子清單，請參閱本主題的Comparison operators to use when filtering queues or messages一節。

如需使用 *Filter* 參數來檢視及管理郵件的程序範例，請參閱[管理佇列](manage-queues-exchange-2013-help.md)。

回到頁首

## Queue 參數

*Queue* 參數只能搭配 **Get-Message** 指令程式使用。您可以使用此參數來取得特定佇列中的所有郵件，或使用萬用字元 (\*) 來取得多個佇列中的所有郵件。使用 *Queue* 參數時，請使用佇列識別碼格式 *\<Server\>*\\*\<Queue\>*，如本主題的＜佇列識別碼＞一節所述。

回到頁首

## 在篩選佇列或郵件時可使用的比較運算子

在使用 *Filter* 參數建立佇列或郵件篩選運算式時，您需要針對要比對的內容值加入比較運算子。下表顯示可以用於篩選運算式中的比較運算子，以及每個運算子的運作方式。對於所有運算子來說，比較的值不區分大小寫。

### 比較運算子

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>運算子</th>
<th>功能</th>
<th>命令介面程式碼範例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>-eq</code></p></td>
<td><p>此運算子是用來指定結果必須完全符合運算式中所提供的內容值。</p></td>
<td><p>顯示擁有「重試」狀態的所有佇列清單：</p>
<p><code>Get-Queue -Filter {Status -eq &quot;Retry&quot;}</code></p>
<p>若要顯示所有狀態為 Retry 的郵件清單：</p>
<p><code>Get-Message -Filter {Status -eq &quot;Retry&quot;}</code></p></td>
</tr>
<tr class="even">
<td><p><code>-ne</code></p></td>
<td><p>此運算子是用來指定結果必須完全符合運算式中所提供的內容值。</p></td>
<td><p>顯示擁有「作用中」狀態的所有佇列清單：</p>
<p><code>Get-Queue -Filter {Status -ne &quot;Active&quot;}</code></p>
<p>顯示擁有「作用中」狀態的所有郵件清單：</p>
<p><code>Get-Message -Filter {Status -ne &quot;Active&quot;}</code></p></td>
</tr>
<tr class="odd">
<td><p><code>-gt</code></p></td>
<td><p>此運算子是與值以整數或日期/時間表示的內容搭配使用。篩選結果只會包含所指定內容的值大於運算式所提供之值的佇列或郵件。</p></td>
<td><p>顯示目前包含超過 1000 封郵件的佇列清單：</p>
<p><code>Get-Queue -Filter {MessageCount -gt 1000}</code></p>
<p>若要顯示目前重試計數大於 3 的郵件清單：</p>
<p><code>Get-Message -Filter {RetryCount -gt 3}</code></p></td>
</tr>
<tr class="even">
<td><p><code>-ge</code></p></td>
<td><p>此運算子是與值以整數或日期/時間表示的內容搭配使用。篩選結果只會包含所指定內容的值大於或等於運算式所提供之值的佇列或郵件。</p></td>
<td><p>顯示目前包含 1000 封以上郵件的佇列清單：</p>
<p><code>Get-Queue -Filter {MessageCount -ge 1000}</code></p>
<p>若要顯示目前重試計數大於或等於 3 的郵件清單：</p>
<p><code>Get-Message -Filter {RetryCount -ge 3}</code></p></td>
</tr>
<tr class="odd">
<td><p><code>-lt</code></p></td>
<td><p>此運算子是與值以整數或日期/時間表示的內容搭配使用。篩選結果只會包含所指定內容的值小於運算式所提供之值的佇列或郵件。</p></td>
<td><p>顯示目前包含少於 1000 封郵件的佇列清單：</p>
<p><code>Get-Queue -Filter {MessageCount -lt 1000}</code></p>
<p>若要顯示 SCL 小於 6 的郵件清單：</p>
<p><code>Get-Message -Filter {SCL -lt 6}</code></p></td>
</tr>
<tr class="even">
<td><p><code>-le</code></p></td>
<td><p>此運算子是與值以整數或日期/時間表示的內容搭配使用。篩選結果只會包含所指定內容的值小於或等於運算式所提供之值的佇列或郵件。</p></td>
<td><p>顯示目前包含 1000 封以下郵件的佇列清單：</p>
<p><code>Get-Queue -Filter {MessageCount -le 1000}</code></p>
<p>若要顯示 SCL 小於或等於 6 的郵件清單：</p>
<p><code>Get-Message -Filter {SCL -le 6}</code></p></td>
</tr>
<tr class="odd">
<td><p><code>-like</code></p></td>
<td><p>此運算子是與值以字串表示的內容搭配使用。篩選結果只會包含所指定內容的值含有運算式所提供之文字字串的佇列或郵件。您可以將 (*) 萬用字元包含在會套用到文字字串欄位 (而非列舉類型欄位) 的 <strong>-like</strong> 運算式中。</p></td>
<td><p>顯示目的地是任何以 Contoso.com 為結尾之 SMTP 網域的傳遞佇列清單：</p>
<p><code>Get-Queue -Filter {Identity -like &quot;*contoso.com&quot;}</code></p>
<p>若要顯示主旨中含有 &quot;payday loan&quot; 等文字的郵件清單：</p>
<p><code>Get-Messages -Filter {Subject -like &quot;*payday loan*&quot;}</code></p></td>
</tr>
</tbody>
</table>


您可以使用 **-and** 比較運算子來指定評估多個運算式的篩選。佇列或郵件必須滿足篩選的所有條件才能包含在結果中。

此範例會顯示目的地是任何以 Contoso.com 為結尾的 SMTP 網域名稱而且目前包含超過 500 封郵件之佇列的清單。

    Get-Queue -Filter {Identity -like "*contoso.com*" -and MessageCount -gt 500}

此範例會顯示從 contoso.com 網域中任何電子郵件地址傳送且 SCL 大於 5 之郵件的清單。

    Get-Message -Filter {FromAddress -like "*Contoso.com*" -and SCL -gt 5}

回到頁首

## 進階分頁參數

視目前的郵件流程而定，向佇列及郵件進行的查詢可能會傳回很大的一組物件。您可以使用進階分頁參數來控制查詢結果的擷取及顯示方式。

使用命令介面檢視佇列及這些佇列中的郵件時，您的查詢一次會擷取一頁的資訊。進階分頁參數會控制結果集的大小，而且可以用來排序結果。所有進階分頁參數都是選用的，而且可以與任何一個參數集一起使用，而這些參數集可與 **Get-Queue** 及 **Get-Message** 指令程式搭配使用。如果未指定任何進階分頁參數，則查詢會以識別碼的遞增順序傳回結果。

指定排序順序時，預設一律會包含郵件識別碼內容，且會用遞增順序排序該內容。這是預設順序關係。因為其他可以用排序順序包含的內容不是唯一的，所以會包含郵件識別碼內容。在排序順序中明確包含郵件識別碼內容，就可以指定結果以遞減順序排序顯示郵件識別碼。

您可以使用 *BookmarkIndex* 和 *BookmarkObject* 參數，標出排序結果集中的位置。如果書籤物件在擷取下一頁的結果時已不復存在，則預設順序關係會確定結果集會從與書籤最近的物件開始。最近的物件則取決於指定的排序順序。

下表描述進階分頁參數。

### 進階分頁參數

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
<td><p><em>BookmarkIndex</em></p></td>
<td><p>此參數指定在結果集中開始顯示結果的位置。此參數的值是總結果集中以 1 為基礎的索引。如果值小於或等於零，則會傳回第一個完整的結果頁面。如果值設為 <code>Int.MaxValue</code>，則會傳回最後一個完整的結果頁面。</p></td>
</tr>
<tr class="even">
<td><p><em>BookmarkObject</em></p></td>
<td><p>此參數指定在結果集中開始顯示結果的物件。如果指定書籤物件，則會將該物件當成搜尋開始點。會擷取該物件之前或之後的列 (取決於 <em>SearchForward</em> 參數的值)。不能在單一查詢中一起使用 <em>BookmarkObject</em> 參數與 <em>BookmarkIndex</em> 參數。</p></td>
</tr>
<tr class="odd">
<td><p><em>IncludeBookmark</em></p></td>
<td><p>此參數可以指定是否要在結果集中包含書籤物件。此值預設是設為 <code>$true</code>，而且會包含書籤物件。您可以執行查詢以限制結果大小，然後將該結果集中的最後一個項目指定為下一個查詢的書籤。在此情況下，您可能會想要將 <em>IncludeBookmark</em> 設為 <code>$false</code>，讓該物件不要包含在這兩個結果集中。</p></td>
</tr>
<tr class="even">
<td><p><em>ResultSize</em></p></td>
<td><p>此參數可以指定每頁要顯示的結果數。如果您不指定值，則會使用 1,000 個物件的預設結果大小。Exchange 會將結果集限制為 250,000 筆。</p></td>
</tr>
<tr class="odd">
<td><p><em>ReturnPageInfo</em></p></td>
<td><p>此參數是隱藏參數。它會傳回總結果數及目前頁面之第一個項目索引的相關資訊。預設值為 <code>$false</code>。</p></td>
</tr>
<tr class="even">
<td><p><em>SearchForward</em></p></td>
<td><p>此參數指定要在結果集中進行往前或往回搜尋。此參數不會影響傳回結果集的順序。它判定的是與書籤索引或物件相對的搜尋方向。如果未指定任何書籤索引或物件，則 <em>SearchForward</em> 參數會判定搜尋是從結果集中的第一個或最後一個物件處開始。</p>
<p>此參數的預設值是 <code>$true</code>。如果此參數是設為 <code>$true</code>，而且指定書籤，則查詢會從該書籤處往前進行搜尋。如果使用此組態，而在該書籤之後沒有任何結果，則查詢會傳回最後一個完整的結果頁面。</p>
<p>如果 <em>SearchForward</em> 參數是設為 <code>$false</code>，而且指定書籤，則查詢會從該書籤處往回進行搜尋。如果使用此組態，而在該書籤之後沒有完整一頁的結果，則查詢會傳回第一個完整的結果頁面。</p></td>
</tr>
<tr class="odd">
<td><p><em>SortOrder</em></p></td>
<td><p>此參數指定用來控制結果集之排序順序的郵件內容陣列。排序順序內容是指定為優先順序的遞減順序。每個內容都是以逗點隔開，並加上加號 (+) 以根據遞增順序排序，或減號 (-) 以根據遞減順序排序。</p>
<p>如果未使用此參數指定明確的排序順序，則會顯示與查詢相符的記錄，而且會根據個別物件類型的 Identity 欄位排序那些記錄。未明確指定排序順序時，結果一律會根據識別碼以遞增順序進行排序。</p></td>
</tr>
</tbody>
</table>


下列程式碼範例顯示如何在查詢中使用進階分頁參數。在此範例中，該命令會連接至指定的伺服器，並擷取內含 500 個物件的結果集。結果會以排序的順序顯示，先根據寄件者地址遞增排序，然後再根據郵件大小遞減排序。

`Get-Message -Server mailbox01.contoso.com -ResultSize 500 -SortOrder +FromAddress,-Size`

如果想要檢視後續的頁面，則可以在結果集中擷取的最後一個物件處設定書籤，並執行其他查詢。您必須使用命令介面的指令碼功能才能執行此程序。

下列範例使用指令碼來擷取第一個結果頁面、設定書籤物件、從結果集中排除書籤物件，然後在所指定的伺服器上擷取下 500 個物件。

1.  開啟命令介面，並輸入下列命令以擷取第一個結果頁面。
    
        $Results=Get-message -Server mailbox01.contoso.com -ResultSize 500 -SortOrder +FromAddress,-Size

2.  若要設定書籤物件，請輸入下列命令，以將第一頁的最後一個元素儲存至變數中。
    
        $temp=$results[$results.length-1]

3.  若要擷取所指定伺服器上的下 500 個物件，以及排除書籤物件，請輸入下列命令。
    
        Get-message -Server mailbox01.contoso.com -BookmarkObject:$temp -IncludeBookmark $False -ResultSize 500 -SortOrder +FromAddress,-Size

回到頁首

