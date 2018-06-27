---
title: '郵件流程或傳輸規則: Exchange 2013 Help'
TOCTitle: 郵件流程規則 （傳輸規則）
ms:assetid: c3d2031c-fb7b-4866-8ae1-32928d0138ef
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd351127(v=EXCHG.150)
ms:contentKeyID: 50474147
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 郵件流程或傳輸規則

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2017-04-28_

您可以使用 \[郵件流程規則 （也稱為傳輸規則） 來識別和流程透過Exchange 2013組織的郵件採取動作。郵件流程規則就類似於Outlook和Outlook Web App中可用的收件匣規則。主要差異在於郵件流程規則採取動作的郵件不斷活躍傳輸，並不之後將郵件傳遞至信箱。郵件流程規則包含更豐富一組條件、 例外狀況和動作\]，可提供讓您實作許多類型的郵件原則的彈性。

本文說明郵件流程規則的元件和它們的運作方式。

如需Exchange Online中的郵件流程規則，請參閱[Exchange Online 中的郵件流程規則 (傳輸規則)](https://technet.microsoft.com/zh-tw/library/jj919238\(v=exchg.150\))。Exchange Online Protection中的郵件流程規則的相關資訊，請參閱[Exchange Online Protection 中的郵件流程規則 (傳輸規則)](https://technet.microsoft.com/zh-tw/library/dn271424\(v=exchg.150\))

您可以使用Exchange 系統管理中心 (EAC) 或Exchange 管理命令介面來管理郵件流程規則。如需如何管理傳輸規則，請參閱[管理郵件流程規則](manage-mail-flow-rules-exchange-2013-help.md)指示。

針對每個規則，您可以選擇強制執行規則、測試規則，或測試規則並通知寄件者。若要深入了解測試選項，請參閱＜[測試郵件流程規則](test-a-mail-flow-rule-exchange-2013-help.md)＞和＜[原則提示](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md)＞。

若要使用郵件流程規則實作特定的訊息原則，請參閱下列主題︰

  - [使用傳輸規則檢查郵件附件](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md)

  - [常見的附件封鎖案例](common-attachment-blocking-scenarios-for-mail-flow-rules-exchange-2013-help.md)

  - [整個組織的免責聲明、簽章、頁尾或標頭](organization-wide-disclaimers-signatures-footers-or-headers-exchange-online-help.md)

  - [使用郵件流程規則讓郵件可以略過雜亂](use-mail-flow-rules-so-messages-can-bypass-clutter-exchange-2013-help.md)

  - [使用清單中的文字、 片語或模式為基礎的路由電子郵件的郵件流程規則](use-mail-flow-rules-to-route-email-based-on-a-list-of-words-phrases-or-patterns-exchange-2013-help.md)

  - [常見的郵件核准案例](common-message-approval-scenarios-exchange-2013-help.md)

## 郵件流程規則元件

郵件流程規則會進行的條件、 例外狀況、 動作和屬性：

  - **條件** 識別您要套用動作的郵件。有些條件會檢查郵件標頭欄位 (例如 \[收件者\]、\[寄件者\] 或 \[副本\] 欄位)。有些條件則會檢查郵件屬性 (例如郵件主旨、內文、附件、郵件大小或郵件分類)。在使用大部分的條件時，您都必須指定比較運算子 (例如等於、不等於或包含) 以及要比對的值。如果沒有條件或例外狀況，則規則會套用至所有郵件。
    
    如需Exchange 2013中的郵件流程規則條件的詳細資訊，請參閱[傳輸規則條件 （述詞）](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)。

  - **例外狀況** 選擇性地識別不應該套用動作的郵件。可在條件中使用的訊息識別碼也可用於例外狀況。例外狀況可覆寫條件並防止規則動作套用到郵件，即使郵件符合所有設定的條件也是如此。

  - **動作** 指定對於符合規則中的條件，但不符合任何例外狀況的郵件，所應採取的動作。有許多動作可用，例如，拒絕、刪除或重新導向郵件、新增其他收件者、在郵件主旨中新增前置詞，或是將免責聲明插入郵件內文。
    
    如需Exchange 2013中的郵件流程規則動作的詳細資訊，請參閱[傳輸規則動作](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md)。

  - **屬性** 指定其他不是條件、例外狀況或動作的規則設定。例如，何時應套用規則、是否強制執行或測試規則，以及規則作用中的時間週期。
    
    如需詳細資訊，請參閱本主題中的 \[郵件流程規則屬性\] 區段。

## 多個條件、例外狀況和動作

下表顯示規則中如何處理多個條件、條件值、例外狀況和動作。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>元件</th>
<th>邏輯</th>
<th>註解</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>多個條件</p></td>
<td><p>AND</p></td>
<td><p>郵件必須符合規則中的所有條件。如果您需要符合一個條件或另一個條件，請對每一個條件使用不同的規則。例如，若要將相同的免責聲明新增至附件和內容包含特定文字的郵件，請為每一個條件建立一個規則。在 EAC 中，您可以輕易地複製規則。</p></td>
</tr>
<tr class="even">
<td><p>具有多個值的一個條件</p></td>
<td><p>OR</p></td>
<td><p>有些條件允許您指定多個值。郵件必須符合任何一個 (而非全部) 指定的值。例如，如果電子郵件的主旨為<strong>股票價格資訊</strong>，而 <strong>[主旨包含任何這些字詞]</strong> 條件設定為符合 <strong>Contoso</strong> 或<strong>股票</strong>這些字，則此電子郵件滿足該條件，因為主旨至少包含其中一個指定的值。</p></td>
</tr>
<tr class="odd">
<td><p>多個例外狀況</p></td>
<td><p>OR</p></td>
<td><p>如果郵件符合任何例外狀況，則動作不會套用到郵件。郵件不必符合所有例外狀況。</p></td>
</tr>
<tr class="even">
<td><p>多個動作</p></td>
<td><p>AND</p></td>
<td><p>符合規則條件的郵件可取得規則中指定的所有動作。例如，如果選取 [在郵件主旨前面加上] 和 [新增收件者到 [密件副本] 方塊] 動作，則兩個動作都會套用至郵件。</p>
<p>請記住，某些動作 (例如，<strong>[刪除郵件而不通知任何人]</strong> 動作) 會阻止後續規則套用至郵件。其他動作 (例如 <strong>[轉寄郵件]</strong>) 則不允許額外的動作。</p>
<p>您也可以在規則上設定動作，以便在套用該規則時，不要將後續的規則套件到郵件。</p></td>
</tr>
</tbody>
</table>


返回頁首

## 郵件流程規則屬性

下表說明郵件流程規則中可用的規則屬性。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>EAC 中的屬性名稱</th>
<th>PowerShell 中的參數名稱</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>優先順序</strong></p></td>
<td><p><em>Priority</em></p></td>
<td><p>表示規則套用到郵件的順序。預設優先順序是以規則的建立時間為基礎 (較舊規則的優先順序高於較新的規則，而較高優先順序的規則會在較低優先順序的規則之前處理)。</p>
<p>您可以在規則清單中向上或向下移動規則，以變更 EAC 中的規則優先順序。在 PowerShell 中，您可設定優先順序號碼 (0 為最高優先順序)。</p>
<p>例如，如果有一個規則是拒絕含有信用卡號碼的郵件，而另一個規則是需要核准，則您一定希望先執行拒絕規則，並停止套用其他規則。</p>
<p>如需詳細資訊，請參閱<a href="manage-mail-flow-rules-exchange-2013-help.md">設定郵件流程規則的優先順序</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>模式</strong></p></td>
<td><p><em>Mode</em></p></td>
<td><p>您可以指定是否要讓規則立即開始處理郵件，或您是否想要測試規則，而不影響郵件傳遞 (不論是否有資料遺失防護或 DLP 原則提示)。</p>
<p>原則提示可在 Outlook 或 網頁型 Outlook 中呈現簡短附註，以提供可能原則違規的相關資訊給正在建立郵件的人員。如需詳細資訊，請參閱<a href="technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md">原則提示</a>。</p>
<p>如需模式的詳細資訊，請參閱＜<a href="test-a-mail-flow-rule-exchange-2013-help.md">測試郵件流程規則</a>＞。</p></td>
</tr>
<tr class="odd">
<td><p><strong>於下列日期啟用此規則</strong></p>
<p><strong>於下列日期停用此規則</strong></p></td>
<td><p><em>ActivationDate</em></p>
<p><em>ExpiryDate</em></p></td>
<td><p>指定規則的有效日期範圍。</p></td>
</tr>
<tr class="even">
<td><p>已選取或未選取 [開啟] 核取方塊</p></td>
<td><p>新規則：<strong>New-TransportRule</strong> Cmdlet 上的 <em>Enabled</em> 參數。</p>
<p>現有規則：使用 <strong>Enable-TransportRule</strong> 或 <strong>Disable-TransportRule</strong> Cmdlet。</p>
<p>此值會顯示在規則的 <strong>State</strong> 屬性中。</p></td>
<td><p>您可以建立已停用的規則，而在您準備進行測試時加以啟用。或者，您可以在不刪除規則的情況下進行停用，以保留設定。</p></td>
</tr>
<tr class="odd">
<td><p><strong>如果無法完成規則處理時便順延郵件</strong></p></td>
<td><p><em>RuleErrorAction</em></p></td>
<td><p>您可以指定如果無法完成規則處理時，應該如何處理郵件。預設會忽略此規則，但您可以選擇重新提交郵件進行處理。</p></td>
</tr>
<tr class="even">
<td><p><strong>符合郵件中的寄件者地址</strong></p></td>
<td><p><em>SenderAddressLocation</em></p></td>
<td><p>如果此規則使用可檢查寄件者電子郵件地址的條件或例外狀況，您可以查看郵件標頭、郵件信封或這兩者的值。</p></td>
</tr>
<tr class="odd">
<td><p><strong>停止處理其他規則</strong></p></td>
<td><p><em>SenderAddressLocation</em></p></td>
<td><p>這是適用於規則的動作，但它看起來像是 EAC 中的屬性。您可以選擇在規則處理郵件之後，停止將其他規則套用至郵件。</p></td>
</tr>
<tr class="even">
<td><p><strong>註解</strong></p></td>
<td><p><em>Comments</em></p></td>
<td><p>您可以輸入有關規則的描述性註解。</p></td>
</tr>
</tbody>
</table>


返回頁首

## 郵件流程規則如何套用至郵件

經過您組織的所有郵件都會根據組織已啟用的郵件流程規則來進行評估。規則會依 EAC 的 \[郵件流程\] \> \[規則\] 頁面所列出的順序來處理，或根據 PowerShell 中對應的 *Priority* 參數值來處理。

每個規則也提供選項可於符合規則時停止處理其他規則。對於符合多個郵件流程規則中條件的郵件而言，此設定很重要 (您想要將哪個規則套用到郵件？全部？僅只一個？）。

## 郵件類型引發的處理差異

通過組織的郵件有幾種類型。下表顯示郵件流程規則可處理的郵件類型。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>郵件類型</th>
<th>可以套用規則嗎?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>一般郵件</strong>   包含單一 RTF 格式 (RTF)、HTML 或純文字郵件內文的郵件，或包含一組多部分或替代郵件內文的郵件。</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><strong>Office 365 郵件加密</strong>    Office 365 中 Office 365 郵件加密 所加密的郵件。如需詳細資訊，請參閱 <a href="https://go.microsoft.com/fwlink/p/?linkid=392525">Office 365 郵件加密</a>。</p></td>
<td><p>規則永遠可以存取信封標頭，並根據可檢查這些標頭的條件來處理郵件。</p>
<p>如需可檢查或修改加密郵件內容的規則，您必須確認已啟用傳輸解密 (強制或選擇性；預設值是選擇性)。如需詳細資訊，請參閱<a href="https://go.microsoft.com/fwlink/p/?linkid=848060">啟用或停用傳輸解密</a>。</p>
<p>您也可以建立規則以自動解密加密的郵件。如需詳細資訊，請參閱<a href="http://go.microsoft.com/fwlink/p/?linkid=402846">定義將電子郵件加密或解密的規則</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>S/MIME 加密的郵件</strong></p></td>
<td><p>規則只可以存取信封標頭，並根據可檢查這些標頭的條件來處理郵件。</p>
<p>無法處理具有需要檢查郵件內容之條件的規則，或具有可以修改郵件內容之動作的規則。</p></td>
</tr>
<tr class="even">
<td><p><strong>RMS 保護的訊息</strong>   已套件 Active Directory Rights Management Services(AD RMS) 或 Azure 版權管理 (RMS) 原則的郵件。</p></td>
<td><p>規則永遠可以存取信封標頭，並根據可檢查這些標頭的條件來處理郵件。</p>
<p>如需可檢查或修改 RMS 保護之郵件內容的規則，您必須確認已啟用傳輸解密 (強制或選擇性；預設值是選擇性)。如需詳細資訊，請參閱<a href="https://go.microsoft.com/fwlink/p/?linkid=848060">啟用或停用傳輸解密</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>明文簽章的郵件</strong>   已簽署但未加密的郵件。</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><strong>UM 郵件</strong>   由整合通訊服務建立或處理的郵件 (如語音信箱、傳真、未接來電通知)，以及使用 Microsoft Outlook 語音存取 建立或轉寄的郵件。</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><strong>匿名郵件</strong>   匿名寄件者所傳送的郵件。</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><strong>讀取報告</strong>   為了回應寄件者的索取讀信回條而產生的報告。讀取內含 <code>IPM.Note*.MdnRead</code> 或 <code>IPM.Note*.MdnNotRead</code> 之郵件類別的報告。</p></td>
<td><p>是</p></td>
</tr>
</tbody>
</table>


## 傳輸規則和群組成員資格

當您使用可展開通訊群組成員資格的條件來定義傳輸規則時，套用規則之信箱伺服器的傳輸服務就會快取最後的收件者清單。此項目亦稱為 *\[擴充的群組快取\]*，而日誌代理程式也會使用此快取來評估日誌規則的群組成員資格。預設情況下，擴充的群組快取會存放群組成員資格達四小時。同時也會存放由動態通訊群組之收件者篩選器所傳回的收件者。擴充的群組快取會重複來回於 Active Directory，造成一直進行不必要的群組成員資格解析動作而產生更多網路流量。

在 Exchange 2013 中，您可以設定此間隔時間，與其他與擴充的群組快取相關的參數。您可以降低快取到期間隔時間，或是一起停用快取，確保能更頻繁地重新整理群組成員資格。您必須針對通訊群組擴充查詢，計劃來增加 Active Directory 網域控制站的負載能力。您也可以重新啟動此伺服器上的 Microsoft Exchange 傳輸服務，以便清除信箱伺服器上的快取。在想要清除快取的每一台信箱伺服器上，您必須執行這項動作。依據通訊群組成員資格來建立、測試與疑難排解使用條件的傳輸規則時，您必須同時考量擴充的群組快取之影響。

## 規則儲存和複寫

建立及設定 Mailbox server 上的郵件流程規則會儲存在Active Directory，與它們讀取，而且套用的組織中所有 Mailbox server 上的傳輸服務。當您建立、 修改或移除郵件流程規則時，變更為您組織中的網域控制站之間複寫。這可讓Exchange整個組織提供一組連續的郵件流程規則。

**附註：**

  - 網域控制站之間複寫不控制由Exchange （例如Active Directory網站數目、） 和網路連結速度的因素而定。因此，您需要在組織中實作郵件流程規則時，請考慮複寫延遲。如需Active Directory複寫的詳細資訊，請參閱 ＜ [Active Directory 複寫及拓撲管理使用 Windows PowerShell 簡介](https://go.microsoft.com/fwlink/p/?linkid=274904)。

  - 每部信箱伺服器快取以避免重複的Active Directory查詢，以決定群組的成員資格的擴充的通訊群組。根據預設，在擴充的群組快取的項目過期取決每隔四個小時。因此，群組的成員資格變更未偵測到的郵件流程規則更新擴充的群組快取之前。若要在信箱伺服器上強制快取立即更新，請重新啟動Microsoft Exchange Transport 服務。您需要重新啟動每個您要強制更新快取的信箱伺服器上的服務。

建立及設定 Edge Transport server 上的郵件流程規則會儲存在伺服器上本機 AD LDS 的執行個體。郵件流程規則沒有自動的複寫發生 Edge Transport server 上。Edge Transport server 上的規則只適用於透過本機伺服器的流程的郵件。如果您需要將多個 Edge Transport server 上套用相同的郵件流程規則集，您可以複製 Edge Transport server 的組態，或匯出及匯入的郵件流程規則。如需詳細資訊，請參閱[Edge Transport server 複製的組態](edge-transport-server-cloned-configuration-exchange-2013-help.md)和[匯入或匯出郵件流程規則集合](manage-mail-flow-rules-exchange-2013-help.md)。

每當 Mailbox server 或 Edge Transport server 上的傳輸服務會偵測已修改的郵件流程規則、 事件會記錄在事件檢視器 （事件識別碼 4002 在 Mailbox server 及 Edge Transport server 上的事件識別碼 16028） 的應用程式記錄檔。

## 混合環境中的規則複寫與儲存

有兩種常見在Exchange 2013的混合式的環境案例：

  - **貴組織的一部分所在UNRESOLVED\_TOKEN\_VAL(Office365)的混合部署**
    
    在混合環境中有無複寫的內部Exchange組織與UNRESOLVED\_TOKEN\_VAL(Office365)之間的規則。因此，當您在Exchange建立規則，您需要在UNRESOLVED\_TOKEN\_VAL(Office365)中建立對應的規則。UNRESOLVED\_TOKEN\_VAL(Office365)中建立的規則會儲存在雲端，而您在內部部署組織中建立規則會儲存在本機上在Active Directory。當您管理在混合環境中的規則時，您需要進行同步處理的這兩個上的芳鄰\] 中所做的變更或一個環境中所做的變更與然後匯出規則及匯入他們在其他環境中的規則兩組。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>即使沒有明顯的重疊的條件和UNRESOLVED_TOKEN_VAL(Office365)和Exchange Server中可用的動作，有差異。如果您打算在兩個位置中建立的相同規則，請確定所有條件和動作您打算使用都所提供。若可用條件和動作UNRESOLVED_TOKEN_VAL(Office365)中可用的清單，請參閱下列主題：<br />
    <a href="https://technet.microsoft.com/zh-tw/library/jj919235(v=exchg.150)">Exchange Online 中的郵件流程規則條件和例外狀況 (predicates)</a><br />
    <a href="https://technet.microsoft.com/zh-tw/library/jj919237(v=exchg.150)">郵件流程規則動作在 Exchange Online</a></td>
    </tr>
    </tbody>
    </table>


  - **Exchange 2010或Exchange 2007與共存**
    
    當您與Exchange 2010或Exchange 2007共存時，所有的郵件流程規則儲存在Active Directory ，而且複製整個組織，不論您用來建立規則Exchange Server版本。不過，郵件流程的所有規則都相關聯之Exchange Server伺服器版本用來建立，而且都會儲存在特定版本容器中Active Directory。當您先在組織中部署Exchange 2013時，任何現有的規則會匯入Exchange 2013安裝程序的一部分。不過，任何變更之後會需要進行這兩個版本。例如，如果您變更Exchange 2013 （Exchange 管理命令介面或 EAC） 中現有的規則，您需要Exchange 2010 （Exchange 管理命令介面或UNRESOLVED\_TOKEN\_VAL(exEMC)） 中進行相同變更。或者，您可以從Exchange 2013匯出規則並匯入Exchange 2010。
    
    Exchange 2010無法處理**版本**或**RuleVersion**值 15 的規則。*n*.*n*.*n*. 並且確定您的所有規則可進行處理，請僅使用值 14 規則。*n*.*n*.*n*.

## 相關資訊

[管理郵件流程規則](manage-mail-flow-rules-exchange-2013-help.md)

[傳輸規則條件 （述詞）](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

[傳輸規則動作](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md)

[傳輸代理程式](transport-agents-exchange-2013-help.md)

