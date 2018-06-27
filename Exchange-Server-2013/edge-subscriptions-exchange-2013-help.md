---
title: 'Edge 訂閱: Exchange 2013 Help'
TOCTitle: Edge 訂閱
ms:assetid: 3addd71a-4165-401f-a009-002bcd8baba6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa997438(v=EXCHG.150)
ms:contentKeyID: 61180451
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Edge 訂閱

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

Edge Transport Server 可處理所有與網際網路相關的郵件流程，並且為您的 Exchange 組織提供 SMTP 轉送和智慧主機服務，而將攻擊面減到最小。更深入的郵件保護和安全性，則由組織周邊網路中的 Edge Transport Server 上執行的一系列代理程式所提供。這些代理程式支援的功能會提供對病毒和垃圾郵件的防護，並且套用傳輸規則以控制郵件流程。

Edge 訂閱可在 Edge Transport Server 上的 Active Directory 輕量型目錄服務 (AD LDS) 執行個體中，填入 Active Directory 資料。雖然可以選擇是否要建立 Edge 訂閱，但讓 Exchange 組織訂閱 Edge Transport Server，將可簡化管理工作並增強反垃圾郵件功能。如果您計劃使用收件者查閱或安全清單彙總，或是要利用相互傳輸層安全性 (MTLS) 來保護與夥伴網域間的 SMTP 通訊安全，您必須建立 Edge 訂閱。

**目錄**

Edge Subscription Process

Microsoft Exchange EdgeSync Service

Managing Edge Subscriptions

## Edge 訂閱程序

Edge Transport Server 沒有 Active Directory 的直接存取權。Edge Transport Server 用以處理郵件的組態和收件者資訊，都儲存在本機的 AD LDS 中。建立 Edge 訂閱，可以將資訊安全而自動地從 Active Directory 複寫至 AD LDS。Edge 訂閱程序會提供認證，用以在 Exchange 2013 信箱伺服器與已訂閱的 Edge Transport Server 之間建立安全的 LDAP 連線。在信箱伺服器上執行的 Microsoft Exchange EdgeSync 服務 (EdgeSync) 會定期執行單向同步處理，將最新的資料傳輸至 AD LDS。這可以讓您設定信箱伺服器，然後將這些資訊同步處理至 Edge Transport Server，而減少您所需執行的管理工作。

您可以讓負責對 Edge Transport Server 傳輸及接收郵件的信箱伺服器所在的 Active Directory 站台訂閱 Edge Transport Server。Edge 訂閱程序會建立 Edge Transport Server 的 Active Directory 站台成員資格聯盟。站台聯盟可讓 Exchange 組織中的信箱伺服器將郵件轉送至 Edge Transport Server，以傳遞到網際網路，而不必設定明確的傳送連接器。

單一 Active Directory 站台可以訂閱一或多部 Edge Transport Server。但多個 Active Directory 站台無法訂閱同一部 Edge Transport Server。如果您已部署多部 Edge Transport Server，每部伺服器可訂閱至不同的 Active Directory 站台。每一個 Edge Transport Server 都需要個別的 Edge 訂閱。

若要部署 Edge Transport Server 並將其訂閱至 Active Directory 站台，請遵循下列步驟：

1.  安裝 Edge Transport server role。

2.  請確認信箱伺服器與 Edge Transport Server 可以使用 DNS 名稱解析找到彼此。

3.  在信箱伺服器上，設定要複寫到 Edge Transport Server 的物件和設定。

4.  在 Edge Transport Server 上，建立並匯出 Edge 訂閱檔案。

5.  將 Edge 訂閱檔案複製到信箱伺服器，或複製到可從您信箱伺服器所在的 Active Directory 站台存取的檔案共用。

6.  將 Edge 訂閱檔案匯入至 Active Directory 站台。

## 建立新的 Edge 訂閱時所將發生的情況

當您建立 Edge 訂閱檔案 (在 Edge Transport Server 上執行 **New-EdgeSubscription** 指令程式) 時，將會執行下列動作：

  - 建立名為 EdgeSync 開機複寫帳戶 (ESBRA) 的 AD LDS 帳戶。這些 ESBRA 認證可用來驗證對 Edge Transport Server 的第一個 EdgeSync 連線。此帳戶依設定會在建立後的 24 小時到期。因此，您必須在 24 小時內完成前一節中說明的六步驟訂閱程序。如果 ESBRA 在完成 Edge 訂閱程序前即到期，您將必須重新執行 **New-EdgeSubscription** 指令程式，以建立新的 Edge 訂閱檔案。

  - 從 AD LDS 擷取 ESBRA 認證並寫入 Edge 訂閱檔案中。Edge Transport Server 自我簽署憑證的公開金鑰也會一併匯出到 Edge 訂閱檔案。寫入至 Edge 訂閱檔案的認證只適用於先前匯出檔案的伺服器。

  - 任何先前在 Edge Transport Server 上建立、而現在即將從 Active Directory 複寫至 AD LDS 的組態物件，都會從 AD LDS 中刪除，且用以設定這些物件的 Exchange 管理命令介面指令程式將會停用。但您仍可使用 **Get-\*** 指令程式來檢視這些物件。執行 **New-EdgeSubscription** 指令程式時，會在 Edge Transport Server 上停用下列的指令程式：
    
      - **Set-SendConnector**
    
      - **New-SendConnector**
    
      - **Remove-SendConnector**
    
      - **New-AcceptedDomain**
    
      - **Set-AcceptedDomain**
    
      - **Remove-AcceptedDomain**
    
      - **New-MessageClassification**
    
      - **Set-MessageClassification**
    
      - **Remove-MessageClassification**
    
      - **New-RemoteDomain**
    
      - **Set-RemoteDomain**
    
      - **Remove-RemoteDomain**

當您在信箱伺服器上執行 **New-EdgeSubscription** 指令程式，以在信箱伺服器上匯入 Edge 訂閱檔案時：

  - 會建立 Edge 訂閱，將 Edge Transport Server 加入 Exchange 組織中。EdgeSync 會將組態資料傳播至這部 Edge Transport Server，在 Active Directory 中建立 Edge 組態物件。

  - Active Directory 站台中的每部信箱伺服器都會接收到來自 Active Directory 的通知，告知已訂閱新的 Edge Transport Server。信箱伺服器會擷取 Edge 訂閱檔案中的 ESBRA。接著，信箱伺服器會使用 Edge Transport Server 自我簽署憑證的公開金鑰，來加密 ESBRA。然後，將加密的認證寫入 Edge 組態物件。

  - 每部信箱伺服器也會使用其本身的公開金鑰來加密 ESBRA，然後將認證儲存在本身的組態物件中。

  - 每組「Edge Transport Server-信箱伺服器」都會在 Active Directory 中建立 EdgeSync 複寫帳戶 (ESRA)。每部信箱伺服器都會將其 ESRA 認證儲存為信箱伺服器組態物件的屬性。

  - 傳送連接器會自動建立，以便將從 Edge Transport Server 輸出的郵件轉送至網際網路，以及將 Edge Transport Server 的輸入轉送至 Exchange 組織。

  - 在信箱伺服器上執行的 Microsoft Exchange EdgeSync 服務會使用 ESBRA 認證，在信箱伺服器與 Edge Transport Server 之間建立安全的 LDAP 連線，並執行資料的初始複寫。複寫到 AD LDS 的資料如下：
    
      - 拓撲資料
    
      - 組態資料
    
      - 複寫資料
    
      - ESRA 認證

  - 在 Edge Transport Server 上執行的 Microsoft Exchange 認證服務會安裝 ESRA 認證。這些認證是用來驗證同步處理連線，並保護稍後的連線安全。

  - 建立 EdgeSync 同步處理排程。

接著，在已訂閱的 Active Directory 站台中的信箱伺服器上執行的 Microsoft Exchange EdgeSync 服務，會以定期排程執行從 Active Directory 到 AD LDS 的單向資料複寫。您也可以使用 **Start-EdgeSynchronization** 指令程式覆寫 EdgeSync 同步處理排程，並立即開始同步處理。

如需 ESRA 帳戶以及如何用以協助保護 EdgeSync 同步處理程序安全的詳細資訊，請參閱[Edge 訂閱認證](edge-subscription-credentials-exchange-2013-help.md)。

此範例會讓指定的站台訂閱 Edge Transport Server，並自動建立網際網路傳送連接器，以及從 Edge Transport Server 至信箱伺服器的傳送連接器。

    New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "C:\EdgeSubscriptionInfo.xml" -Encoding Byte -ReadCount 0)) -CreateInternetSendConnector $true -CreateInboundSendConnector $true -Site "Default-First-Site-Name" 

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><em>CreateInternetSendConnector</em> 和 <em>CreateInboundSendConnector</em> 參數的預設值都是 <code>$true</code>。此處的參數僅供示範之用。</td>
</tr>
</tbody>
</table>


此範例會匯出 Edge 訂閱檔案。

    New-EdgeSubscription -FileName "C:\EdgeSubscriptionInfo.xml"

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在邊際傳輸伺服器上執行 <strong>New-EdgeSubscription</strong> Cmdlet 時，會收到提示，要求您認可將停用的命令以及邊際傳輸伺服器上將被覆寫的組態。若要略過此項確認，您必須使用 <em>Force</em> 參數。此參數適用於您編寫 <strong>New-EdgeSubscription</strong> Cmdlet。<em>Force</em> 參數也用來在您重新訂閱邊際傳輸伺服器時，以您正在建立之檔案的相同名稱，覆寫現有的檔案。</td>
</tr>
</tbody>
</table>


如需詳細的語法及參數資訊，請參閱 [New-EdgeSubscription](https://technet.microsoft.com/zh-tw/library/bb123800\(v=exchg.150\))。

## 傳送在 Edge 訂閱程序期間建立的連接器

根據預設，當您將 Edge 訂閱檔案匯入至信箱伺服器以完成建議的 Edge 訂閱程序時，將會自動建立必要的傳送連接器以啟用網際網路與 Exchange 組織之間的端對端郵件流程，並刪除 Edge Transport Server 上任何現有的傳送連接器。在某些情況下，您可以選擇抑制傳送連接器的自動建立，而手動設定傳送連接器。如需手動設定傳送連接器的相關資訊，請參閱[手動設定 Edge Transport server 郵件流程](manually-configure-edge-transport-server-mail-flow-exchange-2013-help.md)和[不使用 EdgeSync 設定 Edge Transport server 到網際網路郵件流程](configure-internet-mail-flow-through-an-edge-transport-server-without-using-edgesync-exchange-2013-help.md)。

Edge 訂閱程序提供下列傳送連接器：

  - 設定成將電子郵件從 Exchange 組織轉送至網際網路的傳送連接器。

  - 設定成將電子郵件從 Edge Transport Server 轉送至 Exchange 組織的傳送連接器。

此外，將 Edge Transport Server 訂閱至 Exchange 組織，可讓已訂閱的 Active Directory 站台中的信箱伺服器使用組織內的傳送連接器將郵件轉送至這部 Edge Transport Server。

## 自動建立從網際網路接收郵件的輸入傳送連接器

根據預設，當您在信箱伺服器上執行 **New-EdgeSubscription** 指令程式時，輸入傳送連接器參數 *CreateInboundSendConnector* 會設為 `$true`。這會建立將郵件傳送至 Exchange 組織所需的傳送連接器。下表顯示此傳送連接器的組態。

### 自動輸入傳送連接器組態

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>屬性</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>EdgeSync - Inbound to &lt;<em>站台名稱</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p><em>AddressSpaces</em></p></td>
<td><p><code>SMTP:--;1</code></p>
<p>位址空間中的 <code>--</code> 值代表 Exchange 組織所有已授權和公認的內部轉送網域。Edge Transport Server 針對這些公認網域所接收的任何郵件，都會路由傳送至此傳送連接器，並轉送至智慧主機。</p></td>
</tr>
<tr class="odd">
<td><p><em>SourceTransportServers</em></p></td>
<td><p>&lt;<em>Edge 訂閱名稱</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p><em>Enabled</em></p></td>
<td><p>True</p></td>
</tr>
<tr class="odd">
<td><p><em>DNSRoutingEnabled</em></p></td>
<td><p>False</p></td>
</tr>
<tr class="even">
<td><p><em>SmartHosts</em></p></td>
<td><p><code>--</code></p>
<p>智慧主機清單中的 <code>--</code> 值，代表已訂閱的 Active Directory 站台中的所有信箱伺服器。在您建立 Edge 之後新增至已訂閱的 Active Directory 站台中的任何信箱伺服器，都不會加入 EdgeSync 同步處理程序中。但這些伺服器會自動新增至自動建立之輸入傳送連接器的智慧主機清單中。如果已訂閱的 Active Directory 站台中有多部信箱伺服器，則會讓智慧主機間的輸入連線達到負載平衡。</p></td>
</tr>
</tbody>
</table>


對於自動建立的輸入傳送連接器，您無法在建立時修改其位址空間或智慧主機清單。但您可以在建立 Edge 訂閱時，將 *CreateInboundSendConnector* 參數設為 `$false` 值。這可讓您以手動方式設定從 Edge Transport Server 到 Exchange 組織的傳送連接器。

## 自動建立將郵件傳送至網際網路的輸出傳送連接器

根據預設，當您在信箱伺服器上執行 **New-EdgeSubscription** 指令程式時，輸出傳送連接器參數 *CreateInternetSendConnector* 會設為 `$true`。這會建立將郵件傳送至網際網路所需的傳送連接器。下表顯示此傳送連接器的預設組態。

### 自動網際網路傳送連接器組態

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>屬性</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>EdgeSync - &lt;<em>站台名稱</em>&gt; to Internet</p></td>
</tr>
<tr class="even">
<td><p><em>AddressSpaces</em></p></td>
<td><p><code>SMTP:*;100</code></p></td>
</tr>
<tr class="odd">
<td><p><em>SourceTransportServers</em></p></td>
<td><p>&lt;<em>Edge 訂閱名稱</em>&gt;</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Edge 訂閱的名稱會與已訂閱 Edge Transport Server 的名稱相同。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p><em>Enabled</em></p></td>
<td><p>True</p></td>
</tr>
<tr class="odd">
<td><p><em>DNSRoutingEnabled</em></p></td>
<td><p>True</p></td>
</tr>
<tr class="even">
<td><p><em>DomainSecureEnabled</em></p></td>
<td><p>True</p></td>
</tr>
</tbody>
</table>


相同的 Active Directory 站台訂閱了多部 Edge Transport Server 時，將不會建立更多連至網際網路的傳送連接器。此時，所有 Edge 訂閱都會新增至相同的傳送連接器，作為來源伺服器。這可讓各個已訂閱的 Edge Transport Server 對網際網路的輸出連線達到負載平衡。

輸出傳送連接器依設定會使用 DNS 路由將網域名稱解析為 MX 資源記錄，以將電子郵件從 Exchange 組織傳送至所有遠端 SMTP 網域。如需以手動方式設定連接器組態的詳細資訊，請參閱[手動設定 Edge Transport server 郵件流程](manually-configure-edge-transport-server-mail-flow-exchange-2013-help.md)。

## Microsoft Exchange EdgeSync 服務

當您將 Edge Transport Server 訂閱至 Active Directory 站台後，EdgeSync 會將組態和收件者資料複寫至 Edge Transport Server。此服務會將下列資料從 Active Directory 複寫至 AD LDS：

  - 傳送連接器組態

  - 公認的網域

  - 遠端網域

  - 郵件分類

  - 安全寄件者清單

  - 封鎖的寄件者清單

  - 收件者

  - 與合作夥伴進行的網域安全通訊中所使用的傳送和接收網域清單

  - 列為組織傳輸組態內部的 SMTP 伺服器清單

  - 已訂閱的 Active Directory 站台中的信箱伺服器清單

如需複寫至 AD LDS 的資料及其使用方式的詳細資訊，請參閱[EdgeSync 複寫資料](edgesync-replication-data-exchange-2013-help.md)。

EdgeSync 會使用相互驗證及授權的安全 LDAP 通道，將資料從信箱伺服器傳輸至 Edge Transport Server。

為了將資料複寫至 AD LDS，信箱伺服器會繫結至通用類別目錄伺服器，以擷取更新的資料。EdgeSync 會透過非標準 TCP 連接埠 50636，起始信箱伺服器與訂閱的 Edge Transport Server 之間的安全 LDAP 工作階段。

當您第一次將 Edge Transport Server 訂閱至 Active Directory 站台時，將 Active Directory 中的資料填入至 AD LDS 的初始複寫約需五分鐘才能完成，時間長短視目錄服務中的資料數量而定。初始複寫之後，EdgeSync 只會同步處理新增和變更的物件，並且會移除任何已刪除的物件。

## 同步處理排程

不同類型的資料會以不同的排程來加以同步。EdgeSync 同步處理排程會指定 EdgeSync 同步處理的最大間隔。EdgeSync 同步處理的執行間隔如下：

  - 組態資料：3 分鐘。

  - 複寫資料：5 分鐘。

  - 拓撲資料：5 分鐘

如果您要變更這些間隔，請使用 **Set-EdgeSyncServiceConfig** 指令程式。在信箱伺服器上使用 **Start-EdgeSynchronization** 指令程式，可強制 Edge 訂閱同步處理覆寫下一個排定 EdgeSync 同步處理的計時器，並立即啟動 EdgeSync。

## 選取信箱伺服器

每個已訂閱的 Edge Transport Server 都會與一個 Active Directory 站台相關聯。如果站台中有多部信箱伺服器，則其中任一部信箱伺服器都可將資料複寫至已訂閱的 Edge Transport Server。在同步處理時若要避免信箱伺服器之間發生爭用的情況，請依照下列方式選取慣用的信箱伺服器：

1.  在 Active Directory 站台中，第一部執行拓撲掃描及探索新 Edge 訂閱的信箱伺服器，將會執行初始複寫。由於探索會以拓撲掃描的時間點為基礎，因此站台中的任何信箱伺服器都可能會執行初始複寫。

2.  執行初始複寫的信箱伺服器會建立 EdgeSync 租用選項，並在 Edge 訂閱上設定鎖定。租用選項會將這一部信箱伺服器建立為對該 Edge Transport Server 提供同步處理服務的慣用伺服器。鎖定可防止在另一部信箱伺服器上執行的 EdgeSync 接管租用選項。

3.  EdgeSync 租用選項可持續一小時。在這一小時中，除非啟動了手動同步處理，否則將不會有其他 EdgeSync 服務接管租賃選項。如果在啟動手動同步處理時，沒有慣用的信箱伺服器可提供 EdgeSync 服務，則在五分鐘過後就會解除鎖定，而可由另一個 EdgeSync 服務接管租用選項並執行同步處理。

4.  若未啟動手動同步處理，則會根據 EdgeSync 同步處理排程進行同步處理。如果在進行排定的同步處理時沒有慣用伺服器可供使用，則在五分鐘過後就會解除鎖定，而可由另一個 EdgeSync 服務接管租用選項並執行同步處理。

這種鎖定及租用方法，可防止 EdgeSync 服務的多個執行個體同時將資料發送至同一部 Edge Transport Server。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您在已訂閱的 Active Directory 站台中也有 Exchange 2010 或 Exchange 2007 信箱伺服器，Exchange 2013 信箱伺服器將一律具有優先權，並執行複寫。</td>
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
<td>當您將 Edge Transport Server 訂閱至 Active Directory 站台時，該 Active Directory 站台上當時已安裝的所有信箱伺服器都將可加入 EdgeSync 同步處理程序中。若移除其中一部伺服器，在其餘信箱伺服器上執行的 EdgeSync 服務仍會繼續進行資料同步程序。但若您後續又在 Active Directory 站台中安裝新的信箱伺服器，這些伺服器將不會自動加入 EdgeSync 同步處理中。如果您要讓這些新的信箱伺服器加入 EdgeSync 同步處理中，您必須重新訂閱 Edge Transport Server。</td>
</tr>
</tbody>
</table>


下表列出與鎖定和租用相關的 EdgeSync 屬性。您可以使用 **Set-EdgeSyncServiceConfig** 指令程式來設定這些內容。

### EdgeSync 租用內容

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>參數</th>
<th>預設值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>LockDuration</em></p></td>
<td><p><code>00:05:00</code> (5 分鐘)</p></td>
<td><p>此設定可決定特定 EdgeSync 服務取得鎖定的時間長短。如果信箱伺服器上保有此鎖定的 EdgeSync 服務未回應，則五分鐘過後，另一部信箱伺服器上的 EdgeSync 服務即可接管租用。強制立即進行 EdgeSync 同步處理，並不會覆寫此值。</p></td>
</tr>
<tr class="even">
<td><p><em>OptionDuration</em></p></td>
<td><p><code>01:00:00</code> (1 小時)</p></td>
<td><p>此設定可決定 EdgeSync 服務可在 Edge Transport Server 上宣告租用選項的時間。如果保有租用的 EdgeSync 服務無法使用，且在此選項期間內未重新啟動，則除非您強制進行 EdgeSync 同步處理，否則其他 Exchange EdgeSync 服務將無法接管租用選項。</p></td>
</tr>
<tr class="odd">
<td><p><em>LockRenewalDuration</em></p></td>
<td><p><code>00:01:00</code> (1 分鐘)</p></td>
<td><p>此設定可決定當 EdgeSync 服務取得 Edge Transport Server 的鎖定時，更新鎖定欄位的頻率為何。</p></td>
</tr>
</tbody>
</table>


## 準備執行 EdgeSync 服務

您必須先確定您的基礎結構和信箱伺服器已完成 EdgeSync 服務的相關準備，才能將 Edge Transport Server 訂閱至 Exchange 組織。準備進行 EdgeSync 同步處理時，您必須：

  - 確認將 Edge Transport Server 與 Exchange 組織隔開的周邊網路防火牆，已設定為可經由正確的連接埠進行通訊。Edge Transport Server 使用非標準的 LDAP 連接埠。如果您的環境需使用特定連接埠，您可以使用 Exchange 隨附的 ConfigureAdam.ps1 指令碼修改 AD LDS 所使用的連接埠。如需詳細資訊，請參閱[修改 AD LDS 組態](modify-ad-lds-configuration-exchange-2013-help.md)。建立 Edge 訂閱之前，請修改連接埠。如果在建立 Edge 訂閱後才修改連接埠，則必須先將該 Edge 訂閱移除，再建立新的 Edge 訂閱。預設會使用下列 LDAP 連接埠來存取 AD LDS：
    
      - **LDAP**  連接埠 50389/TCP 可在本機上繫結到 AD LDS 執行個體。而不必在周邊網路防火牆上開啟這個連接埠。
    
      - **安全 LDAP**  連接埠 50636/TCP 使用於信箱伺服器到 AD LDS 之間的目錄同步處理。必須在防火牆上開啟此連接埠，才能順利進行 EdgeSync 同步處理。

  - 確認 Edge Transport Server 與信箱伺服器之間能夠雙向解析 DNS 主機名稱。

  - 授權 Edge Transport Server。建立 Edge 訂閱時，會擷取 Edge Transport Server 的授權資訊。在 Edge Transport Server 上套用授權金鑰後，已訂閱的 Edge Transport Servers 必須訂閱至 Exchange 組織。若在執行 Edge 訂閱程序後才在 Edge Transport Server 上套用授權金鑰，則不會在 Exchange 組織中更新授權資訊，而且您必須重新訂閱 Edge Transport Server。

  - 設定下列要傳播至 Edge Transport Server 的傳輸設定：
    
      - **內部 SMTP 伺服器**  在 **Set-TransportConfig** 指令程式上使用 *InternalSMTPServers* 參數，指定 Edge Transport Server 上的寄件者 ID 和連線篩選代理程式所要忽略的內部 SMTP 伺服器 IP 位址清單或 IP 位址範圍。
    
      - **公認的網域**  設定所有授權網域、內部轉送網域與外部轉送網域。
    
      - **遠端網域**  設定遠端網域設定。

回到頁首

## 管理 Edge 訂閱

如需 Edge 訂閱管理工作的逐步指示，請參閱[管理 Edge 訂閱](manage-edge-subscriptions-exchange-2013-help.md)。

