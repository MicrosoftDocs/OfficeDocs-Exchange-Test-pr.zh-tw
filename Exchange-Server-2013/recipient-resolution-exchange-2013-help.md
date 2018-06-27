---
title: '收件者的解決方法: Exchange 2013 Help'
TOCTitle: 收件者的解決方法
ms:assetid: 09deda5a-d405-45b1-a3ff-fefd3d76cdea
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb430743(v=EXCHG.150)
ms:contentKeyID: 52062512
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 收件者的解決方法

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-03-17_

*收件者解析*為展開並解決在郵件中的所有收件者的程序。法案解析收件者會比對的相對應的 Active Directory 物件的 Microsoft Exchange 組織中的收件者。法案展開的收件者會將所有通訊群組都展開成個別的收件者的清單。收件者的解決方法允許郵件限制及正確地套用到每個收件者的替代收件者。

在 Microsoft 部署Exchange Server 2013組織中收件者的解決方法被執行 Mailbox server 上的傳輸服務中分類程式。對每則郵件分類發生之後新送達的郵件放在提交佇列中。之前郵件放入傳遞佇列中的郵件上執行收件者解析，以及內容轉換和路由\]。分類程式執行收件者解析之前路由。負責收件者解析分類程式元件會經常呼叫*解決程式*。

**目錄**

最上層的解決方法

擴充

複本發送及控制收件者的擴充

收件者解析診斷

## 最上層的解決方法

*最上層的解析度*為收件者解析的第一個階段。最上層的解決方法會產生關聯至 Active Directory 中的比對收件者物件的內送郵件中的每個收件者。最上層解決期間分類程式會建立包含寄件者和訊息中存在的初始、 未展開的收件者電子郵件地址的清單。分類程式再使用該清單中的電子郵件地址來查詢 Active Directory 尋找任何具有郵件功能的物件具有比對電子郵件地址屬性。時找到相符項，快取的比對 Active Directory 物件屬性供日後使用。任何寄件者的郵件限制也會強制執行。

## 收件者的電子郵件地址

最上層的解析度開頭為一則訊息與初始、 未展開清單的收件者從*郵件信封*。郵件信封中包含的命令會用來轉送 SMTP 郵件伺服器之間的訊息。寄件者的電子郵件地址包含在**MAIL FROM:**命令。每個收件者的電子郵件地址包含在不同**RCPT TO:**命令。通常是從寄件者和收件者的郵件標頭中的`To:`、 `From:`、 `Cc:`及`Bcc:`標頭欄位建立信封寄件者及信封收件者。但是，這不則為 true。在郵件中的`To:`、 `From:`、 `Cc:`及`Bcc:`標頭欄位輕鬆是與可能不會符合實際的寄件者或已用來傳輸郵件的收件者的電子郵件地址。

## 封裝的電子郵件地址

標準的 SMTP 電子郵件地址例如遵循 RFC 2821 及 RFC 2822 chris@contoso.com，例如的規格。不過，電子郵件地址也可以是有效的 SMTP 地址內封裝非 SMTP 電子郵件地址。Exchange 支援封裝使用網際網路郵件連接器封裝地址 (進行 IMCEA) encapsulation 方法的地址。

這個 encapsulation 方法需要的任何 SMTP 電子郵件地址中無效的字元編碼。英數字元、 等號 （=） 和連字號 （-） 不需要編碼。其他任何字元使用下列編碼的語法：

  - 正斜線 （/） 會加上底線 (\_) 取代。

  - 其他 US-ASCII 字元取代加號 （+） 和其 ASCII 值的兩位數的十六進位寫入。例如，空白字元已編碼的值`+20`。

在進行 IMCEA 封裝方法使用下列語法： `IMCEA<Type>-<address>@<domain>`

版面配置區 \<*Type*\> 識別的非 SMTP 位址，例如`EX`、 `X400`或`FAX`類型。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>雖然<code>SMTP</code>和<code>X500</code>理論上有效值的 &lt;<em>Type</em>&gt;、 Exchange 收件者解析會拒絕使用其中一個這類的所有進行 IMCEA 編碼 」 地址。</td>
</tr>
</tbody>
</table>


版面配置區 \<*address*\> 是編碼的原始地址。版面配置區 \<*domain*\> 代表用來封裝的非 SMTP 位址，例如，contoso.com 的 SMTP 網域

使用進行 IMCEA 封裝方法之後，只有當網域會比對 Exchange 組織中的預設授權網域，個 unencapsulated 位址。如需公認的網域的詳細資訊，請參閱[公認的網域](accepted-domains-exchange-2013-help.md)。

Exchange 中的 SMTP 電子郵件地址的最大長度是 571 個字元。此限制包括下列資訊 ︰

  - 地址的名稱部分 315 字元

  - 255 個字元的網域名稱

  - 參閱註冊 (@) 分隔地址的名稱部分中的網域名稱字元。

請注意 Exchange 不支援的編碼以進行 IMCEA 封裝方法時的地址的名稱部分超過 315 字元，即使完整的電子郵件地址是小於 571 個字元的郵件。

## 位址解析

每封郵件、 寄件者電子郵件地址和所有收件者的電子郵件地址會新增至已用來查詢 Active Directory 的清單。封裝的所有地址是 unencapsulated 之前他們正在新增至的電子郵件地址清單。Active Directory 查詢是在最多 20 電子郵件地址執行一次。如果 Active Directory 查詢發生暫時性錯誤，郵件會傳回至提交佇列，並延遲的`%ExchangeInstallPath%Bin\EdgeTransport.exe.config` XML 應用程式設定檔中有相關聯的 Microsoft Exchange Transport 服務的*ResolverRetryInterval*鍵所指定的時間。預設值為 30 分鐘。

下表說明 Active Directory 中找到的收件者物件。如需 Exchange 收件者類型的詳細資訊，請參閱[收件者](recipients-exchange-2013-help.md)。

### 在 Active Directory 中的收件者物件

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Active Directory 收件者類型</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DistributionGroup</p></td>
<td><p>任何具有郵件功能的群組物件。通訊群組物件類型如下：</p>
<ul>
<li><p><strong>MailUniversalDistributionGroup</strong>  萬用通訊群組物件</p></li>
<li><p><strong>MailUniversalSecurityGroup</strong>  萬用安全性群組 (USG) 物件具有電子郵件地址</p></li>
<li><p><strong>MailNonUniversalGroup</strong>  本機 security group 物件，或是具有電子郵件地址全域安全性群組物件</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>DynamicDistributionGroup</p></td>
<td><p>具有 Active Directory 類別<strong>msExchDynamicDistributionList</strong>的物件。如需詳細資訊，請參閱<a href="manage-dynamic-distribution-groups-exchange-2013-help.md">管理動態通訊群組</a>。</p></td>
</tr>
<tr class="odd">
<td><p>Mailbox</p></td>
<td><p>具有電子郵件地址和定義的<em>Database</em>參數 user 物件</p></td>
</tr>
<tr class="even">
<td><p>MailUser</p></td>
<td><p>具有未定義的<em>Database</em>參數的電子郵件地址使用者物件。如需詳細資訊，請參閱<a href="manage-mail-users-exchange-2013-help.md">管理郵件使用者</a>。</p></td>
</tr>
<tr class="odd">
<td><p>MailContact</p></td>
<td><p>具有電子郵件地址的連絡人物件。郵件連絡人通常用於 Exchange 組織外部收件者。郵件連絡人也會在跨樹系 Exchange 環境中使用。如需詳細資訊，請參閱<a href="manage-mail-contacts-exchange-2013-help.md">管理郵件連絡人</a>。</p></td>
</tr>
<tr class="even">
<td><p>MailPublicFolder</p></td>
<td><p>公用資料夾物件具有電子郵件地址。</p></td>
</tr>
<tr class="odd">
<td><p>MicrosoftExchangeRecipient</p></td>
<td><p>具有 Active Directory 類別<strong>msExchExchangeServerRecipient</strong>的物件。如需 Microsoft Exchange 收件者物件的詳細資訊，請參閱<a href="recipients-exchange-2013-help.md">收件者</a>。</p></td>
</tr>
<tr class="even">
<td><p>SystemAttendantMailbox</p></td>
<td><p>具有 Active Directory 類別<strong>exchangeAdminService</strong>的物件。在 Exchange 組織中應只有一個系統服務員信箱。</p></td>
</tr>
<tr class="odd">
<td><p>SystemMailbox</p></td>
<td><p>使用者物件，位於 Microsoft Exchange 系統物件容器中並已電子郵件地址。應該會有一個系統信箱的 Exchange 組織中每個信箱資料庫。</p></td>
</tr>
</tbody>
</table>


含有遺漏或不正確的要徑屬性的物件都由 Active Directory 查詢歸類為無效的物件。例如，沒有電子郵件地址的動態通訊群組物件會被視為無效。傳送至分類為無效物件的收件者的郵件產生未傳遞回報 (NDR)。

每個電子郵件地址單一的初始查詢被執行所有的可能收件者屬性，例如收件者識別碼、 收件者類型、 郵件限制、 電子郵件地址和替代收件者。收件者的可用內容快取供日後使用。收件者解析分類相似之處中解決收件者的方式，與適用的收件者屬性的相似性為基礎的收件者。

用於位址解析的 LDAP 篩選說明如下：

  - **EX**電子郵件地址類型的 LDAP 篩選根據收件者**legacyExchangeDN** Active Directory 屬性或收件者**proxyAddresses** Active Directory 屬性。會優先**legacyExchangeDN** Active Directory 屬性。

  - 若是其他所有的電子郵件地址類型、 收件者**proxyAddresses** Active Directory 屬性會做為 LDAP 篩選器。

如果郵件中所使用的電子郵件地址不符的相對應的 Active Directory 物件的主要 SMTP 位址，分類程式修正來比對的主要 SMTP 位址訊息的電子郵件地址。原始的電子郵件地址會儲存於`ORCPT=`中的項目中的郵件信封**RCPT TO:**命令。

## 寄件者郵件限制

用於寄件者的郵件大小限制的大小是值**X-MS-Exchange-組織-OriginalSize:**郵件標頭中的標頭\] 欄位。Exchange 會使用此標頭欄位時輸入的 Exchange 組織記錄原始郵件大小的郵件。每當郵件會檢查針對指定的郵件大小限制，則會使用目前的郵件大小或原來的郵件大小標頭的較低值。郵件的大小可以變更由於內容轉換、 編碼及代理程式處理。如果此標頭欄位不存在，則會建立使用目前的郵件大小\] 值。如果郵件是太大，產生的 NDR 與其他郵件處理已停止。

寄件者收件者限制只會在處理郵件的第一個信箱伺服器上的傳輸服務中強制執行。原始的未展開郵件信封收件者計數與寄件者收件者限制相比較。原始的未展開郵件信封收件者計數用來避免部分的郵件傳遞問題時所發生之 Microsoft Exchange Server 2003中巢狀通訊群組清單使用遠端擴充伺服器。

郵件寄件者及所有收件者都會標記為解決的戳記郵件中的擴充的屬性。此延伸的屬性允許郵件略過最上層的解決方法如果郵件必須再次移到收件者的解決方法。郵件可能必須重複收件者解析再次因為重新啟動 Microsoft Exchange Transport 服務。

回到頁首

## 擴充

擴充會在最上層的解決方法之後發生。擴充完全展開成個別的收件者的收件者的巢狀層級。擴充可能需要多個行程進行擴充程序來展開所有收件者。並非所有收件者具有要展開。但是，所有收件者時必須經過擴充程序。擴充程序也會強制執行所有種類的收件者的收件者的郵件的限制。

下列清單說明需要擴充的收件者的種類：

  - **通訊群組和動態通訊群組**  通訊群組是根據**memberOf** Active Directory 屬性擴充。動態通訊群組會展開使用 Active Directory 查詢定義。如果*ExpansionServer*參數設定群組上，不是目前的伺服器來擴充群組。通訊群組會路由傳送到指定之伺服器的擴充。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您選取的特定傳輸伺服器以擴充伺服器在組織中，通訊群組使用方式會變成取決於擴充伺服器的可用性。如果擴充伺服器無法使用，無法傳遞任何傳送至通訊群組的郵件。如果您打算使用特定的擴充伺服器進行通訊群組，以減少服務中斷的風險您應該考慮實作這些伺服器的高可用性解決方案。</td>
    </tr>
    </tbody>
    </table>


  - **替代收件者**  *ForwardingAddress*參數可以設定信箱及擁有郵件功能的公用資料夾。*ForwardingAddress*參數會將所有郵件重新都導向至指定的替代收件者。這就是所謂*轉寄的收件者*。當*ForwardingAddress*參數中指定的替代傳遞地址和*DeliverToMailboxAndForward*參數設為`$true`時、 郵件傳遞至原始收件者和替代收件者。這就是所謂*傳遞和轉寄的收件者*。

  - **連絡人鏈結**  *連絡鏈*是郵件使用者或郵件連絡人已*ExternalEmailAddress*參數設定為 Exchange 組織中的另一個收件者的電子郵件地址。

## 偵測的收件者的循環

為通訊群組、 替代收件者\] 和連絡人鏈結展開、 分類程式檢查*收件者的循環*。收件者迴圈會無限圓形會導致郵件傳遞至相同的收件者的收件者組態問題。下列清單說明不同類型的收件者的循環：

  - **無害收件者的循環**  無害的收件者迴圈會產生成功傳遞郵件。下列清單說明兩種情況無害收件者的循環發生時：
    
      - 當兩個通訊群組成員身分有包含另一個。
    
      - 當信箱或擁有郵件功能的公用資料夾設傳遞和轉送至另一個。這兩個收件者的*DeliverToMailboxAndForward*參數設為`$true`和*ForwardingAddress*參數設為彼此時會發生此情況。
    
    偵測到無害的收件者迴圈時, 郵件傳遞至收件者，但若要將郵件傳遞到相同的收件者進行任何其他的嘗試。

  - **中斷收件者會循環**  中斷的收件者迴圈無法產生成功傳遞郵件。信箱或擁有郵件功能的公用資料夾有*ForwardingAddress*參數設定為另一個時中斷的收件者迴圈的範例。當分類程式偵測到中斷的收件者迴圈時，會停止目前的收件者的擴充活動，與收件者產生的 NDR。

偵測的收件者的循環不會防止重複的郵件傳遞。例如，通訊群組 C 會遇到重複的郵件傳遞如果符合下列條件成立：

  - 通訊群組 B 和通訊群組 C 是通訊群組 a 的成員

  - 通訊群組 C 也是通訊群組 b 的成員

## 傳遞報告重新導向做為通訊群組的

擴充通訊群組時，郵件類型會檢查來判斷該字型是否傳遞報告訊息。如果郵件的傳遞回報，檢查是否有通訊群組的重新導向設定來決定是否需要傳遞回報的重新導向。若要隱藏傳遞回報因為傳遞回報可能透露不想要的通訊群組和其成員資格的相關資訊。

下列清單說明可用的通訊群組和動態通訊群組的傳遞報告重新導向設定：

  - **ReportToManagerEnabled**  此參數可讓傳遞回報傳送給通訊群組管理員。有效值為`$true`或`$false`。預設值為`$false`。通訊群組，主管會由*ManagedBy*參數控制**Set-Group** cmdlet 中。動態通訊群組，主管會由*ManagedBy*參數控制**Set-DynamicDistributionGroup** cmdlet 中。

  - **ReportToOriginatorEnabled**  此參數可讓傳遞回報傳送給寄件者的電子郵件傳送至此通訊群組。有效值為`$true`或`$false`。預設值為`$true`。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><em>ReportToManagerEnabled</em>參數和<em>ReportToOriginatorEnabled</em>參數的值不可同時<code>$true</code>。如果一個參數設為<code>$true</code>、 其他必須設為<code>$false</code>。這兩個參數的值可以是<code>$false</code>。這會隱藏所有傳遞報告郵件的所有重新導向。</td>
    </tr>
    </tbody>
    </table>


下列清單說明可用的傳遞回報郵件：

  - **送達回條 (DR)**  這份報告確認郵件已傳遞至其預定的收件者。

  - **傳遞狀態通知 (DSN)**  這份報告說明嘗試傳遞郵件的結果。如需 DSN 郵件的詳細資訊，請參閱[Dsn 和 Ndr in Exchange 2013](dsns-and-ndrs-in-exchange-2013-exchange-2013-help.md)。

  - **郵件處理通知 (MDN)**  這份報告說明郵件狀態後它已經成功傳送給收件者。讀取的通知 (RN) 和非讀取通知 (NRN) 是 MDN 訊息這兩個範例。MDN 訊息定義於 RFC 2298 管理及控制由郵件標頭中的 \[ **Disposition-Notification-To:**標頭\] 欄位。MDN 設定使用`Disposition-Notification-To:`標頭欄位的不相容的許多不同的郵件伺服器。MDN 設定也可以使用 Microsoft Outlook 與 Exchange 中的 MAPI 屬性所定義。

  - **未傳遞回報 (NDR)**  這份報告會指出郵件寄件者的郵件無法傳遞至指定的收件者。

  - **非讀取通知 (NRN)**  這份報告會指出郵件已刪除之前已讀取。

  - **不在辦公室 (OOF)**  這份報告會指出收件者未回應電子郵件訊息。回到原始的 Microsoft 訊息的系統對應通知其中命名為"移出設備。"縮寫 OOF 日期

  - **讀取通知 (RN)**  這份報告會指出郵件已讀取。

  - **回收報告**  這份報告會指出特定收件者的重新叫用要求的狀態。寄件者會嘗試使用 Outlook 來回收已傳送的郵件時的重新叫用要求。

當傳遞報告訊息傳送至通訊群組之後時，下列設定值會導致報告郵件被刪除：

  - 未設定報表重新導向。或者，報告重新導向設定為郵件寄件者。

  - 報告重新導向設定為通訊群組管理員，並傳遞報告郵件不是 NDR。

當傳遞報告訊息傳送至通訊群組時，傳遞報告郵件可能會傳遞至通訊群組管理員。報告重新導向設為通訊群組管理員，並且報告郵件 NDR 時會發生此情況。

當未傳遞報告訊息的訊息傳送至通訊群組之後時，郵件已傳遞至通訊群組成員。下列清單摘要說明報表要求設定：

  - 如果報表重新導向設定為郵件寄件者、 報表要求設定並不會修改。

  - 如果未設定報表重新導向，則會隱藏所有報表要求設定。`NOTIFY=NEVER`項目新增至**RCPT TO:**郵件信封中的每個收件者。

  - 如果報表重新導向設定為通訊群組管理員，所有報表要求設定會都隱藏除了 NDR 郵件傳送至通訊群組管理員。

## 收件者的郵件限制

擴充程序也會強制執行設定收件者的任何郵件限制。這些限制可能會分別設定為每個收件者或公司的 Exchange 組織中所有 Hub Transport server。下表說明設定收件者的郵件限制。

### 收件者的郵件限制

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>來源</th>
<th>參數</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>Set-MailUser</strong></p>
<p><strong>Set-TransportConfig</strong></p></td>
<td><p><em>MaxReceiveSize</em></p></td>
<td><p><em>MaxReceiveSize</em>參數會指定用於郵件限制的收件者所設定的大小的郵件標頭中的<strong>X-MS-Exchange-Organization-OriginalSize:</strong>標頭欄位值。Exchange 會使用此標頭欄位時輸入的 Exchange 組織記錄原始郵件大小的郵件。每當郵件會檢查針對指定的郵件大小限制，則會使用目前的郵件大小或原來的郵件大小標頭的較低值。郵件的大小可以變更由於內容轉換、 編碼及代理程式處理。如果此標頭欄位不存在，則會建立使用目前的郵件大小] 值。如果郵件是太大，產生的 NDR 與其他郵件處理已停止。</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>Set-MailUser</strong></p></td>
<td><p><em>RequireSenderAuthenticationEnabled</em></p></td>
<td><p><em>RequireSenderAuthenticationEnabled</em>參數要求傳送給收件者的所有郵件都來自已驗證寄件者。當此參數的值設為<code>$true</code>時，會拒絕來自未經過驗證的寄件者的郵件。必須驗證所有寄件者將郵件傳送至系統和系統服務員信箱。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>Set-MailUser</strong></p></td>
<td><p><em>AcceptMessagesOnlyFromSendersOrMembers</em></p>
<p><em>RejectMessagesFromSendersOrMembers</em></p></td>
<td><p><em>AcceptMessagesOnlyFromSendersOrMembers</em>參數會指定寄件者或其成員可以傳送郵件給收件者的通訊群組。請注意此參數會結合較舊的<em>AcceptMessagesOnlyFrom</em>和<em>AcceptMessagesOnlyFromDLMembers</em>參數的功能。</p>
<p><em>RejectMessagesFromSendersOrMembers</em>參數指定通訊群組的成員不允許將訊息傳送給收件者的寄件者。請注意此參數會結合較舊的<em>RejectMessagesFrom</em>和<em>RejectMessagesFromDLMembers</em>參數的功能。</p>
<p>分類程式會檢查在兩個階段中的 「 收件者 」 權限。在第一階段決定寄件者是否存在<em>AcceptOnlyMessagesFromSendersOrMembers</em>或<em>RejectMessagesFromSendersOrMembers</em>參數中。如果找不到其中一個參數中的寄件者，會完全展開通訊群組在這些參數。此通訊群組的完整擴充可能需要一些時間。我們建議您減少這些參數中的巢狀的通訊群組的深度。</p></td>
</tr>
</tbody>
</table>


免除限制時特定類型的已驗證寄件者所傳送的郵件。下列清單說明免除收件者限制時的訊息：

  - **所有的 Microsoft Exchange 收件者所傳送的郵件**  這些訊息包含 DSN 郵件、 日誌報告、 配額郵件及其他系統產生的郵件傳送至內部郵件的寄件者。如需 Microsoft 收件者的詳細資訊，請參閱[收件者](recipients-exchange-2013-help.md)。

  - **所有的由外部該地址傳送的郵件**  這些訊息包括 DSN 郵件及其他系統產生的郵件傳送至外部郵件的寄件者。如需外部該地址的詳細資訊，請參閱[設定外部郵件管理員地址](configure-the-external-postmaster-address-exchange-2013-help.md)。

從 Exchange 組織傳送至外部網域時封鎖特定類型的郵件。設定是由**Set-RemoteDomain**指令程式中的下列參數控制：

  - *AllowedOOFType*

  - *AutoForwardEnabled*

  - *AutoReplyEnabled*

  - *DeliveryReportEnabled*

  - *NDREnabled*

如需詳細資訊，請參閱[遠端網域](remote-domains-exchange-2013-help.md)。

回到頁首

## 複本發送及控制收件者的擴充

因為郵件收件者的完整清單會展開及解決的收件者解析，有不同相同郵件副本必須建立時的情況。下列情況會描述由下列案例：

  - **當郵件收件者需要不同的郵件設定**  例如編製郵件內容的讀取回條可能需要啟用一些收件者與封鎖的其他收件者。建立新版本的訊息，有一些稍有不同屬性大於原始郵件會呼叫*複本發送*。

  - **若要限制為單一訊息中的信封收件者數目**  收件者的擴充程序可以產生數千個個別的收件者時，展開大型通訊群組。在 Exchange 而不被建立單一複本有數千個信封收件者的郵件，所建立的信封收件者數量有限的相同訊息多份複本。

## 複本發送

如果符合下列條件成立收件者解析分成兩部分一則訊息：

  - 當已更新**MAIL FROM:**、 郵件信封、 中的郵件寄件者。範例是在通訊群組的*ReportToManagerEnabled*參數的值為`$true`發生。

  - 當必須抑制自動回覆郵件，例如 Dsn、 郵件答錄機訊息及重新叫用報告。

  - 當展開替代收件者。

  - 當**Resent-From:**標頭欄位必須新增至郵件標頭。重新傳送標頭欄位是可用來判斷使用者是否已轉寄郵件的資訊的標頭欄位。重新傳送標頭欄位用於使會出現訊息給收件者好像送直接的原始寄件者。收件者可以檢視探索誰轉寄郵件的郵件標頭。重新傳送欄位定義 RFC 2822 3.6.6 區段中的標頭。

  - 當必須傳輸的通訊群組擴充的歷程記錄。

## 控制 \[收件者的擴充

展開的收件者數目太大時，分類程式會將郵件分割成多份。作法上是郵件擴充期間減少系統資源使用。在郵件中的信封收件者數目上限是*ExpansionSizeLimit*鍵`%ExchangeInstallPath%Bin\EdgeTransport.exe.config`應用程式設定檔中所控制。預設值為 1000年。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>我們建議您不要修改在實際執行環境中部署 Exchange 傳輸伺服器<em>ExpansionSizeLimit</em>機碼的值。</td>
</tr>
</tbody>
</table>


回到頁首

## 收件者解析診斷

效能計數器和郵件追蹤記錄項目所提供的收件者解析的報告及診斷資訊。這些來源可協助您找出並診斷問題收件者的解決方法。

## 收件者解析效能計數器

下表說明可用的收件者解析的效能計數器。

### 收件者解析效能計數器

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>計數器名稱</th>
<th>顯示名稱</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AmbiguousRecipientsTotal</p></td>
<td><p>不明確的收件者</p></td>
<td><p>這是模稜兩可偵測期間收件者解析收件者總數。不明確的收件者位於不同收件者具有比對<strong>legacyExchangeDN</strong> Active Directory 屬性或比對<strong>proxyAddresses</strong> Active Directory 屬性。</p></td>
</tr>
<tr class="even">
<td><p>AmbiguousSendersTotal</p></td>
<td><p>不明確的寄件者</p></td>
<td><p>這是在收件者解析期間所偵測到的模稜兩可寄件者數目。不明確的寄件者都具有比對<strong>legacyExchangeDN</strong> Active Directory 屬性或比對<strong>proxyAddresses</strong> Active Directory 屬性不同的寄件者。</p></td>
</tr>
<tr class="odd">
<td><p>FailedRecipientsTotal</p></td>
<td><p>失敗的收件者</p></td>
<td><p>這是在收件者解析期間所偵測到失敗的收件者數量。</p></td>
</tr>
<tr class="even">
<td><p>LoopRecipientsTotal</p></td>
<td><p>循環收件者</p></td>
<td><p>這是因為收件者的循環失敗收件者解析的收件者數量。</p></td>
</tr>
<tr class="odd">
<td><p>MessagesChippedTotal</p></td>
<td><p>缺口的郵件</p></td>
<td><p>這是訊息的總數的相同收件者的解決方法來控制的為單一訊息中的信封收件者數目時所建立的複本。在 Exchange 此程序稱為<em>chipping</em>。</p></td>
</tr>
<tr class="even">
<td><p>MessagesCreatedTotal</p></td>
<td><p>建立郵件</p></td>
<td><p>這是在收件者解析期間所建立的訊息數。</p></td>
</tr>
<tr class="odd">
<td><p>MessagesRetriedTotal</p></td>
<td><p>重試一次的郵件</p></td>
<td><p>這是在收件者解析已排程的重試的訊息數。</p></td>
</tr>
<tr class="even">
<td><p>UnresolvedOrgRecipientsTotal</p></td>
<td><p>無法解析的 Org 收件者</p></td>
<td><p>這是無法解析收件者從授權網域所偵測到收件者解析期間數目。</p></td>
</tr>
<tr class="odd">
<td><p>UnresolvedOrgSendersTotal</p></td>
<td><p>無法解析的 Org 寄件者</p></td>
<td><p>這是未解決的寄件者授權網域的收件者解析期間所偵測到的數目。</p></td>
</tr>
</tbody>
</table>


## 郵件追蹤記錄檔中的收件者解析事件

下表說明郵件追蹤記錄檔中寫入的收件者解析事件。

### 郵件追蹤記錄檔中的收件者解析事件

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>郵件追蹤事件</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>依序展開 [</p></td>
<td><p>此事件會指出已展開通訊群組。</p></td>
</tr>
<tr class="even">
<td><p>重新導向</p></td>
<td><p>此事件會指出訊息傳送給信箱收件者或擁有郵件功能的公用資料夾收件者已重新導向至替代<em>ForwardingAddress</em>參數所指定的收件者。</p></td>
</tr>
<tr class="odd">
<td><p>解決</p></td>
<td><p>此事件會指出收件者的電子郵件地址已變更為相對應的 Active Directory 收件者物件的主要 SMTP 電子郵件地址。</p></td>
</tr>
<tr class="even">
<td><p>傳輸</p></td>
<td><p>此事件會指出該郵件複本發送或 chipping 時發生。</p></td>
</tr>
</tbody>
</table>


如需郵件追蹤的詳細資訊，請參閱[郵件追蹤](message-tracking-exchange-2013-help.md)。

