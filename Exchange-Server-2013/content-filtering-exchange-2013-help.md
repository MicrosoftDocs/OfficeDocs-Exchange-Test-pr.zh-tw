---
title: '內容篩選: Exchange 2013 Help'
TOCTitle: 內容篩選
ms:assetid: d660ffbf-de05-46c2-940b-5200eca94e0a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124739(v=EXCHG.150)
ms:contentKeyID: 50474349
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 內容篩選

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在 2016 年 11 月 1，Microsoft 停止產生 Exchange 和 Outlook 中 SmartScreen 篩選器的垃圾郵件定義更新。現有的 SmartScreen 垃圾郵件定義將會保留，但其效果可能會隨著時間降低。如需詳細資訊，請參閱 <a href="https://go.microsoft.com/fwlink/p/?linkid=835894">Outlook 和 Exchange 中 SmartScreen 的取代支援</a>。</td>
</tr>
</tbody>
</table>


內容篩選器代理程式評估的內送的電子郵件並評估垃圾郵件的內送的郵件是合法的機率。與許多其他篩選技術不同的內容篩選器代理程式會使用從統計大幅樣本的電子郵件的特性。此範例中的合法郵件包含減少錯誤的機會。因為內容篩選器代理程式可辨識的合法的郵件和垃圾郵件特性，增加其正確性。透過[Microsoft Update](https://go.microsoft.com/fwlink/p/?linkid=54836)定期更新的內容篩選器代理程式可用。

**目錄**

Using the Content Filter agent

Configuring the Content Filter agent

## 使用內容篩選器代理程式

內容篩選器代理程式將會是其中一個數個反垃圾郵件代理程式 Exchange 中。當您在 Exchange 伺服器上設定反垃圾郵件代理程式時，代理程式處理逐個來減少進入組織的垃圾郵件的郵件。如需如何規劃及部署反垃圾郵件代理程式的詳細資訊，請參閱[反垃圾郵件保護](anti-spam-protection-exchange-2013-help.md)。

內容篩選器代理程式會將垃圾郵件信賴等級 (scl) 指派給每則訊息。Scl 是介於 0 到 9 的數字。較高的 scl 指出郵件的更多可能是垃圾郵件。

您可以將內容篩選器代理程式設定為根據 SCL 分級而對郵件採取下列動作。

  - 刪除郵件

  - 拒絕郵件

  - 隔離郵件

例如，您可以決定是否必須刪除 SCL 分級 7 以上的郵件、是否必須拒絕 SCL 分級 6 的郵件，以及是否必須隔離 SCL 分級 5 的郵件。

您可以調整的 SCL 閾值行為不同 SCL 評等指派給每個這些動作。如需如何調整以符合組織需求的 SCL 閾值與每個收件者 SCL 閾值的相關的詳細資訊，請參閱[垃圾郵件信賴等級閾值](spam-confidence-level-threshold-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>已超過 11 MB 不智慧型郵件篩選器所掃描的郵件。而這些通過內容篩選器不掃描。</td>
</tr>
</tbody>
</table>


## Allow 片語及 Block 片語

您可以自訂內容篩選器代理程式如何指派 SCL 值來設定自訂文字。自訂文字是在個別的單字或片語的內容篩選器代理程式會使用套用適當的篩選處理。您具有允許片語及未的單字或片語封鎖片語與設定已核准的單字或片語。當內容篩選器代理程式內送郵件中偵測預先設定的允許片語時，內容篩選器代理程式自動指派 SCL 值為 0 到郵件。或者，當內容篩選器代理程式內送郵件中偵測已設定的封鎖詞語，內容篩選器代理程式會指派 9 scl。

您可以輸入自訂的單字或片語的任何組合的大寫和小寫字母。不過，當內容篩選器代理程式評估郵件內容，它就會忽略大小寫。自訂文字或片語可以建立的最大數目為 800。

## Outlook 電子郵件郵戳驗證

內容篩選器代理程式也會包含 Microsoft Office Outlook 電子郵件郵戳驗證，Outlook 會套用至以協助辨認合法電子郵件從垃圾電子郵件收件者的郵件系統的外寄郵件的計算校對。此功能可協助降低的誤判。垃圾郵件篩選的內容、*誤判*存在時的垃圾郵件篩選器不正確地識別為垃圾郵件的合法寄件者的訊息。啟用 Outlook 電子郵件郵戳驗證時，內容篩選器代理程式會剖析計算郵戳標頭的內送的郵件。在郵件中的有效、 解決計算郵戳標頭的目前狀態指出產生之郵件的用戶端電腦解決計算郵戳。

電腦不需要以解決個別計算 postmarks 重大的處理時間。不過，處理 postmarks 許多訊息可能過於惡意的寄件者。傳送數以百萬計的垃圾郵件的任何人為可能性投資才可解決計算 postmarks 的所有輸出垃圾郵件的處理能力。如果寄件者的電子郵件包含有效、 解決計算郵戳，最好是可能性寄件者是惡意的寄件者。在此例中的內容篩選器代理程式會降低 scl。如果啟用郵戳驗證功能，其中一個不包含計算郵戳標頭或計算郵戳標頭內送的郵件不是有效的內容篩選器代理程式就不會變更 scl。

## 略過收件者、寄件者及寄件者網域

在某些組織中，必須接受所有電子郵件給特定的別名。如果您組織中管理垃圾郵件的重大的磁碟區產業此案例可以引進的問題。

例如，名為 Woodgrove Bank 的公司具有外部貸款所支付的客戶提供電子郵件式支援別名具名的 customerloans@woodgrovebank.com。Exchange 系統管理員設定中所不道德貸款行政機關傳送的垃圾郵件設定封鎖片語的篩選出單字或片語的通常用內容篩選器代理程式。若要防止可能合法的郵件被拒絕，系統管理員會設為內容篩選輸入 SMTP 電子郵件收件者地址清單中的內容篩選器代理程式組態例外狀況。

您還可以指定不要讓內容篩選器代理程式封鎖的寄件者及寄件者網域。

## 安全清單彙總

在Exchange 2013、 內容篩選器代理程式會使用 Outlook 安全的寄件者清單、 封鎖的寄件者清單、 安全的收件者清單，並從 Outlook 的受信任的連絡人最佳化垃圾郵件篩選。*安全清單彙總*為一組 Outlook 與 Exchange 之間共用的反垃圾郵件功能。為其名稱建議，這項功能從 Outlook 使用者設定的反垃圾郵件安全清單收集資料，並讓 Exchange 伺服器上的反垃圾郵件代理程式可以使用此資料。Outlook 使用者接收來自這些使用者已新增至其 Outlook 安全的收件者清單、 安全的寄件者清單中或受信任的連絡人清單中的連絡人的電子郵件會被識別為安全內容篩選器代理程式。寄件者篩選器代理程式也會執行每個收件者寄件者篩選使用使用者設定的封鎖的寄件者清單。如需詳細資訊，請參閱[安全清單彙總](safelist-aggregation-exchange-2013-help.md)。

## 設定內容篩選器代理程式

使用 Exchange 管理命令介面設定內容篩選器代理程式。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>設定對 Exchange 管理命令介面中內容篩選器代理程式所做的變更只會對本機電腦上進行。如果您在組織中的多部 Exchange 伺服器上執行的內容篩選器代理程式，您必須對每一部電腦進行內容篩選器組態變更。</td>
</tr>
</tbody>
</table>


內容篩選器代理程式取決於更新，以判斷是否可以使用它不是垃圾郵件信賴傳遞訊息。這些更新包含網路釣魚網站的相關資料、 Microsoft SmartScreen 垃圾郵件 heuristics，以及其他智慧型郵件篩選更新。內容篩選器更新通常包含約 6 MB 的其他反垃圾郵件更新資料進行較長的時間很有用的資料。

內容篩選器更新均可在[Microsoft Update](https://go.microsoft.com/fwlink/p/?linkid=54836)。內容篩選器更新資料已更新並可供下載每兩週。

如需如何設定內容篩選的相關資訊，請參閱[管理內容篩選](manage-content-filtering-exchange-2013-help.md)。

