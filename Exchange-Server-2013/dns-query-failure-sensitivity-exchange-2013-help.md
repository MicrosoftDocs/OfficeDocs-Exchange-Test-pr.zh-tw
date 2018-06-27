---
title: 'DNS 查詢失敗敏感度: Exchange 2013 Help'
TOCTitle: DNS 查詢失敗敏感度
ms:assetid: a3c3980c-20ca-4b54-a2e6-76d49af620b4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb676467(v=EXCHG.150)
ms:contentKeyID: 52062582
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# DNS 查詢失敗敏感度

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-12-02_

在 Microsoft Exchange Server 2013 中，您可以調整 DNS 查詢敏感度，以在目的網域發生 DNS 錯誤時，能讓郵件傳遞速度稍微快一點。 不過，視 DNS 錯誤而定，這個調整在某些情況下可能會造成傳遞失敗。

## DNS 查詢及遠端郵件傳遞

負責傳遞郵件給外部收件者的 Exchange 伺服器必須能夠找到可為外部收件者接受郵件的目的郵件伺服器。 視目的地而定，郵件會放置在一或多個遠端傳遞佇列中，等候傳遞給遠端收件者。 如需傳遞佇列的相關資訊，請參閱[佇列](queues-exchange-2013-help.md)。

Exchange 伺服器會查詢設定的 DNS 伺服器，以尋找傳遞郵件所需的 DNS 記錄。 並依照列出的順序來查詢 DNS 伺服器。 如果其中一部 DNS 伺服器無法使用，查詢就會移至清單上的下一部 DNS 伺服器。 會查詢 DNS 伺服器以取得下列資訊：

  - **外部收件者網域部份的郵件交換 (MX) 記錄**   MX 記錄包含負責為網域接受郵件之郵件伺服器的完整網域名稱 (FQDN)，以及郵件伺服器的喜好設定值。 郵件伺服器的喜好設定值愈低表示優先順序愈高。 如果網域有多個 MX 記錄，就一定要有喜好設定值。 為了最佳化容錯，大多數組織都會使用多部郵件伺服器，以及有不同喜好設定值的多個 MX 記錄。

  - **目的郵件伺服器的位址 (A) 記錄**   MX 記錄中使用的每部郵件伺服器都應該有對應的 A 記錄。 A 記錄是用來尋找目的郵件伺服器的 IP 位址。 訂閱的邊際傳輸伺服器會使用 IP 位址，來開啟與目的郵件伺服器的 SMTP 連線。 雖然，技術上可以在 MX 記錄中使用正式名稱 (CNAME) 記錄的 FQDN，但這種作法會違反 RFC 974、RFC 1034、RFC 1912 及 RFC 2181，因此大多數郵件伺服器都不支援。
    
    必須組合以根 DNS 伺服器開始的反覆 DNS 查詢與遞迴 DNS 查詢，以用來將在 MX 記錄中找到的郵件伺服器 FQDN 解析成 IP 位址。

在 Exchange 2013 中，每部 DNS 伺服器的 DNS 查詢限制為 5 秒 (此限制無法設定)，而整個 DNS 查詢的限制則為 1 分鐘。

## 潛在的 DNS 問題

即使已正確設定 Exchange 伺服器上的 DNS 設定，特定網域的 DNS 記錄或是用來為特定網域尋找授權 DNS 伺服器的任何 DNS 伺服器，還是可能發生問題。 一般來說，這些問題已經超出您的控制範圍，必須由擁有這些 DNS 伺服器的各方負責解決。 這些 DNS 相關錯誤，可能是由下列一或多個狀況造成：

  - 目的網域的 DNS 記錄無效

  - DNS 伺服器使用率有問題

  - DNS 伺服器複寫有問題

在 Exchange 2013 中，當 DNS 查詢導致錯誤發生時，只有在該 DNS 伺服器未對目前查詢傳回錯誤時，才會繼續對下一部 DNS 伺服器進行查詢。

您可以透過修改 `%ExchangeInstallPath%bin\EdgeTransport.exe.config` XML 應用程式組態檔，控制 DNS 查詢失敗敏感度。 此檔案與 Microsoft Exchange 傳輸服務關聯。重新啟動 Microsoft Exchange 傳輸服務之後，就會套用您儲存至這檔案的變更。當重新啟動此服務時，會暫時中斷該伺服器上的郵件流程。 DNS 查詢失敗敏感度由 EdgeTransport.exe.config 檔中的 *DnsFaultTolerance* 機碼控制。 此機碼使用下列值：

  - **Lenient**   當 DNS 查詢遇到有效 MX 記錄與無效 MX 記錄的組合時，DNS 查詢會繼續，直到達到一分鐘的 DNS 查詢逾時值。 無效的 MX 記錄會被捨棄，而使用喜好設定值最低的有效 MX 記錄，來將郵件傳遞到目的郵件伺服器。此為預設值。

  - **Normal**   當 DNS 查詢先遇到無效的 MX 記錄時，喜好設定值大於或等於無效 MX 記錄的任何已解析 MX 記錄都會立即遭到捨棄。 會使用喜好設定值最低的其餘 MX 記錄，來將郵件傳遞到目的郵件伺服器，而不需要等到整個 DNS 查詢逾時。 雖然此行為可能會讓郵件傳遞速度變快，但如果下列狀況為真，DNS 查詢可能會沒有任何有效的 MX 記錄，則是這個行為可能會有的缺點：
    
      - 無效的 MX 記錄是目的網域的第一個 MX 記錄。
    
      - 有效的 MX 記錄與無效的 MX 記錄有相同的喜好設定值。

在 `Normal` 模式與 `Lenient` 模式中，絕不會快取無效 MX 記錄的 DNS 查詢結果。 下次執行 DNS 查詢時，將會嘗試為目的網域解析 MX 記錄。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在您安裝 Exchange 累計更新 (CU) 後，將會覆寫您在 Exchange XML 應用程式組態檔 (例如 Client Access Server 上的 web.config 檔案，或 Mailbox Server 上的 EdgeTransport.exe.config 檔案) 中任何自訂的個別伺服器設定。請務必儲存此資訊，以便安裝後能輕易地重新設定伺服器。在安裝 Exchange CU 後，您必須重新配置這些設定。</td>
</tr>
</tbody>
</table>

