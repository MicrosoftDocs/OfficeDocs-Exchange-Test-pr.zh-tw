---
title: '與 SharePoint 和 Lync 整合: Exchange 2013 Help'
TOCTitle: 與 SharePoint 和 Lync 整合
ms:assetid: 056b29f6-e0e9-4974-b763-002518857a93
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ150480(v=EXCHG.150)
ms:contentKeyID: 50472489
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 與 SharePoint 和 Lync 整合

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

Microsoft Exchange Server 2013包含整合Microsoft SharePoint 2013及Microsoft Lync 2013的許多功能。這些產品提供功能可讓企業 eDiscovery 等使用站台信箱的共同作業案例可能的套件。

## 封存、保留，以及 eDiscovery

封存電子郵件和文件，其保留期間所需的符合法規遵循與業務需求及它們滿足 eDiscovery 要求可以快速搜尋能力十分重要在大多數組織中。Exchange 2013、 SharePoint 2013及Lync Server 2013一起提供整合式封存、 保留和 eDiscovery 功能，讓您保留重要資料就地整個 Exchange 信箱、 SharePoint 文件及網站與封存的 Lync 內容。SharePoint 2013 eDiscovery 中心可讓授權的探索經理跨這些存放區執行 eDiscovery 搜尋的內容、 預覽搜尋結果，並將資料匯出法律檢閱。

## 封存 Exchange 2013 中的 Lync Server 2013 內容

Lync Server 2013 Exchange 2013與組織中部署，您可以設定 Lync 封存的立即訊息和共用的簡報或文件中的使用者Exchange 2013信箱等的線上會議內容。封存Exchange 2013中的 Lync 資料可讓您將保留原則套用至它。封存的 Lync 內容也會呈現任何 eDiscovery 搜尋中。如需 Lync 封存及如何部署的詳細資訊，請參閱下列主題：

  - [規劃封存](https://go.microsoft.com/fwlink/p/?linkid=265005)

  - [部署封存](https://go.microsoft.com/fwlink/p/?linkid=265006)

## 使用 SharePoint 2013 eDiscovery Center 搜尋 Exchange、SharePoint，以及 Lync 資料

Exchange 2013允許SharePoint 2013搜尋使用同盟搜尋 API 的 Exchange 信箱內容。SharePoint 2013提供 eDiscovery 中心來讓授權的人員才能執行 eDiscovery。Microsoft Search Foundation 提供Exchange 2013及SharePoint 2013常見編製索引和搜尋基礎結構，並讓您以兩個應用程式都使用相同的查詢語法。這可確保在SharePoint 2013執行 eDiscovery 搜尋會傳回相同Exchange 2013內容為使用中Exchange 2013的就地 eDiscovery 執行相同的搜尋。SharePoint 2013 eDiscovery 中心也可讓您匯出 eDiscovery 搜尋，包括匯出至 PST 檔案的Exchange 2013內容中傳回的內容。

如需詳細資料，請參閱下列主題：

  - [就地 eDiscovery](in-place-ediscovery-exchange-2013-help.md)

  - [就地保留與訴訟暫止](in-place-hold-and-litigation-hold-exchange-2013-help.md)

  - [在 SharePoint 2013 中設定 eDiscovery](https://go.microsoft.com/fwlink/p/?linkid=257727)

  - [What's new in SharePoint Server 2013 的 eDiscovery](https://go.microsoft.com/fwlink/?linkid=275091)

  - [設定 Exchange for SharePoint eDiscovery Center](configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md)

## 網站信箱

許多組織資訊位於兩個不同的存放區集Microsoft Exchange中的電子郵件和文件中的SharePoint，以存取他們的兩個不同介面。這會使斷續的使用者經驗及妨礙有效的共同作業。網站信箱允許使用者將Exchange電子郵件和SharePoint文件一起引進的有效地進行共同作業。為使用者站台信箱會做為中央的存檔 cabinet，提供一個檔案專案電子郵件和文件只可存取及編輯網站成員的位置。站台信箱會在 Outlook 2013 中的呈現並授與使用者容易存取電子郵件和文件的所需注意的專案。此外，內容相同的一組可直接從 SharePoint 網站本身。

\[站台信箱涵蓋，內容會保留其所屬的位置。Exchange 儲存電子郵件、 提供使用相同的訊息檢視的電子郵件交談他們自己的信箱使用每天的使用者。SharePoint 會儲存文件、 文件 coauthoring 和版本設定至表格。Exchange 同步處理只是足夠的中繼資料與 SharePoint Outlook （例如文件標題、 上次修改日期、 上次修改作者、 大小） 中建立的文件檢視。

站台信箱佈建且從SharePoint 2013管理。如需詳細資訊，請參閱下列主題：。

  - [網站信箱](site-mailboxes-exchange-2013-help.md)

  - [在 SharePoint Server 2013 中設定網站信箱](https://go.microsoft.com/fwlink/p/?linkid=258264)

## 整合聯絡資料儲存

整合連絡人存放區 (UCS) 是 Microsoft Office 產品提供一致的連絡人經驗的功能。此功能可讓使用者使相同的連絡人資訊皆可全域 Lync、 Exchange、 Outlook及Outlook Web App， Exchange 2013信箱中儲存所有的連絡人資訊。

Lync Server 2013 Exchange 2013的環境中安裝及設定兩者間的伺服器對伺服器驗證之後，使用者即可啟動的現有連絡人從Lync Server 2013Exchange 2013移轉。如需詳細資訊，請參閱 ＜ [Planning and Deploying Unified Contact Store](https://go.microsoft.com/fwlink/p/?linkid=275092)。

## 使用者相片

使用者相片是一種功能，可讓您儲存Exchange 2013可存取的用戶端應用程式，包括Outlook、 Outlook Web App、 SharePoint 2013、 Lync 2013、 及行動裝置的電子郵件用戶端高解析度使用者相片。低解析度相片也會儲存在Active Directory。 為與整合連絡人存放區使用者相片可讓組織為維持一致的使用者設定檔照片，可供用戶端應用程式而不需要有自己的使用者相片與不同的方式新增及管理其每個應用程式。使用者可以管理使用Outlook Web App、 SharePoint 2013或Lync 2013自己相片。管理 Outlook Web 應用程式的相片相關詳細資料，看到[我的帳號](https://go.microsoft.com/fwlink/p/?linkid=269646)。

## Outlook Web App 中呈現的 Lycn

Exchange 2013在環境中使用Lync Server 2013安裝，您可以設定它們可以讓使用者看到Outlook Web App中的目前狀態資訊。使用者可以查看其立即訊息連絡人\] 及 \[瀏覽窗格中的 Outlook Web App 中的群組、 回覆或啟動立即訊息工作階段從Outlook Web App及管理其立即訊息連絡人與群組。

## OAuth 驗證

Exchange 2013、 SharePoint 2013及Lync Server 2013提供豐富的跨產品功能上述使用 OAuth 驗證通訊協定進行伺服器對伺服器驗證。使用相同的驗證通訊協定順暢地讓這些應用程式和安全地相互驗證。驗證機制支援等應用程式使用的內容連結的帳戶及使用者模擬存取要求進行中的使用者內容的位置進行驗證。

OAuth 是許多網站和 web 服務所使用的標準授權通訊協定。它可讓用戶端存取而不需要提供使用者名稱和密碼資源伺服器所提供的資源。驗證是由受信任的資源擁有者，可提供存取權杖，讓用戶端授權伺服器執行。Token 授與存取特定一組資源在指定期間內。如需詳細資訊Exchange 2013的 OAuth 實作， [\[MS XOAUTH\]： OAuth 2.0 驗證通訊協定 Extensions](https://go.microsoft.com/fwlink/p/?linkid=275093)。

**內部部署中的 OAuth**

內部部署中Exchange 2013、 SharePoint 2013和Lync Server 2013不需要問題權杖授權伺服器。每個這些應用程式發出存取其他應用程式所提供的資源的自我簽署的憑證。提供存取權的資源，例如Exchange 2013、 應用程式必須信任講呼叫應用程式的自我簽署的憑證。 藉由建立包含呼叫應用程式 ApplicationID、 憑證和 AuthMetadataUrl 的呼叫應用程式的*協力廠商應用程式*設定建立信任關係。Exchange 2013、 SharePoint 2013及Lync Server 2013發佈其驗證中繼資料文件中的已知的 URL。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>伺服器</strong></p></td>
<td><p><strong>AuthMetadataUrl</strong></p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013</p></td>
<td><p><code>https://&lt;serverfqdn&gt;/autodiscover/metadata/json/1</code></p></td>
</tr>
<tr class="odd">
<td><p>Lync Server 2013</p></td>
<td><p><code>https://&lt;serverfqdn&gt;/metadata/json/1</code></p></td>
</tr>
<tr class="even">
<td><p>SharePoint 2013</p></td>
<td><p><code>https://&lt;serverfqdn&gt;/_layouts/15/metadata/json/1</code></p></td>
</tr>
</tbody>
</table>


**Exchange 2013 Server Auth Certificate**

Exchange 2013安裝程式會建立自我簽署的憑證與 Microsoft Exchange Server 驗證憑證的易記名稱。憑證已複寫至Exchange 2013組織中的所有前端伺服器。在Exchange 2013的授權組態中，以及其服務名稱，代表在內部Exchange 2013已知 GUID 指定憑證的指紋。Exchange 會使用發行其驗證中繼資料文件的授權組態。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>預設Exchange 2013所建立的伺服器驗證憑證時才有效的五年。您必須確定授權組態包含目前的憑證。</td>
</tr>
</tbody>
</table>


當Exchange 2013收到存取要求從協力廠商應用程式透過 Exchange Web 服務 (EWS) 時，它會剖析 https 要求，其中包含使用其私密金鑰的呼叫伺服器所簽署的存取 token `www-authenticate`標頭。驗證模組會驗證使用協力廠商應用程式設定的存取 token。然後授與存取權授與應用程式的 RBAC 權限為基礎的資源。代表使用者存取權杖時，檢查是否有授與使用者的 RBAC 權限。例如，如果使用者執行的 eDiscovery 搜尋使用SharePoint 2013、 Exchange 檢查中的 eDiscovery 中心是否在使用者為 「 探索管理角色群組的成員或擁有信箱搜尋指派角色和所搜尋的信箱會 RBAC 角色指派的範圍內。如需詳細資訊，請參閱[權限](permissions-exchange-2013-help.md)。

## 管理 OAuth 驗證

在 Exchange 2013 中，您必須為包含夥伴應用程式的 OAuth 驗證管理兩個組態物件：

  - **AuthConfig**  AuthConfig Exchange 2013安裝程式會建立和用以發佈的驗證中繼資料。您不需要管理除了來佈建的新憑證的現有憑證接近到期時驗證設定。在這種情況下，您可以更新現有的憑證並將新的憑證設定為有效的日期及 AuthConfig 中的下一個憑證。新的憑證自動複寫到組織中其他Exchange 2013 、 使用新的憑證詳細資料重新整理授權中繼資料文件和 AuthConfig 變換至新的憑證在有效的日期。

  - **協力廠商應用程式**  若要讓夥伴應用程式從Exchange 2013要求存取 token，您必須建立合作夥伴應用程式設定。Exchange 2013提供`Configure-EnterprisePartnerApplication.ps1`指令碼，它可讓您快速和輕鬆建立合作夥伴應用程式設定並設定錯誤降到最低。如需詳細資訊，請參閱[設定 SharePoint 2013 與 Lync 2013 的 OAuth 驗證](configure-oauth-authentication-with-sharepoint-2013-and-lync-2013-exchange-2013-help.md)。

