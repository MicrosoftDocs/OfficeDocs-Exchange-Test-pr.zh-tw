---
title: '將 AD FS 宣告式驗證用於 Outlook Web App 和 EAC: Exchange 2013 Help'
TOCTitle: 將 AD FS 宣告式驗證用於 Outlook Web App 和 EAC
ms:assetid: 919a9bfb-c6df-490a-b2c4-51796b0f0596
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn635116(v=EXCHG.150)
ms:contentKeyID: 61204230
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 將 AD FS 宣告式驗證用於 Outlook Web App 和 EAC

 

_**適用版本：**Exchange Server 2013 SP1_

_**上次修改主題的時間：**2017-04-14_

**摘要：**

在內部Exchange 2013 Service Pack 1 (SP1) 部署、 安裝及設定Active Directory Federation Services (AD FS) 表示您現在可以使用 AD FS 宣告式驗證連線至Outlook Web App和 EAC。您可以使用Exchange 2013 SP1 整合 AD FS 和宣告式驗證。使用宣告式驗證會取代為傳統驗證方法，包括下列：

  - Windows 驗證

  - 表單驗證

  - 摘要驗證

  - 基本驗證

  - Active Directory 用戶端憑證驗證

驗證程序可確認使用者的身分。進行驗證可確認使用者是否為其聲稱的身分。宣告式身分識別是另一種驗證方式。宣告式驗證會從應用程式 (在此範例中是 Outlook Web App 和 EAC) 移除驗證管理，以透過集中進行驗證來簡化帳戶管理。Outlook Web App 和 EAC 不負責驗證使用者、儲存使用者帳戶和密碼、查閱使用者身分識別詳細資料，或與其他身分識別系統整合。集中進行驗證可讓日後要升級為其他驗證方法時更為方便。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>裝置的 OWA 不支援 AD FS 宣告式驗證。</td>
</tr>
</tbody>
</table>


依下表摘要說明種可以使用的 AD FS 的多個版本。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Windows Server版本</th>
<th>安裝</th>
<th>AD FS 版本</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows Server 2008 R2</p></td>
<td><p><strong>下載並安裝</strong> AD FS 2.0 (這是 Windows 附加元件)。</p></td>
<td><p>AD FS 2.0</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2012</p></td>
<td><p>安裝<strong>內建的</strong> AD FS 伺服器角色。</p></td>
<td><p>AD FS 2.1</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2012 R2</p></td>
<td><p>安裝<strong>內建的</strong> AD FS 伺服器角色。</p></td>
<td><p>AD FS 3.0</p></td>
</tr>
</tbody>
</table>


您將在此處執行的工作取決於含有 AD FS 角色服務的 Windows Server 2012 R2。

**所需步驟的概觀**

Step 1 - Review the certificate requirements for AD FS

Step 2 - Install and configure Active Directory Federation Services (AD FS)

步驟 3-建立 Outlook Web App 和 EAC 的信賴憑證者信任和自訂宣告規則

步驟 4-安裝 Web 應用程式 Proxy 角色服務 （選擇性）

步驟 5-設定 Web 應用程式 Proxy 角色服務 （選擇性）

步驟 6-發佈 Outlook Web App 和 EAC 中使用 Web 應用程式 Proxy （選用）

步驟 7-設定 Exchange 2013 使用 AD FS 驗證

步驟 8-OWA 和 ECP 虛擬目錄上啟用 AD FS 驗證

步驟 9-重新啟動或重複使用 Internet Information Services (IIS)

步驟 10-測試 Outlook Web App 和 EAC 的 AD FS 宣告

Additional information you might want to know

## 開始前需要瞭解什麼？

  - 您至少需要安裝不同的 Windows Server 2012 R2 伺服器：一部作為使用 Active Directory 網域服務 (AD DS) 的網域控制站、一部作為 Exchange 2013 伺服器、一部作為 Web 應用程式 Proxy 伺服器、一部作為 Active Directory Federation Services (AD FS) 伺服器。確認已安裝所有更新。

  - 在您組織中適當數目的 Windows Server 2012 R2 伺服器上安裝 AD DS。您也可以使用 **\[伺服器管理員\]** \> **\[儀表板\]** 中的 **\[通知\]**，**\[將此伺服器升級為網域控制站\]**。

  - 為您的組織安裝適當數目的 Client Access Server 和 Mailbox Server。確認已在您組織中的所有 Exchange 2013 伺服器上安裝所有更新 (包括 SP1)。若要下載 SP1，請參閱 [更新 Exchange 2013](updates-for-exchange-2013-exchange-2013-help.md)。

  - 在伺服器上部署 Web 應用程式 Proxy 時，需要本機系統管理員權限。您必須先在組織中執行 Windows Server 2012 R2 的伺服器上部署 AD FS，才能部署 Web 應用程式 Proxy。

  - 安裝並設定 AD FS 角色，以及在 Windows Server 2012 R2 上建立信賴憑證者信任和宣告規則。若要進行這項作業，您需要使用屬於 Domain Admins、Enterprise Admins 或本機 Administrators 群組成員的使用者帳戶進行登入。

  - 參閱[功能權限](feature-permissions-exchange-2013-help.md)，以判斷 Exchange 2013 的必要權限。

  - 您必須獲指派 Outlook Web App 的管理權限。若要查看您需要哪些權限，請參閱[用戶端和行動裝置權限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主題中的＜Outlook Web App 權限＞項目。

  - 您必須獲指派 EAC 的管理權限。若要查看您需要哪些權限，請參閱 [Exchange 及命令介面基礎結構權限](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)主題中的＜Exchange 系統管理中心連線＞項目。

  - 您可能只能使用命令介面來執行某些程序。若要了解如何在內部部署 Exchange 組織中開啟命令介面，請參閱[開啟命令介面。](https://technet.microsoft.com/zh-tw/library/dd638134\(v=exchg.150\))。

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


## 步驟 1 – 檢閱 AD FS 的憑證需求

憑證扮演保護 Exchange 2013 SP1 伺服器、網頁用戶端 (例如 Outlook Web App) 與 EAC、Windows Server 2012 R2 伺服器 (包括 Active Directory Federation Services (AD FS) 伺服器和 Web 應用程式 Proxy 伺服器) 之間通訊安全性的重要角色。憑證需求會視您要設定 AD FS 伺服器、AD FS Proxy 還是 Web 應用程式 Proxy 伺服器而不同。用於 AD FS 服務的憑證 (包括 SSL 和權杖簽署憑證) 必須匯入至所有 Exchange、AD FS 和 Web 應用程式 Proxy 伺服器上的信任根憑證授權單位存放區。當您使用 [Set-OrganizationConfig](https://technet.microsoft.com/zh-tw/library/aa997443\(v=exchg.150\)) Cmdlet 時，所匯入憑證的指紋也會用於 Exchange 2013 SP1 伺服器。

在任何 AD FS 設計，各種憑證必須使用安全網際網路和 AD FS 伺服器上的使用者之間的通訊。每一部同盟伺服器必須具備服務通訊憑證或安全通訊端層 (SSL) 憑證及 AD FS 伺服器、 Active Directory網域控制站之前, 的權杖簽署憑證和Exchange 2013伺服器可以彼此通訊和進行驗證。視您的安全性和預算需求，所以請謹慎考慮何種憑證會取得由公用 CA 或企業 CA。如果您想要安裝及設定 Enterprise 根或次級 CA，您可以使用Active Directory憑證服務 (AD CS)。如果您想要更了解 AD CS，請參閱[Active Directory 憑證服務概觀 （英文)](https://go.microsoft.com/fwlink/?linkid=392697)。

雖然 AD FS 不需要 CA 所發行的憑證，但是 AD FS 用戶端必須信任 SSL 憑證 (預設也用作服務通訊憑證的 SSL 憑證)。建議您不要使用自我簽署憑證。同盟伺服器會使用 SSL 憑證來保護與網頁用戶端和同盟伺服器 Proxy 之 SSL 通訊的 Web 服務流量。因為用戶端電腦必須信任 SSL 憑證，所以建議您使用信任 CA 所簽署的憑證。您選取的所有憑證都必須有對應的私密金鑰。在您接收到來自 CA (企業或公用) 的憑證之後，請確定所有憑證都是匯入至所有伺服器上的信任根憑證授權單位存放區。您可以使用 **\[憑證\]** MMC 嵌入式管理單元將憑證匯入至存放區，或使用 Active Directory 憑證服務來發佈憑證。重要的是，如果您匯入的憑證過期，則請手動匯入另一個有效的憑證。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您使用來自 AD FS 的自我簽署權杖簽署憑證，必須在所有 Exchange 2013 伺服器上將此憑證匯入至信任根憑證授權單位存放區。如果未使用自我簽署權杖簽署憑證，並部署 Web 應用程式 Proxy，則您必須更新 Web 應用程式 Proxy 組態和所有 AD FS 信賴憑證者信任中的公開金鑰。</td>
</tr>
</tbody>
</table>


設定 Exchange 2013 SP1、AD FS 和 Web 應用程式 Proxy 時，請遵循下列憑證建議：

  - **Mailbox Server**  Mailbox Server 上所使用的憑證就是安裝 Exchange 2013 時所建立的自我簽署憑證。因為所有用戶端都是透過 Exchange 2013 Client Access Server 連線到 Exchange 2013 Mailbox Server，所以唯一需要管理的憑證就是 Client Access Server 上的憑證。

  - **Client Access Server**  需要用於服務通訊的 SSL 憑證。如果現有 SSL 憑證已包括用來設定信賴憑證者信任端點的 FQDN，則不需要其他憑證。

  - **AD FS**  AD FS 需要兩種類型的憑證：
    
      - 用於服務通訊的 SSL 憑證
        
          - 主體名稱：**adfs.contoso.com** (AD FS 部署名稱)
        
          - 主體替代名稱 (SAN)：無
    
      - 權杖簽署憑證
        
          - 主體名稱：**tokensigning.contoso.com**
        
          - 主體替代名稱 (SAN)：無
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>當您取代 AD FS 上的權杖簽署憑證時，必須更新任何現有信賴憑證者信任，以使用新的權杖簽署憑證。</td>
        </tr>
        </tbody>
        </table>


  - **Web 應用程式 Proxy**
    
      - 用於服務通訊的 SSL 憑證
        
          - 主體名稱：**owa.contoso.com**
        
          - 主體替代名稱 (SAN)：無
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>如果您的 Web 應用程式 Proxy 外部 URL 與內部 URL 相同，則可以在此重複使用 Exchange 的 SSL 憑證。</td>
        </tr>
        </tbody>
        </table>
    
      - AD FS Proxy SSL 憑證
        
          - 主體名稱：**adfs.contoso.com** (AD FS 部署名稱)
        
          - 主體替代名稱 (SAN)：無
    
      - 權杖簽署憑證 - 這會在下列步驟時從 AD FS 自動複製過來。如果使用此憑證，則您組織中的 Exchange 2013 伺服器必須信任它。

請參閱憑證需求小節中[檢閱部署 AD FS 的需求](https://go.microsoft.com/fwlink/?linkid=392699)憑證的詳細資訊。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>即使您有 AD FS 的 SSL 憑證，Outlook Web App 和 EAC 還是需要 SSL 加密憑證。SSL 憑證會用於 OWA 和 ECP 虛擬目錄上。</td>
</tr>
</tbody>
</table>


## 步驟 2 – 安裝並設定 Active Directory Federation Services (AD FS)

Windows Server 2012 R2 中的 AD FS 提供簡化、安全的身分識別同盟和網頁單一登入 (SSO) 功能。AD FS 包括一種啟用瀏覽器型 Web SSO、多重要素和宣告式驗證的同盟服務。AD FS 使用宣告式驗證和存取授權機制來維護應用程式安全性，以簡化系統和應用程式存取。

若要在 Windows Server 2012 R2 上安裝 AD FS：

1.  開啟 **\[開始\]** 畫面上的 **\[伺服器管理員\]**，或桌面的工作列上的 **\[伺服器管理員\]**。按一下 **\[管理\]** 功能表上的 **\[新增角色及功能\]**。

2.  在 **\[開始之前\]** 頁面上，按 **\[下一步\]**。

3.  在 **\[選取安裝類型\]** 頁面上，按一下 **\[角色型或功能型安裝\]**，然後按 **\[下一步\]**。

4.  在 **\[選取目的地伺服器\]** 頁面上，按一下 **\[從伺服器集區選取伺服器\]**，並驗證已選取本機電腦，然後按 **\[下一步\]**。

5.  在 **\[選取伺服器角色\]** 頁面上，按一下 **\[Active Directory Federation Services\]**，然後按 **\[下一步\]**。
    
    在 **\[選取功能\]** 頁面上，按 **\[下一步\]**。已為您選取需要的必要條件或功能。您不需要選取其他任何功能。

6.  在 **\[Active Directory Federation Service (AD FS)\]** 頁面上，按 **\[下一步\]**。

7.  在 **\[確認安裝選項\]** 頁面上，核取 **\[必要時自動重新啟動目的地伺服器\]**，然後按一下 **\[安裝\]**。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>請不要在安裝程序期間關閉精靈。</td>
    </tr>
    </tbody>
    </table>


安裝必要的 AD FS 伺服器並產生必要的憑證之後，您必須設定 AD FS，然後先測試 AD FS 運作正常。您也可以使用此為檢查清單此處可協助您在安裝和設定 AD FS：[檢查清單： Setting Up a Federation Server](https://go.microsoft.com/fwlink/?linkid=392700)。

若要設定 Active Directory Federation Services：

1.  在 **\[安裝進度\]** 頁面上，於 **\[Active Directory Federation Services\]** 下的視窗中，按一下 **\[設定此伺服器上的同盟服務\]**。\[Active Directory Federation Service 組態精靈\] 隨即開啟。

2.  在 **\[歡迎使用\]** 頁面上，按一下 **\[在同盟伺服器陣列中建立第一部同盟伺服器\]**，然後按 **\[下一步\]**。

3.  在 **\[連線至 AD DS\]** 頁面上，指定具有此電腦所加入之正確 Active Directory 網域的網域系統管理員權限的帳戶，然後按 **\[下一步\]**。如果您需要選取不同的使用者，請按一下 **\[變更\]**。

4.  在 **\[指定服務屬性\]** 頁面上執行下列動作，然後按 **\[下一步\]**：
    
      - 匯入從 AD CS 或公用 CA 先前取得的 SSL 憑證。此憑證是必要的服務驗證憑證。瀏覽至您的 SSL 憑證的位置。如需建立及匯入 SSL 憑證的詳細資訊，請參閱[伺服器憑證](https://go.microsoft.com/fwlink/?linkid=392703)。
    
      - 輸入同盟服務的名稱 (例如，輸入 **adfs.contoso.com**)。
    
      - 若要提供同盟服務的顯示名稱，請輸入組織名稱 (例如，**Contoso, Ltd.**)。

5.  在 **\[指定服務帳戶\]** 頁面上，選取 **\[使用現有網域使用者帳戶或群組受管理服務帳戶\]**，然後指定在建立網域控制站時所建立的 GMSA 帳戶 (FsGmsa)。請包括帳戶密碼，然後按 **\[下一步\]**。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>全域受管理服務帳戶 (GMSA) 是設定網域控制站時必須建立的帳戶。在 AD FS 安裝和組態期間需要 GMSA 帳戶。如果您尚未建立此帳戶，請執行下列 Windows PowerShell 命令。它會建立 contoso.com 網域和 AD FS 伺服器的帳戶：</td>
    </tr>
    </tbody>
    </table>


6.  執行下列命令。
    
        Add-KdsRootKey -EffectiveTime (Get-Date).AddHours(-10)

7.  此範例會建立名為 FsGmsa 名為 adfs.contoso.com 同盟服務的新 GMSA 帳戶。Federation Service 名稱是用戶端可以看到的值。
    
        New-ADServiceAccount FsGmsa -DNSHostName adfs.contoso.com -ServicePrincipalNames http/adfs.contoso.com

8.  在 **\[指定組態資料庫\]** 頁面上，選取 **\[使用 Windows Internal Database 在此伺服器上建立資料庫\]**，然後按 **\[下一步\]**。

9.  在 **\[檢閱選項\]** 頁面上，驗證組態選取項目。您可以選擇性地使用 **\[檢視指令碼\]** 按鈕來自動進行其他 AD FS 安裝。按 **\[下一步\]**。

10. 在 **\[必要條件檢查\]** 頁面上，確認已順利完成所有必要條件檢查，然後按一下 **\[設定\]**。

11. 在 **\[安裝進度\]** 頁面上，確認已正確安裝所有項目，然後按一下 **\[關閉\]**。

12. 在 **\[結果\]** 頁面上檢閱結果，並檢查是否順利完成組態，然後按一下 **\[完成同盟服務部署所需的後續步驟\]**。

下列Windows PowerShell 命令執行先前的步驟同樣的事情。

    Import-Module ADFS

    Install-AdfsFarm -CertificateThumbprint 0E0C205D252002D535F6D32026B6AB074FB840E7 -FederationServiceDisplayName "Contoso Corporation" -FederationServiceName adfs.contoso.com -GroupServiceAccountIdentifier "contoso\FSgmsa`$"

如需詳細資訊和語法，請參閱 ＜ [Install AdfsFarm](https://go.microsoft.com/fwlink/?linkid=392704)。

若要驗證安裝：在 AD FS 伺服器上，開啟網頁瀏覽器，然後瀏覽至同盟中繼資料的 URL (例如，**https://adfs.contoso.com/federationmetadata/2007-06/federationmetadata.xml**)。

## 步驟 3-建立 Outlook Web App 和 EAC 的信賴憑證者信任和自訂宣告規則

對於所有應用程式與您想要發佈到 Web 應用程式 Proxy 的服務，您必須設定信賴憑證者信任 AD FS 伺服器上。部署多個Active Directory站台使用不同的命名空間， Outlook Web App和 EAC 的信賴憑證者廠商信任必須新增每個命名空間。

EAC 會使用 ECP 虛擬目錄。您可以使用 [Get-EcpVirtualDirectory](https://technet.microsoft.com/zh-tw/library/dd351058\(v=exchg.150\)) 和 [Set-EcpVirtualDirectory](https://technet.microsoft.com/zh-tw/library/dd297991\(v=exchg.150\)) Cmdlet，來檢視或設定 EAC 的設定。若要存取 EAC，您必須使用網頁瀏覽器，並移至 **http://server1.contoso.com/ecp**。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>下面所顯示的 URL 範例在行尾斜線<strong>/</strong>的相對路徑是刻意。請務必確認 AD FS 信賴憑證者信任和 Exchange 對象 URI 的<strong>皆相同</strong>。 這表示信賴憑證者信任 AD FS 與 Exchange 對象 URI 的應該<strong>同時具備</strong>或<strong>兩者發出</strong>尾隨斜線及其 url。本節中的範例包含結尾<strong>/</strong>的之後任何以&quot;owa&quot;(/owa/) 或&quot;ecp&quot;(/ecp/) 的 url。</td>
</tr>
</tbody>
</table>


針對 Outlook Web App，若要使用 Windows Server 2012 R2 中的 \[AD FS 管理\] 嵌入式管理單元來建立信賴憑證者信任：

1.  在 **\[伺服器管理員\]** 中，按一下 **\[工具\]**，然後選取 **\[AD FS 管理\]**。

2.  在 **\[AD FS 嵌入式管理單元\]** 的 **\[AD FS\\信任關係\]** 中，於 **\[信賴憑證者信任\]** 上按一下滑鼠右鍵，然後按一下 **\[新增信賴憑證者信任\]** 以開啟 **\[新增信賴憑證者信任\]** 精靈。

3.  在 **\[歡迎使用\]** 頁面上，按一下 **\[開始\]**。

4.  在 **\[選取資料來源\]** 頁面上，按一下 **\[手動輸入信賴憑證者相關資料\]**，然後按 **\[下一步\]**。

5.  在 \[**指定顯示名稱**\] 頁面上 \[**顯示名稱**\] 方塊中輸入**Outlook Web App**，和 \[**備忘稿**、 type 此信賴憑證者信任 （例如，**這是 https://mail.contoso.com/owa/ 信任**） 的描述及然後按 \[**下一步**。

6.  在 **\[選擇設定檔\]** 頁面上，按一下 **\[AD FS 設定檔\]**，然後按 **\[下一步\]**。

7.  在 **\[設定憑證\]** 頁面上，按 **\[下一步\]**。

8.  在 \[**設定 URL** \] 頁面上按一下 \[**啟用 WS-同盟被動式通訊協定的支援**，然後 \[**信賴憑證者廠商 WS-同盟被動式通訊協定 URL**、**類型 https://mail.contoso.com/owa/**，然後按 \[下一步.

9.  在 **\[設定識別碼\]** 頁面上，指定此信賴憑證者的一個或多個識別碼，並按一下 **\[新增\]** 將它們新增至清單，然後按 **\[下一步\]**。

10. 在 **\[是否立即設定多重要素驗證?\]** 頁面上，選取 **\[設定此信賴憑證者信任的多重要素驗證設定\]**。

11. 在 **\[設定多重要素驗證\]** 頁面上，確認已選取 **\[目前不想要設定此信賴憑證者信任的多重要素驗證設定\]**，然後按 **\[下一步\]**。

12. 在 **\[選擇發行授權規則\]** 頁面上，選取 **\[允許所有使用者存取此信賴憑證者\]**，然後按 **\[下一步\]**。

13. 在 **\[準備好新增信任\]** 頁面上檢閱設定，然後按 **\[下一步\]** 儲存信賴憑證者信任資訊。

14. 在 **\[完成\]** 頁面上，確認未選取 **\[在關閉精靈時開啟此信賴憑證者信任的編輯宣告規則對話方塊\]**，然後按一下 **\[關閉\]**。

若要建立 EAC 的信賴憑證者信任，您必須重新執行這些步驟，並建立第二個信賴憑證者信任，但是是輸入 **EAC**，而不是將 **Outlook Web App** 作為顯示名稱。在描述中輸入 **This is a trust for the Exchange Admin Center**，而且 **\[信賴憑證者 WS-同盟被動通訊協定 URL\]** 是 **https://mail.contoso.com/ecp**。

在宣告式身分識別模型中，作為同盟服務的 Active Directory Federation Services (AD FS) 的功能是發出含有一組宣告的權杖。宣告規則可控管與 AD FS 所發出宣告相關的決策。宣告規則和所有伺服器組態資料都是儲存在 AD FS 組態資料庫中。

它具有您需要建立兩個宣告規則：

  - Active Directory 使用者 SID

  - Active Directory UPN

若要新增必要的宣告規則：

1.  在 **\[伺服器管理員\]** 中，按一下 **\[工具\]**，然後按一下 **\[AD FS 管理\]**。

2.  在主控台樹狀目錄的 **\[AD FS\\信任關係\]** 下，按一下 **\[宣告提供者信任\]** 或 **\[信賴憑證者信任\]**，然後按一下 Outlook Web App 的信賴憑證者信任。

3.  在 **\[信賴憑證者信任\]** 視窗中，於 Outlook Web App 信任上按一下滑鼠右鍵，然後按一下 **\[編輯宣告規則\]**。

4.  在 **\[編輯宣告規則\]** 視窗的 **\[發行轉換規則\]** 索引標籤上，按一下 **\[新增規則\]** 啟動 \[新增轉換宣告規則精靈\]。

5.  在 **\[選取規則範本\]** 頁面的 **\[宣告規則範本\]** 下，選取清單中的 **\[使用自訂規則傳送宣告\]**，然後按 **\[下一步\]**。

6.  在 **\[設定規則\]** 頁面的 **\[選擇規則類型\]** 步驟中，於 **\[宣告規則名稱\]** 下輸入宣告規則的名稱。請使用可描述用途的宣告規則名稱 (例如，**ActiveDirectoryUserSID**)。在 **\[自訂規則\]** 下，為此規則輸入下列宣告規則語言語法：
    
        c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"] => issue(store = "Active Directory", types = ("http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid"), query = ";objectSID;{0}", param = c.Value);

7.  在 **\[設定規則\]** 頁面上，按一下 **\[完成\]**。

8.  在 **\[編輯宣告規則\]** 視窗的 **\[發行轉換規則\]** 索引標籤上，按一下 **\[新增規則\]** 啟動 \[新增轉換宣告規則精靈\]。

9.  在 **\[選取規則範本\]** 頁面的 **\[宣告規則範本\]** 下，選取清單中的 **\[使用自訂規則傳送宣告\]**，然後按 **\[下一步\]**。

10. 在 **\[設定規則\]** 頁面的 **\[選擇規則類型\]** 步驟上，於 **\[宣告規則名稱\]** 下輸入宣告規則的名稱。請使用可描述用途的宣告規則名稱 (例如，**ActiveDirectoryUPN**)。在 **\[自訂規則\]** 下，為此規則輸入下列宣告規則語言語法：
    
        c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"] => issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn"), query = ";userPrincipalName;{0}", param = c.Value);

11. 按一下 **\[完成\]**。

12. 在 **\[編輯宣告規則\]** 視窗中，按一下 **\[套用\]**，然後按一下 **\[確定\]**。

13. 針對 EAC 的信賴憑證者信任重複此程序的步驟 3-12。

或者，您可以建立轉送信任並使用Windows PowerShell 宣告規則：

1.  建立兩個 .txt 檔案 IssuanceAuthorizationRules.txt 和 IssuanceTransformRules.txt。

2.  將其內容匯入至兩個變數。

3.  執行下列兩個 Cmdlet，以建立信賴憑證者信任。在此範例中，這也會設定宣告規則。

**IssuanceAuthorizationRules.txt 包含：**

    @RuleTemplate = "AllowAllAuthzRule" => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

**IssuanceTransformRules.txt 包含：**

    @RuleName = "ActiveDirectoryUserSID" c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"] => issue(store = "Active Directory", types = ("http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid"), query = ";objectSID;{0}", param = c.Value); 
    
    @RuleName = "ActiveDirectoryUPN" c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"] => issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn"), query = ";userPrincipalName;{0}", param = c.Value);

**執行下列命令：**

    [string]$IssuanceAuthorizationRules=Get-Content -Path C:\IssuanceAuthorizationRules.txt
    
    [string]$IssuanceTransformRules=Get-Content -Path c:\IssuanceTransformRules.txt
    
    Add-ADFSRelyingPartyTrust -Name "Outlook Web App" -Enabled $true -Notes "This is a trust for https://mail.contoso.com/owa/" -WSFedEndpoint https://mail.contoso.com/owa/ -Identifier https://mail.contoso.com/owa/ -IssuanceTransformRules $IssuanceTransformRules -IssuanceAuthorizationRules $IssuanceAuthorizationRules
    
    Add-ADFSRelyingPartyTrust -Name "Exchange Admin Center (EAC)" -Enabled $true -Notes "This is a trust for https://mail.contoso.com/ecp/" -WSFedEndpoint https://mail.contoso.com/ecp/ -Identifier https://mail.contoso.com/ecp/ -IssuanceTransformRules $IssuanceTransformRules -IssuanceAuthorizationRules $IssuanceAuthorizationRules

## 步驟 4 – 安裝 Web 應用程式 Proxy 角色服務 （選擇性）

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>步驟 4、 步驟 5 和步驟 6 是如使用者想要發佈 Exchange OWA 和 ECP 使用 Web 應用程式 Proxy，並誰要有執行 AD FS 驗證的 Web 應用程式 Proxy。不過，與 Web 應用程式 Proxy 發佈 Exchange 則不需要，因此您可以略過步驟 7 如果您未使用 Web 應用程式 Proxy 與您想執行本身的 AD FS 驗證 Exchange。</td>
</tr>
</tbody>
</table>


Web 應用程式 Proxy 為Windows Server 2012 R2 中的新遠端存取角色服務。Web 應用程式 Proxy 提供貴公司網路內可允許使用者在公司網路之外存取其從許多裝置上的 web 應用程式的反向 proxy 功能。Web 應用程式 Proxy 會使用Active Directory Federation Services (AD FS) 來預先驗證存取 web 應用程式和也功能為 AD FS proxy。Web 應用程式 Proxy 不一定、 建議的外部用戶端存取 AD FS 時。不過，在Outlook Web App離線存取不支援時使用 AD FS 驗證透過 Web 應用程式 Proxy。您可以找到的[安裝及設定 Web 應用程式 Proxy 發佈的內部應用程式](https://go.microsoft.com/fwlink/?linkid=392705)看不到整合與 Web 應用程式 Proxy 的詳細資訊

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您無法在已安裝 AD FS 的相同伺服器上安裝 Web 應用程式 Proxy。</td>
</tr>
</tbody>
</table>


若要部署 Web 應用程式 Proxy，您必須在將用作 Web 應用程式 Proxy 伺服器的伺服器上，安裝具有 Web 應用程式 Proxy 角色服務的遠端存取伺服器角色。若要安裝 Web 應用程式 Proxy 角色服務：

1.  在 Web 應用程式 Proxy 伺服器上，於 **\[伺服器管理員\]** 中按一下 **\[管理\]**，然後按一下 **\[新增角色及功能\]**。

2.  在 \[新增角色及功能精靈\] 中，按三次 **\[下一步\]**，以到達 **\[伺服器角色\]** 頁面。

3.  在 **\[伺服器角色\]** 頁面上，選取清單中的 **\[遠端存取\]**，然後按 **\[下一步\]**。

4.  在 **\[功能\]** 頁面上，按 **\[下一步\]**。

5.  閱讀 **\[遠端存取\]** 頁面上的資訊，然後按 **\[下一步\]**。

6.  在 **\[角色服務\]** 頁面上，選取 **\[Web 應用程式 Proxy\]**。然後，在 **\[新增角色及功能精靈\]** 視窗中按一下 **\[新增功能\]**，接著再按 **\[下一步\]**。

7.  在 **\[確認\]** 視窗中，按一下 **\[安裝\]**。您也可以核取 **\[必要時自動重新啟動目的地伺服器\]**。

8.  在 **\[安裝進度\]** 對話方塊中，確認安裝成功，然後按一下 **\[關閉\]**。

下列 Windows PowerShell Cmdlet 的作用與先前的步驟相同。

    Install-WindowsFeature Web-Application-Proxy -IncludeManagementTools

## 步驟 5 – 設定 Web 應用程式 Proxy 角色服務 （選擇性）

您必須將 Web 應用程式 Proxy 設定為連線到 AD FS 伺服器。請針對想要部署為 Web 應用程式 Proxy 伺服器的所有伺服器重複此程序。

若要設定 Web 應用程式角色服務：

1.  在 Web 應用程式 Proxy 伺服器上，於 **\[伺服器管理員\]** 中按一下 **\[工具\]**，然後按一下 **\[遠端存取管理\]**。

2.  在 **\[組態\]** 窗格中，按一下 **\[Web 應用程式 Proxy\]**。

3.  在 **\[遠端存取管理\]** 主控台的中間窗格中，按一下 **\[執行 Web 應用程式 Proxy 組態精靈\]**。

4.  在 \[Web 應用程式 Proxy 組態精靈\] 的 **\[歡迎使用\]** 對話方塊中，按 **\[下一步\]**。

5.  在 **\[同盟伺服器\]** 頁面上執行下列動作，然後按 **\[下一步\]**：
    
      - 在 **\[同盟服務名稱\]** 方塊中，輸入 AD FS 伺服器的完整網域名稱 (FQDN) (例如，**adfs.contoso.com**)。
    
      - 在 **\[使用者名稱\]** 和 **\[密碼\]** 方塊中，輸入 AD FS 伺服器上本機系統管理員帳戶的認證。

6.  在 **\[AD FS Proxy 憑證\]** 對話方塊中，於目前安裝於 Web 應用程式 Proxy 伺服器之憑證的清單中，選取 Web 應用程式 Proxy 要用於 AD FS Proxy 功能的憑證，然後按 **\[下一步\]**。您在這裡選擇的憑證應該是主旨為同盟服務名稱的憑證 (例如，**adfs.contoso.com**)。

7.  在 **\[確認\]** 對話方塊中檢閱設定。必要時，您可以複製 Windows PowerShell Cmdlet，以自動進行其他安裝。按一下 **\[設定\]**。

8.  在 **\[結果\]** 對話方塊中，確認組態成功，然後按一下 **\[關閉\]**。

下列 Windows PowerShell Cmdlet 的作用與先前的步驟相同。

    Install-WebApplicationProxy -CertificateThumprint 1a2b3c4d5e6f1a2b3c4d5e6f1a2b3c4d5e6f1a2b -FederationServiceName adfs.contoso.com

## 步驟 6 – 使用 Web 應用程式 Proxy （選用） 發佈 Outlook Web App 和 EAC

在步驟 3、 建立宣告轉送信任Outlook Web App和 EAC 中，您現在需要與發佈兩個這些應用程式。但是您這麼做之前，請確認已建立信賴憑證者信任他們，並確認您具備憑證適用於Outlook Web App和 EAC 的 Web 應用程式 Proxy 伺服器上。您需要在 AD FS 管理主控台中，要發佈的 Web 應用程式 Proxy 的所有 AD FS 端點的您必須設定為**Proxy 啟用**的端點。

依照步驟，使用 Web 應用程式 Proxy 來發佈 Outlook Web App。對 EAC 重複這些步驟。當您發佈 EAC 時，需要變更名稱、外部 URL、外部憑證和後端 URL。

若要使用 Web 應用程式 Proxy 來發佈 Outlook Web App 和 EAC：

1.  在 Web 應用程式 Proxy 伺服器上，於 **\[遠端存取管理\]** 主控台的 **\[瀏覽\]** 窗格中，按一下 **\[Web 應用程式 Proxy\]**，然後按一下 **\[工作\]** 窗格中的 **\[發佈\]**。

2.  在 \[發佈新的應用程式精靈\] 的 **\[歡迎使用\]** 頁面上，按 **\[下一步\]**。

3.  在 **\[預先驗證\]** 頁面上，按一下 **\[Active Directory Federation Services (AD FS)\]**，然後按 **\[下一步\]**。

4.  在 **\[信賴憑證者\]** 頁面上，於信賴憑證者清單中選取想要發佈之應用程式的信賴憑證者，然後按 **\[下一步\]**。

5.  在 **\[發佈設定\]** 頁面上，執行下列動作，然後按 **\[下一步\]**：
    
    1.  在 **\[名稱\]** 方塊中，輸入易記的應用程式名稱。此名稱只用於 **\[遠端存取管理主控台\]** 的已發佈應用程式清單中。您可以使用 **OWA** 和 **EAC** 作為名稱。
    
    2.  在 \[**外部 URL** \] 方塊中輸入此應用程式的外部 URL — 例如**https://external.contoso.com/owa/**Outlook Web App和**https://external.contoso.com/ecp/**的 EAC。
    
    3.  在 **\[外部憑證\]** 清單中，選取其主體名稱符合外部 URL 之主機名稱的憑證。
    
    4.  在**後端伺服器 URL** \] 方塊中輸入後端伺服器的 URL。請注意此值會自動輸入當您輸入的外部 URL，且應只有後端伺服器 URL 不同變更 — 例如**https://mail.contoso.com/owa/**Outlook Web App和**https://mail.contoso.com/ecp/**的 EAC。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Web 應用程式 Proxy 可以轉譯 URL 中的主機名稱，但不能轉譯路徑。因此，您可以輸入不同的主機名稱，但是必須輸入相同的路徑。例如，您可以輸入外部 URL <em>https://external.contoso.com/app1/</em> 和後端伺服器 URL <em>https://mail.contoso.com/app1/</em>。不過，您無法輸入外部 URL <em>https://external.contoso.com/app1/</em> 和後端伺服器 URL <em>https://mail.contoso.com/internal-app1/</em>。</td>
    </tr>
    </tbody>
    </table>


6.  在 **\[確認\]** 頁面上檢閱設定，然後按一下 **\[發佈\]**。您可以複製 Windows PowerShell 命令來設定其他已發佈的應用程式。

7.  在 **\[結果\]** 頁面上，確定已順利發佈應用程式，然後按一下 **\[關閉\]**。

下列 Windows PowerShell Cmdlet 所執行的工作與先前的 Outlook Web App 程序相同。

    Add-WebApplicationProxyApplication -BackendServerUrl 'https://mail.contoso.com/owa/' -ExternalCertificateThumbprint 'E9D5F6CDEA243E6E62090B96EC6DE873AF821983' -ExternalUrl 'https://external.contoso.com/owa/' -Name 'OWA' -ExternalPreAuthentication ADFS -ADFSRelyingPartyName 'Outlook Web App'

下列 Windows PowerShell Cmdlet 所執行的工作與先前的 EAC 程序相同。

    Add-WebApplicationProxyApplication -BackendServerUrl 'https://mail.contoso.com/ecp/' -ExternalCertificateThumbprint 'E9D5F6CDEA243E6E62090B96EC6DE873AF821983' -ExternalUrl 'https://external.contoso.com/ecp/' -Name 'EAC' -ExternalPreAuthentication ADFS -ADFSRelyingPartyName 'Exchange Admin Center'

完成這些步驟之後，Web 應用程式 Proxy 將 Outlook Web App 和 EAC 用戶端執行 AD FS 驗證及也會顯示 proxy 連線至 Exchange 其代理。您不需要設定 AD FS 驗證 Exchange 本身，所以請繼續進行至步驟 10，以測試您的設定。

## 步驟 7 – 設定 Exchange 2013 使用 AD FS 驗證

在設定要對 Exchange 2013 中的 Outlook Web App 和 EAC 的宣告式驗證使用 AD FS 時，您必須針對 Exchange 組織啟用 AD FS。您必須使用 [Set-OrganizationConfig](https://technet.microsoft.com/zh-tw/library/aa997443\(v=exchg.150\)) Cmdlet 設定組織的 AD FS 設定：

  - 設定 AD FS 簽發者為**https://adfs.contoso.com/adfs/ls/**。

  - 設定 AD FS Uri **https://mail.contoso.com/owa/**及**https://mail.contoso.com/ecp/**。

  - 尋找 AD FS 權杖簽署憑證指紋使用 AD FS 伺服器上的Windows PowerShell 並輸入`Get-ADFSCertificate -CertificateType "Token-signing"`。然後，指定您所找到的權杖簽署憑證指紋。如果 AD FS 權杖簽署憑證已過期，從新的 AD FS 權杖簽署憑證指紋必須更新使用[Set-OrganizationConfig](https://technet.microsoft.com/zh-tw/library/aa997443\(v=exchg.150\))指令程式。

在 Exchange 管理命令介面中執行下列命令。

    $uris = @(" https://mail.contoso.com/owa/","https://mail.contoso.com/ecp/")
    Set-OrganizationConfig -AdfsIssuer "https://adfs.contoso.com/adfs/ls/" -AdfsAudienceUris $uris -AdfsSignCertificateThumbprint "88970C64278A15D642934DC2961D9CCA5E28DA6B"

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>這些案例不支援<em>-AdfsEncryptCertificateThumbprint</em>參數。</td>
</tr>
</tbody>
</table>


如需詳細資訊和語法，請參閱[Set-OrganizationConfig](https://technet.microsoft.com/zh-tw/library/aa997443\(v=exchg.150\))和[取得 ADFSCertificate](https://go.microsoft.com/fwlink/?linkid=392706)。

## 步驟 8 – 在 OWA 和 ECP 虛擬目錄上啟用 AD FS 驗證

針對 OWA 和 ECP 虛擬目錄，啟用 AD FS 驗證作為唯一的驗證方法，並停用其他所有形式的驗證。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您必須先設定 ECP 虛擬目錄，再設定 OWA 虛擬目錄。</td>
</tr>
</tbody>
</table>


使用 Exchange 管理命令介面設定 ECP 虛擬目錄。在命令介面\] 視窗中，執行下列命令。

    Get-EcpVirtualDirectory | Set-EcpVirtualDirectory -AdfsAuthentication $true -BasicAuthentication $false -DigestAuthentication $false -FormsAuthentication $false -WindowsAuthentication $false

使用 Exchange 管理命令介面設定 OWA 虛擬目錄。在命令介面\] 視窗中，執行下列命令。

    Get-OwaVirtualDirectory | Set-OwaVirtualDirectory -AdfsAuthentication $true -BasicAuthentication $false -DigestAuthentication $false -FormsAuthentication $false -WindowsAuthentication $false -OAuthAuthentication $false

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>上述的 Exchange 管理命令介面命令在組織中每個用戶端存取伺服器上設定 OWA 和 ECP 虛擬目錄。如果您不想將這些設定套用至所有的用戶端存取伺服器，使用<em>-Identity</em>參數和指定的用戶端存取伺服器。很有可能會想要這些設定僅適用於您組織中用戶端存取伺服器的網際網路對向。</td>
</tr>
</tbody>
</table>


如需詳細資料和語法，請參閱 [Get-OwaVirtualDirectory](https://technet.microsoft.com/zh-tw/library/aa998588\(v=exchg.150\)) 和 [Set-OwaVirtualDirectory](https://technet.microsoft.com/zh-tw/library/bb123515\(v=exchg.150\)) 或 [Get-EcpVirtualDirectory](https://technet.microsoft.com/zh-tw/library/dd351058\(v=exchg.150\)) 和 [Set-EcpVirtualDirectory](https://technet.microsoft.com/zh-tw/library/dd297991\(v=exchg.150\))。

## 步驟 9 – 重新啟動或重複使用 Internet Information Services (IIS)

在您完成所有必要步驟之後 (包括變更 Exchange 虛擬目錄)，便需要重新啟動 Internet Information Services。若要進行這項作業，您可以使用下列其中一種方法：

  - 使用 Windows PowerShell：
    
        Restart-Service W3SVC,WAS -noforce

  - 使用命令列：依序按一下 **\[開始\]**、**\[執行\]**，鍵入 `IISReset /noforce`，然後按一下 **\[確定\]**。

  - 使用 Internet Information Servers (IIS) 管理員：在 **\[伺服器管理員\]** \> **\[IIS\]** 中，按一下 **\[工具\]**，然後按一下 **\[Internet Information Services (IIS) 管理員\]**。在 **\[Internet Information Servers (IIS) 管理員\]** 視窗中，於 **\[管理伺服器\]** 下的動作窗格中，按一下 **\[重新啟動\]**。

## 步驟 10-測試 Outlook Web App 和 EAC 的 AD FS 宣告

測試 Outlook Web App 的 AD FS 宣告：

  - 在網頁瀏覽器中，登入 Outlook Web App — 例如， **https://mail.contoso.com/owa**

  - 在瀏覽器視窗中，如果您收到憑證錯誤，請仍繼續前往 Outlook Web App 網站。您應該會重新導向至 ADFS 登入頁面或 ADFS 提示認證。

  - 輸入您的使用者名稱 (domain\\user) 和密碼\] 和 \[**登入**。

Outlook Web App 會在視窗中載入。

若要測試 EAC 的 AD FS 宣告：

1.  在您的網頁瀏覽器中，移至 **https://mail.contoso.com/ecp**。

2.  在瀏覽器視窗中，如果您收到憑證錯誤，請仍繼續前往 ECP 網站。您應該會重新導向至 ADFS 登入頁面或 ADFS 提示認證。

3.  輸入您的使用者名稱 (domain\\user) 和密碼\] 和 \[**登入**。

4.  EAC 應該就會在視窗中載入。

## 您可能想要知道的其他資訊

**多重要素驗證**

針對內部部署 Exchange 2013 SP1 部署，使用宣告來部署和設定 Active Directory Federation Services (AD FS) 2.0，即表示 Exchange 2013 SP1 中的 Outlook Web App 和 EAC 可以支援多重要素驗證方法 (例如憑證型驗證、驗證或安全性權杖，以及指紋驗證)。雙重要素驗證常與其他形式的驗證混淆。多重要素驗證需要使用三種驗證要素的其中兩個。這些要素如下：

  - 使用者才會知道的資訊 (例如，密碼、PIN 或模式)

  - 使用者才會擁有的物件 (例如，ATM 卡、安全性權杖、智慧卡或行動電話)

  - 使用者才會有的特質 (例如，指紋等生物特徵)

Windows Server 2012 R2 中的多重要素驗證的詳細資訊，請參閱[概觀 （英文)： 與其他的多重要素驗證機密的應用程式的管理風險](https://go.microsoft.com/fwlink/?linkid=392707)和[逐步指南： 與管理風險機密的應用程式的其他多重要素驗證](https://go.microsoft.com/fwlink/?linkid=392708)。

在Windows Server 2012 R2 AD FS 角色服務，federation service 做為安全性權杖服務、 提供可用以宣告安全性權杖並讓您能夠支援多重要素驗證。Federation service 發出 token 根據所提供的認證。帳戶儲存區驗證使用者的認證之後，使用者宣告所產生的信任原則規則和再新增至發行給用戶端安全性權杖。如需宣告的詳細資訊，請參閱[了解宣告](https://go.microsoft.com/fwlink/?linkid=392709)。

**與其他版本的 Exchange 共同現有**

有可能時您有多個版本的 Exchange 部署在組織中使用 Outlook Web App 和 EAC 的 AD FS 驗證。此案例僅支援 Exchange 2010 與 Exchange 2013 部署和只有當所有用戶端連線到 Exchange 2013 伺服器**與**這些 Exchange 2013 伺服器已設定為 AD FS 驗證。

使用 Exchange 2010 伺服器上信箱的使用者可以透過設定 AD FS 驗證的 Exchange 2013 server 存取其信箱。Exchange 2013 伺服器的初始的用戶端連線會使用 AD FS 驗證。代理連線到 Exchange 2010 伺服器，但是會使用 Kerberos。 沒有直接的 AD FS 驗證設定 Exchange Server 2010 支援的方法。

