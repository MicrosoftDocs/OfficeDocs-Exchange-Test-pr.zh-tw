---
title: '同盟: Exchange 2013 Help'
TOCTitle: 同盟
ms:assetid: 0046e2eb-6940-4941-bd5b-cbe6bffa3b94
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd335047(v=EXCHG.150)
ms:contentKeyID: 50472444
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 同盟

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

資訊工作者常常需要與外部收件者、廠商、合作夥伴與客戶合作，並共用其空閒/忙碌 (也就是所謂的行事曆可用性) 資訊。Microsoft Exchange Server 2013 中的同盟有助於這些合作。*「同盟」*是指支援*「同盟共用」*的基礎信任基礎結構，對使用者而言，這是與其他外部同盟組織中的收件者共用行事曆資訊的簡易方法。若要深入了解同盟共用，請參閱[共用](sharing-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>此 Exchange Server 2013 功能與中國的 21Vianet 所運作的 Office 365 不完全相容，部分功能可能受限。如需詳細資訊，請參閱<a href="https://go.microsoft.com/fwlink/?linkid=313640">了解 21Vianet 運作的 Office 365</a>。</td>
</tr>
</tbody>
</table>


**目錄**

Key terminology

Azure AD 驗證系統

Federation trust

Federated organization identifier

Federation example

Certificate requirements for Federation

Transitioning to a new certificate

Firewall Considerations for Federation

## 重要詞彙

下表定義與 Exchange 2013 中的同盟相關聯的核心元件。

  - **應用程式識別碼 (AppID)**  
    唯一數字產生Azure Active Directory驗證系統的識別Exchange組織。當您使用Azure Active Directory驗證系統建立同盟信任，AppID 會自動產生。

<!-- end list -->

  - **委派 Token**  
    可讓使用者從一部同盟組織到另一個同盟組織所信任Azure Active Directory驗證系統發出安全性聲明標記語言 (SAML) 權杖。委派 token 包含使用者的電子郵件地址、 不變的識別碼及與 token 發行動作的產品項目相關資訊。

<!-- end list -->

  - **外部同盟組織**  
    建立與Azure Active Directory驗證系統的同盟信任外部Exchange組織。

<!-- end list -->

  - **同盟共用**  
    運用能夠跨Exchange組織Azure Active Directory驗證系統的同盟信任的Exchange功能的群組，包括跨部署Exchange部署。在一起，這些功能可用來進行伺服器代表跨多個Exchange組織使用者之間的驗證的要求。

<!-- end list -->

  - **同盟網域**  
    新增至 Exchange 組織之組織識別碼 (OrgID) 的公認授權網域。

<!-- end list -->

  - **網域證明加密字串**  
    提供組織擁有Azure Active Directory驗證系統搭配使用的網域證明Exchange組織所使用的密碼編譯安全字串。字串會自動產生時使用 \[**啟用同盟信任**\] 精靈或可產生使用**Get-FederatedDomainProof**指令程式。

<!-- end list -->

  - **同盟共用原則**  
    一個組織層級原則，可支援及控制由使用者建立、個人對個人的行事曆資訊共用。

<!-- end list -->

  - **同盟**  
    在兩個 Exchange 組織之間達成共同目的之以信任為基礎的合約。使用同盟時，兩個組織都希望一個組織的驗證判斷能由另一個組織所辨識。

<!-- end list -->

  - **同盟信任**  
    與定義下列元件Exchange組織Azure Active Directory驗證系統的關係：
    
      - 帳戶命名空間
    
      - 應用程式識別碼 (AppID)
    
      - 組織識別碼 (OrgID)
    
      - 同盟網域
    
    若要設定與其他同盟的Exchange組織的同盟共享，必須與Azure Active Directory驗證系統建立同盟信任。

<!-- end list -->

  - **非同盟組織**  
    不具與Azure Active Directory驗證系統建立同盟信任的組織。

<!-- end list -->

  - **組織識別碼 (OrgID)**  
    會定義授權的公認網域設定在組織中的哪些已啟用同盟。僅有使用 OrgID 中設定同盟網域的電子郵件地址的收件者會辨識Azure Active Directory驗證系統和能夠使用同盟共用功能。OrgID 是預先定義的字串以及選取 \[**啟用同盟信任**\] 精靈中的同盟的第一個公認的網域的組合。例如，如果您指定為貴組織的主要 SMTP 網域的同盟的網域 contoso.com，帳戶命名空間 FYDIBOHF25SPDLT.contoso.com 會是自動建立為同盟信任 OrgID。

<!-- end list -->

  - **組織關聯性**  
    允許收件者共用空閒/忙碌資訊 （行事曆可用性） 資訊的兩個同盟的Exchange組織之間一對一的關係。組織關聯性需要與Azure Active Directory驗證系統的同盟信任和取代使用Active DirectoryExchange組織之間的樹系或網域信任需要。

<!-- end list -->

  - **Azure Active Directory驗證系統**  
    做為同盟 Microsoft Exchange組織之間的信任 broker 免費、 雲端身分識別服務。它會負責時所要求來自其他同盟的Exchange組織中收件者的資訊會核發委派 token Exchange收件者。若要深入了解，請參閱[Azure Active Directory](https://go.microsoft.com/fwlink/?linkid=392500)。

## Azure AD 驗證系統

Azure Active Directory驗證系統，由 Microsoft 提供的免費雲端式服務會為您的內部部署Exchange 2013組織和其他同盟的Exchange 2010和Exchange 2013組織之間的信任代理人。如果您想Exchange組織中設定同盟，您必須建立一次性的同盟信任與Azure Active Directory驗證系統，使其可成為與您組織的同盟協力廠商。與此信任位置中，依Active Directory （又稱為*身分識別提供者*） 來驗證的使用者是由Azure AD驗證系統發出安全性聲明標記語言 (SAML) 委派 token。下列委派 token 允許使用者從一部同盟的Exchange組織到另一個同盟的Exchange組織所信任。使用Azure AD驗證系統做為信任 broker 組織未所需的建立與其他組織的多個個別的信任關係及使用者可存取外部資源的使用單一登入 (SSO) 體驗。如需詳細資訊，請參閱[Azure Active Directory](https://go.microsoft.com/fwlink/?linkid=392500)。

回到頁首

## 同盟信任

若要使用Exchange 2013同盟共用功能，您必須Exchange 2013組織和Azure AD驗證系統之間建立同盟信任。建立與Azure AD驗證系統的同盟信任進行交換Azure AD驗證系統與您的組織數位安全性憑證並擷取Azure AD驗證系統憑證和同盟中繼資料。您可以使用 \[**啟用同盟信任**精靈在 Exchange 系統管理中心 (EAC) 或**New-FederationTrust**指令程式在Exchange管理命令介面來建立同盟信任。自我簽署的憑證的 \[**啟用同盟信任**\] 精靈會自動建立並用於簽署和加密Azure AD驗證系統中的委派 token 可讓使用者可信任的外部同盟組織。如需憑證需求的詳細資訊，請參閱本主題稍後的同盟的憑證需求。

當您對Azure AD驗證系統建立同盟信任時，*應用程式識別碼*(AppID) 是自動產生Exchange組織和**Get-FederationTrust**指令程式的輸出中所提供。應用程式識別碼是Azure AD驗證系統用來唯一地識別組織Exchange 。它也會提供證明您的組織擁有Azure AD驗證系統搭配使用的網域使用Exchange組織。做法是建立部署公用網域名稱系統 (DNS) 區域每個同盟網域中的文字 (TXT) 記錄。

回到頁首

## 同盟組織識別碼

*同盟組織識別碼*(OrgID) 會定義授權的公認網域設定於組織中的哪些已啟用同盟。僅有使用中 OrgID 設定公認的網域的電子郵件地址的收件者會辨識Azure AD驗證系統且能夠使用同盟共用功能。當您建立新的同盟信任時，OrgID 會自動建立與Azure AD驗證系統。此 OrgID 是預先定義的字串和公認的網域選取精靈中的共用網域作為的組合。例如在 Edit Sharing-Enabled 網域精靈\] 如果您組織中指定作為主要的共用網域同盟的網域**contoso.comFYDIBOHF25SPDLT.contoso.com**帳戶命名空間將會自動建立為 OrgID Exchange組織的同盟信任。

雖然通常Exchange組織，此網域的主要 SMTP 網域沒有為 Exchange 組織中公認的網域並不需要網域名稱系統 (DNS) 證明擁有權的 TXT 記錄。唯一的需求是公認的網域選取要加入同盟會限制最大值為 32 個字元。此子網域的唯一目的是做為該要求 SAML 委派 token 維護收件者的唯一識別碼的Azure AD驗證系統的同盟命名空間。如需 SAML 權杖的詳細資訊，請參閱[SAML 權杖及宣告](https://go.microsoft.com/fwlink/?linkid=198561)

可隨時從同盟信任中新增或移除接受的網域。如果您要啟用或停用組織中的所有同盟共用功能，只要啟用或停用同盟信任的 OrgID 即可。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您變更 OrgID、公認的網域或用於同盟信任的 AppID，組織中的所有同盟共用功能都會受到影響。這也會影響所有的外部同盟 Exchange 組織，包括 Exchange Online 以及混合部署組態。建議您通知所有外部同盟夥伴關於這些同盟信任組態設定的所有變更。</td>
</tr>
</tbody>
</table>


回到頁首

## 同盟範例

兩個Exchange組織 Contoso，ltd。 及 Fabrikam，Inc.希望能夠彼此共用行事曆空閒/忙碌資訊其使用者。每個組織Azure AD驗證系統建立同盟信任並設定其包含使用其使用者的電子郵件地址的網域的網域的帳戶命名空間。

Contoso 員工使用的其中一個下電子郵件位址網域： contoso.com、 contoso.co.uk 新增或 contoso.ca。Fabrikam 員工使用的其中一個下電子郵件位址網域： fabrikam.com、 fabrikam.org、 或 fabrikam.net 之類的網域。兩個組織請確定所有公認的網域的電子郵件都包含在其與Azure AD驗證系統的同盟信任的帳戶命名空間。不需要兩個組織之間的複雜Active Directory樹系或網域信任組態，這兩個組織設定組織關係彼此啟用行事曆空閒/忙碌資訊共用。

下圖說明 Contoso, Ltd. 和 Fabrikam, Inc. 之間的同盟組態。

**同盟共用範例**

![同盟信任和同盟共用](images/Dd335047.310f0698-b67d-4b0e-91e4-231c6e9db952(EXCHG.150).gif "同盟信任和同盟共用")

## 同盟的憑證需求

若要建立同盟信任與Azure AD驗證系統的自我簽署的憑證或簽署的憑證授權單位的 X.509 憑證必須建立並安裝於用來建立信任Exchange 2013伺服器 (CA)。我們強烈建議使用自我簽署的憑證，系統會自動建立並安裝在 EAC 中使用 \[**啟用同盟信任**\] 精靈。此憑證只能用來簽署和加密用於同盟共用的委派 token 和只有一個憑證所需的同盟信任。Exchange 2013自動分散每個要在組織中的所有其他Exchange 2013伺服器的憑證。

如果您要使用外部 CA 所簽署的 X.509 憑證，該憑證必須符合下列需求：

  - **受信任的 CA**   如果可能的話，X.509 安全通訊端層 (SSL) 憑證應由Windows Live 所信任的 CA 發出。不過，您能使用目前尚未獲 Microsoft 認證的 CA 所發出之憑證。如欲瞭解目前的受信任 CA 清單，請參閱 [同盟信任之信任的根憑證授權](trusted-root-certification-authorities-for-federation-trusts-exchange-2013-help.md)。

  - **主體金鑰識別碼**   憑證必須有主體金鑰識別碼欄位。由商業 CA 發出的大多數 X.509 憑證都有這個識別碼。

  - **CryptoAPI 密碼編譯服務提供者 (CSP)**  憑證必須使用 CryptoAPI CSP。使用密碼編譯 API 的憑證： 下一個產生 (CNG) 提供者不支援同盟。如果您使用Exchange來建立憑證要求時，會使用 CryptoAPI 提供者。如需詳細資訊，請參閱[密碼編譯 API︰ 新一代](https://go.microsoft.com/fwlink/?linkid=187890)。

  - **RSA 簽章演算法**   憑證必須使用 RSA 作為簽章演算法。

  - **可匯出私密金鑰**   用於產生憑證的私密金鑰必須可匯出。當您使用 EAC 中的 \[新增 Exchange 憑證\]精靈，或命令介面中的 [New-ExchangeCertificate](https://technet.microsoft.com/zh-tw/library/aa998327\(v=exchg.150\)) 指令程式建立憑證要求時，您可以指定私密金鑰為可匯出。

  - **目前的憑證**   憑證必須是當今的。您無法使用過期或撤銷的憑證建立同盟信任。

  - **增強金鑰使用方法**   憑證必須包含增強金鑰使用方法 (EKU) 類型 \[用戶端驗證 (1.3.6.1.5.5.7.3.2)\]。此使用方法類型用來向遠端電腦證明您的身分識別。如果您使用 EAC 或命令介面產生憑證要求，則預設會包含此使用方法類型。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>因為憑證未用於驗證，所以沒有任何的主體名稱或主體別名需求。您可以使用其主體名稱與主機名稱、網域名稱或其他任何名稱相同的憑證。</td>
</tr>
</tbody>
</table>


回到頁首

## 轉換為新憑證

用於建立同盟信任的憑證可指定為目前憑證。不過，您可能需要定期為同盟信任安裝並使用新的憑證。例如，如果目前的憑證到期，您可能需要使用新的憑證，或者，您可能需要符合新的商務或安全性需求。為了確保能夠無縫轉換成新的憑證，您必須在您的 Exchange 2013 伺服器上安裝新的憑證，並設定同盟信任將新憑證指定為新憑證。Exchange 2013 會自動將新憑證散佈至組織中的其他 Exchange 2013 伺服器。散佈憑證可能需要一些時間，時間長短則取決於您的 Active Directory 拓撲。您可以使用命令介面中的 [Test-FederationTrustCertificate](https://technet.microsoft.com/zh-tw/library/dd335228\(v=exchg.150\)) 指令程式來驗證憑證狀態。

確認憑證的通訊群組狀態之後，您可以設定以使用新的憑證的信任。後切換憑證，目前的憑證指派為先前的憑證，並將新的憑證指定為目前的憑證。將新的憑證發佈至Azure AD驗證系統並使用新的憑證加密所有新的權杖交換Azure AD驗證系統。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>此憑證轉換程序僅由同盟使用。如果您為其他需要憑證的 Exchange 2013 功能使用相同的憑證，則當規劃取得、安裝或轉換成新憑證時，您必須將該功能需求納入考量。</td>
</tr>
</tbody>
</table>


回到頁首

## 同盟的防火牆考量

同盟功能需要您組織中的 Mailbox 和 Client Access Server 必須可使用 HTTPS 向外存取網際網路。您必須允許組織中的所有 Exchange 2013 Mailbox 和 Client Access Server 可透過 HTTPS 向外存取 (連接埠 443 供 TCP 使用)。

為了讓外部組織存取您組織的空閒/忙碌資訊，您必須將一個 Client Access Server 發行至網際網路。這需要 HTTPS 從網際網路向內存取 Client Access Server。Active Directory 站台若未將 Client Access Server 發行至網際網路，則站台中的 Client Access Server 可以使用其他可從網際網路存取的 Active Directory 站台中的 Client Access Server。尚未發行至網際網路的 Client Access Server 必須有 Web 服務虛擬目錄的外部 URL，該虛擬目錄已設定外部組織看得到的 URL。

[回到頁首](sharing-exchange-2013-help.md)

