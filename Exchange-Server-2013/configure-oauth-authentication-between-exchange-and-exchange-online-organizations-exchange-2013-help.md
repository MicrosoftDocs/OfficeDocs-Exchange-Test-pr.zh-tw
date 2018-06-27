---
title: '設定 Exchange 與 Exchange Online 組織之間的 OAuth 驗證: Exchange 2013 Help'
TOCTitle: 設定 Exchange 與 Exchange Online 組織之間的 OAuth 驗證
ms:assetid: f703e153-98e2-4268-8a6e-07a86b0a1d22
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn594521(v=EXCHG.150)
ms:contentKeyID: 61170837
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定 Exchange 與 Exchange Online 組織之間的 OAuth 驗證

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

只具有 Exchange 2013 的混合式部署是使用混合組態精靈來設定 OAuth 驗證。對於混合的 Exchange 2013/2010 和 Exchange 2013/2007 混合式部署，Office 365 與內部部署 Exchange 組織之間的新的混合式部署 OAuth 型驗證連線，並不是由混合組態精靈來設定。依預設，這些部署會繼續使用同盟信任程序。不過，整個組織必須使用新的 Exchange OAuth 驗證通訊協定，才能完整取得某些 Exchange 2013 功能。

新的 Exchange OAuth 驗證程序目前啟用下列 Exchange 功能：

  - 郵件權限管理 (MRM)

  - Exchange 就地 eDiscovery

  - Exchange 就地封存

對於以 Exchange 2013 和 Exchange Online 來實作混合式部署的所有混合的 Exchange 組織，在設定其混合式部署之後，建議使用混合組態精靈來設定 Exchange OAuth 驗證。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您的內部部署組織與累計更新 5 執行只有 Exchange 2013 伺服器或稍後安裝，執行混合式部署精靈而不是執行本主題中的步驟。<br />
此 Exchange Server 2013 功能與中國的 21Vianet 所運作的 Office 365 不完全相容，部分功能可能受限。如需詳細資訊，請參閱<a href="https://go.microsoft.com/fwlink/?linkid=313640">了解 21Vianet 運作的 Office 365</a>。</td>
</tr>
</tbody>
</table>


## 開始之前有哪些須知？

  - 完成此工作的預估時間：15 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [Exchange 及命令介面基礎結構權限](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)主題中的「同盟與憑證」權限項目。

  - 完成的混合式部署使用混合式部署精靈\] 設定。如需詳細資訊，請參閱[Exchange Server 混合部署](https://technet.microsoft.com/zh-tw/library/jj200581\(v=exchg.150\))。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

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


## 您要如何設定內部部署 Exchange 與 Exchange Online 組織之間的 OAuth 驗證？

## 步驟 1：建立 Exchange Online 組織的授權伺服器物件

在此程序中，您必須為 Exchange Online 組織指定一個已經過驗證的網域。這個網域應該與作為雲端電子郵件帳戶之主要 SMTP 網域的網域相同。在下列程序中，這個網域稱為「您已驗證的網域」。

在內部部署 Exchange 組織的 Exchange 管理命令介面 (Exchange PowerShell) 中執行下列命令。

    New-AuthServer -Name "WindowsAzureACS" -AuthMetadataUrl https://accounts.accesscontrol.windows.net/<your verified domain>/metadata/json/1

## 步驟 2：啟用 Exchange Online 組織的夥伴應用程式

在內部部署 Exchange 組織的 Exchange PowerShell 中執行下列命令。

    Get-PartnerApplication |  ?{$_.ApplicationIdentifier -eq "00000002-0000-0ff1-ce00-000000000000" -and $_.Realm -eq ""} | Set-PartnerApplication -Enabled $true

## 步驟 3：匯出內部部署授權憑證

在此步驟中，您必須執行 PowerShell 指令碼以匯出內部部署授權憑證，然後該憑證會在下一個步驟中匯入至 Exchange Online 組織。

1.  將下列文字儲存到 PowerShell 指令碼檔案 (例如 **ExportAuthCert.ps1**)。
    
        $thumbprint = (Get-AuthConfig).CurrentCertificateThumbprint
         
        if((test-path $env:SYSTEMDRIVE\OAuthConfig) -eq $false)
        {
            md $env:SYSTEMDRIVE\OAuthConfig
        }
        cd $env:SYSTEMDRIVE\OAuthConfig
         
        $oAuthCert = (dir Cert:\LocalMachine\My) | where {$_.Thumbprint -match $thumbprint}
        $certType = [System.Security.Cryptography.X509Certificates.X509ContentType]::Cert
        $certBytes = $oAuthCert.Export($certType)
        $CertFile = "$env:SYSTEMDRIVE\OAuthConfig\OAuthCert.cer"
        [System.IO.File]::WriteAllBytes($CertFile, $certBytes)

2.  在內部部署 Exchange 組織的 Exchange PowerShell 中，執行您在前一個步驟中建立的 PowerShell 指令碼。例如：
    
        .\ExportAuthCert.ps1

## 步驟 4： 將內部部署授權憑證上傳至 Azure Active Directory ACS

接下來，您必須使用 Windows PowerShell 上傳您匯出至Azure Active Directory 存取控制服務 (ACS)先前步驟中的內部部署授權憑證。若要這樣做， Windows PowerShell 的 Azure Active Directory 模組指令程式已經安裝。如果未安裝，請移至安裝Windows PowerShell 的 Azure Active Directory 模組<https://aka.ms/aadposh> 。安裝Windows PowerShell 的 Azure Active Directory 模組後完成下列步驟。

1.  按一下 \[開啟已安裝Azure AD指令程式的 Windows PowerShell 工作區的**Azure Active Directory 的 Windows PowerShell 模組**捷徑。在此步驟中的所有命令將都會使用 Windows PowerShell for Azure Active Directory主控台執行。

2.  將下列文字儲存到 PowerShell 指令碼檔案 (例如 **UploadAuthCert.ps1**)。
    
        Connect-MsolService;
        Import-Module msonlineextended;
        
        $CertFile = "$env:SYSTEMDRIVE\OAuthConfig\OAuthCert.cer"
        
        $objFSO = New-Object -ComObject Scripting.FileSystemObject;
        $CertFile = $objFSO.GetAbsolutePathName($CertFile);
        
        $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
        $cer.Import($CertFile);
        $binCert = $cer.GetRawCertData();
        $credValue = [System.Convert]::ToBase64String($binCert);
        
        $ServiceName = "00000002-0000-0ff1-ce00-000000000000";
        
        $p = Get-MsolServicePrincipal -ServicePrincipalName $ServiceName
        New-MsolServicePrincipalCredential -AppPrincipalId $p.AppPrincipalId -Type asymmetric -Usage Verify -Value $credValue

3.  執行您在前一個步驟中建立的 PowerShell 指令碼。例如：
    
        .\UploadAuthCert.ps1

4.  啟動指令碼之後，會顯示 \[認證\] 對話方塊。輸入 Microsoft Online Azure AD組織中的租用戶系統管理員帳戶的認證。之後執行指令碼、 Windows PowerShell Azure AD工作階段保持在開啟狀態。您將使用此下一個步驟中執行 PowerShell 指令碼。

## 步驟 5： 利用 Azure Active Directory 註冊外部內部部署 Exchange HTTP 端點的所有主機名稱授權單位

在此步驟中，您必須對內部部署 Exchange 組織中每個可公開存取的端點執行指令碼。我們建議您盡可能使用萬用字元。例如，假設 **https://mail.contoso.com/ews/exchange.asmx** 可對外提供 Exchange。在此情況下，可使用單一萬用字元：**\*.contoso.com**。這會涵蓋 autodiscover.contoso.com 與 mail.contoso.com 端點。但是不涵蓋最上層網域 **contoso.com**。在最上層主機名稱授權單位可外部存取 Exchange 2013 Client Access Server 的情況下，此主機名稱授權單位也必須註冊為 **contoso.com**。註冊其他外部主機名稱授權單位並無限制。

若不確定內部部署 Exchange 組織中的外部 Exchange 端點，可以在內部部署 Exchange 組織的 Exchange PowerShell 中執行下列命令，即可取得外部設定的 Web 服務端點清單。

    Get-WebServicesVirtualDirectory | FL ExternalUrl

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>成功執行下列指令碼需要Azure Active Directory Windows PowerShell 連線至 Microsoft Online Azure AD租用戶，步驟 4 上一節所述。</td>
</tr>
</tbody>
</table>


1.  將下列文字儲存到 PowerShell 指令碼檔案 (例如 **RegisterEndpoints.ps1**)。這個範例使用萬用字元來註冊 contoso.com 的所有端點。以您的內部部署 Exchange 組織的主機名稱授權單位取代 **contoso.com**。
    
        $externalAuthority="*.contoso.com"
         
        $ServiceName = "00000002-0000-0ff1-ce00-000000000000";
         
        $p = Get-MsolServicePrincipal -ServicePrincipalName $ServiceName;
         
        $spn = [string]::Format("{0}/{1}", $ServiceName, $externalAuthority);
        $p.ServicePrincipalNames.Add($spn);
         
        Set-MsolServicePrincipal -ObjectID $p.ObjectId -ServicePrincipalNames $p.ServicePrincipalNames;

2.  在Azure Active Directory的 Windows PowerShell 中執行您在上一個步驟中建立 Windows PowerShell 指令碼。例如：
    
        .\RegisterEndpoints.ps1

## 步驟 6：建立從內部部署組織至 Office 365 的 IntraOrganizationConnector

您必須為 Exchange Online 中裝載的信箱定義目標位址。建立 Office 365 租用戶後，就會自動建立此目標位址。例如，如果您的組織裝載於 Office 365 承租人中的網域為 "contoso.com"，則目標服務位址為 "contoso.mail.onmicrosoft.com"。

使用 Exchange PowerShell，在內部部署組織中執行下列 Cmdlet：

    New-IntraOrganizationConnector -name ExchangeHybridOnPremisesToOnline -DiscoveryEndpoint https://outlook.office365.com/autodiscover/autodiscover.svc -TargetAddressDomains <your service target address>

## 步驟 7：建立從 Office 365 租用戶至內部部署 Exchange 組織的 IntraOrganizationConnector

您必須為內部部署組織中裝載的信箱定義目標位址。如果貴組織的主要 SMTP 位址為 "contoso.com"，則目標位址會是 "contoso.com"。

您還必須定義內部部署組織的外部自動探索端點。如果貴公司是 "contoso.com"，這通常是下列其中一項：

  - https://autodiscover.\<主要 SMTP 網域\>/autodiscover/autodiscover.svc

  - https://\<主要 SMTP 網域\>/autodiscover/autodiscover.svc

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您可同時在內部部署和 Office 365 租用戶中使用 <a href="https://technet.microsoft.com/zh-tw/library/dn551183(v=exchg.150)">Get-IntraOrganizationConfiguration</a> Cmdlet，以判斷 <a href="https://technet.microsoft.com/zh-tw/library/dn551178(v=exchg.150)">New-IntraOrganizationConnector</a> Cmdlet 所需的端點值。</td>
</tr>
</tbody>
</table>


使用 Windows PowerShell 執行下列 Cmdlet：

    $UserCredential = Get-Credential
    
    $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $UserCredential -Authentication Basic -AllowRedirection
    
    Import-PSSession $Session
    
    New-IntraOrganizationConnector -name ExchangeHybridOnlineToOnPremises -DiscoveryEndpoint <your on-premises Autodiscover endpoint> -TargetAddressDomains <your on-premises SMTP domain>

## 步驟 8：針對 Exchange 2013 SP1 以前的伺服器設定 AvailabilityAddressSpace

當您在 Exchange 2013 以前的組織中設定混合式部署時，在現有的 Exchange 組織中，您至少必須安裝一個具備 Client Access 和 Mailbox server role 的 Exchange 2013 SP1 或更新版本的伺服器。Exchange 2013 Client Access Server 和 Mailbox Server 作為前端伺服器，可協調現有 Exchange 內部部署組織與 Exchange Online 組織之間的通訊。此通訊包括內部部署與 Exchange Online 組織之間的郵件傳輸與訊息傳送功能。我們強烈建議您在內部部署組織中安裝多個 Exchange 2013 伺服器，以協助增進混合部署功能的可靠性與可用性。

在含有 Exchange 2013/2010 或 Exchange 2013/2007 的混合式部署中，內部部署組織的所有面向網際網路的前端伺服器最好都是執行 Exchange 2013 SP1 或更新版本的 Client Access Server。來自 Office 365 和 Exchange Online 的所有 Exchange Web 服務 (EWS) 要求，必須連接到內部部署中的 Exchange 2013 Client Access Server。此外，內部部署 Exchange 組織中針對 Exchange Online 而發出的所有 EWS 要求，必須經由執行 Exchange 2013 SP1 或更新版本的 Client Access Server 代理。因為這些 Exchange 2013 Client Access Server 必須處理此額外的輸入和輸出 EWS 要求，必須有足夠數量的 Exchange 2013 Client Access Server 來應付處理負載和提供連線備援。需要的 Client Access Server 數量取決於 EWS 要求的平均數目，且隨著組織而有所不同。

完成下列步驟之前，請確定：

  - 前端混合伺服器是 Exchange 2013 SP1 或更新版本

  - Exchange 2013 伺服器必須有唯一的外部 EWS URL。Office 365 承租人必須連接到這些伺服器，混合式功能的雲端要求才能正確運作。

  - 伺服器同時具備 Mailbox 和 Client Access server role

  - 任何現有的 Exchange 2010/2007 Mailbox Server 和 Client Access Server 已套用最新的累計更新 (CU) 或 Service Pack (SP)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>現有的 Exchange 2010/2007 Mailbox Server 可繼續使用 Exchange 2010/2007 Client Access Server 作為非混合式功能連線的前端伺服器。只有來自 Office 365 承租人的混合式部署功能才需要連接到 Exchange 2013 伺服器。</td>
    </tr>
    </tbody>
    </table>


在 Exchange 2013 以前的 Client Access Server 上，必須設定 *AvailabilityAddressSpace* 來指向內部部署 Exchange 2013 SP1 Client Access Server 的 Exchange Web 服務端點。此端點與前面步驟 5 所述的端點相同，也可以在內部部署 Exchange 2013 SP1 Client Access Server 上執行下列指令程式來決定：

    Get-WebServicesVirtualDirectory | FL AdminDisplayVersion,ExternalUrl

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果從多部伺服器傳回虛擬目錄資訊，請確定您使用針對 Exchange 2013 SP1 Client Access Server 傳回的端點。它將會針對 <em>AdminDisplayVersion</em> 參數顯示 15.0 (組建 847.32) 或以上版本。</td>
</tr>
</tbody>
</table>


若要設定 *AvailabilityAddressSpace*，請使用 Exchange PowerShell 並在內部部署組織中執行下列指令程式：

    Add-AvailabilityAddressSpace -AccessMethod InternalProxy -ProxyUrl <your on-premises External Web Services URL> -ForestName <your Office 365 service target address> -UseServiceAccount $True

## 如何知道這是否正常運作？

您可以使用 [Test-OAuthConnectivity](https://technet.microsoft.com/zh-tw/library/jj218623\(v=exchg.150\)) Cmdlet 驗證 OAuth 組態是否正確。此指令程式會驗證內部部署 Exchange 和 Exchange Online 端點是否可成功驗證彼此的要求。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用遠端 PowerShell 連線至 Exchange Online 組織時，您必須使用 <strong>Import-PSSession</strong> 指令程式並搭配 <em>AllowClobber</em> 參數，將最新的命令匯入至本機 PowerShell 工作階段。</td>
</tr>
</tbody>
</table>


若要驗證內部部署 Exchange 組織是否可成功連線至 Exchange Online，請在內部部署組織的 Exchange PowerShell 中執行下列命令：

    Test-OAuthConnectivity -Service EWS -TargetUri https://outlook.office365.com/ews/exchange.asmx -Mailbox <On-Premises Mailbox> -Verbose | fl

若要驗證 Exchange Online 組織是否可成功連線至內部部署 Exchange 組織，請使用[遠端 PowerShell](https://technet.microsoft.com/zh-tw/library/jj984289\(v=exchg.150\)) 連線至 Exchange Online 組織並執行下列命令：

    Test-OAuthConnectivity -Service EWS -TargetUri <external hostname authority of your Exchange On-Premises deployment>/metadata/json/1 -Mailbox <Exchange Online Mailbox> -Verbose | fl

如此，例如，Test-oauthconnectivity-服務 EWS TargetUri https://lync.contoso.com/metadata/json/1-Mailbox ExchangeOnlineBox1-Verbose |fl

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您可以忽略「沒有與 SMTP 位址關聯的信箱」錯誤。唯一重要的是 <em>ResultTask</em> 參數傳回 [成功] 值。例如，測試輸出的最後一個區段應該如下：<br />
<code>ResultType: Success</code><br />
<code>Identity: Microsoft.Exchange.Security.OAuth.ValidationResultNodeId</code><br />
<code>IsValid: True</code><br />
<code>ObjectState: New</code></td>
</tr>
</tbody>
</table>


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

