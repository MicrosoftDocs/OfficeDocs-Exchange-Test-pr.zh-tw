---
title: '自動探索服務: Exchange 2013 Help'
TOCTitle: 自動探索服務
ms:assetid: b03c0f21-cbc2-4be8-ad03-73a7dac16ffc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124251(v=EXCHG.150)
ms:contentKeyID: 50554050
ms.date: 01/01/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 自動探索服務

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

瞭解 Microsoft Exchange 2013 的 Exchange 自動探索服務。您將瞭解 Exchange 自動探索服務及其運作方式，以及有哪些部署選項。

MicrosoftExchange 2013 包含一個名為自動探索服務的服務。本主題提供此服務概觀，說明其運作方式及其如何設定 Outlook 用戶端，以及在郵件環境中部署自動探索服務時有哪些選項。

自動探索服務會執行下列作業：

  - 自動設定執行 MicrosoftOffice Outlook 2007、Outlook 2010 或 Outlook 2013 的用戶端，以及受支援手機的使用者設定檔設定。執行 Windows Mobile 6.1 或更新版本的手機皆受支援。如果您的手機不是 Windows 行動電話，請查看您的行動電話文件，了解是否支援此服務。

  - 對於連接至 Exchange 郵件環境的 Outlook 2007、Outlook 2010 或Outlook 2013 用戶端，會提供 Exchange 功能的存取權。

  - 會利用使用者的電子郵件地址及密碼，將設定檔設定提供給 Outlook 2007、Outlook 2010 或 Outlook 2013 用戶端及支援的行動電話。若 Outlook 用戶端已加入網域，則會利用使用者的網域帳戶。

**目錄**

自動探索服務概觀

自動探索服務的運作方式

自動探索服務的部署選項

設定適合跨樹系移動的自動探索

## 自動探索服務概觀

自動探索服務讓設定 Outlook 2007、Outlook 2010 或 Outlook 2013 和一些行動電話變得更加容易。您無法使用自動探索服務來搭配早於 Outlook 的 Office Outlook 2007 版本。在舊版的 Microsoft Exchange (Exchange 2003 SP2 或更早版本) 與 Outlook (Outlook 2003 或更早版本) 中，您必須手動設定所有使用者設定檔以存取 Exchange。如果郵件環境發生變更，就需要額外的工作來管理這些設定檔。否則，Outlook 用戶端將無法正常運作。

透過自動探索服務，Outlook 找到一個新的連線點，此連線點是由使用者信箱 GUID + @ + 使用者主要 SMTP 位址的網域部分所組成。自動探索服務會將下列資訊傳回用戶端：

  - 使用者的顯示名稱

  - 內部及外部連線的不同連線設定

  - 使用者郵件信箱伺服器的位置。

  - 管理空閒/忙碌資訊、整合通訊及離線通訊錄等功能之各種 Outlook 功能的 URL

  - Outlook Anywhere 伺服器設定。

當使用者的 Exchange 資訊變更時，Outlook 會使用自動探索服務自動重設使用者的設定檔。例如，若使用者的信箱移動或是用戶端無法連接至使用者的信箱或可用的 Exchange 功能，Outlook 就會連絡自動探索服務，並自動更新使用者的設定檔，以使其具有連接至信箱及 Exchange 功能所需的資訊。

回到頁首

## 自動探索服務的運作方式

在執行 Exchange 2013 的電腦上安裝用戶端存取伺服器時，網際網路資訊服務 (IIS) 中的預設網站底下會建立名為 Autodiscover 的預設虛擬目錄。在下列情況中，此虛擬目錄會處理來自 Outlook 2007、Outlook 2010 和 Outlook 2013 用戶端及受支援行動電話的自動探索服務要求：

  - 設定或更新使用者帳戶時

  - Outlook 用戶端定期檢查 Exchange Web 服務 URL 是否有變更時

  - Exchange 郵件環境中發生底層網路連線變更時

另外，在安裝用戶端存取伺服器的伺服器上會建立稱為服務連線點 (SCP) 的新 Active Directory 物件。

SCP 物件會包含樹系之自動探索服務 URL 的授權清單。您可以使用 **Set-ClientAccessServer** Cmdlet 更新 SCP 物件。如需詳細資訊，請參閱[Set-ClientAccessServer](https://technet.microsoft.com/zh-tw/library/bb125157\(v=exchg.150\))。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在執行 <strong>Set-ClientAccessServer</strong> Cmdlet 前，請確定用戶端存取伺服器上已驗證的使用者帳戶，具有該 SCP 物件的讀取權限。如果使用者的權限不正確，將無法搜尋及讀取項目。</td>
</tr>
</tbody>
</table>


如需 SCP 物件的詳細資訊，請參閱[使用服務連線點進行發佈](https://go.microsoft.com/fwlink/p/?linkid=72744)。

若是外部存取或使用 DNS，用戶端會利用使用者電子郵件地址的主要 SMTP 網域位址，在網際網路上尋找自動探索服務。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您必須在 DNS 中提供主機服務 (SRV) 資源記錄，讓 Outlook 用戶端使用 DNS 探索自動探索服務。如需相關資訊，請參閱您的 Windows 文件內有關 DNS 設定資訊，並參閱<a href="https://go.microsoft.com/fwlink/p/?linkid=85214">白皮書：Exchange 2007 自動探索服務</a>。</td>
</tr>
</tbody>
</table>


視是否在個別站台上設定自動探索服務而定，自動探索服務 URL 會是 https://\<*smtp-address-domain*\>/autodiscover/autodiscover.xml 或 https://autodiscover.\<*smtp-address-domain*\>/autodiscover/autodiscover.xml，其中 ://\<*smtp-address-domain*\> 是主要 SMTP 網域位址。例如，如果使用者的電子郵件地址是 tony@contoso.com，則主要 SMTP 網域位址是 .contoso.com。當用戶端連接至 Active Directory時，用戶端會尋找安裝期間所建立的 SCP 物件。在包含多部 Client Access Server 的部署中，會針對每一部 Client Access Server 建立一個自動探索 SCP 物件。SCP 物件包含 *ServiceBindingInfo* 屬性，此屬性含有 Client Access Server 的網域全名 (FQDN)，其格式為 https://CAS01/autodiscover/autodiscover.xml，其中 CAS01 為 Client Access Server 的 FQDN。利用使用者認證，Outlook 2007、Outlook 2010 或 Outlook 2013 用戶端會驗證 Active Directory，並搜尋自動探索 SCP 物件。在用戶端取得並列舉自動探索服務的執行個體之後，用戶端會連接至列舉清單中的第一部 Client Access Server，並取得格式為 XML 資料的設定檔資訊，此設定檔資訊為連接至使用者的信箱及可用的 Exchange 功能所需的資訊。

回到頁首

## 自動探索服務的部署選項

自動探索服務必須正確部署和設定，Outlook 2007、Outlook 2010 和 Outlook 2013 用戶端才能自動連接到 Exchange 功能，例如離線通訊錄、可用性服務及整合通訊 (UM)。部署自動探索服務只是確保 Exchange、Outlook 2007 或 Outlook 2010 用戶端可存取 Outlook 2013 服務 (例如可用性服務) 的其中一個步驟。

## 設定適合跨樹系移動的自動探索

自動探索服務可以針對從某個已從 Outlook 樹系移至另一個樹系的信箱，向連線端的 Exchange 用戶端提供其使用者設定檔資訊。若要這樣做，您必須同時在使用者信箱所在的原始樹系與目標樹系中使用 **New-MailUser** Cmdlet 來設定擁有郵件功能的使用者。在來源樹系中，您應在 Cmdlet 中使用 *ExternalEmailAddress* 參數來指定目標樹系中的新信箱郵件地址。如需詳細資訊，請參閱[New-MailUser](https://technet.microsoft.com/zh-tw/library/aa996335\(v=exchg.150\))。

在您設定擁有郵件功能的使用者時，原始樹系中的自動探索服務，會將驗證使用者重新導向至目標樹系中新的電子郵件地址。連線端的 Outlook 用戶端，則會被重新導向至目標樹系中已經移動信箱的用戶端存取伺服器。

回到頁首

