---
title: '設定裝置的 OWA 的推入通知代理: Exchange 2013 Help'
TOCTitle: 設定裝置的 OWA 的推入通知代理
ms:assetid: c0f4912d-8bd3-4a54-9097-03619c645c6a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn511017(v=EXCHG.150)
ms:contentKeyID: 59954257
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定裝置的 OWA 的推入通知代理

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

針對 Microsoft Exchange 2013 的內部部署啟用 裝置的 OWA (OWA for iPhone 和 OWA for iPad) 的推播通知，可讓使用者在自己的 OWA for iPhone 和 OWA for iPad 的 Outlook Web App 圖示上接收更新，以指出使用者收件匣中的未讀郵件數目。如果未設定並啟用推播通知，則具有 裝置的 OWA 的使用者在未啟動該應用程式的情況下，便無法得知收件匣中有未讀郵件。有新的郵件送達時，使用者裝置上的 裝置的 OWA 徽章會更新，看起來就像下列徽章。

![裝置名牌的 OWA](images/Dn511017.f399ba74-5395-4d24-ae7d-d16bf0ac7b35(EXCHG.150).png "裝置名牌的 OWA")

## 如何啟用推播通知？

若要啟用推播通知，內部部署 Exchange 2013 伺服器必須連線至 Office 365 推播通知服務，才能將推播通知傳送至 iPhone 和 iPad。Exchange 2013 內部部署伺服器會透過 Office 365 通知服務路由傳送更新通知，而不必向協力廠商推播通知服務註冊開發人員帳戶。下圖顯示 iPhone 和 iPad 使用者如何取得未讀郵件之徽章更新的程序。

![推入通知的程序](images/Dn511017.36764ce6-7351-492f-a17e-c42b781e2781(EXCHG.150).jpg "推入通知的程序")

若要啟用推播通知，系統管理員必須：

1.  在企業用 Office 365 中註冊您的組織。

2.  將所有內部部署伺服器更新為 Exchange Server 2013 累計更新 3 (CU3) 或更新版本。

3.  將內部部署 Exchange 2013 設定為 Office 365 驗證

4.  啟用由內部部署 Exchange Server 2013 送往 Office 365 的推播通知，並確認推播通知可以運作。

## 在企業用 Office 365 中註冊您的組織

Office 365 是一項雲端架構服務，旨在協助達成您的組織對於健全安全性、可靠性和使用者生產力的需求。Office 365 所涉及的訂閱計劃可讓您存取透過網際網路 (雲端服務) 提供的 Office 應用程式和其他生產力服務，例如 Lync Web 會議功能和 Exchange Online 企業用託管電子郵件。

許多 Office 365 計劃還包含了最新 Office 應用程式的桌面版本，可供使用者安裝於多部電腦和裝置上。所有 Office 365 計劃都是依照訂閱方式 (每月或每年) 付費。若要找到更多資訊或在 Office 365 中註冊您的組織，請參閱[企業用 Office 365 是什麼？](http://go.microsoft.com/fwlink/?linkid=335705)。若要深入了解透過 Office 365 提供的各項服務，請參閱 [Office 365 服務說明](http://go.microsoft.com/fwlink/?linkid=335704)。

## 更新為 CU3 或更新版本

Exchange Server 2013 的累計更新 3 (CU3) 可解決 Exchange Server 2013 自發行 RTM 版之後所發現的問題。此更新包含 CU1 和 CU2 中的所有問題和修正，以及 CU2 發行後的其他修正和更新。強烈建議所有 Exchange Server 2013 內部部署客戶採用此更新，且需要有此更新才能使用推播通知。若要了解累計更新 (包括 CU3)，請參閱 [更新 Exchange 2013](updates-for-exchange-2013-exchange-2013-help.md)。

## 將內部部署 Exchange 2013 設定為 Office 365 驗證

Exchange Server 2013 使用單一、標準化方式進行伺服器對伺服器驗證。[Exchange Server 2013](http://go.microsoft.com/fwlink/?linkid=290946) (以及 [Lync Server 2013](http://go.microsoft.com/fwlink/?linkid=273796) 和 [SharePoint 2013](http://go.microsoft.com/fwlink/?linkid=335701)) 和 [Office 2013](http://go.microsoft.com/fwlink/?linkid=335696) 都支援以 OAuth (開啟授權) 通訊協定進行伺服器對伺服器驗證與授權。有了 OAuth (許多主要網站所用的一種標準授權通訊協定)，就不必在不同電腦之間傳遞使用者認證和密碼。而是會以 OAuth 安全性權杖為基礎進行驗證和授權；這些權杖會授與使用者在特定一段時間內存取一組特定資源的權限。

OAuth 驗證通常與三個元件有關：一個授權伺服器以及兩個需要彼此通訊的領域。安全性權杖是由授權伺服器 (也稱為安全性權杖伺服器) 發行給兩個需要通訊的領域；這些權杖會確認源自其中一個領域的通訊應受到另一個領域的信任。例如，授權伺服器發行的權杖可確認來自特定 Lync Server 2013 領域的使用者能夠存取指定的 Exchange 2013 領域 (反之亦然)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>領域是安全性容器。</td>
</tr>
</tbody>
</table>


不過，內部部署伺服器對伺服器的驗證不需要使用協力廠商權杖伺服器。各項伺服器產品 (如 Lync Server 2013 和 Exchange 2013) 都有內建的權杖伺服器，可用於驗證其他支援伺服器對伺服器驗證的 Microsoft 伺服器 (如 SharePoint Server)。例如，Lync Server 2013 可以自行發行並簽署安全性權杖，然後使用該權杖來與 Exchange 2013 通訊。在這種情況下，便不需要協力廠商權杖伺服器。

若要將內部部署的 Exchange Server 2013 實作的伺服器對伺服器驗證設定為 Office 365，您必須完成兩個步驟：

  -  
    **步驟 1 – 將憑證指派給內部部署 Exchange Server 的內建權杖發行者。**首先，內部部署 Exchange 系統管理員必須使用下列 Exchange 管理命令介面指令碼來建立憑證 (如果先前尚未建立憑證)，並將該憑證指派給內部部署 Exchange Server 的內建權杖發行者。這項程序只需進行一次；憑證建立好之後，便可重複用於其他驗證情況且不會被取代。務必要將 *$tenantDomain* 的值更新為您的網域名稱。若要這麼做，請複製並貼上下列程式碼。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb125224.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>複製程式碼並貼到文字編輯器 (如「記事本」) 中並以 .ps1 副檔名加以儲存，以便能夠輕易執行命令介面指令碼。</td>
    </tr>
    </tbody>
    </table>
    
        # Make sure to update the following $tenantDomain with your Office 365 tenant domain.
        
        $tenantDomain = "Fabrikam.com"
        
        # Check whether the cert returned from Get-AuthConfig is valid and keysize must be >= 2048
        
        $c = Get-ExchangeCertificate | ?{$_.CertificateDomains -eq $env:USERDNSDOMAIN -and $_.Services -ge "SMTP" -and $_.PublicKeySize -ge 2048 -and $_.FriendlyName -match "OAuth"}
        If ($c.Count -eq 0)
        {
            Write-Host "Creating certificate for oAuth..."
            $ski = [System.Guid]::NewGuid().ToString("N")
            $friendlyName = "Exchange S2S OAuth"
            New-ExchangeCertificate -FriendlyName $friendlyName -DomainName $env:USERDNSDOMAIN -Services Federation -KeySize 2048 -PrivateKeyExportable $true -SubjectKeyIdentifier $ski
            $c = Get-ExchangeCertificate | ?{$_.friendlyname -eq $friendlyName}
        }
        ElseIf ($c.Count -gt 1)
        {
            $c = $c[0]
        }
        
        $a = $c | ?{$_.Thumbprint -eq (get-authconfig).CurrentCertificateThumbprint}
        If ($a.Count -eq 0)
        {
            Set-AuthConfig -CertificateThumbprint $c.Thumbprint
        }
        Write-Host "Configured Certificate Thumbprint is:"(get-authconfig).CurrentCertificateThumbprint
        
        # Export the certificate
        
        Write-Host "Exporting certificate..."
        if((test-path $env:SYSTEMDRIVE\OAuthConfig) -eq $false)
        {
            md $env:SYSTEMDRIVE\OAuthConfig
        }
        cd $env:SYSTEMDRIVE\OAuthConfig
        
        $oAuthCert = (dir Cert:\LocalMachine\My) | where {$_.FriendlyName -match "OAuth"}
        $certType = [System.Security.Cryptography.X509Certificates.X509ContentType]::Cert
        $certBytes = $oAuthCert.Export($certType)
        $CertFile = "$env:SYSTEMDRIVE\OAuthConfig\OAuthCert.cer"
        [System.IO.File]::WriteAllBytes($CertFile, $certBytes)
        
        # Set AuthServer
        $authServer = Get-AuthServer MicrosoftSts;
        if ($authServer.Length -eq 0)
        {
            Write-Host "Creating AuthServer Config..."
            New-AuthServer MicrosoftSts -AuthMetadataUrl https://accounts.accesscontrol.windows.net/metadata/json/1/?realm=$tenantDomain
        }
        elseif ($authServer.AuthMetadataUrl -ne "https://accounts.accesscontrol.windows.net/metadata/json/1/?realm=$tenantDomain")
        {
            Write-Warning "AuthServer config already exists but the AuthMetdataUrl doesn't match the appropriate value. Updating..."
            Set-AuthServer MicrosoftSts -AuthMetadataUrl https://accounts.accesscontrol.windows.net/metadata/json/1/?realm=$tenantDomain
        }
        else
        {
            Write-Host "AuthServer Config already exists."
        }
        Write-Host "Complete."
    
    預期的結果應該會類似下列輸出。
    
        Configured Certificate Thumbprint is: 7595DBDEA83DACB5757441D44899BCDB9911253C
        Exporting certificate...
        Complete.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb125224.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>在繼續之前， Windows PowerShell 的 Azure Active Directory 模組指令程式，則需要。如果尚未安裝 （先前稱為 PowerShell 的 Microsoft Online Services 模組 for Windows） Windows PowerShell 的 Azure Active Directory 模組指令程式，您可以從<a href="http://aka.ms/aadposh">管理 Azure AD 使用 Windows PowerShell</a>來進行安裝。</td>
    </tr>
    </tbody>
    </table>


  -  
    **步驟 2 – 設定 Office 365 以便與內部部署 Exchange 2013 通訊。**將要作為 Exchange Server 2013 通訊對象的 Office 365 伺服器設定為合作夥伴應用程式。例如，若內部部署 Exchange Server 2013 需要與 Office 365 通訊，您就必須將內部部署 Exchange 設定為合作夥伴應用程式。合作夥伴應用程式就是 Exchange 2013 可以與其直接交換安全性權杖，而不必經過協力廠商安全性權杖伺服器的應用程式。內部部署 Exchange 2013 系統管理員必須使用下列 Exchange 管理命令介面指令碼，將要作為 Exchange 2013 通訊對象的 Office 365 租用戶設定為夥伴應用程式。在執行期間，系統將會提示輸入 Office 365 租用戶網域的系統管理員使用者名稱和密碼 (例如，administrator@fabrikam.com)。如果先前的指令碼並未建立憑證，請務必將 *$CertFile* 的值更新為憑證的位置。若要這麼做，請複製並貼上下列程式碼。
    
        # Make sure to update the following $CertFile with the path to the cert if not using the previous script.
        
        $CertFile = "$env:SYSTEMDRIVE\OAuthConfig\OAuthCert.cer"
        
        If (Test-Path $CertFile)
        {
            $ServiceName = "00000002-0000-0ff1-ce00-000000000000";
        
            $objFSO = New-Object -ComObject Scripting.FileSystemObject;
            $CertFile = $objFSO.GetAbsolutePathName($CertFile);
        
            $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
            $cer.Import($CertFile);
            $binCert = $cer.GetRawCertData();
            $credValue = [System.Convert]::ToBase64String($binCert);
        
            Write-Host "Please enter the administrator user name and password of the Office 365 tenant domain..."
        
            Connect-MsolService;
            Import-Module msonlineextended;
        
            Write-Host "Adding a key to Service Principal..."
        
            $p = Get-MsolServicePrincipal -ServicePrincipalName $ServiceName
            New-MsolServicePrincipalCredential -AppPrincipalId $p.AppPrincipalId -Type asymmetric -Usage Verify -Value $credValue -StartDate $cer.GetEffectiveDateString() -EndDate $cer.GetExpirationDateString()
        }
        Else
        {
            Write-Error "Cannot find certificate."
        } 
    
    預期的結果應如下所示。
    
        Please enter the administrator user name and password of the Office 365 tenant domain...
        Adding a key to Service Principal...
        Complete.

## 啟用推播通知代理

在完成上述步驟而成功設定 OAuth 驗證之後，內部部署系統管理員必須使用下列指令碼來啟用推播通知代理。務必要將 *$tenantDomain* 的值更新為您的網域名稱。若要這麼做，請複製並貼上下列程式碼。

    $tenantDomain = "Fabrikam.com"
    Enable-PushNotificationProxy -Organization:$tenantDomain

預期的結果應該會類似下列輸出。

    RunspaceId        : 4f2eb5cc-b696-482f-92bb-5b254cd19d60
    DisplayName       : On Premises Proxy app
    Enabled           : True
    Organization      : fabrikam.com
    Uri               : https://outlook.office365.com/PushNotifications
    Identity          : OnPrem-Proxy
    IsValid           : True
    ExchangeVersion   : 0.20 (15.0.0.0)
    Name              : OnPrem-Proxy
    DistinguishedName : CN=OnPrem-Proxy,CN=Push Notifications Settings,CN=First Organization,CN=Microsoft
                        Exchange,CN=Services,CN=Configuration,DC=Domain,DC=extest,DC=microsoft,DC=com
    Guid              : 8b567958-58a4-403c-a8f0-524d7f1e9279
    ObjectCategory    : fabrikam.com/Configuration/Schema/ms-Exch-Push-Notifications-App
    ObjectClass       : {top, msExchPushNotificationsApp}
    WhenChanged       : 8/27/2013 7:23:47 PM
    WhenCreated       : 8/14/2013 1:30:27 PM
    WhenChangedUTC    : 8/28/2013 2:23:47 AM
    WhenCreatedUTC    : 8/14/2013 8:30:27 PM
    OrganizationId    :
    OriginatingServer : server.fabrikam.com
    ObjectState       : Unchanged

## 確認推播通知可以運作

在完成上述步驟之後，就可以透過下列其中一種方式測試推播通知：

  - **將測試電子郵件傳送到使用者的信箱：**
    
    1.  在行動裝置上於「裝置的 OWA」中設定帳戶，以便訂閱通知。
    
    2.  返回裝置主畫面，將「裝置的 OWA」退到背景中。
    
    3.  從其他裝置 (如電腦) 傳送電子郵件，使其送至在行動裝置上設定之帳戶的收件匣。
    
    4.  如此一來，應用程式圖示應該就會在幾分鐘內顯示未讀郵件計數。

  - **啟用監控：**另一種測試推播通知或調查通知失敗原因的方式，就是對貴組織的信箱伺服器啟用監控。內部部署 Exchange 2013 伺服器系統管理員必須使用下列指令碼來叫用推播通知 Proxy 監控。若要這麼做，請複製並貼上下列程式碼。
    
        # Send a push notification to verify connectivity.
        
        $s = Get-ExchangeServer | ?{$_.ServerRole -match "Mailbox"}
        If ($s.Count -gt 1)
        {
            $s = $s[0]
        }
        If ($s.Count -ne 0)
        {
            # Restart the monitoring service to clear the cache from when push was previously disabled.
            Restart-Service MSExchangeHM
        
            # Give the monitoring service enough time to load.
            Start-Sleep -Seconds:120
        
            Invoke-MonitoringProbe PushNotifications.Proxy\PushNotificationsEnterpriseConnectivityProbe -Server:$s.Fqdn | fl ResultType, Error, Exception
        }
        Else
        {
            Write-Error "Cannot find a Mailbox server in the current site."
        }
    
    預期的結果應該會類似下列輸出。
    
        ResultType : Succeeded
        Error      :
        Exception  :

