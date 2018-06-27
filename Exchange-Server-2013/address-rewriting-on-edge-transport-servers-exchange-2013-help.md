---
title: '地址修正 Edge Transport server 上: Exchange 2013 Help'
TOCTitle: 地址修正 Edge Transport server 上
ms:assetid: 23f1eaf6-247a-4671-ad72-aae19d9b511d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa996806(v=EXCHG.150)
ms:contentKeyID: 61060513
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 地址修正 Edge Transport server 上

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

地址修正會對透過 Edge Transport Server 進入或離開您的組織的郵件，修改寄件者和收件者的電子郵件地址。Edge Transport Server 上有兩個傳輸代理程式提供此修正功能：地址修正輸入代理程式和地址修正輸出代理程式。對輸出郵件進行地址修正的主要原因，是為了向外部收件者呈現單一而一致的電子郵件網域。對輸入郵件進行地址修正的主要原因，則是為了將郵件傳遞給正確的收件者。

您所建立的*「地址修正項目」*會指定內部地址 (您要變更的電子郵件地址) 和外部地址 (您想要的最終電子郵件地址)。您可以指定要同時修正輸入和輸出郵件中的電子郵件地址，或是僅修正輸出郵件的電子郵件地址。您可以為單一使用者建立地址寫入項目 (chris@contoso.com 修正為 support@contoso.com)、為單一網域中的所有使用者建立 (contoso.com 修正為 fabrikam.com)，或為多個子網域 (有例外狀況) 中的使用者建立 (\*.fabrikam.com 修正為 contoso.com，但 legal.fabrikam.com 除外)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>無論您想要如何使用地址修正，您都必須確認產生的電子郵件地址在您的組織中是唯一的，以免出現重複項目。這是因為地址修正並不會驗證修正後的電子郵件是否具有獨特性。</td>
</tr>
</tbody>
</table>


**目錄**

Address rewriting scenarios

Message properties modified by address rewriting

What address rewriting doesn't change

Considerations for outbound-only address rewriting

Considerations for inbound and outbound address rewriting

Considerations for rewriting addresses in multiple domains

Priority of address rewrite entries

Digitally signed, encrypted, and rights-protected messages

## 地址修正的案例

下列案例將說明您可以如何使用地址修正：

  - **群組合併**   有些組織基於企業或技術需求，將其內部企業區分為不同的網域。此組態會造成電子郵件看似來自不同群組，甚至不同組織。
    
    下列範例說明 Contoso, Ltd. 這個組織如何對外部收件者隱藏其內部子網域：
    
      - 來自 northamerica.contoso.com、europe.contoso.com 和 asia.contoso.com 網域的輸出郵件經過修正後，看似來自單一 contoso.com 網域。所有郵件在通過 Edge Transport server 時會修正，這些伺服器在整個組織和網際網路之間提供 SMTP 連線。
    
      - 傳給 contoso.com 收件者的輸入郵件，由 Edge Transport Server 轉送至信箱伺服器。郵件會根據收件者信箱上設定的 Proxy 位址，傳遞給正確的收件者。

  - **併購和收購**   被收購的公司可能繼續以個別企業的形式運作，但您可以使用地址修正功能，讓這兩個組織看起來像是一個整合的組織。
    
    下列範例說明 Contoso, Ltd. 如何隱藏新收購的公司 Fourth Coffee 的電子郵件網域：
    
      - Contoso, Ltd. 想讓所有來自 Fourth Coffee Exchange 組織的輸出郵件，看起來都像是從 Contoso.com 所發出。來自這兩個組織的所有郵件皆透過 Contoso, Ltd. 的 Edge Transport Server 進行傳送；在此處，電子郵件會從 *user*@fourthcoffee.com 修正為 *user*@contoso.com。
    
      - 傳至 *user*@contoso.com 的輸入郵件會進行修正，並路由傳送至 *user*@fourthcoffee.com 信箱。傳送至 *user*@fourthcoffee.com 的輸入郵件，會直接路由傳送至 Fourth Coffee 的電子郵件伺服器。

  - **合作夥伴**   許多組織都會使用外部合作夥伴，來提供服務給客戶、其他組織或該組織本身。為了避免混淆，組織可以用自己的電子郵件網域來取代合作夥伴組織的電子郵件網域。
    
    下列範例說明 Contoso, Ltd. 如何隱藏合作夥伴的電子郵件網域：
    
      - Contoso, Ltd. 會對更大型的 Wingtip Toys 組織提供支援。Wingtip Toys 希望其電子郵件對客戶而言能有整體感，因此，Contoso, Ltd. 的支援人員所發出的所有郵件，看起來必須像是從 Wingtip Toys 傳送的一樣。所有與 Wingtip Toys 相關的輸出郵件都會透過其 Edge Transport Server 傳送，使所有 contoso.com 電子郵件地址修正為 wingtiptoys.com 電子郵件地址。
    
      - support@wingtiptoys.com 的輸入郵件會由 Wingtip Toy 的 Edge Transport Server 所接收，並在修正後路由傳送至 support@contoso.com 電子郵件地址。

回到頁首

## 以地址修正修改的郵件內容

標準 SMTP 電子郵件由「郵件信封」(Message Envelope) 和郵件內容組成。郵件信封包含在 SMTP 郵件伺服器之間傳輸及傳遞郵件所需的資訊。郵件內容包含統稱為 (「郵件標頭」) 的郵件標頭欄位和郵件內容。RFC 2821 會說明郵件信封，而 RFC 2822 會說明郵件標頭。

當寄件者撰寫電子郵件並提交傳遞時，郵件會包含遵循 SMTP 標準所需的基本資訊，例如寄件者、收件者、郵件撰寫的日期和時間、選用的主旨行，以及選用的郵件內文。這些資訊包含在郵件本身，並且也可藉由定義包含在郵件標頭內。

寄件者的郵件伺服器會藉由使用寄件者和收件者位於郵件標頭中的資訊，來產生郵件的郵件信封。然後，它會將郵件傳輸至網際網路，以傳遞至收件者的電子郵件伺服器。收件者一律不會看見郵件信封，因為郵件信封是在郵件傳輸過程中產生的，且實際上不是郵件的一部分。

「地址修正」會修正郵件標頭或郵件信封中的特定欄位，而變更電子郵件地址。地址修正會變更輸出郵件中的數個欄位，但只會變更輸入電子郵件中的一個欄位。下表列出在輸出和輸入郵件受到修正的 SMTP 標頭欄位。

### 在輸出和輸入郵件上修正的郵件欄位

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>欄位名稱</th>
<th>位置</th>
<th>輸出郵件</th>
<th>輸入郵件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>MAIL FROM</strong></p></td>
<td><p>郵件信封</p></td>
<td><p>已修正</p></td>
<td><p>未修正</p></td>
</tr>
<tr class="even">
<td><p><strong>RCPT TO</strong></p></td>
<td><p>郵件信封</p></td>
<td><p>未修正</p></td>
<td><p>已修正</p></td>
</tr>
<tr class="odd">
<td><p><strong>To</strong></p></td>
<td><p>郵件標頭</p></td>
<td><p>已修正</p></td>
<td><p>未修正</p></td>
</tr>
<tr class="even">
<td><p><strong>Cc</strong></p></td>
<td><p>郵件標頭</p></td>
<td><p>已修正</p></td>
<td><p>未修正</p></td>
</tr>
<tr class="odd">
<td><p><strong>寄件者</strong></p></td>
<td><p>郵件標頭</p></td>
<td><p>已修正</p></td>
<td><p>未修正</p></td>
</tr>
<tr class="even">
<td><p><strong>Sender</strong></p></td>
<td><p>郵件標頭</p></td>
<td><p>已修正</p></td>
<td><p>未修正</p></td>
</tr>
<tr class="odd">
<td><p><strong>Reply-To</strong></p></td>
<td><p>郵件標頭</p></td>
<td><p>已修正</p></td>
<td><p>未修正</p></td>
</tr>
<tr class="even">
<td><p><strong>Return-Receipt-To</strong></p></td>
<td><p>郵件標頭</p></td>
<td><p>已修正</p></td>
<td><p>未修正</p></td>
</tr>
<tr class="odd">
<td><p><strong>Disposition-Notification-To</strong></p></td>
<td><p>郵件標頭</p></td>
<td><p>已修正</p></td>
<td><p>未修正</p></td>
</tr>
<tr class="even">
<td><p><strong>Resent-From</strong></p></td>
<td><p>郵件標頭</p></td>
<td><p>已修正</p></td>
<td><p>未修正</p></td>
</tr>
<tr class="odd">
<td><p><strong>Resent-Sender</strong></p></td>
<td><p>郵件標頭</p></td>
<td><p>已修正</p></td>
<td><p>未修正</p></td>
</tr>
</tbody>
</table>


回到頁首

## 地址修正不會變更的項目

地址修正不會修改任何會妨礙到 SMTP 功能的郵件標頭欄位。例如，若修改特定標頭欄位，可能會影響到路由迴圈偵測、使簽章失效，或者使權限受到保護的郵件無法讀取。因此，地址修正不會修改下列標頭欄位。

  - **Return-Path**

  - **Received**

  - **Message-ID**

  - **X-MS-TNEF-Correlator**

  - **Content-Type Boundary=string**

  - 位於 MIME 內文部分中的標頭欄位

地址修正會忽略未受 Exchange 組織控制的網域。換句話說，若標頭欄位中包含 Exchange 組織不具權限的網域，「地址修正」即不會加以修正。修正這類網域會造成無法控制的郵件轉送格式。

地址修正也不會修改內嵌於另一封郵件內之郵件的標題欄位。寄件者和收件者預期內嵌郵件會維持不變，只要郵件不觸發寄件者和收件者之間執行的傳輸規則，郵件在傳送時就不會遭到修改。

回到頁首

## 僅限輸出的地址修正的注意事項

對 Edge Transport Server 進行僅限輸出的地址修正時，將會在郵件從 Exchange 組織送出時修改寄件者的電子郵件地址。您可以為單一使用者設定僅限輸出的地址修正 (chris@contoso.com 修正為 support@contoso.com)，或為單一網域中的所有使用者設定 (contoso.com 修正為 fabrikam.com)。您必須為多個子網域中的使用者設定僅限輸出的地址修正 (\*.fabrikam.com 修正為 .contoso.com)。

修正後的電子郵件地址必須設定為受影響之收件者的 Proxy 位址。例如，如果 laura@sales.contoso.com 修正為 laura@contoso.com，則必須在 Laura 的信箱上設定 Proxy 位址 laura@contoso.com。這允許正確地傳遞回覆和輸入郵件。

回到頁首

## 輸入和輸出地址修正的注意事項

對 Edge Transport Server 進行輸入和輸出或*「雙向」*地址修正時，會在 Exchange 組織所送出的郵件中修改寄件者的電子郵件地址，並且在進入 Exchange 組織的郵件中修改收件者的電子郵件地址。

您可以為單一使用者設定僅限輸出的地址修正 (chris@contoso.com 修正為 support@contoso.com)，並且為單一網域中的所有使用者設定 (contoso.com 修正為 fabrikam.com)。您必須為多個子網域中的使用者設定雙向地址修正 (\*.fabrikam.com 修正為 .contoso.com)。

回到頁首

## 修正多個網域中的電子郵件地址的注意事項

當您將多個內部網域或子網域合併為單一外部網域時，您必須考量下列因素：

  - **驗證唯一別名**   所有電子郵件別名 (@ 符號左側的部分) 在所有子網域間都必須是唯一的。比方說，如果有 joe@sales.contoso.com，就不能有 joe@marketing.contoso.com，因為這兩個使用者修正後的電子郵件地址都將是 joe@contoso.com。

  - **新增 Proxy 位址**   修正後的電子郵件地址必須在受影響的網域中設定為所有受影響之寄件者的 Proxy 位址。例如，如果 joe@sales.contoso.com 修正為 joe@contoso.com，您就必須將 Proxy 位址 joe@contoso.com 新增至 Joe 的信箱。這允許正確地傳遞回覆和輸入郵件。

  - **非 Exchange 組織的郵件連絡人**   如果您要修正非 Exchange 電子郵件系統中的電子郵件地址，您必須在 Exchange 中建立電子郵件連絡人來代表非 Exchange 電子郵件系統中的使用者。這些電子郵件連絡人必須包含原始的電子郵件地址和修正後的電子郵件地址。例如，如果 joe@unix.contoso.com 修正為 joe@contoso.com，則您必須建立以 joe@unix.contoso.com 作為外部電子郵件地址、並以 joe@contoso.com 作為 Proxy 位址的郵件連絡人。

## 驗證唯一別名

當您修正多個子網域中的電子郵件地址時，您必須確定所有電子郵件別名在您所有的子網域間都是唯一的。例如，請看下列組態：

下列使用者位於 sales.contoso.com、marketing.contoso.com 和 research.contoso.com 子網域中：

  - maria@sales.contoso.com

  - chris@sales.contoso.com

  - david@marketing.contoso.com

  - brian@marketing.contoso.com

  - chris@research.contoso.com

  - adam@research.contoso.com

假設您想將 sales.contoso.com、marketing.contoso.com 和 research.contoso.com into 這三個子網域修正為單一網域 contoso.com。

在修正各個子網域中的電子郵件地址時，chris@sales.contoso.com 與 chris@research.contoso.com 之間會發生衝突，因為這兩個電子郵件地址都會修正為 chris@contoso.com。若要解決此狀況，您必須變更其中一個受影響之收件者的電子郵件地址。例如，您可以將 chris@research.contoso.com 變更為 christopher@research.contoso.com，使其電子郵件地址修正為 christopher@contoso.com。

回到頁首

## 地址修正項目的優先順序

如果使用者的電子郵件地址符合多個地址修正項目，其電子郵件地址將只會根據最接近的相符項目修正一次。下列清單說明地址修正項目的優先順序 (從最高優先順序到最低優先順序)：

1.  **個別電子郵件地址**   地址修正項目依設定會將 john@contoso.com 的電子郵件地址修正為 support@contoso.com。

2.  **網域或子網域對應**   地址修正項目依設定會將所有的 contoso.com 電子郵件地址修正為 northwindtraders.com，或將所有的 sales.contoso.com 電子郵件地址修正為 contoso.com。

3.  **網域簡維**   地址修正項目依設定會將 \*.contoso.com 電子郵件地址修正為 contoso.com。

例如，請考量設定了下列輸出地址修正項目的 Edge Transport Server：

  - \*.contoso.com 電子郵件地址會修正為 contoso.com

  - japan.sales.contoso.com 電子郵件地址會修正為 contoso.jp

如果 masato@japan.sales.contoso.com 傳送了電子郵件，其地址將會修正為 masato@contoso.jp，因為該項目最符合寄件者的電子郵件地址。

回到頁首

## 數位簽章、加密和權限受保護的郵件

地址修正不得影響大部分已簽章、加密或權限受保護的郵件。如果地址修正會以任何形式使這些類型的郵件失效或變更其安全性狀態，則不會套用地址修正。

下列值由於不是郵件簽章、加密或權限保護的一部分，因此是可以修正的：

  - 郵件信封中的欄位

  - 最上層郵件內文標題

下列值屬於郵件簽章、加密或權限保護的一部分，因此不會修正：

  - 位於可能已簽章之 MIME 內文部分中的標頭欄位

  - MIME 內容類型的界限字串參數

回到頁首

