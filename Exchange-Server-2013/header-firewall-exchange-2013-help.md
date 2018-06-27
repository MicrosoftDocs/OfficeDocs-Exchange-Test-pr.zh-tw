---
title: '標頭防火牆: Exchange 2013 Help'
TOCTitle: 標頭防火牆
ms:assetid: 9b148f7b-47a9-4379-a55b-8d5310c1772f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb232136(v=EXCHG.150)
ms:contentKeyID: 52062565
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 標頭防火牆

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

在 Microsoft Exchange Server 2013、*標頭防火牆*會為輸入及輸出郵件會移除特定的標頭欄位的機制。有兩種不同受到標頭防火牆的標頭欄位：

  - **X 標頭**  *X-header*是使用者定義、 非公務標頭\] 欄位。X-header 未特別提及 RFC 2822 之中，但開頭**X-**未定義的標頭欄位使用已經成為公認的方式將非公務標頭欄位新增至郵件。訊息應用程式，例如反垃圾郵件、 防毒軟體、 與郵件伺服器就可能會將自己 X 標題新增至郵件。在 Exchange X 標頭欄位包含的詳細資訊的動作所執行的郵件傳輸服務，例如垃圾郵件信賴等級 (SCL) 內容篩選結果和規則處理狀態。此處未經授權來源此資訊可能造成潛在安全性風險。

  - **路由標頭**  路由標頭是 RFC 2821 及 RFC 2822 中所定義的標準 SMTP 標頭欄位。路由標頭戳記訊息使用不同的郵件伺服器用來將郵件傳遞給收件者的相關資訊。插入惡意使用者的郵件的路由標頭可以顯現錯誤訊息旅行了達到收件者的路由路徑。

標頭防火牆防止這些 Exchange 相關的 X 標題詐騙來移除來自不受信任的來源輸入 Exchange 組織的內送郵件。標頭防火牆來移除外寄郵件傳送到 Exchange 組織外的受信任目的地防止這些 Exchange 相關 X 標頭的揭露。標頭防火牆也可避免詐騙的標準可用來追蹤郵件的路由歷程記錄的路由標頭。

**目錄**

Message header fields affected by header firewall in Exchange

How header firewall is applied to Receive connectors and Send connectors

Header firewall for inbound messages on Receive connectors

Header firewall for outbound messages on Send connectors

Header firewall for other message sources

Organization X-headers and forest X-headers in Exchange

## Exchange 中受到標頭防火牆影響的郵件標頭欄位

下列 X-header 和路由標頭類型會受到標頭防火牆影響：

  - **組織 X-header**   這些 X-header 欄位的開頭為 **X-MS-Exchange-Organization-**。

  - **樹系 X-header**   這些 X-header 欄位的開頭為 **X-MS-Exchange-Forest-**。
    
    如需組織 X-header 與樹系 X-header 的範例，請參閱本主題最後的 Organization X-headers and forest X-headers in Exchange 一節。

  - **Received ︰ 路由標頭**  此標頭欄位的不同的執行個體的每一個郵件伺服器接受並將郵件轉寄給收件者新增至郵件標頭。**Received:**標頭通常包含郵件伺服器和日期-時間戳記的名稱。

  - **重新傳送-\*: 路由標頭**  重新傳送標頭欄位是可用來判斷使用者是否已轉寄郵件的資訊的標頭欄位。下列最近的標頭欄位僅供 ︰ **Resent-Date:**、 **Resent-From:**、 **Resent-Sender:**、 **Resent-To:**、 **Resent-Cc:**、 **Resent-Bcc:**及**Resent-Message-ID:**。如此會出現訊息給收件者好像送直接的原始寄件者用**Resent-**欄位。收件者可以檢視探索誰轉寄郵件的郵件標頭。

Exchange 使用兩種不同方式，對郵件內的組織 X-header、樹系 X-header 和路由標頭套用標頭防火牆：

  - 對傳送連接器或接收連接器指派權限，以便在郵件通過連接器時保留或移除郵件中的特定標頭類型。

  - 提交其他郵件類型時，會對郵件內的特定標頭類型自動實作標頭防火牆。

回到頁首

## 標頭防火牆如何套用至傳送連接器和接收連接器

標頭防火牆會根據指派給連接器的特定權限，套用至通過傳送連接器和接收連接器的郵件。

如果權限指派給接收連接器或 \[傳送連接器\] 標頭防火牆不會套用至通過連接器的郵件。受影響的標頭欄位會保留在郵件中。

如果權限不指派給接收連接器或 \[傳送連接器\] 標頭防火牆會套用至通過連接器的郵件。受影響的標頭欄位是從郵件中移除。

下表說明傳送連接器和接收連接器上用來套用標頭防火牆的權限，以及受影響的標頭欄位。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>連接器類型</th>
<th>權限</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>接收連接器</p></td>
<td><p><strong>Ms-Exch-Accept-Headers-Organization</strong></p></td>
<td><p>此權限會影響輸入郵件中開頭為 <strong>X-MS-Exchange-Organization-</strong> 的組織 X-header 欄位。</p></td>
</tr>
<tr class="even">
<td><p>接收連接器</p></td>
<td><p><strong>Ms-Exch-Accept-Headers-Forest</strong></p></td>
<td><p>此權限會影響輸入郵件中開頭為 <strong>X-MS-Exchange-Forest-</strong> 的樹系 X-header 欄位。</p></td>
</tr>
<tr class="odd">
<td><p>接收連接器</p></td>
<td><p><strong>Ms-Exch-Accept-Headers-Routing</strong></p></td>
<td><p>此權限會影響輸入郵件中的 <strong>Received:</strong> 和 <strong>Resent-*:</strong> 路由標頭欄位。</p></td>
</tr>
<tr class="even">
<td><p>傳送連接器</p></td>
<td><p><strong>Ms-Exch-Send-Headers-Organization</strong></p></td>
<td><p>此權限會影響輸出郵件中開頭為 <strong>X-MS-Exchange-Organization-</strong> 的組織 X-header 欄位。</p></td>
</tr>
<tr class="odd">
<td><p>傳送連接器</p></td>
<td><p><strong>Ms-Exch-Send-Headers-Forest</strong></p></td>
<td><p>此權限會影響輸出郵件中開頭為 <strong>X-MS-Exchange-Forest-</strong> 的樹系 X-header 欄位。</p></td>
</tr>
<tr class="even">
<td><p>傳送連接器</p></td>
<td><p><strong>Ms-Exch-Send-Headers-Routing</strong></p></td>
<td><p>此權限會影響輸出郵件中的 <strong>Received:</strong> 和 <strong>Resent-*:</strong> 路由標頭欄位。</p></td>
</tr>
</tbody>
</table>


## 接收連接器上輸入郵件的標頭防火牆

下表說明接收連接器上標頭防火牆權限的預設應用。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>權限</th>
<th>已指派權限的預設 Exchange 安全性主體</th>
<th>以安全性主體為成員的權限群組</th>
<th>將權限群組指派給接收連接器的預設用法類型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Ms-Exch-Accept-Headers-Organization</strong> 和 <strong>Ms-Exch-Accept-Headers-Forest</strong></p></td>
<td><ul>
<li><p>Hub Transport Server</p></li>
<li><p>Edge Transport Server</p></li>
<li><p>Exchange 伺服器</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>僅在 Hub Transport server 上</td>
</tr>
</tbody>
</table>

</li>
</ul></td>
<td><p><strong>ExchangeServers</strong></p></td>
<td><p><code>Internal</code></p></td>
</tr>
<tr class="even">
<td><p><strong>Ms-Exch-Accept-Headers-Routing</strong></p></td>
<td><p>匿名使用者帳戶</p></td>
<td><p><strong>Anonymous</strong></p></td>
<td><p><code>Internet</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>Ms-Exch-Accept-Headers-Routing</strong></p></td>
<td><p>已驗證的使用者帳戶</p></td>
<td><p><strong>ExchangeUsers</strong></p></td>
<td><p><code>Client</code> (Edge Transport Server 上無法使用)</p></td>
</tr>
<tr class="even">
<td><p><strong>Ms-Exch-Accept-Headers-Routing</strong></p></td>
<td><ul>
<li><p>Hub Transport Server</p></li>
<li><p>Edge Transport Server</p></li>
<li><p>Exchange 伺服器</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>僅限 Hub Transport server</td>
</tr>
</tbody>
</table>

</li>
<li><p>以外部方式保護安全的伺服器</p></li>
</ul></td>
<td><p><strong>ExchangeServers</strong></p></td>
<td><p><code>Internal</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>Ms-Exch-Accept-Headers-Routing</strong></p></td>
<td><p>協力程式伺服器帳戶</p></td>
<td><p><strong>Partner</strong></p></td>
<td><p><code>Internet</code>和<code>Partner</code></p></td>
</tr>
</tbody>
</table>


回到頁首

## 自訂接收連接器上的標頭防火牆

如果在自訂接收連接器案例中您想要對郵件套用標頭防火牆，請使用下列任何一種方法：

  - 建立自動套用至郵件的 \[標頭防火牆流量類型的接收連接器。請注意您就可以設定流量類型，僅當您建立的接收連接器。
    
      - 若要從郵件中移除組織 X-header 或樹系 X-header，請建立接收連接器並選取 `Internal` 以外的用法類型。
    
      - 若要從郵件中移除路由標頭，請執行下列其中一個動作：
        
          - 建立的接收連接器，並選取 \[使用狀況類型`Custom`。未指派任何權限群組至接收連接器。
        
          - 修改現有的接收連接器，然後將 *PermissionGroups* 參數值設為 `None`。
        
        請注意，如果您的接收連接器未被指派任何權限群組，則須依照上一個步驟所述對接收連接器新增安全性主體。

  - 使用接收連接器設定**Remove-ADPermission**指令程式來移除**Ms-Exch-Accept-Headers-Organization**權限、 **Ms-Exch-Accept-Headers-Forest**權限與**Ms-Exch-Accept-Headers-Routing**權限安全性主體。此方法不適如果權限已指派給在接收連接器上使用的權限群組的安全性主體因為您無法修改權限指派\] 或 \[權限群組的群組成員資格。

  - 使用**Add-ADPermission**指令程式可新增所需的郵件流程的接收連接器上的適當的安全性主體。請確定沒有安全性主體具有**Ms-Exch-Accept-Headers-Organization**權限、 **Ms-Exch-Accept-Headers-Forest**權限\] 及 \[ **Ms-Exch-Accept-Headers-Routing** \] 權限指派給他們。必要時，使用**Add-ADPermission** cmdlet 來拒絕接收連接器設定的安全性主體**Ms-Exch-Accept-Headers-Organization**權限、 **Ms-Exch-Accept-Headers-Forest**權限及**Ms-Exch-Accept-Headers-Routing**權限。

如需相關資訊，請參閱下列主題：

  - [接收連接器](receive-connectors-exchange-2013-help.md)

  - [Add-ADPermission](https://technet.microsoft.com/zh-tw/library/bb124403\(v=exchg.150\))

  - [Remove-ADPermission](https://technet.microsoft.com/zh-tw/library/aa996048\(v=exchg.150\))

回到頁首

## 傳送連接器上輸出郵件的標頭防火牆

下表說明傳送連接器上標頭防火牆權限的預設應用。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>權限</th>
<th>已指派權限的預設 Exchange 安全性主體</th>
<th>將安全性主體指派給傳送連接器的預設用法類型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Ms-Exch-Send-Headers-Organization</strong> 和 <strong>Ms-Exch-Send-Headers-Forest</strong></p></td>
<td><ul>
<li><p>Hub Transport Server</p></li>
<li><p>Edge Transport Server</p></li>
<li><p>Exchange 伺服器</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>僅在 Hub Transport server 上</td>
</tr>
</tbody>
</table>

</li>
<li><p>以外部方式保護安全的伺服器</p></li>
<li><p><strong>ExchangeLegacyInterop</strong> 萬用安全性群組</p></li>
</ul></td>
<td><p><code>Internal</code></p></td>
</tr>
<tr class="even">
<td><p><strong>Ms-Exch-Send-Headers-Routing</strong></p></td>
<td><ul>
<li><p>Hub Transport Server</p></li>
<li><p>Edge Transport Server</p></li>
<li><p>Exchange 伺服器</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>僅在 Hub Transport server 上</td>
</tr>
</tbody>
</table>

</li>
<li><p>以外部方式保護安全的伺服器</p></li>
<li><p><strong>ExchangeLegacyInterop</strong> 萬用安全性群組</p></li>
</ul></td>
<td><p><code>Internal</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>Ms-Exch-Send-Headers-Routing</strong></p></td>
<td><p>匿名使用者帳戶</p></td>
<td><p><code>Internet</code></p></td>
</tr>
<tr class="even">
<td><p><strong>Ms-Exch-Send-Headers-Routing</strong></p></td>
<td><p>協力程式伺服器</p></td>
<td><p><code>Partner</code></p></td>
</tr>
</tbody>
</table>


回到頁首

## 自訂傳送連接器上的標頭防火牆

如果在自訂傳送連接器案例中您想要對郵件套用標頭防火牆，請使用下列任何一種方法：

  - 建立傳送連接器會自動套用至郵件的 \[標頭防火牆流量類型。請注意您就可以設定流量類型，僅當您建立的傳送連接器。
    
      - 若要從郵件中移除組織 X-header 或樹系 X-header，請建立傳送連接器並選取 `Internal` 或 `Partner` 以外的用法類型。
    
      - 若要從郵件中移除路由標頭，請建立傳送連接器並選取 \[使用狀況類型`Custom`。**Ms-Exch-Send-Headers-Routing**權限指派給所有傳送連接器用法類型`Custom`除外。

  - 從連接器移除指派了 **Ms-Exch-Send-Headers-Organization** 權限、**Ms-Exch-Send-Headers-Forest** 權限和 **Ms-Exch-Send-Headers-Routing** 權限的安全性主體。

  - 使用 **Remove-ADPermission** 指令程式，從傳送連接器上設定的其中一個安全性主體移除 **Ms-Exch-Send-Headers-Organization** 權限、**Ms-Exch-Send-Headers-Forest** 權限和 **Ms-Exch-Send-Headers-Routing** 權限。

  - 使用 **Add-ADPermission** 指令程式，在傳送連接器上設定的其中一個安全性主體中，拒絕 **Ms-Exch-Send-Headers-Organization** 權限、**Ms-Exch-Send-Headers-Forest** 權限和 **Ms-Exch-Send-Headers-Routing** 權限。

如需相關資訊，請參閱下列主題：

  - [傳送連接器](send-connectors-exchange-2013-help.md)

  - [Add-ADPermission](https://technet.microsoft.com/zh-tw/library/bb124403\(v=exchg.150\))

  - [Remove-ADPermission](https://technet.microsoft.com/zh-tw/library/aa996048\(v=exchg.150\))

回到頁首

## 其他郵件來源的標頭防火牆

訊息可以在信箱伺服器或 Edge Transport server 上的傳輸管線輸入而不需使用傳送連接器或接收連接器。下列清單所述標頭防火牆套用到這些郵件來源：

  - **收取目錄和重新顯示\] 目錄**  \[收取\] 目錄是由系統管理員或應用程式用來送出郵件的檔案。重新顯示目錄用來重新提交已從 Exchange 訊息佇列匯出的郵件。如需 Pickup 和 Replay 目錄的詳細資訊，請參閱[收取目錄和重新顯示\] 目錄](pickup-directory-and-replay-directory-exchange-2013-help.md)。
    
    會從收取目錄的郵件檔案中移除組織 X-header、樹系 X-header 和路由標頭。
    
    但保留重新顯示目錄所提交之郵件中的路由標頭。
    
    會保留還是移除重新顯示目錄中郵件的組織 X-header 和樹系 X-header，由郵件檔案中的 **X-CreatedBy:** 標頭欄位控制：
    
      - 如果 **X-CreatedBy:** 的值是 `MSExchange15`，則保留郵件中的組織 X-header 和樹系 X-header。
    
      - 如果 **X-CreatedBy:** 的值不是 `MSExchange15`，則移除郵件中的組織 X-header 和樹系 X-header。
    
      - 如果郵件檔案中沒有 **X-CreatedBy:** 標頭欄位，則移除郵件中的組織 X-header 和樹系 X-header。

  - **放置目錄**  放置目錄用以 Mailbox server 上的外部連接器將郵件傳送至不使用 SMTP 傳輸郵件的郵件伺服器。如需外部連接器的詳細資訊，請參閱[外部連接器](foreign-connectors-exchange-2013-help.md)。
    
    在將郵件檔案放入放置目錄之前，會先移除檔案中的組織 X-header 與樹系 X-header。
    
    但保留放置目錄所提交之郵件中的路由標頭。

  - **信箱傳輸**  轉送訊息與 Mailbox server 上的信箱的信箱伺服器上有信箱傳輸服務。如需 Mailbox Transport service 的詳細資訊，請參閱[郵件流程](mail-flow-exchange-2013-help.md)。
    
    會從由信箱傳輸提交服務自信箱傳送的外寄郵件中，移除組織 X-header、樹系 X-header 和路由標頭。
    
    路由標頭會保留給信箱收件者的內送郵件的信箱傳輸傳遞服務。下列組織 x-header 會保留給信箱收件者的內送郵件的信箱傳輸傳遞服務：
    
      - **X-MS-Exchange-Organization-SCL**
    
      - **X-MS-Exchange-Organization-AuthDomain**
    
      - **X-MS-Exchange-Organization-AuthMechanism**
    
      - **X-MS-Exchange-Organization-AuthSource**
    
      - **X-MS-Exchange-Organization-AuthAs**
    
      - **X-MS-Exchange-Organization-OriginalArrivalTime**
    
      - **X-MS-Exchange-Organization-OriginalSize**

  - **DSN 郵件**  在樹系組織 X 標頭、 X 標頭和路由標頭已從原始郵件或附加至 DSN 郵件的原始郵件標頭。如需 DSN 郵件的詳細資訊，請參閱[Dsn 和 Ndr in Exchange 2013](dsns-and-ndrs-in-exchange-2013-exchange-2013-help.md)。

  - **傳輸代理程式提交**   會保留傳輸代理程式提交之郵件中的組織 X-header、樹系 X-header 和路由標頭。

回到頁首

## Exchange 中的組織 X-Header 與樹系 X-Header

Mailbox Server 或 Edge Transport Server 上的傳輸服務會將自訂 X-header 欄位插入郵件標頭。

組織 X 標題的開頭**X-MS-Exchange-Organization-**。樹系 X 標題的開頭**X-MS-Exchange-Forest-**。下表說明一些組織 X 標頭和樹系中部署 Exchange 組織的郵件中所用的 X 標題。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>X-header</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Forest-RulesExecuted</strong></p></td>
<td><p>處理郵件的傳輸規則。</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-Antispam-Report</strong></p></td>
<td><p>內容篩選器代理程式對郵件套用反垃圾郵件篩選器後所得的結果摘要。</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-AuthAs</strong></p></td>
<td><p>指定的驗證來源。此 x-header 會一直存在時的郵件安全性的評估。可能的值為<code>Anonymous</code>、 <code>Internal</code>、 <code>External</code>或<code>Partner</code>。</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-AuthDomain</strong></p></td>
<td><p>填入 Domain Secure 驗證期間。此值為已驗證的遠端網域的 FQDN。</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-AuthMechanism</strong></p></td>
<td><p>指定送出郵件的驗證機制。此值是 2 位數的十六進位數字。</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-AuthSource</strong></p></td>
<td><p>指定代表組織進行郵件驗證評估之伺服器電腦的 FQDN。</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-Journal-Report</strong></p></td>
<td><p>會識別傳輸規則中的日誌報告。一旦訊息離開的傳輸服務、 標頭會變成<strong>X-MS-Journal-Report</strong>。</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-OriginalArrivalTime</strong></p></td>
<td><p>識別郵件初次進入 Exchange 組織的時間。</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-Original-Sender</strong></p></td>
<td><p>在被隔離郵件初次進入 Exchange 組織時識別其原始寄件者。</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-OriginalSize</strong></p></td>
<td><p>在被隔離郵件初次進入 Exchange 組織時識別其原始大小。</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-Original-Scl</strong></p></td>
<td><p>在被隔離郵件初次進入 Exchange 組織時識別其原始 SCL。</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-PCL</strong></p></td>
<td><p>識別網路釣魚信賴等級。可能的網路釣魚信賴等級值是從 1 到 8。較大的值表示可疑郵件。如需詳細資訊，請參閱<a href="anti-spam-stamps-exchange-2013-help.md">反垃圾郵件戳記</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-Quarantine</strong></p></td>
<td><p>會指出已隔離郵件垃圾郵件隔離信箱中及已傳送的傳遞狀態通知 (DSN)。或者，即表示已隔離郵件，並由系統管理員發行。此 X 標頭] 欄位會防止發行的訊息重新提交給垃圾郵件隔離信箱。如需詳細資訊，請參閱<a href="release-quarantined-messages-from-the-spam-quarantine-mailbox-exchange-2013-help.md">版本隔離的垃圾郵件隔離信箱的郵件</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-SCL</strong></p></td>
<td><p>會識別郵件的 SCL。可能的 SCL 值是從 0 到 9。較大的值表示可疑郵件。特殊值-1 豁免不內容篩選器代理程式所處理的郵件。如需詳細資訊，請參閱<a href="content-filtering-exchange-2013-help.md">內容篩選</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-SenderIdResult</strong></p></td>
<td><p>會包含寄件者識別碼代理程式的結果。寄件者識別碼代理程式使用的寄件者原則架構 (SPF) 比較郵件的來源 IP 位址用於網域中寄件者的電子郵件地址。寄件者識別碼結果用來計算郵件的 SCL。如需詳細資訊，請參閱<a href="sender-id-exchange-2013-help.md">寄件者識別碼</a>。</p></td>
</tr>
</tbody>
</table>


回到頁首

