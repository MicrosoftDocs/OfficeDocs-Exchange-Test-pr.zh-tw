---
title: '設定同盟信任: Exchange 2013 Help'
TOCTitle: 設定同盟信任
ms:assetid: 7c2b539f-faed-4374-8578-9f329ca628db
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ657462(v=EXCHG.150)
ms:contentKeyID: 50473573
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定同盟信任

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2017-07-26_

同盟信任會建立 Microsoft Exchange 2013組織和Azure Active Directory驗證系統之間的信任關係。透過設定同盟信任，您可以設定與共用行事曆空閒/忙碌資訊的收件者之間其他同盟 Exchange 組織的同盟共用。兩個同盟的Exchange 2013組織之間或同盟的Exchange 2013組織和同盟的Exchange 2010組織之間可以設定同盟共用。您也可以設定與 Office 365 組織共用。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>建立同盟信任是在您 Exchange 組織中設定同盟共用的數個步驟之一。若要檢閱所有步驟，請參閱<a href="configure-federated-sharing-exchange-2013-help.md">設定同盟共用</a>。</td>
</tr>
</tbody>
</table>


如需與同盟相關的其他管理工作，請參閱[同盟程序](federation-procedures-exchange-2013-help.md)。

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


## 開始之前有哪些須知？

  - 預估完成時間：30 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱「 同盟與憑證 」 權限中的項目[Exchange 及命令介面基礎結構權限](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)主題。

  - 用於建立同盟信任的網域應該要能夠從網際網路進行解析。若要這麼做，必須向網域註冊機構註冊該網域，並將網域的網域名稱系統 (DNS) 區域存放在可從網際網路存取的 DNS 伺服器上。如果組織可以接收該網域的網際網路電子郵件，表示已符合這些需求。

  - 您將需要新增 TXT 記錄到您的公用 DNS。請檢閱將 TXT 記錄新增至裝載公用 DNS 記錄之組織的需求。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

  - 這兩個Exchange組織同盟共用關係必須使用相同的Azure AD驗證系統對於其同盟信任。這項需求適用於設定同盟共用的兩個內部部署Exchange組織之間或內部Exchange組織部署和主控的Office 365https://go.microsoft.com/fwlink/?linkId=392576.

  - 當您為Exchange 2013組織與Azure AD驗證系統建立同盟信任時，同盟信任會使用Azure AD驗證系統的商務執行個體。不過，其他同盟 Exchange 組織與舊版 Exchange 的和現有的同盟信任使用Azure AD驗證系統的商務或取用者執行個體。
    
    下列Exchange組織預設使用Azure AD驗證系統的商務執行個體：
    
      - 使用 \[啟用同盟信任\] 精靈與自行簽署的憑證建立同盟信任的 Exchange 2013 組織。
    
      - Exchange 2010SP1 或更新版本組織使用**新的同盟信任**\] 精靈與自行簽署的憑證建立同盟信任。
    
      - Office 365 所主控的 Exchange 組織，例如 Exchange Online。
    
    下列Exchange組織預設使用Azure AD驗證系統的用戶執行個體：
    
      - 釋出的量產發行 (RTM) 版本的Exchange 2010組織使用協力廠商憑證授權單位所發出的憑證。
    
    建議所有Exchange組織的同盟信任都使用Azure AD驗證系統的商務執行個體。之前設定兩個的 Exchange 組織之間的同盟共用，您必須確認每個Exchange組織使用的任何現有的同盟信任之Azure AD驗證系統執行個體。若要判斷Exchange組織要使用現有的同盟信任之Azure AD驗證系統執行個體，請執行下列命令介面。
    
        Get-FederationInformation -DomainName <hosted Exchange domain namespace>
    
    商務執行個體傳回 *TokenIssuerURIs* 參數的 `<uri:federation:MicrosoftOnline>` 值。
    
    用戶執行個體傳回 *TokenIssuerURIs* 參數的 `<uri:WindowsLiveID>` 值。
    
    若要設定與現有的同盟信任使用Azure AD驗證系統的商務執行個體的Exchange組織的同盟共用，請遵循本主題中的步驟。這些步驟的所有您需要執行建立可用來啟用同盟共用的兩個Exchange 2013組織之間或Exchange 2013組織和已在使用Exchange 2010組織之間的同盟信任Azure AD驗證系統的商務執行個體。
    
    若要設定Exchange 2013組織與現有的同盟信任使用Azure AD驗證系統的用戶執行個體的Exchange組織之間的同盟共用的 Exchange 組織使用用戶執行個體應該安裝 Exchange 2010 SP2 或更新版本，或升級至Exchange 2013。如果您決定要安裝 Exchange 2010 SP2 或更新版本中，使用**新的同盟信任**精靈來移除並重新建立現有的同盟的網域和同盟信任。重新建立同盟信任之時，會使用Azure AD驗證系統的商務執行個體。

## 使用 EAC 來建立與設定同盟信任

1.  在內部部署組織中的 Exchange 2013 伺服器上，瀏覽至 \[組織\] \> \[共用\]。

2.  按一下 \[啟用\] 以啟動 \[啟用同盟信任\] 精靈。

3.  精靈完成之後，請按一下 \[關閉\]。

4.  在 \[共用\] 標籤的\[同盟信任\] 區段中，按一下 \[修改\]。

5.  在 \[已啟用共用的網域\] 中，在 \[步驟 1\] 旁邊，按一下 \[瀏覽\]。

6.  在 \[選取公認的網域\] 中，從清單中選取主要的共用網域，接著按一下 \[確定\]。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您所選取的網域將會用來設定同盟信任的 OrgID。如需 OrgID 的詳細資訊，請參閱<a href="federation-exchange-2013-help.md">同盟</a>。</td>
    </tr>
    </tbody>
    </table>


7.  記下 \[產生主要的共用網域同盟的網域證明。您將使用此字串公用 DNS 伺服器上建立 TXT 記錄。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>同盟的網域證明為英數字元的字串。若要避免輸入的錯誤，建議您將字串複製從 EAC 中，並將它貼到 [記事本] 之類的文字編輯器。您可以再文字編輯器中將它複製到剪貼簿，然後貼到<strong>文字</strong>欄位建立 TXT 記錄時。如果使用建立 TXT 記錄不正確的同盟網域證明字串、 Azure AD驗證系統將不能夠確認證明網域擁有權和您不可以將它新增至同盟的組織識別碼。</td>
    </tr>
    </tbody>
    </table>


8.  在 \[**步驟 2**中，按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")將其他的網域新增至將會需要同盟共用功能的使用者在組織中所使用的電子郵件地址的同盟信任\]。例如，如果您有使用例如 sales.contoso.com 其電子郵件地址中的子網域的使用者，您將 sales.contoso.com 將網域新增至同盟信任。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>其他每個選取的網域都會建立同盟網域證明字串。您必須在其他每個網域的公用 DNS 上建立不同的 TXT 記錄。</td>
    </tr>
    </tbody>
    </table>


9.  使用為每個網域建立的同盟網域證明字串，為您公用 DNS 伺服器上這些網域中每一個建立 TXT 記錄。視您的公用 DNS 主機的更新排程而定，DNS 變更的複寫可能需要 15 分鐘或更長的時間。

10. 在建立並複寫 TXT 記錄後，按一下 \[更新\]。

## 使用命令介面來建立與設定同盟信任

1.  執行此命令來建立同盟信任憑證的唯一主體金鑰識別碼：
    
        $ski = [System.Guid]::NewGuid().ToString("N")

2.  若要建立自我簽署的憑證的同盟信任使用下列語法：
    
        New-ExchangeCertificate -FriendlyName "<Descriptive Name>" -DomainName <domain> -Services Federation -KeySize 2048 -PrivateKeyExportable $true -SubjectKeyIdentifier $ski
    
    此範例會對Azure AD驗證系統建立同盟信任的自我簽署的憑證。憑證使用 Exchange 同盟共用的易記名稱值和網域值從**USERDNSDOMAIN**環境變數來擷取。
    
        New-ExchangeCertificate -FriendlyName "Exchange Federated Sharing" -DomainName $env:USERDNSDOMAIN -Services Federation -KeySize 2048 -PrivateKeyExportable $true -SubjectKeyIdentifier $ski

3.  若要建立同盟信任和自動部署在組織中Exchange伺服器上一個步驟中所建立的自我簽署的憑證，使用下列語法：
    
        Get-ExchangeCertificate | ?{$_.FriendlyName -eq "<FriendlyName>"} | New-FederationTrust -Name "<Descriptive Name>"
    
    本範例會建立名為 Azure AD 驗證的同盟信任和部署名為 Exchange 同盟共用的自我簽署的憑證。
    
        Get-ExchangeCertificate | ?{$_.FriendlyName -eq "Exchange Federated Sharing"} | New-FederationTrust -Name "Azure AD Authentication"

4.  使用此語法來傳回證明網域擁有權具有所需的任何設定同盟信任的網域的 TXT 記錄。
    
        Get-FederatedDomainProof -DomainName <domain>
    
    此範例會傳回證明網域擁有權具有所需的主要共用的網域 contoso.com 的 TXT 記錄。
    
        Get-FederatedDomainProof -DomainName contoso.com
    
    **附註：**
    
      - 每個網域或子網域的同盟信任需要證明網域擁有權 TXT 記錄，所以您可能需要執行此程序設定命令時間使用不同*DomainName*值的倍數。
    
      - 我們建議您在命令介面中以滑鼠右鍵按一下、 選取**Mark**、 選取**概念**\] 值，並按 Enter，以便可以建立 TXT 記錄時使用複製的網域證明字串。如果您使用不正確的同盟的網域證明字串建立 TXT 記錄， Azure AD驗證系統無法驗證您擁有權的網域，並將無法將其新增至同盟的組織識別碼。

5.  使用上一個步驟的資訊，請將同盟信任中包含的每個網域中您公用 DNS 伺服器上建立 TXT 記錄。視您公用 DNS 主機的更新排程，複寫 DNS 的變更可能需要 15 分鐘或更久。您已新增 TXT 記錄可用來驗證後繼續。

6.  執行此命令可從Azure AD擷取的中繼資料和憑證：
    
        Set-FederationTrust -RefreshMetadata -Identity "Azure AD authentication"

7.  使用此語法來設定您在步驟 3 中建立同盟信任的主要共用的網域。您指定的網域將用來設定同盟信任的組織識別碼 (OrgID)。如需 OrgID 的詳細資訊，請參閱 ＜[同盟組織識別碼](federation-exchange-2013-help.md)。
    
        Set-FederatedOrganizationIdentifier -DelegationFederationTrust "<Federation Trust Name>" -AccountNamespace <Accepted Domain> -Enabled $true
    
    此範例會將公認的網域 contoso.com 為主要共用同盟信任的網域名為 Azure AD 驗證。
    
        Set-FederatedOrganizationIdentifier -DelegationFederationTrust "Azure AD authentication" -AccountNamespace contoso.com -Enabled $true

8.  若要新增其他網域同盟信任，請使用下列語法：
    
        Add-FederatedDomain -DomainName <AdditionalDomain>
    
    此範例將子網域 sales.contoso.com 新增至同盟信任，因為與 sales.contoso.com 網域中的電子郵件地址的使用者需要同盟共用的功能。
    
        Add-FederatedDomain -DomainName sales.contoso.com
    
    請記住，任何網域或子網域新增至同盟信任需要證明網域擁有權 TXT 記錄

如需詳細的語法及參數資訊，請參閱[New-ExchangeCertificate](https://technet.microsoft.com/zh-tw/library/aa998327\(v=exchg.150\))、 [New-FederationTrust](https://technet.microsoft.com/zh-tw/library/dd351047\(v=exchg.150\))、 [Get-FederatedDomainProof](https://technet.microsoft.com/zh-tw/library/ff717833\(v=exchg.150\))、 [Set-FederationTrust](https://technet.microsoft.com/zh-tw/library/dd298034\(v=exchg.150\))、 [Set-FederatedOrganizationIdentifier](https://technet.microsoft.com/zh-tw/library/dd351037\(v=exchg.150\))及[Add-FederatedDomain](https://technet.microsoft.com/zh-tw/library/dd351208\(v=exchg.150\))。

## 如何知道這是否正常運作？

成功完成 \[啟用同盟信任\] 與 \[已啟用共用的網域\] 精靈即表示同盟信任如預期完成設定。

若要更進一步驗證您已成功建立與設定同盟信任，請執行下列操作：

1.  執行下列命令介面命令，確認同盟信任資訊。
    
        Get-FederationTrust | Format-List

2.  *\<PrimarySharedDomain\>*取代為您主要的共用網域，並執行下列命令介面命令來確認可以從您的組織擷取同盟資訊。
    
        Get-FederationInformation -DomainName <PrimarySharedDomain>

如需詳細的語法及參數資訊，請參閱 [Get-FederationTrust](https://technet.microsoft.com/zh-tw/library/dd351262\(v=exchg.150\)) 與 [Get-FederationInformation](https://technet.microsoft.com/zh-tw/library/dd351221\(v=exchg.150\))。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>

