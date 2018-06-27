---
title: '共同作業: Exchange 2013 Help'
TOCTitle: 共同作業
ms:assetid: f45c1be1-2a66-4610-a28d-4adc6d212769
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ218725(v=EXCHG.150)
ms:contentKeyID: 50474586
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 共同作業

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

Exchange 2013 提供下列豐富的功能可協助您的使用者輕鬆地進行共同作業的電子郵件：

  - 網站信箱

  - 公用資料夾

  - 共用信箱

  - 通訊群組

這些功能有不同的使用者經驗及功能及應根據使用者需要達成目標與您的組織可以提供使用。例如，站台信箱提供更好的文件共同作業功能。不過，站台信箱依賴 SharePoint Server 2013，因此如果您未計劃部署 SharePoint、 所應使用的公用資料夾共用文件。

本主題會比較這些協同作業功能，協助您決定應為使用者提供什麼功能。

## 網站信箱

網站 mailboxe 具有相同的作用組成 SharePoint 2013 網站成員資格 （擁有者及成員）、 共用存放裝置透過 Exchange 2013 信箱的電子郵件訊息及 SharePoint 2013 網站來儲存和共用。基本上，站台信箱結合 Exchange 電子郵件與 SharePoint 文件。使用者、 站台信箱會做為專案中，提供檔案專案電子郵件以及文件可存取及編輯網站成員只能由中央歸檔 cabinet。此外，站台信箱已指定的週期並最佳化要用於設定開始和結束日期的專案。若要完整實作網站信箱，使用者必須使用 Outlook 2013。

若要深入了解，請參閱[網站信箱](site-mailboxes-exchange-2013-help.md)。

## 公用資料夾

公用資料夾的設計目的在於共用存取，並提供簡易有效率的方式來收集及組織資訊，以及與工作群組或組織中的其他人員共用資訊。

公用資料夾組織很容易瀏覽深層階層中的內容。使用者瀏覽到階層的相關給他們的分支探索有趣及相關內容。使用者永遠會看到其 Outlook 資料夾檢視中的完整階層。公用資料夾是更好的技術的通訊群組封存。可擁有郵件功能的公用資料夾及新增為通訊群組的成員。傳送至通訊群組的電子郵件會自動新增至公用資料夾供日後參考。公用資料夾也提供簡單的文件共用並不需要在組織中安裝 SharePoint Server 2013。最後，使用者可以具有下列支援的 Outlook 用戶端使用的公用資料夾： Outlook 2007、 Outlook 2010 和 Outlook 2013。

若要深入了解，請參閱[公用資料夾](public-folders-exchange-2013-help.md)。

## 共用信箱

共用信箱是指可讓多位指定使用者存取以閱讀及傳送電子郵件，以及共用共同行事曆的信箱。共用信箱可以提供通用電子郵件地址 (例如 info@contoso.com 或 sales@contoso.com)，讓客戶用來查詢公司的相關資訊。如果受委派使用者在回覆電子郵件時，指派「傳送為」權限給共用信箱，則電子郵件中會顯示是該信箱 (如 sales@contoso.com) 進行回覆，而不是實際的使用者。

若要深入了解，請參閱[共用信箱](shared-mailboxes-exchange-2013-help.md)。

## 群組

群組 (也稱為通訊群組) 是出現在共用通訊錄中，由兩個以上收件者所構成的集合。當群組收到一封電子郵件時，群組的所有成員都會收到該封郵件。通訊群組可依特定的討論主題 (如「愛狗人士」) 加以分組，或依需要經常通訊而共用共同工作結構的使用者加以分組。

若要深入了解，請參閱[收件者](recipients-exchange-2013-help.md)。

## 要使用哪一種？

下表提供每個協同合作功能的快速概覽，協助您決定應使用那一項。


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
<th> </th>
<th>網站信箱</th>
<th>公用資料夾</th>
<th>共用信箱</th>
<th>群組</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>群組類型</strong></p></td>
<td><p>針對有明確開始和結束日期的特定專案而一起團隊合作的使用者。</p></td>
<td><p>只要具有適當的權限，組織中的每個人都能存取和搜尋公用資料夾。公用資料夾是維護歷史記錄或發佈群組對話的理想選擇。</p></td>
<td><p>可代表虛擬身分委派工作，並以該共用信箱身分回覆電子郵件。範例：support@tailspintoys.com</p></td>
<td><p>需要傳送電子郵件給一群有共同興趣或特性之收件者的使用者。</p></td>
</tr>
<tr class="even">
<td><p><strong>理想的群組大小</strong></p></td>
<td><p>小</p></td>
<td><p>大型</p></td>
<td><p>小</p></td>
<td><p>大型</p></td>
</tr>
<tr class="odd">
<td><p><strong>Access</strong></p></td>
<td><p>網站信箱擁有者和成員。</p></td>
<td><p>組織中的任何人都能夠存取。</p></td>
<td><p>使用者可以被授與「完整存取權」和/或「傳送為」權限。若獲授與「完整存取權」權限，使用者還必須將共用信箱加入至其 Outlook 設定檔，以便存取共用信箱。</p></td>
<td><p>通訊群組的成員，必須手動新增。動態通訊群組的成員會新增根據篩選準則。</p></td>
</tr>
<tr class="even">
<td><p><strong>共用行事曆？</strong></p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p><strong>電子郵件會進入個人收件匣嗎？</strong></p></td>
<td><p>不，電子郵件是進入網站信箱中。</p></td>
<td><p>不，電子郵件是進入公用資料夾。</p></td>
<td><p>不，電子郵件是進入共用信箱的收件匣。</p></td>
<td><p>會。電子郵件會進入通訊群組成員的收件匣。</p></td>
</tr>
<tr class="even">
<td><p><strong>支援的用戶端</strong></p></td>
<td><ul>
<li><p>Outlook 2013</p></li>
<li><p>SharePoint 2013</p></li>
</ul></td>
<td><ul>
<li><p>Outlook 2013</p></li>
<li><p>Outlook 2010</p></li>
<li><p>Outlook 2007</p></li>
</ul></td>
<td><ul>
<li><p>Outlook 2013</p></li>
<li><p>Outlook Web App</p></li>
<li><p>Outlook 2010</p></li>
<li><p>Outlook 2007</p></li>
</ul></td>
<td><ul>
<li><p>Outlook 2013</p></li>
<li><p>Outlook Web App</p></li>
<li><p>Outlook 2010</p></li>
<li><p>Outlook 2007</p></li>
</ul></td>
</tr>
</tbody>
</table>

