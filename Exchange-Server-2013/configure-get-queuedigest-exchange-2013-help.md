---
title: '設定 Get-QueueDigest: Exchange 2013 Help'
TOCTitle: 設定 Get-QueueDigest
ms:assetid: f730c520-4ba5-4a15-8846-132bff500bb8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn505733(v=EXCHG.150)
ms:contentKeyID: 59637265
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定 Get-QueueDigest

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-12-16_

**Get-QueueDigest** Cmdlet 可讓您使用單一命令，即可檢視 Exchange 組織中的部分或全部佇例的相關資訊。

依預設，**Get-QueueDigest** Cmdlet 所傳回的會是一到二分鐘之前的結果。這些值會由下列設定控制：

  - **EdgeTransport.exe.config 中的 QueueLoggingInterval 機碼**   此機碼可指定佇列資料的記錄頻率，並可供 **Get-QueueDigest** 使用。預設值為 `00:01:00` (一分鐘)。若要指定值，請輸入時間範圍值：*hh:mm:ss*，其中 *h* = 小時數、*m* = 分鐘數，而 *s* = 秒數。依預設，此機碼不會出現在 EdgeTransport.exe.config 檔案中。

  - **Set-TransportConfig 上的 QueueDiagnosticsAggregationInterval 參數**   此參數可指定在 Mailbox Server 間共用佇列資料的頻率。預設值為 `00:01:00` (一分鐘)。若要指定值，請輸入時間範圍值：*hh:mm:ss*，其中 *h* = 小時數、*m* = 分鐘數，而 *s* = 秒數。

**QueueLoggingInterval** 機碼和 *QueueDiagnosticsAggregationInterval* 參數值的總和會決定 **Get-QueueDigest** 所傳回結果的保留天數上限。

另外，**Get-QueueDigest** 會根據佇列類型和佇列狀態傳回不同的結果。例如，下列佇列只要包含至少一個訊息便會顯示在結果中：

  - 提交佇列、無法存取之佇列及有害訊息佇列 (持續性佇列)。

  - 處於擱置狀態的傳遞佇列 (由系統管理員手動擱置的佇列)。

依預設，只有當佇列包含 10 個以上的郵件時，結果中才會傳回狀態為 \[作用中\]、\[正在連線\]、\[準備就緒\] 或 \[重試\] 的傳遞佇列。此值是由 EdgeTransport.exe.config 檔案中的 **QueueLoggingThreshold** 機碼所控制。您可以指定較小或較大的整數值。依預設，此機碼不會出現在 EdgeTransport.exe.config 檔案中。

## 開始之前有哪些須知？

  - 預估完成時間：15 分鐘

  - 若要查看在 Exchange 管理命令介面中執行 **Set-TransportConfig** 所需的 Exchange 權限，請參閱[郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「傳輸組態」項目。

  - Exchange 權限不適用於修改 EdgeTransport.exe.config 檔案以及重新啟動 Microsoft Exchange Transport 服務。在 Exchange 伺服器的作業系統中執行這些程序。

  - 在重新啟動 Microsoft Exchange Transport 服務之後，系統便會套用您在 EdgeTransport.exe.config 檔案儲存的變更。重新啟動此服務時，系統會暫時中斷該伺服器上的郵件流程。

  - 在您安裝 Exchange 累計更新 (CU) 後，將會覆寫您在 Exchange XML 應用程式組態檔 (例如 Client Access Server 上的 web.config 檔案，或 Mailbox Server 上的 EdgeTransport.exe.config 檔案) 中任何自訂的個別伺服器設定。請務必儲存此資訊，以便安裝後能輕易地重新設定伺服器。在安裝 Exchange CU 後，您必須重新配置這些設定。

  - 使用 **Set-TransportConfig** 所做的變更會影響組織中的所有 Mailbox Server。您在 EdgeTransport.exe.config 檔案中所做的變更只會影響本機 Mailbox Server。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 設定 Get-QueueDigest

1.  在 \[命令提示字元\] 視窗中執行下列命令，即可在記事本中開啟 EdgeTransport.exe.config 檔案：
    
        Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config

2.  在 `<appSettings>` 區段中新增下列一或二個機碼。
    
        <add key="QueueLoggingThreshold" value="<integer>" />
        <add key="QueueLoggingInterval" value="<hh:mm:ss>" />
    
    例如，若要將 **QueueLoggingThreshold** 值設為 1，並將 **QueueLoggingInterval** 值設為 30 秒，請使用下列值：
    
        <add key="QueueLoggingThreshold" value="1" />
        <add key="QueueLoggingInterval" value="00:00:30" />

3.  完成後，儲存並關閉 EdgeTransport.exe.config 檔案。

4.  執行下列命令，以重新啟動 Microsoft Exchange 傳輸服務：
    
        net stop MSExchangeTransport && net start MSExchangeTransport

5.  若要在 Exchange 管理命令介面中變更 *QueueDiagnosticsAggregationInterval* 參數值，請使用下列語法：
    
        Set-TransportConfig -QueueDiagnosticsAggregationInterval <hh:mm:ss>
    
    例如，若要將值變更為 30 秒，請執行下列命令：
    
        Set-TransportConfig -QueueDiagnosticsAggregationInterval 00:00:30

## 如何知道這是否正常運作？

若要驗證您是否已成功設定 **Get-QueueDigest**，請執行下列作業：

1.  驗證 EdgeTransport.exe.config 檔案中的 **QueueLoggingThreshold** 和 **QueueLoggingInterval** 機碼值。如果機碼不存在，便會使用預設值。

2.  透過執行下列命令來驗證 *QueueDiagnosticsAggregationInterval* 參數值：
    
        Get-TransportConfig | Format-List *queue*

