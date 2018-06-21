---
title: 'Exchange Server 混合部署: Exchange 2013 Help'
TOCTitle: '@NoTitle'
ms:assetid: 59e32000-4fcf-417f-a491-f1d8f9aeef9b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ200581(v=EXCHG.150)
ms:contentKeyID: 50474704
ms.date: 05/05/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange Server 混合部署

 

_<strong>適用版本：</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>上次修改主題的時間：</strong>2018-04-16_

**摘要：** 您對於規劃 Exchange 混合式部署需要知道的項目。

混合部署為組織提供了從現有內部部署 Microsoft Exchange 組織將功能豐富的經驗與管理控制延伸至雲端的能力。混合部署在內部部署 Exchange 組織與 Microsoft Office 365 的 Exchange Online 之間提供了單一 Exchange 組織的完美外觀與感受。此外，混合部署還能夠當做一個中繼步驟，有助於完整移轉至 Exchange Online 組織。

**目錄**

Exchange 混合式部署功能

Exchange 混合式部署考量

Exchange 混合式部署元件

Exchange 混合式部署範例

設定 Exchange 混合式部署之前的考量事項

重要詞彙

Exchange 混合式部署文件

## Exchange 混合式部署功能

混合部署具備下列特色：

  - 內部部署和 Exchange Online 組織之間的安全郵件路由。

  - 以共用網域命名空間進行的郵件路由傳送。例如，內部部署和 Exchange Online 組織都採用 @contoso.com SMTP 網域。

  - 統一的全域通訊清單 (GAL)，也稱為「共用通訊錄」。

  - 在內部部署和 Exchange Online 組織之間共用空閒/忙碌和行事曆。

  - 集中式輸入與輸出郵件流程控制。您可設定所有輸入與輸出 Exchange Online 郵件以透過內部部署 Exchange 組織路由傳輸。

  - 內部部署和 網頁型 Outlook 線上組織採用單一 Exchange URL。

  - 將現有內部部署信箱移至 Exchange Online 組織的能力。若需要，Exchange Online 信箱也可移回至內部部署組織。

  - 使用內部部署 Exchange 系統管理中心 (EAC) 進行集中式信箱管理。

  - 在內部部署與Exchange Online 織之間進行郵件追蹤、郵件提示和多信箱搜尋。

  - 適用於內部部署 Exchange 信箱的雲端式郵件封存。Exchange Online 封存可搭配混合式部署來使用。若要深入了解 Exchange Online 封存，請參閱 [Microsoft Office 365 其他服務](https://go.microsoft.com/fwlink/p/?linkid=233231)。

## Exchange 混合式部署考量

實作 Exchange 混合式部署之前，您應該考量下列事項：

  - **混合部署的需求**設定交互式部署之前，您必須先確認內部部署組織符合成功部署所需的所有必要條件。如需詳細資訊，請參閱 [混合部署必要條件](hybrid-deployment-prerequisites-exchange-2013-help.md)。

  - **Exchange ActiveSync 用戶端**  當您將信箱從您的內部部署 Exchange 組織移至 Exchange Online 時，所有存取信箱的用戶端都必須更新為使用 Exchange Online；其中包括 Exchange ActiveSync 裝置。大部分的 Exchange ActiveSync 用戶端即將在信箱移至 Exchange Online 時自動重新設定，但是某些較舊的裝置可能無法正確更新。如需詳細資訊，請參閱 [Exchange ActiveSync 裝置設定與 Exchange 混合式部署](exchange-activesync-device-settings-with-exchange-hybrid-deployments-exchange-2013-help.md)。

  - **信箱權限移轉**  明確套用至在信箱的內部部署信箱權限 (例如「傳送為」、「完整存取」、「代理傳送者」及「資料夾權限」) 會移轉至 Exchange Online。繼承 (非明確) 的信箱權限以及在 Exchange Online 中授與未啟用郵件功能的物件的權限不會移轉。您應該在移轉之前確定已明確授與所有權限，且所有物件都已啟用郵件功能。因此，您必須規劃在 Office 365 中設定這些權限 (若適用於貴組織)。在使用「傳送為」權限的情況下，若要嘗試傳送的使用者和資源不會同時移動，則您必須使用 **Add-RecipientPermission** Cmdlet 明確地將「傳送為」權限加入 Exchange Online。

  - **支援跨部門信箱權限** Exchange 混合式部署支援在位於內部部署 Exchange 組織的信箱與位於 Office 365 的信箱之間，使用 \[完整存取\]、\[代理傳送者\] 權限。若要使用 \[傳送為\] 權限，則需要其他步驟。此外，根據您內部部署組織中安裝的 Exchange 版本，可能需要一些額外配置來支持跨部門郵箱權限。如需詳細資訊，請參閱＜[Exchange 混合式部署中的權限](permissions-in-exchange-hybrid-deployments-exchange-2013-help.md)＞和＜[設定 Exchange 混合部署中支援委派的信箱權限](configure-exchange-to-support-delegated-mailbox-permissions-in-a-hybrid-deployment-exchange-2013-help.md)[＞中的委派信箱權限](permissions-in-exchange-hybrid-deployments-exchange-2013-help.md)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ150559.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>自 2018 年 2 月起，會推出支援完整存取權、代理傳送者代表以及跨樹系資料夾權限等功能，並預計會在 2018 年 4 月 之前完成。</td>
    </tr>
    </tbody>
    </table>


  - **登出**  在進行中的收件者管理過程裡，您可能必須將 Exchange Online 信箱移回您的內部部署環境。
    
    如需如何在 Exchange 2010 型混合式部署中移動信箱的詳細資訊，請參閱 [將 Exchange Online 信箱移動至內部部署組織](https://technet.microsoft.com/zh-tw/library/hh882527\(v=exchg.150\))。
    
    如需如何根據 Exchange 2013 或更新版本在混合部署中移動信箱的詳細資訊，請參閱 [在混合式部署中內部部署與 Exchange Online 組織之間移動信箱](move-mailboxes-between-on-premises-and-exchange-online-organizations-in-hybrid-deployments-exchange-2013-help.md)。

  - **信箱轉寄設定**可以將信箱設定為將寄給他們的郵件轉寄給另一個信箱。Exchange Online 中支援信箱轉寄，在移轉信箱時不會將轉寄設定複製到 Exchange Online。在將信箱移轉至 Exchange Online，請確定您為每個信箱匯出轉寄設定。轉寄設定會儲存在每個信箱上的 `DeliverToMailboxAndForward`、`ForwardingAddress`，和 `ForwardingSmtpAddress` 內容。

## Exchange 混合式部署元件

混合部署涉及了數種不同的服務和元件：

  - **Exchange 伺服器**  如果您想要設定混合部署，內部部署組織中必須設定至少一個 Exchange 伺服器。如果您正在執行 Exchange 2013 或更舊版本，您必須安裝至少一個執行信箱和用戶端存取角色的伺服器。如果您正在執行 Exchange 2016 或更新版本，必須安裝至少一個執行信箱角色的伺服器。如有必要，Exchange Edge Transport Server 也可以安裝在周邊網路，並支援與 Office 365 之間的安全郵件流程。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ150559.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>我們不支援在周邊網路中安裝執行信箱或用戶端存取伺服器角色的 Exchange 伺服器。</td>
    </tr>
    </tbody>
    </table>


  - **Microsoft Office 365**   Office 365 服務包含 Exchange 雲端式組織做為訂閱服務的一部分。設定混合部署的組織必須為每個移轉至 Exchange Online 組織或在其中建立的信箱購買授權。

  - **混合組態精靈**Exchange 包括混合組態精靈，可提供有效率的程序，讓您在內部部署 Exchange 與 Exchange Online 組織之間設定混合部署。
    
    若要深入了解，請參閱 [混合組態精靈](hybrid-configuration-wizard-exchange-2013-help.md)。

  - **Azure AD 驗證系統**   Azure Active Directory (AD) 驗證系統是免費的雲端服務，可作為您的內部部署 Exchange 2016 組織和 Exchange Online 組織之間的信任代理人。設定混合式部署的內部部署組織，必須具有對 Azure AD 驗證系統的同盟信任。同盟信任可以在設定內部部署 Exchange 組織與其他同盟 Exchange 組織之間的同盟資訊共用功能時手動建立，也可以在使用混合組態精靈設定混合部署時手動建立。當您啟動 Office 365 服務帳戶時，系統會自動為您的 Office 365 租用戶設定對 Azure AD 驗證系統的同盟信任。
    
    若要深入了解，請參閱 [Azure AD 驗證系統](https://go.microsoft.com/fwlink/p/?linkid=135986)。

  - **Azure Active Directory 同步處理**  Azure AD 同步處理會使用 Azure AD Connect 複寫所有擁有郵件功能物件的資訊之內部部署 Active Directory 資訊至 Office 365 組織，以支援統一的全域通訊清單(GAL) 和使用者驗證。設定混合部署的組織必須在不同的內部部署伺服器上部署 Azure AD Connect，才能同步處理您的內部部署 Active Directory 和 Office 365。
    
    若要深入了解，請參閱：[Azure AD Connect - 概觀](https://go.microsoft.com/fwlink/p/?linkid=203007)

重要詞彙

## 混合式部署範例

請參閱下列案例。這是一般 Exchange 2016 部署的範例拓撲。Contoso, Ltd. 是單一樹系、單一網域組織，其中安裝了兩個網域控制站和一個 Exchange 2016 伺服器。遠端 Contoso 使用者在網際網路上使用 網頁型 Outlook 連線至 Exchange 2016，以檢查信箱和存取 Outlook 行事曆。

![已設定與 Office 365 混合式部署之前，先內部部署 Exchange 部署](images/JJ200581.dad133ae-d18a-42ec-8f0a-dd1de391200e(EXCHG.150).png "已設定與 Office 365 混合式部署之前，先內部部署 Exchange 部署")

假設您是 Contoso 的網路系統管理員，而您想要設定混合部署。您會部署和設定必要的 Azure AD Connect 伺服器，並且決定使用 Azure AD Connect 密碼同步處理功能來讓使用者將相同的認證用於他們的內部部署網路帳戶和他們的 Office 365 帳戶。在您完成混合部署先決條件並使用混合組態精靈選取混合部署的選項之後，您的新拓撲組態如下：

  - 使用者將使用其相同的使用者名稱和密碼來登入內部部署與 Exchange Online 組織 (「單一登入」)。

  - 位於內部部署及 Exchange Online 組織中的使用者信箱將使用相同的電子郵件地址網域。例如，位於內部部署的信箱及位於 Exchange Online 組織中的信箱都會在使用者電子郵件地址中使用 @contoso.com。

  - 所有外送郵件都由內部部署組織傳遞至網際網路。內部部署組織會控制所有郵件傳輸，並擔任 Exchange Online 組織的轉送站 (「集中式郵件傳輸」)。

  - 內部部署和 Exchange Online 組織使用者可以彼此共用行事曆空閒/忙碌資訊。為這兩個組織設定的組織關係，也會啟用跨部署郵件追蹤、郵件提示及訊息搜尋。

  - 內部部署和 Exchange Online 使用者在網際網路上會使用相同的 URL 來連線至信箱。

![已設定與 Office 365 混合式部署之後，再內部部署 Exchange 部署](images/JJ200581.e8681849-f15d-4d0e-b77e-6105b6096c4b(EXCHG.150).png "已設定與 Office 365 混合式部署之後，再內部部署 Exchange 部署")

如果您比較 Contoso 的現有組織組態與混合部署組態，則會看到設定混合部署時已新增伺服器及服務，以支援在內部部署組織與 Exchange Online 組織之間共用的其他通訊及功能。以下概述混合部署從初始內部部署 Exchange 組織進行的變更。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>組態</th>
<th>混合部署前</th>
<th>混合部署後</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>信箱位置</p></td>
<td><p>僅有內部部署信箱。</p></td>
<td><p>位於內部部署與 Office 365 中的信箱。</p></td>
</tr>
<tr class="even">
<td><p>訊息傳輸</p></td>
<td><p>內部部署信箱伺服器負責處理所有輸入及輸出的訊息路由。</p></td>
<td><p>內部部署信箱伺服器會處理在內部部署組織和 Office 365 組織之間的內部訊息路由。</p></td>
</tr>
<tr class="odd">
<td><p>網頁型 Outlook</p></td>
<td><p>內部部署信箱伺服器接收所有的 網頁型 Outlook 要求並顯示信箱資訊。</p></td>
<td><p>內部部署信箱伺服器將 網頁型 Outlook 要求重新導向至內部部署 Exchange 2016 信箱伺服器，或提供登入 Office 365 的連結。</p></td>
</tr>
<tr class="even">
<td><p>兩個組織都通用的統一 GAL</p></td>
<td><p>不適用；僅有單一組織。</p></td>
<td><p>內部部署 Active Directory 同步伺服器將擁有郵件功能之物件的 Active Directory 資訊複寫至 Office 365。</p></td>
</tr>
<tr class="odd">
<td><p>兩個組織都通用的單一登入</p></td>
<td><p>不適用；僅有單一組織。</p></td>
<td><p>內部部署 Active Directory 和 Office 365 會將相同的使用者名稱和密碼用在位於內部部署或 Office 365 的信箱。</p></td>
</tr>
<tr class="even">
<td><p>建立的組織關係以及對 Azure AD 驗證系統的同盟信任</p></td>
<td><p>您可以設定對 Azure AD 驗證系統的信任關係，以及與其他同盟 Exchange 組織之間的組織關係。</p></td>
<td><p>對 Azure AD 驗證系統的信任關係是必要的。在內部部署與 Office 365 之間建立組織關係。</p></td>
</tr>
<tr class="odd">
<td><p>空閒/忙碌資訊共用</p></td>
<td><p>僅能在內部部署使用者之間進行空閒/忙碌資訊共用。</p></td>
<td><p>在內部部署使用者與 Office 365 使用者之間進行空閒/忙碌資訊共用。</p></td>
</tr>
</tbody>
</table>


## 設定混合式部署之前的考量事項

既然您已較熟悉混合部署，您需要仔細考量一些重要議題。設定混合部署可能會影響您目前網路及 Exchange 組織中的多個區域。

## 目錄同步處理及單一登入

每隔 3 小時由執行 Active Directory Connect 的伺服器執行內部部署和 Office 365 之間的 Active Directory 同步處理，這是設定混合部署的必要項。目錄同步處理可讓任何組織中的收件者在全域通訊清單中看到對方。它也會同步處理使用者名稱和密碼，讓使用者利用相同的認證登入您的內部部署組織和 Office 365。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ150559.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您選擇使用 AD FS 設定 Azure AD Connect，內部部署使用者的使用者名稱和密碼在預設上仍然會同步到 Office 365。不過，使用者將會透過 AD FS 驗證您的內部部署 Active Directory，做為其主要的驗證方法。萬一 AD FS 因任何原因無法連線至您的內部部署 Active Directory，用戶端將嘗試切換方法，並驗證同步至 Office 365 的使用者名稱和密碼。</td>
</tr>
</tbody>
</table>


Azure Active Directory 和 Office 365 的所有客戶預設都有限制：50,000 個物件 (使用者、擁有郵件功能的連絡人和群組)。此限制決定您可以在 Office 365 組織中建立多少物件。當您驗證第一個網域時，此物件限制會自動增加至 300,000 個物件。如果您已驗證網域並需要同步處理 300,000 個以上的物件，或者沒有任何網域需要進行驗證並需要同步處理 50,000 個以上的物件，則需要連絡「Azure Active Directory 支援」以要求增加至您的物件配額限制。

除了執行 Azure AD Connect 的伺服器，如果您選擇設定 AD FS，您也必須部署 Web 應用程式 Proxy 伺服器。此伺服器應該放在周邊網路，並且做為您的內部 Azure AD Connect 伺服器和網際網路之間的媒介。Web 應用程式 Proxy 伺服器必須接受在網際網路上使用 TCP 連接埠 443 的用戶端連線。

## 混合部署管理

您會透過可同時用於管理內部部署和 Exchange Online 組織的單一統一管理主控台，管理 Exchange 2016 中的混合部署。*Exchange 系統管理中心* (EAC) 取代了 Exchange 管理主控台和 Exchange 控制台，可讓您連接和設定這兩種組織的功能。當您初次執行混合組態精靈時，會提示您連接到 Exchange Online 組織。您必須使用本身為 Organization Management 角色群組成員的 Office 365 帳戶，將 EAC 連接至您的 Exchange Online 組織。

## 憑證

安全通訊端層 (SSL) 數位憑證扮演設定混合部署的重要角色。這些憑證有助於保護內部部署混合伺服器與 Exchange Online 組織之間通訊的安全。憑證是設定數種類型服務所必要的。如果您已在 Exchange 組織中使用數位憑證，則可能需要修改憑證以包括其他網域，或向信任的憑證授權單位 (CA) 購買其他憑證。如果您尚未使用憑證，則需要向信任的 CA 購買一或多個憑證。

若要深入了解，請參閱：[混合部署的憑證需求](certificate-requirements-for-hybrid-deployments-exchange-2013-help.md)

## 頻寬

與網際網路的網路連線會直接影響內部部署組織與 Office 365 組織之間的通訊效能。尤其是將內部部署 Exchange 2016 伺服器中的信箱移至 Office 365 組織時，影響更顯著。可用的網路頻寬量，加上信箱大小以及平行移動的信箱數目，會導致完成信箱移動的時間不同。此外，其他 Office 365 服務 (例如 SharePoint Server 2016 和 商務用 Skype) 也可能會影響郵件服務的可用頻寬。

將信箱移至 Office 365 之前，您應該：

  - 決定要移至 Office 365 之信箱的平均大小。

  - 判斷從內部部署組織到網際網路連線的平均連線及輸送量速度。

  - 計算平均預期傳送速度，並據此計劃信箱移動。

若要深入了解，請參閱[網路功能](https://go.microsoft.com/fwlink/p/?linkid=280178)。

## 整合通訊

整合通訊 (UM) 是一種在內部部署組織和 Office 365 組織之間的混合部署中支援的服務。您的內部部署電話語音解決方案必須能夠與 Office 365 組織進行通訊。因此您可能會需要購買其他的硬體和軟體。

如果您要將信箱從內部部署組織移至 Office 365，且這些信箱已針對 UM 進行設定，則您必須在移動信箱之前，在您的混合部署內設定 UM。如果您在於混合部署中設定 UM 之前移動信箱，這些信箱將不再具有 UM 功能的存取權限。

若要深入了解，請參閱：[在混合部署中設定整合通訊](https://go.microsoft.com/fwlink/p/?linkid=842271)

## 資訊版權管理

資訊版權管理 (IRM) 可讓使用者套用 Active Directory Rights Management Services (AD RMS) 範本至他們傳送的郵件。AD RMS 範本讓使用者控制可開啟受權限保護郵件的人員，以及這些人員在開啟郵件後可對郵件執行的動作，藉此來防止資訊外洩。

混合部署中的 IRM 需要規劃、手動設定 Office 365 組織，以及了解用戶端如何根據他們位於內部部署或 Exchange Online 組織的信箱來使用 AD RMS 伺服器。

若要深入了解，請參閱：[Exchange 混合式部署中的 IRM](irm-in-exchange-hybrid-deployments-exchange-2013-help.md)

## 行動裝置

在混合部署中是支援行動裝置的。如果已在現有的伺服器上啟用 Exchange ActiveSync，其會持續將來自行動裝置的要求重新導向至位於內部部署信箱伺服器上的信箱。對於連接至從內部部署組織移至 Office 365 的現有信箱之行動裝置而言，Exchange ActiveSync 設定檔必需自動更新為連接至大部分電話上的 Office 365。所有支援 Exchange ActiveSync 的行動裝置都應該能與混合部署相容。

若要深入了解，請參閱：[行動電話](https://go.microsoft.com/fwlink/p/?linkid=206387)

## 用戶端需求

我們建議您的用戶端使用 Outlook 2016 或 Outlook 2013，以獲得混合部署的最佳體驗及效能。預先的 Outlook 2010 用戶端在混合部署或 Office 365 中不受支援。

## Office 365 授權

若要將信箱移至 Office 365 或是在其中建立信箱，您需要註冊 Office 365 企業版，而且必須具有授權。當您註冊 Office 365 時，會收到可指派給新信箱或指派給從內部部署組織移動之信箱的特定數目授權。Office 365 中的每個信箱都必須要有授權。

## 防毒及反垃圾郵件服務

Exchange Online Protection (EOP) 會自動為移至 Office 365 的信箱提供防毒及反垃圾郵件保護 (由 Office 365 提供的服務)。若您選擇透過 EOP 服務路由傳送所有內送網際網路郵件，則必須為內部部署使用者購買額外的 EOP 授權。建議您仔細評估，在您 Office 365 中的 EOP 保護是否同樣符合內部部署組織的防毒及反垃圾郵件需求。如果您的內部部署組織已有保護功能，則您可能需要升級或設定內部部署的防毒及反垃圾郵件解決方案，以取得組織的最大保護。

若要深入了解，請參閱：[反垃圾郵件和反惡意程式碼保護](https://technet.microsoft.com/zh-tw/library/jj200731\(v=exchg.150\))

## 公用資料夾

Office 365 中已支援公用資料夾，而且內部部署公用資料夾可移轉至 Office 365。此外，Office 365 中的公用資料夾可移至內部部署 Exchange 2016 組織。內部部署與 Office 365 使用者均可存取位於使用網頁型 Outlook、Outlook 2016、Outlook 2013 或 Outlook 2010 SP2 或更新版本之組織中的公用資料夾。在設定混合部署時，現有的內部部署公用資料夾組態以及內部部署信箱的存取不會變更。

若要深入了解，請參閱：[公用資料夾](https://technet.microsoft.com/zh-tw/library/jj150538\(v=exchg.150\))

## 協助工具

如需適用於此檢查清單中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](https://technet.microsoft.com/zh-tw/library/jj150484\(v=exchg.150\))。

## 重要詞彙

下方列表提供 Exchange 2013 中與混合部署相關的核心元件定義。

  - **集中郵件傳輸**  
    所有 Exchange Online 輸入與輸出網際網路郵件皆經由內部部署 Exchange 組織路由傳輸的混合組態選項。此路由傳輸選項可於混合組態精靈中設定。如需詳細資訊，請參閱 [Exchange 混合式部署中的傳輸選項](transport-options-in-exchange-hybrid-deployments-exchange-2013-help.md)。

<!-- end list -->

  - **共存網域**  
    新增至內部部署組織的混合郵件流可接受的網域，以及 Office 365 服務的自動探索服務請求。此網域將當做次要 Proxy 網域新增到任何具有混合組態精靈中所選取網域之 *PrimarySmtpAddress* 範本的電子郵件地址原則。依預設，此網域為 \<domain\>.mail.onmicrosoft.com。

<!-- end list -->

  - ***HybridConfiguration* Active Directory 物件**  
    包含於混合組態精靈中選擇的預期混合部署組態參數之內部部署組織中的 Active Directory 物件。混合組態引擎在設定內部部署與 Exchange Online 設定時將使用這些參數來啟用混合功能。*HybridConfiguration* 物件的內容將在每次執行混合組態精靈時重置。

<!-- end list -->

  - **混合組態引擎**  
    「混合組態引擎」(HCE) 會執行設定及更新混合部署所需的核心動作。HCE 將比較 *HybridConfiguration* Active Directory 物件與目前內部部署 Exchange 及 Exchange Online 組態設定的狀態，然後執行任務以讓部署組態設定與 *HybridConfiguration* Active Directory 物件中定義的參數相符。如需詳細資訊，請參閱 [Hybrid Configuration Engine](hybrid-configuration-wizard-exchange-2013-help.md)。

<!-- end list -->

  - **混合組態精靈 (HCW)**  
    Exchange 中提供調適性工具將領導管理者在內部部署與 Exchange Online 組織間設定混合部署。精靈將定義 *HybridConfiguration* 物件中的混合部署組態參數，並指引混合組態引擎執行必要的組態任務，以啟用定義的混合功能。如需詳細資訊，請參閱 [混合組態精靈](hybrid-configuration-wizard-exchange-2013-help.md)。

<!-- end list -->

  - **以 Exchange 2010 為基礎的混合部署**  
    將 Exchange Server 2010 內部部署伺服器 Service Pack 3 (SP3) 作為 Office 365 與 Exchange Online 服務連接端點進行設定的混合部署。內部部署 Exchange 2010、Exchange Server 2007 以及 Exchange Server 2003 組織的混合部署選項。

<!-- end list -->

  - **以 Exchange 2013 為基礎的混合部署**  
    將 Exchange Server 2013 內部部署伺服器 Service Pack 3 (SP3) 作為 Office 365 與 Exchange Online 服務連接端點進行設定的混合部署。內部部署 Exchange 2013、Exchange 2010 以及 Exchange 2007 組織的混合部署選項。

<!-- end list -->

  - **以 Exchange 2016 為基礎的混合部署**  
    將 Exchange Server 2016 內部部署伺服器 Service Pack 3 (SP3) 作為 Office 365 與 Exchange Online 服務連接端點進行設定的混合部署。內部部署 Exchange 2016、Exchange 2013 以及 Exchange 2010 組織的混合部署選項。

<!-- end list -->

  - **安全郵件運輸**  
    混合組態的自動設定功能，可於內部部署與 Exchange Online 組織間使用安全郵件。以混合組態精靈中選擇的憑證來使用相互傳輸層安全性 (TLS) 進行郵件加密與驗證。Office 365 租用戶為源於內部部署組織的混合傳輸連接端點，且為混合傳輸連接至來自 Exchange Online 內部部署組織的端點。

重要詞彙

## Exchange 混合式部署文件

下表包含主題的連結，這些主題可協助您了解及管理 Microsoft Exchange 中的混合部署。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>主題</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="hybrid-configuration-wizard-exchange-2013-help.md">混合組態精靈</a></p></td>
<td><p>了解混合組態精靈和「混合組態引擎」如何設定混合部署。</p></td>
</tr>
<tr class="even">
<td><p><a href="hybrid-deployment-prerequisites-exchange-2013-help.md">混合部署必要條件</a></p></td>
<td><p>深入了解混合部署先決條件，包括相容的 Exchange Server 組織、Office 365 需求及其他內部部署組態需求。</p></td>
</tr>
<tr class="odd">
<td><p><a href="certificate-requirements-for-hybrid-deployments-exchange-2013-help.md">混合部署的憑證需求</a></p></td>
<td><p>深入了解混合部署中數位憑證的需求。</p></td>
</tr>
<tr class="even">
<td><p><a href="transport-options-in-exchange-hybrid-deployments-exchange-2013-help.md">Exchange 混合式部署中的傳輸選項</a></p></td>
<td><p>深入了解混合部署中的內送和外寄郵件傳輸選項。</p></td>
</tr>
<tr class="odd">
<td><p><a href="transport-routing-in-exchange-hybrid-deployments-exchange-2013-help.md">Exchange 混合式部署中的傳輸路由</a></p></td>
<td><p>深入了解混合部署中的內送和外寄郵件路由選項。</p></td>
</tr>
<tr class="even">
<td><p><a href="hybrid-management-in-exchange-hybrid-deployments-exchange-2013-help.md">Exchange 混合式部署中的混合式管理</a></p></td>
<td><p>深入了解使用 Exchange 系統管理中心和 Exchange 管理命令介面來管理您的混合部署。</p></td>
</tr>
<tr class="odd">
<td><p><a href="shared-free-busy-in-exchange-hybrid-deployments-exchange-2013-help.md">Exchange 混合式部署中的共用空閒/忙碌</a></p></td>
<td><p>深入了解混合部署中內部部署和 Exchange Online 組織之間的行事曆空閒/忙碌資訊共用。</p></td>
</tr>
<tr class="even">
<td><p><a href="server-roles-in-exchange-hybrid-deployments-exchange-2013-help.md">Exchange 混合式部署中的伺服器角色</a></p></td>
<td><p>深入了解 Exchange 伺服器角色在混合部署中的運作方式。</p></td>
</tr>
<tr class="odd">
<td><p><a href="irm-in-exchange-hybrid-deployments-exchange-2013-help.md">Exchange 混合式部署中的 IRM</a></p></td>
<td><p>深入了解資訊版權管理在混合部署中的運作方式。</p></td>
</tr>
<tr class="even">
<td><p><a href="permissions-in-exchange-hybrid-deployments-exchange-2013-help.md">Exchange 混合式部署中的權限</a></p></td>
<td><p>深入了解混合部署如何使用應用角色的存取控制 (RBAC) 來控制權限。</p></td>
</tr>
<tr class="odd">
<td><p><a href="edge-transport-servers-with-hybrid-deployments-exchange-2013-help.md">Edge Transport server 與混合式部署</a></p></td>
<td><p>深入了解 Exchange Edge Transport Server 及其在混合部署中部署和操作的方式。</p></td>
</tr>
<tr class="even">
<td><p><a href="single-sign-on-with-hybrid-deployments-exchange-2013-help.md">單一登入與混合式部署</a></p></td>
<td><p>深入了解如何使用混合部署中的密碼同步處理和 AD FS 功能進行單一登入。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hybrid-deployment-procedures-exchange-2013-help.md">混合式部署程序</a></p></td>
<td><p>探索建立和修改 Exchange 內部部署和 Exchange Online 組織之混合部署的程序。</p></td>
</tr>
<tr class="even">
<td><p><a href="hybrid-deployments-with-exchange-2013-and-exchange-2010-exchange-2013-help.md">採用 Exchange 2013 及 Exchange 2010 的混合式部署</a></p></td>
<td><p>深入了解以 Exchange 2013 為基礎的混合部署與 Exchange 2010 組織。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hybrid-deployments-with-exchange-2013-and-exchange-2007-exchange-2013-help.md">採用 Exchange 2013 及 Exchange 2007 的混合部署</a></p></td>
<td><p>深入了解以 Exchange 2013 為基礎的混合部署與 Exchange 2007 組織。</p></td>
</tr>
</tbody>
</table>


## 初次使用 Office 365 嗎？


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><img src="images/Dn249373.eac8a413-9498-4220-8544-1e37d1aaea13(EXCHG.150).png" title="LinkedIn Learning 的短圖示" alt="LinkedIn Learning 的短圖示" /> <strong>初次使用 Office 365？</strong><br />
探索 LinkedIn Learning 提供的 <a href="https://support.office.com/zh-tw/article/office-365-admin-and-it-pro-courses-68cc9b95-0bdc-491e-a81f-ee70b3ec63c5">Office 365 admins and IT pros</a> 免費影片課程。</p></td>
</tr>
</tbody>
</table>

