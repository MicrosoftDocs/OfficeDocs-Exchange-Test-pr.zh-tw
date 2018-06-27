---
title: 'Exchange 2013 的效能計數器: Exchange 2013 Help'
TOCTitle: Exchange 2013 的效能計數器
ms:assetid: 9143dd77-7c30-4769-8de1-28c717cfa9e9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn904093(v=EXCHG.150)
ms:contentKeyID: 63914489
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013 的效能計數器

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2017-02-06_

## Exchange 2013 的效能計數器

下列各節將列出您可以使用時疑難排解 Exchange 2013 的效能問題的實用的效能計數器。

## Exchange 的網域控制站連線計數器

下表顯示可接受的閾值與 Exchange 的網域控制站連線計數器的相關資訊。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>計數器</th>
<th>描述</th>
<th>閾值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MSExchange ADAccess 網域控制站 （*） \LDAP 讀取時間</p></td>
<td><p>顯示時間毫秒 (ms) 傳送 LDAP 讀取至指定的網域控制站的要求及接收回應。</p></td>
<td><p>應 50 毫秒低於平均。暴增 （最大值） 不應該是大於 100 毫秒。</p></td>
</tr>
<tr class="even">
<td><p>MSExchange ADAccess 網域控制站 （*） \LDAP 搜尋時間</p></td>
<td><p>顯示的時間 （毫秒） LDAP 搜尋要求傳送及接收回應。</p></td>
<td><p>應 50 毫秒低於平均。暴增 （最大值） 不應該是大於 100 毫秒。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange ADAccess 程序 （*） \LDAP 讀取時間</p></td>
<td><p>顯示的時間 （毫秒） 傳送 LDAP 讀取至指定的網域控制站的要求及接收回應。</p></td>
<td><p>應 50 毫秒低於平均。暴增 （最大值） 不應該是大於 100 毫秒。</p></td>
</tr>
<tr class="even">
<td><p>MSExchange ADAccess 程序 （*） \LDAP 搜尋時間</p></td>
<td><p>顯示的時間 （毫秒） LDAP 搜尋要求傳送及接收回應。</p></td>
<td><p>應 50 毫秒低於平均。暴增 （最大值） 不應該是大於 100 毫秒。</p></td>
</tr>
</tbody>
</table>


## 處理器和程序計數器

下表顯示可接受的閾值與處理器和處理程序計數器的相關資訊。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>計數器</th>
<th>描述</th>
<th>閾值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>處理器 (_Total) \ %處理器時間</p></td>
<td><p>顯示應用程式或作業系統程序執行所處理器時間百分比。這是時的處理器不閒置。</p></td>
<td><p>應小於 75%平均。</p></td>
</tr>
<tr class="even">
<td><p>處理器 (_Total) \ %使用者時間</p></td>
<td><p>顯示在使用者模式下所花費的處理器時間百分比。使用者模式是設計應用程式、 環境子系統及整合子系統限制的處理模式。</p></td>
<td><p>應小於 75%平均。</p></td>
</tr>
<tr class="odd">
<td><p>處理器 (_Total) \ %特殊權限的時間</p></td>
<td><p>顯示所需的權限模式的處理器時間百分比。權限的模式是設計用於作業系統元件和硬體操作驅動程式處理模式。允許直接存取權的硬體及所有的記憶體。</p></td>
<td><p>應小於 75%平均。</p></td>
</tr>
<tr class="even">
<td><p>系統 \ 處理器佇列長度 （所有執行個體）</p></td>
<td><p>會指出服務每個處理器的執行緒數目。處理器佇列長度可用來識別是否處理器爭用或高的 CPU 使用率由正在不足以處理指派給它的工作負載的處理器容量所造成。處理器佇列長度顯示的處理器準備就緒佇列中延遲和等候來排定執行的執行緒數目。列出的值會將最後的觀察的值位於度量單位的所需的時間。</p></td>
<td><p>不應該是大於每個處理器 5。</p></td>
</tr>
<tr class="odd">
<td><p>程序 （*） \ %處理器時間</p></td>
<td><p>可用來識別特定耗用 CPU 的程序。</p></td>
<td><p>不適用</p></td>
</tr>
</tbody>
</table>


## 記憶體計數器

下表顯示可接受的閾值與記憶體計數器的相關資訊。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>計數器</p></td>
<td><p>描述</p></td>
<td><p>閾值</p></td>
</tr>
<tr class="even">
<td><p>Memory\Available Mbytes</p></td>
<td><p>顯示實體記憶體量 (mb)，或系統使用的程序的配置立即可用。等於指定給待命 （快取） 可用的記憶體的總和及零頁面清單。記憶體管理員的完整說明，請參閱 Microsoft Developer Network (MSDN) 或 「 系統效能與疑難排解指南 》 Windows Server 2003 Resource Kit 中。</p></td>
<td><p>應保持 5%的總 RAM 上方。</p></td>
</tr>
<tr class="odd">
<td><p>Memory\%認可所使用的位元組</p></td>
<td><p>顯示 Memory\Committed 位元組的比例來 Memory\Commit 限制。認可的記憶體是實體記憶體所使用的空間已保留分頁檔案中應需要寫入至磁碟。分頁檔大小取決於認可限制。如果分頁檔放大，會增加認可限制，並減少比率。此計數器會顯示目前的百分比值僅限主動不是平均。</p></td>
<td><p>如果這個值是多個 80%，最好是系統會提供更多的記憶體壓力下可能指示。</p></td>
</tr>
</tbody>
</table>


## .NET framework 計數器

下表顯示可接受的閾值與.NET Framework 計數器的相關資訊。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>計數器</p></td>
<td><p>描述</p></td>
<td><p>閾值</p></td>
</tr>
<tr class="even">
<td><p>.NET CLR 記憶體 （*） \ GC %時間</p></td>
<td><p>顯示當發生記憶體回收。當計數器超出臨界值時，表示 CPU 會清除與不負載有效率地使用。新增至伺服器的記憶體會改善此情況。</p></td>
<td><p>應為 10%低於平均。</p></td>
</tr>
<tr class="odd">
<td><p>.NET CLR 例外狀況 （*） \ 數目 Excepts 擲回 / 秒</p></td>
<td><p>會顯示每秒擲回例外狀況的數目。包含.NET Framework 例外日期] 及 [未受管理取得轉換成.NET Framework 例外規則的例外狀況。例如，null 指標參考 （英文） unmanaged 程式碼中會取得擲回例外狀況一次以 managed 程式碼以.NET Framework System.NullReferenceException。此計數器會包含已處理和未處理的例外狀況。</p></td>
<td><p>應小於 5%的總每秒要求數目 (RPS) (網頁伺服器 (_Total) \Connection 嘗試次數/秒 *.05 上</p></td>
</tr>
<tr class="even">
<td><p>.NET CLR 記憶體 （*） \ # 中所有堆積位元組</p></td>
<td><p>顯示四個其他計數器的總和： 產生 0 堆積大小、 產生 1 堆積大小、 產生 2 堆積大小和堆積大型物件。此計數器會指出目前的記憶體配置以位元組為單位上 GC 堆積。</p></td>
<td><p>不適用</p></td>
</tr>
</tbody>
</table>


## 網路計數器

下表顯示可接受的閾值與一般網路計數器的相關資訊。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>計數器</p></td>
<td><p>描述</p></td>
<td><p>閾值</p></td>
</tr>
<tr class="even">
<td><p>網路介面 （*） \Packets 輸出錯誤</p></td>
<td><p>會指出無法傳送因發生錯誤的輸出封包的數目。</p></td>
<td><p>應該永遠為 0。</p></td>
</tr>
<tr class="odd">
<td><p>TCPv6\Connection 失敗</p></td>
<td><p>顯示目前的狀態為 [ESTABLISHED] 或 [關閉] 等候 TCP 連線數目。分頁集區的大小限制，可以建立的 TCP 連線數目。當已耗盡分頁集區時，可建立沒有新的連線。</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="even">
<td><p>TCPv4\Connections 重設</p></td>
<td><p>顯示 TCP 連線對直接轉換為封閉的狀態從 ESTABLISHED 狀態或關閉等候狀態的次數。</p></td>
<td><p>重設數目增加時或重設一致地增加時率可以指出頻寬不足。</p></td>
</tr>
<tr class="odd">
<td><p>TCPv6\Connections 重設</p></td>
<td><p>顯示的 TCP 連線對直接轉換為封閉的狀態從 ESTABLISHED 狀態或關閉等候狀態的次數。</p></td>
<td><p>重設數目增加時或重設一致地增加時率可以指出頻寬不足。</p></td>
</tr>
</tbody>
</table>


## Netlogon 計數器

下表顯示可接受的閾值與一般計數器監視 NTLM 驗證問題與 MaxConcurrentAPI 問題的相關資訊。請參閱 Microsoft 知識庫文章 2688798[如何執行效能調整使用 MaxConcurrentAPI 設定 NTLM 驗證](https://go.microsoft.com/fwlink/p/?linkid=389728)如需詳細資訊。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>計數器</p></td>
<td><p>描述</p></td>
<td><p>閾值</p></td>
</tr>
<tr class="even">
<td><p>\Netlogon\Semaphore 等候者</p></td>
<td><p>取得號誌等候的執行緒數目。</p></td>
<td><p>請參閱 Microsoft 知識庫文章 2688798<a href="https://go.microsoft.com/fwlink/p/?linkid=389728">如何執行效能調整使用 MaxConcurrentAPI 設定 NTLM 驗證</a></p></td>
</tr>
<tr class="odd">
<td><p>\Netlogon\Semaphore 宣稱</p></td>
<td><p>會保留號誌的執行緒數目。</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="even">
<td><p>\Netlogon\Semaphore 取得</p></td>
<td><p>透過 _Total 的存留期的安全性通道連線，或自系統啟動取得號誌總次數。</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="odd">
<td><p>\Netlogon\Semaphore 逾時</p></td>
<td><p>號誌等待的 _Total 安全性通道連線，或是自系統啟動存留期的執行緒已逾時它的總次數。</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="even">
<td><p>\Netlogon\Average 號誌保留時間</p></td>
<td><p>平均時間 （以秒為單位） 號誌保留透過在最後一個範例。</p></td>
<td><p>不適用</p></td>
</tr>
</tbody>
</table>


## 資料庫計數器

下表顯示使用中記錄 I/O 延遲需求計數器和其可接受的閾值。當已超出臨界值時，而且會降低用戶端體驗。例如，使用者可能會遇到郵件傳遞延遲或慢速系統效能。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>一般儲存體延遲指導 in Exchange 2013 是非常類似的指引從 Exchange 2010。其他資料庫計數器可以在<a href="https://go.microsoft.com/fwlink/p/?linkid=525622">信箱伺服器計數器</a>中找到。</td>
</tr>
</tbody>
</table>



<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>計數器</p></td>
<td><p>描述</p></td>
<td><p>閾值</p></td>
</tr>
<tr class="even">
<td><p>MSExchange 資料庫 = = &gt; 執行個體 （*） \I/O 資料庫讀取 （附加） 的平均延遲</p></td>
<td><p>會顯示每個資料庫的讀取作業的平均毫秒 (ms) 的時間長度。</p></td>
<td><p>應小於 20ms年平均。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange 資料庫 = = &gt; 執行個體 （*） \I/O 資料庫寫入次數 （附加） 的平均延遲</p></td>
<td><p>顯示每個資料庫寫入作業的平均時間長度 (毫秒)。</p></td>
<td><p>應小於 50ms年平均。</p></td>
</tr>
<tr class="even">
<td><p>MSExchange 資料庫 = = &gt; 執行個體 （*） \I/O 記錄檔寫入的平均延遲</p></td>
<td><p>顯示毫秒，每個記錄檔寫入作業的平均時間長度。</p></td>
<td><p>應小於 10 毫秒平均。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange 資料庫 = = &gt; 執行個體 （*） \I/O 資料庫讀取 （修復） 平均延遲</p></td>
<td><p>顯示毫秒，每個被動資料庫的讀取作業的平均時間長度。</p></td>
<td><p>應小於 200ms年平均。</p></td>
</tr>
<tr class="even">
<td><p>MSExchange 資料庫 = = &gt; 執行個體 （*） \I/O 資料庫寫入次數 （修復） 平均延遲</p></td>
<td><p>顯示毫秒，每個被動資料庫寫入作業的平均時間長度。</p></td>
<td><p>應小於之相同的執行個體的讀取延遲是透過 MSExchange 資料庫所衡量 = = &gt; 執行個體 （*） \I/O 資料庫讀取 （修復） 平均延遲效能計數器。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange 資料庫 = = &gt; 執行個體 （*） \I/O 資料庫讀取次數 （附加） 秒</p></td>
<td><p>顯示讀取作業每秒每個附加的資料庫執行個體的資料庫數目。</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="even">
<td><p>MSExchange 資料庫 = = &gt; 執行個體 （*） \I/O 資料庫寫入次數 （附加） / 秒</p></td>
<td><p>顯示每秒每個附加的資料庫執行個體的資料庫寫入作業的數目。</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange 資料庫 = = &gt; 執行個體 （*） \I/O 記錄檔寫入次數/秒</p></td>
<td><p>顯示每秒每個資料庫執行個體寫入記錄檔的數目。</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="even">
<td><p>MSExchange Active Manager (_total) \Database 裝載</p></td>
<td><p>在伺服器上會顯示使用中資料庫副本的數目。</p></td>
<td><p>不適用</p></td>
</tr>
</tbody>
</table>


## ASP.NET

下表顯示可接受的閾值與 ASP.NET 計數器的相關資訊。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>計數器</p></td>
<td><p>描述</p></td>
<td><p>閾值</p></td>
</tr>
<tr class="even">
<td><p>ASP.NET\Application 重新啟動</p></td>
<td><p>顯示已在網頁伺服器的存留期間重新啟動應用程式的次數。</p></td>
<td><p>應該永遠為 0。</p></td>
</tr>
<tr class="odd">
<td><p>ASP.NET\Worker 程序重新啟動</p></td>
<td><p>在電腦上顯示的工作者處理序重新啟動的次數。</p></td>
<td><p>應該永遠為 0。</p></td>
</tr>
<tr class="even">
<td><p>ASP.NET\Request 等候時間</p></td>
<td><p>在佇列中顯示最新的要求等候的毫秒的數。</p></td>
<td><p>應該永遠為 0。</p></td>
</tr>
<tr class="odd">
<td><p>應用程式佇列中的 ASP.NET 應用程式 （*） \Requests</p></td>
<td><p>應用程式要求佇列中顯示要求的數目。</p></td>
<td><p>應該永遠為 0。</p></td>
</tr>
<tr class="even">
<td><p>ASP.NET 應用程式 （*） \Requests 執行</p></td>
<td><p>顯示目前執行要求的數目。</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="odd">
<td><p>ASP.NET 應用程式 （*） \Requests/Sec</p></td>
<td><p>顯示執行每秒要求數目。</p></td>
<td><p>不適用</p></td>
</tr>
</tbody>
</table>


## RPC 用戶端存取計數器

下表顯示可接受的閾值與 RPC Client Access 計數器的相關資訊。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>計數器</p></td>
<td><p>描述</p></td>
<td><p>閾值</p></td>
</tr>
<tr class="even">
<td><p>MSExchange RpcClientAccess\RPC 平均延遲</p></td>
<td><p>顯示延遲毫秒 (ms) 的過去平均 1024 封包。</p></td>
<td><p>應低於 250 毫秒。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange RpcClientAccess\RPC 要求</p></td>
<td><p>顯示目前正在處理 RPC Client Access 服務的用戶端要求數。</p></td>
<td><p>不應該是超過 40。</p></td>
</tr>
<tr class="even">
<td><p>MSExchange RpcClientAccess\Active 使用者人數</p></td>
<td><p>顯示已顯示最後一個 2 分鐘某些活動的單獨使用者人數。</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange RpcClientAccess\Connection 計數</p></td>
<td><p>顯示的用戶端總數維護的連線。</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="even">
<td><p>MSExchange RpcClientAccess\RPC 作業/秒</p></td>
<td><p>顯示率在哪些 RPC 作業發生，每秒。</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange RpcClientAccess\User 計數</p></td>
<td><p>顯示連線至服務的使用者人數。</p></td>
<td><p>不適用</p></td>
</tr>
</tbody>
</table>


## HTTP Proxy 計數器

下表顯示 HTTP Proxy 計數器的相關資訊。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>計數器</p></td>
<td><p>描述</p></td>
</tr>
<tr class="even">
<td><p>MSExchange HttpProxy （*） \MailboxServerLocator 平均延遲</p></td>
<td><p>顯示 MailboxServerLocator web 服務呼叫的平均延遲 （毫秒）。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange HttpProxy （*） \Average 驗證延遲</p></td>
<td><p>透過最後 200 個範例顯示的平均時間所花費的驗證 CA 要求。</p></td>
</tr>
<tr class="even">
<td><p>MSExchange HttpProxy （*） \Average ClientAccess 伺服器處理延遲</p></td>
<td><p>顯示 （不包括所花費的時間代理） 的 CA 處理時間的平均延遲 （毫秒） 一段的最後 200 個要求。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange HttpProxy （*） \Mailbox Server Proxy 失敗率</p></td>
<td><p>顯示連線的百分比最後 200 個範例透過相關此用戶端存取伺服器與 MBX 伺服器之間的失敗。</p></td>
</tr>
<tr class="even">
<td><p>MSExchange HttpProxy （*） \Outsanding Proxy 要求</p></td>
<td><p>顯示未完成的 proxy 並行要求數目。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange HttpProxy （*） \Proxy 要求數/秒</p></td>
<td><p>顯示每秒處理的 proxy 要求數目。</p></td>
</tr>
<tr class="even">
<td><p>MSExchange HttpProxy （*） \Requests/Sec</p></td>
<td><p>顯示每秒處理的要求數目。</p></td>
</tr>
</tbody>
</table>


## 資訊儲存庫計數器

下表顯示可接受的閾值與資訊儲存庫計數器的相關資訊。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>一般儲存體延遲指導在 Exchange 2013 是指導來從 Exchange 2010 非常類似。其他資訊儲存庫計數器可以在<a href="https://go.microsoft.com/fwlink/p/?linkid=525622">信箱伺服器計數器</a>中找到。</td>
</tr>
</tbody>
</table>



<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>計數器</p></td>
<td><p>描述</p></td>
<td><p>閾值</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeIS 存放區 （*） \RPC 要求</p></td>
<td><p>指出目前在資訊儲存庫處理程序內執行的整體 RPC 要求。</p></td>
<td><p>應該永遠低於 70。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeIS 用戶端類型 （*） \RPC 平均延遲</p></td>
<td><p>顯示伺服器 RPC 延遲 (毫秒)，該延遲是特定用戶端通訊協定過去 1,024 個封包的平均值。</p></td>
<td><p>每個用戶端平均應該小於 50 毫秒。</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeIS 存放區 （*） \RPC 平均延遲</p></td>
<td><p>RPC 延遲平均 （毫秒） 是以毫秒為單位的每個資料庫 RPC 要求的平均延遲。平均值的計算所有 Rpc over exrpc32 載入。</p></td>
<td><p>應小於 50ms年隨時可見，與暴增小於 100ms年。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeIS 存放區 （*） \RPC 作業/秒</p></td>
<td><p>顯示每秒每個資料庫執行個體的 RPC 作業數目。</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeIS 用戶端類型 （*） \RPC 作業/秒</p></td>
<td><p>顯示每秒每個用戶端類型連接 RPC 作業數目。</p></td>
<td><p>不適用</p></td>
</tr>
</tbody>
</table>


## 用戶端存取伺服器計數器

下表顯示用戶端連線計數器和網際網路資訊服務 (IIS) 計數器的相關資訊。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>計數器</p></td>
<td><p>描述</p></td>
</tr>
<tr class="even">
<td><p>MSExchange ActiveSync\Requests/秒</p></td>
<td><p>顯示每秒透過 ASP.NET 之用戶端接收到的 HTTP 要求數。判斷目前的 Exchange ActiveSync 要求率。僅用於判斷目前的使用者負載。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange ActiveSync\Ping 命令暫止</p></td>
<td><p>顯示佇列中的目前擱置的 ping 命令。</p></td>
</tr>
<tr class="even">
<td><p>MSExchange ActiveSync\Sync 命令/秒</p></td>
<td><p>顯示每秒處理的同步處理命令數。用戶端會使用此命令來同步處理資料夾內的項目。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange 可用性 Service\Availability 要求 （秒）</p></td>
<td><p>顯示每秒提供服務的要求數目。要求可以僅針對空閒 / 忙碌資訊或包含建議。一個要求可能包含多個信箱。決定可用性服務要求發生建議的速率。</p></td>
</tr>
<tr class="even">
<td><p>MSExchange OWA\Current 單獨使用者</p></td>
<td><p>顯示目前已登入 Outlook Web app 的單獨使用者人數。此值會使只移除使用者此計數器他們登出或他們的工作階段逾時之後監視唯一作用中的使用者工作階段的數目。會判斷目前的使用者負載。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange OWA\Requests/秒</p></td>
<td><p>顯示每秒處理的 Outlook Web App 的要求數目。會判斷目前的使用者負載。</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeAutodiscover\Requests/sec</p></td>
<td><p>顯示每秒處理的自動探索服務要求數。會判斷目前的使用者負載。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeWS\Requests/sec</p></td>
<td><p>顯示每秒處理的要求數目。判斷目前的使用者負載。</p></td>
</tr>
<tr class="even">
<td><p>Web 服務 (_Total) \Current 連線</p></td>
<td><p>顯示目前建立的 Web 服務的連線數目。會判斷目前的使用者負載。</p></td>
</tr>
<tr class="odd">
<td><p>Web 服務 （預設網站） \Current 連線</p></td>
<td><p>顯示目前以對應至方式來點擊 Front End CAS 伺服器角色的連線數目的預設網站建立的連線數目。會判斷目前的使用者負載。</p></td>
</tr>
<tr class="even">
<td><p>WebService (_Total) \Connection 嘗試次數/秒</p></td>
<td><p>顯示率正在嘗試連線至 Web 服務。會判斷目前的使用者負載。</p></td>
</tr>
<tr class="odd">
<td><p>Web 服務 (_Total) \Other 要求方法/秒</p></td>
<td><p>顯示率 HTTP 要求所做的未使用的選項、 取得、 向、 文章、 放入、 DELETE、 追蹤、 移動、 複製、 MKCOL、 PROPFIND、 PROPPATCH、 搜尋、 鎖定或解除鎖定方法。會判斷目前的使用者負載。</p></td>
</tr>
</tbody>
</table>


## 工作負載管理計數器

下表會顯示 Exchange 工作負載管理計數器的相關資訊。這些計數器會監視因為工作負載管理可能在離峰時段在背景中執行的工作。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>計數器</p></td>
<td><p>描述</p></td>
</tr>
<tr class="even">
<td><p>MSExchange WorkloadManagement 工作量 （*） \ActiveTasks</p></td>
<td><p>顯示作用中工作負載管理在背景中目前正在執行的工作數目。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange WorkloadManagement 工作量 （*） \CompletedTasks</p></td>
<td><p>顯示工作負載數已完成的管理工作。</p></td>
</tr>
<tr class="even">
<td><p>MSExchange WorkloadManagement 工作量 （*） \QueuedTasks</p></td>
<td><p>顯示的工作負載目前佇列中等待處理中的管理工作。</p></td>
</tr>
</tbody>
</table>

