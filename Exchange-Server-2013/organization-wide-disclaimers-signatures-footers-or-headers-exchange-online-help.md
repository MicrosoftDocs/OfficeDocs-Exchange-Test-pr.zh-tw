---
title: '整個組織的免責聲明、簽章、頁尾或標頭: Exchange 2013 Help'
TOCTitle: 整個組織的免責聲明、簽章、頁尾或標頭
ms:assetid: e45e33c9-e53b-427c-ada5-70901bc399b8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn600437(v=EXCHG.150)
ms:contentKeyID: 61060479
ms.date: 01/01/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 整個組織的免責聲明、簽章、頁尾或標頭

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

您可以新增電子郵件免責聲明、法律免責聲明、公開揭示聲明、簽章或其他資訊到進入或離開您的組織的電子郵件訊息的頂端或底部。法律、商務或法規需求可能需要這些項目，來識別可能不安全的電子郵件訊息，或針對您的組織獨特的其他理由。

若要設定免責聲明，您可以建立傳輸規則，其中包含條件，例如當寄件者在特定群組時，或者當訊息包含特定文字模式以及要加入的文字時。若要將多個免責聲明套用至單一電子郵件，您使用多個傳輸規則。

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>如果您只想要在外寄郵件中新增訊息，您必須新增條件，例如收件者位於組織外部。根據預設，傳輸規則套用至內送和外寄郵件。</p></li>
</ul></td>
</tr>
</tbody>
</table>


**目錄**

範例

設定免責聲明的範圍

格式化免責聲明

無法加入免責聲明時的後援選項

相關資訊

正在尋找程序嗎？請參閱[整個組織的郵件免責聲明、 簽章、 頁尾或 Office 365 中的標頭](https://technet.microsoft.com/zh-tw/library/dn600323\(v=exchg.150\))。

## 範例

以下是一些如何使用免責聲明的想法。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>類型</th>
<th>已新增的範例文字</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>法律 – 外寄郵件</p></td>
<td><p>這封電子郵件和與它一起傳輸的任何檔案都是機密的，僅限所傳送的個人或實體使用。如果您錯誤地收到這封電子郵件，請通知系統管理員。</p></td>
</tr>
<tr class="even">
<td><p>法律 – 內送郵件</p></td>
<td><p>員工明確被要求不要做誹謗性聲明，也不要對電子郵件通訊的任何其他法律權限的版權造成侵害或侵權。收到這類電子郵件的員工必須立即通知其主管。</p></td>
</tr>
<tr class="odd">
<td><p>請注意，該訊息已傳送至別名</p></td>
<td><p>此訊息已傳送給「業務」討論群組。</p></td>
</tr>
<tr class="even">
<td><p>簽章 – 提取每位員工的資料</p></td>
<td><p>Kathleen Mayer<br />
業務部門<br />
Contoso<br />
www.contoso.com<br />
kathleen@contoso.com<br />
儲存格︰111-222-1234</p></td>
</tr>
<tr class="odd">
<td><p>廣告</p></td>
<td><p>請按一下這裡以取得 3 月特殊項目</p></td>
</tr>
</tbody>
</table>


這份文件中的範例不適合以原本的樣式使用。針對您的需求修改它們。

## 設定免責聲明的範圍

當您使用您的免責聲明時，請考慮它們應該套用到哪些郵件。例如，您可能想要針對內部與外部郵件，或是特定部門中的使用者所傳送的郵件，使用不同的免責聲明。若要確定只有對話中的第一個訊息取得免責聲明，新增例外狀況，在免責聲明中尋找唯一文字。

以下是一些您可以使用的條件及例外狀況的範例。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>描述</th>
<th>EAC 中的條件及例外狀況</th>
<th>Shell 中的條件及例外狀況</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>在組織外，如果原始訊息並不包含免責聲明的文字，例如「CONTOSO 法律注意事項」</p></td>
<td><p>條件：<strong>收件者位於</strong> &gt; <strong>在組織外</strong></p>
<p>例外狀況：<strong>主旨或內文</strong> &gt; <strong>主旨或內文符合這些文字模式</strong> &gt; <strong>CONTOSO 法律注意事項</strong></p></td>
<td><pre><code>-FromScope NotInOrganization -ExceptIf -SubjectOrBodyMatches &quot;CONTOSO LEGAL NOTICE&quot;</code></pre></td>
</tr>
<tr class="even">
<td><p>內送郵件具有可執行檔附件</p></td>
<td><p>條件 1：<strong>寄件者位於</strong> &gt; <strong>組織外部</strong></p>
<p>條件 2：<strong>任何附件</strong> &gt; <strong>具有可執行的內容</strong></p></td>
<td><pre><code>-FromScope NotInOrganization -AttachmentHasExecutableContent</code></pre></td>
</tr>
<tr class="odd">
<td><p>寄件者在行銷部門中</p></td>
<td><p>條件：<strong>寄件者</strong> &gt; <strong>是此群組的成員</strong> &gt; <strong>群組名稱</strong></p></td>
<td><pre><code>-FromMemberOf &quot;Marketing Team&quot;</code></pre></td>
</tr>
<tr class="even">
<td><p>來自外部寄件者給銷售討論群組的每個訊息</p></td>
<td><p>條件 1：<strong>寄件者位於</strong> &gt; <strong>組織外部</strong></p>
<p>條件 2：<strong>訊息</strong> &gt; <strong>收件者或副本方塊包含此人員</strong> &gt; <strong>群組名稱</strong></p></td>
<td><pre><code>-FromScope NotInOrganization -SentTo &quot;Sales Discussion Group&quot; -PrependSubject &quot;Sent to Sales Discussion Group: &quot;</code></pre></td>
</tr>
<tr class="odd">
<td><p>在外寄郵件前面加上廣告一個月</p></td>
<td><p>條件 1：<strong>收件者位於</strong> &gt; <strong>在組織外</strong></p>
<p>在 [<strong>新規則</strong>] 對話方塊的底部指定日期。</p></td>
<td><p>-ApplyHtmlDisclaimerLocation 'Prepend' -SentToScope 'NotInOrganization' –ActivationDate ‘03/1/2014’ –ExpiryDate ‘03/31/2014’</p></td>
</tr>
</tbody>
</table>


如需您可以用來作為免責聲明的傳輸規則條件的完整清單，請參閱下列其中一項：

  - [Exchange Online 中的郵件流程規則條件和例外狀況 (predicates)](https://technet.microsoft.com/zh-tw/library/jj919235\(v=exchg.150\)) (Exchange Online)

  - [傳輸規則條件 （述詞）](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md) (Exchange 2013)

  - [Exchange Online 中的郵件流程規則條件和例外狀況 (predicates)](https://technet.microsoft.com/zh-tw/library/jj919235\(v=exchg.150\)) (Exchange Online Protection)

## 格式化免責聲明

您可以視需要來格式化您的免責聲明。以下是可以包含在免責聲明文字中的項目。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>資訊類型</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>文字</p></td>
<td><p>最大長度是 5000 個字元，包括任何 HTML 標記和內嵌階層式樣式表 (CSS)。</p></td>
</tr>
<tr class="even">
<td><p>HTML 和內嵌 CSS</p></td>
<td><p>您可以使用 HTML 和內嵌 CSS 樣式來格式化文字。例如，使用 <code>&lt;HR&gt;</code> 標記以在免責聲明前新增一行。</p>
<p>如果免責聲明是新增至純文字訊息，則會忽略在免責聲明中的 HTML。</p></td>
</tr>
<tr class="odd">
<td><p>新增影像</p></td>
<td><p>使用 <code>&lt;IMG&gt;</code> 標記指向在網際網路上可用的影像。例如，<code>&lt;IMG src=&quot;http://contoso.com/images/companylogo.gif&quot; alt=&quot;Contoso logo&quot;&gt;</code></p>
<p>請記住，根據預設 Outlook Web App 和 Outlook 會封鎖外部 Web 內容，包括影像。如果使用者想要檢視封鎖的外部內容，可能需要執行特定動作。這表示使用 <code>IMG</code> 標記新增的影像預設可能無法顯示。建議您使用您的收件者可能會在電子郵件用戶端中使用的 <code>IMG</code> 標記，來測試免責聲明，以確定影像顯示良好。</p></td>
</tr>
<tr class="even">
<td><p>新增個人化簽章的資訊</p></td>
<td><p>如果您希望每個人具有以相同方式格式化且具有相同資訊的簽章，您可以為每位員工新增唯一的資訊，例如<code>DisplayName</code>、<code>FirstName</code>、<code>LastName</code>、<code>PhoneNumber</code>、<code>Email</code>、<code>FaxNumber</code> 和 <code>Department</code>。這項資訊必須包含在資訊每一邊的兩個百分比符號 (%%) 內。例如，若要使用 <code>DisplayName</code>，您必須在免責聲明中使用 <strong>%%DisplayName%%</strong>。</p>
<p>觸發免責聲明規則時，就會插入該使用者的對應值。來自寄件者的 Active Directory 使用者帳戶的資料 (針對內部部署 Exchange Server)，或來自 Exchange Online 的寄件者的 Office 365 帳戶的資料。</p>
<p>如需免責聲明與個人化簽章中可以使用的完整屬性清單，請參閱 <a href="mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md">傳輸規則條件 （述詞）</a> (Exchange Server)、<a href="https://technet.microsoft.com/zh-tw/library/jj919235(v=exchg.150)">Exchange Online 中的郵件流程規則條件和例外狀況 (predicates)</a> (Exchange Online) 或 <a href="https://technet.microsoft.com/zh-tw/library/jj919234(v=exchg.150)">郵件流程規則條件和例外狀況 （述詞） 在 [Exchange Online Protection</a> (Exchange Online Protection) 中 <code>ADAttribute</code> 屬性的描述。</p></td>
</tr>
</tbody>
</table>


例如，以下是包含簽章、`IMG` 標記和內嵌 CSS 的 HTML 免責聲明的範例。

    <div style="font-size:9pt;  font-family: 'Calibri',sans-serif;">
    %%displayname%%</br>
    %%title%%</br>
    %%company%%</br>
    %%street%%</br>
    %%city%%, %%state%% %%zipcode%%</div>
    &nbsp;</br>
    <div style="background-color:#D5EAFF; border:1px dotted #003333; padding:.8em; ">
    <div><img alt="Fabrikam"  src="http://fabrikam.com/images/fabrikamlogo.png"></div>
    <span style="font-size:12pt;  font-family: 'Cambria','times new roman','garamond',serif; color:#ff0000;">HTML Disclaimer Title</span></br>
    <p style="font-size:8pt; line-height:10pt; font-family: 'Cambria','times roman',serif;">This message contains confidential information and is intended only for the individual(s) addressed in the message. If you are not the named addressee, you should not disseminate, distribute, or copy this e-mail. If you are not the intended recipient, you are notified that disclosing, distributing, or copying this e-mail is strictly prohibited.  </p>
    <span style="padding-top:10px; font-weight:bold; color:#CC0000; font-size:10pt; font-family: 'Calibri',Arial,sans-serif; "><a href="http://www.fabrikam.com">Fabrikam, Inc. </a></span></br></br>
    </div>

## 無法加入免責聲明時的後援選項

有些郵件 (例如加密的郵件) 會防止 Exchange 修改原始郵件的內容。您可以控制組織處理郵件的方式。您指定是否要將無法修改的郵件包在含有免責聲明的郵件信封中、拒絕無法新增免責聲明的郵件，或是在沒有免責聲明的情況下忽略免責聲明或傳送郵件。

下列清單說明每個後援動作：

  - **包裝**   如果無法將免責聲明插入原始郵件中，Exchange 會將原始郵件包住或包裝在新的郵件信封中，然後再將免責聲明插入新郵件中。如果無法將原始郵件包裝到新郵件信封中，將不會傳送原始郵件。郵件的寄件者會收到未傳遞回報 (NDR)，解釋郵件未傳遞的原因。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果原始郵件包裝在新的郵件信封中，則會將後續的傳輸規則套用到新郵件信封，而不是套用到原始郵件。 因此在您設定其他傳輸規則後，必須設定免責聲明動作會將原始郵件包在新郵件內文的傳輸規則。</td>
    </tr>
    </tbody>
    </table>


  - **Reject**   如果無法將免責聲明插入原始郵件中，Exchange 就不會傳送郵件。郵件的寄件者會收到 NDR，解釋郵件未傳遞的原因。

  - **Ignore**   如果無法將免責聲明插入原始郵件中，Exchange 會處理郵件，不進行任何修改。不會加入任何免責聲明。

## 相關資訊

[整個組織的郵件免責聲明、 簽章、 頁尾或 Office 365 中的標頭](https://technet.microsoft.com/zh-tw/library/dn600323\(v=exchg.150\))

[郵件流程或傳輸規則](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange Server 2013)

[Exchange Online 中的郵件流程規則 (傳輸規則)](https://technet.microsoft.com/zh-tw/library/jj919238\(v=exchg.150\)) (Exchange Online)

[Exchange Online Protection 中的郵件流程規則 (傳輸規則)](https://technet.microsoft.com/zh-tw/library/dn271424\(v=exchg.150\)) (Exchange Online Protection)

