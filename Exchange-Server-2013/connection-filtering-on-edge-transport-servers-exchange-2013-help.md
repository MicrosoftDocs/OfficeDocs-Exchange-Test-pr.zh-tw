---
title: '在 Edge Transport Server 上的連線篩選: Exchange 2013 Help'
TOCTitle: 在 Edge Transport Server 上的連線篩選
ms:assetid: b513755c-5d3e-44fa-a6cb-771d48b544ac
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124320(v=EXCHG.150)
ms:contentKeyID: 60828735
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 在 Edge Transport Server 上的連線篩選

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

連線篩選是 Microsoft Exchange Server 2013 中根據郵件來源允許或封鎖電子郵件的反垃圾郵件功能。連線篩選由只有在 Edge Transport Server 上才有的連線篩選代理程式所執行。連線篩選代理程式依賴連線郵件伺服器的 IP 位址，判斷要對輸入郵件採取的動作 (如果有的話)。

連線篩選代理程式預設是 Edge Transport Server 上第一個評估輸入郵件的反垃圾郵件代理程式。系統會根據允許和封鎖的 IP 位址來檢查 SMTP 連線的來源 IP 位址。如果來源 IP 位址受到明確允許，則郵件會傳送給組織中的收件者，不會經過其他反垃圾郵件代理程式的處理。如果來源 IP 位址明確受到封鎖，則 SMTP 連線會遭捨棄。如果來源 IP 位址未受到明確允許或封鎖，則郵件會傳經 Edge Transport Server 上的其他反垃圾郵件代理程式。

連線篩選會將來源郵件伺服器的 IP 位址比較 IP 允許清單、IP 封鎖清單、IP 允許清單提供者和 IP 封鎖清單提供者中的值。您至少需要設定這四個 IP 位址資料儲存區的其中一個，連線篩選才會運作。如果您未指定任何 IP 位址資料，則應該停用連線篩選代理程式。如需詳細資訊，請參閱 [管理 Edge Transport Server 上的連線篩選](manage-connection-filtering-on-edge-transport-servers-exchange-2013-help.md)。

**目錄**

IP Block list

IP Allow list

IP Block List providers

IP Allow List providers

Test IP Block List providers and IP Allow List providers

Configure connection filtering on Edge Transport servers that aren't directly connected to the Internet

## IP 封鎖清單

IP 封鎖清單包含您想要封鎖之電子郵件伺服器的 IP 位址。您可以手動在 IP 封鎖清單中維護 IP 位址。您可以新增個別 IP 位址或 IP 位址範圍。您可以指定任何到期時間，藉以指定要封鎖 IP 位址項目多久時間。當到期時間已到，就會停用 IP 封鎖清單中的 IP 位址項目。

如果連線篩選代理程式發現來源 IP 位址列在 IP 封鎖清單上，則會在處理郵件中的所有 **RCPT TO** 標頭 (信封收件者) 之後捨棄 SMTP 連線。

通訊協定分析代理程式的寄件者信譽功能也可以自動新增 IP 位址至 IP 封鎖清單。如需詳細資訊，請參閱 [寄件者信譽和通訊協定分析代理程式](sender-reputation-and-the-protocol-analysis-agent-exchange-2013-help.md)。

## IP 允許清單

IP 允許清單包含您想要指定作為高可信電子郵件來源之電子郵件伺服器的 IP 位址。其他 Exchange 反垃圾郵件代理程式不會處理來自 IP 允許清單中所指定郵件伺服器的電子郵件。

您可以手動在 IP 允許清單中維護 IP 位址。您可以新增個別 IP 位址或 IP 位址範圍。您可以指定任何到期時間，藉以指定要允許 IP 位址項目多久時間。當到期時間已到，就會停用 IP 允許清單中的 IP 位址項目。

回到頁首

## IP 封鎖清單提供者

IP 封鎖清單提供者常被稱為「即時封鎖清單」(簡稱 RBL)。IP 封鎖清單提供者會將傳送垃圾郵件的郵件伺服器 IP 位址編成清單。許多 IP 封鎖清單提供者也會將可能用來傳送垃圾郵件的郵件伺服器 IP 位址編成清單。範例包括被設定來進行開放式轉送的郵件伺服器、會指派動態 IP 位址的網際網路服務提供者 (ISP)，以及會允許撥號帳戶發出 SMTP 郵件伺服器流量的 ISP。

當您設定連線篩選為使用 IP 封鎖清單提供者時，連線篩選代理程式會比較連線郵件伺服器的 IP 位址與位於 IP 封鎖清單提供者那邊的 IP 位址清單。如果相符，則不允許郵件進入您的組織中。您可以設定連線篩選為使用多個 IP 封鎖清單提供者，並且指派不同的優先順序值給每個提供者。

連線篩選代理程式會在 IP 允許清單和 IP 封鎖清單檢查來源 IP 位址。如果 IP 位址完全不在這些清單上，則連線篩選代理程式會根據指派的優先順序值來查詢 IP 封鎖清單提供者。如果 IP 位址已定義於 IP 封鎖清單提供者那邊，則 Edge Transport Server 會等待收到並處理 **RCPT TO** 標頭，並使用 `SMTP 550` 錯誤來回應傳送端郵件伺服器，然後關閉連線。連線不會立即中斷，以便能夠記錄該次連線動作，而且您可能已指定不讓任何 IP 封鎖清單提供者封鎖某些收件者的郵件。

如果 IP 位址未定義於任何 IP 封鎖清單提供者那邊，則內容篩選代理程式會將郵件遞交給 Edge Transport Server 上的下一個傳輸代理程式。

針對每個 IP 封鎖清單提供者，您可以自訂封鎖郵件時傳回給寄件者的 `SMTP 550` 錯誤。您應該識別將郵件來源識別為垃圾郵件的 IP 封鎖清單提供者。如此一來，如果某個合法的來源郵件伺服器被誤認為垃圾郵件來源，系統管理員就可以連絡該 IP 封鎖清單提供者，並採取必要的步驟將郵件伺服器自 IP 封鎖清單提供者那邊移除。

IP 封鎖清單提供者可以傳回不同的代碼，來識別其清單中定義了某個 IP 位址的原因。大部分 IP 封鎖清單提供者會傳回位元遮罩或絕對值資料類型。在這些資料類型內，IP 封鎖清單提供者可以使用多個值，依威脅類型來分類 IP 位址。

使用 IP 封鎖清單提供者時需要考量一些問題：

  - IP 封鎖清單提供者服務若是發生中斷或延遲，可能會導致 Edge Transport Server 上的郵件處理延遲。您應該一律選取可靠的 IP 封鎖清單提供者。

  - 您認識的合法來源伺服器可能會被誤認為垃圾郵件來源。例如，郵件伺服器可能被意外設定成當成開放式轉送運作。您選取的 IP 封鎖清單提供者，應該一律要能就郵件的評估以及自服務中移除，提供清楚的程序。

回到頁首

## 位元遮罩和絕對值範例

本節顯示大部份封鎖清單提供者傳回之狀態碼的範例。如需提供者傳回的狀態碼詳細資訊，請參閱來自特定提供者的文件。

若是位元遮罩資料類型，IP 封鎖清單提供者服務會傳回狀態碼 127.0.0.*x*，其中整數 *x* 是下表所列的任何一個值。

### 位元遮罩資料類型的值與狀態碼

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
<th>狀態碼</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1</p></td>
<td><p>IP 位址在 IP 封鎖清單上。</p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td><p>SMTP 伺服器是設定成當成開放式轉送運作。</p></td>
</tr>
<tr class="odd">
<td><p>4</p></td>
<td><p>IP 位址支援撥接 IP 位址。</p></td>
</tr>
</tbody>
</table>


若是絕對值類型，IP 封鎖清單提供者會傳回明確的回應，其中定義其封鎖清單中定義了 IP 位址的原因。下表顯示絕對值和明確回應的範例。

### 絕對值資料類型的值與狀態碼

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
<th>明確回應</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>127.0.0.2</p></td>
<td><p>IP 位址是直接垃圾郵件來源。</p></td>
</tr>
<tr class="even">
<td><p>127.0.0.4</p></td>
<td><p>IP 位址是大量郵件寄件者。</p></td>
</tr>
<tr class="odd">
<td><p>127.0.0.5</p></td>
<td><p>傳送訊息的遠端伺服器已知可支援多階段開放式轉送。</p></td>
</tr>
</tbody>
</table>


回到頁首

## IP 允許清單提供者

IP 允許清單提供者也稱為「安全清單」或「白名單」。設定 IP 允許清單提供者的方式就像 IP 封鎖清單提供者一樣，只是結果相反：所定義的是肯定與垃圾郵件活動無關的郵件伺服器 IP 位址。如果 IP 允許清單提供者那邊已定義連線端郵件伺服器的 IP 位址，郵件就不會經過其他 Exchange 反垃圾郵件代理程式的處理。因此，使用 IP 封鎖清單提供者的頻率會遠高於 IP 允許清單提供者。請謹慎選擇您的 IP 允許清單提供者。

回到頁首

## 測試 IP 封鎖清單提供者和 IP 允許清單提供者

設定連線篩選為使用 IP 封鎖清單提供者或 IP 允許清單提供者之後，就可以執行測試，確認這些提供者正確運作中。大部分提供者都會測試 IP 位址，供您用來測試其服務。當您測試提供者時，連線篩選代理程式會發出應該會導致提供者傳回特定回應的 DNS 查詢。如需如何針對 IP 封鎖清單提供者服務或 IP 允許清單提供者服務測試 IP 位址的詳細資訊，請參閱[管理 Edge Transport Server 上的連線篩選](manage-connection-filtering-on-edge-transport-servers-exchange-2013-help.md)。

回到頁首

## 在未直接連線至網際網路的 Edge Transport Server 上設定連線篩選

您可以在未直接自網際網路接收電子郵件的 Edge Transport Server 上使用連線篩選。在此情況下，Edge Transport Server 是位於另一部直接自網際網路接收郵件並進行處理的郵件伺服器後面。例如，貴組織傳送的電子郵件流量可能會先通過反垃圾郵件的伺服器、服務或設備，然後才到達 Edge Transport Server。在此情況下，連線篩選代理程式需要從郵件中擷取正確的來源 IP 位址。為了這麼做，連線篩選代理程式需要剖析郵件標頭中的 **Received** 標頭欄位值，再將那些值拿來與位於 Edge Transport Server 與網際網路間之郵件伺服器的已知 IP 位址比較。

在傳遞路徑中每部接受和轉送 SMTP 郵件的郵件伺服器都會在郵件標頭中加上自己的 **Received** 標頭欄位。**Received** 標頭通常會包含已處理該郵件之郵件伺服器的網域名稱和 IP 位址。

如果 Edge Transport Server 不直接自網際網路接受郵件，則您需要在 Exchange 2013 Mailbox Server 上使用加上 *InternalSMTPServers* 參數的 **Set-TransportConfig** 指令程式，識別位於 Edge Transport Server 與網際網路間之郵件伺服器的 IP 位址。EdgeSync 會將 IP 位址資料複寫到 Edge Transport Server。Edge Transport Server 收到郵件時，連線篩選代理程式會假設 **Received** 標頭欄位中不符合 *InternalSMTPServers* 參數所指定值的 IP 位址是需要檢查的來源 IP 位址。因此，您需要指定所有內部 SMTP 伺服器，連線篩選才能正確運作。

回到頁首

