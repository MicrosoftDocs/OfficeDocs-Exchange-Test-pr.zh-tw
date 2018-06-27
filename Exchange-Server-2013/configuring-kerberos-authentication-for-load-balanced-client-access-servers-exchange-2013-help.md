---
title: '設定負載平衡的 Client Access server 的 Kerberos 驗證: Exchange 2013 Help'
TOCTitle: 設定負載平衡的 Client Access server 的 Kerberos 驗證
ms:assetid: 8f4faeea-a825-438d-97dc-1c398ce7aba5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ff808312(v=EXCHG.150)
ms:contentKeyID: 62835940
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定負載平衡的 Client Access server 的 Kerberos 驗證

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

**摘要：**說明如何使用 Kerberos 驗證與負載平衡的 Client Access server 在 Exchange 2013。

為了讓您使用負載平衡用戶端存取伺服器使用 Kerberos 驗證，您需要完成本文中所述的設定步驟。

## 在 Active Directory 網域服務中建立的備用服務帳戶認證

共用相同的命名空間和 Url 的所有用戶端存取伺服器需使用相同的備用服務帳戶認證。一般而言，它是足夠讓每個版本的 Exchange 樹系的單一帳戶。*備用服務帳戶認證*或*ASA 認證*。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Exchange 2010 與 Exchange 2013 無法共用相同的 ASA 認證。您需要建立新的 ASA 認證 for Exchange 2013。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>雖然共用命名空間支援 CNAME 記錄，Microsoft 建議使用 A 記錄。這可確保用戶端正確發出的共用的名稱，並不是伺服器的 FQDN 為基礎的 Kerberos 票證要求。</td>
</tr>
</tbody>
</table>


當您設定好 ASA 認證時，記住以下指導方針：

  - **帳戶類型。**我們建議您建立電腦帳戶，而不是使用者帳戶。電腦帳戶不允許互動式登入並可能會有較簡單的安全性原則與使用者帳戶。如果您建立電腦帳戶，不會過期的密碼，但建議您密碼定期更新繼續。您可以使用本機群組原則指定電腦帳戶和指令碼來定期刪除電腦帳戶不符合目前原則保留時間上限。您的本機安全性原則也會決定當您需要變更密碼。雖然建議您依照電腦帳戶，您可以建立的使用者帳戶。

  - **帳戶名稱。**沒有名稱之帳戶的需求。您可以使用符合任何名稱命名的配置。

  - **帳戶群組。**用於 ASA 認證的帳戶不需要特殊安全性權限。如果您使用的電腦帳戶然後的帳戶僅必須是網域的電腦安全性群組的成員。如果您使用的使用者帳戶然後帳戶只必須是網域使用者的 \[安全性\] 群組的成員。

  - **帳戶密碼。**會使用您提供當您建立之帳戶的密碼。因此當您建立的帳戶，您應該使用的複雜密碼，並確定密碼符合貴組織的密碼需求。

若要建立電腦帳戶作為 ASA 認證

1.  已加入網域的電腦上，執行 Windows PowerShell 或 Exchange 管理命令介面。
    
    若要匯入 Active Directory 模組中使用**Import-Module**指令程式。
    
        Import-Module ActiveDirectory

2.  使用**New-ADComputer**指令程式來建立新的 Active Directory 電腦帳戶使用此 cmdlet 的語法：
    
        New-ADComputer [-Name] <string> [-AccountPassword <SecureString>] [-AllowReversiblePasswordEncryption <System.Nullable[boolean]>] [-Description <string>] [-Enabled <System.Nullable[bool]>]
    
    **範例：**
    
        New-ADComputer -Name EXCH2013ASA -AccountPassword (Read-Host 'Enter password' -AsSecureString) -Description 'Alternate Service Account credentials for Exchange' -Enabled:$True -SamAccountName EXCH2013ASA
    
    其中*EXCH2013ASA*是帳戶的名稱、 描述*Alternate Service Account credentials for Exchange*是您想它是的而值*SamAccountName*參數，在這種情況下*EXCH2013ASA*，需要您的目錄中是唯一的。

3.  使用**Set-ADComputer**指令程式來啟用 AES 256 加密 cipher 支援使用 Kerberos 使用此 cmdlet 的語法：
    
        Set-ADComputer [-Name] <string> [-add @{<attributename>="<value>"]
    
    **範例：**
    
        Set-ADComputer EXCH2013ASA -add @{"msDS-SupportedEncryptionTypes"="28"}
    
    其中*EXCH2013ASA*是帳戶的名稱和要修改的屬性是*msDS-SupportedEncryptionTypes*十進位值為 28、 可讓下列 cipher: RC4 HMAC、 AES128-CTS-HMAC-SHA1-96、 AES256-CTS-HMAC-SHA1-96。

如需這些 cmdlet 的詳細資訊，請參閱[匯入模組](https://technet.microsoft.com/library/hh849725.aspx)和[新增 ADComputer](https://technet.microsoft.com/library/ee617245.aspx)。

## 跨樹系案例

如果您有跨樹系或資源樹系部署，且您具有包含ExchangeActive Directory樹系以外的使用者，您需要設定樹系間的樹系信任關係。此外，每個樹系部署中，您需要設定讓所有名稱尾碼樹系內及跨樹系間的信任關係的路由規則。如需管理跨樹系信任的詳細資訊，請參閱[Managing 樹系信任](https://technet.microsoft.com/library/cc772440.aspx)。

## 識別要關聯 ASA 認證的服務主要名稱

建立 ASA 認證之後，您需要Exchange服務主要名稱 (Spn) 關聯 ASA 認證。Exchange 的 Spn 清單可能會因您的設定而異，但應至少包含下列：

  - **http /**  使用此 SPN Outlook 無所不在、 MAPI over HTTP、 Exchange Web 服務、 自動探索、 及離線通訊錄。

SPN 的值必須符合在網路負載平衡器，而不是個別伺服器上的服務名稱。若要協助規劃您應該使用哪個 SPN 值，請考慮下列情況：

  - 單一 Active Directory 站台

  - 多個 Active Directory 站台

在每個這些案例中，會假設負載平衡、 完整網域名稱 (Fqdn) 已由用戶端存取伺服器成員所部署的內部 Url、 外部 Url 和自動探索使用內部的 URI。如需詳細資訊，請參閱了解代理和重新導向。

## 單一 Active Directory 站台

如果您有單一 Active Directory 站台中，您的環境可能類似下圖中：

![CAS 陣列，包含單一 AD 站台和 Kerberos 驗證](images/Ff808312.97a1a926-f4ac-4498-bc6b-32e7fb1b70f1(EXCHG.150).jpg "CAS 陣列，包含單一 AD 站台和 Kerberos 驗證")

根據內部圖中的 Outlook 用戶端所使用的 Fqdn，需要下列 Spn 關聯 ASA 認證：

  - http/mail.corp.tailspintoys.com

  - http/autodiscover.corp.tailspintoys.com

## 多個 Active Directory 站台

如果您有多個 Active Directory 站台，您的環境可能類似下圖中：

![CAS 陣列，包含多個 AD 站台和 Kerberos 驗證](images/Ff808312.95b52bd8-7074-4055-8bd2-e6bf1f112b42(EXCHG.150).jpg "CAS 陣列，包含多個 AD 站台和 Kerberos 驗證")

根據上圖中的 Outlook 用戶端所使用的 Fqdn，您將需要下列 Spn 關聯 ADSite 1 中的用戶端存取伺服器會使用 ASA 認證：

  - http/mail.corp.tailspintoys.com

  - http/autodiscover.corp.tailspintoys.com

您也將需要下列 Spn 關聯 ADSite 2 中的用戶端存取伺服器會使用 ASA 認證：

  - http/mailsdc.corp.tailspintoys.com

  - http/autodiscoversdc.corp.tailspintoys.com

## 設定，然後確認 ASA 認證在每部用戶端存取伺服器上的設定

您已建立帳戶之後，您需要驗證的帳戶已複寫到所有 AD DS 網域控制站。主要是針對的帳戶必須要有將會使用 ASA 認證每部用戶端存取伺服器上。接下來，您設定帳戶作為 ASA 認證在每部用戶端存取伺服器上部署中。

您使用 Exchange 管理命令介面中其中一個這些程序所述設定 ASA 認證：

  - 第一部 Exchange 2013 用戶端存取伺服器部署 ASA 認證

  - 後續的 Exchange 2013 Client Access server 部署 ASA 認證

部署 ASA 認證的唯一支援的方法是使用 RollAlternateServiceAcountPassword.ps1 指令碼。如需詳細資訊，請參閱[在命令介面中使用 RollAlternateserviceAccountCredential.ps1 指令碼](using-the-rollalternateserviceaccountcredential-ps1-script-in-the-shell-exchange-2013-help.md)。執行指令碼之後，建議您確認已正確更新所有目標的伺服器。

## 第一部 Exchange 2013 用戶端存取伺服器部署 ASA 認證

1.  開啟 Exchange 管理命令介面在 Exchange 2013 伺服器上。

2.  將目錄變更為*\<Exchange 2013 installation directory\>*\\V15\\Scripts。

3.  執行下列命令以第一部 Exchange 2013 用戶端存取伺服器部署 ASA 認證：
    
        .\RollAlternateServiceAccountPassword.ps1 -ToSpecificServer cas-1.corp.tailspintoys.com -GenerateNewPasswordFor tailspin\EXCH2013ASA$

4.  當您正在詢問想要變更的備用服務帳戶的密碼時，回答**\[是\]**。

以下是輸出的有顯示當您執行 RollAlternateServiceAccountPassword.ps1 指令碼範例。

    ========== Starting at 01/12/2015 10:17:47 ==========
    Creating a new session for implicit remoting of "Get-ExchangeServer" command...
    Destination servers that will be updated:
    
    Name                                                        PSComputerName
    ----                                                        --------------
    cas-1                                                   cas-1.corp.tailspintoys.com
    
    
    Credentials that will be pushed to every server in the specified scope (recent first):
    
    UserName                                                                                                        
    Password
    --------                                                                                                        
    --------
    tailspin\EXCH2013ASA$                                                                             
    System.Security.SecureString
    
    
    Prior to pushing new credentials, all existing credentials that are invalid or no longer work will be removed from  the destination servers.
    Pushing credentials to server cas-1
    Setting a new password on Alternate Serice Account in Active Directory
    
    Password change
    Do you want to change password for tailspin\EXCH2013ASA$ in Active Directory at this time?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
    Preparing to update Active Directory with a new password for tailspin\EXCH2013ASA$ ...
    Resetting a password in the Active Directory for tailspin\EXCH2013ASA$ ...
    New password was successfully set to Active Directory.
    Retrieving the current Alternate Service Account configuration from servers in scope
    Alternate Service Account properties:
    
    StructuralObjectClass QualifiedUserName Last Pwd Update       SPNs
    --------------------- ----------------- ---------------       ----
    computer              tailspin\EXCH2013ASA$   1/12/2015 10:19:53 AM
    
    Per-server Alternate Service Account configuration as of the time of script completion:
    
    
       Array: {mail.corp.tailspintoys.com}
    
    Identity  AlternateServiceAccountConfiguration
    --------  ------------------------------------
    cas-1 Latest: 1/12/2015 10:19:22 AM, tailspin\EXCH2013ASA$
              ...
    
    ========== Finished at 01/12/2015 10:20:00 ==========
    
            THE SCRIPT HAS SUCCEEDED

## 將 ASA 認證部署至另一部 Exchange 2013 用戶端存取伺服器

1.  開啟 Exchange 管理命令介面在 Exchange 2013 伺服器上。

2.  將目錄變更為*\<Exchange 2013 installation directory\>*\\V15\\Scripts。

3.  執行下列命令以部署至另一部 Exchange 2013 用戶端存取伺服器的 ASA 認證：
    
        .\RollAlternateServiceAccountPassword.ps1 -ToSpecificServer cas-2.corp.tailspintoys.com -CopyFrom cas-1.corp.tailspintoys.com

4.  針對您想要部署至 ASA 認證每部用戶端存取伺服器重複步驟 3。

以下是輸出的有顯示當您執行 RollAlternateServiceAccountPassword.ps1 指令碼範例。

    ========== Starting at 01/12/2015 10:34:35 ==========
    Destination servers that will be updated:
    
    Name                                                        PSComputerName
    ----                                                        --------------
    cas-2                                                   cas-2.corp.tailspintoys.com
    
    
    Credentials that will be pushed to every server in the specified scope (recent first):
    
    UserName                                                                                                        
    Password
    --------                                                                                                        
    --------
    tailspin\EXCH2013ASA$                                                                             
    System.Security.SecureString
    
    Prior to pushing new credentials, all existing credentials will be removed from the destination servers.
    Pushing credentials to server cas-2
    Retrieving the current Alternate Service Account configuration from servers in scope
    Alternate Service Account properties:
    
    StructuralObjectClass QualifiedUserName Last Pwd Update       SPNs
    --------------------- ----------------- ---------------       ----
    computer              tailspin\EXCH2013ASA$   1/12/2015 10:19:53 AM
    
    Per-server Alternate Service Account configuration as of the time of script completion:
    
    
       Array: cas-2.corp.tailspintoys.com
    
    Identity  AlternateServiceAccountConfiguration
    --------  ------------------------------------
    cas-2 Latest: 1/12/2015 10:37:59 AM, tailspin\EXCH2013ASA$
              ...
    
    
    ========== Finished at 01/12/2015 10:38:13 ==========
    
            THE SCRIPT HAS SUCCEEDED

## 確認 ASA 認證的部署

  - 開啟 Exchange 管理命令介面在 Exchange 2013 伺服器上。

  - 執行下列命令以檢查用戶端存取伺服器上的設定：
    
        Get-ClientAccessServer CAS-3 -IncludeAlternateServiceAccountCredentialStatus | Format-List Name, AlternateServiceAccountConfiguration

  - 您想要用來驗證 ASA 認證的部署每部用戶端存取伺服器上重複步驟 2。

以下是輸出的當您執行上述 Get-clientaccessserver 命令及任何先前 ASA 認證已設定具有所示範例。

    Name                                 : CAS-1
    AlternateServiceAccountConfiguration : Latest: 1/12/2015 10:19:22 AM, tailspin\EXCH2013ASA$
                                           Previous: <Not set>
                                               ...

以下是輸出的當您執行上述 Get-clientaccessserver 命令與先前已設定 ASA 認證已顯示範例。會傳回上一個 ASA 認證的日期和時間下限設為。

    Name                                 : CAS-3
    AlternateServiceAccountConfiguration : Latest: 1/12/2015 10:19:22 AM, tailspin\EXCH2013ASA$
                                           Previous: 7/15/2014 12:58:35 PM, tailspin\oldSharedServiceAccountName$
                                               ...

## 關聯 ASA 認證的服務主要名稱 (Spn)

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>未關聯的 Spn ASA 認證直到您已部署該認證至少一部 Exchange 伺服器，以部署至第一部 Exchange 2013 Client Access server ASA 認證稍早所述。否則，您會遇到 Kerberos 驗證錯誤。</td>
</tr>
</tbody>
</table>


Spn 關聯 ASA 認證之前，您必須確認目標 Spn 已經不在樹系中的不同帳戶相關聯。ASA 認證必須是唯一的帳戶與這些 Spn 相關聯的樹系中。您可以確認樹系中的沒有其他帳戶相關聯的 Spn 執行**setspn**命令，從命令列。

確認 SPN 尚未關聯的樹系中的帳戶執行 setspn 命令

1.  按**啟動**。在 \[**搜尋**\] 方塊清單中的結果，然後輸入**命令提示字元處**，選取 \[**命令提示字元**。

2.  在命令提示字元處輸入下列命令：
    
        setspn -F -Q <SPN>
    
    您想要關聯 ASA 認證 \< SPN \> 所在的 SPN。例如：
    
        setspn -F -Q http/mail.corp.tailspintoys.com
    
    此命令應傳回 nothing。如果它傳回的某個項目，另一個帳戶相關聯已經 SPN。一旦想要 ASA 認證與相關聯的每個 SPN 重複此步驟。

使用 setspn 命令建立關聯的 ASA 認證 SPN

1.  按**啟動**。在 \[**搜尋**\] 方塊清單中的結果，然後輸入**命令提示字元處**，選取 \[**命令提示字元**。

2.  在命令提示字元處輸入下列命令：
    
        setspn -S <SPN> <Account>$
    
    其中 \< SPN \> 是想要 ASA 認證與相關聯的 SPN，\< 帳戶 \> 是 ASA 認證與相關聯的帳戶。例如：
    
        setspn -S http/mail.corp.tailspintoys.com tailspin\EXCH2013ASA$
    
    想要 ASA 認證與相關聯的每個 SPN 之後執行此命令。

確認您與相關聯的 Spn ASA 認證使用 setspn 命令

1.  按**啟動**。在 \[**搜尋**\] 方塊清單中的結果，然後輸入**命令提示字元處**，選取 \[**命令提示字元**。

2.  在命令提示字元處輸入下列命令：
    
        setspn -L <Account>$
    
    其中 \< 帳戶 \> 是 ASA 認證與相關聯的帳戶。例如：
    
        setspn -L tailspin\EXCH2013ASA$
    
    您只需要執行此命令一次。

## 啟用 Outlook 用戶端的 Kerberos 驗證

1.  開啟 Exchange 管理命令介面在 Exchange 2013 伺服器上。

2.  若要啟用 Outlook 無所不在用戶端的 Kerberos 驗證，請在用戶端存取伺服器上執行下列命令：
    
        Get-OutlookAnywhere -server CAS-1 | Set-OutlookAnywhere -InternalClientAuthenticationMethod  Negotiate

3.  若要啟用 MAPI over HTTP 用戶端的 Kerberos 驗證，請在 Exchange 2013 Client Access server 上執行下列命令：
    
        Get-MapiVirtualDirectory -Server CAS-1 | Set-MapiVirtualDirectory -IISAuthenticationMethods Ntlm, Negotiate

4.  針對您要啟用 Kerberos 驗證每個 Exchange 2013 Client Access server 重複步驟 2 和 3。

## 驗證 Exchange 用戶端 Kerberos 驗證

您已成功設定 Kerberos 和 ASA 認證之後，請確認用戶端可以驗證成功這些工作中所述。

## 確認正在執行 Microsoft Exchange 服務主機服務

Microsoft Exchange 服務主機上的服務 (MSExchangeServiceHost) 用戶端存取伺服器負責管理 ASA 認證。如果這項服務未執行，不是可能的 Kerberos 驗證。根據預設，此服務已啟動電腦時自動啟動。

若要確認 Microsoft Exchange 服務主機服務已啟動

1.  按一下 \[**開始\]**、 輸入**services.msc**，並從清單中選取**services.msc** 。

2.  在 \[**服務**\] 視窗中，尋找 \[ **Microsoft Exchange 服務主機**服務的服務清單中。

3.  應**執行**的服務的狀態。如果狀態不**執行**，以滑鼠右鍵按一下服務\] 和 \[**啟動**。

## Kerberos 驗證從用戶端存取伺服器

當您在每個用戶端存取伺服器上設定 ASA 認證時，在執行**set-ClientAccessServer** cmdlet。一旦您已執行此指令程式，您可以使用記錄檔來確認成功的 Kerberos 連線。

若要驗證的 Kerberos 運作正常使用 HttpProxy 記錄檔

1.  在文字編輯器中，瀏覽至儲存 HttpProxy 記錄檔的資料夾。根據預設，記錄檔會儲存於下列資料夾：
    
    %ExchangeInstallPath%\\Logging\\HttpProxy\\RpcHttp

2.  開啟的最新的記錄檔並尋找 word**交涉**。在記錄檔中的行會看起來類似下列範例：
    
        2014-02-19T13:30:49.219Z,e19d08f4-e04c-42da-a6be-b7484b396db0,15,0,775,22,,RpcHttp,mail.corp.tailspintoys.com,/rpc/rpcproxy.dll,,Negotiate,True,tailspin\Wendy,tailspintoys.com,MailboxGuid~ad44b1e0-e44f-4a16-9396-3a437f594f88,MSRPC,192.168.1.77,EXCH1,200,200,,RPC_OUT_DATA,Proxy,exch2.tailspintoys.com,15.00.0775.000,IntraForest,MailboxGuidWithDomain,,,,76,462,1,,1,1,,0,,0,,0,0,16272.3359,0,0,3,0,23,0,25,0,16280,1,16274,16230,16233,16234,16282,?ad44b1e0-e44f-4a16-9396-3a437f594f88@tailspintoys.com:6001,,BeginRequest=2014-02-19T13:30:32.946Z;BeginGetRequestStream=2014-02-19T13:30:32.946Z;OnRequestStreamReady=2014-02-19T13:30:32.946Z;BeginGetResponse=2014-02-19T13:30:32.946Z;OnResponseReady=2014-02-19T13:30:32.977Z;EndGetResponse=2014-02-19T13:30:32.977Z;,PossibleException=IOException;
    
    如果您看到**識別碼**值會**交涉**，則伺服器已成功建立 Kerberos 的驗證連線。

## 維護 ASA 認證

如果您需要定期重新整理 ASA 認證密碼，請設定 ASA 認證本文中的使用步驟。請考慮設定來執行一般密碼維護排定的工作。請務必監視以確保及時密碼變換並防止可能驗證中斷排定的工作。

## 關閉 Kerberos 驗證

若要設定您的用戶端存取伺服器，讓它不會使用 Kerberos，解除關聯或移除的 Spn ASA 認證。若要移除的 Spn，Kerberos 驗證將不會嘗試在用戶端，並設定為使用交涉驗證用戶端將會改用 NTLM。若要使用只 Kerberos 設定的用戶端無法連線。一旦移除 Spn 您也應該刪除帳戶。

若要移除 ASA 認證

1.  開啟 Exchange 管理命令介面在 Exchange 2013 伺服器並執行下列命令：
    
        Set-ClientAccessServer CAS-1 -RemoveAlternateServiceAccountCredentials

2.  雖然您沒有立即執行這項作業，請最後應重新啟動以清除 \[從電腦的 Kerberos 票證快取的所有用戶端電腦。

