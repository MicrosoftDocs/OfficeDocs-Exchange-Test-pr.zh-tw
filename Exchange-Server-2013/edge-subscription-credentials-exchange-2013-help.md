---
title: 'Edge 訂閱認證: Exchange 2013 Help'
TOCTitle: Edge 訂閱認證
ms:assetid: 1d291bc1-9c00-4d1b-8da0-cb81f63d8305
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb266959(v=EXCHG.150)
ms:contentKeyID: 61180448
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Edge 訂閱認證

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

本主題說明 Edge 訂閱處理程序如何提供認證以確保 EdgeSync 同步處理程序的安全性，以及 EdgeSync 如何使用這些認證來建立 Exchange 2013 信箱伺服器與 Edge Transport Server 之間的安全 LDAP 連線。若要深入了解 Edge 訂閱程序，請參閱[Edge 訂閱](edge-subscriptions-exchange-2013-help.md)。

**目錄**

Edge Subscription process

EdgeSync replication accounts

Authenticate initial replication

Authenticate scheduled synchronization sessions

Renew EdgeSync replication accounts

## Edge 訂閱程序

Active Directory 站台會訂閱 Edge Transport Server，以建立 Active Directory 站台中的信箱伺服器與已訂閱的 Edge Transport Server 之間的同步處理關係。Edge 訂閱處理程序期間提供的認證，可用來保護信箱伺服器與周邊網路中的 Edge Transport Server 之間的 LDAP 連線安全。

當您在 Edge Transport Server 上執行 **New-EdgeSubscription** 指令程式時，將會先在本機伺服器的 Active Directory 輕量型目錄服務 (AD LDS) 目錄中建立 EdgeSync 開機複寫帳戶 (ESBRA) 認證，然後將其寫入至 Edge 訂閱檔案。這些認證只會用來建立初始同步處理，且會在建立 Edge 訂閱檔案之後的 24 小時過期。如果未在 24 小時內完成 Edge 訂閱處理程序，您將必須重新執行 **New-EdgeSubscription** 指令程式，以建立新的 Edge 訂閱檔案。Edge 訂閱 XML 檔案會儲存 Edge 訂閱的組態資料。

Edge 訂閱 XML 檔案包含下表所列的資料。

### Edge 訂閱檔案內容

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>訂閱資料</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>EdgeServerName</strong></p></td>
<td><p>Edge Transport Server 的 NetBIOS 名稱。Edge 訂閱的 Active Directory 名稱會與此名稱相符。</p></td>
</tr>
<tr class="even">
<td><p><strong>EdgeServerFQDN</strong></p></td>
<td><p>Edge Transport Server 的網域全名 (FQDN)。已訂閱的 Active Directory 站台中的信箱伺服器必須能夠使用 DNS 來解析 FQDN，以找到 Edge Transport Server。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EdgeCertificateBlob</strong></p></td>
<td><p>Edge Transport Server 之自行簽署憑證的公開金鑰。</p></td>
</tr>
<tr class="even">
<td><p><strong>ESRAUsername</strong></p></td>
<td><p>指派給 ESBRA 的名稱。ESBRA 帳戶具有下列格式：ESRA.<em>Edge Transport Server 名稱</em>。ESRA 表示 EdgeSync 複寫帳戶；請留意 ESBRA (初始開機複寫帳戶) 與 ESRA 的差異。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ESRAPassword</strong></p></td>
<td><p>指派給 ESBRA 的密碼。密碼是使用亂數產生器所產生，並以純文字格式儲存在 Edge 訂閱檔案中。</p></td>
</tr>
<tr class="even">
<td><p><strong>EffectiveDate</strong></p></td>
<td><p>Edge 訂閱檔案的建立日期。</p></td>
</tr>
<tr class="odd">
<td><p><strong>持續時間</strong></p></td>
<td><p>這些認證在逾期之前的有效時間長度。ESBRA 帳戶的有效時間只有 24 個小時。</p></td>
</tr>
<tr class="even">
<td><p><strong>AdamSslPort</strong></p></td>
<td><p>將資料從 Active Director 同步處理至 AD LDS 時，EdgeSync 所繫結到的安全 LDAP 連接埠。這預設是 TCP 連接埠 50636。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ProductID</strong></p></td>
<td><p>Edge Transport Server 的授權資訊。在建立 Edge 訂閱之前，您必須取得 Edge Transport Server 的授權。</p></td>
</tr>
<tr class="even">
<td><p><strong>VersionNumber</strong></p></td>
<td><p>Edge 訂閱檔案的版本號碼。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SerialNumber</strong></p></td>
<td><p>Edge Transport Server 的 Exchange 版本。</p></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ESBRA 認證會以純文字格式寫入至 Edge 訂閱檔案。您在整個訂閱處理程序中都必須保護此檔案。將 Edge 訂閱檔案匯入 Exchange 組織後，您應立即將 Edge 訂閱檔案從 Edge Transport Server、用以將檔案匯入 Exchange 組織的網路共用，以及任何卸除式媒體中刪除。</td>
</tr>
</tbody>
</table>


回到頁首

## EdgeSync 複寫帳戶

EdgeSync 複寫帳戶 (ESRA) 是 EdgeSync 安全性的重要部分。ESRA 的驗證和授權是一種機制，用來保護 Edge Transport Server 與信箱伺服器之間的連線安全。

Edge 訂閱檔案中所含的 ESBRA 可在初始同步處理期間用來建立安全 LDAP 連線。將 Edge 訂閱檔案匯入至訂閱 Edge Transport Server 之 Active Directory 站台中的信箱伺服器之後，將會在 Active Directory 中為每個「Edge Transport-信箱伺服器」配對建立其他 ESRA 帳戶。而在初始同步處理期間，會將新建立的 ESRA 認證複寫至 AD LDS。這些 ESRA 認證是用來協助保護後續同步處理工作階段的安全。

下表所列的內容會指派給每個 EdgeSync 複寫帳戶。

### Ms-Exch-EdgeSyncCredential 屬性

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>內容名稱</th>
<th>類型</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>TargetServerFQDN</strong></p></td>
<td><p>字串</p></td>
<td><p>接受這些認證的 Edge Transport Server。</p></td>
</tr>
<tr class="even">
<td><p><strong>SourceServerFQDN</strong></p></td>
<td><p>¦r¦ê</p></td>
<td><p>呈現這些認證的信箱伺服器。如果認證是開機認證，則此值會是空的。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EffectiveTime</strong></p></td>
<td><p>DateTime (UTC)</p></td>
<td><p>開始使用此認證的時間。</p></td>
</tr>
<tr class="even">
<td><p><strong>ExpirationTime</strong></p></td>
<td><p>DateTime (UTC)</p></td>
<td><p>停止使用此認證的時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserName</strong></p></td>
<td><p>¦r¦ê</p></td>
<td><p>用來進行驗證的使用者名稱。</p></td>
</tr>
<tr class="even">
<td><p><strong>Password</strong></p></td>
<td><p>位元組</p></td>
<td><p>用來進行驗證的密碼。密碼會使用 <strong>ms-Exch-EdgeSync-Certificate</strong> 進行加密。</p></td>
</tr>
</tbody>
</table>


下列各節將說明如何在 EdgeSync 同步處理程序期間提供及使用 ESRA 認證。

## 提供 EdgeSync 開機複寫帳戶

在 Edge Transport Server 上執行 **New-EdgeSubscription** 指令程式時，會如下提供 ESBRA：

  - 在 Edge Transport Server 上建立自行簽署憑證 (Edge-Cert)。私密金鑰會儲存在本機電腦儲存區中，而公開金鑰則會寫入至 Edge 訂閱檔案。

  - ESBRA 帳戶會建立在 AD LDS 中，而其認證會寫入至 Edge 訂閱檔案。

  - Edge 訂閱檔案的匯出方式是複製到卸除式媒體 (因為 Edge Server 不在 Active Directory 中，因此您無法使用共用資料夾匯出檔案)。此檔案現在已可匯入至信箱伺服器。

## 在 Active Directory 中提供 EdgeSync 複寫帳戶

在信箱伺服器上匯入 Edge 訂閱檔案時，須執行下列步驟，以在 Active Directory 中建立 Edge 訂閱的記錄，以及提供其他 ESRA 認證。

1.  在 Active Directory 中建立 Edge Transport Server 組態物件。而 Edge-Cert 憑證會寫入至此物件當成屬性。

2.  在已訂閱的 Active Directory 站台中，每部信箱伺服器都會接收到 Active Directory 通知，告知已登錄新的 Edge 訂閱。一接收到通知，每部信箱伺服器就會擷取 ESRA.Edge 帳戶，並使用 Edge-Cert 公開金鑰加密該帳戶。加密的 ESRA.edge 帳戶會寫入至 Edge Transport Server 組態物件。

3.  每部信箱伺服器都會建立自我簽署憑證 (TransportService-Cert)。私密金鑰會儲存在本機電腦存放區中，而公開金鑰則會儲存在 Active Directory 的信箱伺服器組態物件中。

4.  每部信箱伺服器都會使用其本身 TransportService 憑證的公開金鑰來加密 ESRA.edge 帳戶，然後再將該帳戶儲存在其本身的組態物件中。

5.  每部信箱伺服器都會為 Active Directory 中每個現有的 Edge Transport Server 組態物件產生一個 ESRA (ESRA.edge. *Mailboxname.\#*)。
    
    範例：ESRA.edge.Example.0
    
    ESRA.edge 的密碼是使用亂數產生器所產生，並且會使用 TransportService-Cert 憑證的公開金鑰加密。產生的密碼具有 Windows Server 允許的最大長度。

6.  每個 ESRA.edge. *Mailboxname.\#* 帳戶都會使用 Edge-Cert 憑證的公開金鑰進行加密，並儲存在 Active Directory 的 Edge Transport Server 組態物件上。

下列各節將說明如何在 EdgeSync 同步處理期間使用這些帳戶。

回到頁首

## 驗證初始複寫

只有在建立初始同步處理時，才會使用初始 ESBRA 帳戶。在第一次 EdgeSync 同步處理期間，會將其他 ESRA 帳戶 (ESRA.edge.*Mailboxname.\#*) 複寫至 AD LDS。這些帳戶是用來驗證後續的 EdgeSync 同步處理工作階段。

執行初始複寫的信箱伺服器是隨機決定的。在 Active Directory 站台中，第一部執行拓撲掃描及探索新 Edge 訂閱的信箱伺服器，將會執行初始複寫。由於探索會以拓撲掃描的時間點為基礎，因此站台中的任何信箱伺服器都可能會執行初始複寫。

EdgeSync 會起始從信箱伺服器到 Edge Transport Server 的安全 LDAP 工作階段。Edge Transport Server 會呈現其自我簽署憑證，而信箱伺服器會驗證該憑證是否符合 Active Directory 中的 Edge Transport Server 組態物件所儲存的憑證。驗證 Edge Transport Server 的識別碼之後，信箱伺服器會將 ESRA.edge.*Mailboxname.\#* 帳戶的認證提供給 Edge Transport Server。Edge Transport Server 會根據儲存在 AD LDS 中的帳戶來驗證認證。

接著，信箱伺服器上的 EdgeSync 服務會將拓撲、組態和收件者資料從 Active Directory 發送至 AD LDS。Active Directory 中的 Edge Transport Server 組態物件的變更會複寫至 AD LDS。AD LDS 接收到新增的 ESRA.edge.*Mailboxname.\#* 項目後，Microsoft Exchange 認證服務會建立對應的 AD LDS 帳戶。這些帳戶現在可用來驗證後續排定的 EdgeSync 同步處理工作階段。

## Microsoft Exchange Credential Service

Microsoft Exchange 認證服務是 Edge 訂閱處理程序的一部分。認證服務只會在 Edge Transport Server 上執行。此服務會在 AD LDS 中建立逆向 ESRA 帳戶，使信箱伺服器能夠驗證 Edge Transport Server，以執行 EdgeSync 同步處理。EdgeSync 並不會直接與 Microsoft Exchange 認證服務進行通訊。Microsoft Exchange 認證服務會與 AD LDS 進行通訊，並在信箱伺服器更新 ESRA 認證時安裝 ESRA 認證。

回到頁首

## 驗證排定的同步處理工作階段

完成初始 EdgeSync 同步處理之後，會建立 EdgeSync 同步處理排程，而且會在 AD LDS 中定期更新任何有所變更的 Active Directory 資料。信箱伺服器會對 Edge Transport Server 上的 AD LDS 執行個體起始安全 LDAP 工作階段。AD LDS 會呈現其自我簽署憑證，以向該信箱伺服器證明它的身分識別。信箱伺服器會將其 ESRA.edge 認證呈現給 AD LDS。ESRA.edge密碼會使用信箱伺服器的自我簽署憑證公開金鑰進行加密。只有該信箱伺服器可使用這些認證對 AD LDS 進行驗證。

回到頁首

## 更新 EdgeSync 複寫帳戶

ESRA 帳戶的密碼必須遵守本機伺服器的密碼原則。為了防止密碼更新處理程序造成暫時性的驗證失敗，在第一個 ESRA.edge 帳戶到期的七天前，會建立第二個 ESRA.edge 帳戶，其生效時間為第一個 ESRA 到期時間的前三天。第二個 ESRA.edge 帳戶生效後，EdgeSync 會隨即停止使用第一個帳戶，並開始使用第二個帳戶。到達第一個帳戶的到期時間時，就會刪除那些 ESRA 認證。除非移除 Edge 訂閱，否則此更新處理程序會繼續進行。

回到頁首

