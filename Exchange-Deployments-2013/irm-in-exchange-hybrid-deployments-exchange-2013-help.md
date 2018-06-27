---
title: 'Exchange 混合式部署中的 IRM: Exchange 2013 Help'
TOCTitle: Exchange 混合式部署中的 IRM
ms:assetid: ba6ec48b-8f79-4807-b74b-fd442bbbe82f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ659052(v=EXCHG.150)
ms:contentKeyID: 50474706
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 混合式部署中的 IRM

 


_**適用版本：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：** 2016-12-09_


**摘要：** IRM 在 Exchange 混合式環境中如何運作，以及如何設定 IRM 以在 Exchange Online 與您的內部部署 Exchange 伺服器之間運作。

資訊版權管理 (IRM) 可針對電子郵件訊息和附件提供持續性的線上及離線保護，以協助您防止敏感資訊外洩。您的 Exchange 內部部署組織以及 Office 365 企業版中的 Exchange Online 皆可支援 IRM。不過，這兩種執行方式之間會有一些差異，且您需要先在 Exchange Online 組織內設定 IRM，才能提供給該組織的使用者使用。

IRM 使用 Active Directory Rights Management Services (AD RMS)，該服務同時是 Windows Server 2008 和更新版本的元件。AD RMS 可讓使用者建立權限保護的內容 (例如電子郵件訊息和附件)，然後控制內容的使用方式以及發佈的對象。使用者可指定決定內容使用方式的範本。例如，使用者可指定電子郵件訊息不能轉寄給其他收件者，或者不能複製郵件中的資訊。

深入了解 Exchange 2010 中的 IRM：[瞭解資訊版權管理](https://technet.microsoft.com/zh-tw/library/dd638140\(v=exchg.141\).aspx)。

若要深入了解 Exchange 2013 和 Exchange 2016 中的 IRM，請參閱[資訊版權管理](https://technet.microsoft.com/zh-tw/library/dd638140\(v=exchg.150\))。

若要深入了解 AD RMS，請參閱 [Active Directory Rights Management Services 概觀](http://go.microsoft.com/fwlink/p/?linkid=215243)。

## IRM 在 Exchange 內部部署和 Exchange Online 之間的差異

內部部署 Exchange 組織中可用的 IRM 功能與 Exchange Online 組織中可用的功能可能不相同。下表提供每個組織中可用的特性與功能摘要。(若要深入了解這些功能，請參閱[資訊版權管理](https://technet.microsoft.com/zh-tw/library/dd638140\(v=exchg.150\)))

### 可用的 IRM 功能

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>可在 Exchange 2007 和更早版本中使用</th>
<th>可在 Exchange 2010 中使用</th>
<th>可在 Exchange Online 和 Exchange 2013 以及更新版本中使用</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 中的手動郵件保護</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>Outlook Web App 中的手動郵件保護</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>在 Outlook 中檢視受 IRM 保護的郵件</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>在 Outlook Web App 中檢視受 IRM 保護的郵件</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>IRM 預先授權代理程式</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>RMS 原則範本</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>傳輸解密</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>日誌報告解密</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>Exchange 搜尋及探索解密</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>自動 Outlook 保護規則</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>自動傳輸保護規則</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
</tbody>
</table>


## 混合式部署中的 IRM

Exchange 會在 Active Directory 樹系中使用 AD RMS 伺服器，該樹系中已安裝 Exchange 伺服器。針對您的內部部署 Exchange 伺服器，則會使用內部部署 AD RMS。針對您的 Exchange Online 組織，則會使用在 Office 365 資料中心所維護的 AD RMS 伺服器。每個 Exchange 組織使用的 AD RMS 組態都是獨立於其他 AD RMS 部署之外。

AD RMS 組態與 IRM 組態不會自動在您的內部部署 Exchange 組織與 Exchange Online 組織之間複寫。您定義的任何 AD RMS 範本都不會自動複製到 Exchange Online 組織中。如果您要讓相同的 AD RMS 範本可在 Exchange Online 組織中使用，您必須手動將範本從內部部署組織匯出，然後將其套用至 Office 365 組織。請參閱本主題稍後的設定混合式部署中的 IRM。

## 使用者經驗

套用至使用者的 IRM 組態會視使用者所使用的用戶端與使用者信箱的位置而定。下表顯示使用者將使用的 AD RMS 伺服器。

### Active AD RMS 伺服器

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>用戶端</th>
<th>內部部署信箱</th>
<th>Exchange Online 信箱</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 桌面用戶端</p></td>
<td><p>內部部署 AD RMS</p></td>
<td><p>內部部署 AD RMS</p></td>
</tr>
<tr class="even">
<td><p>網頁型 Outlook</p></td>
<td><p>內部部署 AD RMS</p></td>
<td><p>Exchange Online AD RMS</p></td>
</tr>
<tr class="odd">
<td><p>ActiveSync 裝置</p></td>
<td><p>內部部署 AD RMS</p></td>
<td><p>Exchange Online AD RMS</p></td>
</tr>
</tbody>
</table>


根據您在內部部署和 Exchange Online 組織中設定的 AD RMS 組態，使用 Outlook 2007 和 網頁型 Outlook 的使用者可能會看見不同的 AD RMS 範本。基於此原因，我們強烈建議您在內部部署和 Exchange Online 組織中都套用相同的範本。

無論信箱位於內部署或 Exchange Online 組織中，Outlook 用戶端使用者的 IRM 體驗都不會有所差異。

信箱位於 網頁型 Outlook 內部部署伺服器的 Exchange 使用者在安裝 Internet Explorer 的權限管理增益集之後，只能開啟有權限保護的郵件。他們無法回覆或建立新的權限保護郵件。

信箱位於 Exchange Online 的 網頁型 Outlook 使用者可開啟權限保護郵件而不需要任何其他軟體，並且可以回覆及建立新的權限保護郵件。

## 伺服器功能

內部部署 Exchange 伺服器會使用 AD RMS 預先授權代理程式來解密權限保護郵件，因此使用者在開啟這些郵件時不需要提供認證。內部部署 Exchange 伺服器會與內部部署 AD RMS 伺服器聯繫以檢查使用原則和權限，並要求將郵件解密的授權。

Exchange Online 組織可提供數種利用 Exchange Online AD RMS 的其他 IRM 相關功能。這些功能 (例如日誌報告解密) 可將權限保護郵件的內容提供給 Exchange 服務以進行其他的處理。例如，已解密的日誌郵件內容可與原始權限保護郵件一併儲存，以利於探索作業的進行。此外，IRM 範本可使用 Outlook 保護規則或傳輸規則自動套用至郵件中，以確保這些郵件能符合與資訊保護有關的組織原則。

## 設定混合式部署中的 IRM

Exchange 中的 IRM 會取決於部署在 Active Directory 樹系的 AD RMS (Exchange 伺服器位於此樹系中)。AD RMS 組態不會自動在內部部署與 Exchange Online 組織之間進行同步處理。您必須從內部部署 AD RMS 伺服器手動匯出稱為受信任發行網域 (TPD) 的 AD RMS 組態，然後將組態匯入 Exchange Online 組織。TPD 包含 AD RMS 組態，其中包括 Exchange Online 組織在使用 IRM 時所需要的範本。

若要深入了解，請參閱 [AD RMS 受信任發行網域考量](http://go.microsoft.com/fwlink/p/?linkid=215244) 。

除了將內部部署 AD RMS 組態套用至 Exchange Online 組織，您還必須確認內部部署網路以外的 Outlook 和 ActiveSync 用戶端能夠與您的 AD RMS伺服器聯繫。如果您要讓這些用戶端存取內部部署網路以外的權限保護郵件，就必須執行此作業。

在設定內部部署網路並匯出 TPS 資料之後，您將需要匯入 TPD 資料並啟用 IRM 以設定 Exchange Online 組織。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ150559.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>任何時候當您要修改內部部署 AD RMS 組態時，都必須手動將新組態套用至 Exchange Online 組織。若要這樣做，請將 TPD 資料從您的內部部署 AD RMS 伺服器匯出，然後將其匯入 Exchange Online 組織。</td>
</tr>
</tbody>
</table>


## 如何在 Exchange 混合式部署中設定 IRM

如果您在內部部署 Exchange 組織中使用 IRM，並要讓 Exchange Online 使用者也使用 IRM，您必須執行下列動作：

1.  設定內部部署 Active Directory Rights Management Services (AD RMS) 伺服器。

2.  在 Exchange Online 組織中啟用 IRM。

3.  將匯入的 AD RMS 範本發佈給 Exchange Online 組織中的使用者。

## 我如何設定內部部署 AD RMS 伺服器？

若要在混合式部署中設定 IRM，您需要使用 Windows PowerShell 來存取您的內部部署 AD RMS 伺服器。若要深入了解，請參閱：[使用 Windows PowerShell 管理 AD RMS](http://go.microsoft.com/fwlink/p/?linkid=214938)

執行下列動作，從您的內部部署 AD RMS 伺服器匯出信任發行網域 (TPD) 資料，然後為外部用戶端設定 AD RMS 伺服器的存取權。

1.  將 TPD 資料從內部部署組織匯出。若要深入了解，請參閱：[匯出信任發行網域](http://go.microsoft.com/fwlink/p/?linkid=214942)

2.  設定從外部用戶端對 AD RMS 伺服器的存取。若要深入了解，請參閱：[新增外部網路叢集 URL](http://go.microsoft.com/fwlink/p/?linkid=214945)

## 如何在 Exchange Online 組織中啟用 IRM？

從您的內部部署 AD RMS 伺服器匯出 TPD 資料後，您需要將該資料匯入到 Exchange Online 組織，然後再啟用 IRM。

1.  在 Exchange Online 組織中，匯入 TPD 資料。
    
        Import-RMSTrustedPublishingDomain -FileData $( [Byte[]] (Get-Content -Encoding Byte -Path "<Path to exported TPD file>" -ReadCount 0))

2.  在 Exchange Online 組織中啟用 IRM。
    
        Set-IRMConfiguration -InternalLicensingEnabled $True

## 如何在 Exchange Online 組織中發佈 AD RMS 範本？

在 Exchange Online 組織中啟用 IRM 後，您必須發佈匯入的 AD RMS 範本。下列 Exchange Online 使用者和功能會使用 AD RMS 範本：

  - 網頁型 Outlook 使用者

  - Exchange ActiveSync 使用者

  - 傳輸規則

  - 日誌報告解密

  - Outlook 保護規則

<!-- end list -->

1.  在 Exchange Online 組織中，擷取 AD RMS 範本的清單。
    
        Get-RMSTemplate -Type All

2.  將 AD RMS 範本發佈給 Exchange Online 組織中的使用者和功能。
    
        Set-RMSTemplate <template name> -Type Distributed
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ150559.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您無法修改「不要轉寄」AD RMS 範本。</td>
    </tr>
    </tbody>
    </table>


3.  為每個您要發佈的 AD RMS 範本重複步驟 2。

## 如何才能了解運作是否正常？

網頁型 Outlook 使用者應能將 AD RMS 範本套用到新郵件。網頁型 Outlook 和 Exchange ActiveSync 使用者應能讀取已套用 AD RMS 範本的郵件。此外，當您執行 **Get-RMSTemplate** 指令程式時，將會列出從您的內部部署組織匯入的所有 AD RMS 範本。

在 Exchange Online 組織中執行下列命令。

    Get-RMSTemplate 

若要深入了解，請參閱： [Outlook Web App 中的資訊版權管理](https://technet.microsoft.com/zh-tw/library/dd876891\(v=exchg.150\))

