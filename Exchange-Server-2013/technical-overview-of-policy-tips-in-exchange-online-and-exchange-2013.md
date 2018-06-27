---
title: '原則提示: Exchange Online Help'
TOCTitle: 原則提示
ms:assetid: 4266b83c-dd8a-4b3d-99ff-402e68fc810c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ150512(v=EXCHG.150)
ms:contentKeyID: 50472270
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 原則提示

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2015-07-22_

您可以協助防止貴組織的 Microsoft Outlook、 Outlook Web App (OWA) 和 OWA for Devices 電子郵件使用者不當傳送機密資訊藉由建立包含*原則提示*通知郵件的資料外洩防護 (DLP) 原則。類似於 Microsoft Exchange Server 2010中所引進的寄件提醒、 原則提示通知郵件會顯示Outlook中的使用者他們所撰寫的電子郵件時。原則提示通知郵件只顯示如果寄件者的電子郵件訊息的相關的某個項目似乎違反您已經備妥的 DLP 原則及原則包含以符合您所建立的條件時通知寄件者的規則。觀賞此影片以深入了解。

> [!VIDEO https://www.microsoft.com/zh-tw/videoplayer/embed/dd629bb7-063d-49f3-b7e1-8f2e0aa4de13]

為向您的電子郵件寄件者顯示原則提示，您的規則必須包含 \[以原則提示通知寄件者\] 動作。您可從 Exchange 系統管理中心新增此規則編輯器。如需詳細資訊，請參閱 [管理原則提示](how-to-configure-and-manage-policy-tips-a-dlp-feature-exchange.md)。

強制 DLP 原則的傳輸規則代理程式在原則中評估郵件及情況時，不會區分電子郵件附件、內容文字或主旨行。例如，如果使用者所建立的電子郵件在郵件內文中包含信用卡號碼，且使用者嘗試將郵件傳送給組織以外的收件者，則會在 Outlook 或 Outlook Web App 中向使用者顯示原則提示通知郵件，提醒使用者企業對此類資訊的期望。不過，此類通知只會在您已設定限制說明的範例動作之 DLP 原則時顯示；在此情況下，可將外部電子郵件別名新增到具有信用卡資訊的郵件標頭。建立 DLP 原則時，有各種條件、動作以及期望可選擇。這些選擇讓您可量身訂做資料遺失防護，以滿足您的特定組織需求。

每當您使用規則內的通知寄件者動作或覆寫動作時，我們建議您一併包含郵件從組織中傳送的條件。若要這麼做，您可以使用原則規則編輯器來新增下列條件：\[寄件者位於…\] \> \[在組織內部\]。若要深入了解變更現有 DLP 原則的相關資訊，請參閱[管理 DLP 原則](manage-dlp-policies-exchange-2013-help.md)。由於通知寄件者動作會隨著公司的郵件建立經驗一併套用，因此這是最佳作法建議。動作參照的寄件者是公司內的郵件作者。使用者無法針對傳入郵件採取原則提示提供的使用者互動，因此當寄件者位於組織外部時，使用者互動將會被忽略。您可以套用 DLP 原則以掃描傳入郵件並採取多種動作，但是如果您要這樣做，請勿新增通知寄件者動作。

如果組織中正在進行撰寫郵件動作的寄件者透過原則提示通知即時注意到組織期望與標準，則較不會違反組織要強制的標準。

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Exchange Online：DLP 是付費功能，需要 Exchange Online 計劃 2 授權。如需詳細資訊，請參閱 <a href="https://go.microsoft.com/fwlink/p/?linkid=286154">Exchange Online 授權</a>。</p></li>
<li><p>Exchange 2013：DLP 是需要 Exchange 企業版用戶端存取授權 (CAL) 的高階功能。如需 CAL 和伺服器授權的詳細資訊，請參閱 <a href="https://go.microsoft.com/fwlink/p/?linkid=237292">Exchange Server 授權</a>。</p></li>
<li><p>如果您的組織使用 Exchange 2013 SP1 或 Exchange Online，則原則提示將適用於從 Outlook 2013、Outlook Web App 或 裝置的 OWA 傳送郵件的人員。但若您的組織目前使用 Exchange 2013，則原則提示僅適用於從 Outlook 2013 傳送郵件的人員。</p></li>
</ul></td>
</tr>
</tbody>
</table>


## 原則提示及規則選項預設

當您將寄件者通知原則新增到 DLP 原則時，會有一系列可能的選項。當您在 DLP 原則中使用 \[以原則提示通知寄件者\] 動作新增原則來通知寄件者時，可選擇限制的方式。下表列出可用的通知選項。如需編輯原則的一般資訊，請參閱[管理 DLP 原則](manage-dlp-policies-exchange-2013-help.md)。如需建立元則提示的具體資訊，請參閱[管理原則提示](how-to-configure-and-manage-policy-tips-a-dlp-feature-exchange.md)。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>通知規則</th>
<th>意義</th>
<th>Outlook的使用者將看到的預設原則提示通知郵件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>僅通知</strong></p></td>
<td><p>與 MailTips 類似，這會導致資訊原則提示通知郵件違反原則。寄件者可使用可在 Outlook中存取的原則提示選項對話方塊避免出現此類型提示。</p></td>
<td><p>此郵件可能包含敏感內容。所有收件者都必須被都授權接收此內容。</p></td>
</tr>
<tr class="even">
<td><p><strong>拒絕郵件</strong></p></td>
<td><p>直到不再出現此情況後才會傳遞郵件。寄件者會提供選項來表示其電子郵件不包含敏感性內容。這也稱為誤判覆寫。若寄件者指出此情況，則 Outlook 將允許郵件離開寄件匣，讓使用者的報告可被稽核，不過 Exchange 將封鎖訊息傳送。</p></td>
<td><p>此郵件可能包含敏感內容。內容移除前，組織不允許傳送此郵件。</p></td>
</tr>
<tr class="odd">
<td><p><strong>除非誤判覆寫，否則拒絕</strong></p></td>
<td><p>此通知規則的結果與 [拒絕郵件] 通知規則類似。不過，若您選擇此規則，則 Exchange 將允許郵件傳送給預定的收件者，而不會封鎖郵件。</p></td>
<td><p><strong>在寄件者前選擇一個選項來覆寫：</strong>此郵件可能包含敏感內容。內容移除前，組織不允許傳送此郵件。</p>
<p><strong>在寄件者選擇一個選項來覆寫後：</strong> 郵件傳送時將提交您的回覆給管理員。</p></td>
</tr>
<tr class="even">
<td><p><strong>除非無訊息覆寫，否則拒絕</strong></p></td>
<td><p>直到不再出現此情況或寄件者表示覆寫後才會傳遞郵件。寄件者會提供選項以表示他們希望覆寫原則。</p></td>
<td><p><strong>在寄件者前選擇一個選項來覆寫：</strong>此郵件可能包含敏感內容。內容移除前，組織不允許傳送此郵件。</p>
<p><strong>在寄件者選擇一個選項來覆寫後：</strong> 您已覆寫此郵件中組織原則的敏感內容。您的動作將由組織進行稽核。</p></td>
</tr>
<tr class="odd">
<td><p><strong>除非明確覆寫，否則拒絕</strong></p></td>
<td><p>此通知原則結果與 [除非無訊息覆寫，否則拒絕] 通知規則類似，除非此案例中寄件者嘗試覆寫原則，寄件者需要提供覆寫原則的論證。</p></td>
<td><p><strong>在寄件者前選擇一個選項來覆寫：</strong>此郵件可能包含敏感內容。內容移除前，組織不允許傳送此郵件。</p>
<p><strong>在寄件者選擇一個選項來覆寫後：</strong> 您已覆寫此郵件中組織原則的敏感內容。您的動作將由組織進行稽核。</p></td>
</tr>
</tbody>
</table>


## 自訂原則提示通知郵件

若要自訂的電子郵件的寄件者查看其電子郵件程式中的 「 原則提示通知文字，選取 \[資料外洩防護\] 頁面上的**管理原則提示**。 為了讓您自訂文字的任何出現，DLP 原則規則必須包含的**通知寄件者以原則提示**巨集指令。使用 DLP 規則編輯器中新增的規則動作。

說明如何建立您自己的原則提示，請參閱[管理原則提示](how-to-configure-and-manage-policy-tips-a-dlp-feature-exchange.md)的程序。您建立的自訂文字可以取代預設的文字上表所示。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>原則提示通知動作與設定</th>
<th>意義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>通知寄件者</strong></p></td>
<td><p>初始化<strong>通知寄件者，但允許他們傳送</strong>動作時，才會顯示您的文字。</p></td>
</tr>
<tr class="even">
<td><p><strong>允許寄件者覆寫</strong></p></td>
<td><p>下列動作會初始化時才會出現在文字 ︰<strong>它設定為誤判封鎖郵件</strong>、<strong>封鎖郵件，但允許寄件者覆寫及傳送</strong>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>封鎖郵件</strong></p></td>
<td><p>初始化<strong>封鎖郵件</strong>動作時，才會顯示您的文字。</p></td>
</tr>
<tr class="even">
<td><p><strong>連結到規範 URL</strong></p></td>
<td><p>規範 URL 是您可以在此說明在規範並覆寫原則的網頁連結。此連結將顯示原則提示] 中當使用者按一下 [<strong>更多詳細資料</strong>] 連結。</p></td>
</tr>
</tbody>
</table>


## 相關資訊

[資料遺失防護](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[管理 DLP 原則](manage-dlp-policies-exchange-2013-help.md)

[管理原則提示](how-to-configure-and-manage-policy-tips-a-dlp-feature-exchange.md)

