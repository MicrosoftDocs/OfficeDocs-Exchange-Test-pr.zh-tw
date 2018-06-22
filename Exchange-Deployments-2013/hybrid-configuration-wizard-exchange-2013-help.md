---
title: '混合組態精靈: Exchange 2013 Help'
TOCTitle: 混合組態精靈
ms:assetid: 2e6ed294-ee74-4038-8b71-b61786372ba4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh529921(v=EXCHG.150)
ms:contentKeyID: 50474699
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 混合組態精靈

 

_<strong>適用版本：</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>上次修改主題的時間：</strong>2016-12-09_

本主題為您提供 Exchange 混合式部署組態程序、可用的混合式部署功能和選項，以及執行設定和更新混合式部署所需核心動作之「混合組態引擎」的概觀。

如需混合式部署的相關資訊，請參閱[Exchange Server 混合部署](exchange-server-hybrid-deployments-exchange-2013-help.md)。

**目錄**

混合組態程序

混合組態功能

混合組態選項

混合組態引擎

## 混合組態程序

以下是混合組態精靈程序的簡要概觀。首先，此精靈會在您的內部部署 Active Directory 中建立 **HybridConfiguration** 物件。這個 Active Directory 物件會儲存混合式部署的混合組態資訊，並透過混合組態精靈進行更新。接著，此精靈會收集現有的內部部署 Exchange 和 Active Directory 拓撲組態資料、Office 365 租用戶和 Exchange Online 組態資料，定義數個組織參數，然後同時在內部部署和 Exchange Online 組織中執行一系列組態工作。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ906432.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用混合組態精靈之前，有幾個重要的考量事項和先決條件需要先完成。您需要符合 <a href="hybrid-deployment-prerequisites-exchange-2013-help.md">混合部署必要條件</a> 中所述的混合式部署需求。然後，您就可以使用混合組態精靈針對混合式部署設定 Exchange 組織。</td>
</tr>
</tbody>
</table>


混合式部署組態程序的一般階段包括：

1.  **驗證必要條件並執行拓撲檢查**   混合組態精靈會驗證您的內部部署和 Exchange Online 組織是否可支援混合式部署。此精靈在內部部署和 Exchange Online 組織中驗證及檢查的一些項目包括：
    
      - 內部部署 Exchange Server 版本
    
      - Exchange Online 版本
    
      - Active Directory 同步處理目前狀態和組態
    
      - 同盟和公認的網域
    
      - 現有的同盟信任和組織關係
    
      - Web 服務虛擬目錄
    
      - Exchange 憑證

2.  **測試帳戶認證**   指定的內部部署和 Office 365 混合管理帳戶會存取內部部署和 Exchange Online 組織，以收集必要條件驗證資訊並進行組織參數組態的變更來啟用混合式部署功能。混合組態精靈會檢查該帳戶是否具有適當的認證，以及是否可連接到內部部署和 Exchange Online 組織。內部部署和 Office 365 組織的混合式部署管理帳戶必須是組織管理角色群組的成員，混合組態精靈才能順利完成這些工作。

3.  **進行混合式部署組態變更**   測試混合管理帳戶、進行驗證和拓撲檢查，以及收集您在精靈程序中定義的組態資訊之後，混合組態精靈會進行組態變更以建立和啟用混合式部署。混合組態的所有變更都會自動記錄在混合組態記錄檔中。依預設，混合組態記錄檔位於內部部署信箱伺服器上的 `%UserProfile%\AppData\Roaming\Microsoft\Exchange Hybrid Configuration`。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ906432.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>輸入郵件流程是由組織的 MX 記錄所控制。混合式部署的內送網際網路電子郵件不是由混合組態精靈所設定。</td>
    </tr>
    </tbody>
    </table>


## 混合組態功能

混合組態精靈預設會在每次執行時，自動啟用所有混合式部署功能。如果您要停用特定的混合組態功能，則需要使用 Exchange 管理命令介面 和 **Set-HybridConfiguration** Cmdlet。依預設，精靈會啟用下列混合式部署功能：

  - **空閒/忙碌資訊共用**   空閒/忙碌資訊共用功能可讓行事曆資訊在內部部署和 Exchange Online 組織使用者之間共用。空閒/忙碌資訊共用會在進行內部部署和 Exchange Online 組織的同盟共用和組織關聯性組態設定時啟用。若要深入了解，請參閱 [共用](https://technet.microsoft.com/zh-tw/library/dd638083\(v=exchg.150\))。

  - **郵件提示**   郵件提示是使用者在撰寫郵件時，對使用者顯示的資訊性訊息。藉由在混合式部署中啟用郵件提示，內部部署和 Exchange Online 寄件者即可調整他們正在撰寫的郵件，以避免組織間出現不希望發生的狀況或未傳遞回報 (NDR)。若要深入了解，請參閱 [MailTips](https://technet.microsoft.com/zh-tw/library/jj649091\(v=exchg.150\))。

  - **線上封存**   線上封存可讓 Exchange Online 組織為內部部署及 Exchange Online 使用者兩者主控使用者的電子郵件封存。若要深入瞭解，請參閱[設定 Exchange Online 封存](http://go.microsoft.com/fwlink/p/?linkid=266565)。

  - **網頁型 Outlook 重新導向**網頁型 Outlook 重新導向提供單一的通用 URL，可存取內部部署信箱和 Exchange Online 信箱。Client Access Server 會自動將 網頁型 Outlook 要求重新導向至內部部署信箱伺服器，或為 Exchange Onine 組織的使用者提供其信箱的連結。

  - **Exchange ActiveSync 重新導向**  當您將信箱從您的內部部署 Exchange 組織移至 Exchange Online 時，所有存取信箱的用戶端都必須更新為使用 Exchange Online；其中包括 Exchange ActiveSync 裝置。大部分的 Exchange ActiveSync 用戶端即將在信箱移至 Exchange Online 時自動重新設定。如需詳細資訊，請參閱 [Exchange ActiveSync 裝置設定與 Exchange 混合式部署](exchange-activesync-device-settings-with-exchange-hybrid-deployments-exchange-2013-help.md)。

  - **安全郵件**    安全郵件可透過傳輸層安全性 (TLS) 通訊協定，在內部部署和 Exchange Onine 組織之間啟用安全郵件傳遞。內部部署和 Exchange Onine 組織會透過數位憑證主體和電子郵件標頭進行相互驗證，而 RTF 郵件格式則在各組織間予以保留。

## 混合組態選項

混合組態精靈可讓您選取混合式部署中多個範圍的特定選項。如果您要在初次設定混合式部署之後更新特定混合組態選項，可以使用混合組態精靈或 Exchange 管理命令介面 選取不同的組態選項。

下表概述混合組態精靈修改及設定的主要選項。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>組態範圍</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>網域</p></td>
<td><p>此精靈會為混合式郵件流程將公認的網域加入到內部部署組織，並為雲端組織新增自動探索要求。此網域稱為<em>「共存網域」</em>，會當做次要 Proxy 網域新增到任何具有混合組態精靈中所選取網域之 <em>PrimarySmtpAddress</em> 範本的電子郵件地址原則。依預設，此網域為 &lt;domain&gt;.mail.onmicrosoft.com。</p>
<p>您可以在 Exchange Online 上的 Exchange 管理命令介面 中執行下列指令來檢視公認的網域。</p>
<pre><code>Get-AcceptedDomain | FL DomainName, IsCoexistenceDomain</code></pre></td>
</tr>
<tr class="even">
<td><p>安全郵件憑證</p></td>
<td><p>此精靈會要求您選取協力廠商憑證授權單位 (CA) 發行的特定憑證，用來驗證內部部署和 Exchange Online 組織之間傳送的安全電子郵件。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange 同盟共用</p></td>
<td><p>此精靈會檢查與內部部署組織的 Azure Active Directory 驗證系統之間，是否存在現有的 OAuth 驗證關係或同盟信任。如果存在，則會使用現有的 OAuth 驗證或同盟信任來支援混合式部署。如果不存在，此精靈會設定 OAuth 驗證或建立內部部署組織與 Azure AD 驗證系統的同盟信任，視內部部署 Exchange 組態的類型而定。此精靈也會視需要將混合組態精靈中選取的任何網域加入至同盟信任。</p>
<p>除了 OAuth 驗證或同盟信任組態之外，此精靈還會為內部部署和 Exchange Online 組織建立和設定組織關聯性。這些組織關聯性可讓精靈啟用多個混合式部署功能，包括空閒/忙碌資訊共用、網頁型 Outlook 重新導向及郵件提示。</p></td>
</tr>
<tr class="even">
<td><p>郵件流程</p></td>
<td><p>此精靈可讓您選取及設定欲使用哪些 Exchange 伺服器來處理內部部署和 Exchange Online 組織之間的安全郵件傳輸。在 Exchange 2010 中，此為 Hub Transport server。在 Exchange 2013 中，此為 Client Access server。在 Exchange 2016 及更新版本中，此為信箱伺服器。</p>
<p>此精靈可設定您的內部部署 Exchange 及 Exchange Online 組織以進行混合郵件路由。透過在內部部署組織中設定新的和現有的傳送和接收連接器，以及在 Exchange Online 中設定輸入和輸出連接器後，此精靈便可讓您選擇要將從 Exchange Online 組織傳遞到網際網路的輸出郵件直接傳送給外部郵件收件者，或是要透過包含在混合式部署中的內部部署 Exchange 伺服器進行路由。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/JJ906432.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>輸入郵件流程是由組織的 MX 記錄所控制。混合式部署的內送網際網路電子郵件不是由混合組態精靈所設定。</td>
</tr>
</tbody>
</table>

</td>
</tr>
</tbody>
</table>


## 混合組態引擎

「混合組態引擎」會執行設定及更新混合式部署所需的核心動作。負責處理 `Update-HybridConfiguration` Cmdlet 動作的「混合組態引擎」會比對 *HybridConfiguration*Active Directory 物件與目前內部部署 Exchange 和 Exchange Online 組態設定的狀態，然後再針對 *HybridConfiguration*Active Directory 物件中定義的參數執行符合部署組態設定的工作。如果目前的內部部署 Exchange 和 Exchange Online 部署組態狀態已符合 *HybridConfiguration*Active Directory 物件中定義的設定，則「混合組態引擎」不會對內部部署或 Exchange Online 組織進行任何變更。

更新現有的混合式部署時，「混合組態引擎」會執行下列步驟：

1.  *Update-HybridConfiguration* Cmdlet 會觸發「混合組態引擎」使其啟動。

2.  「混合組態引擎」會讀取儲存在 `HybridConfiguration`Active Directory 物件上的「需要的狀態」。

3.  「混合組態引擎」會探索內部部署 Exchange 組織的拓撲資料和目前的組態。

4.  「混合組態引擎」會探索 Exchange Online 組織的拓撲資料和目前的組態。

5.  根據需要的狀態、拓撲資料和目前的組態，「混合組態引擎」會在內部部署 Exchange 和 Exchange Online 組織間建立「差異」，然後執行組態工作以建立需要的狀態。

下圖概略說明在混合式部署程序進行期間，「混合組態引擎」擷取及修改內部部署 Exchange 伺服器和 Exchange Online 組態設定的方法。

![混合式組態引擎流程](images/Hh529921.7e01b239-b978-4377-9eac-aa5bc4561866(EXCHG.150).gif "混合式組態引擎流程")

