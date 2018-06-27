---
title: '混合部署必要條件: Exchange 2013 Help'
TOCTitle: 混合部署必要條件
ms:assetid: e7454db0-fed4-4662-8890-9501126b1ba2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh534377(v=EXCHG.150)
ms:contentKeyID: 50474713
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 混合部署必要條件

 


_**適用版本：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：** 2017-07-25_


**摘要：** 您的 Exchange 環境在您可以設定混合式部署之前需要的項目。

在您使用混合組態精靈建立與設定混合式部署之前，您現有的內部部署 Exchange 組織需要符合特定需求。如果您未符合這些需求，將無法完成混合組態精靈內的步驟，而且也無法在內部部署 Exchange 組織與 Exchange Online 之間設定混合式部署。

## 混合式部署的必要條件

下列為設定混合式部署時須具備的必要條件：

  - **內部部署 Exchange 組織**   您可以針對內部部署 Exchange 2007 組織或更新版本設定混合部署。
    
    在您的內部部署組織中所安裝的 Exchange 版本，決定了您所能安裝的混合式部署版本。通常情況下，您應該設定貴組織所能支援的最新混合式部署版本。舉例來說，若您的內部部署組織目前使用 Exchange 2007，您需要設定以 Exchange 2013 為基礎的混合式部署。如需 Exchange Server 與 Office 365 企業混合式部署功能的完整清單，請參閱下表。
    
    
    <table>
    <colgroup>
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>內部部署環境</th>
    <th>以 Exchange 2016 為基礎的混合部署</th>
    <th>以 Exchange 2013 為基礎的混合部署</th>
    <th>以 Exchange 2010 為基礎的混合部署</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Exchange 2016</p></td>
    <td><p>支援</p></td>
    <td><p>不支援</p></td>
    <td><p>不支援</p></td>
    </tr>
    <tr class="even">
    <td><p>Exchange 2013</p></td>
    <td><p>支援</p></td>
    <td><p>支援</p></td>
    <td><p>不支援</p></td>
    </tr>
    <tr class="odd">
    <td><p>Exchange 2010</p></td>
    <td><p>支援</p></td>
    <td><p>支援</p></td>
    <td><p>支援</p></td>
    </tr>
    <tr class="even">
    <td><p>Exchange 2007</p></td>
    <td><p>不支援</p></td>
    <td><p>支援</p></td>
    <td><p>支援</p></td>
    </tr>
    </tbody>
    </table>


  - **內部部署 Exchange 版本** 混合部署需要最新的累計更新或更新彙總套件，可供您已安裝在內部部署組織的 Exchange 版本使用。若您無法安裝最新的累計更新或更新彙總套件，亦支援前一版本。較舊的累計更新或更新彙總套件則無法提供支援。
    
    舉例來說，假設您已在內部部署組織安裝 Exchange 2013 累計更新 8，而目前 Exchange 2013 最新可用的版本是累計更新 10。為保持可受混合組態支援的狀態，至少需要將您的 Exchange 2013 伺服器升級累計更新 9。然而，我們強烈建議您升級至累計更新 10。
    
    累計更新與更新彙總套件會以每季一次的頻率發行。因此，若您定期需要額外時間來完成升級作業，請讓您的伺服器保持使用最新的累計更新或更新彙總套件，以便在時間上有些彈性。

  - **內部部署伺服器角色** 您需要安裝在貴內部部署組織的伺服器角色，需視您目前安裝的 Exchange 版本而定。
    
      - **Exchange 2010** 至少需有一部伺服器安裝了 Mailbox、Hub Transport 和 Client Access server role。雖然可以將 Mailbox、Hub Transport 和 Client Access role 安裝在不同的伺服器上，但我們強烈建議您在各個伺服器上安裝所有角色，以便提供額外的可靠性與經過改善的效能。
    
      - **Exchange 2013** 至少需有一部伺服器安裝了 Mailbox 和 Client Access server role。雖然可以將 Mailbox 與 Client Access role 安裝在不同的伺服器上，但我們強烈建議您在各個伺服器上安裝兩種角色，以便提供額外的可靠性與經過改善的效能。
    
      - **Exchange 2016 及更新版本** 至少需有一部伺服器已安裝 Mailbox server role。
    
    混合部署也支援執行 Edge Transport Server role 的 Exchange 伺服器。Edge Transport Server 也需要更新至適用於您目前所安裝 Exchange 版本的最新累計更新或更新彙總套件。我們強烈建議您在周邊網路部署 Edge Transport Server。Mailbox 及 Client Access server 則無法部署於周邊網路。

  - **Office 365**   所有支援 Azure Active Directory 同步處理 的 Office 365 計劃都支援混合式部署。所有的 Office 365 Enterprise、Government、Academic 和 Midsize 計劃都支援混合式部署。Office 365 Business 和 Home 計劃不支援混合式部署。
    
    若要深入了解，請參閱[註冊 Office 365](https://go.microsoft.com/fwlink/p/?linkid=203981)。

  - **自訂網域**   使用 Office 365 註冊任何您想在混合部屬內使用的自訂網域。您可以在您的內部部署組織中使用 Office 365 管理入口網站，或選擇設定 Active Directory 同盟服務 (AD FS) 來達成此一目的。
    
    若要深入了解，請參閱[新增網域至 Office 365](https://go.microsoft.com/fwlink/p/?linkid=229238)。

  - **Active Directory 同步處理**   部署Azure Active Directory Connect 工具，以啟用與內部部署組織的 Active Directory 同步處理。
    
    若要深入了解，請參閱 [Azure AD Connect 使用者登入選項](http://go.microsoft.com/fwlink/p/?linkid=723514)。

  - **自動探索 DNS 記錄**   為您現有的 SMTP 網域設定自動探索公用 DNS 記錄，以指向內部部署 Exchange 2013 Client Access Server。

  - **Exchange 系統管理中心 (EAC) 中的 Office 365 組織**   Office 365 組織節點預設包含在內部部署 EAC 中，但是您必須使用您的 Office 365 系統管理員認證，將 EAC 連線到 Office 365 組織才能使用混合式組態精靈。這樣還能讓您從單一管理主控台，同時管理內部部署與 Exchange Online 組織。
    
    若要深入了解，請參閱 [Exchange 混合式部署中的混合式管理](hybrid-management-in-exchange-hybrid-deployments-exchange-2013-help.md)。

  - 
    
    **憑證**   將 Exchange 服務安裝並指派至向受信任的憑證授權單位 (CA) 購買的有效數位憑證。雖然自我簽署憑證應用於與 Microsoft Federation Gateway 之間的內部部署同盟信任，但自我簽署憑證無法用於混合式部署中的 Exchange 服務。混合式部署中所設定 Exchange 上的網際網路資訊服務 (IIS) 執行個體必須擁有向受信任的 CA 購買的有效數位憑證。另外，在您的公共 DNS 中已指定的 EWS 外部 URL 與自動探索端點，必須列在憑證的主旨替代名稱 (SAN) 中。混合式部署中郵件傳輸所使用的 Exchange 伺服器上安裝的憑證全都必須使用相同的憑證 (也就是說，由相同 CA 所發行且擁有相同主旨)。
    
    若要深入了解，請參閱 [混合部署的憑證需求](certificate-requirements-for-hybrid-deployments-exchange-2013-help.md)。

  - **EdgeSync**   如果您已在內部部署組織中部署 Edge Transport Server，而且想要設定 Edge Transport Server 進行混合式安全郵件傳輸，則必須在使用混合式組態精靈之前先設定 EdgeSync。每次將新的累積更新或更新彙總套件套用至 Edge Transport Server 時，也須執行 EdgeSync。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ906432.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>雖然 EdgeSync 是使用 Edge Transport Server 的部署中所必需，但是當您設定 Edge Transport Server 進行混合安全郵件傳輸時，仍需要進行其他手動傳輸組態設定。</td>
    </tr>
    </tbody>
    </table>
    
    若要深入了解，請參閱 [Edge Transport server 與混合式部署](edge-transport-servers-with-hybrid-deployments-exchange-2013-help.md)。

  - **已啟用整合通訊 (UM) 信箱** 如果您有已啟用 UM 的信箱，且您想要將其移至 Office 365，除了 Exchange 混合式部署之外，您還需要下列項目。在您將任何已啟用 UM 的信箱移至 Office 365 **之前**，必須符合這些需求。
    
      - 與您的內部部署電話語音系統整合的 Lync Server 2010、Lync Server 2013 或商務用 Skype Server 2015 (或更新版本)，**或**
    
      - 與您的內部部署電話語音系統整合的商務用 Skype Online，**或**
    
      - 傳統的內部部署 PBX 或 IP-PBX 解決方案。
    
      - 在 Exchange Online 中所建立的 UM 信箱原則，對映您內部部署的組織中 UM 信箱原則的名稱。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/JJ150559.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>您可以將多個內部部署 UM 信箱原則對應至 Exchange Online 中的一個 UM 信箱原則。如果您想要執行這項操作，您必須使用 Exchange 管理命令介面，手動將每一個內部部署 UM 信箱原則對應至 Exchange Online 原則。</td>
        </tr>
        </tbody>
        </table>
    
    如需詳細資訊，請參閱 [UM 電話系統整合](https://technet.microsoft.com/zh-tw/library/jj673558\(v=exchg.150\))、[Exchange 2013 的電話語音 advisor](https://technet.microsoft.com/zh-tw/library/ee364753\(v=exchg.150\)) 和[設定雲端 PBX 語音信箱](https://go.microsoft.com/fwlink/p/?linkid=826207)。

## 混合式部署通訊協定、連接埠和端點

混合部署功能和元件需要 Office 365 可以存取特定傳入通訊協定、連接埠和連線端點，才能正確運作。設定混合部署之前，請確認內部部署網路和安全性組態可以支援下表中的功能和元件。除了允許特定的輸入通訊協定、連接埠和端點，您網路上的電腦也需要能夠存取列在 [Office 365 URL 與 IP 位址範圍](https://go.microsoft.com/fwlink/?linkid=823100) 中的 IP 位址、連接埠和 URL。


<table>
<colgroup>
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
</colgroup>
<thead>
<tr class="header">
<th>傳輸通訊協定</th>
<th>上層通訊協定</th>
<th>功能/元件</th>
<th>內部部署端點</th>
<th>內部部署路徑</th>
<th>驗證提供者</th>
<th>授權方法</th>
<th>是否支援預先驗證？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>TCP 25 (SMTP)</p></td>
<td><p>SMTP/TLS</p></td>
<td><p>Office 365 與內部部署之間的郵件流程</p></td>
<td><p>Exchange 2016 Mailbox/Edge</p>
<p>Exchange 2013 CAS/EDGE</p>
<p>Exchange 2010 HUB/EDGE</p></td>
<td><p>不適用</p></td>
<td><p>不適用</p></td>
<td><p>憑證型</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>自動探索</p></td>
<td><p>自動探索</p></td>
<td><p>Exchange 2016 Mailbox</p>
<p>Exchange 2013/2010 CAS</p></td>
<td><p>/autodiscover/autodiscover.svc/wssecurity</p>
<p>/autodiscover/autodiscover.svc</p></td>
<td><p>Azure AD 驗證系統</p></td>
<td><p>WS-Security 驗證</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>EWS</p></td>
<td><p>空閒/忙碌、寄件提醒、郵件追蹤</p></td>
<td><p>Exchange 2016 Mailbox</p>
<p>Exchange 2013/2010 CAS</p></td>
<td><p>/ews/exchange.asmx/wssecurity</p></td>
<td><p>Azure AD 驗證系統</p></td>
<td><p>WS-Security 驗證</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>EWS</p></td>
<td><p>多信箱搜尋</p></td>
<td><p>Exchange 2016 Mailbox</p>
<p>Exchange 2013/2010 CAS</p></td>
<td><p>/ews/exchange.asmx/wssecurity</p>
<p>/autodiscover/autodiscover.svc/wssecurity</p>
<p>/autodiscover/autodiscover.svc</p></td>
<td><p>驗證伺服器</p></td>
<td><p>WS-Security 驗證</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>EWS</p></td>
<td><p>信箱移轉</p></td>
<td><p>Exchange 2016 Mailbox</p>
<p>Exchange 2013/2010 CAS</p></td>
<td><p>/ews/mrsproxy.svc</p></td>
<td><p>NTLM</p></td>
<td><p>基本</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>自動探索</p>
<p>EWS</p></td>
<td><p>OAuth</p></td>
<td><p>Exchange 2016 Mailbox</p>
<p>Exchange 2013/2010 CAS</p></td>
<td><p>/ews/exchange.asmx/wssecurity</p>
<p>/autodiscover/autodiscover.svc/wssecurity</p>
<p>/autodiscover/autodiscover.svc</p></td>
<td><p>驗證伺服器</p></td>
<td><p>WS-Security 驗證</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>無</p></td>
<td><p>AD FS (隨附於 Windows)</p></td>
<td><p>Windows 2008/2012 Server</p></td>
<td><p>/adfs/*</p></td>
<td><p>Azure AD 驗證系統</p></td>
<td><p>會依每個組態而不同</p></td>
<td><p>雙因素</p></td>
</tr>
<tr class="even">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>無</p></td>
<td><p>Azure Active Directory Connect 搭配 AD FS</p></td>
<td><p>Windows 2012 R2 Server</p></td>
<td><p>/adfs/*</p></td>
<td><p>Azure AD 驗證系統</p></td>
<td><p>會依每個組態而不同</p></td>
<td><p>雙因素</p></td>
</tr>
</tbody>
</table>


## 建議的工具與服務

當您使用混合組態精靈設定混合式部署時，除了先前所述的必要條件之外，仍有其他有用的工具與服務：

  - **Exchange Server 部署助理**   Exchange Server 部署助理是一種免費 Web 型工具，可協助您在內部部署組織中部署 Exchange、設定內部部署組織與 Office 365 的混合式部署，或完全移轉至 Office 365。此工具會問您一小組簡單的問題，然後根據您的答案，建立部署或設定 Exchange Server 時所需的自訂指示檢查清單。部署助理會提供設定混合式部署時所需的確切正確資訊。
    
    若要深入了解，請參閱 [Exchange Server 部署助理](https://technet.microsoft.com/exdeploy2013)。
    
     

  - **Remote Connectivity Analyzer 工具**   Microsoft Remote Connectivity Analyzer 工具會檢查您內部部署 Exchange 組織的對外連線能力，並確保您能夠著手設定混合式部署。我們強烈建議您在使用混合組態精靈設定混合式部署前，先使用 Remote Connectivity Analyzer 工具來檢查您的內部部署組織。
    
    若要深入了解，請參閱：[Microsoft Remote Connectivity Analyzer](https://testconnectivity.microsoft.com/)。
    
     

  - **單一登入**   單一登入功能可讓使用者以單一使用者名稱和密碼存取內部部署和 Exchange Online 組織。還可提供使用者熟悉的單一登入體驗，並讓系統管理員能輕鬆地透過內部部署 Active Directory 管理工具來控制 Exchange Online 組織信箱的帳戶原則。
    
    部署單一登入時，您會有兩個選項：密碼同步處理和 Active Directory 同盟服務。這兩個選項皆由 Azure Active Directory Connect 提供。密碼同步化可讓幾乎任何組織 (不論大小) 輕鬆地實作單一登入。基於這個理由，且因混合式部署中的使用者經驗比啟用單一登入還要好得多，我們強烈建議實作它。對於超大型組織，例如有多個 Active Directory 樹系需要加入混合式部署的組織，需要 Active Directory 聯盟服務。
    
    若要深入了解，請參閱 [單一登入與混合式部署](single-sign-on-with-hybrid-deployments-exchange-2013-help.md)。

