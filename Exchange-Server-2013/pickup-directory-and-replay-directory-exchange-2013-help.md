---
title: '收取目錄和重新顯示] 目錄: Exchange 2013 Help'
TOCTitle: 收取目錄和重新顯示] 目錄
ms:assetid: ae191700-953f-411c-906f-dc90feec3d5a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124230(v=EXCHG.150)
ms:contentKeyID: 50473964
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 收取目錄和重新顯示\] 目錄

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

根據預設，\[收取\] 目錄和重新顯示\] 目錄存在於每一個 Microsoft Exchange Server 2013 Mailbox server 或 Edge Transport server 上。正確地格式化電子郵件訊息檔案複製到 \[收取\] 目錄或重新顯示目錄所送出的傳遞。郵件流程測試或應用程式所必須建立並送出自己的郵件系統管理員會使用 \[收取\] 目錄。重新顯示目錄接收的郵件來自外部的閘道伺服器和也可用來重新提交從 Exchange 伺服器的佇列匯出系統管理員的郵件。

**目錄**

Anatomy of an email message file

How the Pickup and Replay directories process messages

Pickup directory message file requirements

Pickup directory message header modifications

Replay directory message file requirements

Replay directory message header modifications

Failures in Pickup and Replay directory message processing

Security considerations for the Pickup and Replay directories

Permissions for the Pickup and Replay directories

## 電子郵件檔案的分析

標準 SMTP 電子郵件訊息所組成的*郵件信封*和郵件內容。郵件信封包含所需的傳輸與傳送之郵件的資訊。郵件內容包含 （統稱為 「*郵件標頭*） 的郵件標頭欄位及郵件內文。郵件標頭描述 RFC 2822 與 RFC 2821 中所述的郵件信封。

如果寄件者所撰寫的電子郵件送傳遞，郵件包含遵守 SMTP 標準，如寄件者、 收件者、 日期和時間郵件已由所需的基本資訊、 選用的主旨行及選用的郵件內文結尾。此資訊包含在訊息本身並依定義也包含在郵件標頭。

寄件者的郵件伺服器所使用的郵件標頭中找到的寄件者和收件者資訊將會產生之郵件的郵件信封並傳輸至收件者的郵件伺服器傳送網際網路郵件。收件者永遠不會看到郵件信封，因為其產生的郵件傳輸程序並不是實際的郵件的一部分。

參與的郵件傳輸的每部伺服器可能會插入在傳遞郵件或其他應用程式特定的郵件標頭欄位到的郵件標頭中的伺服器角色的相關的郵件標頭欄位。收件開啟時訊息所使用的電子郵件用戶端，電子郵件用戶端顯示一些郵件標頭，例如以傳送者、 收及郵件內文與主旨的更多相關資訊。

回到頁首

## 收取及重新顯示目錄如何處理郵件

在Exchange 2013，\[收取\] 目錄的預設位置是`%ExchangeInstallPath%TransportRoles\Pickup`。重新顯示\] 目錄的預設位置為`%ExchangeInstallPath%TransportRoles\Replay`。正確地格式化的.eml 將郵件檔案複製到 \[收取\] 目錄或重新顯示\] 目錄會處理提交下列步驟：

1.  Pickup 和 Replay 目錄會檢查有新郵件檔案每隔五秒鐘。您無法修改此輪詢間隔。您可以調整**Set-TransportService**指令程式上使用*PickupDirectoryMaxMessagesPerMinute*參數來處理郵件檔案的速率。此參數會影響 \[收取\] 目錄和重新顯示目錄。預設值是每分鐘 100 封郵件。無法開啟檔案留在 \[收取\] 目錄和評估在下一個投票。

2.  檢查有限制放在 \[收取\] 目錄，例如標頭大小上限和收件者數目上限的郵件檔案。依預設，標頭大小上限為 64 kb (KB) 和收件者數目上限為 100。您可以使用**Set-TransportService**指令程式變更這些限制。這些設定會影響僅 \[收取\] 目錄。

3.  檔案已從*\<filename\>*.eml *\<filename\>*.tmp 來重新命名。如果*\<filename\>*.tmp 檔案已存在，會將檔案重新命名為*\<filename\>\<datetime\>*.tmp。如果檔案重新命名失敗，會產生事件記錄檔錯誤，並收取程序會繼續下一個檔案。

4.  .Tmp 檔案成功地轉換到電子郵件訊息之後， **delete on close**的命令會發給.tmp 檔案。.Tmp 檔看起來會維持在收取目錄中，但無法開啟檔案。

5.  郵件已成功排入佇列的傳遞之後，發出**close**命令，並從 \[收取\] 目錄刪除.tmp 檔案。如果刪除失敗，事件記錄檔會產生錯誤。如果重新啟動 Microsoft Exchange Transport 服務則收取目錄中.tmp 檔案時，所有.tmp 檔案重新命名為.eml 檔案並已重新處理。這可能導致重複的郵件傳輸。

回到頁首

## 收取目錄郵件檔案需求

複製到收取目錄的郵件檔案必須符合下列需求才能成功傳遞：

  - 將郵件檔案必須遵守基本的 SMTP 郵件格式的文字檔案。支援 MIME 郵件標頭欄位及內容。

  - 郵件檔案的副檔名必須為 .eml。

  - 至少一個電子郵件地址必須存在於`Sender`或`From`郵件標頭欄位中的郵件標頭。如果單一電子郵件地址存在的`Sender`和`From`欄位中， `From`欄位中的電子郵件地址會當做建立者的郵件信封中的郵件。

  - `Sender` \] 欄位中可以存在只有一個電子郵件地址。不允許多個電子郵件地址。如果只有一個電子郵件地址存在於`From`欄位`Sender`欄位是選用的。

  - 多個電子郵件地址的`From`欄位中，但單一電子郵件地址也必須存在於`Sender` \] 欄位。`Sender`欄位中的地址然後會做為建立者的郵件信封中的郵件。

  - `To`、`Cc` 或 `Bcc` 欄位中必須至少有一個電子郵件地址存在。

  - 郵件標頭與郵件內文之間必須有一行空白行。

以下是純文字郵件的範例，該郵件使用收取目錄可接受的格式。

    To: mary@contoso.com
    From: bob@fabrikam.com
    Subject: Message subject
    
    This is the body of the message.

收取目錄郵件檔案也支援 MIME 內容。MIME 定義多種 7 位元 ASCII 文字、 HTML 和其他多媒體內容中包含無法表示語言的郵件內容。MIME 和其需求的完整說明已超出本主題的範圍。此範例顯示可接受的格式設定收取目錄使用簡單 MIME 郵件。

    To: mary@contoso.com
    From: bob@fabrikam.com
    Subject: Message subject
    MIME-Version: 1.0
    Content-Type: text/html; charset="iso-8859-1"
    Content-Transfer-Encoding: 7bit
    
    <HTML><BODY>
    <TABLE>
    <TR><TD>cell 1</TD><TD>cell 2</TD></TR>
    <TR><TD>cell 3</TD><TD>cell 4</TD></TR>
    </TABLE>

    </BODY></HTML>

回到頁首

## 收取目錄郵件標頭修改

收取目錄會從郵件標頭移除以下任何的郵件標頭欄位：

  - `Received`

  - `Resent-*`

  - `Bcc`
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>任何電子郵件地址正確處理中的郵件標頭欄位的選用<code>Bcc</code>郵件標頭中找到。<code>Bcc</code>收件者升級為不可見的郵件信封收件者之後，他們會移除郵件標頭來保護其身分識別。如果郵件含有僅<code>Bcc</code>收件者、 <strong>Undisclosed Recipients</strong>的值新增至郵件標頭的<code>To</code>欄位。</td>
    </tr>
    </tbody>
    </table>


\[收取\] 目錄將自己`Received`標頭\] 欄位新增至郵件為郵件送出程序的一部分。以下列格式套用`Received`標頭\] 欄位。

    Received: from localhost by Pickup with Microsoft SMTP Server id <ExchangeServerVersion><datetime>

收取目錄會修改下列郵件標頭欄位 (如果遺失或格式錯誤的話)：

  - **訊息識別碼** 如果 `Message-Id` 欄位遺漏或空白，收取目錄會使用 *\<GUID\>*@*\<defaultdomain\>* 格式來新增 \[訊息識別碼\] 欄位。

  - **日期**   如果 `Date` 欄位遺漏或格式錯誤，收取目錄會新增收取目錄處理郵件的日期和時間。

回到頁首

## 重新顯示目錄郵件檔案需求

重新顯示目錄用來重新提交匯出的 Exchange 郵件以及從外部閘道伺服器接收郵件。這些訊息已經格式化的重新顯示目錄。就少或沒有需要供系統管理員或應用程式撰寫與使用重新顯示目錄提交新的郵件檔案。收取目錄應該用來建立並送出新的郵件檔案。

重新顯示目錄郵件請常使用*X 標頭*。X-header 已存在於郵件標頭中的使用者定義的非公務郵件標頭欄位。X-header 未特別提及 RFC 2822 之中，但開頭"X-"未定義的郵件標頭欄位使用已經成為非公務郵件標頭欄位新增至郵件公認一種方式。Exchange 特有 X 標頭用於目錄實際可以設定通常是存在於郵件信封中的傳遞資訊重新顯示的訊息檔案。這項功能，才能使用重新顯示目錄來處理來自另一部 Exchange 伺服器匯出的訊息時保留原始郵件資訊。

複製至重新顯示目錄的郵件檔必須符合下列需求，才能順利傳遞：

  - 將郵件檔案必須遵守基本的 SMTP 郵件格式的文字檔案。支援 MIME 郵件標頭欄位及內容。

  - 郵件檔案的副檔名必須為 .eml。

  - X-Header 必須放在所有標準標頭欄位之前。

  - 標頭欄位與郵件內文之間必須有一行空白行。

重新顯示目錄中的郵件需要下列清單描述的 X-Header：

  - **X-寄件者**  此 X-header 會取代為一般的 SMTP 郵件的`From`郵件標頭欄位需求。必須存在一個`X-Sender`欄位包含一個電子郵件地址。如果它是存在，雖然收件者的電子郵件用戶端顯示`From`郵件標頭欄位的值為郵件的寄件者重新顯示目錄會略過`From`郵件標頭\] 欄位。其他參數通常是存在於`X-Sender` \] 欄位中，如下列範例所示。
    
        X-Sender: <bob@fabrikam.com> BODY=7bit RET=HDRS ENVID=12345ABCD auth=<someAuth>
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>這些參數彼此通常由傳送伺服器產生的郵件信封值。您可能會看到類似匯出的訊息檔案中的參數。<br />
    <code>RET</code> 會指定若郵件未能傳遞時，應將整封郵件或只將標頭傳回給寄件者。<code>RET</code> 可以有 <code>HDRS</code> 或 <code>FULL</code> 的值。<code> ENVID</code> 是郵件信封識別碼。<code>BODY</code> 會指定郵件的文字編碼。<code>auth</code> 會指定通訊伺服器的驗證機制，如 RFC 2554 中所述。</td>
    </tr>
    </tbody>
    </table>


  - **X 接收器**  此 X-header 會取代為一般的 SMTP 郵件的`To`郵件標頭欄位需求。至少一個包含一個電子郵件地址的`X-Receiver`欄位必須存在。多個`X-Receiver`欄位允許的多個收件者。如果雖然收件者的電子郵件用戶端的郵件收件者顯示`To`郵件標頭欄位的值是存在，重新顯示目錄會略過`To`郵件標頭欄位。下列範例所示其他選用的參數可能存在`X-Receiver` \] 欄位。
    
        X-Receiver: <mary@contoso.com> NOTIFY=NEVER ORcpt=mary@contoso.com
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>這些參數彼此通常由傳送伺服器產生的郵件信封值。您可能會看到類似匯出的訊息檔案中的參數。這些參數相關傳遞狀態通知 (DSN) 郵件 RFC 1891 所述。<br />
    <code>NOTIFY</code> 可以有 <code>NEVER</code>、<code>DELAY</code> 或 <code>FAILURE</code> 的值。<code>ORcpt</code> 會保留原始郵件收件者。</td>
    </tr>
    </tbody>
    </table>


重新顯示目錄中的郵件檔可以選用下列清單描述的 X-Header。

  - **X-CreatedBy**  用於頁首防火牆功能。如果此 X-header 存在，必須不是空白。如果`X-CreatedBy`欄位不存在，則會新增**Unspecified**的值。一般而言，此欄位的值是**MSExchange15**，但它也可能會包含非 SMTP 位址空間類型設定的傳送連接器，例如**Notes**。

  - **X-EndOfInjectedXHeaders**  大小 （位元組） 所有 X 標頭的存在。此 X-header 可能會標記為用來指出上次的 X-header 才能正常的郵件標頭欄位啟動。

  - **X-ExtendedMessageProps**   郵件的延伸郵件內容。

  - **X-HeloDomain**   初始 SMTP 通訊協定交談期間所呈現的 HELO/EHLO 網域字串。

  - **X-來源**  使用佇列檢視器**MessageSourceName** \] 欄下。如果未指定此 X-header 值，則會使用**Replay**的值。針對此 X-header 其他可能的值是**Smtp Receive Connector**和**Smtp Send Connector**。

  - **X-SourceIPAddress**  傳送伺服器的 IP 位址。此欄位，則`0.0.0.0`不指定任何 IP 位址。

以下是純文字郵件的範例，該郵件使用重新顯示目錄可接受的格式。

    X-Receiver: <mary@contoso.com> NOTIFY=NEVER ORcpt=mary@contoso.com
    X-Sender: <bob@fabrikam.com> BODY=7bit ENVID=12345AB auth=<someAuth>
    Subject: Optional message subject
    
    This is the body of the message.

重新顯示目錄訊息檔案也支援 MIME 內容。MIME 定義多種 7 位元 ASCII 文字、 HTML 和其他多媒體內容中包含無法表示語言的郵件內容。MIME 和其需求的完整說明已超出本主題的範圍。此範例會顯示簡易的 MIME 郵件使用可接受的重新顯示\] 目錄的格式設定。

    X-Receiver: <mary@contoso.com> NOTIFY=NEVER ORcpt=mary@contoso.com
    X-Sender: <bob@fabrikam.com> BODY=7bit ENVID=12345ABCD auth=<someAuth>
    To: mary@contoso.com
    From: bob@fabrikam.com
    Subject: Optional message subject
    MIME-Version: 1.0
    Content-Type: text/html; charset="iso-8859-1"
    Content-Transfer-Encoding: 7bit
    
    <HTML><BODY>
    <TABLE>
    <TR><TD>cell 1</TD><TD>cell 2</TD></TR>
    <TR><TD>cell 3</TD><TD>cell 4</TD></TR>
    </TABLE>

    </BODY></HTML>

回到頁首

## 重新顯示目錄郵件標頭修改

重新顯示目錄會刪除郵件檔中的 `Bcc` 郵件標頭欄位。

重新顯示目錄將自己`Received`郵件標頭欄位新增至郵件為郵件送出程序的一部分。已接收郵件標頭\] 欄位會套用下列格式。

    Received: from <ReceivingServerName> by Replay with <ExchangeServerVersion><DateTime>

重新顯示目錄會在郵件標頭中修改下列郵件標頭欄位：

  - **訊息識別碼** 如果此訊息標頭欄位遺失或空白，重新顯示目錄會使用 *\<GUID\>*@*\<defaultdomain\>* 格式來新增 \[訊息識別碼\] 訊息標頭欄位。

  - **日期**   如果此郵件標頭欄位遺失或格式錯誤，重新顯示目錄會以重新顯示目錄處理郵件的日期和時間來加入 Date 郵件標頭欄位。

回到頁首

## 收取及重新顯示目錄郵件處理失敗

將郵件檔案複製到 \[收取\] 目錄或重新顯示\] 目錄可能不會成功排入佇列的傳遞。即會發生下列郵件送出失敗的類別：

  - **傳遞失敗**  正確地格式化將郵件檔案與有效的寄件者無法成功送出一起傳遞的產生未傳遞回報 (NDR)。格式不正確的內容或收取目錄郵件限制違規也可能造成 NDR。郵件處理期間產生的 NDR，原始郵件檔案附加至 NDR 郵件，並將郵件檔案刪除 \[收取\] 目錄或重新顯示目錄。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>送出到傳輸管線正確地格式化的郵件稍後可能會遇到傳遞失敗並傳回給寄件者與 NDR。這種失敗可能會對收取] 目錄或重新顯示目錄，例如通訊伺服器故障或路由傳送之郵件的傳遞路徑失敗不相關的傳輸問題所造成。</td>
    </tr>
    </tbody>
    </table>


  - **Badmail**  郵件分類為*badmail*具有嚴重問題，防止送出的郵件傳遞 \[收取\] 目錄或重新顯示\] 目錄。郵件格式正確，但收件者無效，且無法 NDR 郵件傳送給寄件者因為寄件者不是有效時，才會使 badmail 的條件。
    
    決定要 badmail 郵件檔案收取或重新顯示目錄中左和從*\<filename\>*.eml *\<filename\>*.bad 要重新命名。如果*\<filename\>*.bad 檔案已存在，該檔案已重新命名為*\<filename\>\<datetime\>*.bad。如果 badmail 存在於 \[收取\] 目錄或重新顯示\] 目錄中，會產生事件記錄檔錯誤，但是相同的 badmail 訊息不會產生重複的事件記錄檔錯誤。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>永遠撰寫並將郵件檔案儲存在不同的位置之前將其複製到 [收取] 目錄進行傳遞。[收取] 目錄輪詢新郵件的每隔五秒鐘。因此，如果您嘗試撰寫，並將郵件檔案儲存本身收取目錄中，[收取] 目錄可能會嘗試重新處理郵件檔案之前完成撰寫它們。</td>
    </tr>
    </tbody>
    </table>


回到頁首

## 收取及重新顯示目錄的安全性考量

下列清單描述收取目錄及重新顯示目錄常用的安全性考量：

  - 在接收連接器上設定的任何安全性檢查 (例如反垃圾郵件、反惡意程式碼、寄件者篩選，或是收件者篩選動作) 都不會針對透過收取目錄或重新顯示目錄提交的郵件執行。

  - 洩漏收取目錄或重新顯示\] 目錄可以擔任開放式轉送運作。這可讓需重新提交的郵件，或*轉送*至遮罩，則為 true 的郵件來源使用不同的伺服器。

下列清單描述適用於重新顯示目錄的安全性考量：

  - 使用 \[重新顯示目錄 X 標頭允許在手動建立的郵件信封。`X-Sender`和`X-Receiver`欄位中的資訊可以是截然不同`To`或`From`郵件標頭欄位顯示的電子郵件用戶端。寄件者和網域的這類模擬經常會呼叫*詐騙*。*詐騙的郵件*是具有傳送位址的上次修改看起來像於非實際的郵件寄件者的寄件者的電子郵件訊息。

  - 如果`X-CreatedBy`欄位**MSExchange15**的值，目的地會被視為值得信任，並不會套用標頭防火牆。*標頭防火牆*是一種方式，以保留 X-header 訊息中的 exchange 傳輸之間信任的 Exchange 伺服器或可能會移除此處 X 標頭從郵件傳送到 Exchange 組織外的受信任目的地。這些 X 標頭可用來共用垃圾郵件信賴等級 (SCL) 郵件簽章，例如 Exchange 資訊或之間的加密授權 Exchange 伺服器。此處未經授權來源此資訊可能的潛在安全性風險。 如需標頭防火牆的詳細資訊，請參閱[Understanding 標頭防火牆](https://go.microsoft.com/fwlink/?linkid=268394)。

要重新顯示\] 目錄套用因為重新顯示目錄相關聯的其他安全性風險之間更緊密的安全性。使用者或必須產生和送出的郵件應用程式可以授與存取權 \[收取\] 目錄，但它們不應該需要重新顯示目錄權限。

收取目錄和重新顯示目錄會啟用所有 Mailbox server 和 Edge Transport server 上的預設。如果 \[收取\] 目錄或重新顯示目錄不需要在特定的 Mailbox server 或 Edge Transport server 在組織中的，您可以停用 \[收取\] 目錄或該伺服器上的重新顯示目錄將收取目錄路徑或重新顯示目錄路徑設定為值`$null`。如需詳細資訊，請參閱[設定 \[收取\] 目錄和重新顯示目錄](configure-the-pickup-directory-and-the-replay-directory-exchange-2013-help.md)。

回到頁首

## 收取及重新顯示目錄的權限

收取和重新顯示目錄需要下列權限：

  - 系統管理員： 完全控制

  - 系統：完全控制

  - 網路服務： 讀取、 寫入及刪除子資料夾和檔案

根據預設，Microsoft Exchange Transport 服務會使用網路服務使用者帳戶的安全性認證管理的位置和 Pickup 和 Replay 目錄的權限。網路服務帳戶需要這些權限 \[收取\] 目錄如此才能開啟.eml 檔案、 重新命名為.tmp 及刪除或如果郵件分類為 badmail.bad 來重新命名。

您可以使用*PickupDirectoryPath*與*ReplayDirectoryPath*參數**Set-TransportService**指令程式上移動這些目錄的位置。已成功變更 \[收取目錄位置而定的新的目錄位置、 網路服務帳戶授與權限及是否新目錄已經存在。如果目錄不存在，且網路服務帳戶建立資料夾與套用級的權限所需的權限會建立新的位置，將目錄，並套用正確的權限。如果新目錄已經存在，未檢查現有的資料夾權限。每當您移動目錄位置**Set-TransportService**指令程式搭配使用*PickupDirectoryPath*或*ReplayDirectoryPath*參數，一律確認新目錄存在新目錄已套用正確的權限。

回到頁首

