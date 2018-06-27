---
title: '通訊記錄管理錯誤和事件: Exchange 2013 Help'
TOCTitle: 通訊記錄管理錯誤和事件
ms:assetid: 8bc3f5ae-403b-45af-86c1-b2fccab34e63
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb310783(v=EXCHG.150)
ms:contentKeyID: 51409225
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 通訊記錄管理錯誤和事件

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

通訊記錄管理 (MRM) 就會產生您可以檢視事件檢視器中的事件。這可讓您疑難排解並確認受管理的資料夾助理員的效能。事件檢視器來追蹤下列類型的事件依下列順序，根據重要性：

1.  錯誤事件

2.  警告事件

3.  參考事件

## MRM 錯誤與事件

下表提供您可以用來疑難排解 MRM 的事件的清單。記錄類型包括：

  - 標示為 **LogAlways** 的事件一律個別記錄。

  - 不每次時所發生任何五分鐘期間內只有一次記錄標示為**LogPeriodic**的事件。這有助於防止過多的記錄項目。

### 受管理的資料夾助理員類別中的 MRM 事件

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>事件識別碼</strong></th>
<th><strong>類別</strong></th>
<th><strong>事件類型</strong></th>
<th><strong>記錄</strong></th>
<th><strong>值或描述</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>10003</p></td>
<td><p>受管理的資料夾助理員</p></td>
<td><p>錯誤</p></td>
<td><p>LogPeriodic</p></td>
<td><p>無法取得伺服器的組態物件從Active Directory。&lt;<em>Exception details</em>&gt;。檢查網域控制站網路連線問題或不正確的 DNS 組態。</p></td>
</tr>
<tr class="even">
<td><p>10004</p></td>
<td><p>受管理的資料夾助理員</p></td>
<td><p>錯誤</p></td>
<td><p>LogAlways</p></td>
<td><p>將不會套用信箱 &lt;<em>mailbox</em>&gt; &lt;<em>folder</em>&gt; 資料夾的保留原則。受管理的資料夾助理員是無法處理的受管理的資料夾 &lt;<em>managed folder</em>&gt; 受管理內容設定 &lt;<em>content setting</em>&gt;。RetentionAction MoveToFolder 但未指定目的地資料夾。請指定目的地資料夾。</p></td>
</tr>
<tr class="odd">
<td><p>10005</p></td>
<td><p>受管理的資料夾助理員</p></td>
<td><p>錯誤</p></td>
<td><p>LogAlways</p></td>
<td><p>保留原則不會套用到信箱 &lt;<em>mailbox</em>&gt; &lt;<em>folder</em>&gt; 資料夾。無法處理的受管理的資料夾 &lt;<em>managed folder</em>&gt; 受管理的內容設定 &lt;<em>content setting</em>&gt;。RetentionAction MoveToFolder 但目的地資料夾 &lt;<em>folder</em>&gt; 是來源資料夾 &lt;<em>folder</em>&gt; 相同。請指定不同的來源資料夾目的地資料夾。</p></td>
</tr>
<tr class="even">
<td><p>10009</p></td>
<td><p>受管理的資料夾助理員</p></td>
<td><p>錯誤</p></td>
<td><p>LogAlways</p></td>
<td><p>受管理的資料夾助理員會略過因為無法讀取的稽核記錄參數從Active Directory處理本機伺服器上的所有資料庫。它會在 [排程] 視窗中稍後再試。目前的資料庫： &lt;<em>database</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>10010</p></td>
<td><p>受管理的資料夾助理員</p></td>
<td><p>錯誤</p></td>
<td><p>LogAlways</p></td>
<td><p>受管理的資料夾助理員會略過處理本機伺服器上的所有資料庫因為稽核記錄已啟用但Active Directory中遺漏的稽核記錄檔的路徑。它會在 [排程] 視窗中稍後再試。目前的資料庫： &lt;<em>database</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>10011</p></td>
<td><p>受管理的資料夾助理員</p></td>
<td><p>錯誤</p></td>
<td><p>LogAlways</p></td>
<td><p>受管理的資料夾助理員可能不需設定稽核記錄。它會停止處理目前的資料庫： '%1'。它會在 [排程] 視窗中稍後再試。例外狀況詳細資料： &lt;<em>details</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>10012</p></td>
<td><p>受管理的資料夾助理員</p></td>
<td><p>錯誤</p></td>
<td><p>LogAlways</p></td>
<td><p>受管理的資料夾助理員並未寫入稽核記錄。它會停止處理目前的資料庫： &lt;<em>database</em>&gt;。它會嘗試寫入至稍後再在 [排程] 視窗中的稽核記錄。例外狀況詳細資料： &lt;<em>details</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>10017</p></td>
<td><p>受管理的資料夾助理員</p></td>
<td><p>錯誤</p></td>
<td><p>LogAlways</p></td>
<td><p>時發生例外狀況中受管理的資料夾助理員處理信箱 ︰ &lt;<em>mailbox</em>&gt; 資料夾 ︰ 名稱： &lt;<em>folder name</em>&gt; Id: &lt;<em>folder ID</em>&gt; 項目： Id: &lt;<em>IDs</em>&gt;。例外狀況 ︰ &lt;<em>exception</em>&gt;。</p></td>
</tr>
</tbody>
</table>


### 助理員類別中的 MRM 事件

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>事件識別碼</strong></th>
<th><strong>類別</strong></th>
<th><strong>事件類型</strong></th>
<th><strong>記錄</strong></th>
<th><strong>值或描述</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>9004</p></td>
<td><p>助理員</p></td>
<td><p>警告</p></td>
<td><p>LogAlways</p></td>
<td><p>服務 &lt;<em>service</em>&gt;。&lt;<em>service</em>&gt; 無法處理的信箱 &lt;<em>mailbox</em>&gt;。下列例外狀況造成失敗： &lt;<em>exception</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9014</p></td>
<td><p>助理員</p></td>
<td><p>警告</p></td>
<td><p>LogAlways</p></td>
<td><p>服務 &lt;<em>service</em>&gt;。無法處理排程變更。下列例外狀況造成失敗： &lt;<em>exception</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>9017</p></td>
<td><p>助理員</p></td>
<td><p>參考</p></td>
<td><p>LogAlways</p></td>
<td><p>服務 &lt;<em>service</em>&gt;。&lt;<em>service</em>&gt; 如資料庫 &lt;<em>database</em>&gt; 正在輸入排定的時間間隔。有 &lt;<em>number</em>&gt; 信箱移轉至程序。</p></td>
</tr>
<tr class="even">
<td><p>9018</p></td>
<td><p>助理員</p></td>
<td><p>參考</p></td>
<td><p>LogAlways</p></td>
<td><p>服務 &lt;<em>service</em>&gt;。資料庫 &lt;<em>database</em>&gt; 的 &lt;<em>service</em>&gt; 正在結束已排程的時間範圍。&lt;<em>number</em>&gt; 個信箱當中已順利處理 &lt;<em>number</em>&gt; 個。&lt;<em>number</em>&gt; 個信箱由於發生錯誤已經略過。&lt;<em>number</em>&gt; 個信箱已經單獨處理。&lt;<em>number</em>&gt; 個信箱由於時間不足而未處理。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>受管理的資料夾助理員會在下次執行時從上次未完成的地方繼續處理。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="odd">
<td><p>9019</p></td>
<td><p>助理員</p></td>
<td><p>警告</p></td>
<td><p>LogPeriodic</p></td>
<td><p>服務 &lt;<em>service</em>&gt;。無法儲存資料庫 &lt;<em>database</em>&gt; &lt;<em>service</em>&gt; 的進度。（助理員無法儲存停止使其無法繼續執行有其重新啟動時）。下列例外狀況造成失敗： &lt;<em>exception</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9020</p></td>
<td><p>助理員</p></td>
<td><p>警告</p></td>
<td><p>LogAlways</p></td>
<td><p>服務 &lt;<em>service</em>&gt;。&lt;<em>assistant name</em>&gt; 無法啟動資料庫 &lt;<em>database</em>&gt;。下列例外狀況造成失敗： &lt;<em>exception</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>9021</p></td>
<td><p>助理員</p></td>
<td><p>參考</p></td>
<td><p>LogAlways</p></td>
<td><p>服務 &lt;<em>service</em>&gt;。&lt;<em>service</em>&gt; 如資料庫 &lt;<em>database</em>&gt; 正在處理的隨選要求。有 &lt;<em>number</em>&gt; 信箱移轉至程序。</p></td>
</tr>
<tr class="even">
<td><p>9022</p></td>
<td><p>助理員</p></td>
<td><p>參考</p></td>
<td><p>LogAlways</p></td>
<td><p>服務 &lt;<em>service</em>&gt;。資料庫 &lt;<em>database</em>&gt; 的 &lt;<em>service</em>&gt; 已完成點播要求。&lt;<em>number</em>&gt; 個信箱中有 &lt;<em>number</em>&gt; 個已順利處理完畢。&lt;<em>number</em>&gt; 個信箱由於發生錯誤已經略過。</p></td>
</tr>
<tr class="odd">
<td><p>9023</p></td>
<td><p>助理員</p></td>
<td><p>警告</p></td>
<td><p>LogAlways</p></td>
<td><p>服務 &lt;<em>service</em>&gt;。&lt;<em>service</em>&gt; 無法在資料庫 &lt;<em>database</em>&gt; 開始時間] 視窗處理程序。下列例外狀況造成失敗： &lt;<em>exception</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9025</p></td>
<td><p>助理員</p></td>
<td><p>參考</p></td>
<td><p>LogAlways</p></td>
<td><p>服務 &lt;<em>service</em>&gt;。&lt;<em>service</em>&gt; 忽略 &lt;<em>number</em>&gt; 信箱資料庫 &lt;<em>database</em>&gt; 上。信箱 ︰ &lt;<em>mailboxes</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>9026</p></td>
<td><p>助理員</p></td>
<td><p>警告</p></td>
<td><p>LogAlways</p></td>
<td><p>服務 &lt;<em>service</em>&gt;。&lt;<em>service</em>&gt; 無法啟動隨選處理資料庫 &lt;<em>database</em>&gt; 上。下列例外狀況造成失敗： &lt;<em>exception</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9027</p></td>
<td><p>助理員</p></td>
<td><p>錯誤</p></td>
<td><p>LogAlways</p></td>
<td><p>服務 &lt;<em>service</em>&gt;。&lt;<em>service</em>&gt; 造成終止 &lt;<em>number</em>&gt; 次數 &lt;<em>database</em>&gt; 入處理信箱 &lt;<em>mailbox</em>&gt; 時的程序。這個信箱不會再將處理要求的時間間隔或隨選要求中。下列例外狀況造成失敗： &lt;<em>exception</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>9028</p></td>
<td><p>助理員</p></td>
<td><p>警告</p></td>
<td><p>LogAlways</p></td>
<td><p>服務 &lt;<em>service</em>&gt;。&lt;<em>service</em>&gt; 造成終止 &lt;<em>number</em>&gt; 次數 &lt;<em>database</em>&gt; 入處理信箱 &lt;<em>mailbox</em>&gt; 時的程序。下列例外狀況造成失敗： &lt;<em>exception</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9033</p></td>
<td><p>助理員</p></td>
<td><p>警告</p></td>
<td><p>LogAlways</p></td>
<td><p>服務 &lt;<em>service</em>&gt;。&lt;<em>service</em>&gt; 如資料庫 &lt;<em>database</em>&gt; 接收到的隨選要求。但有未處理的信箱。</p></td>
</tr>
<tr class="odd">
<td><p>9034</p></td>
<td><p>助理員</p></td>
<td><p>參考</p></td>
<td><p>LogAlways</p></td>
<td><p>服務 &lt;<em>service</em>&gt; 已終止對資料庫 &lt;<em>database</em>&gt; 的受管理的資料夾助理員執行以時間為基礎的作業。</p></td>
</tr>
<tr class="even">
<td><p>9035</p></td>
<td><p>助理員</p></td>
<td><p>警告</p></td>
<td><p>LogAlways</p></td>
<td><p>服務 &lt;<em>service</em>&gt;。&lt;<em>assistant name</em>&gt; 無法處理 &lt;<em>number</em>&gt; 個信箱，因為時間不夠。</p></td>
</tr>
<tr class="odd">
<td><p>9037</p></td>
<td><p>助理員</p></td>
<td><p>錯誤</p></td>
<td><p>LogAlways</p></td>
<td><p>服務 &lt;<em>service</em>&gt;。處理 RPC 時發生例外狀況。方法： &lt;<em>method</em>&gt; 例外狀況 ︰ &lt;<em>exception</em>&gt;</p></td>
</tr>
</tbody>
</table>

