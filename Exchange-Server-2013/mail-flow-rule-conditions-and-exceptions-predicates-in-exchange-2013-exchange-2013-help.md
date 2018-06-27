---
title: '傳輸規則條件 （述詞）: Exchange 2013 Help'
TOCTitle: 郵件流程規則條件和例外狀況 (predicates)
ms:assetid: c918ea00-1e68-4b8b-8d51-6966b4432e2d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd638183(v=EXCHG.150)
ms:contentKeyID: 50474221
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 傳輸規則條件 （述詞）

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2017-12-20_

條件和例外狀況的郵件流程規則 （也稱為傳輸規則） 來識別此規則會套用到或不會套用至郵件。例如，如果規則新增至郵件免責聲明，您可以設定僅套用至包含特定字詞、 特定使用者所傳送的郵件訊息或除外特定群組的成員所傳送的所有郵件的規則。統稱條件和例外狀況的郵件流程規則也稱為*述詞*，因為是針對每個條件，沒有使用完全相同的設定和語法的對應例外。唯一的不同是條件指定要包含例外規則指定要排除的郵件時的郵件。

大部分的條件和例外狀況有一個需要一或多個值的屬性。例如，**寄件者**條件需要郵件的寄件者。某些條件有兩個屬性。例如**的郵件標頭包含任何這些字詞**條件需要一個屬性來指定郵件標頭\] 欄位中，並將第二個屬性來指定要在 \[標題\] 欄位中尋找的文字。某些條件或例外狀況不需要任何屬性。例如，**任何附件都有可執行檔內容**條件只是尋找具有可執行檔內容的郵件中的附件。

如需Exchange Server 2013中的郵件流程規則的詳細資訊，請參閱[郵件流程或傳輸規則](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)。

如需條件和例外狀況中Exchange Online Protection或Exchange Online中的郵件流程規則的詳細資訊，請參閱[Exchange Online 中的郵件流程規則條件和例外狀況 (predicates)](https://technet.microsoft.com/zh-tw/library/jj919235\(v=exchg.150\))或[郵件流程規則條件和例外狀況 （述詞） 在 \[Exchange Online Protection](https://technet.microsoft.com/zh-tw/library/jj919234\(v=exchg.150\))。

## 條件和例外狀況的 Mailbox server 上的郵件流程規則

下列各節中的表格說明條件和 Mailbox server 上的郵件流程規則中可用的例外狀況。在 \[屬性類型\] 區段中說明的內容類型。

寄件者

收件者

郵件主旨或內文

附件

任何收件者

為郵件敏感資訊類型和 \[副本\] 值、 大小和字元集

寄件者和收件者

編製郵件內容

郵件標頭

**附註：**

  - 您在Exchange 系統管理中心 (EAC) 中選取的條件或例外狀況之後，最終示**套用此規則情況**或**如果除了**欄位的值通常是不同 （小於） 您所選取的 click 路徑值。此外，當您建立新的範本 （已篩選清單的案例） 為基礎的規則，您通常可以選取而不是遵循完成 click 路徑的簡短的條件名稱。簡短的名稱與完整按一下值顯示在表格中的 \[EAC\] 欄中的路徑。

  - 如果您在 EAC 中選取**\[套用到所有郵件\]** ，您無法指定任何其他條件。建立規則未指定任何條件參數是Exchange 管理命令介面中的相對應。

  - 設定與屬性是相同的條件和例外狀況，因此**Get-TransportRulePredicate**指令程式的輸出不會分別列出例外狀況。此外，此指令程式會傳回述詞的部分名稱不同於相對應的參數名稱，且述詞可能需要多個參數。

## 寄件者

條件和例外狀況的檢查寄件者地址，您可以指定規則尋找寄件者地址的位置。

在 EAC 中，**此規則的屬性**\] 區段中按一下 \[**訊息中的比對寄件者地址**。請注意您可能需要按一下 \[**更多選項\]**以查看此設定。在Exchange 管理命令介面，則*SenderAddressLocation*參數。可用的值為：

  - **標頭**  只檢查郵件標頭 （例如**From**、 **Sender**或**Reply-To**欄位） 中的寄件者。這是預設值，並且郵件流程規則正常運作之前Exchange 2013累計更新 1 (CU1) 的方式。

  - **信封**  只檢查寄件者從郵件信封 （ **MAIL FROM**值所使用的 SMTP 傳輸，通常是儲存於**Return-Path**欄位）。請注意郵件信封搜尋只適用於下列情況 （和對應的例外狀況）：
    
      - **寄件者**(*From*)
    
      - **寄件者屬於**(*FromMemberOf*)
    
      - **寄件者地址包含**(*FromAddressContainsWords*)
    
      - **寄件者地址符合**(*FromAddressMatchesPatterns*)
    
      - **寄件者的網域是**(*SenderDomainIs*)

  - **標頭或信封**(`HeaderOrEnvelope`)  檢查郵件標頭和郵件信封中的寄件者。


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>條件或例外狀況在 EAC 中</th>
<th>Exchange 管理命令介面中的條件和例外狀況參數</th>
<th>屬性類型</th>
<th>描述</th>
<th>可用於</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>寄件者是</strong></p>
<p><strong>寄件者</strong>&gt;<strong>是此人</strong></p></td>
<td><p><em>From</em></p>
<p><em>ExceptIfFrom</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>由指定的信箱、 郵件使用者或Exchange組織中的郵件連絡人所傳送的郵件。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="even">
<td><p><strong>寄件者位於</strong></p>
<p><strong>寄件者</strong>&gt;<strong>外部/內部</strong></p></td>
<td><p><em>FromScope</em></p>
<p><em>ExceptIfFromScope</em></p></td>
<td><p><code>UserScopeFrom</code></p></td>
<td><p>由內部的寄件者或外部寄件者所傳送的郵件。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>寄件者是以下的成員</strong></p>
<p><strong>寄件者</strong>&gt;<strong>是此群組的成員</strong></p></td>
<td><p><em>FromMemberOf</em></p>
<p><em>ExceptIfFromMemberOf</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>所指定之群組的成員所傳送的郵件。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="even">
<td><p><strong>寄件者地址包含</strong></p>
<p><strong>寄件者</strong>&gt;<strong>地址包含任何這些字詞</strong></p></td>
<td><p><em>FromAddressContainsWords</em></p>
<p><em>ExceptIfFromAddressContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>包含寄件者的電子郵件地址中指定的文字的郵件。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>寄件者地址符合</strong></p>
<p><strong>寄件者</strong>&gt;<strong>地址符合任何這些文字模式</strong></p></td>
<td><p><em>FromAddressMatchesPatterns</em></p>
<p><em>ExceptIfFromAddressMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>出寄件者的電子郵件地址中包含的文字模式符合指定規則運算式的郵件。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="even">
<td><p><strong>寄件者的指定摘要資訊包含任何這些字詞</strong></p>
<p><strong>寄件者</strong>&gt;<strong>具有特定的屬性包括任何這些字詞</strong></p></td>
<td><p><em>SenderADAttributeContainsWords</em></p>
<p><em>ExceptIfSenderADAttributeContainsWords</em></p></td>
<td><p>第一個屬性： <code>ADAttribute</code></p>
<p>第二個屬性： <code>Words</code></p></td>
<td><p>寄件者指定的Active Directory内容中包含任何指定文字的郵件。</p>
<p>請注意<strong>Country</strong>屬性需要兩個字母國家/地區碼值 (例如 DE 德國)。</p></td>
<td><p>Exchange 2010或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>寄件者指定的摘要資訊符合這些文字模式</strong></p>
<p><strong>寄件者</strong>&gt;<strong>具有符合這些文字模式的特定屬性</strong></p></td>
<td><p><em>SenderADAttributeMatchesPatterns</em></p>
<p><em>ExceptIfSenderADAttributeMatchesPatterns</em></p></td>
<td><p>第一個屬性： <code>ADAttribute</code></p>
<p>第二個屬性： <code>Patterns</code></p></td>
<td><p>寄件者指定的Active Directory内容中包含文字模式符合指定規則運算式的郵件。</p></td>
<td><p>Exchange 2010或更新版本</p></td>
</tr>
<tr class="even">
<td><p><strong>寄件者已覆寫原則提示</strong></p>
<p><strong>寄件者</strong>&gt;<strong>已覆寫原則提示</strong></p></td>
<td><p><em>HasSenderOverride</em></p>
<p><em>ExceptIfHasSenderOverride</em></p></td>
<td><p>不適用</p></td>
<td><p>其中寄件者選擇覆寫資料外洩防護 (DLP) 原則的郵件。如需 DLP 原則的詳細資訊，請參閱<a href="technical-overview-of-dlp-data-loss-prevention-in-exchange.md">資料遺失防護</a>。</p></td>
<td><p>Exchange 2013或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>寄件者的 IP 位址在此範圍內</strong></p>
<p><strong>寄件者</strong>&gt; <strong>IP 位址在任何這些範圍或完全符合</strong></p></td>
<td><p><em>SenderIPRanges</em></p>
<p><em>ExceptIfSenderIPRanges</em></p></td>
<td><p><code>IPAddressRanges</code></p></td>
<td><p>寄件者的 IP 位址出符合指定的 IP 位址，或落在指定的 IP 位址範圍內的郵件。</p></td>
<td><p>Exchange 2013或更新版本</p></td>
</tr>
<tr class="even">
<td><p><strong>寄件者的網域為</strong></p>
<p><strong>寄件者</strong>&gt;<strong>網域是</strong></p></td>
<td><p><em>SenderDomainIs</em></p>
<p><em>ExceptIfSenderDomainIs</em></p></td>
<td><p><code>DomainName</code></p></td>
<td><p>出寄件者的電子郵件地址的網域符合指定的值的郵件。</p>
<p>如果您需要找出寄件者的網域，<em>包含</em>指定的網域 （例如，網域的所有子網域）、 使用<strong>寄件者地址符合</strong>(<em>FromAddressMatchesPatterns</em>) 條件以及使用語法來指定網域： <code>'@domain\.com$'</code>。</p></td>
<td><p>Exchange 2013或更新版本</p></td>
</tr>
</tbody>
</table>


返回頁首

## 收件者


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>條件或例外狀況在 EAC 中</th>
<th>Exchange 管理命令介面中的條件和例外狀況參數</th>
<th>屬性類型</th>
<th>描述</th>
<th>可用於</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>收件者是</strong></p>
<p><strong>收件者</strong>&gt;<strong>是此人</strong></p></td>
<td><p><em>SentTo</em></p>
<p><em>ExceptIfSentTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>其中一個收件者是指定的信箱、 郵件使用者或郵件的郵件連絡人Exchange組織中。收件者可以將郵件<strong>To</strong>、 <strong>Cc</strong>或<strong>Bcc</strong>欄位中。</p>
<p><strong>附註：</strong> 您無法指定通訊群組或擁有郵件功能的安全性群組。如果您需要對傳送至群組的郵件採取動作，請改用<strong>至] 方塊包含</strong>(<em>AnyOfToHeader</em>) 條件。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="even">
<td><p><strong>收件者位於</strong></p>
<p><strong>收件者</strong>&gt;<strong>是外部/外部</strong></p></td>
<td><p><em>SentToScope</em></p>
<p><em>ExceptIfSentToScope</em></p></td>
<td><p><code>UserScopeTo</code></p></td>
<td><p>傳送給內部收件者、 外部收件者、 合作夥伴組織外部收件者或非合作夥伴組織外部收件者的郵件。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>收件者是以下的成員</strong></p>
<p><strong>收件者</strong>&gt;<strong>是此群組的成員</strong></p></td>
<td><p><em>SentToMemberOf</em></p>
<p><em>ExceptIfSentToMemberOf</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>郵件包含收件者屬於指定之群組的成員。群組可以<strong>To</strong>、 <strong>Cc</strong>或<strong>Bcc</strong>欄位中的郵件。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="even">
<td><p><strong>收件者地址包含</strong></p>
<p><strong>收件者</strong>&gt;<strong>地址包含任何這些字詞</strong></p></td>
<td><p><em>RecipientAddressContainsWords</em></p>
<p><em>ExceptIfRecipientAddressContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>包含收件者的電子郵件地址中指定的文字的郵件。</p>
<p><strong>注意事項：</strong>這種情況並未考慮傳送至收件者 Proxy 位址的郵件。而只比對傳送至收件者主要電子郵件地址的郵件。</p></td>
<td><p>Exchange 2010或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>收件者地址符合</strong></p>
<p><strong>收件者</strong>&gt;<strong>地址符合任何這些文字模式</strong></p></td>
<td><p><em>RecipientAddressMatchesPatterns</em></p>
<p><em>ExceptIfRecipientAddressMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>出收件者的電子郵件地址中包含的文字模式符合指定規則運算式的郵件。</p>
<p><strong>注意事項：</strong>這種情況並未考慮傳送至收件者 Proxy 位址的郵件。而只比對傳送至收件者主要電子郵件地址的郵件。</p></td>
<td><p>Exchange 2010或更新版本</p></td>
</tr>
<tr class="even">
<td><p><strong>收件者的指定摘要資訊可以包含任何這些字詞</strong></p>
<p><strong>收件者</strong>&gt;<strong>具有特定的屬性包括任何這些字詞</strong></p></td>
<td><p><em>RecipientADAttributeContainsWords</em></p>
<p><em>ExceptIfRecipientADAttributeContainsWords</em></p></td>
<td><p>第一個屬性： <code>ADAttribute</code></p>
<p>第二個屬性： <code>Words</code></p></td>
<td><p>收件者指定的Active Directory内容中包含任何指定文字的郵件。</p>
<p>請注意<strong>Country</strong>屬性需要兩個字母國家/地區碼值 (例如 DE 德國)。</p></td>
<td><p>Exchange 2010或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>收件者的指定摘要資訊符合這些文字模式</strong></p>
<p><strong>收件者</strong>&gt;<strong>具有符合這些文字模式的特定屬性</strong></p></td>
<td><p><em>RecipientADAttributeMatchesPatterns</em></p>
<p><em>ExceptIfRecipientADAttributeMatchesPatterns</em></p></td>
<td><p>第一個屬性： <code>ADAttribute</code></p>
<p>第二個屬性： <code>Patterns</code></p></td>
<td><p>收件者指定的Active Directory内容中包含文字模式符合指定規則運算式的郵件。</p></td>
<td><p>Exchange 2010或更新版本</p></td>
</tr>
<tr class="even">
<td><p><strong>收件者的網域是</strong></p>
<p><strong>收件者</strong>&gt;<strong>網域是</strong></p></td>
<td><p><em>RecipientDomainIs</em></p>
<p><em>ExceptIfRecipientDomainIs</em></p></td>
<td><p><code>DomainName</code></p></td>
<td><p>郵件的收件者的電子郵件地址的網域符合指定的值的位置。</p>
<p>如果您需要找出收件者的網域，<em>包含</em>指定的網域 （例如，網域的所有子網域），請使用<strong>收件者地址符合</strong>(<em>RecipientAddressMatchesPatterns</em>) 條件，並使用下列的語法<code>'@domain\.com$'</code>指定的網域。</p></td>
<td><p>Exchange 2013或更新版本</p></td>
</tr>
</tbody>
</table>


返回頁首

## 郵件主旨或內文

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在主旨或郵件的其他標頭欄位中搜尋字詞或文字模式，會發生在郵件已從 MIME 內容傳輸編碼方法進行解碼<em>之後</em>，該編碼方法用來在 SMTP 伺服器之間傳送 ASCII 文字二進位訊息。您無法使用條件或例外狀況來搜尋主旨或郵件中其他標頭欄位的原始 (通常是 Base64) 編碼值。</td>
</tr>
</tbody>
</table>



<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>條件或例外狀況在 EAC 中</th>
<th>Exchange 管理命令介面中的條件和例外狀況參數</th>
<th>屬性類型</th>
<th>描述</th>
<th>可用於</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>在主旨或內文中包含</strong></p>
<p><strong>在主旨或本文</strong>&gt;<strong>主旨或內文中包含任何這些字詞</strong></p></td>
<td><p><em>SubjectOrBodyContainsWords</em></p>
<p><em>ExceptIfSubjectOrBodyContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p><strong>Subject</strong>欄位或郵件內文中含有指定的文字的郵件。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="even">
<td><p><strong>主旨或內文符合</strong></p>
<p><strong>在主旨或本文</strong>&gt;<strong>主旨或內文符合這些文字模式</strong></p></td>
<td><p><em>SubjectOrBodyMatchesPatterns</em></p>
<p><em>ExceptIfSubjectOrBodyMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>其中 patterns <strong>Subject</strong>欄位或郵件內文包含文字的郵件符合指定規則運算式。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>主旨包含</strong></p>
<p><strong>在主旨或本文</strong>&gt;<strong>主旨包含任何這些字詞</strong></p></td>
<td><p><em>SubjectContainsWords</em></p>
<p><em>ExceptIfSubjectContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>在 [ <strong>Subject</strong> ] 欄位中含有指定的文字的郵件。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="even">
<td><p><strong>主旨符合</strong></p>
<p><strong>在主旨或本文</strong>&gt;<strong>主旨符合這些文字模式</strong></p></td>
<td><p><em>SubjectMatchesPatterns</em></p>
<p><em>ExceptIfSubjectMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>其中<strong>Subject</strong>欄位包含文字模式符合指定規則運算式的郵件。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
</tbody>
</table>


返回頁首

## 附件

如需如何郵件流程規則檢查郵件附件的詳細資訊，請參閱[使用傳輸規則檢查郵件附件](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>條件或例外狀況在 EAC 中</th>
<th>Exchange 管理命令介面中的條件和例外狀況參數</th>
<th>屬性類型</th>
<th>描述</th>
<th>可用於</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>任何附件的內容包含</strong></p>
<p><strong>任何附件</strong>&gt;<strong>內容包含任何這些字詞</strong></p></td>
<td><p><em>AttachmentContainsWords</em></p>
<p><em>ExceptIfAttachmentContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>出附件包含指定的文字的郵件。</p></td>
<td><p>Exchange 2010或更新版本</p></td>
</tr>
<tr class="even">
<td><p><strong>任何附件內容符合</strong></p>
<p><strong>任何附件</strong>&gt;<strong>內容符合這些文字模式</strong></p></td>
<td><p><em>AttachmentMatchesPatterns</em></p>
<p><em>ExceptIfAttachmentMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>出附件包含文字模式符合指定規則運算式的郵件。</p>
<p><strong>請注意：</strong> 掃描僅第 150 kb 的附件。</p></td>
<td><p>Exchange 2010或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>無法檢查任何附件的內容</strong></p>
<p><strong>任何附件</strong>&gt;<strong>無法檢查內容</strong></p></td>
<td><p><em>AttachmentIsUnsupported</em></p>
<p><em>ExceptIfAttachmentIsUnsupported</em></p></td>
<td><p>不適用</p></td>
<td><p>其中附件原本就無法辨識Exchange，而不信箱伺服器上安裝必要的 IFilter 的郵件。如需詳細資訊，請參閱<a href="register-filter-pack-ifilters-with-exchange-2013-exchange-2013-help.md">對 Exchange 2013 註冊 Filter Pack IFilter</a>。</p></td>
<td><p>Exchange 2010或更新版本</p></td>
</tr>
<tr class="even">
<td><p><strong>任何附件的檔案名稱符合</strong></p>
<p><strong>任何附件</strong>&gt;<strong>檔案名稱符合這些文字模式</strong></p></td>
<td><p><em>AttachmentNameMatchesPatterns</em></p>
<p><em>ExceptIfAttachmentNameMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>出附件的檔案名稱中包含的文字模式符合指定規則運算式的郵件。</p></td>
<td><p>Exchange 2010或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>任何附件的副檔名符合</strong></p>
<p><strong>任何附件</strong>&gt;<strong>副檔名包括這些字詞</strong></p></td>
<td><p><em>AttachmentExtensionMatchesWords</em></p>
<p><em>ExceptIfAttachmentExtensionMatchesWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>如果有附件的副檔名符合任何指定文字的郵件。</p></td>
<td><p>Exchange 2013或更新版本</p></td>
</tr>
<tr class="even">
<td><p><strong>任何附件均大於或等於</strong></p>
<p><strong>任何附件 &gt; 大小為大於或等於</strong></p></td>
<td><p><em>AttachmentSizeOver</em></p>
<p><em>ExceptIfAttachmentSizeOver</em></p></td>
<td><p><code>Size</code></p></td>
<td><p>任何附件所在大於或等於指定值的郵件。</p>
<p>在 EAC 中，您可以只指定的大小 (kb)。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>郵件未完成掃描</strong></p>
<p><strong>任何附件</strong>&gt;<strong>未完成掃描</strong></p></td>
<td><p><em>AttachmentProcessingLimitExceeded</em></p>
<p><em>ExceptIfAttachmentProcessingLimitExceeded</em></p></td>
<td><p>不適用</p></td>
<td><p>讓規則引擎無法完成掃描附件的郵件。您可以使用這個條件來建立共同運作來識別及其中無法完全掃描內容會處理郵件的規則。</p></td>
<td><p>Exchange 2013或更新版本</p></td>
</tr>
<tr class="even">
<td><p><strong>任何附件都有可執行的內容</strong></p>
<p><strong>任何附件</strong>&gt;<strong>具有可執行內容</strong></p></td>
<td><p><em>AttachmentHasExecutableContent</em></p>
<p><em>ExceptIfAttachmentHasExecutableContent</em></p></td>
<td><p>不適用</p></td>
<td><p>附件是可執行檔的所在的郵件。系統會檢查檔案的內容而不是依賴檔案的副檔名。</p></td>
<td><p>Exchange 2013或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>所有附件均受密碼保護</strong></p>
<p><strong>任何附件</strong>&gt;<strong>受到密碼保護</strong></p></td>
<td><p><em>AttachmentIsPasswordProtected</em></p>
<p><em>ExceptIfAttachmentIsPasswordProtected</em></p></td>
<td><p>不適用</p></td>
<td><p>郵件其中附件均受密碼保護 （及無法掃描）。密碼偵測僅適用於Office文件及.zip 檔案。</p></td>
<td><p>Exchange 2013或更新版本</p></td>
</tr>
</tbody>
</table>


返回頁首

## 任何收件者

條件和例外狀況本節中的提供當郵件包含至少其中一個指定的收件者會影響*所有*收件者的唯一功能。例如，假設您已拒絕郵件的規則。如果您使用的收件者條件從 \[收件者\] 區段中，這些指定的收件者是只會拒絕該訊息。例如，如果規則找到指定的收件者的訊息，但郵件包含五個其他收件者。郵件被拒絕該一個收件者，並傳遞至五個其他收件者。

如果您從這個\] 區段中新增的收件者條件，該相同的郵件遭拒偵測到的收件者和五個其他收件者。

相反地，收件者例外狀況從此區段*可防止*從不只是為了偵測到的收件者套用到*所有*收件者的郵件之規則動作。

**注意事項：**這種情況並未考慮傳送至收件者 Proxy 位址的郵件。而只比對傳送至收件者主要電子郵件地址的郵件。


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>條件或例外狀況在 EAC 中</th>
<th>Exchange 管理命令介面中的條件和例外狀況參數</th>
<th>屬性類型</th>
<th>描述</th>
<th>可用於</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>任何收件者地址包含</strong></p>
<p><strong>任何收件者</strong>&gt;<strong>地址包含任何這些字詞</strong></p></td>
<td><p><em>AnyOfRecipientAddressContainsWords</em></p>
<p><em>ExceptIfAnyOfRecipientAddressContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>包含指定的文字的郵件<strong>To</strong>、 <strong>Cc</strong>或<strong>Bcc</strong>欄位中的郵件。</p></td>
<td><p>Exchange 2013或更新版本</p></td>
</tr>
<tr class="even">
<td><p><strong>任何收件者地址符合</strong></p>
<p><strong>任何收件者</strong>&gt;<strong>地址符合任何這些文字模式</strong></p></td>
<td><p><em>AnyOfRecipientAddressMatchesPatterns</em></p>
<p><em>ExceptIfAnyOfRecipientAddressMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>其中<strong>To</strong>、 <strong>Cc</strong>或<strong>Bcc</strong>欄位包含的文字模式符合指定規則運算式的郵件。</p></td>
<td><p>Exchange 2013或更新版本</p></td>
</tr>
</tbody>
</table>


返回頁首

## 為郵件敏感資訊類型和 \[副本\] 值、 大小和字元集

在這個條件\] 區段的外觀 for **To**和**Cc**欄位中的值的行為像任何收件者\] 區段中的條件 （*所有*收件者的郵件會受影響的規則，而不只是偵測到收件者）。

**注意事項：**這種情況並未考慮傳送至收件者 Proxy 位址的郵件。而只比對傳送至收件者主要電子郵件地址的郵件。


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>條件或例外狀況在 EAC 中</th>
<th>Exchange 管理命令介面中的條件和例外狀況參數</th>
<th>屬性類型</th>
<th>描述</th>
<th>可用於</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>郵件包含敏感資訊</strong></p>
<p><strong>郵件</strong>&gt;<strong>包含上述任何類型的敏感資訊</strong></p></td>
<td><p><em>MessageContainsDataClassifications</em></p>
<p><em>ExceptIfMessageContainsDataClassifications</em></p></td>
<td><p><code>SensitiveInformationTypes</code></p></td>
<td><p>包含機密資訊如資料遺失防護 (DLP) 原則所定義的郵件。</p>
<p>此條件，則需要使用<strong>通知寄件者以原則提示</strong>(<em>NotifySender</em>) 巨集指令的規則。</p></td>
<td><p>Exchange 2013或更新版本</p></td>
</tr>
<tr class="even">
<td><p><strong>[收件者] 方塊包含</strong></p>
<p><strong>郵件</strong>&gt;<strong>至] 方塊包含此人</strong></p></td>
<td><p><em>AnyOfToHeader</em></p>
<p><em>ExceptIfAnyOfToHeader</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>其中<strong>To</strong> ] 欄位包含任何指定收件者的郵件。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>[收件者] 方塊包含下列成員</strong></p>
<p><strong>郵件</strong>&gt;<strong>至] 方塊包含下列此群組的成員</strong></p></td>
<td><p><em>AnyOfToHeaderMemberOf</em></p>
<p><em>ExceptIfAnyOfToHeaderMemberOf</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>出<strong>To</strong>欄位包含收件者屬於指定之群組成員的郵件。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="even">
<td><p><strong>[副本] 方塊包含</strong></p>
<p><strong>郵件</strong>&gt; <strong>[副本] 方塊包含此人</strong></p></td>
<td><p><em>AnyOfCcHeader</em></p>
<p><em>ExceptIfAnyOfCcHeader</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>其中<strong>Cc</strong> ] 欄位包含任何指定收件者的郵件。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>[副本] 方塊包含下列的成員</strong></p>
<p><strong>郵件</strong>&gt;<strong>包含此群組的成員</strong></p></td>
<td><p><em>AnyOfCcHeaderMemberOf</em></p>
<p><em>ExceptIfAnyOfCcHeaderMemberOf</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>出<strong>Cc</strong>欄位包含收件者屬於指定之群組成員的郵件。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="even">
<td><p><strong>[收件者] 或 [副本] 方塊包含</strong></p>
<p><strong>郵件</strong>&gt;<strong>以或 [副本] 方塊包含此人</strong></p></td>
<td><p><em>AnyOfToCcHeader</em></p>
<p><em>ExceptIfAnyOfToCcHeader</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>其中<strong>To</strong>或<strong>Cc</strong>欄位包含任何指定收件者的郵件。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>[收件者] 或 [副本] 方塊包含下列的成員</strong></p>
<p><strong>郵件</strong>&gt;<strong>以或 [副本] 方塊包含此群組的成員</strong></p></td>
<td><p><em>AnyOfToCcHeaderMemberOf</em></p>
<p><em>ExceptIfAnyOfToCcHeaderMemberOf</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>其中<strong>To</strong>或<strong>Cc</strong>欄位包含收件者屬於指定之群組成員的郵件。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="even">
<td><p><strong>郵件大小大於或等於</strong></p>
<p><strong>郵件</strong>&gt;<strong>大小為大於或等於</strong></p></td>
<td><p><em>MessageSizeOver</em></p>
<p><em>ExceptIfMessageSizeOver</em></p></td>
<td><p><code>Size</code></p></td>
<td><p>其中的總大小 （郵件加上的附件） 是大於或等於指定值的郵件。</p>
<p>在 EAC 中，您可以只指定的大小 (kb)。</p>
<p><strong>請注意：</strong> 在信箱上的郵件大小限制的郵件流程規則之前評估。之前發生此情況的規則能夠處理郵件會被拒絕太大信箱的郵件。</p></td>
<td><p>Exchange 2013或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>郵件字元集名稱包含任何這些字詞</strong></p>
<p><strong>郵件</strong>&gt;<strong>字元集名稱包含任何這些字詞</strong></p></td>
<td><p><em>ContentCharacterSetContainsWords</em></p>
<p><em>ExceptIfContentCharacterSetContainsWords</em></p></td>
<td><p><code>CharacterSets</code></p></td>
<td><p>具有任何指定字元集的訊息設定名稱。</p></td>
<td><p>Exchange 2013或更新版本</p></td>
</tr>
</tbody>
</table>


返回頁首

## 寄件者和收件者


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>條件或例外狀況在 EAC 中</th>
<th>Exchange 管理命令介面中的條件和例外狀況參數</th>
<th>屬性類型</th>
<th>描述</th>
<th>可用於</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>寄件者是其中一個收件者</strong></p>
<p><strong>寄件者和收件者</strong>&gt;<strong>則收件者的寄件者的關聯</strong></p></td>
<td><p><em>SenderManagementRelationship</em></p>
<p><em>ExceptIfSenderManagementRelationship</em></p></td>
<td><p><code>ManagementRelationship</code></p></td>
<td><p>其中任一寄件者是收件者、 主管或寄件者受管理的收件者的郵件。</p></td>
<td><p>Exchange 2010或更新版本</p></td>
</tr>
<tr class="even">
<td><p><strong>郵件是在這些群組的成員之間</strong></p>
<p><strong>寄件者和收件者</strong>&gt;<strong>郵件是在這些群組的成員之間</strong></p></td>
<td><p><em>BetweenMemberOf1</em>和<em>BetweenMemberOf2</em></p>
<p><em>ExceptIfBetweenMemberOf1</em>和<em>ExceptIfBetweenMemberOf2</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>指定群組的成員之間傳送的郵件。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>寄件者或收件者的經理是</strong></p>
<p><strong>寄件者和收件者</strong>&gt;<strong>寄件者或收件者的經理是此人</strong></p></td>
<td><p><em>ManagerForEvaluatedUser</em>和<em>ManagerAddress</em></p>
<p><em>ExceptIfManagerForEvaluatedUser</em>和<em>ExceptIfManagerAddress</em></p></td>
<td><p>第一個屬性： <code>EvaluatedUser</code></p>
<p>第二個屬性： <code>Addresses</code></p></td>
<td><p>其中指定的使用者是寄件者、 主管或指定的使用者是收件者主管的郵件。</p></td>
<td><p>Exchange 2010或更新版本</p></td>
</tr>
<tr class="even">
<td><p><strong>寄件者與任何收件者的屬性比較結果為</strong></p>
<p><strong>寄件者和收件者</strong>&gt;<strong>寄件者和收件者的屬性比較結果為</strong></p></td>
<td><p><em>ADAttributeComparisonAttribute</em>和<em>ADComparisonOperator</em></p>
<p><em>ExceptIfADAttributeComparisonAttribute</em>和<em>ExceptIfADComparisonOperator</em></p></td>
<td><p>第一個屬性： <code>ADAttribute</code></p>
<p>第二個屬性： <code>Evaluation</code></p></td>
<td><p>其中的寄件者和收件者的指定的Active Directory屬性符合或不相符的郵件。</p></td>
<td><p>Exchange 2010或更新版本</p></td>
</tr>
</tbody>
</table>


返回頁首

## 郵件屬性


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>條件或例外狀況在 EAC 中</th>
<th>Exchange 管理命令介面中的條件和例外狀況參數</th>
<th>屬性類型</th>
<th>描述</th>
<th>可用於</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>郵件類型為</strong></p>
<p><strong>郵件內容</strong>&gt;<strong>包含郵件類型</strong></p></td>
<td><p><em>MessageTypeMatches</em></p>
<p><em>ExceptIfMessageTypeMatches</em></p></td>
<td><p><code>MessageType</code></p></td>
<td><p>將指定之類型的郵件。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當Outlook或Outlook Web App設定為郵件轉寄時， <strong>ForwardingSmtpAddress</strong>屬性已新增至郵件。郵件類型不被變更為<code>AutoForward</code>。</td>
</tr>
</tbody>
</table>

</td>
<td><p>Exchange 2010或更新版本</p></td>
</tr>
<tr class="even">
<td><p><strong>郵件被分類為</strong></p>
<p><strong>郵件內容</strong>&gt;<strong>包含此分類</strong></p></td>
<td><p><em>HasClassification</em></p>
<p><em>ExceptIfHasClassification</em></p></td>
<td><p><code>MessageClassification</code></p></td>
<td><p>已指定的郵件分類的郵件。這是可以在組織中使用<strong>New-MessageClassification</strong>指令程式來建立自訂的郵件分類。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>郵件未有任何分類標示</strong></p>
<p><strong>郵件內容</strong>&gt;<strong>不包含任何分類</strong></p></td>
<td><p><em>HasNoClassification</em></p>
<p><em>ExceptIfHasNoClassification</em></p></td>
<td><p>不適用</p></td>
<td><p>不具郵件分類的郵件。</p></td>
<td><p>Exchange 2010或更新版本</p></td>
</tr>
<tr class="even">
<td><p><strong>郵件的 SCL 大於或等於</strong></p>
<p><strong>郵件內容</strong>&gt;<strong>包含的 SCL 大於或等於</strong></p></td>
<td><p><em>SCLOver</em></p>
<p><em>ExceptIfSCLOver</em></p></td>
<td><p><code>SCLValue</code></p></td>
<td><p>出指派垃圾郵件信賴等級 (SCL) 大於或等於指定值的郵件。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>郵件重要性已設為</strong></p>
<p><strong>郵件內容</strong>&gt;<strong>包含的重要性層級</strong></p></td>
<td><p><em>WithImportance</em></p>
<p><em>ExceptIfWithImportance</em></p></td>
<td><p><code>Importance</code></p></td>
<td><p>指定的重要性層級標示的郵件。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
</tbody>
</table>


返回頁首

## 郵件標頭

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在主旨或郵件的其他標頭欄位中搜尋字詞或文字模式，會發生在郵件已從 MIME 內容傳輸編碼方法進行解碼<em>之後</em>，該編碼方法用來在 SMTP 伺服器之間傳送 ASCII 文字二進位訊息。您無法使用條件或例外狀況來搜尋主旨或郵件中其他標頭欄位的原始 (通常是 Base64) 編碼值。</td>
</tr>
</tbody>
</table>



<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>條件或例外狀況在 EAC 中</th>
<th>Exchange 管理命令介面中的條件和例外狀況參數</th>
<th>屬性類型</th>
<th>描述</th>
<th>可用於</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>郵件標頭包含</strong></p>
<p><strong>郵件標頭</strong>&gt;<strong>包含任何這些字詞</strong></p></td>
<td><p><em>HeaderContainsMessageHeader</em>和<em>HeaderContainsWords</em></p>
<p><em>ExceptIfHeaderContainsMessageHeader</em>和<em>ExceptIfHeaderContainsWords</em></p></td>
<td><p>第一個屬性： <code>MessageHeaderField</code></p>
<p>第二個屬性： <code>Words</code></p></td>
<td><p>包含指定的標頭] 欄位中，而該標頭欄位的值的郵件會包含指定的文字。</p>
<p>永遠一起使用的標頭欄位的名稱及標頭欄位的值。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="even">
<td><p><strong>郵件標頭符合</strong></p>
<p><strong>郵件標頭</strong>&gt;<strong>符合這些文字模式</strong></p></td>
<td><p><em>HeaderMatchesMessageHeader</em>和<em>HeaderMatchesPatterns</em></p>
<p><em>ExceptIfHeaderMatchesMessageHeader</em>和<em>ExceptIfHeaderMatchesPatterns</em></p></td>
<td><p>第一個屬性： <code>MessageHeaderField</code></p>
<p>第二個屬性： <code>Patterns</code></p></td>
<td><p>包含指定的標頭] 欄位中，而該標頭欄位的值的郵件會包含指定的規則運算式。</p>
<p>永遠一起使用的標頭欄位的名稱及標頭欄位的值。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
</tbody>
</table>


返回頁首

## 條件和例外狀況的 Edge Transport server 上的郵件流程規則

條件和例外狀況 Edge Transport server 上的郵件流程規則中可使用的是什麼是可在信箱伺服器上的小型子集。您只可以管理中Exchange 管理命令介面本機 Edge Transport server 上的郵件流程規則讓 Edge Transport server 上有無 EAC。條件和例外狀況下表所述。在 \[屬性類型\] 區段中說明的內容類型。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange 管理命令介面中的條件和例外狀況參數</th>
<th>屬性類型</th>
<th>描述</th>
<th>可用於</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>AnyOfRecipientAddressContainsWords</em></p>
<p><em>ExceptIfAnyOfRecipientAddressContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>包含<strong>To</strong>、 <strong>Cc</strong>或<strong>Bcc</strong>欄位中的指定的文字的郵件。</p>
<p>當郵件含有指定收件者時，規則動作是套用 （或不會套用） 給<em>所有</em>收件者的郵件。例如，郵件遭拒的所有收件者的郵件而不只是針對指定的收件者。</p></td>
<td><p>Exchange 2013或更新版本</p></td>
</tr>
<tr class="even">
<td><p><em>AnyOfRecipientAddressMatchesPatterns</em></p>
<p><em>ExceptIfAnyOfRecipientAddressMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>其中<strong>To</strong>、 <strong>Cc</strong>或<strong>Bcc</strong>欄位包含的文字模式符合指定規則運算式的郵件。</p>
<p>當郵件含有指定收件者時，規則動作是套用 （或不會套用） 給<em>所有</em>收件者的郵件。例如，郵件遭拒的所有收件者的郵件而不只是針對指定的收件者。</p></td>
<td><p>Exchange 2013或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><em>AttachmentSizeOver</em></p>
<p><em>ExceptIfAttachmentSizeOver</em></p></td>
<td><p><code>Size</code></p></td>
<td><p>任何附件大於或等於指定值所在的附件的郵件。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="even">
<td><p><em>FromAddressContainsWords</em></p>
<p><em>ExceptIfFromAddressContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>包含寄件者的電子郵件地址中指定的文字的郵件。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><em>FromAddressMatchesPatterns</em></p>
<p><em>ExceptIfFromAddressMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>出寄件者的電子郵件地址中包含的文字模式符合指定規則運算式的郵件。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="even">
<td><p><em>FromScope</em></p>
<p><em>ExceptIfFromScope</em></p></td>
<td><p><code>UserScopeFrom</code></p></td>
<td><p>由內部的寄件者或外部寄件者所傳送的郵件。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><em>HeaderContainsMessageHeader</em>和<em>HeaderContainsWords</em></p>
<p><em>ExceptIfHeaderContainsMessageHeader</em>和<em>ExceptIfHeaderContainsWords</em></p></td>
<td><p>第一個屬性： <code>MessageHeaderField</code></p>
<p>第二個屬性： <code>Words</code></p></td>
<td><p>包含指定的標頭] 欄位中，而該標頭欄位的值的郵件會包含指定的文字。</p>
<p>永遠一起使用的標頭欄位的名稱及標頭欄位的值。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="even">
<td><p><em>HeaderMatchesMessageHeader</em>和<em>HeaderMatchesPatterns</em></p>
<p><em>ExceptIfHeaderMatchesMessageHeader</em>和<em>ExceptIfHeaderMatchesPatterns</em></p></td>
<td><p>第一個屬性： <code>MessageHeaderField</code></p>
<p>第二個屬性： <code>Patterns</code></p></td>
<td><p>包含指定的標頭] 欄位中，而該標頭欄位的值的郵件會包含指定的規則運算式。</p>
<p>永遠一起使用的標頭欄位的名稱及標頭欄位的值。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><em>MessageSizeOver</em></p>
<p><em>ExceptIfMessageSizeOver</em></p></td>
<td><p><code>Size</code></p></td>
<td><p>其中的總大小 （郵件加上的附件） 是大於或等於指定值的郵件。</p></td>
<td><p>Exchange 2013或更新版本</p></td>
</tr>
<tr class="even">
<td><p><em>SCLOver</em></p>
<p><em>ExceptIfSCLOver</em></p></td>
<td><p><code>SCLValue</code></p></td>
<td><p>指派給 SCL 大於或等於指定值的郵件。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><em>SubjectContainsWords</em></p>
<p><em>ExceptIfSubjectContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>包含指定的文字的<strong>Subject</strong>欄位中的郵件。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="even">
<td><p><em>SubjectMatchesPatterns</em></p>
<p><em>ExceptIfSubjectMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>其中<strong>Subject</strong>欄位包含文字模式符合指定規則運算式的郵件。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="odd">
<td><p><em>SubjectOrBodyContainsWords</em></p>
<p><em>ExceptIfSubjectOrBodyContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>包含指定的文字<strong>Subject</strong>欄位或郵件內文中的郵件。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
<tr class="even">
<td><p><em>SubjectOrBodyMatchesPatterns</em></p>
<p><em>ExceptIfSubjectOrBodyMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>其中 patterns <strong>Subject</strong>欄位或郵件內文包含文字的郵件符合指定規則運算式。</p></td>
<td><p>Exchange 2007或更新版本</p></td>
</tr>
</tbody>
</table>


返回頁首

## 屬性類型

下表說明可用的條件和例外狀況的屬性類型。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果此內容是字串，則尾端不能有空格。</td>
</tr>
</tbody>
</table>



<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>屬性類型</th>
<th>有效值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>ADAttribute</code></p></td>
<td><p>從預先定義的Active Directory屬性清單中選取</p></td>
<td><p>UNRESOLVED_TOKENBLOCK_VAL(PD_Transport_Rules_ADAttributes_Snippet)</p>
<p>在 EAC 中，若要指定多個字或文字模式相同的屬性、 值以逗號隔開。例如值<strong>金山、 Palo AltoCity</strong>屬性會尋找&quot;-市/鎮等於金山&quot;或-市/鎮等於 Palo Alto&quot;。</p>
<p>在Exchange 管理命令介面中，使用語法<code>&quot;AttributeName1:Value1,Value 2 with spaces,Value3...&quot;,&quot;AttributeName2:Word4,Value 5 with spaces,Value6...&quot;</code><code>Value</code>其中是您想要比對字或文字模式。</p>
<p>例如， <code>&quot;City:San Francisco,Palo Alto&quot;</code>或<code>&quot;City:San Francisco,Palo Alto&quot;</code>、<code>&quot;Department:Sales,Finance&quot;</code>。</p>
<p>當您指定多個屬性或多個相同的屬性值時，會使用<strong>or</strong>運算子。不搭配值前置空格或尾端空格。</p>
<p>請注意<strong>Country</strong>屬性需要兩個字母 ISO 3166-1 國家/地區碼值 (例如 DE 德國)。若要搜尋的值，請參閱 ＜ <a href="https://go.microsoft.com/fwlink/p/?linkid=331680">https://go.microsoft.com/fwlink/p/?LinkId=331680</a>。</p></td>
</tr>
<tr class="even">
<td><p><code>Addresses</code></p></td>
<td><p>Exchange收件者</p></td>
<td><p>根據條件或例外狀況的性質，您可以指定 （例如收件者相關條件），在組織中任何具有郵件功能的物件或您可能會限制在特定的物件類型 （例如群組的群組成員資格條件）。與條件或例外狀況可能需要一個值，或允許多個值。</p>
<p>在Exchange 管理命令介面，請以逗點分隔多個值。</p>
<p><strong>注意事項：</strong>這種情況並未考慮傳送至收件者 Proxy 位址的郵件。而只比對傳送至收件者主要電子郵件地址的郵件。</p></td>
</tr>
<tr class="odd">
<td><p><code>CharacterSets</code></p></td>
<td><p>字元集名稱的陣列</p></td>
<td><p>在郵件中存在的一或多個內容的字元組。例如：</p>
<ul>
<li><p><code>Arabic/iso-8859-6</code></p></li>
<li><p><code>Chinese/big5</code></p></li>
<li><p><code>Chinese/euc-cn</code></p></li>
<li><p><code>Chinese/euc-tw</code></p></li>
<li><p><code>Chinese/gb2312</code></p></li>
<li><p><code>Chinese/iso-2022-cn</code></p></li>
<li><p><code>Cyrillic/iso-8859-5</code></p></li>
<li><p><code>Cyrillic/koi8-r</code></p></li>
<li><p><code>Cyrillic/windows-1251</code></p></li>
<li><p><code>Greek/iso-8859-7</code></p></li>
<li><p><code>Hebrew/iso-8859-8</code></p></li>
<li><p><code>Japanese/euc-jp</code></p></li>
<li><p><code>Japanese/iso-022-jp</code></p></li>
<li><p><code>Japanese/shift-jis</code></p></li>
<li><p><code>Korean/euc-kr</code></p></li>
<li><p><code>Korean/johab</code></p></li>
<li><p><code>Korean/ks_c_5601-1987</code></p></li>
<li><p><code>Turkish/windows-1254</code></p></li>
<li><p><code>Turkish/iso-8859-9</code></p></li>
<li><p><code>Vietnamese/tcvn</code></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code>DomainName</code></p></td>
<td><p>SMTP 網域的陣列</p></td>
<td><p>例如， <code>contoso.com</code>或<code>eu.contoso.com</code>。</p>
<p>在Exchange 管理命令介面中，您可以指定多個以逗號分隔的網域。</p></td>
</tr>
<tr class="odd">
<td><p><code>EvaluatedUser</code></p></td>
<td><p><strong>寄件者</strong>或<strong>收件者</strong>的單一值</p></td>
<td><p>會指定是否要尋找之主管的寄件者或收件者主管的規則。</p></td>
</tr>
<tr class="even">
<td><p><code>Evaluation</code></p></td>
<td><p><strong>等於</strong>或<strong>不等於</strong>(<code>NotEqual</code>) 的單一值</p></td>
<td><p>當比較寄件者和收件者的Active Directory屬性，這會指定值是否應相符，或不相符。</p></td>
</tr>
<tr class="odd">
<td><p><code>Importance</code></p></td>
<td><p><strong>Low</strong>、<strong>標準模式</strong>、 或<strong>高</strong>的單一值</p></td>
<td><p>指定給郵件寄件者Outlook或Outlook Web App重要性層級。</p></td>
</tr>
<tr class="even">
<td><p><code>IPAddressRanges</code></p></td>
<td><p>IP 位址或位址範圍的陣列</p></td>
<td><p>您可以輸入 IPv4 位址使用下列語法：</p>
<ul>
<li><p><strong>單一 IP 位址</strong>  例如， <code>192.168.1.1</code>。</p></li>
<li><p><strong>IP 位址範圍</strong>  例如， <code>192.168.0.1-192.168.0.254</code>。</p></li>
<li><p><strong>無類別網域間路由選擇 (CIDR) IP 位址範圍</strong>  例如， <code>192.168.0.1/25</code>。</p></li>
</ul>
<p>在Exchange 管理命令介面中，您可以指定多個 IP 位址或以逗號分隔的範圍。</p></td>
</tr>
<tr class="odd">
<td><p><code>ManagementRelationship</code></p></td>
<td><p><strong>Manager</strong>或<strong>直屬</strong>(<code>DirectReport</code>) 的單一值</p></td>
<td><p>會指定寄件者與任何收件者之間的關係。此規則會檢查中看到如果寄件者是收件者、 主管或寄件者收件者管理Active Directory<strong>Manager</strong>屬性。</p></td>
</tr>
<tr class="even">
<td><p><code>MessageClassification</code></p></td>
<td><p>單一郵件分類</p></td>
<td><p>在 EAC 中，從清單中選取的已建立的郵件分類。</p>
<p>在Exchange 管理命令介面中，您可以使用<strong>Get-MessageClassification</strong>指令程式來識別的郵件分類。例如，使用下列命令來搜尋<code>Company Internal</code>分類的郵件並搭配值<code>CompanyInternal</code>在郵件主旨前面加上。</p>
<p><code>New-TransportRule &quot;Rule Name&quot; -HasClassification @(Get-MessageClassification &quot;Company Internal&quot;).Identity -PrependSubject &quot;CompanyInternal&quot;</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MessageHeaderField</code></p></td>
<td><p>單一字串</p></td>
<td><p>指定的標頭欄位的名稱。標頭欄位的名稱一律成對的標頭欄位 （word 或文字模式符合） 中的值。</p>
<p><em>郵件標頭</em>是在郵件中的必要及選用的標頭欄位的集合。標頭欄位的範例是<strong>To</strong>、 <strong>From</strong>、 <strong>Received</strong>及<strong>Content-Type</strong>。官方的標頭欄位定義於 RFC 5322。非公務標頭欄位開頭<strong>X-</strong>和稱為<em>X 標頭</em>。</p></td>
</tr>
<tr class="even">
<td><p><code>MessageType</code></p></td>
<td><p>單一郵件類型值</p></td>
<td><p>指定下列其中一個下列郵件類型：</p>
<ul>
<li><p><strong>自動回覆</strong>(<code>OOF</code>)</p></li>
<li><p><strong>自動轉寄</strong>(<code>AutoForward</code>)</p></li>
<li><p><strong>加密</strong></p></li>
<li><p><strong>行事曆</strong></p></li>
<li><p><strong>控制 」 權限</strong>(<code>PermissionControlled</code>)</p></li>
<li><p><strong>語音信箱</strong></p></li>
<li><p><strong>簽署</strong></p></li>
<li><p><strong>核准要求</strong>(<code>ApprovalRequest</code>)</p></li>
<li><p><strong>讀取回條</strong>(<code>ReadReceipt</code>)</p></li>
</ul>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當Outlook或Outlook Web App設定為郵件轉寄時， <strong>ForwardingSmtpAddress</strong>屬性已新增至郵件。郵件類型不被變更為<code>AutoForward</code>。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="odd">
<td><p><code>Patterns</code></p></td>
<td><p>規則運算式的陣列</p></td>
<td><p>指定一或多個規則運算式用來識別值中的文字模式。如需詳細資訊，請參閱<a href="https://go.microsoft.com/fwlink/p/?linkid=180327">規則運算式語法</a>。</p>
<p>在Exchange 管理命令介面中，指定多個以逗號分隔的規則運算式，您以引號 （&quot;） 括住每一個規則運算式。</p></td>
</tr>
<tr class="even">
<td><p><code>SCLValue</code></p></td>
<td><p>下列其中一個值：</p>
<ul>
<li><p><strong>略過垃圾郵件篩選</strong>(<code>-1</code>)</p></li>
<li><p>整數 0 到 9</p></li>
</ul></td>
<td><p>會指定指派給郵件的垃圾郵件信賴等級 (SCL)。較高的 SCL 值表示郵件更多可能是垃圾郵件。</p></td>
</tr>
<tr class="odd">
<td><p><code>SensitiveInformationTypes</code></p></td>
<td><p>敏感資訊類型的陣列</p></td>
<td><p>會指定您組織中所定義的一或多個敏感資訊類型。如需內建的敏感資訊類型的清單，請參閱<a href="what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md">在 Exchange 中的敏感資訊類型外觀</a>。</p>
<p>在Exchange 管理命令介面中，使用語法<code>@{&lt;SensitiveInformationType1&gt;},@{&lt;SensitiveInformationType2&gt;},...</code>。例如，若要尋找包含至少兩種信用卡數字及至少一個阿拉巴馬州路由號碼的內容，使用值<code>@{Name=&quot;Credit Card Number&quot;; minCount=&quot;2&quot;},@{Name=&quot;ABA Routing Number&quot;; minCount=&quot;1&quot;}</code>。</p></td>
</tr>
<tr class="even">
<td><p><code>Size</code></p></td>
<td><p>單一大小] 值</p></td>
<td><p>指定附件或整個郵件的大小。</p>
<p>在 EAC 中，您可以只指定的大小 (kb)。</p>
<p>在Exchange 管理命令介面中，當您輸入的值，請來限定值使用其中一個單位：</p>
<ul>
<li><p><code>B</code> (位元組)</p></li>
<li><p><code>KB</code> (KB)</p></li>
<li><p><code>MB</code> (MB)</p></li>
<li><p><code>GB</code> (GB)</p></li>
</ul>
<p>例如，<code>20MB</code></p>
<p>未限定的值通常會被視為位元組，但較小的值可能會進位至最接近的 KB。</p></td>
</tr>
<tr class="odd">
<td><p><code>UserScopeFrom</code></p></td>
<td><p><strong>在組織內</strong>(<code>InOrganization</code>) 或<strong>組織外</strong>(<code>NotInOrganization</code>) 的單一值</p></td>
<td><p>寄件者會被視為在組織內其中一個符合下列條件成立時：</p>
<ul>
<li><p>寄件者是信箱、 郵件使用者、 群組或擁有郵件功能的公用資料夾存在於組織Active Directory中。</p></li>
<li><p>寄件者的電子郵件地址是中公認的網域設定為授權網域] 或 [內部轉送網域，<strong>並</strong>將郵件已傳送或接收透過未經過驗證的連線。如需公認的網域的詳細資訊，請參閱<a href="accepted-domains-exchange-2013-help.md">公認的網域</a>。</p></li>
</ul>
<p>寄件者會被視為組織外部的其中一個符合下列條件成立時：</p>
<ul>
<li><p>寄件者的電子郵件地址不在公認的網域。</p></li>
<li><p>寄件者的電子郵件地址是設定為外部轉送網域的公認網域中。</p></li>
</ul>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要判斷郵件連絡人會被視為內部或外部組織，寄件者地址會比較與組織的公認網域。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p><code>UserScopeTo</code></p></td>
<td><p>下列其中一個值：</p>
<ul>
<li><p><strong>在組織內</strong>(<code>InOrganization</code>)</p></li>
<li><p><strong>組織外</strong>(<code>NotInOrganization</code>)</p></li>
<li><p><strong>外部合作夥伴組織中</strong>(<code>ExternalPartner</code>)</p></li>
<li><p><strong>外部非協力廠商組織中</strong>(<code>ExternalNonPartner</code>)</p></li>
</ul></td>
<td><p>收件者會被視為在組織內其中一個符合下列條件成立時：</p>
<ul>
<li><p>收件者是信箱、 郵件使用者、 群組或擁有郵件功能的公用資料夾存在於組織Active Directory中。</p></li>
<li><p>收件者的電子郵件地址是中公認的網域設定為授權網域] 或 [內部轉送網域，<strong>並</strong>將郵件已傳送或接收透過未經過驗證的連線。</p></li>
</ul>
<p>收件者會被視為組織外部的其中一個符合下列條件成立時：</p>
<ul>
<li><p>收件者的電子郵件地址不在公認的網域。</p></li>
<li><p>收件者的電子郵件地址是設定為外部轉送網域的公認網域中。</p></li>
</ul>
<p>外部合作夥伴組織是您已在此設定將郵件傳送的網域安全性 （相互驗證 TLS） 的外部網域。</p>
<p>外部非合作夥伴組織的所有其他的外部網域不被視為協力廠商網域。</p></td>
</tr>
<tr class="odd">
<td><p><code>Words</code></p></td>
<td><p>字串陣列</p></td>
<td><p>指定一或多個要尋找的文字。單字不區分大小寫，並可圍繞空格和標點符號。不支援萬用字元和部分相符項目。</p>
<p>例如，&quot;contoso&quot;找出 「 Contoso 」。。不過，如果圍繞其他任何字元的文字，它不被視為相符項目。例如，&quot;contoso&quot;不符合下列值：</p>
<ul>
<li><p>Acontoso</p></li>
<li><p>Contosoa</p></li>
<li><p>Acontosob</p></li>
</ul>
<p>星號 （*） 會被視為常值的字元，並不當做萬用字元。</p></td>
</tr>
</tbody>
</table>


返回頁首

## 相關資訊

[郵件流程或傳輸規則](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[傳輸規則動作](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md)

[郵件流程或傳輸規則程序](mail-flow-or-transport-rule-procedures-exchange-2013-help.md)

針對Exchange Online[Exchange Online 中的郵件流程規則條件和例外狀況 (predicates)](https://technet.microsoft.com/zh-tw/library/jj919235\(v=exchg.150\))

針對Exchange Online Protection[郵件流程規則條件和例外狀況 （述詞） 在 \[Exchange Online Protection](https://technet.microsoft.com/zh-tw/library/jj919234\(v=exchg.150\))

