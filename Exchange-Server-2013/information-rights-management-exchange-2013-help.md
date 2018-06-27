---
title: '資訊版權管理: Exchange 2013 Help'
TOCTitle: 資訊版權管理
ms:assetid: 6ea3a695-3ddd-4d53-b3c6-90041f44ef64
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd638140(v=EXCHG.150)
ms:contentKeyID: 50473455
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 資訊版權管理

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

資訊工作者每天都會使用電子郵件來交換機密資訊，例如財務報表和資料、法律合約、機密產品資訊、銷售報告和預測、競爭分析、研究和專利資訊，以及客戶和員工資訊。由於人員現在幾乎可從任何位置存取其電子郵件，因此信箱已轉換為包含大量潛在機密資訊的存放庫。因此，資訊外洩可能會對組織造成嚴重威脅。為了防止資訊外洩，Microsoft Exchange Server 2013 包含資訊版權管理 (IRM) 功能，可針對電子郵件訊息和附件提供持續性的線上和離線保護。

**目錄**

What is information leakage?

Traditional solutions to information leakage

IRM in Exchange 2010

Applying IRM protection to messages

Scenarios for IRM protection

Decrypting IRM-protected messages to enforce messaging policies

Prelicensing

IRM agents

IRM requirements

Configuring and testing IRM

Extend Rights Management with the Rights Management connector

## 何謂資訊外洩？

洩漏可能具機密性的資訊會造成組織的損失，且對組織及其業務、員工、客戶和夥伴帶來廣泛的影響。有越來越多的本地和產業規定用於管理儲存、傳輸和保護特定資訊類型的方式。為了避免違反適用的規定，組織必須保護自己，防止故意、不慎或意外的資訊外洩。

資訊外洩可能造成的一些後果如下：

  - **財務損失**   視規模、產業和本地規定而定，資訊外洩可能會由於業務損失，或是法庭和法規機構裁定的罰款和懲罰性賠償，而造成財務上的影響。上市公司也可能由於不利的媒體報導，面臨損失市值的風險。

  - **形象和信譽受損**   資訊外洩可能危害組織在客戶間的形象和信譽。此外，視通訊的本質而定，外洩的電子郵件訊息可能是造成寄件者和組織困窘的來源。

  - **失去競爭優勢**   資訊外洩所造成的最嚴重威脅之一，就是失去企業競爭優勢。洩漏策略性計劃或洩漏合併與收購資訊，有可能導致損失收益或市值。其他威脅還包括失去研究資訊、分析資料及其他智慧財產。

回到頁首

## 資訊外洩的傳統解決方案

雖然資訊外洩的傳統解決方案可以保護對資料的初始存取，但通常無法提供持續的保護。下表列出一些傳統解決方案及其限制。

### 傳統解決方案

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>解決方案</th>
<th>描述</th>
<th>限制</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>傳輸層安全性 (TLS)</p></td>
<td><p>TLS 是網際網路標準通訊協定，可利用加密方法保護透過網路進行的通訊。在郵件環境中，TLS 可用來保護伺服器/伺服器及用戶端/伺服器通訊的安全。</p>
<p>根據預設， Exchange 2010使用 TLS 的所有內部郵件傳輸。預設值也會啟用隨機 TLS 與外部主機的工作階段。Exchange會先嘗試使用 TLS 加密工作階段，但如果無法建立 TLS 連線與目的地伺服器， Exchange使用 SMTP。您也可以設定來強制執行相互 TLS 與外部組織網域安全性。</p></td>
<td><p>TLS 只保護兩個 SMTP 主機之間的 SMTP 工作階段。亦即，TLS 會保護移動中的資訊，但不會在郵件層級或對靜止的資訊提供保護。除非使用其他方法加密郵件，否則寄件者和收件者信箱中的郵件仍然不受保護。對於傳送到組織外部的電子郵件，可以只要求第一個躍點使用 TLS。您組織外部的遠端 SMTP 主機收到郵件後，可以透過未加密的工作階段將郵件轉送到其他 SMTP 主機。由於 TLS 是傳輸層技術，因此對於收件者對郵件採取的動作無法提供控制。</p></td>
</tr>
<tr class="even">
<td><p>電子郵件加密</p></td>
<td><p>使用者可以使用 S/MIME 等技術來加密郵件。</p></td>
<td><p>使用者可決定是否加密郵件。由於伴隨使用者憑證管理與私密金鑰保護等開銷，因此加密會增加公開金鑰基礎結構 (PKI) 部署的額外成本。在郵件解密之後，無法控制收件者可對該資訊採取什麼動作。解密的資訊可以複製、列印或轉寄。預設情況下，儲存的附件不會受到保護。</p>
<p>您的組織無法存取使用 S/MIME 等技術加密的郵件。組織不能檢查郵件內容，因此無法強制執行郵件原則、掃描郵件中的病毒或惡意內容，或是採取任何需要存取內容的動作。</p></td>
</tr>
</tbody>
</table>


最後，傳統的解決方案通常缺乏強制執行工具，以致無法套用統一的郵件原則來防止資訊外洩。例如，使用者傳送包含機密資訊的郵件，並將該郵件標記為 **\[公司機密\]** 及 **\[不要轉寄\]**。在郵件傳遞給收件者後，寄件者或組織便無法再控制該資訊。收件者可以有意或無意地轉寄郵件 (透過使用自動轉寄規則等功能) 到外部電子郵件帳戶，使您的組織遭受顯著的資訊外洩風險。

回到頁首

## Exchange 2013 中的 IRM

在 Exchange 2013 中，您可以使用 IRM 功能，將持續保護套用至郵件和附件。IRM 使用 Active Directory Rights Management Services (AD RMS)，這是 Windows Server 2008 和更新版本中的資訊保護技術。組織和使用者可以使用 Exchange 2013 中的 IRM 功能，控制收件者對電子郵件所具有的權限。IRM 也可協助允許或限制收件者動作，例如將郵件轉寄給其他收件者、列印郵件或附件，或是透過複製和貼上來擷取郵件或附件內容。IRM 保護可由使用者在 Microsoft Outlook 或 Office Outlook Web App 中套用，也可以根據您組織的郵件原則，使用傳輸保護規則或 Outlook 保護規則來套用。不像其他電子郵件加密解決方案，IRM 還可讓您的組織解密受保護的內容，以強制執行原則符合性。

AD RMS 使用以可延伸版權標記語言 (XrML) 為基礎的憑證和授權，來認證電腦和使用者並保護內容。使用 AD RMS 來保護文件或郵件等內容時，會附加 XrML 授權，其中包含授權使用者對該內容所擁有的權限。若要存取受 IRM 保護的內容，已啟用 AD RMS 的應用程式必須為 AD RMS 叢集中的授權使用者取得使用授權。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在 Exchange 2013 中，Prelicensing 代理程式會將使用授權附加至使用組織中的 AD RMS 叢集來保護的郵件。如需相關資訊，請參閱本主題稍後的Prelicensing。</td>
</tr>
</tbody>
</table>


用來建立內容的應用程式必須已啟用 RMS，才能使用 AD RMS 對內容套用持續性的保護。Microsoft Office 應用程式 (如 Word、Excel、PowerPoint 和 Outlook) 已啟用 RMS，可用來建立和取用受保護的內容。

IRM 可協助您執行下列動作：

  - 防止受 IRM 保護之內容的授權收件者轉寄、修改、列印、傳真、儲存或剪下並貼上內容。

  - 使用與郵件相同的保護層級，保護支援的附件檔案格式。

  - 支援受 IRM 保護之郵件和附件的到期功能，以便經過指定期間之後便無法再加以檢視。

  - 防止使用 Microsoft Windows 中的剪取工具來複製受 IRM 保護的內容。

不過，IRM 無法防止使用下列方法來複製資訊：

  - 協力廠商螢幕擷取程式

  - 使用照相機等影像裝置，拍攝螢幕上顯示的受 IRM 保護的內容

  - 使用者記住或手動抄錄資訊

若要深入了解 AD RMS，請參閱[Active Directory Rights Management Services](https://go.microsoft.com/fwlink/p/?linkid=129823)。

## AD RMS 權限原則範本

AD RMS 使用以 XrML 為基礎的權限原則範本，讓已啟用 IRM 的相容應用程式套用一致的保護原則。在 Windows Server 2008 和更新版本中，AD RMS 伺服器會公開 Web 服務，這項服務可用來列舉和取得範本。Exchange 2013 隨附 \[不要轉寄\] 範本。當 \[不要轉寄\] 範本套用至郵件時，只有郵件中所列的收件者才能解密郵件。收件者無法轉寄郵件、複製郵件中的內容或列印郵件。您可以在組織中的 AD RMS 伺服器上建立額外的 RMS 範本，以符合您的 IRM 保護需求。

IRM 保護是透過套用 AD RMS 權限原則範本來套用。您可以使用原則範本，控制收件者對郵件所擁有的權限。透過將適當的權限原則範本套用至郵件，即可控制如回覆、全部回覆、轉寄、從郵件擷取資訊、儲存郵件或列印郵件等動作。

如需權限原則範本的詳細資訊，請參閱[AD RMS 原則範本考量](https://go.microsoft.com/fwlink/p/?linkid=179455)。

如需建立 AD RMS 權限原則範本的詳細資訊，請參閱[AD RMS 權限原則範本部署逐步指南](https://go.microsoft.com/fwlink/p/?linkid=136593)。

回到頁首

## 將 IRM 保護套用至郵件

在Exchange 2010、 IRM 保護可以套用至郵件使用下列方法：

  - **由 Outlook 使用者手動**  Outlook使用者可以 IRM 保護的郵件 AD RMS 權限原則範本提供給他們。此程序會使用Outlook、 和Exchange中的 IRM 功能。不過，您可以使用Exchange存取郵件，而您可以採取動作 （例如套用傳輸規則） 通訊原則來強制執行您的組織。如需在Outlook中使用 IRM 的詳細資訊，請參閱[使用 IRM 的電子郵件簡介](https://go.microsoft.com/fwlink/p/?linkid=166897)。

  - **由 Outlook Web App 使用者手動進行**   當您在 Outlook Web App 中啟用 IRM 時，使用者可用 IRM 保護所傳送的郵件，並檢視收到的受 IRM 保護的郵件。在 Exchange 2013 累計更新 1 (CU1) 中，Outlook Web App 使用者也可使用 Web-Ready 文件檢視來檢視受 IRM 保護的附件。如需 Outlook Web App 中 IRM 的詳細資訊，請參閱[Outlook Web App 中的資訊版權管理](information-rights-management-in-outlook-web-app-exchange-2013-help.md)。

  - **手動由 Windows Mobile 及 Exchange ActiveSync 裝置的使用者**  量產發行 (RTM) 版本Exchange 2010版本、 Windows行動裝置的使用者可以檢視及建立受 IRM 保護的郵件。這需要使用者在其支援的Windows行動裝置連線至電腦並啟用他們的 IRM。在Exchange 2010 SP1，您可以在 Microsoft Exchange ActiveSync允許Exchange ActiveSync裝置 （包括Windows行動裝置） 的使用者檢視中啟用 IRM、 回覆、 轉寄，並建立受 IRM 保護的郵件。在Exchange ActiveSyncIRM 的相關資訊，請參閱[Exchange ActiveSync 中的資訊版權管理](information-rights-management-in-exchange-activesync-exchange-2013-help.md)。

  - **在 Outlook 2010 和更新版本中自動進行**   您可以在 Outlook 2010 和更新版本中中建立 Outlook 保護規則，以自動為郵件套用 IRM 保護。Outlook 保護規則會自動部署至 Outlook 2010 用戶端，且會在使用者撰寫郵件時由 Outlook 2010 套用 IRM 保護。如需 Outlook 保護規則的詳細資訊，請參閱[Outlook 保護規則](outlook-protection-rules-exchange-2013-help.md)。

  - **在信箱伺服器上自動進行** 在 Exchange 2013 信箱伺服器上，您可以建立傳輸保護規則，以自動為郵件套用 IRM 保護。如需傳輸保護規則的詳細資訊，請參閱[傳輸保護規則](transport-protection-rules-exchange-2013-help.md)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>IRM 保護不會再次套用到已受 IRM 保護的郵件。例如，如果使用者在 Outlook 或 Outlook Web App 中以 IRM 保護郵件，就不會使用傳輸保護規則將 IRM 保護套用至郵件。</td>
    </tr>
    </tbody>
    </table>


回到頁首

## IRM 保護的案例

下表說明 IRM 保護的案例。

### IRM 保護的案例

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>傳送受 IRM 保護的訊息</th>
<th>支援</th>
<th>需求</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>在相同內部部署 Exchange 2013 部署中</p></td>
<td><p>是</p></td>
<td><p>如需有關需求的資訊，請參閱本主題稍後的 IRM Requirements。</p></td>
</tr>
<tr class="even">
<td><p>在內部部署的不同樹系之間</p></td>
<td><p>是</p></td>
<td><p>如需需求，請參閱<a href="https://go.microsoft.com/fwlink/p/?linkid=199009">設定 AD RMS 與 Exchange Server 2010 跨多個樹系整合</a>。</p></td>
</tr>
<tr class="odd">
<td><p>在內部部署 Exchange 2013 部署與雲端式 Exchange 組織之間</p></td>
<td><p>是</p></td>
<td><ul>
<li><p>使用內部部署 AD RMS 伺服器。</p></li>
<li><p>從內部部署 AD RMS 伺服器匯出信任的發行網域。</p></li>
<li><p>在雲端式組織中匯入信任的發行網域。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>寄給外部收件者</p></td>
<td><p>否</p></td>
<td><p>Exchange 2010不包括非同盟組織中的外部收件者傳送受 IRM 保護之訊息的解決方案。AD RMS 提供使用信任原則解決方案。您可以設定 AD RMS 叢集與 Microsoft 帳戶 （以前稱為Windows Live ID） 之間的信任原則。兩個組織之間傳送的郵件，您可以建立兩個使用Active Directory Federation Services (AD FS) 的Active Directory樹系間的同盟的信任。深入了解，請參閱 ＜<a href="https://go.microsoft.com/fwlink/p/?linkid=182909">了解 AD RMS 信任原則</a>。</p></td>
</tr>
</tbody>
</table>


回到頁首

## 解密受 IRM 保護的郵件以強制執行郵件原則

為強制執行郵件原則及法規遵從目的，您必須可以存取加密的郵件內容。為符合起因於訴訟、法規稽核或內部調查的 eDiscovery 需求，您還必須可以搜尋加密的郵件。為協助進行這些工作，Exchange 2013 包含下列 IRM 功能：

  - **傳輸解密**   若要套用郵件原則，傳輸代理程式 (例如傳輸規則代理程式) 應可存取郵件內容。傳輸解密可允許安裝在 Exchange 2013 伺服器上的傳輸代理程式存取郵件內容。如需詳細資訊，請參閱[傳輸解密](transport-decryption-exchange-2013-help.md)。

  - **日誌報告解密**   為了達到符合性或企業需求，組織可使用日誌記錄來保留郵件內容。日誌代理程式會針對要進行日誌記錄的郵件建立日誌報告，並在報告中包含郵件的中繼資料。原始郵件會附加至日誌報告。如果日誌報告中的郵件受 IRM 保護，則日誌報告解密會將郵件的純文字副本附加至日誌報告。如需詳細資訊，請參閱[日誌報告解密](journal-report-decryption-exchange-2013-help.md)。

  - **Exchange 搜尋的 IRM 解密** 藉由 Exchange 搜尋的 IRM 解密，Exchange 搜尋可以進行受 IRM 保護的郵件內容索引。當探索管理員執行就地 eDiscovery 搜尋時，會在搜尋結果中傳回已建立索引的 IRM 保護郵件。如需更多資訊，請參閱[就地 eDiscovery](in-place-ediscovery-exchange-2013-help.md)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>中Exchange 2010 SP1 和更新版本、 探索管理角色群組的成員可以存取受 IRM 保護所探索搜尋傳回與郵件中的探索信箱。若要啟用此功能，請先<a href="https://technet.microsoft.com/zh-tw/library/dd979792(v=exchg.150)">Set-IRMConfiguration</a>指令程式搭配<em>EDiscoverySuperUserEnabled</em>參數的物件。如需詳細資訊，請參閱<a href="configure-irm-for-exchange-search-and-in-place-ediscovery-exchange-2013-help.md">將 IRM 設定 Exchange 搜尋與就地 ediscovery （英文）</a>。</td>
    </tr>
    </tbody>
    </table>


若要啟用這些解密功能，Exchange 伺服器必須可以存取郵件。這是透過將同盟信箱 (由 Exchange 安裝程式所建立的系統信箱) 新增至 AD RMS 伺服器上的超級使用者群組來達成。如需詳細資訊，請參閱[至 AD RMS 超級使用者群組新增同盟信箱](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md)。

回到頁首

## Prelicensing

為檢視受 IRM 保護的郵件和附件，Exchange 2013 會自動將先期授權附加至受保護的郵件。如此用戶端就不必多次到 AD RMS 伺服器擷取使用授權，還可啟用受 IRM 保護之郵件和附件的離線檢視。Prelicensing 也可讓受 IRM 保護的訊息於 Outlook Web App 中檢視。啟用 IRM 功能時，Prelicensing 也會依預設啟用。

回到頁首

## IRM 代理程式

在 Exchange 2013 中，已使用信箱伺服器之傳輸服務中的傳輸代理程式啟用 IRM 功能。IRM 代理程式會由 Exchange 安裝程式在信箱伺服器上安裝。您無法使用傳輸代理程式的管理工作來控制 IRM 代理程式。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在 Exchange 2013 中，IRM 代理程式是內建代理程式。內建代理程式不包含在 <strong>Get-TransportAgent</strong> 指令程式傳回的代理程式清單中。如需詳細資訊，請參閱<a href="transport-agents-exchange-2013-help.md">傳輸代理程式</a>。</td>
</tr>
</tbody>
</table>


下表列出了信箱伺服器的傳輸服務中實作的 IRM 代理程式。

### 信箱伺服器的傳輸服務中的 IRM 代理程式

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Agent</th>
<th>事件</th>
<th>功能</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>RMS 解密代理程式</p></td>
<td><p>OnEndOfData (SMTP) 與 OnSubmittedMessage</p></td>
<td><p>解密郵件以允許存取傳輸代理程式。</p></td>
</tr>
<tr class="even">
<td><p>傳輸規則代理程式</p></td>
<td><p>OnRoutedMessage</p></td>
<td><p>將符合傳輸保護規則中規則條件的郵件，標幟為由 RMS 加密代理程式提供 IRM 保護。</p></td>
</tr>
<tr class="odd">
<td><p>RMS 加密代理程式</p></td>
<td><p>OnRoutedMessage</p></td>
<td><p>將 IRM 保護套用至傳輸規則代理程式所標幟的郵件，並重新加密傳輸解密的郵件。</p></td>
</tr>
<tr class="even">
<td><p>Prelicensing 代理程式</p></td>
<td><p>OnRoutedMessage</p></td>
<td><p>將先期授權附加至受 IRM 保護的郵件。</p></td>
</tr>
<tr class="odd">
<td><p>日誌報告解密代理程式</p></td>
<td><p>OnCategorizedMessage</p></td>
<td><p>解密附加至日誌報告的受 IRM 保護的郵件，並連同原始加密的郵件內嵌純文字版本。</p></td>
</tr>
</tbody>
</table>


如需傳輸代理程式的相關資訊，請參閱[傳輸代理程式](transport-agents-exchange-2013-help.md)。

回到頁首

## IRM 需求

若要在您的 Exchange 2013 組織中實作 IRM，您的部署必須符合下表所述的需求：

### IRM 需求

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>伺服器</th>
<th>需求</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AD RMS 叢集</p></td>
<td><ul>
<li><p><strong>作業系統</strong>   需要 Windows Server 2012、Windows Server 2008 R2 或 Windows Server 2008 SP2 (具備 Hotfix <a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=973247">Windows Server 2008 中的 Active Directory Rights Management Services 角色</a>)。</p></li>
<li><p><strong>服務連線點</strong>   Exchange 2010和 AD RMS 感知應用程式使用Active Directory中登錄的服務連線點來探索 AD RMS 叢集與 Url。AD RMS 可讓您以登錄服務連線點從 AD RMS 安裝程式中。如果用來設定 AD RMS 的帳戶不是 Enterprise Admins 安全性群組的成員，服務連線點註冊可以執行安裝程式完成後。沒有 AD RMS Active Directory樹系中只有一個服務連線點。</p></li>
<li><p><strong>權限</strong>   必須指派 AD RMS 伺服器憑證管線 (AD RMS 伺服器上的 <code>ServerCertification.asmx</code> 檔案) 的讀取和執行權限給下列項目：</p>
<ul>
<li><p>Exchange 伺服器群組或個別 Exchange 伺服器</p></li>
<li><p>AD RMS 伺服器上的 AD RMS 服務群組</p></li>
</ul>
<p>根據預設，ServerCertification.asmx 檔案位於 AD RMS 伺服器上的 [ <code>\inetpub\wwwroot\_wmcs\certification\</code> ] 資料夾中。如需詳細資訊，請參閱<a href="https://go.microsoft.com/fwlink/p/?linkid=186951">AD RMS 伺服器憑證管線上設定權限</a>。</p></li>
<li><p><strong>AD RMS 超級使用者</strong>   若要啟用傳輸解密、日誌報告解密、Outlook Web App 中的 IRM，以及 Exchange 搜尋的 IRM，您必須將同盟信箱 (由 Exchange 2013 安裝建立的系統信箱) 新增至 AD RMS 叢集的超級使用者群組。如需詳細資訊，請參閱<a href="add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md">至 AD RMS 超級使用者群組新增同盟信箱</a>。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Exchange</p></td>
<td><ul>
<li><p>Exchange 2010或更新版本，則需要。</p></li>
<li><p>Hotfix <a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=973136">FIX：當 .NET Framework 2.0 SP2 型應用程式嘗試處理非同步 ASP.NET Web 服務要求的零長度內容回應時，傳回 ArgumentNullException 例外狀況錯誤訊息：「值不能為 null」</a> 建議用於 Microsoft .NET Framework 2.0 SP2。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Outlook</p></td>
<td><ul>
<li><p>使用者可以將 IRM 保護套用至 Outlook 中的郵件。從 Outlook 2003 開始，已支援受 IRM 保護之訊息的 AD RMS 範本。</p></li>
<li><p>Outlook保護規則會Exchange 2010和Outlook 2010 」 功能。舊版的Outlook不支援這項功能。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Exchange ActiveSync</p></td>
<td><ul>
<li><p>支援 Exchange ActiveSync 通訊協定 14.1 版的裝置 (包括 Windows Mobile 裝置) 可支援 Exchange ActiveSync 中的 IRM。裝置上的行動電子郵件應用程式必須支援 Exchange ActiveSync 通訊協定 14.1 版中定義的 <strong>RightsManagementInformation</strong> 標記。在 Exchange 2013 中，Exchange ActiveSync 中的 IRM 可讓使用者使用支援裝置來檢視、回覆、轉寄及建立受 IRM 保護的訊息，而且使用者不需要將裝置連接到電腦以啟動它進行 IRM。如需詳細資訊，請參閱 <a href="information-rights-management-in-exchange-activesync-exchange-2013-help.md">Exchange ActiveSync 中的資訊版權管理</a>。</p></li>
</ul></td>
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
<td><em>AD RMS叢集</em>這個詞彙是用來描述組織中的 AD RMS 部署，包括單一伺服器部署。AD RMS 是一種 Web 服務。該服務不需要您設定 Windows Server 容錯移轉叢集。為達到高可用性與負載平衡，您可在叢集中部署多個 AD RMS 伺服器，並使用網路負載平衡。</td>
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
<td>在實際執行環境中，不支援將 AD RMS 和 Exchange 安裝在相同的伺服器上。</td>
</tr>
</tbody>
</table>


Exchange 2013Microsoft Office 檔案格式支援的 IRM 功能。您可以藉由部署自訂保護裝置延長 IRM 保護為其他檔案格式。更多自訂保護裝置的相關資訊，如資訊保護及控制協力廠商的[獨立軟體廠商](https://go.microsoft.com/fwlink/p/?linkid=210336)。

回到頁首

## 設定和測試 IRM

您在 Exchange 2013 中必須使用 Exchange 管理命令介面來設定 IRM 功能。若要設定個別的 IRM 功能，請使用 [Set-IRMConfiguration](https://technet.microsoft.com/zh-tw/library/dd979792\(v=exchg.150\)) Cmdlet。您可以啟用或停用內部訊息的 IRM、傳輸解密、日誌報告解密、Exchange 搜尋，以及 Outlook Web App。如需設定 IRM 功能的詳細資訊，請參閱[資訊版權管理程序](information-rights-management-procedures-exchange-2013-help.md)。

在設定 Exchange 2013 伺服器之後，您可以使用 [Test-IRMConfiguration](https://technet.microsoft.com/zh-tw/library/dd979798\(v=exchg.150\)) Cmdlet 來執行 IRM 部署的端對端測試。若要在一完成初始 IRM 設定後或持續地驗證 IRM 功能，這些測試會很有用。指令程式會執行下列測試：

  - 檢查 Exchange 2013 組織的 IRM 組態。

  - 檢查 AD RMS 伺服器的版本與 Hotfix 資訊。

  - 透過擷取權限帳戶憑證 (RAC) 和用戶端授權人憑證，驗證是否能啟動 RMS 的 Exchange 伺服器。

  - 從 AD RMS 伺服器取得 AD RMS 權限原則範本。

  - 確定指定的寄件者可以傳送受 IRM 保護的訊息。

  - 為指定的收件者擷取超級使用者使用授權。

  - 為指定的收件者取得先期授權。

回到頁首

## 使用權限管理連接器擴大權限管理

Microsoft 權限管理連接器 (RMS 連接器) 是選用應用程式，可增強您的 Exchange 2013 伺服器的資料保護，方法是使用雲端式的 Microsoft 權限管理服務。安裝 RMS 連接器之後，它可在資訊的週期期間提供持續的資料保護，並且因為這些是可自訂的服務，所以您可以定義所需的保護層級。例如，您可以限制特定使用者才能進行電子郵件存取，或針對特定郵件設定僅限檢視權限。

若要深入了解 RMS 連接器及其安裝方式，請參閱[權限管理連接器](https://technet.microsoft.com/en-us/library/dn375964.aspx)。

