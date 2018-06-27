---
title: 'Exchange 2013 版本資訊: Exchange 2013 Help'
TOCTitle: Exchange 2013 版本資訊
ms:assetid: 1879fd5e-3d63-4264-9cc2-9c050c6ab3c5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ150489(v=EXCHG.150)
ms:contentKeyID: 50472640
ms.date: 04/18/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 版本資訊

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2018-04-16_

歡迎使用 Microsoft Exchange Server 2013！本主題包含成功部署 Exchange 2013 所需了解的重要資訊。請在開始部署之前，仔細閱讀本主題。

本主題包含下列各節：

  - 安裝與部署

  - Exchange 管理命令介面

  - 信箱

  - 公用資料夾

  - 郵件流程

  - 用戶端連線

  - Exchange 2010 共存

## 安裝與部署

  - **msExchProductId 並不會反映安裝的 Exchange 2013 版本** 在 Exchange 擴充 Active Directory 結構描述並準備適用於 Exchange 的 Active Directory 之後，數個屬性已更新以顯示準備完成。其中一個屬性是 `Configuration` 命名內容中 `CN=<your organization>, CN=Microsoft Exchange, CN=Services, CN=Configuration, DC=<domain>` 容器下的 *msExchangeProductId*。如果您正在安裝的 Exchange 2013 版本中沒有引入 Active Directory 結構描述變更，則這個屬性不會更新，或可能會顯示未預期的值。如果值不符合正在安裝的 Exchange 2013 版本，可能會造成混淆。
    
    這是預期的行為，因 *msExchProductId* 的值並不會反映正在安裝的 Exchange 2013 版本。這個屬性會反映上次對 Active Directory 結構描述進行變更的 Exchange 2013 版本。若要避免混淆，建議您依循 [準備 Active Directory 及網域](prepare-active-directory-and-domains-exchange-2013-help.md) 中[如何了解這可否運作？](prepare-active-directory-and-domains-exchange-2013-help.md)一節的步驟，以確認 Active Directory 已更新，且已就緒適用於正在安裝的 Exchange 2013 版本。

  - **安裝程式不正確地要求 .NET Framework 4.0**   如果您嘗試安裝 Exchange 2013，但電腦上未安裝 .NET Framework，安裝程式會不正確地要求您安裝 .NET Framework 4.0，但事實上需要 .NET Framework 4.5 或更新的版本。
    
    若要解決此問題，請安裝 .NET Framework 4.5 或更新的版本。您不需要安裝 .NET Framework 4.0。如需必要條件的完整清單，請參閱＜[Exchange 2013 必要條件](exchange-2013-prerequisites-exchange-2013-help.md)＞。

  - **在累計更新安裝期間會覆寫 Exchange XML 應用程式組態檔**   在您安裝 Exchange 累計更新或 Service Pack 後，將會覆寫您在 Exchange XML 應用程式組態檔 (例如 Client Access Server 上的 web.config 檔案，或信箱伺服器上的 EdgeTransport.exe.config 檔案) 中任何自訂的個別伺服器設定。請務必儲存此資訊，以便安裝後能輕易地重新設定伺服器。在安裝 Exchange 累計更新或 Service Pack 後，您必須重新配置這些設定。

  - **使用委派管理權限來安裝 Exchange 會造成安裝程式失敗** 當只屬於 Delegated Setup 角色群組成員的使用者嘗試在預先佈建的伺服器上安裝 Exchange 時，安裝程式會失敗。之所以發生此情況，是因為 Delegated Setup 群組缺少必要權限，因此無法在 Active Directory 中建立和設定某些物件。
    
    若要解決此問題，請執行下列其中一個動作：
    
      - 將安裝 Exchange 的使用者新增至 Domain Admins Active Directory 安全性群組。
    
      - 讓屬於 Organization Management 角色群組成員的使用者負責安裝 Exchange。

如需如何安裝 Exchange 2013 的詳細資訊，請參閱＜[規劃及部署](planning-and-deployment-for-exchange-2013-installation-instructions.md)＞。

## Exchange 管理命令介面

  - **命令介面意外載入 Exchange 2007 或 Exchange 2010 Cmdlet** 先前，開啟 Exchange 2013 伺服器上的命令介面會導致命令介面啟動連線至本機伺服器或另一部執行 Exchange 2013 的伺服器。連線後會載入 Exchange 2013 Cmdlet。從 Exchange 2013 CU11 開始，命令介面將連線到登入的使用者信箱所在的 Exchange 伺服器。如果登入的使用者沒有信箱，命令介面會連線到 SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c} 仲裁信箱所在的伺服器。目標伺服器可以是 Exchange 任何支援的版本。這代表如果登入的使用者信箱 (或是仲裁信箱，如果使用者沒有信箱) 位於 Exchange 2010 伺服器上，命令介面就會連線到該伺服器並載入 Exchange 2010 Cmdlet。這可防止您執行某些工作，因為 Exchange 2010 Cmdlet 無法管理 Exchange 2013 組態或伺服器。
    
    從 Exchange 2013 CU11 開始，這種方式是經過設計的。若要確保命令介面載入 Exchange 2013 Cmdlet，請將登入使用者的信箱移至 Exchange 2013。如果登入的使用者沒有信箱，將 SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c} 仲裁信箱移至 Exchange 2013 伺服器。
    
    關於如何移動仲裁信箱的詳細資訊，請參閱 Exchange 團隊部落格上的＜[Exchange 管理命令介面和信箱錨定](https://go.microsoft.com/fwlink/?linkid=717722)＞。

## 信箱

  - **執行不同 Exchange 版本的信箱伺服器可以新增至相同的資料庫可用性群組** **Add-DatabaseAvailabilityGroupServer** Cmdlet 和 Exchange 系統管理中心錯誤地讓 Exchange 2013 伺服器可以新增至以 Exchange 2016 為基礎的資料庫可用性群組 (DAG)，反之亦然。Exchange 只支援將執行相同版本 (例如，Exchange 2013 或 Exchange 2016) 的信箱伺服器新增至 DAG。此外，Exchange 系統管理中心會在可供新增至 DAG 的伺服器清單中同時顯示 Exchange 2013 和 Exchange 2016 伺服器。這可能會讓系統管理員不經意地將執行不相容 Exchange 版本的伺服器新增至 DAG (例如，將 Exchange 2013 伺服器新增至以 Exchange 2016 為基礎的 DAG)。
    
    此問題目前沒有解決方法。系統管理員在將信箱伺服器新增至 DAG 時，必須自己注意這個問題。只將 Exchange 2013 伺服器新增至以 Exchange 2013 為基礎的 DAG，以及只將 Exchange 2016 伺服器新增至以 Exchange 2016 為基礎的 DAG。您可以查看 Exchange 系統管理中心之伺服器清單中的**版本**資料行，以分辨 Exchange 的各個版本。以下是 Exchange 2013 和 Exchange 2016 的伺服器版本：
    
      - **Exchange 2013** 15.0 (組建 xxx.xx)
    
      - **Exchange 2016** 15.1 (組建 xxx.xx)

  - **從舊版 Exchange 移轉時信箱變大**   當您將信箱從舊版 Exchange 移至 Exchange 2013 時，回報的信箱大小可能會增加 30% 至 40%。信箱資料庫使用的磁碟空間尚未增加，僅增加每一個信箱使用的空間屬性。信箱大小的增加是由於所有項目內容加入配額計算中，為其信箱中的項目所耗用的空間提供更精確的計算。此增量可能會造成當信箱移至 Exchange 2013 時，部分使用者超出其信箱大小配額。
    
    若要避免使用者超出信箱大小配額，請增加資料庫或信箱配額值，以符合新的配額計算。若要設定資料庫或信箱配額值，請在 **Set-MailboxDatabase** 與**Set-Mailbox**指令程式上，分別使用 *IssueWarningQuota*、*ProhibitSendQuota*，以及 *ProhibitSendReceiveQuota* 參數。

  - **Outlook 2007 和 Outlook 2010 用戶端可能無法下載離線通訊錄**   如果無法從網際網路存取離線通訊錄 (OAB) 內部 URL，則 Outlook 2007 和 Outlook 2010 用戶端可能無法下載 OAB。
    
    若要解決 Outlook 2007 和 Outlook 2010 用戶端的這個問題，請開放 OAB 內部 URL 供網際網路存取。此問題不影響 Outlook 2013。

  - **將 Exchange 2013 安裝在現有的 Exchange 組織，可能導致所有用戶端下載 OAB**   將第一部 Exchange 2013 伺服器安裝至現有的 Exchange 2007 或 Exchange 2010 組織，可能導致組織中的所有用戶端下載新的 OAB 副本，因而發生網路飽和及伺服器效能問題。發生此問題的原因為 Exchange 2013 在組織中建立新的預設 OAB，取代 Exchange 2007 或 Exchange 2010 OAB。信箱若未被指派特定 OAB，或位於未指派特定 OAB 的信箱資料庫中，將下載新的預設 OAB。
    
    若要防止用戶端在 Exchange 2013 安裝時下載新的 OAB 副本，請將 OAB 指派給每一個信箱或信箱所在的信箱資料庫。此動作必須在 Exchange 2013 安裝在組織之前完成。

  - **使用者可能路由傳送到不負責所要求 OAB 的 OAB 產生信箱**   Exchange 2013 CU5 和較新的 CU 已變更 OAB 如何連結至 OAB 產生信箱。此變更可將使用者路由傳送到不負責使用者所要求之 OAB 的 OAB 產生信箱。當下列條件全部成立時，就會發生此情況：
    
      - 您的組織中有一個以上的 OAB 產生信箱。
    
      - 請先升級主控 OAB 產生信箱的 Mailbox Server，然後再升級 Client Access Server。
    
      - 您將 Exchange 2013 伺服器從 CU5 以前的版本升級到較新的版本 (例如，從 Exchange 2013 CU3 升級到 Exchange 2013 CU6)。
    
      - Client Access Server 執行 CU5 以前的版本。
    
    若要解決這個問題，請確定您先將 Client Access Server 升級到 Exchange 2013 CU6 或較新的版本，然後才升級 Mailbox Server。這樣可確保 Client Access Server 了解如何對負責產生使用者 OAB 的 OAB 產生信箱來代理要求。
    
    如需詳細了解 Exchange 2013 CU5 中的 OAB 變更，請參閱＜[Exchange 2013 累計更新 5 中的 OAB 改進](https://go.microsoft.com/fwlink/p/?linkid=400642)＞。

## 公用資料夾

  - **未經授權的寄件者不能再傳送郵件至擁有郵件功能的公用資料夾**   在 Exchange 2013 CU6 之前的版本中，未經授權的寄件者可以傳送郵件至擁有郵件功能的公用資料夾。這使得外部寄件者可傳送郵件至擁有郵件功能的公用資料夾，而不論公用資料夾上設定的權限。
    
    從 Exchange 2013 CU6 開始，如果想讓外部寄件者傳送郵件至擁有郵件功能的公用資料夾，**匿名**使用者至少必須取得**建立項目**權限。如果您已設定擁有郵件功能的公用資料夾但還未這麼做，外部寄件者將會收到傳遞失敗通知，且郵件不會傳送至擁有郵件功能的公用資料夾。
    
    您可以使用命令介面或 Outlook 設定匿名使用者的權限。若要深入了解如何設定匿名使用者的權限，請參閱＜[郵件啟用或停用郵件功能的公用資料夾](mail-enable-or-mail-disable-a-public-folder-exchange-2013-help.md)＞。

  - 可以從舊版 Exchange 伺服器移轉到 Exchange 2013 的公用資料夾數目上限為 500,000。如需公用資料夾移轉的相關資訊，請參閱＜[使用批次移轉公用資料夾從舊版移轉至 Exchange 2013](use-batch-migration-to-migrate-public-folders-to-exchange-2013-from-previous-versions-exchange-2013-help.md)＞。

## 郵件流程

  - **Client Access Server 上的 TransportAgent 指令程式需要本機 Windows PowerShell**   **\*-TransportAgent** 指令程式有問題，在 Exchange 管理命令介面中無法使用這些指令程式在 Client Access Server 上安裝、解除安裝及管理傳輸代理程式。若要在 Client Access Server 上安裝、解除安裝，以及管理傳輸代理程式，必須手動載入 ExchangeWindows PowerShell 嵌入式管理單元，然後執行 **\*-TransportAgent** 指令程式。如果您嘗試使用 Exchange 管理命令介面安裝、解除安裝，以及管理傳輸代理程式，您所做的變更將會套用至已連接的 Exchange 2013 信箱伺服器。
    
    若要在 Client Access Server 上安裝、解除安裝，以及管理傳輸代理程式，請在您想要管理的 Client Access Server 上執行下列動作：
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>不支援載入 <code>Microsoft.Exchange.Management.PowerShell.SnapIn</code>Windows PowerShell 嵌入式管理單元並執行 <strong>*-TransportAgent</strong> 指令程式以外的指令程式，可能會對您的 Exchange 部署造成無法挽回的損害。<br />
    在您想要安裝、解除安裝或管理傳輸代理程式的 Client Access Server 上，您必須是本機管理員。不支援在 Exchange 檔案、目錄或 Active Directory 物件上修改存取控制清單 (ACL)。</td>
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
    <td>僅限在 Client Access Server 上執行以下程序。如果您想要在信箱伺服器上管理傳輸代理程式，不需要載入 ExchangeWindows PowerShell 嵌入式管理單元。</td>
    </tr>
    </tbody>
    </table>
    
    1.  開啟新的 Windows PowerShell 視窗。
    
    2.  執行下列命令。
        
            Add-PSSnapin Microsoft.Exchange.Management.PowerShell.SnapIn
    
    3.  正常執行傳輸代理程式管理工作。
    
    4.  在每一個您想要管理的 Client Access Server 上重複此程序。

## 用戶端連線

  - **未加入網域的用戶端發生 NTLM 驗證失敗**   當下列條件成立時，Windows Live Mail 之類的用戶端與 Exchange 2013 之間的驗證可能會失敗：
    
      - 然後用戶端使用的驗證方法是 NTLM。
    
      - 電腦未加入網域。
    
    若要解決這個問題，您可以執行下列其中一項：
    
      - 將執行用戶端的電腦加入到網域。
    
      - 將用戶端使用的驗證類型從 NTLM 變更為透過 TLS 的基本驗證。

  - **GSSAPI 驗證用於 Send-MailMessage 指令程式時失敗**   使用 Windows PowerShell 預設安裝隨附的 **Send-MailMessage** 指令程式將經過驗證的郵件傳送至 Exchange 2013 時，一般安全性服務應用程式介面 (GSSAPI) 驗證可能會失敗。發生這種情況時，您將在接受連線的 Exchange 2013 Client Access Server 上看見 **\[應用程式\]** 事件記錄檔出現一個項目，資訊如下：
    
      - **來源**   MSExchangeFrontEndTransport
    
      - \[事件 ID\]   1035
    
      - \[描述\]   接收連接器用戶端前端 \<*伺服器名稱*\> 發生錯誤 `IllegalMessage`，造成輸入驗證失敗。驗證機制為 Gssapi。嘗試向 Exchange 驗證的用戶端本身的來源 IP 位址是 \[\<*用戶端 IP 位址*\>\]。
    
    若要解決此問題，您需要從 Exchange 2013 Client Access Server 的用戶端接收連接器移除 `Integrated` 驗證方法。若要從用戶端接收連接器移除 `Integrated` 驗證方法，請在各個 Exchange 2013 Client Access Server (從執行**Send-MailMessage** 指令程式的電腦接收連線) 上執行下列命令：
    
        Set-ReceiveConnector "<server name>\Client Frontend <server name>" -AuthMechanism Tls, BasicAuth, BasicAuthRequireTLS

  - **升級至 Exchange 2013 SP1 時，MAPI over HTTP 的效能可能會變差**   如果您從 Exchange 2013 累計更新升級至 Exchange 2013 SP1，並啟用 MAPI over HTTP，則使用此通訊協定連接到 Exchange 2013 SP1 伺服器的用戶端可能會出現效能變差的狀況。這是由於從累計更新升級至 Exchange 2013 SP1 期間未配置必要設定所致。如果您從 Exchange 2013 RTM 升級至 Exchange 2013 SP1，或是安裝新的 Exchange 2013 SP1 或更新版本的伺服器，就不會發生此問題。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>只有在 Client Access Server 上啟用了 MAPI over HTTP 通訊協定時，才會構成問題。依預設會加以停用。在停用 MAPI over HTTP 時，用戶端會改用 RPC over HTTP 通訊協定。</td>
    </tr>
    </tbody>
    </table>
    
    若要解決此問題，請執行下列動作：
    
    1.  在執行 Client Access server role 的伺服器上，使用 Windows 命令提示字元執行下列命令：
        
            set AppCmdLocation=%windir%\System32\inetsrv
            set ExchangeLocation=%ProgramFiles%\Microsoft\Exchange Server\V15
            
            %AppCmdLocation%\appcmd.exe SET AppPool "MSExchangeMapiFrontEndAppPool" /CLRConfigFile:"%ExchangeLocation%\bin\MSExchangeMapiFrontEndAppPool_CLRConfig.config"
            %AppCmdLocation%\appcmd.exe RECYCLE AppPool "MSExchangeMapiFrontEndAppPool"
    
    2.  在執行 Mailbox server role 的伺服器上，使用 Windows 命令提示字元執行下列命令：
        
            set AppCmdLocation=%windir%\System32\inetsrv
            set ExchangeLocation=%ProgramFiles%\Microsoft\Exchange Server\V15
            
            %AppCmdLocation%\appcmd.exe SET AppPool "MSExchangeMapiMailboxAppPool" /CLRConfigFile:"%ExchangeLocation%\bin\MSExchangeMapiMailboxAppPool_CLRConfig.config"
            %AppCmdLocation%\appcmd.exe RECYCLE AppPool "MSExchangeMapiMailboxAppPool"
            
            %AppCmdLocation%\appcmd.exe SET AppPool "MSExchangeMapiAddressBookAppPool" /CLRConfigFile:"%ExchangeLocation%\bin\MSExchangeMapiAddressBookAppPool_CLRConfig.config"
            %AppCmdLocation%\appcmd.exe RECYCLE AppPool "MSExchangeMapiAddressBookAppPool"

## Exchange 2010 共存

  - **當透過 Exchange 2013 Client Access Server 進行 Proxy 處理時，存取 Exchange 2010 信箱的要求可能無法運作**   在某些情況中，未安裝任何更新彙總套件的 Exchange 2013 和 Exchange 2010 Service Pack 3 (SP3) Client Access Server 之間的 Proxy 要求可能無法正常運作，且會出現錯誤。當下列條件全部成立時，就會發生此情況：
    
      - 具有 Exchange 2013 信箱的使用者嘗試使用下列其中一種方法來開啟 Exchange 2010 信箱：
        
          - Outlook Web App 的 **\[開啟另一個信箱\]** 選項 **-或-**
        
          - Exchange 系統管理中心的 **\[其他使用者\]** 選項
    
      - 使用者連接的 Client Access Server 正在執行 Exchange 2013。
    
      - Exchange 2010 Client Access Server 已從 Exchange 2010 的量產發行 (RTM) 版本或先前的 Exchange 2010 Service Pack 升級至 Exchange 2010 SP3。
    
    如果上述條件全部成立，則使用者將無法存取其他使用者的 Exchange 2010Outlook Web App 選項，而且可能出現空白頁面。
    
    若要解決此問題，請在各個 Exchange 2010 伺服器上安裝 Exchange 2010 SP3 更新彙總套件 1 或更新版本。

