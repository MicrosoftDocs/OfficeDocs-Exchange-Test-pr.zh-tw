---
title: 'Edge Transport server 複製的組態: Exchange 2013 Help'
TOCTitle: Edge Transport server 複製的組態
ms:assetid: 683a6b8a-59bf-43ed-96c8-504945c2f665
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa998622(v=EXCHG.150)
ms:contentKeyID: 61180453
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Edge Transport server 複製的組態

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

Edge Transport Server 會將其組態資訊儲存在 Active Directory 輕量型目錄服務 (AD LDS) 中。您可以在周邊網路中安裝多部 Edge Transport Server，並使用 DNS 循環配置，協助平衡 Edge Transport Server 中的網路流量。循環配置是 DNS 伺服器所使用的一項簡單機制，可共用以及分配網路資源的負載。

若要確保所有 Edge Transport Server 使用相同的組態資訊，請使用提供的複製組態指令碼，在目標伺服器上複製來源伺服器的組態。

*複製組態* 用來根據已設定的來源伺服器來部署新的 Edge Transport Server。來源伺服器組態資訊即會進行複製，然後匯出至 XML 檔案。然後會將 XML 檔案匯入至目標伺服器。

本主題會提供複製的組態處理程序的概述。如需使用複製的組態設定 Edge Transport Server 的詳細步驟，請參閱[使用複製的組態設定 Edge Transport server](configure-edge-transport-server-using-cloned-configuration-exchange-2013-help.md)。

**目錄**

Cloned configuration and EdgeSync

Cloned configuration process

Transport configuration information

## 複製組態和 EdgeSync

匯入複製的組態之後，執行 EdgeSync 處理程序。若要執行收件者查閱及郵件安全性工作，Edge Transport Server 需要位於 Active Directory 中的資料。*EdgeSync* 是一組在 Exchange 2013 Mailbox Server 上執行的程序，負責建立單向收件者與組態資訊複寫，也就是從 Active Directory 複寫到 Edge Transport Server 上的 AD LDS 執行個體。EdgeSync 只會複製 Edge Transport Server 執行反垃圾郵件工作所需的資訊，以及啟用端對端郵件流程所需連接器組態的相關資訊。EdgeSync 會執行排定的更新，讓 AD LDS 資訊保持最新。

複製組態並不會複製伺服器的 Edge 訂閱設定。也不會複製 EdgeSync 所使用的憑證。您必須個別執行每個 Edge Transport Server 的 EdgeSync 處理程序。EdgeSync 會覆寫複製組態資訊和 EdgeSync 複寫資訊中所含的任何設定。這些設定包括傳送連接器、接收連接器、公認的網域，以及遠端網域。

## 複製組態程序

複製的組態處理程序由三個步驟組成：

1.  從來源伺服器匯出組態。
    
    執行 ExportEdgeConfig.ps1 指令碼 (位於 %ExchangeInstallPath%Scripts 中)，將來源伺服器的組態資訊匯出至中繼 XML 檔案。

2.  驗證目標伺服器上的組態。
    
    執行 ImportEdgeConfig.ps1 指令碼 (位於 %ExchangeInstallPath%Scripts)。此指令碼會檢查中繼 XML 檔案中的現有資訊，以查看已匯出的設定是否對目標伺服器有效，然後建立回應檔案。回應檔案指定將組態匯入至目標伺服器時所使用的伺服器特有資訊。回應檔案包含對目標伺服器無效之每個來源伺服器設定的項目。您可以修改這些設定，使其對目標伺服器有效。如果所有設定均有效，則回應檔案不會包含任何項目。

3.  在目標伺服器上匯入組態。
    
    ImportEdgeConfig.ps1 指令碼使用中繼 XML 檔案及回應檔案來複製現有的組態，或將伺服器還原至特定的組態。

## 步驟 1：從來源伺服器匯出組態

在安裝並設定 Edge Transport server role 之後，請執行 ExportEdgeConfig.ps1 指令碼 (位於 %ExchangeInsallPath%Scripts)。此指令碼會擷取來源伺服器的組態資訊，並將資訊儲存在中繼 XML 檔案中。

下列資訊是從來源伺服器匯出並儲存在中繼 XML 檔案中：

  - 傳輸服務相關資訊及記錄檔路徑資訊：
    
      - *ReceiveProtocolLogPath*
    
      - *SendProtocolLogPath*
    
      - *MessageTrackingLogPath*
    
      - *PickupDirectoryPath*
    
      - *RoutingTableLogPath*

  - 傳輸代理程式相關資訊 (包括每一個傳輸代理程式之狀態及優先順序設定)。

  - 所有傳送連接器相關資訊。如果有任何傳送連接器是設定成使用認證，則會將密碼當做加密的字串寫入中繼 XML 檔案。您可以使用 *-key* 參數搭配 ImportEdgeConfig.ps1 及 ExportEdgeConfig.ps1 指令碼，指定用於密碼加密及解密的 32 位元組字串。如果未使用 *-key* 參數，則會使用預設加密金鑰。

  - 接收連接器相關資訊。若要修改區域網路繫結及連接埠內容，您必須修改在驗證組態步驟中建立之回應檔案中的組態資訊。

  - 公認的網域組態。

  - 遠端網域組態。

  - 反垃圾郵件功能組態設定：
    
      - IP 允許清單資訊。只匯出系統管理員已手動設定的 IP 允許清單項目。
    
      - IP 封鎖清單資訊。
    
      - 內容篩選器組態。
    
      - 收件者篩選器組態。
    
      - 地址修正項目。
    
      - 附件篩選器項目。

回到頁首

## 步驟 2：驗證目標伺服器上的組態

目標伺服器是具有 Edge Transport server role 全新安裝的 Exchange 2013 伺服器。請先在目標伺服器上執行 ImportEdgeConfig.ps1 指令碼 (位於 %ExchangeInsallPath%Scripts)，以驗證中繼 XML 檔案中的現有資訊，並建立回應檔案。回應檔案指定將組態匯入至目標伺服器時所使用的伺服器特有資訊。回應檔案包含對目標伺服器無效之每個來源伺服器設定的項目。您將需要修改這些設定，使其對目標伺服器有效。如果所有設定均有效，則回應檔案不會包含任何項目。中繼 XML 檔案可以用於不同的目標伺服器。回應檔案是目標伺服器所特有的。

ImportEdgeConfig.ps1 指令碼 (位於 %ExchangeInsallPath%Scripts) 會執行下列工作：

  - 驗證是否可在目標伺服器上建立資料路徑及記錄檔路徑。如果無法建立路徑，將在回應檔案中插入空白路徑。

  - 對於 XML 檔案中的每一個傳送連接器，指令碼會在回應檔案中對來源 IP 位址新增空白項目。

  - 對於 XML 檔案中的每一個接收連接器，指令碼會在回應檔案中對區域網路連結新增空白項目。

您將需要手動修改回應檔案，才能提供下列有關伺服器特有設定的資訊：

  - 填寫資料路徑及記錄檔路徑。如果將回應檔案中的這些路徑空白，當您將組態匯入至目標伺服器時，會在下一個步驟中使用中繼 XML 檔案中所設定的路徑。

  - 對於每一個傳送連接器項目，填寫來源 IP 位址。如果此欄位空白，則匯入組態步驟會發生錯誤。

  - 對於每一個接收連接器項目，填寫區域網路連結。如果區域網路繫結空白，則嘗試將組態匯入至目標伺服器時會發生錯誤。

回到頁首

## 步驟 3：將組態匯入至目標伺服器

您可以在任何目標伺服器上執行此步驟，以複製現有 Edge Transport Server 的組態，或將伺服器還原至特定組態。執行 ImportEdgeConfig.ps1 指令碼 (位於 %ExchangeInsallPath%Scripts)，以驗證並匯入新的組態。執行此指令碼之後，目標伺服器的組態會符合中繼 XML 檔案及回應檔案中的設定。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>建議您在執行匯入組態程序之前備份現有的伺服器組態，這樣一來，如果複製作業失敗，則可以將伺服器還原至其先前的穩定狀態。</td>
</tr>
</tbody>
</table>


此步驟使用回應檔案中所提供的伺服器特有資訊。如果未在回應檔案中指定設定，則會使用中繼 XML 檔案中的資料。在指令碼修改組態之前，指令碼會驗證中繼 XML 檔案及回應檔案中的資料。

匯入組態會修改下列目標伺服器組態設定：

  - 已修改傳輸代理程式組態。

  - 移除目標伺服器上的現有連接器，並新增中繼 XML 檔案中呈現的連接器。

  - 移除現有公認的網域，並新增中繼 XML 檔案中公認的網域項目。

  - 移除現有的遠端網域，並新增中繼 XML 檔案中的遠端網域項目。

  - 移除現有的 IP 允許清單項目，並新增中繼遠端網域檔案中的 IP 允許清單項目。

  - 移除現有的 IP 封鎖清單項目，並新增中繼遠端網域檔案中的 IP 封鎖清單項目。

  - 下列反垃圾郵件組態會複製到目標伺服器：
    
      - 內容篩選器組態
    
      - 收件者篩選器組態
    
      - 地址修正項目
    
      - 附件篩選器項目

回到頁首

## 傳輸組態資訊

此傳輸組態物件的設定會為 Edge Transport Server 定義全伺服器的電子郵件傳輸設定。當您將中繼 XML 檔匯入到目標伺服器時，會匯入除了下列以外的所有傳輸組態物件設定：

  - 從匯出的 XML 檔案得到的一般名稱與建立日期

  - 傳送連接器資訊

  - 接收連接器資訊

  - 附件篩選器項目

  - **MaxDumpsterSizePerStorageGroup** 屬性項目

匯入程序完成之後，您也可以使用 **Set-TransportConfig** Cmdlet 來設定設定。如需相關資訊，請參閱 [Set-TransportConfig](https://technet.microsoft.com/zh-tw/library/bb124151\(v=exchg.150\))。

下表中的屬性是與傳輸組態物件關聯的屬性及預設值。您可以在 Mailbox Server 和 Edge Transport Server 上設定此物件。不過，許多屬性只適用於 Exchange 2013 Mailbox Server 上的傳輸服務。在 Edge Transport Server 上設定這些屬性不會造成任何影響。

### 傳輸組態屬性和預設值

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>屬性</th>
<th>描述</th>
<th>預設值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ClearCategories</strong></p></td>
<td><p>此屬性指定是否要在內容轉換期間清除 Microsoft Outlook 類別。</p></td>
<td><p>True</p></td>
</tr>
<tr class="even">
<td><p><strong>GenerateCopyOfDSNFor</strong></p></td>
<td><p>此屬性指定的傳遞狀態通知 (DSN) 代碼會將 DSN 郵件複製到郵件管理員電子郵件地址。DSN 代碼的輸入格式為 <em>x.y.z</em>，多個 DSN 代碼之間以逗號隔開。</p></td>
<td><p>5.4.8, 5.4.6, 5.4.4, 5.2.4, 5.2.0, 5.1.4</p></td>
</tr>
<tr class="odd">
<td><p><strong>InternalSMTPServers</strong></p></td>
<td><p>此屬性可指定內部 SMTP 伺服器的 IP 位址或 IP 位址範圍的清單，列出寄件者識別碼及連線篩選應忽略的 IP 位址。</p></td>
<td><p>Null</p></td>
</tr>
<tr class="even">
<td><p><strong>JournalingReportNdrTo</strong></p></td>
<td><p>此屬性指定日誌記錄信箱無法使用時，日誌報告要傳送至的電子郵件地址。此屬性不適用於 Edge Transport Server 的組態。</p></td>
<td><p>Null</p></td>
</tr>
<tr class="odd">
<td><p><strong>MaxDumpsterSizePerStorageGroup</strong></p></td>
<td><p>此屬性指定 Mailbox Server 上傳輸暫放的大小上限。此屬性不適用於 Edge Transport Server 的組態。</p></td>
<td><p>18 MB</p></td>
</tr>
<tr class="even">
<td><p><strong>MaxDumpsterTime</strong></p></td>
<td><p>此屬性指定在 Mailbox Server 的傳輸暫放中應該保留電子郵件多久時間。此屬性不適用於 Edge Transport Server 的組態。</p></td>
<td><p>7.00:00:00</p></td>
</tr>
<tr class="odd">
<td><p><strong>MaxReceiveSize</strong></p></td>
<td><p>此屬性指定組織中的收件者可以接收的郵件大小上限。此屬性不適用於 Edge Transport Server 的組態。</p></td>
<td><p>10 MB</p></td>
</tr>
<tr class="even">
<td><p><strong>MaxRecipientEnvelopeLimit</strong></p></td>
<td><p>此屬性指定單一電子郵件中允許的收件者數目上限。此屬性不適用於 Edge Transport Server 的組態。</p></td>
<td><p>5,000</p></td>
</tr>
<tr class="odd">
<td><p><strong>MaxSendSize</strong></p></td>
<td><p>此屬性指定組織中的寄件者可以傳送的郵件大小上限。此屬性不適用於 Edge Transport Server 的組態。</p></td>
<td><p>10 MB</p></td>
</tr>
<tr class="even">
<td><p><strong>TLSReceiveDomainSecureList</strong></p></td>
<td><p>此屬性指定遠端網域，這些遠端網域會透過設定來支援網域安全性的接收連接器使用相互傳輸層安全性 (TLS) 驗證。必須用逗號隔開多個網域。此屬性中所列網域不支援萬用字元 (*)。</p></td>
<td><p>Null</p></td>
</tr>
<tr class="odd">
<td><p><strong>TLSSendDomainSecureList</strong></p></td>
<td><p>此屬性指定的遠端網域，會在透過設定來支援網域安全性的傳送連接器與目標網域的位址空間傳送電子郵件時，使用相互 TLS 驗證。必須用逗號隔開多個網域。此屬性中所列網域不支援萬用字元 (*)。</p></td>
<td><p>Null</p></td>
</tr>
<tr class="even">
<td><p><strong>VerifySecureSubmitEnabled</strong></p></td>
<td><p>此屬性會驗證從信箱伺服器之信箱提交郵件的電子郵件用戶端使用的是加密的 MAPI 提交。此屬性不適用於 Edge Transport Server 的組態。此屬性的有效值為 <code>$true</code> 或 <code>$false</code>。</p></td>
<td><p>False</p></td>
</tr>
<tr class="odd">
<td><p><strong>VoicemailJournalingEnabled</strong></p></td>
<td><p>此屬性指定日誌代理程式是否會記載整合通訊語音信箱。此屬性不適用於 Edge Transport Server 的組態。</p></td>
<td><p>True</p></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>稍後若向 Exchange 組織訂閱 Edge Transport Server，則會在 EdgeSync 程序期間覆寫 <strong>InternalSMTPServers</strong> 屬性的值。如需詳細資訊，請參閱<a href="edge-subscriptions-exchange-2013-help.md">Edge 訂閱</a>。</td>
</tr>
</tbody>
</table>


回到頁首

