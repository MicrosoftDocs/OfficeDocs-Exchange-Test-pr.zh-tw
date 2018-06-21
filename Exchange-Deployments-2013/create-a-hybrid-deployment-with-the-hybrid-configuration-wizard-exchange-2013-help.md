---
title: '使用混合組態精靈建立混合部署: Exchange 2013 Help'
TOCTitle: 使用混合組態精靈建立混合部署
ms:assetid: 997a25d3-7fb3-4d4e-bb28-defcbf542c99
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ200787(v=EXCHG.150)
ms:contentKeyID: 50474703
ms.date: 03/14/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 使用混合組態精靈建立混合部署

本主題正在編輯中。  

_<strong>適用版本：</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>上次修改主題的時間：</strong>2016-12-09_

藉由建立混合部署，您就可以將現有內部部署 Exchange Server 組織內功能豐富的經驗與管理控制延伸至雲端。混合部署還會透過 Exchange Online 封存，為內部部署信箱提供雲端式封存解決方案，同時作為將內部部署信箱完整移轉至 Exchange Online 的中繼步驟。

本主題涵蓋使用混合組態精靈設定 Office 365 企業版中內部部署 Exchange 組織與 Exchange Online 組織的混合部署。在本主題中，混合部署是針對下列組織組態所建立：

  - 內部部署組織為單一樹系內部部署 Exchange 組織。

  - 內部部署組織不使用現有的 Microsoft Exchange Online Protection (EOP) 服務提供內部部署保護。

  - 內部部署組織未部署 Edge Transport Server。混合組態精靈支援在混合部署過程中設定 Edge Transport Server，但是在精靈中設定 Edge Transport Server 並未涵蓋在本主題中。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ906432.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用混合組態精靈設定混合部署需要先有幾項重要的必要條件，精靈才能順利完成且混合部署功能才能正確運作。您必須先完成<a href="hybrid-deployment-prerequisites-exchange-2013-help.md">混合部署必要條件</a>中所述的所有必要條件，再使用混合組態精靈建立及設定混合部署。<br />
此外，<a href="http://technet.microsoft.com/exdeploy2013">Exchange Server 部署助理</a> 是免費的 Web 化工具，可協助您在內部部署組織與 Office 365 之間設定混合式部署，或完整地移轉到 Office 365。此工具會提出一些簡單的問題，然後根據您的回答來建立自訂的檢查清單，並指示如何設定混合式佈署。強烈建議您使用部署助理，根據您特定的組織需求來產生自訂的混合式部署檢查清單。</td>
</tr>
</tbody>
</table>


如需其他混合式部署相關的管理工作資訊，請參閱 [混合式部署程序](hybrid-deployment-procedures-exchange-2013-help.md)。

若要深入了解混合部署，請參閱[Exchange Server 混合部署](exchange-server-hybrid-deployments-exchange-2013-help.md)。若要深入了解 Office 365，請參閱[什麼是 Office 365](http://go.microsoft.com/fwlink/?linkid=266712)。

## 開始之前有哪些須知？

  - 預估完成時間：30 分鐘
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ906432.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>設定混合部署的需求所需的時間會比預估完成本主題中所述的混合組態精靈程序所需的時間更長。例如，註冊 Office 365 (企業用戶適用)、設定 Active Directory 同步處理，以及指派 Exchange Online 授權，都需要投入相當長的時間，而且可能包含網路拓撲變更。您規劃完成端對端混合部署組態的整體時間，應比所列完成此程序的時間更長。</td>
    </tr>
    </tbody>
    </table>


  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱[Exchange 及命令介面基礎結構權限](https://technet.microsoft.com/zh-tw/library/dd638114\(v=exchg.150\))主題中的「混合式部署」項目。

  - 您需要從執行最新版 Exchange 支援版本的電腦執行混合組態精靈。在混合組態精靈中，最後設定 Exchange OAuth 驗證的步驟要求從內部部署 Exchange 或任何加入網域的伺服器或工作站來執行步驟。此外，使用 Internet Explorer 11 或更新的桌上型版本時，OAuth 驗證程序的效果最佳。

  - 請檢閱[Exchange Server 混合部署](exchange-server-hybrid-deployments-exchange-2013-help.md)，確認您了解設定混合部署將影響的範圍。

  - 請檢閱並完成[混合部署必要條件](hybrid-deployment-prerequisites-exchange-2013-help.md)中所述的所有混合部署需求。

  - Microsoft Remote Connectivity Analyzer 工具會檢查內部部署 Exchange 組織的對外連線能力，並確保您能夠著手設定混合部署。我們強烈建議您在使用混合組態精靈設定混合部署前，先使用 Remote Connectivity Analyzer 工具來檢查您的內部部署組織。若要深入了解，請造訪 [Remote Connectivity Analyzer 工具](http://go.microsoft.com/fwlink/p/?linkid=167905)。

  - 我們強烈建議使用 Azure Active Directory Connect 的密碼同步處理來設定單一登入。單一登入可讓使用者以單一使用者名稱和密碼存取內部部署和 Exchange Online 組織。單一登入還可確保使用 Exchange Online 封存時，不會在使用者存取 Exchange Online 組織中的封存內容時提示其提供認證。如需關於密碼同步處理的詳細資訊，請參閱 [Azure AD Connect 同步：實施密碼同步處理](http://go.microsoft.com/fwlink/p/?linkid=723513)

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](https://technet.microsoft.com/zh-tw/library/jj150484\(v=exchg.150\))。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ906432.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 使用 Exchange 系統管理中心和混合組態精靈建立混合部署

使用下列程序建立和設定混合部署：

1.  在內部部署組織之 Exchange 伺服器上的 EAC 中，瀏覽至 **\[混合\]** 節點。

2.  在 **\[混合\]** 節點，按一下 **\[設定\]** 輸入您的 Office 365 認證。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ906432.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您的內部部署組織位於中國，且 Office 365 承租人由 21Vianet 所主控，則必須選取 <strong>[我的 Office 365 組織由 21Vianet 主控]</strong> 核取方塊。如果您的 Office 365 承租人由 21Vianet 所主控，但未選取此核取方塊，則混合組態精靈不會連接到 21Vianet 服務，將無法辨識您的 Office 365 帳戶認證，精靈也無法正確完成。</td>
    </tr>
    </tbody>
    </table>


3.  在提示您登入 Office 365 時，請選取 **\[登入 Office 365\]**，並輸入帳戶認證。您登入的帳戶必須是 Office 365 的全域管理員。

4.  再按一下 **\[設定\]**，啟動混合組態精靈。

5.  在 \[**Microsoft Office 365 混合組態精靈下載**\] 頁面上，按一下 **請按這裡** 以下載精靈。當您被提示時，按一下 **\[應用程式安裝\]** 對話方塊上的 **\[安裝\]**。

6.  按一下 **\[下一步\]**，然後在 **\[內部部署 Exchange Server 組織\]** 的區段中，選取 **偵測執行Exchange 2013 CAS 或 Exchange 2016 的伺服器**。精靈將會嘗試偵測內部部署 Exchange 伺服器。如果精靈未偵測到 Exchange 伺服器，或如果您想要使用不同的伺服器，請選取 **指定執行 Exchange 2013 CAS 或 Exchange 2016 的伺服器**，然後指定 Exchange 信箱伺服器的內部 FQDN。

7.  在 **\[Office 365 Exchange Online\]** 區段中，選取 **Microsoft Office 365**，然後按一下 **\[下一步\]**。

8.  在 \[**認證**\] 頁面上的 \[**輸入內部部署帳戶認證**\] 區段中，選取 \[**使用目前的 Windows 認證**\] 讓精靈使用您登入的帳戶存取您的內部部署 Active Directory 和 Exchange 伺服器。若要指定一組不同的認證，請取消選取「**使用目前的 Windows 認證**」，並指定您想要使用的 Active Directory 帳戶的使用者名稱和密碼。無論選擇何者，您使用的帳戶必須是 Enterprise Admins 安全性群組的成員。

9.  在 \[**輸入您的 Office 365**\] 認證區段中，指定具有全域管理員權限的 Office 365 帳戶使用者名稱和密碼。按 **\[下一步\]**。

10. 在 \[**驗證連線和認證**\] 頁面上，精靈會連線到您的內部部署組織和您的 Office 365 組織，以驗證認證並檢查這兩個組織目前的設定。完成後按 **\[下一步\]**。

11. 在 **\[混合網域\]** 上，選取您想要包含在混合式部署中的網域。在大部分的部署中，您可以將每個網域的 **\[自動探索\]** 欄位設定為 **\[否\]**。唯有需要強制精靈使用特定網域的自動探索資訊時，才在網域旁選取 **\[是\]**。按 **\[下一步\]**。
    
    <table>
    <colgroup>
    <col style="width: 100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><img src="images/JJ906432.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>當您執行混合組態精靈時，精靈中的這個網域選取步驟不一定會出現。<br />
    下列情況不會出現這個步驟：
    <ul>
    <li><p>您只新增一個內部部署公認的網域至 Office 365 租用戶。由於這是唯一可供混合部署組態使用的網域，因此會自動選取此網域，並且略過精靈中的這個步驟。</p></li>
    <li><p>未將任何內部部署公認的網域新增至 Office 365 租用戶。在此情況下，您會收到錯誤，並且至少需要新增一個網域至 Office 365 租用戶才能繼續。您可以使用 Office 365 管理入口網站或選擇性地在內部部署組織中設定 Active Directory Federation Services (AD FS)，藉此執行上述操作。</p></li>
    </ul>
    如果您已新增多個內部部署公認的網域至 Office 365 租用戶，這個步驟就會出現。</td>
    </tr>
    </tbody>
    </table>


12. 在 \[**同盟信任**\] 頁面上，按一下 **\[啟用\]**，然後按一下 **\[下一步\]**。

13. 在 \[**網域所有權**\] 頁面上，按一下 **\[按一下以複製到剪貼簿\]**，複製您所選取要包含在混合部署中之網域的網域證明 Token 資訊。開啟文字編輯器 (例如 \[記事本\])，並貼上這些網域的 Token 資訊。繼續執行混合組態精靈之前，您必須使用這項資訊為公用 DNS 中的每個網域建立 TXT 記錄。如需如何將 TXT 記錄新增至 DNS 區域的相關資訊，請參閱您 DNS 主機的 \[說明\]。建立 TXT 記錄並複寫 DNS 記錄之後，按 **\[下一步\]**。

14. 在 \[**傳輸憑證**\] 頁面上的 **選取參考伺服器** 欄位，選取擁有先前在檢查清單中設定的憑證的 Exchange 伺服器。

15. 在 \[**選取憑證**\] 欄位中，選取用於安全郵件傳輸的憑證。此清單會顯示上一個步驟中所選取之信箱伺服器上安裝的協力廠商憑證授權單位 (CA) 發行的數位憑證。按 **\[下一步\]**。

16. 在 \[**組織 FQDN**\] 頁面上，針對網際網路對向的 Exchange 伺服器，輸入可從外部存取的 FQDN。Office 365 中的 EOP 服務會使用此 FQDN 設定 Exchange 組織之間安全郵件傳輸所使用的服務連接器。例如，輸入「mail.contoso.com」。按 **\[下一步\]**。

17. 混合部署組態選項已經過更新，而且您已準備好開始進行 Exchange 服務變更和混合部署組態。按一下 \[更新\] 以啟動組態程序。混合組態程序執行時，此精靈會在更新過程中顯示正在設定混合部署的功能和服務範圍。

18. 精靈會顯示完成訊息，且會顯示 **\[關閉\]** 按鈕。按一下 **\[關閉\]**，完成混合式部署設定程序並關閉精靈。

## 設定 Exchange 與 Exchange Online 組織之間的 OAuth 驗證

對於混合的 Exchange 2013/2010 和 Exchange 2013/2007 混合式部署，Office 365 與內部部署 Exchange 組織之間的新的混合式部署 OAuth 型驗證連線，並不是由混合組態精靈來設定。依預設，這些部署會繼續使用同盟信任程序。不過，只有利用新的 Exchange OAuth 驗證通訊協定，才能完整取得某些 Exchange 2013 功能，例如郵件記錄管理 (MRM)、Exchange 就地封存和就地 eDiscovery。對於想要在新的混合式部署中以 Exchange Online 來實作這些功能的所有混合的 Exchange 2013/2010 和 Exchange 2013/2007 組織，建議在使用混合組態精靈來設定混合式部署之後，設定 Exchange OAuth 驗證。

如需詳細的設定步驟，請參閱＜[設定 Exchange 與 Exchange Online 組織之間的 OAuth 驗證](https://technet.microsoft.com/zh-tw/library/dn594521\(v=exchg.150\))＞

如需有關使用 OAuth 驗證的 Exchange 安全性和符合性功能的詳細資訊，請參閱：

  - [在 Exchange 混合式部署中使用 OAuth 驗證來支援封存](https://technet.microsoft.com/zh-tw/library/dn689104\(v=exchg.150\))

  - [在 Exchange 混合式部署中使用 OAuth 驗證來支援 eDiscovery](https://technet.microsoft.com/zh-tw/library/dn497703\(v=exchg.150\))

## 如何知道這是否正常運作？

成功完成混合組態精靈，就表示完成的混合組態步驟如預期般運作。

若要進一步確認您已成功建立和設定混合部署，請執行下列動作：

  - 在內部部署組織的 Exchange 管理命令介面中執行下列命令。這個命令會顯示混合部署組態的值和設定、混合功能及傳輸端點。確認這些值正確無誤。
    
        Get-HybridConfiguration

  - 藉由檢查混合組態記錄檔的方式，確認混合組態精靈已完成全部的組態步驟。根據預設，記錄檔位於內部部署信箱伺服器上的 C:\\Program Files\\Microsoft\\Exchange Server\\V15\\Logging\\Update-HybridConfiguration 中。

  - 將現有的內部部署信箱移至 Exchange Online 組織來測試信箱移動功能支援，或在 Exchange Online 組織中建立新的使用者信箱來測試兩個組織之間的空閒/忙碌行事曆共用。上述任一個信箱動作都可讓您測試和確認內部部署與 Exchange Online 組織之間現有信箱的郵件傳遞正常運作，而且郵件傳遞受到安全保護並視為 Exchange 組織的內部郵件。
    
      - 使用 EAC 並且瀏覽至 \[企業版\] \> \[收件者\] \> \[信箱\]，可在 Exchange Online 中建立新的遠端信箱。
    
      - 使用 EAC 並且瀏覽至 \[Office 365\] \> \[收件者\] \> \[移轉\]，可將現有信箱移至 Exchange Online。

