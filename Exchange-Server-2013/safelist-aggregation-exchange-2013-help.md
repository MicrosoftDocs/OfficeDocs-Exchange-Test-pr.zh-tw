---
title: '安全清單彙總: Exchange 2013 Help'
TOCTitle: 安全清單彙總
ms:assetid: f05430a0-0405-4b65-a18d-18c9e86a13c4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb125168(v=EXCHG.150)
ms:contentKeyID: 50474560
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 安全清單彙總

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2013-09-30_

在 Microsoft Exchange Server 2013 中，「安全清單彙總」一詞指的是在 Microsoft Outlook 和 Exchange 之間共用的反垃圾郵件功能。此功能會從反垃圾郵件的 \[安全的收件者清單\]、\[安全的寄件者清單\]、\[封鎖的寄件者清單\] 以及 Outlook 使用者設定的連絡人資料中收集資料，並將該資料提供給 Exchange 反垃圾郵件代理程式。

當您啟用並正確設定安全清單彙總時，內容篩選器代理程式會將安全的電子郵件傳到企業信箱，不須額外的處理。內容篩選器代理程式會將 Outlook 使用者所收到之來自加入至其 Outlook \[安全的收件者清單\] 或 \[安全的寄件者清單\] 或其信任之連絡人的電子郵件，識別為安全的電子郵件。Outlook「連絡人」就是指使用者組織內部或外部的人員，使用者可以儲存與其相關的多項資訊類型，例如電子郵件及實際地址、電話及傳真號碼，以及網頁 URL 等。

在 Exchange 2013 中，安全清單彙總程序也能讓寄件者篩選器代理程式根據每位收件者的 \[封鎖寄件者清單\]，封鎖內送郵件。

安全清單彙總可以協助減少 Exchange 所執行之反垃圾郵件篩選中的誤判執行個體。以垃圾郵件篩選而言，如果垃圾郵件篩選器將合法郵件誤認為垃圾郵件，這種情形就稱為「誤判」。

對於每天需要篩選成千上萬則來自網際網路之郵件的組織而言，即使發生誤判的百分比很低，仍然意味著使用者可能無法收到許多被錯誤識別為垃圾郵件，因為這些郵件會被隔離或遭到刪除。

安全清單彙總可說是最能夠有效減少誤判的方式。在 Outlook 2010 或更新版本中，使用者可以建立「安全的寄件者清單」。\[安全的寄件者清單\] 可指定 Outlook 使用者想接收其郵件的來源網域名稱及電子郵件地址清單。依預設，Outlook 連絡人及 Exchange 全域通訊清單中的電子郵件地址都會包含在清單中。此外，Outlook 預設也將使用者會傳送郵件的目標外部連絡人加入 \[安全的寄件者清單\] 中。

**目錄**

Information stored in the Outlook user's safelist collection

How Exchange uses the safelist collection

Hashing of safelist collection entries

Enabling safelist aggregation

## 儲存在 Outlook 使用者安全清單集合中的資訊

「安全清單集合」結合了使用者的 \[安全的寄件者清單\]、\[安全的收件者清單\]、\[封鎖的寄件者清單\] 以及外部連絡人的資料。此資料會儲存在 Outlook 及 Exchange 信箱中。

下列資訊類型會儲存在 Outlook 使用者的安全清單集合中：

  - **安全的寄件者及安全的收件者**   寄件者郵件標題就是指寄件者。電子郵件的 \[收件者\] 欄位就是指收件者。安全的寄件者及安全的收件者會以完整的 SMTP 位址來呈現，例如 masato@contoso.com。Outlook 使用者可以將寄件者及收件者新增至其安全清單中。

  - **封鎖的寄件者**   就像安全的寄件者一樣，使用者可以將這些不想要的寄件者，新增至其封鎖的寄件者清單中來封鎖他們。

  - **安全的網域**   網域是指 @ 符號後面的 SMTP 位址部分。例如， contoso.com 就是 masato@contoso.com 地址中的網域。Outlook 使用者可以將寄送網域新增至其安全清單中。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>預設情況下，Exchange 不包含安全清單彙總期間的網域。但您可以設定反垃圾郵件代理程式的安全清單彙總，以包括安全網域資料。如需詳細資訊，請參閱<a href="configure-content-filtering-to-use-safe-domain-data-exchange-2013-help.md">設定內容篩選要使用安全網域資料</a>。</td>
    </tr>
    </tbody>
    </table>


  - **外部連絡人**   安全清單彙總中可以包含兩種類型的外部連絡人。第一種外部連絡人類型包含 Outlook 使用者已有傳送郵件的目標連絡人。只有當 Outlook 使用者在 Outlook 2007 的 \[垃圾郵件\] 設定中選取相對應的選項時，此連絡人類別才會新增至 \[安全的寄件者清單\] 中。
    
    第二種外部連絡人類型包含使用者的 Outlook 連絡人。使用者可以將這些連絡人新增或匯入 Outlook 中。只有當 Outlook 使用者在 Outlook 2010 或 Outlook 2007 的 \[垃圾郵件篩選\] 設定中選取相對應的選項時，此連絡人類別才會新增至 \[安全的寄件者清單\] 中。

回到頁首

## Exchange 如何使用安全清單集合

安全清單集合儲存於使用者的信箱伺服器上。使用者的安全清單集合中，最多可包含 1,024 個唯一的項目。Exchange 2013 裡有一個信箱助理員 (稱為垃圾郵件選項信箱助理員)，負責監視信箱裡安全清單集合的變更。此助理員會接著將這些變更複寫至 Active Directory，並將安全清單集合儲存在每個使用者物件上。當安全清單集合儲存在 Active Directory 裡的使用者物件上時，安全清單集合就會彙總 Exchange 2013 的反垃圾郵件功能，並且進行最佳化讓儲存及複寫量降至最低。Exchange 在內容篩選過程中會使用安全清單集合資料。如果您的周邊網路中有訂閱的 Edge Transport Server，Microsoft Exchange EdgeSync 服務會將安全清單集合複寫至 Edge Transport Server 上的 Active Directory 輕量型目錄服務 (AD LDS) 執行個體。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>雖然安全的收件者資料儲存在 Outlook 中，並可彙總成為安全清單集合，但內容篩選功能不會對安全的收件者資料採取動作。</td>
</tr>
</tbody>
</table>


回到頁首

## 安全清單集合項目的雜湊

將安全清單集合項目當作二進位大型物件，儲存為跨三種使用者物件屬性 (**msExchSafeSenderHash**、**msExchSafeRecipientHash** 與 **msExchBlockedSendersHash**) 的陣列集之前，會先對這些安全清單集合項目進行單向雜湊處理 (SHA-256)。對資料進行雜湊處理時，會產生固定長度的輸出；該輸出也應該是唯一的。對於安全清單集合項目的雜湊處理，則會產生 4 位元組的雜湊。當收到來自網際網路的郵件時，Exchange 就會雜湊處理寄件者地址，並且將它與代表郵件傳送目標之 Outlook 使用者而儲存的雜湊進行比較。如果寄件者符合安全寄件者雜湊，該郵件就會略過內容篩選。如果寄件者符合封鎖的寄件者雜湊，便會封鎖該郵件。

單向的安全清單集合項目雜湊處理可執行下列重要功能：

  - **最小化儲存及複寫空間**   在大部分情形中，雜湊處理都能夠減少已雜湊資料的大小。因此，儲存並傳輸安全清單集合項目的已雜湊版本，可節省儲存區空間及複寫時間。例如，在其安全清單集合中含有 200 個項目的使用者可以建立大小約為 800 個位元組的雜湊資料，這些資料是在 Active Directory 中進行儲存及複寫。

  - **可讓惡意使用者無法利用使用者安全清單集合**   因為單向雜湊值不可能進行反向工程來變回原始的 SMTP 位址或網域，所以安全清單集合會讓可能入侵 Exchange 伺服器的惡意使用者無法使用那些電子郵件地址。

回到頁首

## 啟用安全清單彙總

Exchange 2013 中預設會啟用安全清單彙總。與 Exchange Server 2007 不同的是，您不需要手動執行 **Update-SafeList** Cmdlet 來雜湊處理安全清單集合資料以及將其寫入 Active Directory。在 Exchange 2013 中，安全清單集合資料是由垃圾郵件選項信箱助理員來寫入 Active Directory。

若要讓 Active Directory 中的安全清單彙總資料能夠供周邊網路中的 Edge Transport Server 使用，您需安裝並設定 Microsoft Exchange EdgeSync 服務，讓安全清單彙總資料能夠複寫至 AD LDS。

您仍可以使用 **UpdateSafelist** 指令程式，以手動方式執行安全清單彙總。不過，您需要注意執行此命令時會產生的網路和複寫流量。對頻繁使用安全清單的多個信箱執行 **Update-Safelist**，可能會產生大量的流量。建議您若要對多個信箱執行此命令，應該在離峰、非上班時間執行命令。

**Update-SafeList** 指令程式會讀取使用者信箱中的安全清單集合、雜湊處理每個項目、排序項目以利於搜尋，然後將雜湊轉換為二進位屬性。最後，**Update-SafeList** 指令程式會將所建立的二進位屬性，與屬性中儲存的任何值進行比較。如果兩個值相同，**Update-SafeList** 指令程式就不會使用安全清單彙總資料來更新使用者屬性值。如果兩個屬性值不同，**Update-SafeList** 指令程式就會更新安全清單彙總值。

回到頁首

