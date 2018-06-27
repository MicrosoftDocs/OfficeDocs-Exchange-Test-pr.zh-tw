---
title: '反垃圾郵件戳記: Exchange 2013 Help'
TOCTitle: 反垃圾郵件戳記
ms:assetid: 28d3a5c2-8509-4b25-9876-763536e77c27
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa996878(v=EXCHG.150)
ms:contentKeyID: 50472750
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 反垃圾郵件戳記

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

反垃圾郵件戳記可協助您診斷套用診斷的中繼資料、 或戳記，例如寄件者相關的資訊、 拼圖驗證結果，以及內容篩選結果，郵件通過時篩選來自網際網路的內送的郵件的反垃圾郵件功能的垃圾郵件相關的問題。以下是三個反垃圾郵件戳記： 網路釣魚信賴等級戳記、 垃圾郵件信賴等級戳記，以及寄件者識別碼戳記。

您可以使用反垃圾郵件戳記作為診斷工具，判斷對使用者在信箱中接收到的誤判及可疑垃圾郵件所要採取的動作。

## 檢視反垃圾郵件戳記

您可以使用 Microsoft Outlook 檢視反垃圾郵件戳記。如需詳細資訊，請參閱[在 Outlook 中檢視反垃圾郵件戳記](view-anti-spam-stamps-in-outlook-exchange-2013-help.md)。

## 了解反垃圾郵件報告

反垃圾郵件報告是已套用至電子郵件訊息的反垃圾郵件篩選結果的摘要報告。內容篩選器代理程式適用於此戳記 x-header 表單中的郵件信封，如下所示。

    X-MS-Exchange-Organization-Antispam-Report: DV:<DATVersion>;CW:CustomList;PCL:PhishingVerdict <verdict>;P100:PhishingBlock;PP:Presolve;SID:SenderIDStatus <status>;TIME:<SendReceiveDelta>;MIME:MimeCompliance 

下表說明可以出現在反垃圾郵件報告中的篩選器資訊。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>反垃圾郵件報告只會顯示已套用至特定郵件的篩選器資訊。反垃圾郵件報告通常不會包含下表所列的所有資訊。例如，可能會收到下列反垃圾郵件報告： <code>DV:3.1.3924.1409;SID:SenderIDStatus Fail;PCL:PhishingLevel SUSPICIOUS;CW:CustomList;PP:Presolved;TIME:TimeBasedFeatures</code>。</td>
</tr>
</tbody>
</table>


### 反垃圾郵件報告中的篩選器資訊

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>戳記</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SID</p></td>
<td><p>寄件者識別碼 (SID) 戳記根據授權網域電子郵件中使用的寄件者原則架構 (SPF)。SPF <code>Received-SPF</code>以顯示在郵件信封。寄件者識別碼評估程序會產生之郵件的寄件者識別碼狀態。此狀態可以傳回為下列值之一：</p>
<ul>
<li><p><strong>Pass</strong>   IP 位址及 Purported Responsible Address (PRA) 均通過寄件者識別碼驗證檢查。</p></li>
<li><p><strong>Neutral</strong>   發佈的寄件者識別碼明確未下定論。</p></li>
<li><p><strong>Soft fail</strong>   PRA 的 IP 位址可能位於不允許的集合內。</p></li>
<li><p><strong>Fail   </strong>不允許 IP 位址；傳入的郵件中找不到 PRA，或者傳送網域不存在。</p></li>
<li><p><strong>None   </strong>寄件者的 DNS 中沒有發行的 SPF 資料。</p></li>
<li><p><strong>TempError   </strong>發生暫時的 DNS 失敗 (如 DNS 伺服器無法使用)。</p></li>
<li><p><strong>PermError   </strong>DNS 記錄無效 (如記錄格式錯誤)。</p></li>
</ul>
<p>在郵件信封中，寄件者識別碼戳記會顯示為 X 標頭 (如下所示)：</p>
<pre><code>X-MS-Exchange-Organization-SenderIdResult:&lt;status&gt;</code></pre>
<p>如需寄件者識別碼的相關資訊，請參閱<a href="sender-id-exchange-2013-help.md">寄件者識別碼</a>。</p></td>
</tr>
<tr class="even">
<td><p>DV</p></td>
<td><p>DAT 版本 (DV) 戳記可指出在掃描郵件時，使用的垃圾郵件定義檔版本。</p></td>
</tr>
<tr class="odd">
<td><p>SA</p></td>
<td><p>簽章動作 (SA) 戳記可指出因為在郵件中找到簽章，所以已復原或刪除郵件。</p></td>
</tr>
<tr class="even">
<td><p>SV</p></td>
<td><p>簽章 DAT 版本 (DV) 戳記可指出在掃描郵件時，使用的簽章檔版本。</p></td>
</tr>
<tr class="odd">
<td><p>PCL</p></td>
<td><p>網路釣魚信賴等級 (PCL) 戳記顯示分級根據其內容的郵件，並由內容篩選器代理程式處理郵件時套用。此狀態可以傳回為下列值之一：</p>
<ul>
<li><p><strong>Neutral   </strong>郵件的內容不可能是網路釣魚。</p></li>
<li><p><strong>Suspicious   </strong>郵件的內容可能是網路釣魚。</p></li>
</ul>
<p>PCL 值可介於 1 到 8。介於 1 到 3 PCL 分級會傳回<code>Neutral</code>狀態。這表示郵件內容不太可能是網路釣魚。從 4 到 8 PCL 分級會傳回<code>Suspicious</code>狀態。這表示郵件是可能是網路釣魚。</p>
<p>值會用來決定 Outlook 郵件採取的動作。Outlook 會使用 PCL 戳記来封鎖的可疑郵件內容。</p>
<p>在郵件信封中，PCL 戳記會顯示為 X 標頭 (如下所示)：</p>
<pre><code>X-MS-Exchange-Organization-PCL:&lt;status&gt;</code></pre></td>
</tr>
<tr class="even">
<td><p>SCL</p></td>
<td><p>垃圾郵件信賴等級 (SCL) 戳記的郵件顯示其內容為基礎之郵件的評等。內容篩選器代理程式會使用 Microsoft SmartScreen 技術來評估郵件的內容並指派給每個郵件的 scl。SCL 值是從 0 至 9，其中 0 會被視為較可能是垃圾郵件和 9 會被視為多可能是垃圾郵件。Exchange 與 Outlook 採取動作取決於您的 SCL 閾值設定。</p>
<p>在郵件信封中，SCL 戳記會顯示為 X 標頭 (如下所示)：</p>
<pre><code>X-MS-Exchange-Organization-SCL:&lt;status&gt;</code></pre>
<p>如需 SCL 閾值及動作的相關資訊，請參閱<a href="spam-confidence-level-threshold-exchange-2013-help.md">垃圾郵件信賴等級閾值</a>。</p></td>
</tr>
<tr class="odd">
<td><p>CW</p></td>
<td><p>郵件的自訂加權 (CW) 戳記可指出郵件包含不核准的文字或字詞，並將該不核准文字或字詞的 SCL 值 (或是加權) 套用至最終的 SCL 分數。</p>
<ul>
<li><p>不核准字詞 (或封鎖字詞) 的加權最大，而且 SCL 分數會變更為 9。</p></li>
<li><p>核准文字或字詞 (或允許字詞) 的加權最小，而且 SCL 分數會變為 0。</p></li>
</ul>
<p>如需如何將核准及不核准文字或字詞新增至內容篩選代理程式的相關資訊，請參閱<a href="manage-content-filtering-exchange-2013-help.md">管理內容篩選</a>。</p></td>
</tr>
<tr class="even">
<td><p>PP</p></td>
<td><p>Presolved 的拼圖 (PP) 戳記指出是否寄件者的郵件包含有效、 解決計算郵戳，根據 Outlook 電子郵件郵戳驗證功能，它的可能性寄件者是惡意的寄件者。在此例中的內容篩選器代理程式會減少 scl。</p>
<p>如果啟用電子郵件郵戳驗證功能，而且符合下列任一條件，則內容篩選器代理程式不會變更 SCL 分級：</p>
<ul>
<li><p>輸入郵件未包含計算的郵戳標頭。</p></li>
<li><p>計算的郵戳標頭無效。</p></li>
</ul>
<p>如需郵戳驗證功能的相關資訊，請參閱<a href="content-filtering-exchange-2013-help.md">內容篩選</a>。</p></td>
</tr>
<tr class="odd">
<td><p>TIME:TimeBasedFeatures</p></td>
<td><p>時間戳記指出所傳送之郵件的時間與收到郵件的時間之間的重大的時間延遲。時間戳記用於判斷訊息的最終的 scl。</p></td>
</tr>
<tr class="even">
<td><p>MIME:MIMECompliance</p></td>
<td><p>MIME 戳記可指出電子郵件不符合 MIME 標準。</p></td>
</tr>
<tr class="odd">
<td><p>P100:PhishingBlock</p></td>
<td><p>P100 戳記可指出郵件所含的 URL 位在網路釣魚定義檔中。</p></td>
</tr>
<tr class="even">
<td><p>IPOnAllowList</p></td>
<td><p>IPOnAllowList 戳記指出寄件者的 IP 位址的 IP 允許清單上。如需 IP 允許清單的詳細資訊，請參閱<a href="http://go.microsoft.com/fwlink/?linkid=268732">了解連線篩選</a>。</p></td>
</tr>
<tr class="odd">
<td><p>MessageSecurityAntispamBypass</p></td>
<td><p>MessageSecurityAntispamBypass 戳記可指出該郵件未篩選過內容，而且已授與寄件者權限可以略過反垃圾郵件篩選器。</p></td>
</tr>
<tr class="even">
<td><p>SenderBypassed</p></td>
<td><p>SenderBypassed 戳記指出內容篩選器代理程式不會處理從此寄件者收到的郵件的任何內容篩選。如需詳細資訊，請參閱<a href="manage-content-filtering-exchange-2013-help.md">管理內容篩選</a>。</p></td>
</tr>
<tr class="odd">
<td><p>AllRecipientsBypassed</p></td>
<td><p>AllRecipientsBypassed 戳記可指出郵件中所列的所有收件者符合下列其中一個條件：</p>
<ul>
<li><p><em>AntispamBypassedEnabled</em>參數收件者的信箱上已設為<code>$true</code>。這是您可以只將使用<strong>Set-Mailbox</strong>指令程式的管理員中的每個收件者設定。</p></li>
<li><p>郵件寄件者是收件者 Outlook 安全寄件者清單中。詳細安全的寄件者清單的相關資訊，請參閱<a href="manage-safelist-aggregation-exchange-2013-help.md">管理安全清單彙總</a>。</p></li>
<li><p>內容篩選器代理程式不會處理傳送給此收件者的郵件的篩選的任何內容。如需收件者例外狀況的詳細資訊，請參閱<a href="manage-content-filtering-exchange-2013-help.md">管理內容篩選</a>。</p></li>
</ul></td>
</tr>
</tbody>
</table>

