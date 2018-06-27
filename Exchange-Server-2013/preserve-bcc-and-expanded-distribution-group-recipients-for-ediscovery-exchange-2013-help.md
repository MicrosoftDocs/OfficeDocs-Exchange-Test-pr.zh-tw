---
title: '保留 並展開的通訊群組收件者 ediscovery （英文）: Exchange Online Help'
TOCTitle: 保留 並展開的通訊群組收件者 ediscovery （英文）
ms:assetid: eb8ddf15-0080-457e-9d83-e73e193da334
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn770225(v=EXCHG.150)
ms:contentKeyID: 62516659
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 保留 並展開的通訊群組收件者 ediscovery （英文）

 

_**適用版本：**Exchange Online, Exchange Server 2013, Office 365 Enterprise_

_**上次修改主題的時間：**2017-06-19_

就地保留、 訴訟暫止狀態、 和[Office 365 的保留原則](http://go.microsoft.com/fwlink/?linkid=827811)（在Office 365 安全規範中心中建立） 可讓您以保留信箱內容以符合法規遵循與 eDiscovery 需求。收件者的相關資訊直接定址及 \[副本\] 欄位的訊息中的所有郵件根據預設，包含但您的組織可能需要的功能來搜尋並重現相關之訊息的所有收件者的詳細資訊。這包括：

  - **解決使用之郵件的密件副本\] 欄位的收件者**  \[密件副本收件者會儲存在郵件寄件者的信箱中但不是包含在傳送給收件者的郵件標頭。

  - **展開通訊群組收件者**  因為它們是通訊群組的成員的郵件已傳送給，在 \[收件者、 中接收郵件收件者 \[副本\] 或 \[密件副本\] 欄位。

Exchange Online和Exchange Server 2013 （累計更新 7 或更新版本） 保留 \[密件副本\] 並展開的通訊群組的收件者的相關資訊。您可以使用就地 eDiscovery 搜尋中Exchange 系統管理中心 (EAC) 或安全規範中心在內容搜尋來搜尋此資訊。

## 保留 \[密件副本收件者及擴充的通訊群組的收件者的方式

如先前所述之密件副本接收者收件者的相關資訊會儲存與寄件者的信箱中的郵件。此資訊是已編製索引並可供 eDiscovery 搜尋並保留。

展開的通訊群組的收件者的相關資訊會儲存訊息之後您將信箱設為就地保留或訴訟暫止狀態。在Office 365，這項資訊也會儲存Office 365保留原則套用到信箱時。通訊群組成員資格決定在傳送郵件的時間。展開的收件者清單中儲存的郵件不會影響群組的成員資格的變更之後傳送郵件。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>資訊...]</th>
<th>會儲存在...]</th>
<th>預設儲存吗？</th>
<th>是可存取...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>若要與 [副本] 收件者</p></td>
<td><p>寄件者和收件者的信箱中的郵件內容。</p></td>
<td><p>是</p></td>
<td><p>寄件者、 收件者及規範的主管</p></td>
</tr>
<tr class="even">
<td><p>[密件副本收件者</p></td>
<td><p>在 [寄件者的信箱的郵件屬性。</p></td>
<td><p>是</p></td>
<td><p>寄件者和規範主管</p></td>
</tr>
<tr class="odd">
<td><p>展開的通訊群組的收件者</p></td>
<td><p>在 [寄件者的信箱的郵件內容。</p></td>
<td><p>[否]。展開的通訊群組收件者資訊儲存後信箱處於就地保留或訴訟資料暫留狀態，或是指派給Office 365保留原則。</p></td>
<td><p>法規遵循主管</p></td>
</tr>
</tbody>
</table>


## 搜尋 \[密件副本\] 並展開的通訊群組的收件者傳送的郵件

搜尋郵件傳送給收件者、 時 eDiscovery 搜尋結果現在包括傳送至收件者為成員的通訊群組的郵件。下表顯示出 \[密件副本\] 並展開的通訊群組的收件者傳送的郵件會傳回 eDiscovery 搜尋中的案例。

案例 1： John 是美國銷售通訊群組的成員。下表顯示 eDiscovery 搜尋結果時 Bob 將郵件傳送至 John 直接或間接透過通訊群組。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>當您搜尋 Bob 的信箱傳送的郵件...]</th>
<th>然後使用傳送郵件...</th>
<th>結果包含的郵件吗？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>若要： John</p></td>
<td><p>John 入</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>若要： John</p></td>
<td><p>美國-Sales 入</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>若要： 美國銷售</p></td>
<td><p>美國-Sales 入</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>Cc:John</p></td>
<td><p>在 [副本] John</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>Cc:John</p></td>
<td><p>在 [副本] 上的美國銷售</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>Cc:US-銷售</p></td>
<td><p>在 [副本] 上的美國銷售</p></td>
<td><p>是</p></td>
</tr>
</tbody>
</table>


案例 2： Bob 就會將電子郵件傳送至 John (以 / \[副本\]) 和取代 (密件副本直接或間接的方式透過通訊群組)。下表顯示 eDiscovery 搜尋結果。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>當您搜尋...]</th>
<th>郵件的傳送...]</th>
<th>結果包含的郵件吗？</th>
<th>附註</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Bob 的信箱</p></td>
<td><p>若要 / Cc:John</p></td>
<td><p>是</p></td>
<td><p>呈現取代已之密件副本接收者指示。</p></td>
</tr>
<tr class="even">
<td><p>Bob 的信箱</p></td>
<td><p>Bcc:Jack</p></td>
<td><p>是</p></td>
<td><p>呈現取代已之密件副本接收者指示。</p></td>
</tr>
<tr class="odd">
<td><p>Bob 的信箱</p></td>
<td><p>Bcc:Jack （透過通訊群組）</p></td>
<td><p>是</p></td>
<td><p>EDiscovery search preview、 匯出以及記錄檔中看擴充時傳送郵件之密件副本接收者通訊群組成員的清單。</p></td>
</tr>
<tr class="even">
<td><p>John 的信箱</p></td>
<td><p>若要 / Cc:John</p></td>
<td><p>是</p></td>
<td><p>[密件副本收件者並未指出。</p></td>
</tr>
<tr class="odd">
<td><p>John 的信箱</p></td>
<td><p>Bcc:Jack （直接或透過通訊群組）</p></td>
<td><p>否</p></td>
<td><p>[密件副本資訊不會儲存在傳送給收件者的郵件。您必須搜尋寄件者的信箱。</p></td>
</tr>
<tr class="even">
<td><p>取代的信箱</p></td>
<td><p>若要 / Cc:John （直接或透過通訊群組）</p></td>
<td><p>是</p></td>
<td><p>若要 / 傳遞給所有收件者的訊息中包含 [副本] 資訊。</p></td>
</tr>
<tr class="odd">
<td><p>取代的信箱</p></td>
<td><p>Bcc:Jack （直接或透過通訊群組）</p></td>
<td><p>否</p></td>
<td><p>[密件副本資訊不會儲存在傳送給收件者的郵件。您必須搜尋寄件者的信箱。</p></td>
</tr>
</tbody>
</table>


## 常見問題集

**問時間與位置是 \[密件副本收件者資訊儲存？**  
A \[密件副本收件者資訊保留原始郵件寄件者的信箱中的預設。如果 \[密件副本收件者的通訊群組、 通訊群組成員資格僅展開如果寄件者的信箱處於 \[保留或是指派給Office 365保留原則。

**問時間與位置是儲存群組收件者的擴充通訊群組清單？**  
a 群組成員資格就會跟著展開在傳送郵件的時間。展開的通訊群組成員的清單會儲存在原始郵件的寄件者的信箱。寄件者的信箱必須位於就地保留，訴訟暫止狀態，或指派給Office 365保留原則。

**問可以 \[收件者 / \[副本\] 收件者查看哪些收件者已之密件副本接收者？**  
A.\[否\]。這項資訊不包含在郵件標頭中並不可見的至 / \[副本\] 收件者。寄件者可以看到儲存在他們的信箱中儲存原始郵件的密件副本\] 欄位。搜尋寄件者的信箱時法務人員可以看到此資訊。

**問： 如何確保擴充的通訊群組的收件者一律會保留？**  
A。為確保擴充的通訊群組成員一律保留訊息、 [將所有的信箱就地保留](place-all-mailboxes-on-hold-exchange-2013-help.md)或建立全組織Office 365保留原則。

**問支援哪些類型的群組？**  
支援 a 通訊群組、 擁有郵件功能的安全群組和動態通訊群組。

**問是否有限制的通訊群組數目會跟著展開並儲存在郵件中的群組收件者吗？**  
保留 a 最多 10000 的通訊群組的成員。

**問是巢狀通訊群組支援吗？**  
A。是，展開的巢狀的通訊群組的 25 層級。

**問所在的 \[密件副本和擴充的通訊群組可見的收件者資訊吗？**  
A \[密件副本\] 並展開的通訊群組的收件者資訊時執行的 eDiscovery 搜尋就可以看到法務人員。在搜尋結果複製到探索信箱或匯出至 PST 檔案和 eDiscovery 記錄檔包含在搜尋結果中包含 \[密件副本\] 並展開的通訊群組的收件者。\[密件副本收件者資訊也是 search preview 中可用的。

**問發生什麼事通訊群組的成員會隱藏從組織的全域通訊清單 (GAL)？**  
a 該處的任何影響。如果收件者 GAL 中隱藏的他們正在仍包含的收件者展開的通訊群組清單中。

