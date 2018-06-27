---
title: '內容轉換: Exchange 2013 Help'
TOCTitle: 內容轉換
ms:assetid: bc367eb3-0306-4da9-9a84-4341caef77af
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb232174(v=EXCHG.150)
ms:contentKeyID: 50474126
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 內容轉換

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

*內容轉換*為正確格式一則訊息設定每個收件者的程序。若要在郵件上執行內容轉換的決策取決於目的地及正在處理郵件的格式。在 Microsoft Exchange Server 2013，有兩種不同內容轉換：

  - **外部收件者的郵件轉換**  此類型的內容轉換包含 Transport Neutral Encapsulation Format (TNEF) 對話選項及郵件編碼選項的外部收件者。郵件傳送至 Exchange 組織內的收件者不需要這種類型的內容轉換。此類型的內容轉換的信箱伺服器上的傳輸服務中分類程式處理方式。對每則郵件分類發生後新送達的郵件放在提交佇列中。收件者解析及路由解析度，除了是在郵件上執行內容轉換之前郵件放入傳遞佇列中。如果為單一訊息中包含多個收，分類程式會決定適當的每個郵件收件編碼。內容轉換追蹤不會擷取所有內容轉換失敗的分類程式遇到為將轉換為外部收件者傳送的郵件。

  - **MAPI 轉換的內部收件者**  此類型的內容轉換的信箱傳輸服務的處理方式。Mailbox Transport service 存在於本機伺服器上之信箱資料庫與 Mailbox server 上的傳輸服務間轉送訊息的 Mailbox server 上。主要是針對信箱傳輸提交服務會傳輸寄件者的寄件匣的信箱伺服器上的傳輸服務的郵件。Mailbox Transport 傳遞服務傳輸郵件從信箱伺服器上的傳輸服務給收件者的收件匣。信箱傳輸提交服務會從 MAPI 轉換所有外寄郵件和信箱傳輸傳遞服務會將所有內送郵件轉換成 MAPI。內容轉換追蹤擷取這些 MAPI 轉換失敗率。如需詳細資訊，請參閱[內容轉換追蹤](content-conversion-tracing-exchange-2013-help.md)。

本主題說明外部收件者的郵件轉換選項。

**目錄**

Exchange and Outlook message formats

Content conversion options for external recipients

Understanding the structure of email messages

## Exchange 和 Outlook 郵件格式

下列清單描述 Exchange 和 Microsoft Outlook 中可用的基本郵件格式：

  - **純文字**  純文字郵件使用僅限 US-ASCII 文字 RFC 2822 中所述。郵件不能包含不同字型或其他文字格式設定。純文字郵件可用下列兩種格式：
    
      - 郵件標頭和郵件內文 US-ASCII 文字所組成。必須使用*Uuencode*編碼的附件。Uuencode 代表 Unix-Unix 編碼及定義的電子郵件內文中儲存二進位附件使用 US-ASCII 文字字元編碼演算法。
    
      - 郵件為 text/plain 的內容類型值和 multipart 郵件文字部分的 7 位元傳輸編碼內容值使用 MIME 編碼。任何郵件附件的編碼使用引號列印或 Base64 編碼。根據預設，當您撰寫並傳送純文字郵件在 Outlook 中，訊息是內容類型值為 text/plain MIME 編碼。

  - **HTML**  HTML 郵件支援文字格式、 背景圖像、 表格、 項目符號及其他圖形元素。根據定義，HTML 格式郵件長度必須 MIME 編碼為保存這些元素的格式設定。

  - **Rtf 格式 (RTF)**  RTF 支援文字格式設定與其他圖形元素。RTF 是 deliverable TNEF。可以交替使用 TNEF 與 RTF。Rtf 文字郵件格式是截然不同的 Microsoft Word 中可用的 rtf 文字文件格式。
    
    只有 Outlook 和少數其他 MAPI 電子郵件用戶端能夠判讀 RTF 郵件。

  - **TNEF**  Transport Neutral Encapsulation Format 為 Microsoft 特定格式封裝 MAPI 編製郵件內容。TNEF 郵件包含郵件和附件封裝郵件的原始格式化的版本的純文字版本。一般而言，這個附件名為 Winmail.dat。Winmail.dat 附件包含下列資訊：
    
      - 原始格式版本的郵件，例如包括字型、文字大小及文字色彩
    
      - OLE 物件，例如包括內嵌圖片或內嵌 Microsoft Office 文件
    
      - 特殊的 Outlook 功能，例如包括自訂表單、投票按鈕或會議邀請
    
      - 原始郵件中的一般郵件附件
    
    產生的純文字郵件可以用下列格式呈現：
    
      - RFC 2822 相容郵件，只由 US-ASCII 文字及 Uuencode 編碼的 Winmail.dat 附件組成
    
      - 含有 Winmail.dat 附件的 Multipart MIME 編碼郵件
    
    MAPI 相容的電子郵件用戶端完全可識別 TNEF，例如 Outlook、 處理 Winmail.dat 附件，並顯示原始郵件內容不屬於顯示 Winmail.dat 附件。不支援 tnef 的電子郵件用戶端可能會造成 TNEF 郵件任何下列兩種：
    
      - 顯示純文字版的郵件，且郵件包含附件 Winmail.dat、Win.dat 或其他通稱，例如 Att*nnnnn*.dat 或 Att*nnnnn*.eml，其中的 *nnnnn* 預留位置代表隨機數字。
    
      - 顯示純文字版的郵件。忽略或移除 TNEF 附件。結果為純文字郵件。
    
      - 訊息了解 TNEF 的伺服器可以設定來移除內送郵件的 TNEF 附件。結果是純文字郵件。此外，例如 Microsoft Outlook Express 某些電子郵件用戶端可能不瞭解 TNEF，但能辨識和略過 TNEF 附件。結果是純文字郵件。
    
    有協力廠商公用程式可以協助轉換 Winmail.dat 附件。
    
    自 Exchange Server 5.5 版 起，所有 Exchange 版本都可判讀 TNEF。

  - **摘要 Transport Neutral Encapsulation Format (STNEF)**  STNEF 即等於使用 TNEF。不過，STNEF 郵件的 TNEF 郵件不同編碼。尤其是 STNEF 郵件一定是 MIME 編碼且一律二進位內容傳輸編碼值。因此，有無純文字的表示法郵件，並沒有不同 Winmail.dat 附件的郵件內文中包含。整個郵件被表示使用僅限二進制資料。具有內容傳輸編碼的二進位值的郵件只可傳送的支援及 advertise BINARYMIME 和區塊處理 SMTP extensions RFC 3030 中所定義的 SMTP 郵件伺服器之間。郵件一定會轉接之間 SMTP 通訊使用 BDAT 命令，而不是標準的 \[資料\] 命令。
    
    STNEF 會自Exchange 2000瞭解的所有 Exchange 版本。STNEF 就會自動用於所有 Exchange 伺服器中的原生模式Exchange Server 2003自組織之間傳送的郵件。
    
    Exchange 永遠不會將 STNEF 郵件傳送給外部收件者。僅限 TNEF 郵件可以傳送至 Exchange 組織外部收件者。

回到頁首

## 外部收件者的內容轉換選項

您在 Exchange 組織中可為外部收件者設定的內容轉換選項分為下列幾類來說明：

  - **TNEF 轉換選項**   這些轉換選項指定是否該從離開 Exchange 組織的郵件中保留或移除 TNEF。

  - **郵件編碼選項**   這些選項指定郵件編碼選項，例如 MIME 和非 MIME 字元集、郵件編碼及附件格式。

這些轉換和編碼選項是獨立的另一個。例如 TNEF 郵件是否可以讓 Exchange 組織不相關的 MIME 編碼設定或純文字編碼設定的那些郵件。

您可以在 Exchange 組織的各種層級指定內容轉換，如下列清單所述：

  - **遠端網域設定**  遠端網域定義 Exchange 組織與外部網域之間的外寄郵件傳輸的設定。.即使您沒有建立針對特定網域的遠端網域項目時，有預先定義的遠端網域名為套用至所有遠端的位址空間 （\*） 的預設值。

  - **郵件使用者和郵件連絡人設定**  郵件使用者和郵件連絡人是類似因為兩者有外部電子郵件地址和包含 Exchange 組織外部人員的相關資訊。主要差異在於郵件使用者具有可以用來登入組織中的 Active Directory 網域及存取資源帳戶。

  - **Outlook 設定**   在 Outlook 中，您可以設定郵件格式和編碼選項，如下列清單所述：
    
      - **郵件格式** 您可以為所有郵件設定預設郵件格式。在撰寫特定郵件時，也可以覆寫預設郵件格式。
    
      - **網際網路郵件格式**  您可以控制是否 TNEF 郵件傳送至遠端收件者或是否他們會先轉換成多相容的格式。您也可以指定各種訊息傳送給遠端收件者的郵件編碼選項。這些設定不會套用到傳送至 Exchange 組織中的收件者的郵件。
    
      - **網際網路收件者郵件格式**  您可以控制是否 TNEF 郵件傳送給特定收件者或是否他們會先轉換成多相容的格式。您可以設定特定的連絡人對話選項您連絡人\] 資料夾中與您可以覆寫特定收件中，\[副本\] 對話選項或 \[密件副本欄位為您在撰寫郵件。這些轉換選項不適用於 Exchange 組織中收。
    
      - **網際網路收件者的郵件編碼選項**  您可以控制 MIME 或純文字編碼選項的特定連絡人\] 資料夾中與您的連絡人可以覆寫轉換選項特定收件者在收件者\]、 \[副本\] 或 \[密件副本\] 欄位為您在撰寫郵件。這些轉換選項不適用於 Exchange 組織中收。
    
      - **國際選項**   您可以控制郵件使用的字元集。

## TNEF 轉換選項

您可以指定下列層級的 TNEF 轉換選項：

  - 遠端網域設定

  - 郵件使用者和郵件連絡人設定

  - Outlook 設定，包括：
    
      - 郵件格式
    
      - 網際網路郵件格式
    
      - 網際網路收件者郵件格式

## 郵件編碼選項

您可以指定下列層級的郵件編碼選項：

  - 遠端網域設定

  - 郵件使用者和郵件連絡人設定

  - Outlook 設定，包括：
    
      - 郵件格式
    
      - 網際網路郵件
    
      - 網際網路收件者郵件格式
    
      - 郵件字元集編碼選項

如需詳細資訊，請參閱[郵件編碼選項](message-encoding-options-exchange-2013-help.md)。

回到頁首

## 了解電子郵件的結構

要更容易理解外部收內容對話選項，您必須了解電子郵件訊息的結構。SMTP 郵件根據撰寫並傳送電子郵件訊息的純文字 7 位元 US-ASCII 文字。標準的 SMTP 郵件是由下列元素所組成：

  - **郵件信封**  郵件信封定義於 RFC 2821 中。郵件信封包含傳輸和將郵件傳遞所需的資訊。收件者永遠不會看到郵件信封，因為其產生的郵件傳輸程序並不是真正的一部分訊息內容。

  - **郵件內容**   RFC 2822 中會定義郵件內容。郵件內容是由下列元素組成：
    
      - **郵件標頭**  郵件標頭是標頭欄位的集合。標頭欄位包含欄位名稱，後面接著冒號 （:） 字元、 後面欄位內文和結束的歸位/換 (CR/LF) 字元組合。
        
        欄位名稱必須包含的可列印 US-ASCII 文字字元除外冒號 （:） 字元。尤其被允許的值從透過 57 和 59 透過 126 33 ASCII 字元。
        
        欄位內文可能是任何 US-ASCII 字元，但不包括換行 (CR) 字元及 lf （換行） 字元換行字元所組成。但是，欄位內文包含可能 CR/換行字元組合中*標題摺疊*使用。標頭摺疊為單一標頭\] 欄位內文結尾的區隔將多行區段 2.2.3 RFC 2822 中所述。3 和 4 的 RFC 2822 各節將說明其他欄位內文的語法需求。
    
      - **郵件內文**  郵件內文是出現在郵件標頭之後的 US-ASCII 文字字元線的集合。郵件標頭和郵件內文結尾 CR/換行字元組合一個空白列以分隔。郵件內文是選擇性的。文字郵件內文中的任何一行必須小於 998 個字元。指出線條結尾只能一起出現 CR 和換行字元。

當 SMTP 訊息包含不純文字 US-ASCII 文字的元素時，郵件必須編碼要保留這些項目。MIME 標準定義的編碼中的郵件不是文字的內容的方法。MIME 允許其他字元集、 不含文字、 multipart 郵件內文和標頭欄位其他字元組中的附件中的文字。MIME 定義於 RFC 2045、 RFC 2046、 RFC 2047、 RFC 2048 及 RFC 2077 中。MIME 定義其他訊息屬性會指定的標頭欄位的集合。下表說明一些重要的 MIME 標頭欄位。

### 重要的 MIME 標頭欄位

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>標頭欄位名稱</th>
<th>預設值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MIME-Version</p></td>
<td><p>1.0</p></td>
<td><p>此標頭欄位是出現在格式化的 MIME 郵件中的第一個 MIME 標頭欄位。其他標準 RFC 2822 標頭欄位後面，但其他的 MIME 標頭欄位之前會出現此標頭] 欄位。MIME 感知的電子郵件用戶端會使用此標頭] 欄位來識別 MIME 編碼的訊息。缺少此標頭欄位時，MIME 感知的電子郵件用戶端會識別為純文字的郵件。</p></td>
</tr>
<tr class="even">
<td><p>Content-Type</p></td>
<td><p>text/plain</p></td>
<td><p>此標頭] 欄位會識別 RFC 2046 中所述的郵件內容的媒體類型。媒體類型是由類型、 subtype 及一或多個選擇性參數，例如會定義 MIME 字元集編碼<em>charset=</em>參數所組成。以&quot;x-&quot;開頭的類型不標準。開頭為&quot;vnd。&quot;的子類型為特定廠商。網際網路指派號碼授權單位 (IANA) 維護已登錄的媒體類型的清單。如需詳細資訊，請參閱<a href="https://www.iana.org/assignments/media-types/">MIME 媒體類型</a>。</p>
<p><em>Multipart</em>媒體類型允許相同的訊息中的多個郵件組件的使用不同的媒體類型所定義的章節。某些內容類型欄位的值包括 text/plain、 text/html、 multipart/mixed 及 multipart/alternative。</p></td>
</tr>
<tr class="odd">
<td><p>Content-Transfer-Encoding</p></td>
<td><p>7bit</p></td>
<td><p>此標頭欄位可以說明下列郵件資訊：</p>
<ul>
<li><p>用來轉換郵件內文中的任何非 US-ASCII 文字或二進位資料的編碼演算法。</p></li>
<li><p>說明郵件內文目前狀況的指標。</p></li>
</ul>
<p>可以有多個值的 MIME 郵件中的內容傳輸編碼標頭] 欄位。當內容傳輸編碼標頭] 欄位會出現在郵件標頭時，套用至整個郵件的本文。當內容傳輸編碼標頭] 欄位會出現在一個 multipart 郵件的組件時，它只適用於該部分的郵件。</p>
<p>當編碼的演算法套用至郵件內文資料時、 郵件內文資料會轉換成純文字 US-ASCII 文字。這個轉換允許透過舊僅支援 US-ASCII 文字中的 [郵件 SMTP 郵件伺服器的一點傳輸訊息。指出編碼的演算法用於在郵件內文的內容傳輸編碼標頭欄位的值如下：</p>
<ul>
<li><p><strong>Quoted-printable</strong>  此編碼演算法使用列印 US-ASCII 字元編碼郵件內文資料。如果原始郵件文字是多半 US-ASCII 文字，引號列印編碼提供有點可讀取及精簡結果。等號 （=） 字元以外所有列印 US-ASCII 文字字元可以代表不含編碼。</p></li>
<li><p><strong>Base64</strong>  此編碼的演算法主要根據隱私權增強郵件 (PEM) 標準 RFC 1421 中所定義。Base64 編碼要編碼的郵件內文資料使用演算法與輸出邊框距離設 PEM 所定義的字元編碼 64 個字元數字。Base64 編碼郵件通常是大於原始郵件的 33%。Base64 編碼郵件大小中建立可預測的增加也最佳的二進位資料和非 US-ASCII 文字。</p></li>
</ul>
<p>在相同的郵件中，通常不會使用多種編碼演算法。</p>
<p>在郵件內文的使用未編碼的演算法時, 的內容傳輸編碼標頭欄位純粹識別郵件內文資料的目前條件。下列內容傳輸編碼標頭欄位的值表示未編碼的演算法用於在郵件內文：</p>
<ul>
<li><p><strong>7 位元</strong>此值表示郵件內文資料已處於 RFC 2822 格式。特別是，這表示下列條件必須成立：</p>
<ul>
<li><p>所有文字行的長度必須少於 998 個字元。</p></li>
<li><p>所有字元必須是具有字元值 1 至 127 的 US-ASCII 文字。</p></li>
<li><p>CR 和 LF 字元必須一起使用來表示一行文字的結尾。</p></li>
</ul>
<p>整個郵件內文可能是 7 的位元或郵件內文結尾 multipart 郵件中的組件可能是 7 位元。如果 multipart 郵件包含有任何二進制資料或非 US-ASCII 文字，必須使用引號列印或 Base64 編碼演算法要編碼的郵件的組件的其他組件。</p>
<p>利用標準的 DATA 命令，具有 7bit 內文的郵件可以在 SMTP 郵件伺服器之間流通。</p></li>
<li><p><strong>8 位元</strong>此值表示郵件內文資料包含非美國 ASCII 字元。特別是，這表示下列條件必須成立：</p>
<ul>
<li><p>所有文字行的長度必須少於 998 個字元。</p></li>
<li><p>郵件內文中有一或多個字元的值大於 127。</p></li>
<li><p>CR 和 LF 字元必須一起使用來表示一行文字的結尾。</p></li>
</ul>
<p>整個訊息本文可能 8 位元或 multipart 郵件中的郵件內文部分可能是 8 位元。如果 multipart 郵件包含具有二進制資料的其他組件，必須使用引號列印或 Base64 編碼演算法編碼該部分的郵件。</p>
<p>已 8 位元內文的郵件只可以旅行社支援 8BITMIME SMTP 延伸等伺服器執行Exchange 2000 Server或較新版本中 RFC 1652 所定義的 SMTP 郵件伺服器之間。特別是，這表示下列條件必須成立：</p>
<ul>
<li><p>伺服器的 EHLO 回應中必須通告 8BITMIME 關鍵字。</p></li>
<li><p>郵件仍會使用 SMTP 標準資料命令來轉接。不過，本文 = 8BITMIME 參數必須新增至 MAIL FROM 命令的結尾。</p></li>
</ul></li>
<li><p><strong>二進位</strong>  此值表示郵件內文含有非 US-ASCII 文字或二進位資料。特別是，這表示下列條件成立：</p>
<ul>
<li><p>允許任何字元順序。</p></li>
<li><p>不限制行長度。</p></li>
<li><p>二進位郵件元素不需要編碼。</p></li>
</ul>
<p>已二進位內文的郵件只可以旅行社支援 BINARYMIME SMTP 副檔名例如執行Exchange 2000 Server或較新版本的伺服器中 RFC 3030 所定義的 SMTP 郵件伺服器之間。特別是，這表示下列條件必須成立：</p>
<ul>
<li><p>伺服器的 EHLO 回應中必須通告 BINARYMIME 關鍵字。</p></li>
<li><p>BINARYMIME SMTP 分機只用於區塊處理 SMTP 副檔名。<em>區塊</em>可讓大型郵件內文中多個、 較小的區塊中傳送。也定義於 RFC 3030 區塊。區塊關鍵字必須也是在該伺服器的 EHLO 回應中進行通告。</p></li>
<li><p>郵件是利用 BDAT 命令來傳輸，而不是用標準的 DATA 命令。</p></li>
<li><p>當郵件有郵件內文時，MAIL FROM 命令的結尾必須加上 <em>BODY=BINARYMIME</em> 參數。</p></li>
</ul></li>
</ul>
<p>值 7 位元、 8 位元和二進位永遠不存在於搭配相同的 multipart 郵件中。值就是互斥的。7 位元或 8 位元 multipart 郵件內文、 但永遠不在二進位郵件內文中的引號列印或 Base64 值可能會出現。如果 multipart 郵件內文包含 7 位元和 8 位元內容所組成的不同組件，整個郵件被分類為 8 位元。如果 multipart 郵件內文包含 7 位元、 8 位元和二進位內容所組成的不同組件，整個郵件被分類為二進位。</p></td>
</tr>
<tr class="even">
<td><p>Content-Disposition</p></td>
<td><p>Attachment</p></td>
<td><p>此標頭] 欄位會指示 MIME 啟用電子郵件用戶端上應該如何顯示的附加的檔案，並 RFC 2183 中所述。此欄位的值可以是內嵌或附件。當此欄位的值為 Inline 時、 郵件內文中顯示附件。當此欄位的值為附件時，附加的檔案會顯示為一般附件分開郵件內文。其他參數時，可使用其值是否為附件、 檔案名稱，例如建立日期、 及大小。</p></td>
</tr>
</tbody>
</table>


回到頁首

