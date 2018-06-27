---
title: '設定 SSL 卸載在 Exchange 2013: Exchange 2013 Help'
TOCTitle: 設定 SSL 卸載在 Exchange 2013
ms:assetid: 654cc2c2-918b-48fc-9532-9c8e3012810d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn635115(v=EXCHG.150)
ms:contentKeyID: 61204229
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定 SSL 卸載在 Exchange 2013

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-08-22_

以下內容協助您在已安裝 Service Pack (SP1) 的 Exchange 2013 Client Access Server 上設定通訊協定和相關服務的 SSL 卸載。如果您有多部 Client Access Server，則必須在內部部署組織中已安裝 SP1 的每一部 Client Access Server 上，為每一個通訊協定或服務執行必要的步驟。當然，組織中的每一部 Client Access Server 必須有相同的設定。如果您要升級到較新的累計更新 (CU) 或 Service Pack，但想要繼續使用 SSL 卸載，則在升級或套用這些更新之後，您必須在 Exchange 2013 Client Access Server 上再次執行下列步驟。

SSL 卸載最大的優點之一是可讓您更輕鬆管理已使用的憑證。不必為每一部已安裝 SP1 的 Client Access Server 準備個別的 SSL 憑證，只要使用一個 SSL 憑證並匯入到所有 Client Access Server 即可。可使用現有的或最新建立的 SSL 憑證。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您使用網際網路資訊服務 (IIS) 管理員、 Exchange 管理命令介面或命令列介面來設定 SSL 卸載時，請注意也會在<strong>預設的網站</strong>和<strong>Exchange Back End</strong>站台。Ssl 卸載，僅限設定<strong>預設的網站</strong>和<strong>Exchange Back End</strong>網站不進行任何變更。</td>
</tr>
</tbody>
</table>


**目錄**

Configuring SSL offloading for Outlook Web App

Configuring SSL offloading for the Exchange Admin Center (EAC)

Configuring SSL offloading for Outlook Anywhere

Configuring SSL offloading for the Offline Address Book (OAB)

Configuring SSL offloading for Exchange ActiveSync (EAS)

Configuring SSL offloading for Exchange Web Services (EWS)

Configuring SSL offloading for the Autodiscover service

Configuring SSL offloading for the Mailbox Replication Proxy Service (MRSProxy)

設定 Outlook 用戶端的 SSL 卸載 (MAPI 虛擬目錄)

Using a Shell script to enable SSL offloading for all protocols and services

Configuring coexistence with Exchange 2007 and Exchange 2010

## 開始之前有哪些須知？

  - 在組織中安裝所有必要的 Client Access Server 和 Mailbox Server。

  - 在組織中的每一部 Client Access Server 和 Mailbox Server 上安裝 Service Pack 1 (SP1)。若要下載 SP1，請參閱 [更新 Exchange 2013](updates-for-exchange-2013-exchange-2013-help.md)。

  - 請參閱[功能權限](feature-permissions-exchange-2013-help.md)，以決定 Exchange 2013 的必要權限。

  - 若要知道您需要的 Client Access Server 權限，請參閱[用戶端和行動裝置權限](clients-and-mobile-devices-permissions-exchange-2013-help.md)中的「Client Access Server 權限」。

  - 若要知道您需要的 Client Access Server 權限，請參閱[用戶端和行動裝置權限](clients-and-mobile-devices-permissions-exchange-2013-help.md)中的「Outlook Web App 權限」。

  - 您可能只能使用命令介面來執行某些程序。若要了解如何在內部部署 Exchange 組織中開啟命令介面，請參閱[開啟命令介面。](https://technet.microsoft.com/zh-tw/library/dd638134\(v=exchg.150\))。

  - 若要在您終止 SSL 連線的 Client Access Server 和裝置上使用現有的憑證，請在 Client Access Server 上將憑證和私密金鑰一起匯出，再匯入或安裝到裝置上。如需詳細資訊，請參閱[Export-ExchangeCertificate](https://technet.microsoft.com/zh-tw/library/aa996305\(v=exchg.150\))。

  - 若要使用新的憑證，您必須使用 EAC 或命令介面來建立、匯入和啟用新的憑證。如需詳細資訊，請參閱[Exchange 2013 憑證管理 UI](exchange-2013-certificate-management-ui-exchange-2013-help.md)。

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


## 設定 Outlook Web App 的 SSL 卸載

若要對 Outlook Web App 啟用 SSL 卸載，您需要在 **\[Default Web Site\]** 的 **owa** 虛擬目錄上移除 SSL 需求。

  - **步驟 1**   您可以使用 Internet Information Services (IIS) 管理員或命令列，在 **owa** 虛擬目錄上停用 SSL：
    
      - 使用 Internet Information Services (IIS) 管理員，展開 **\[站台\]** \> **\[Default Web Site\]**，然後選取 **owa** 虛擬目錄。在結果窗格中的 **\[IIS\]** 下方，按兩下 **\[SSL 設定\]**。在 **\[SSL 設定\]** 結果窗格中，清除 **\[需要 SSL\]** 核取方塊，然後在 **\[動作\]** 窗格中按一下 **\[套用\]**。
    
      - 使用命令提示字元，輸入下列命令，然後按 Enter 鍵。
        
            appcmd set config "Default Web Site/owa" /section:access /sslFlags:None /commit:APPHOST

  - **步驟 2**   您需要使用下列其中一個命令，收回正確的應用程式集區或重新啟動 Internet Information Services：
    
      - 使用命令列：移至 **\[開始\]** \> **\[執行\]**，輸入 **cmd**，然後按 Enter 鍵。在命令提示字元視窗中，輸入下列命令，然後按 Enter 鍵。
        
            appcmd Recycle AppPool MSExchangeOWAAppPool
    
      - 使用 Windows PowerShell 指令程式，輸入下列命令，然後按 Enter 鍵。
        
            IIS:\>Restart-WebAppPool MSExchangeOWAAppPool
    
      - 使用命令列：移至 **\[開始\]** \> **\[執行\]**，輸入 **cmd**，然後按 Enter 鍵。在命令提示字元視窗中，輸入下列命令，然後按 Enter 鍵。
        
            iisreset /noforce
    
      - 使用 Internet Information Services (IIS) 管理員：在 Internet Information Services (IIS) 管理員的 **\[動作\]** 窗格中，按一下 **\[重新啟動\]**。

回到頁首

## 設定 Exchange 系統管理中心 (EAC) 的 SSL 卸載

若要對 EAC 啟用 SSL 卸載，您需要在 **\[Default Web Site\]** 的 **ecp** 虛擬目錄上移除 SSL 需求。

  - **步驟 1**   您可以使用 Internet Information Services (IIS) 管理員或命令列，在 **ecp** 虛擬目錄上停用 SSL：
    
      - 使用 Internet Information Services (IIS) 管理員，展開 **\[站台\]** \> **\[Default Web Site\]**，然後選取 **ecp** 虛擬目錄。在結果窗格中的 **\[IIS\]** 下方，按兩下 **\[SSL 設定\]**。在 **\[SSL 設定\]** 結果窗格中，清除 **\[需要 SSL\]** 核取方塊，然後在 **\[動作\]** 窗格中按一下 **\[套用\]**。
    
      - 使用命令提示字元，輸入下列命令，然後按 Enter 鍵。
        
            appcmd set config "Default Web Site/ecp" /section:access /sslFlags:None /commit:APPHOST
        
        ``` 
        ```

  - **步驟 2**   您需要使用下列其中一個命令，收回正確的應用程式集區或重新啟動 Internet Information Services：
    
      - 使用命令列：移至 **\[開始\]** \> **\[執行\]**，輸入 **cmd**，然後按 Enter 鍵。在命令提示字元視窗中，輸入下列命令，然後按 Enter 鍵。
        
            appcmd Recycle AppPool MSExchangeECPAppPool
    
      - 使用 Windows PowerShell 指令程式，輸入下列命令，然後按 Enter 鍵。
        
            IIS:\>Restart-WebAppPool MSExchangeECPAppPool
    
      - 使用命令列：移至 **\[開始\]** \> **\[執行\]**，輸入 **cmd**，然後按 Enter 鍵。在命令提示字元視窗中，輸入下列命令，然後按 Enter 鍵。
        
            iisreset /noforce
    
      - 使用 Internet Information Services (IIS) 管理員：在 Internet Information Services (IIS) 管理員的 **\[動作\]** 窗格中，按一下 **\[重新啟動\]**。

回到頁首

## 設定 Outlook Anywhere 的 SSL 卸載

預設會啟用 SSL 卸載 Outlook 無所不在 」。Outlook 無所不在用戶端可以從取得電子郵件的私人或公開網路。根據預設，內部主機名稱或伺服器的 FQDN 用來啟用內部的 Outlook 用戶端連線。不過，如果 Outlook 無所不在 」 不會在內部使用，您應該移除的內部主機名稱。若要允許內部和外部存取的 Outlook 用戶端，您必須設定內部與外部主機名稱、 每個設定的驗證方法及設定兩個內部和外部用戶端以要求使用 SSL。若要設定外部用戶端的驗證方法，您可以使用 EAC 或 Exchange 管理命令介面中，但針對內部用戶端，您必須使用命令介面：

  - **步驟 1**  您可以使用 EAC 或命令介面如果尚未新增 Outlook anywhere 的外部主機名稱：
    
      - 使用 EAC，移至 **\[伺服器\]**，在清單中選取 Client Access Server 的名稱，然後按一下 **\[編輯\]**。在 **\[Exchange Server\]** 視窗中，按一下 **\[Outlook Anywhere\]**，然後在 **\[指定外部主機名稱 (例如，contoso.com)，供使用者用來連線到您的組織\]** 方塊中，輸入外部主機名稱。確認已選取 **\[允許 SSL 卸載\]** 選項，然後按一下 **\[儲存\]**。
    
      - 使用 Exchange 管理命令介面，按一下 **\[開始\]**，在 **\[開始\]** 功能表上按 **\[Exchange 管理命令介面\]**。在視窗中，輸入下列命令，然後按 Enter 鍵：
        
            Set-OutlookAnywhere -Identity ClientAccessServer1\Rpc* -Externalhostname ClientAccessServer1.contoso.com -ExternalClientsRequireSsl:$True -ExternalClientAuthenticationMethod Basic

  - **步驟 2**   預設會啟用 SSL 卸載。不過，如果 SSL 卸載已停用，您可以使用 EAC 或 Exchange 管理命令介面來啟用它：
    
      - 使用 EAC，移至 **\[伺服器\]**，在清單中選取 Client Access Server 的名稱，然後按一下 **\[編輯\]**。在 **\[Exchange Sever\]** 視窗中，依序按一下 **\[Outlook Anywhere\]**、**\[允許 SSL 卸載\]** 選項及 **\[儲存\]**。
    
      - 使用命令介面，輸入下列命令，然後按 Enter 鍵。
        
            Set-OutlookAnywhere -Identity ClientAccessServer1\Rpc* -SSLOffloading $true

  - **步驟 3**   **Rpc** 虛擬目錄上預設不會選取 **\[需要 SSL\]**，但如果想要確認 SSL 已停用，您可以使用 Internet Information Services (IIS) 管理員。
    
      - 使用 Internet Information Services (IIS) 管理員，展開 **\[站台\]** \> **\[Default Web Site\]**，然後選取 **Rpc** 虛擬目錄。在結果窗格中的 **\[IIS\]** 下方，按兩下 **\[SSL 設定\]**。在 **\[SSL 設定\]** 結果窗格中，確認已清除 **\[需要 SSL\]** 核取方塊，然後在 **\[動作\]** 窗格中按一下 **\[套用\]**。

  - **步驟 4**   您需要使用下列其中一個命令，收回正確的應用程式集區或重新啟動 Internet Information Services：
    
      - 使用命令列：移至 **\[開始\]** \> **\[執行\]**，輸入 **cmd**，然後按 Enter 鍵。在命令提示字元視窗中，輸入下列命令，然後按 Enter 鍵。
        
            appcmd Recycle AppPool MSExchangeRpcProxyFrontEndAppPool
    
      - 使用 Windows PowerShell 指令程式，輸入下列命令，然後按 Enter 鍵。
        
            IIS:\>Restart-WebAppPool MSExchangeRpcProxyFrontEndAppPool
    
      - 使用命令列：移至 **\[開始\]** \> **\[執行\]**，輸入 **cmd**，然後按 Enter 鍵。在命令提示字元視窗中，輸入下列命令，然後按 Enter 鍵。
        
            iisreset /noforce
    
      - 使用 Internet Information Services (IIS) 管理員：在 Internet Information Services (IIS) 管理員的 **\[動作\]** 窗格中，按一下 **\[重新啟動\]**。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>即使是在 Client Access Server 上重新啟動 IIS，您也必須等待服務主機處理程序每 15 分鐘將 Active Directory 的任何變更套用至 Internet Information Services (IIS)。</td>
</tr>
</tbody>
</table>


回到頁首

## 設定離線通訊錄 (OAB) 的 SSL 卸載

若要對離線通訊錄 (OAB) 啟用 SSL 卸載，您需要在 **\[Default Web Site\]** 的 **OAB** 虛擬目錄上移除 SSL 需求。

  - **步驟 1**   您可以使用 Internet Information Services (IIS) 管理員或命令列，在 **OAB** 虛擬目錄上停用 SSL：
    
      - 使用 Internet Information Services (IIS) 管理員，展開 **\[站台\]** \> **\[Default Web Site\]**，然後選取 **OAB** 虛擬目錄。在結果窗格中的 **\[IIS\]** 下方，按兩下 **\[SSL 設定\]**。在 **\[SSL 設定\]** 結果窗格中，清除 **\[需要 SSL\]** 核取方塊，然後在 **\[動作\]** 窗格中按一下 **\[套用\]**。
    
      - 使用命令提示字元，輸入下列命令，然後按 Enter 鍵。
        
            appcmd set config "Default Web Site/OAB" /section:access /sslFlags:None /commit:APPHOST

  - **步驟 2**   您需要使用下列其中一個命令，收回正確的應用程式集區或重新啟動 Internet Information Services：
    
      - 使用命令列：移至 **\[開始\]** \> **\[執行\]**，輸入 **cmd**，然後按 Enter 鍵。在命令提示字元視窗中，輸入下列命令，然後按 Enter 鍵。
        
            appcmd Recycle AppPool MSExchangeOABAppPool
    
      - 使用 Windows PowerShell 指令程式，輸入下列命令，然後按 Enter 鍵。
        
            IIS:\>Restart-WebAppPool MSExchangeOABAppPool
    
      - 使用命令列：移至 **\[開始\]** \> **\[執行\]**，輸入 **cmd**，然後按 Enter 鍵。在命令提示字元視窗中，輸入下列命令，然後按 Enter 鍵。
        
            iisreset /noforce
    
      - 使用 Internet Information Services (IIS) 管理員：在 Internet Information Services (IIS) 管理員的 **\[動作\]** 窗格中，按一下 **\[重新啟動\]**。

回到頁首

## 設定 Exchange ActiveSync (EAS) 的 SSL 卸載

若要對 Exchange ActiveSync (EAS) 啟用 SSL 卸載，您需要在 **\[Default Web Site\]** 的 **Microsoft-Server-ActiveSync** 虛擬目錄上移除 SSL 需求。

  - **步驟 1**   您可以使用 Internet Information Services (IIS) 管理員或命令列，在 **Microsoft-Server-ActiveSync** 虛擬目錄上停用 SSL：
    
      - 使用 Internet Information Services (IIS) 管理員，展開 **\[站台\]** \> **\[Default Web Site\]**，然後選取 **Microsoft-Server-ActiveSync** 虛擬目錄。在結果窗格中的 **\[IIS\]** 下方，按兩下 **\[SSL 設定\]**。在 **\[SSL 設定\]** 結果窗格中，清除 **\[需要 SSL\]** 核取方塊，然後在 **\[動作\]** 窗格中按一下 **\[套用\]**。
    
      - 使用命令提示字元，輸入下列命令，然後按 Enter 鍵。
        
            appcmd set config "Default Web Site/MSExchangeSyncAppPool" /section:access /sslFlags:None /commit:APPHOST

  - **步驟 2**   您需要使用下列其中一個命令，收回正確的應用程式集區或重新啟動 Internet Information Services：
    
      - 使用命令列：移至 **\[開始\]** \> **\[執行\]**，輸入 **cmd**，然後按 Enter 鍵。在命令提示字元視窗中，輸入下列命令，然後按 Enter 鍵。
        
            appcmd Recycle AppPool MSExchangeSyncAppPool
    
      - 使用 Windows PowerShell 指令程式，輸入下列命令，然後按 Enter 鍵。
        
            IIS:\>Restart-WebAppPool MSExchangeSyncAppPool
    
      - 使用命令列：移至 **\[開始\]** \> **\[執行\]**，輸入 **cmd**，然後按 Enter 鍵。在命令提示字元視窗中，輸入下列命令，然後按 Enter 鍵。
        
            iisreset /noforce
    
      - 使用 Internet Information Services (IIS) 管理員：在 Internet Information Services (IIS) 管理員的 **\[動作\]** 窗格中，按一下 **\[重新啟動\]**。

回到頁首

## 設定 Exchange Web 服務 (EWS) 的 SSL 卸載

若要對 Exchange Web Services (EWS) 啟用 SSL 卸載，您需要在 **\[Default Web Site\]** 的 **EWS** 虛擬目錄上移除 SSL 需求。

  - **步驟 1**   您可以使用 Internet Information Services (IIS) 管理員或命令列，在 **EWS** 虛擬目錄上停用 SSL：
    
      - 使用 Internet Information Services (IIS) 管理員，展開 **\[站台\]** \> **\[Default Web Site\]**，然後選取 **EWS** 虛擬目錄。在結果窗格中的 **\[IIS\]** 下方，按兩下 **\[SSL 設定\]**。在 **\[SSL 設定\]** 結果窗格中，清除 **\[需要 SSL\]** 核取方塊，然後在 **\[動作\]** 窗格中按一下 **\[套用\]**。
    
      - 使用命令提示字元，輸入下列命令，然後按 Enter 鍵。
        
            appcmd set config "Default Web Site/EWS" /section:access /sslFlags:None /commit:APPHOST

  - **步驟 2**   您需要使用下列其中一個命令，收回正確的應用程式集區或重新啟動 Internet Information Services：
    
      - 使用命令列：移至 **\[開始\]** \> **\[執行\]**，輸入 **cmd**，然後按 Enter 鍵。在命令提示字元視窗中，輸入下列命令，然後按 Enter 鍵。
        
            appcmd Recycle AppPool MSExchangeServicesAppPool
    
      - 使用 Windows PowerShell 指令程式，輸入下列命令，然後按 Enter 鍵。
        
            IIS:\>Restart-WebAppPool MSExchangeServicesAppPool
    
      - 使用命令列：移至 **\[開始\]** \> **\[執行\]**，輸入 **cmd**，然後按 Enter 鍵。在命令提示字元視窗中，輸入下列命令，然後按 Enter 鍵。
        
            iisreset /noforce
    
      - 使用 Internet Information Services (IIS) 管理員：在 Internet Information Services (IIS) 管理員的 **\[動作\]** 窗格中，按一下 **\[重新啟動\]**。

回到頁首

## 設定自動探索服務的 SSL 卸載

若要對自動探索服務啟用 SSL 卸載，您需要在 **\[Default Web Site\]** 的 **Autodiscover** 虛擬目錄上移除 SSL 需求。

  - **步驟 1**   您可以使用 Internet Information Services (IIS) 管理員或命令列，在 **Autodiscover** 虛擬目錄上停用 SSL：
    
      - 使用 Internet Information Services (IIS) 管理員，展開 **\[站台\]** \> **\[Default Web Site\]**，然後選取 **Autodiscover** 虛擬目錄。在結果窗格中的 **\[IIS\]** 下方，按兩下 **\[SSL 設定\]**。在 **\[SSL 設定\]** 結果窗格中，清除 **\[需要 SSL\]** 核取方塊，然後在 **\[動作\]** 窗格中按一下 **\[套用\]**。
    
      - 使用命令提示字元，輸入下列命令，然後按 Enter 鍵。
        
            appcmd set config "Default Web Site/autodiscover" /section:access /sslFlags:None /commit:APPHOST

  - **步驟 2**   您需要使用下列其中一個命令，收回正確的應用程式集區或重新啟動 Internet Information Services：
    
      - 使用命令列：移至 **\[開始\]** \> **\[執行\]**，輸入 **cmd**，然後按 Enter 鍵。在命令提示字元視窗中，輸入下列命令，然後按 Enter 鍵。
        
            appcmd Recycle AppPool MSExchangeAutodiscoverAppPool
    
      - 使用 Windows PowerShell 指令程式，輸入下列命令，然後按 Enter 鍵。
        
            IIS:\>Restart-WebAppPool MSExchangeAutodiscoverAppPool
    
      - 使用命令列：移至 **\[開始\]** \> **\[執行\]**，輸入 **cmd**，然後按 Enter 鍵。在命令提示字元視窗中，輸入下列命令，然後按 Enter 鍵。
        
            iisreset /noforce
    
      - 使用 Internet Information Services (IIS) 管理員：在 Internet Information Services (IIS) 管理員的 **\[動作\]** 窗格中，按一下 **\[重新啟動\]**。

回到頁首

## 設定信箱複寫 Proxy 服務 (MRSProxy) 的 SSL 卸載

每台 Exchange 2013 用戶端存取伺服器上安裝的 「 信箱複寫 Proxy (MRSProxy) 服務。MRSProxy 可幫助您進行跨樹系移動要求的內部以及移動內部部署信箱移轉至 Office 365。不過，根據預設，MRSProxy 已停用。如果您要啟用它，您應將信箱移至 Office 365 的內部部署 Exchange 樹系或跨樹系、 內部部署信箱移動的遠端 Exchange 樹系中加以啟用。雖然 MRSProxy 服務是執行 Exchange Web 服務 (EWS) 下，則不支援設定 SSL 卸載。

這是因為 MRSProxy 服務會要求流量必須經過簽署/加密。任何硬體負載平衡器或防火牆必須先重新加密 MRSProxy 流量，然後才傳送至 Client Access 伺服器。如果是這種情形，建議您設定 SSL 橋接來啟用卸載。

**反向 SSL 或 SSL 橋接**  如果您啟用反向 SSL 或 SSL 橋接硬體負載平衡器上，您不需要在每個 CAS 伺服器上執行上述步驟。不過，讓您的硬體負載平衡器上的反向 SSL 表示 SSL 加密與解密會保持與用戶端存取伺服器。在此例中 SSL 加密與解密就會發生硬體負載平衡器和用戶端存取伺服器上。選擇要使用 Exchange 2013 SSL 卸載或反向 SSL （SSL 橋接） 是取決於組織目標和必須實作的安全性作法。下圖顯示用戶端連線以 SSL 橋接 (反向 SSL) 啟用。

![SSL 橋接](images/Dn635115.a08aacc1-0ab4-46b3-bdae-b9518a3f5748(EXCHG.150).jpg "SSL 橋接")

## 設定 Outlook 用戶端的 SSL 卸載 (MAPI 虛擬目錄)

若要對 Outlook 用戶端啟用 SSL 卸載，您需要在 **\[Default Web Site\]** 的 **MAPI** 虛擬目錄上移除 SSL 需求。

  - **步驟 1**   您可以使用 Internet Information Services (IIS) 管理員或命令列，在 **MAPI** 虛擬目錄上停用 SSL：
    
      - 使用 Internet Information Services (IIS) 管理員，展開 **\[站台\]** \> **\[Default Web Site\]**，然後選取 **MAPI** 虛擬目錄。在結果窗格中的 **\[IIS\]** 下方，按兩下 **\[SSL 設定\]**。在 **\[SSL 設定\]** 結果窗格中，清除 **\[需要 SSL\]** 核取方塊，然後在 **\[動作\]** 窗格中按一下 **\[套用\]**。
    
      - 使用命令提示字元，輸入下列命令，然後按 Enter 鍵。
        
            appcmd set config "Default Web Site/MAPI" /section:access /sslFlags:None /commit:APPHOST

  - **步驟 2**   您需要使用下列其中一個命令，收回正確的應用程式集區或重新啟動 Internet Information Services：
    
      - 使用命令列：移至 **\[開始\]** \> **\[執行\]**，輸入 **cmd**，然後按 Enter 鍵。在命令提示字元視窗中，輸入下列命令，然後按 Enter 鍵。
        
            appcmd Recycle AppPool MSExchangeMapiFrontEndAppPool
    
      - 使用 Windows PowerShell 指令程式，輸入下列命令，然後按 Enter 鍵。
        
            IIS:\>Restart-WebAppPool MSExchangeMapiFrontEndAppPool
    
      - 使用命令列：移至 **\[開始\]** \> **\[執行\]**，輸入 **cmd**，然後按 Enter 鍵。在命令提示字元視窗中，輸入下列命令，然後按 Enter 鍵。
        
            iisreset /noforce
    
      - 使用 Internet Information Services (IIS) 管理員：在 Internet Information Services (IIS) 管理員的 **\[動作\]** 窗格中，按一下 **\[重新啟動\]**。

回到頁首

## 使用指令碼來啟用所有通訊協定和服務的 SSL 卸載

如果您與具有多部 Exchange 2013 Client Access Server 的大型組織合作，您可能希望加速進行前述已完成的步驟。您可以將下列任一段指令碼中的命令複製到記事本，進行任何變更，.ps1 副檔名儲存檔案，然後從 Exchange 管理命令介面執行它。根據需求而定，不論是一或多部 Client Access Server，這兩段指令碼可用來設定所有通訊協定和服務的 SSL 卸載。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Set-OutlookAnywhere</strong>指令程式項目，將&quot;MyServer&quot;用戶端存取伺服器的名稱。</td>
</tr>
</tbody>
</table>


**使用 Set-WebConfigurationProperty**

    Set-OutlookAnywhere -Identity MyServer\Rpc* -Externalhostname MyServer.mail.contoso.com -ExternalClientsRequireSsl $True -ExternalClientAuthenticationMethod Basic
    Set-OutlookAnywhere -Identity MyServer\Rpc* -SSLOffloading $true
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS:  -Location "Default Web Site/OWA"
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/ecp"
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/EWS"
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/Autodiscover"
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/Microsoft-Server-ActiveSync"
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/OAB"
    Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/MAPI"
    iisreset /noforce

**使用 appcmd**

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Set-OutlookAnywhere</strong>指令程式項目，將&quot;MyServer&quot;用戶端存取伺服器的名稱。</td>
</tr>
</tbody>
</table>


    Set-OutlookAnywhere -Identity MyServer\Rpc* -Externalhostname MyServer.mail.contoso.com -ExternalClientsRequireSsl $True -ExternalClientAuthenticationMethod Basic
    Set-OutlookAnywhere -Identity MyServer\Rpc* -SSLOffloading $true
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/owa" /section:access /sslFlags:None /commit:APPHOST
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/ecp" /section:access /sslFlags:None /commit:APPHOST
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/EWS" /section:access /sslFlags:None /commit:APPHOST
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/Autodiscover" /section:access /sslFlags:None /commit:APPHOST
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/Microsoft-Server-ActiveSync" /section:access /sslFlags:None /commit:APPHOST
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/OAB" /section:access /sslFlags:None /commit:APPHOST
    &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/MAPI" /section:access /sslFlags:None /commit:APPHOST
    iisreset /noforce

回到頁首

## 設定 Exchange 2007 與 Exchange 2010 共存

當組織中有 Exchange 2003 與 Exchange 2010 伺服器共存時，您在部署 Exchange 2010 Client Access Server 之後的第一件事就是變更 DNS，讓 Exchange 2003 使用者可從一群 Exchange 2010 Client Access Server 存取他們的信箱。在此情況下，負責將用戶端流量分散至 Client Access Server 的負載平衡器上，完全支援啟用 SSL 卸載。

**與其他版本的 Outlook Web App 共存**

只要在 Exchange 2013 Client Access Server 上設定 SSL 卸載，就能與 Exchange 2007 及 Exchange 2010 共存：

  - 若要與 Exchange 2007 共存，需要有先前的命名空間，且只有針對 Outlook Web App 和 Exchange Web 服務，才會重新導向至這個命名空間。自動探索、Outlook Anywhere 和 Exchange ActiveSync 會經由 Proxy 導向舊版。

  - 若要與 Exchange 2010 共存，如果您已設定外部 URL，則會使用重新導向。如果未設定，則會使用 Proxy。

回到頁首

