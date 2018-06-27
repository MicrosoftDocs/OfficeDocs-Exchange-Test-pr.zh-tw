---
title: '就地封存 in Exchange 2013: Exchange 2013 Help'
TOCTitle: 就地封存 in Exchange 2013
ms:assetid: b5e4c0e9-0558-4b90-bc12-f67adbfb59ac
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd979800(v=EXCHG.150)
ms:contentKeyID: 50474033
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 就地封存 in Exchange 2013

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

因為不再需要個人儲存區 (.pst) 檔案，*「就地封存」*(In-Place Archiving) 可協助您重新取得組織郵件資料的控制權，並且讓使用者將郵件儲存到能夠在 MicrosoftOutlook 2010 和更新版本以及 Microsoft OfficeOutlook Web App 中存取的*「封存信箱」*(Archive Mailbox)。

在 Microsoft Exchange Server 2013 中，「就地封存」可為使用者提供不同的儲存位置，用於儲存歷史郵件資料。個人封存是針對信箱使用者啟用的其他信箱 (稱為封存信箱)。Outlook 2007 和更新版本以及 Outlook Web App 使用者可以完整存取其封存信箱。只要使用這些用戶端應用程式，使用者就能檢視封存信箱，並且在主要信箱和封存之間移動或複製郵件。「就地封存」會對使用者呈現一致的郵件資料檢視，並且消除使用者管理 .pst 檔的負擔。

您可以佈建使用者的主要信箱、 另一個信箱資料庫相同的信箱伺服器上為相同的信箱資料庫或同一個Active Directory網站中的另一個信箱伺服器上的信箱資料庫上的使用者的封存。在混合式部署中的Exchange 2010及更新版本，您也可以提供雲端式封存的信箱位於內部部署信箱伺服器上。

**目錄**

Messaging data and .pst files

Client access to archive mailboxes

Delegate access

Moving messages to the archive mailbox

Archive and retention policies

Default MRM policy

Archive quotas

In-Place Archives and other Exchange features

Managing archive mailboxes

## 郵件資料與 .pst 檔

Outlook 使用 .pst 檔儲存位於使用者本機電腦或網路共用上的資料。與離線儲存區 (.ost) 檔案 (Outlook 在 Exchange 快取模式 (離線) 下用來儲存信箱副本以供離線存取) 的不同的是，.pst 檔不會與使用者的 Exchange 信箱同步。如果使用者將郵件移至 .pst 檔，這些郵件就會從信箱中移除。

使用 .pst 檔管理郵件資料可能會導致下列問題：

  - **不受管理的檔案**   一般而言，.pst 檔是由使用者所建立，並且位於其電腦或網路共用上。這些檔案不受組織的管理。因此，使用者可以建立多個包含相同或不同郵件的 .pst 檔，並且將它們儲存到不同位置，而不受組織控制。

  - **探索成本增加** 法律訴訟和某些公司或其他商業或法規需求有時會導致探索要求發生。尋找位於使用者電腦上 .pst 檔中的郵件資料可能會造成相當昂貴的人力成本。由於追蹤不受管理的 .pst 檔可能相當困難，因此在許多情況下可能無法探索 .pst 資料。這種情況可能使您的組織暴露於法律與財務風險中。

  - **無法套用郵件保留原則**   郵件保留原則無法套用至位於 .pst 檔中的郵件。因此，根據商業或適用的法規而定，您的組織可能不符合規定。

  - **資料遭竊的風險** 儲存在 .pst 檔中的郵件資料容易遭竊取。例如，.pst 檔經常儲存在可攜式裝置中，例如膝上型電腦、卸除式硬碟，以及可攜式媒體 (如 USB 磁碟機、CD 和 DVD)。

  - **零散的郵件資料檢視**   將資訊儲存在 .pst 檔中的使用者無法檢視一致的資料。儲存在 .pst 檔中的郵件通常只可於 .pst 檔所在的電腦上使用。因此，若使用者使用另一部電腦上的 Outlook Web App 或 Outlook 存取他們的信箱，就無法存取儲存在 .pst 檔中的郵件。

## 存取封存信箱的用戶端

下表列出可用來存取封存信箱的用戶端應用程式。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>用戶端</th>
<th>存取封存信箱</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2013、Outlook 2010、Outlook 2007 和 Outlook Web App</p></td>
<td><p>是。Outlook 2013、Outlook 2010、Outlook 2007 和 Outlook Web App 使用者可以將項目從主要信箱複製或移動至封存信箱，也可以使用保留原則將項目移至封存。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Outlook 2010 與更新版本和 Outlook 2007 使用者可以也複製或將項目從.pst 檔案移到封存信箱。Outlook 2007 使用者需要 2011 年 2 月 Office 2007 累計更新。Outlook 2010 及更新版本及 Outlook 2007 之間存在封存支援的一些差異。如需詳細資訊，請參閱 Exchange 團隊部落格文章，請參閱<a href="https://blogs.technet.com/b/exchange/archive/2010/12/20/3411710.aspx">是維吉尼亞州、 有 Outlook 2007 中的 Exchange 2010 封存支援</a>。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p>Exchange ActiveSync</p></td>
<td><p>否</p></td>
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
<td>就地封存 premium 功能，且需要 Exchange 企業用戶端存取授權 (CAL)。如需如何授權 Exchange 的詳細資訊，請參閱<a href="https://go.microsoft.com/fwlink/?linkid=237292">Exchange Server 授權</a>。如需詳細資訊 Outlook 存取封存信箱所需的版本，請參閱<a href="https://go.microsoft.com/fwlink/?linkid=237276">個人封存和保留原則的授權需求</a>。</td>
</tr>
</tbody>
</table>


即使已設定為使用 Exchange 快取模式 (離線)，Outlook 也不會在使用者的電腦上建立封存信箱的本機副本。使用者只能在線上模式下存取封存信箱。

## 委派存取

*「委派存取」*是在為某個使用者或一組使用者提供其他使用者信箱的存取權時發生。提供委派存取的案例有很多，包括：

  - 為一個或多個使用者存取不再受僱於組織的使用者信箱的存取權。在此情況下，被指定委派存取的使用者包括已離開使用者的經理或主管，或其他將承接已離開使用者職務的使用者。

  - 為一個或多個使用者提供存取共用信箱的存取權。

  - 為行政助理提供其所協助之管理人員信箱的存取權。

在Exchange 2013、 信箱指派完整存取權限時要指派權限委派並也可以存取使用者的封存。代理人必須使用 Outlook 來存取信箱，並他們必須連線至Exchange 2010 SP1 或更新版本進行自動探索的用戶端存取伺服器。自動探索是Exchange提供服務的自動設定 Outlook 用戶端的組態設定。代理人使用 Outlook 來存取Exchange 2013信箱，當主要信箱和封存的他們可以存取都是從 Outlook 顯示。

## 將郵件移至封存信箱

將郵件移至封存信箱的方法有很多種：

  - **手動移動或複製郵件** 信箱使用者可以手動將郵件從他們的主要信箱或 .pst 檔移動或複製到他們的封存信箱。封存信箱在 Outlook 和 Outlook Web App 中會顯示為另一個信箱或 .pst 檔。

  - **使用收件匣規則移動或複製郵件**   信箱使用者可以在 Outlook 或 Outlook Web App 中建立收件匣規則，自動將郵件移至封存信箱中的某個資料夾。若要深入了解，請參閱[了解收件匣規則](http://help.outlook.com/zh-tw/140/bb899620.aspx)。

  - **使用保留原則移動郵件** 您可以使用保留原則將郵件自動移至封存。使用者也可以對移至封存的郵件套用個人標記。如需封存和保留原則的詳細資訊，請參閱本主題稍後的Archive and retention policies。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>個人標記只有在 Outlook Web App 以及 Outlook 2010 和更新版本中提供。</td>
    </tr>
    </tbody>
    </table>


  - **匯入訊息從.pst 檔案**  在Exchange 2013，您可以使用信箱匯入要求至使用者的封存或主要信箱匯入訊息從.pst 檔案。如需詳細資訊，請參閱[信箱匯入及匯出要求](mailbox-import-and-export-requests-exchange-2013-help.md)。您也可以使用 PST 擷取工具在組織中搜尋的電腦上的.pst 檔案和.pst 檔案將資料匯入使用者的封存。

## 封存和保留原則

在 Exchange 2013 中，您可以將封存原則套用至信箱，該信箱會在指定的期間之後，自動將使用者主要信箱的郵件移到封存信箱。封存原則是透過建立使用 \[移至封存\] 保留動作的保留標記所實作。

郵件會移至封存信箱中的資料夾，而該資料夾名稱與主要信箱中的來源資料夾名稱相同。如果封存信箱中不存在具有相同名稱的資料夾，則會在 \[受管理的資料夾助理員\] 移動郵件時建立該資料夾。在封存信箱中重新建立相同的資料夾階層可讓使用者輕鬆地尋找郵件。

若要深入了解保留原則、保留標記和 \[移至封存\] 保留動作，請參閱[保留標記和保留原則](retention-tags-and-retention-policies-exchange-2013-help.md)。

## 預設 MRM 原則

Exchange 2013 安裝程式會建立 \[預設 MRM 原則\] 這項預設封存和保留原則。此原則內含具有 \[移至封存\] 動作的保留標記，如下表中所示。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在 Exchange 2010 中，Exchange 安裝程式所建立的預設封存和保留原則名為 <strong>[預設封存和保留原則]</strong>。</td>
</tr>
</tbody>
</table>



<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>保留標記名稱</th>
<th>標記類型</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>預設 2 年移至封存</strong></p></td>
<td><p>預設 (DPT)</p></td>
<td><p>郵件會在二年後自動移到封存信箱。這項原則會套用至未明確套用保留標記或繼承自資料夾的整個信箱中的項目。</p></td>
</tr>
<tr class="even">
<td><p><strong>個人 1 年移至封存</strong></p></td>
<td><p>個人</p></td>
<td><p>郵件會在一年後自動移到封存信箱。</p></td>
</tr>
<tr class="odd">
<td><p><strong>個人 5 年移至封存</strong></p></td>
<td><p>個人</p></td>
<td><p>郵件會在 5 年後自動移到封存信箱。</p></td>
</tr>
<tr class="even">
<td><p><strong>個人永不移至封存</strong></p></td>
<td><p>個人</p></td>
<td><p>郵件永不會移至封存信箱。</p></td>
</tr>
<tr class="odd">
<td><p><strong>可復原的項目 14 天移至封存</strong></p></td>
<td><p>可復原的項目資料夾</p></td>
<td><p>郵件會從使用者主要信箱的 [可復原的項目] 資料夾移至封存信箱的 [可復原的項目] 資料夾。使用者若要在封存中復原刪除的郵件，必須使用封存信箱上的 [復原刪除的郵件] 進行。</p></td>
</tr>
</tbody>
</table>


如果為信箱使用者啟用「就地封存」，而該信箱尚未指派保留原則，則會自動為其指派預設封存和保留原則。在受管理的資料夾助理員處理信箱之後，這些標記就可以供使用者使用，接著使用者就可以標記要移至封存信箱的資料夾或郵件。依預設，整個信箱的電子郵件會在兩年後移動。

為使用者提供封存信箱之前，建議您通知使用者將會套用至其信箱之封存原則的相關資訊，並提供後續的教育訓練或符合其需求的文件。其中應該包含下列詳細資料：

  - 可在封存中使用的功能，預設封存和保留原則。

  - 郵件何時會自動移至封存的相關資訊。

  - 封存信箱中建立之資料夾階層的相關資訊。

  - 如何套用個人標記 (顯示於 Outlook 和 Outlook Web App 的 \[封存原則\] 功能表中)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您將保留原則套用至擁有封存信箱的使用者，保留原則會取代預設 MRM 原則。您可以建立一或多個擁有 [移至封存] 動作的保留標記，然後將標記連結至保留原則。您也可以將預設的 [移至封存] 標記 (安裝程式所建立，並連結至預設 MRM 原則) 新增至您所建立的任何保留原則。</td>
</tr>
</tbody>
</table>


規範與封存在 Outlook 2010 和更新版本的相關資訊，請參閱[規劃規範與封存在 Outlook 2010](https://go.microsoft.com/fwlink/?linkid=210902)。

## 封存配額

封存信箱的設計在於讓使用者於主要信箱外部儲存歷史郵件資料。使用者時常因為信箱儲存配額不足，以及超過這些配額時強制執行的限制而使用 .pst 檔。例如，使用者的信箱大小超過 \[禁止傳送配額\] 時，就無法傳送郵件。同樣地，使用者的信箱大小超過 \[禁止收發配額\] 時，就無法傳送和接收郵件。

為了免除對 .pst 檔的需要，您可以對封存信箱提供符合使用者需求的儲存限制。不過，您可能想要保留對儲存配額和封存信箱增加的控制，以便有助於監控成本和擴充。

為了有助於這項控制，您可以為封存信箱設定*封存警告配額*和*封存配額*。當封存信箱超過指定的封存警告配額時，會在應用程式事件記錄中記錄警告事件。當封存信箱超過指定的封存配額時，郵件就不會再移至封存，此時會在應用程式事件記錄中記錄警告事件，並且會傳送配額訊息給信箱使用者。根據預設，Exchange 2013 中的封存警告配額設為 45 GB，而封存配額設為 50 GB。

下表列出達到封存警告配額和封存配額時傳送的記錄事件和警告訊息。


<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>配額</th>
<th>事件識別碼</th>
<th>類型</th>
<th>來源</th>
<th>類別</th>
<th>郵件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>封存警告配額</p></td>
<td><p>10022</p></td>
<td><p>警告</p></td>
<td><p>MSExchangeMailboxAssistants</p></td>
<td><p>受管理的資料夾助理員</p></td>
<td><p>封存信箱 '&lt;Display Name&gt;:&lt;GUID&gt;:&lt;Mailbox Database&gt;:&lt;Server FQDN&gt;' 超出封存警告配額 '&lt;Archive warning quota&gt;'。封存信箱大小為 '&lt;Size&gt;' 位元組。</p></td>
</tr>
<tr class="even">
<td><p>封存配額</p></td>
<td><p>8537</p></td>
<td><p>警告</p></td>
<td><p>MSExchangeIS</p></td>
<td><p>一般</p></td>
<td><p>&lt;Legacy DN&gt; 的封存信箱已超出封存信箱大小的上限。您無法將郵件複製或移入封存信箱。所有將郵件移至封存信箱的訊息保留動作都會失敗，且主要信箱中可能會有附帶逾期保留標記的郵件，直到封存信箱的大小縮回到最大限制的範圍內。有關封存信箱的情況，需通知信箱的擁有者。</p></td>
</tr>
</tbody>
</table>


## 就地封存和其他 Exchange 功能

本節說明「就地封存」和各種 Exchange 功能之間的功能運作：

  - **Exchange 搜尋**快速搜尋郵件的能力與封存信箱變得更加重要。在主要和封存信箱之間執行 Exchange 搜尋沒有什麼差別。兩種信箱中的內容都會進行索引。由於未在使用者的電腦上對封存信箱進行快取 (即使是在 Exchange 快取模式下使用 Outlook)，封存的搜尋結果一定是由 Exchange 搜尋所提供。在 Outlook 2010 和更新版本以及 Outlook Web App 中搜尋整個信箱時，搜尋結果會包含使用者的主要和封存信箱。

  - **就地 eDiscovery**   探索管理員執行就地 eDiscovery 搜尋時，也會搜尋使用者的封存信箱。從 Exchange 系統管理中心 (EAC) 建立探索搜尋時，並沒有提供排除封存信箱的選項。使用 Exchange 管理命令介面建立探索搜尋時，可以使用 *DoNotIncludeArchive* 參數將封存排除。如需詳細資訊，請參閱 [New-MailboxSearch](https://technet.microsoft.com/zh-tw/library/dd298064\(v=exchg.150\))。若要深入了解，請參閱[就地 eDiscovery](in-place-ediscovery-exchange-2013-help.md)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您無法使用就地 eDiscovery 搜尋中斷連線的信箱。</td>
    </tr>
    </tbody>
    </table>


  - **就地保留和訴訟資料暫留：**當您對信箱進行就地保留或訴訟資料暫留時，會同時保留主要和封存信箱。若要深入了解就地保留和訴訟資料暫留，請參閱[就地保留與訴訟暫止](in-place-hold-and-litigation-hold-exchange-2013-help.md)。

  - **可復原的項目資料夾**封存信箱內含其所擁有的 \[可復原的項目\] 資料夾，受限於主要信箱中相同 \[可復原的項目\] 資料夾的配額。若要深入了解可復原的項目，請參閱[可復原的項目資料夾](recoverable-items-folder-exchange-2013-help.md)。

  - **封存 Exchange 中的 Lync 內容：**   您可以將立即訊息對話和共用的線上會議文件封存到使用者的主要信箱。信箱必須位於 Exchange 2013 信箱伺服器上，而且您的組織中必須已部署 Microsoft Lync 2013。如需詳細資訊，請參閱[與 SharePoint 和 Lync 整合](integration-with-sharepoint-and-lync-exchange-2013-help.md)。

## 管理封存信箱

在 Exchange 2013 中，建立及管理封存信箱會與一般信箱管理工作整合，包括：

  - **建立封存信箱** 您可以在建立信箱時建立封存信箱，或為現有信箱啟用封存信箱。如需詳細資訊，請參閱[管理 Exchange 2013 中的就地封存](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md)。

  - **移動封存信箱**   您可以獨立於主要信箱之外，將使用者的封存信箱移至相同信箱伺服器上的另一個信箱資料庫，或移至另一部伺服器。若要移動使用者的封存信箱，您必須建立信箱移動要求。如需詳細資訊，請參閱[管理內部移動](manage-on-premises-moves-exchange-2013-help.md)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>不支援在不同的 Exchange Server 版本上尋找使用者的信箱和封存。</td>
    </tr>
    </tbody>
    </table>


  - **停用封存信箱：**您可能想要停用使用者的封存信箱以進行疑難排解，或者要將主要信箱移至不支援就地封存的 Exchange 版本。停用封存和停用主要信箱的步驟類似。如需詳細資訊，請參閱[管理 Exchange 2013 中的就地封存](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md)。在內部部署的部署中，停用的封存信箱會保留於信箱資料庫中，直到達到該資料庫的刪除信箱保留期間為止。在此期間，您可以將封存重新與信箱使用者連線。達到刪除信箱保留期間時，就會將中斷連線的封存信箱從信箱資料庫中清除。

  - **擷取信箱統計資料和資料夾統計資料** 您可以使用 *Archive* 參數搭配 [Get-MailboxStatistics](https://technet.microsoft.com/zh-tw/library/bb124612\(v=exchg.150\)) 和 [Get-MailboxFolderStatistics](https://technet.microsoft.com/zh-tw/library/aa996762\(v=exchg.150\)) 指令程式，擷取使用者封存信箱的信箱統計資料和信箱資料夾統計資料。

  - **測試封存連線**   在 Exchange 2013 中，您可以使用 [Test-ArchiveConnectivity](https://technet.microsoft.com/zh-tw/library/hh529914\(v=exchg.150\)) Cmdlet 測試與指定使用者的內部部署或雲端式封存的連線。

