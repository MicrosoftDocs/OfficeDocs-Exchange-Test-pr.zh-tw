---
title: 'Exchange 2013 用戶端存取伺服器組態: Exchange 2013 Help'
TOCTitle: Exchange 2013 用戶端存取伺服器組態
ms:assetid: 01432ae4-2a00-44a4-a4dd-4eb8d7e6cfae
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh529912(v=EXCHG.150)
ms:contentKeyID: 50472455
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013 用戶端存取伺服器組態

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2017-07-25_

在您安裝 Exchange 2013 用戶端存取伺服器後，有幾個可執行的設定工作。雖然在 Exchange 2013 中的用戶端存取伺服器無法處理用戶端通訊協定，仍有數個設定需套用至用戶端存取伺服器，其中包含虛擬目錄設定與憑證設定。

## 設定伺服器憑證

在 Exchange 2013 中，您可以使用憑證精靈請求憑證授權單位頒發數位憑證。在您請求取得數位憑證後，需將憑證安裝於用戶端存取伺服器中。

不需將數位憑證安裝組織內的信箱伺服器上。自我簽署憑證將依預設安裝於信箱伺服器上，不需要被取代。組織中的用戶端存取伺服器完全信任信箱伺服器上的自我簽署憑證。如需詳細資訊，請參閱 [Exchange 2013 憑證管理 UI](exchange-2013-certificate-management-ui-exchange-2013-help.md)。

## 設定虛擬目錄

有數個您可為離線通訊錄 (OAB)、Exchange Web 服務、Exchange ActiveSync、Outlook Web App 以及 Exchange Administration Center 於虛擬目錄上設定的設定。若需關於虛擬目錄管理的額外資訊，請參閱 [虛擬目錄管理](virtual-directory-management-exchange-2013-help.md)。可使用下列命令來設定虛擬目錄。

  - Exchange 2013 提供兩組 Outlook Anywhere 組態的 HTTP 連線設定，因此系統管理員可以同時設定內部和外部端點。
    
    若要以單一連線 URL 設定 Outlook Anywhere，您必須提供主機名稱、指出是否需要 SSL，並在 Exchange 管理命令介面中使用下列命令來指定 AutoPackage：
    
        Get-OutlookAnywhere | Set-OutlookAnywhere -InternalHostname "internalServer.contoso.com" -InternalClientAuthenticationMethod Ntlm -InternalClientsRequireSsl $true -IISAuthenticationMethods Negotiate,NTLM,Basic
    
    您也可以在 Exchange 管理命令介面中使用下列命令，來指定可與外部連線的端點：
    
        Get-OutlookAnywhere | Set-OutlookAnywhere -InternalHostname "internalServer.contoso.com" -InternalClientAuthenticationMethod Ntlm -InternalClientsRequireSsl $true -ExternalHostname "externalServer.company.com" -ExternalClientAuthenticationMethod Basic -ExternalClientsRequireSsl $true -IISAuthenticationMethods Negotiate,NTLM,Basic
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>雖然 Exchange 2013 支援 Outlook Anywhere HTTP 交涉驗證，但此方法僅應用在環境中的所有伺服器都執行 Exchange 2013 時。</td>
    </tr>
    </tbody>
    </table>


  - 若要設定 Exchange ActiveSync，請執行下列命令：
    
        Set-ActiveSyncVirtualDirectory -Identity "<CAS2013>\Microsoft-Server-ActiveSync (Default Web Site)" -ExternalUrl "https://mail.contoso.com/Microsoft-Server-ActiveSync"

  - 若要設定 Exchange Web 服務虛擬目錄，請執行下列命令。
    
        Set-WebServicesVirtualDirectory -Identity "<CAS2013>\EWS (Default Web Site)" -ExternalUrl https://mail.contoso.com/EWS/Exchange.asmx

  - 使用下列命令來設定離線通訊錄：
    
        Set-OABVirtualDirectory -Identity "<CAS2013>\OAB (Default Web Site)" -ExternalUrl "https://mail.contoso.com/OAB"

  - 若要設定服務連線點，請執行下列命令。
    
        Set-ClientAccessServer -Identity <CAS2013> -AutoDiscoverServiceInternalURI https://autodiscover.contoso.com/AutoDiscover/AutoDiscover.xml

## 從 Exchange 2007 及 2010 用戶端存取升級

使用此區段，來協助您對 Exchange 2013 Client Access Server 上的通訊協定設定外部存取。在上面的設定虛擬目錄區段中執行 Exchange 管理命令介面命令，以及執行下面的命令。

您將必須執行下列命令，才能設定 Exchange 2013 的虛擬目錄。

1.  若要設定 Outlook Web App 的外部 URL，請在 Exchange 管理命令介面中執行下列命令。
    
        Set-OwaVirtualDirectory "<CAS2013>\OWA (Default Web Site)" -ExternalUrl https://mail.contoso.com/OWA
    
    設定好 Outlook Web App 虛擬目錄後，在命令提示字元中執行下列命令。
    
        Net stop IISAdmin /y
    
        Net start W3SVC

2.  若要設定外部 EAC 存取，請在 Exchange 管理命令介面中執行下列命令。
    
        Set-EcpVirtualDirectory "<CAS2013>\ECP (Default Web Site)" -ExternalUrl https://mail.contoso.com/ECP -InternalURL https://mail.contoso.com/ECP 

3.  若要設定可用性服務，請在 Exchange 管理命令介面中執行下列命令。
    
        Set-WebServicesVirtualDirectory -Identity "<CAS2013>\EWS (Default Web Site)" -ExternalURL https://mail.contoso.com/EWS/Exchange.asmx

若要確認的外部 URL 已正確設定Exchange ActiveSync或Outlook Web App，您可以使用 Remote Connectivity Analyzer Microsoft 提供的免費 Web 式工具。您可以找到 Remote Connectivity Analyzer[以下](http://go.microsoft.com/fwlink/?linkid=154308)。

若要確認已為 Exchange ActiveSync 或 Outlook Web App 正確設定驗證，也可以使用 ExRCA。

若要確認已為 Outlook Web App 正確設定直接檔案存取，請使用公用電腦選項並以使用者身分登入 Outlook Web App，再嘗試存取及儲存附加至電子郵件的檔案。

## 設定 Exchange 2007 Client Access Server 上的通訊協定

您將必須執行下列命令，才能設定 Exchange 2007 的虛擬目錄。

  - 若要在 Exchange ActiveSync 虛擬目錄上設定外部 URL，請在 Exchange 管理命令介面中執行下列命令。
    
        Set-ActiveSyncVirtualDirectory -Identity "<CAS2007>\Microsoft-Server-ActiveSync (Default Web Site)" -ExternalUrl https://mail.contoso.com/Microsoft-Server-ActiveSync

  - 若要在 Outlook Web App 虛擬目錄上設定外部 URL，請在 Exchange 管理命令介面中執行下列命令。
    
        Set-OwaVirtualDirectory -Identity "<CAS2007>\owa (Default Web Site)" -ExternalUrl https://legacy.contoso.com/owa

