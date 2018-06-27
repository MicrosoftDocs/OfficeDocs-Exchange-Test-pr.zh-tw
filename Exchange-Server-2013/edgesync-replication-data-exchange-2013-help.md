---
title: 'EdgeSync 複寫資料: Exchange 2013 Help'
TOCTitle: EdgeSync 複寫資料
ms:assetid: c7dd137d-7ed4-4f16-9895-f354c449cf9b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb232177(v=EXCHG.150)
ms:contentKeyID: 61180457
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# EdgeSync 複寫資料

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

當您部署 Edge Transport Server 時，該伺服器沒有 Active Directory 的存取權。為了執行收件者查閱及安全清單彙總工作，及使用相互傳輸層安全性 (MTLS) 驗證來實作網域安全性，Edge Transport Server 需要取得 Active Directory 中的資料。此資料是利用 EdgeSync 複寫到 Edge Transport Server，而 Edge Transport Server 會以 Active Directory 輕量型目錄服務 (AD LDS) 儲存所有複寫的資訊。

本主題著重於在 Active Directory 站台訂閱的 Edge Transport Server 上從 Active Directory 複寫到 AD LDS 的資料。若要深入了解 EdgeSync 和 Edge 訂閱，請參閱 [Edge 訂閱](edge-subscriptions-exchange-2013-help.md)。

有四種類型的資料會複寫到 AD LDS 並由 Edge Transport Server 使用：

Edge Subscription information

Configuration information

Recipient information

Topology information

## Edge 訂閱資訊

Exchange 2013 會延伸 Active Directory 和 AD LDS 兩種架構，以提供 **ms-Exch-ExchangeServer** 物件的屬性，來代表控制 EdgeSync 同步處理程序所需的資料。這些屬性提供三個功能給 EdgeSync：

  - 自動佈建和維護認證，協助保護 Mailbox Server 與訂閱的 Edge Transport Server 之間的 LDAP 連線。

  - 對同步處理鎖定和租用處理程序進行仲裁，確保一次只有一部伺服器會嘗試與個別 Edge Transport Server 進行同步處理。如需鎖定和租用處理程序的詳細資訊，請參閱[Edge 訂閱](edge-subscriptions-exchange-2013-help.md)。

  - 最佳化 EdgeSync 同步處理以維護目前同步處理狀態的記錄。輕鬆地檢視同步處理狀態，有助於避免過多的手動同步處理。

下表列出 Edge 訂閱特有的架構延伸模組。指派給這些屬性的值是由 Edge 訂閱和 EdgeSync 維護；這些值不適合以手動方式編輯。

### Edge 訂閱架構延伸模組

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>屬性名稱</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ms-Exch-Server-EKPK-Public-Key</strong></p></td>
<td><p>伺服器正在使用之憑證的目前公開金鑰。此值由 Edge Transport Server 和 Mailbox Server 所儲存。公開金鑰用來加密可在 LDAP 與 SMTP 通訊期間用於驗證伺服器的認證。</p></td>
</tr>
<tr class="even">
<td><p><strong>ms-Exch-EdgeSync-Credential</strong></p></td>
<td><p>EdgeSync 用來與 AD LDS 建立已驗證 LDAP 工作階段的認證清單。在 Mailbox Server 上，這個屬性僅包含 Mailbox Server 用來驗證已訂閱 Edge Transport Server 的認證。在 Edge Transport Server 上，此屬性包含已訂閱之 Active Directory 站台中參與 EdgeSync 同步處理程序的每個 Mailbox Server 的認證。這個屬性只會出現在執行 EdgeSync 同步處理的 Mailbox Server 上以及訂閱的 Edge Transport Server 上。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ms-Exch-Edge-Sync-Lease</strong></p></td>
<td><p>當有多個 Mailbox Server 嘗試複寫到相同的 Edge Transport Server 時，此屬性可用來進行 Mailbox Server 之間的仲裁。</p></td>
</tr>
<tr class="even">
<td><p><strong>ms-Exch-Edge-Sync-Status</strong></p></td>
<td><p>只會出現在 Edge Transport Server 物件上的 AD LDS 中。此屬性可為 AD LDS 執行個體追蹤複寫狀態，而且包含複寫的相關資訊。</p></td>
</tr>
</tbody>
</table>


回到頁首

## 組態資訊

當您為組織訂閱 Edge Transport Server 時，就可以從組織內管理 Edge Transport Server 與 Exchange 組織所共用的組態物件。接著使用 EdgeSync 將這些變更複寫到 Edge Transport Server。此處理程序有助於在涉及郵件處理的所有伺服器之間維護一致組態。

在 Edge Transport Server 上也必須維護 Exchange 組織的組態資料子集。在 EdgeSync 同步處理期間，Edge Transport Server 所需的組態資料會寫入 AD LDS 的組態磁碟分割。寫入 AD LDS 的組態資料包括：

  - **Mailbox Server**   Edge Transport Server 上的本機 AD LDS 儲存區可以使用已訂閱之 Active Directory 站台中每個 Mailbox Server 的網域全名 (FQDN)。此資訊是用來衍生輸入傳送連接器的智慧主機伺服器清單。

  - **公認的網域**   針對 Exchange 組織設定的所有授權網域、內部轉送網域及外部轉送網域，都會寫入 AD LDS。讓 Edge Transport Server 可以使用公認的網域，Exchange 組織就能夠執行網域篩選，並儘早拒絕要進入組織的無效 SMTP 流量。如需公認的網域的相關資訊，請參閱[公認的網域](accepted-domains-exchange-2013-help.md)。

  - **郵件分類**   如果在 Edge Transport Server 上可使用郵件分類，則傳輸代理程式和內容轉換可對周邊網路中的郵件分類採取動作。例如，當附件篩選器代理程式移除附件時，就會套用 \[已移除附件\] 的分類，並將參考文字傳送給 Microsoft Outlook 使用者或 Outlook Web App 使用者，以告知收件者發生什麼情況。開發供協力廠商應用程式使用的代理程式，可以用類似的方式使用郵件分類。

  - **遠端網域**   針對 Exchange 組織設定的所有遠端網域項目都會寫入到 AD LDS。遠端網域項目可控制遠端網域的郵件答錄機郵件設定和郵件格式設定。如需遠端網域的相關資訊，請參閱[遠端網域](remote-domains-exchange-2013-help.md)。

  - **傳送連接器**   依預設，建立 Edge 訂閱時會自動建立傳送連接器，必須有此連接器才能在訂閱 Edge Transport Server 時啟用 Exchange 組織與網際網路之間的端對端郵件流程。任何在 Edge Transport Server 上的傳送連接器都會加以刪除。如果您想要設定其他傳送連接器，可在 Exchange 組織內設定傳送連接器，然後選取 Edge 訂閱作為連接器的來源伺服器。如需詳細資訊，請參閱 [Edge 訂閱](edge-subscriptions-exchange-2013-help.md)。

  - **內部 SMTP 伺服器**   *InternalSMTPServers* 屬性的值同時儲存在 Exchange 組織和本機 Edge Transport Server 的 **TransportConfig** 物件上。在 EdgeSync 同步處理期間，會以 Exchange 組織的此物件上儲存的值，覆寫本機 Edge Transport Server 物件上儲存的值。此屬性可指定內部 SMTP 伺服器的 IP 位址或 IP 位址範圍的清單，列出寄件者識別碼及連線篩選應忽略的 IP 位址。

  - **網域安全清單**   *TLSReceiveDomainSecureList* 和 *TLSSendDomainSecureList* 屬性同時儲存在 Exchange 組織和本機 Edge Transport Server 的 **TransportConfig** 物件上。在 EdgeSync 同步處理期間，會以 Exchange 組織的此物件上儲存的值，覆寫本機 Edge Transport Server 物件上儲存的值。這些屬性指定為相互 TLS 驗證而設定的遠端網域清單。

回到頁首

## 收件者資訊

複寫到 AD LDS 的收件者資訊只包括收件者屬性子集。只會複寫 Edge Transport Server 執行特定反垃圾郵件工作時所需的資料。複寫到 AD LDS 的收件者資訊包括：

  - **收件者**   Exchange 組織中的收件者清單會複寫到 AD LDS。每個收件者都是由指派的 Active Directory GUID 加以識別。如果您將收件者的帳戶設定為拒絕接收組織以外的郵件，則不會將該收件者複寫到 AD LDS。如果您停用或刪除收件者的信箱，該信箱就不會再複寫到 AD LDS。

  - **Proxy 位址**   指派給每個收件者的所有 Proxy 位址都會以雜湊資料的方式複寫到 AD LDS。這是使用安全雜湊演算法 (SHA) 256 的單向雜湊。SHA-256 會產生原始資料的 256 位元郵件摘要。萬一 Edge Transport Server 或 AD LDS 受到危害，將 Proxy 位址儲存為雜湊資料即可幫助保護這項資訊。當 Edge Transport Server 執行收件者查閱反垃圾郵件工作時，會參考 Proxy 位址。

  - **安全寄件者清單、封鎖的寄件者清單及安全收件者清單**   在每個收件者的 Outlook 執行個體中定義的安全寄件者清單、封鎖的寄件者清單及安全收件者清單，都會彙總並複寫到 AD LDS。這些設定儲存在收件者信箱所在的信箱資料庫中。Outlook 使用者安全清單集合結合了使用者的安全寄件者清單、安全收件者清單、封鎖的寄件者清單及外部連絡人的資料。讓 AD LDS 中有可用的安全清單集合資料，Edge Transport Server 就能適當挑選寄件者，減少篩選郵件時產生的額外負荷。此資訊會以雜湊資料的方式傳送。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>雖然安全收件者資料儲存在 Outlook 中，而且可在 Edge Transport Server 上彙總成 AD LDS 執行個體的安全清單集合，但是內容篩選功能不會處理安全收件者資料。</td>
    </tr>
    </tbody>
    </table>


  - **每位收件者反垃圾郵件設定**   您可以使用 **Set-Mailbox** Cmdlet，指派每位收件者的反垃圾郵件閾值設定，它們不同於全組織適用的反垃圾郵件設定。如果您設定每位收件者的反垃圾郵件設定，這些設定會覆寫全組織適用的設定。將這些設定複寫到 AD LDS，就可以在將郵件轉送到 Exchange 組織之前，先考慮每位收件者的設定。此資訊會以雜湊資料的方式傳送。

回到頁首

## 拓撲資訊

拓撲資訊包括新訂閱的 Edge Transport Server 或已移除的 Edge 訂閱的通知。此資料每隔五分鐘會更新一次。

回到頁首

