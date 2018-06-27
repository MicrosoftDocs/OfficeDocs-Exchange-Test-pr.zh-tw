---
title: '使用 Outlook Web App 網頁組件: Exchange 2013 Help'
TOCTitle: 使用 Outlook Web App 網頁組件
ms:assetid: 7272e3ab-430c-4d6c-8621-9535236ce463
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Mt574711(v=EXCHG.150)
ms:contentKeyID: 70076143
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用 Outlook Web App 網頁組件

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-07-31_

您可使用MicrosoftOfficeOutlook Web App指定開啟信箱的網頁組件、 開啟、，信箱內的資料夾和內容檢視可使用。

Outlook Web App網頁組件可讓您直接從 URL 存取Outlook Web App內容。可以輸入至網頁瀏覽器或內嵌於應用程式 URL。一般而言，未手動建立網頁組件。而它們根據，建立以程式設計方式進行使用者介面 (UI) 中的選取範圍或他們正在內嵌直接在 SharePoint Server\] 頁面等的應用程式中。程式碼後置 UI 接著會建立 URL。一個用於Outlook Web App網頁組件是在 SharePoint 頁面上顯示使用者的收件匣或行事曆。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在相同的Active Directory樹系中必須位於使用者的信箱與信箱正在開啟透過網頁組件使用Outlook Web App網頁組件。</td>
</tr>
</tbody>
</table>


## 使用 Outlook Web Access 網頁組件的權限

Outlook Web App網頁組件，您必須至少是可使用委派的 「 檢閱者 」 存取權開啟的內容。如果您已內嵌Outlook Web App需要轉換為應用程式驗證的網頁組件，您必須傳遞透過與之要求的網頁組件中的驗證資訊。若要執行這項作業的其中一個方法是藉由設定為使用整合式的Windows驗證Outlook Web App虛擬目錄。整合式的Windows驗證可讓使用者已經登入使用其Active Directory帳戶使用Outlook Web App時不必重新輸入認證。

## Outlook Web App 網頁組件的語法

Outlook Web App 2013 Exchange 中具有要用於要求送至 /owa 虛擬目錄的 URL 格式。輸入 URL 以在網頁瀏覽器會將直接或透過 Web 應用程式，例如 SharePoint Server\] 頁面中嵌入 URL 可以進行這些要求。

Outlook Web App網頁組件可用來建立不同的複雜性的 Url。簡單的網頁組件 URL 可用來開啟任何信箱的收件匣。較複雜的網頁組件 URL 無法用來指定開啟信箱、 資料夾內開啟，該信箱和內容檢視以使用。

根據已套用至您的網路安全性措施，您可能必須設定的網頁組件 URL 編碼。設定的編碼方式之後，背後的使用者介面的程式碼會使用 URL 編碼的參數建立 URL。URL 編碼的參數使用 %20 取代空格和 %2f 路徑分隔字元取代"/"。本主題中的所有範例都使用編碼的參數。

下表列出網頁組件與使用方法的範例參數。

### 網頁組件參數和使用方式

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>URL 參數</th>
<th>描述</th>
<th>值和範例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>伺服器名稱和目錄 （必要）</p></td>
<td><p>Outlook Web App虛擬目錄的 URL。</p></td>
<td><p>這可能是相同的 URL 使用者用來登入至Outlook Web App，例如：</p>
<p>https://&lt; ；<em>server name</em>&gt; / owa</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013 明確登入信箱識別 （選用）</p></td>
<td><p>任何已開啟信箱相關聯的 SMTP 位址。</p>
<p>如果此] 區段中的 URL，開啟預設的信箱的已驗證的使用者。</p>
<p>若未不指定任何其他參數的預設行為是以開啟收件匣。</p></td>
<td><p>若要開啟 SMTP 地址 tsmith@fourthcoffee.com 信箱，使用下列 URL：</p>
<p>https://&lt;<em>server name</em>&gt;/owa/tsmith@fourthcoffee.com</p></td>
</tr>
<tr class="odd">
<td><p>cmd （如果您正在指定任何參數的明確登入信箱識別非必要）</p></td>
<td><p>？ cmd = 內容顯示Outlook Web App而非完整Outlook Web App使用者介面參數所指定的網頁組件。</p></td>
<td><p>如果未不指定任何信箱，則 cmd 參數而言登入地址後，如下所示：</p>
<p>https://&lt; ；<em>server name</em>&gt;/owa/?cmd = 內容</p>
<p>如果指定的信箱，則 cmd 參數而言明確信箱識別、 之後，如下所示：</p>
<p>https://&lt; ；<em>server name</em>&gt; /owa/ &lt;<em>SMTP address</em>&gt; / ?cmd = 內容</p>
<p>若未不指定任何其他參數的預設行為是以開啟收件匣。</p></td>
</tr>
<tr class="even">
<td><p>exsvurl</p></td>
<td><p>此參數必須包含時使用 LiveID 驗證</p>
<p>所有參數則會都捨棄 LiveID 驗證期間如果&quot;exsvurl = 1&quot;不存在。此參數是僅限 Office 365 信箱。</p></td>
<td><p>https://&lt;server 名稱 &gt; /owa/ 吗？ cmd = 內容 exsvurl = 1</p></td>
</tr>
<tr class="odd">
<td><p>fpath （選用）</p></td>
<td><p>此 URL 部分可能需要將由使用 URL 編碼方式，讓它可以通過防火牆寫入。</p>
<p>當您使用 URL 編碼時，空格會變成 %20，且路徑分隔符號 （/） 成為 %2f。</p>
<p>資料夾階層應開始從信箱根目錄。</p>
<p>此資料夾的路徑可以指向一般資料夾或搜尋資料夾。</p></td>
<td><p>若要開啟收件匣的子專案，使用下列 URL：</p>
<p>https://&lt; ；<em>server name</em>&gt;/owa/?cmd = 內容 fpath = 收件匣 %2fprojects</p></td>
</tr>
<tr class="even">
<td><p>單元 （選用）</p></td>
<td><p>此參數可用來指定預設資料夾而不需要知道的本地化的名稱。</p></td>
<td><p>模組參數的值不區分大小寫，並包括下列各項：</p>
<ul>
<li><p>收件匣</p></li>
<li><p>行事曆</p></li>
<li><p>Teammailbox</p></li>
</ul>
<p>若要開啟不論當地語系化信箱的行事曆，請使用下列 URL：</p>
<p>https://&lt; ；<em>server name</em>&gt;/owa/?cmd = 內容模組 = 行事曆</p></td>
</tr>
<tr class="odd">
<td><p>檢視 （選用）</p></td>
<td><p>此參數會指定要顯示的資料夾檢視。</p>
<p>此參數不存在時的預設檢視如下所示：</p>
<ul>
<li><p>每日的行事曆</p></li>
<li><p>郵件的郵件</p></li>
</ul>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>預設檢視的字串就會自動編碼的 URL。</td>
</tr>
</tbody>
</table>

<p>檢視預設排序是會排序資料夾，如果從中開啟Outlook Web App用戶端中的方式。</p>
<p>用於識別檢視字串不當地語系化並不區分大小寫。</p></td>
<td><p>可檢視會根據資料夾類型而有所不同。</p>
<p>行事曆檢視︰</p>
<ul>
<li><p>每天每日的 [行事曆] 檢視</p></li>
<li><p>每週每週的 [行事曆] 檢視</p></li>
<li><p>每月每月的行事曆檢視</p></li>
</ul>
<p>郵件檢視︰</p>
<ul>
<li><p>郵件郵件檢視與預設排序</p></li>
<li><p>%20sender 郵件檢視中排序由從寄件者名稱開頭為&quot;a&quot;在上方</p></li>
<li><p>由 %20subject 郵件檢視中依主題主旨開頭為&quot;a&quot;在上方排序</p></li>
<li><p>藉由 %20Conversation %20topic 交談檢視，不適用於Outlook Web App light 版]</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>d、 m、 y （選用）</p></td>
<td><p>會指定應該顯示行事曆中的日期。這些參數可以依任何順序中輸入與可以單獨或一起使用。</p>
<p>如果未指定任何這些參數，預設值是目前的日期、 月份和年份值。例如，如果當日 2016 年 5 月 3，且您指定的月份值為&quot;9&quot;9 月、 日期顯示將是 2016 年 9 月 3、。</p></td>
<td><p>資料參數的有效值如下：</p>
<p>d = [1-31]</p>
<p>m = [1-12]</p>
<p>y = [四位數的年份]</p>
<p>若要開啟 [行事曆日期 2016 年 5 月 3，您會使用下列 URL： https://&lt; ；<em>server name</em>&gt;/owa/?cmd = 內容 fpath = 行事曆檢視 = 每日 &amp; d = 3 &amp; m = 5 y = 2016年</p></td>
</tr>
<tr class="odd">
<td><p>（選用） 的組件</p></td>
<td><p>會指定該Outlook Web App應該顯示較小的網頁組件。</p></td>
<td><p>當您使用網頁組件來存取Outlook Web App內容時，所顯示的 UI 會小於完整Outlook Web App UI。組件參數可減少進一步的 UI。下列的範例 URL 會顯示 [工作] 清單中最小的網頁組件格式：</p>
<p>https://&lt; ；<em>server name</em>&gt;/owa/?cmd = 內容組件 = 1</p>
<p>組件參數不會套用至行事曆模組。</p></td>
</tr>
<tr class="even">
<td><p>FolderList</p></td>
<td><p>此組件參數包含使用者的子資料夾之間切換的資料夾清單控制項。這僅適用於電子郵件資料夾。</p></td>
<td><p>https://&lt;server 名稱 &gt; /owa/ 吗？ cmd = 內容 folderlist = 1</p></td>
</tr>
</tbody>
</table>


## 手動輸入 Outlook Web App 網頁組件

Outlook Web App網頁組件可以是也可手動輸入網頁瀏覽器中。例如，使用者可以使用Outlook Web App網頁組件 URL 以開啟另一個使用者的行事曆。

下列範例顯示如何直接存取一般的 Outlook Web App 檢視︰

  - **收件匣：** https://*\<server name\>*/owa/?cmd = 內容模組 = 收件匣

  - **行事曆 （今天）：**https://*\<server name\>*/owa/?cmd = 內容模組 = 行事曆 exsvurl = 1

  - **行事曆 （每週）：** https://*\<server name\>*/owa/?cmd = 內容模組 = 行事曆檢視 = 每週 exsvurl = 1

  - **（每月） 的行事曆︰** https://*\<server name\>*/owa/?cmd = 內容模組 = 行事曆檢視 = 月 exsvurl = 1

## 相關資訊

  - [自訂 Outlook Web App 登入、語言選擇與錯誤頁面](customize-the-outlook-web-app-sign-in-language-selection-and-error-pages-exchange-2013-help.md)

  - [建立 Outlook Web App 的佈景主題](create-a-theme-for-outlook-web-app-exchange-2013-help.md)

