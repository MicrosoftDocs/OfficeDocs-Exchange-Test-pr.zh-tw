---
title: '保留期間的計算方式: Exchange Online Help'
TOCTitle: 保留期間的計算方式
ms:assetid: a7daf7aa-0411-4b26-a422-eefd1b113f9f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb430780(v=EXCHG.150)
ms:contentKeyID: 50473890
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 保留期間的計算方式

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2016-07-27_

「受管理的資料夾助理員 (MFA)」是在信箱伺服器上執行的許多*「信箱助理員」*程序之一。它的工作是處理已套用「保留原則」的信箱、將原則中包含的「保留標記」加入至信箱，以及處理信箱中的項目。如果項目有保留標記，助理員會測試這些項目的存留期。如果項目超過*「保留時間」*，則會採取指定的*「保留動作」*。保留動作包括將項目移至使用者的封存檔、刪除項目和允許復原，或永久刪除項目。

請參閱[保留標記和保留原則](retention-tags-and-retention-policies-exchange-2013-help.md)的詳細資訊。

## 決定不同項目類型的保留天數

信箱項目保留期間的計算從類似的未傳遞，但使用者所建立的項目的建立的日期草稿項目是或是傳遞的日期。管理的資料夾助理員處理信箱的項目時, 加上戳記開始日期及到期所有包含的項目保留標記與**刪除並允許復原**或**永久刪除**保留動作。已封存標記項目的也會 move date 加上戳記。

「刪除的郵件」資料夾中的項目及具有開始和結束日期的項目，例如行事曆項目 (會議和約會) 和工作，有不同於此表格中所顯示的處理方式。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>如果項目類型是…</th>
<th>且項目是…</th>
<th>則計算保留時間是根據...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>電子郵件</p></li>
<li><p>文件</p></li>
<li><p>傳真</p></li>
<li><p>日誌項目</p></li>
<li><p>會議邀請、回覆或取消</p></li>
<li><p>未接來電</p></li>
</ul></td>
<td><p>不在「刪除的郵件」資料夾中</p></td>
<td><p>傳遞日期或建立日期</p></td>
</tr>
<tr class="even">
<td><ul>
<li><p>電子郵件</p></li>
<li><p>文件</p></li>
<li><p>傳真</p></li>
<li><p>日誌項目</p></li>
<li><p>會議邀請、回覆或取消</p></li>
<li><p>未接來電</p></li>
</ul></td>
<td><p>在「刪除的郵件」資料夾中</p></td>
<td><ul>
<li><p>傳遞日期或建立日期，除非是從沒有繼承或隱含保留標記的資料夾中刪除項目。</p></li>
<li><p>如果項目所在的資料夾未套用繼承或隱含的保留標記，則不會由 MFA 來處理項目，因此沒有它所加上的開始日期。當使用者刪除這類項目時，且 MFA 在「刪除的項目」資料夾中第一次處理它，則它會標上目前的日期作為開始日期。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>行事曆</p></td>
<td><p>不在「刪除的郵件」資料夾中</p></td>
<td><ul>
<li><p>非週期性行事曆項目是否過期取決於其結束日期。</p></li>
<li><p>週期性行事曆項目是否過期取決於前次發生的結束日期。沒有結束日期的週期性行事曆項目不會過期。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>行事曆</p></td>
<td><p>在「刪除的郵件」資料夾中</p></td>
<td><ol>
<li><p>行事曆項目是否過期取決於 <code>message-received date</code> (若有的話)。</p></li>
<li><p>如果行事曆項目沒有 <code>message-received date</code>，則是否過期取決於其 <code>message-creation date</code>。</p></li>
<li><p>如果行事曆項目沒有 <code>message-received date</code>，也沒有 <code>message-creation date</code>，則不會過期。</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>工作</p></td>
<td><p>不在「刪除的郵件」資料夾中</p></td>
<td><ul>
<li><p>非週期性工作：</p>
<ol>
<li><p>非週期性工作是否過期取決於 <code>message-received date</code> (若有的話)。</p></li>
<li><p>如果非週期性工作沒有 <code>message-received date</code>，則是否過期取決於其 <code>message-creation date</code>。</p></li>
<li><p>如果非週期性工作沒有 <code>message-received date</code>，也沒有 <code></code><code>message-creation date</code>，則不會過期。</p></li>
</ol></li>
<li><p>週期性工作是否過期取決於其前次發生的 <code>end date</code>。如果週期性工作沒有 <code>end date</code>，則不會過期。</p></li>
<li><p>重新產生的工作 (週期性工作，在工作的前一個執行個體完成之後，經過一段指定的時間就會重新產生) 不會過期。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>工作</p></td>
<td><p>在「刪除的郵件」資料夾中</p></td>
<td><ol>
<li><p>工作是否過期取決於 <code>message-received date</code> (若有的話)。</p></li>
<li><p>如果工作沒有 <code>message-received date</code>，則是否過期取決於其 <code>message-creation date</code>。</p></li>
<li><p>如果工作沒有 <code>message-received date</code>，也沒有 <code>message-creation date</code>，則不會過期。</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>Contact</p></td>
<td><p>在任何資料夾</p></td>
<td><p>連絡人未加上戳記開始日期或到期日、，讓他們正在略過受管理的資料夾助理員並不會過期。</p></td>
</tr>
<tr class="even">
<td><p>損毀</p></td>
<td><p>任何資料夾中</p></td>
<td><p>受管理的資料夾助理員會略過損毀的項目，這些項目不會過期。</p></td>
</tr>
</tbody>
</table>


## 範例


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>如果使用者...</th>
<th>資料夾的保留標記...</th>
<th>受管理的資料夾助理員...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ol>
<li><p>2013/01/26「收件匣」中收到郵件。</p></li>
<li><p>2013/2/27 刪除郵件。</p></li>
</ol>
<p></p></td>
<td><ul>
<li><p>收件匣：365 天內刪除</p></li>
<li><p>刪除的郵件：30 天內刪除</p></li>
</ul>
<p></p></td>
<td><ol>
<li><p>2013/1/26 處理「收件匣」中的郵件，標上<em>「開始日期」</em>2013/01/26 和<em>「到期日期」</em>14/01/26。</p></li>
<li><p>2013/2/27 再次於「刪除的郵件」資料夾中處理郵件。根據相同的開始日期 (01/26/2013) 重新計算到期日期。</p></li>
<li><p>由於該項目超過 30 天，因此立即到期。</p></li>
</ol></td>
</tr>
<tr class="even">
<td><ol>
<li><p>2013/01/26「收件匣」中收到郵件。</p></li>
<li><p>2013/2/27 刪除郵件。</p></li>
</ol></td>
<td><ul>
<li><p>收件匣：無 (繼承或隱含)</p></li>
<li><p>刪除的郵件：30 天內刪除</p></li>
</ul></td>
<td><ol>
<li><p>2013/02/27 在「刪除的郵件」資料夾中處理郵件，確定該項目沒有開始日期。它標上目前日期作為開始日期，標示 2013/03/27 作為到期日期。</p></li>
<li><p>該項目在 2013/3/27 到期，也就是在使用者將項目刪除或移至「刪除的郵件」資料夾後的 30 天。</p></li>
</ol></td>
</tr>
</tbody>
</table>


## 其他資訊

  - 在Exchange Online、 受管理的資料夾助理員處理信箱一次七天。這可能會導致正在最多七個到期的幾天之後到期日期戳記項目上的項目。

  - 啟用 「 保留信箱中的項目未處理的受管理的資料夾助理員直到移除保留為止。

  - 如果信箱處於「就地保留」或「訴訟暫止」狀態，則過期的項目會從收件匣中移除，但會保留在「可復原項目」資料夾中，直到信箱結束[就地保留與訴訟暫止](in-place-hold-and-litigation-hold-exchange-2013-help.md)狀態為止。

  - 在混合式部署中，內部部署和 Exchange Online 組織中必須存在相同的保留標記和保留原則，兩個組織才能一致地移動項目和使項目過期。請參閱[匯出及匯入保留標記](export-and-import-retention-tags-exchange-2013-help.md)的詳細資訊。

