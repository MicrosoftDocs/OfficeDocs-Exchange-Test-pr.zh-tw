---
title: '比對方法和規則套件的技術: Exchange Online Help'
TOCTitle: 比對方法和規則套件的技術
ms:assetid: 09fe9278-d077-452c-b7e5-729b3dc70b1b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ674702(v=EXCHG.150)
ms:contentKeyID: 50472520
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 比對方法和規則套件的技術

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2016-07-28_

本主題說明如何符合模式和證據資料外洩防護 (DLP) XML 檔案包含您自己的自訂的敏感資訊類型規則套件的設計元素。建立正確的 XML 檔案之後，您可以使用 Exchange 系統管理中心 (EAC) 或 Exchange 管理命令介面以協助建立 Microsoft Exchange Server 2013 DLP 解決方案匯入檔案。您可以設定之前，請使用此處所述的對應方法，您應該已啟動 DLP XML 檔案。如需定義您自己的 DLP 範本和 XML 檔案的詳細資訊，請參閱[定義自己的 DLP 範本和資訊類型](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)。

## 比對元素

`Match`元素用在`Pattern`與`Evidence`元素代表基礎關鍵字、 regex 或即將比對的函數。比對本身的定義儲存外部`Rule`元素，並參照到`idRef`必要的屬性。多個`Match`元素可以包含圖樣定義其可以直接在`Pattern`元素中包含或結合使用`Any`元素來定義比對語意中。

    <?xml version="1.0" encoding="utf-8"?>
    <Rules packageId="...">
            ...
    <Entity id="...">
      <Pattern confidenceLevel="85">
                 <IdMatch idRef="FormattedSSN" />
                 <Match idRef="USDate" />
                 <Match idRef="USAddress" />
      </Pattern>
    </Entity>
            ...
             <Keyword id="FormattedSSN "> ... </Keyword>
             <Regex id=" USDate "> ... </Regex>
             <Regex id="USAddress"> ... </Regex>
            ...
    
    </Rules>

## 定義關鍵字比對

規則的一般需求是以符合根據已知關鍵字字串運算式。這被藉由使用`Keyword`元素。關鍵字元素具有會做為相對應的實體或相似性規則中參照 \[識別碼\] 屬性。可在多個實體與親和性規則參照單一關鍵字項目。

比對可以使用執行完全相符還是 word 相符基礎演算法。完全相符會使用搜尋區分大小寫演算法中指定之語言的文字。Word 相符項目適用於 word 的限制為基礎的比對演算法。要比對的條款可以包含的內嵌關鍵字定義中使用的字詞子元素。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用常數型相符項目樣式透過獲得更佳的效率和效能的 regex。比對只在其中常數基礎符合的情況下使用 regex 不足夠且需要的規則運算式的彈性。</td>
</tr>
</tbody>
</table>


    <Keyword id="Word_Example">
        <Group matchStyle="word">
           <Term>card verification</Term>
           <Term>cvn</Term>
           <Term>cid</Term>
           <Term>cvc2</Term>
           <Term>cvv2</Term>
           <Term>pin block</Term>
           <Term>security code</Term>
        </Group>
    </Keyword>
    ...
    <Keyword id="String_Example">
        <Group matchStyle="string">
           <Term>card</Term>
           <Term>pin</Term>
           <Term>security</Term>
        </Group>
    </Keyword>

## 定義規則運算式的比對

根據規則運算式的比對的另一種常見方法。規則運算式相符的彈性讓這一般選擇實作相符項目資料，如駕授權號碼、 地址。一般規則運算式語法用來定義的 regex 模式。此處的表格提供最常見的規則運算式權杖的一些的範例。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用常數透過獲得更佳的效率和效能的 regex 型相符項目樣式。使用 regex 相符僅限在其中常數架構符合的情況下不足夠且需要的規則運算式的彈性。</td>
</tr>
</tbody>
</table>



<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>符號</th>
<th>意義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>c</p></td>
<td><p>根據字面比對 c 字元，除非它是其中一個特殊字元。</p></td>
</tr>
<tr class="even">
<td><p>^</p></td>
<td><p>比對一行的開頭。</p></td>
</tr>
<tr class="odd">
<td><p>.</p></td>
<td><p>比對任一非新行的字元。</p></td>
</tr>
<tr class="even">
<td><p>$</p></td>
<td><p>比對一行的結尾。</p></td>
</tr>
<tr class="odd">
<td><p>|</p></td>
<td><p>運算式之間的邏輯 OR。</p></td>
</tr>
<tr class="even">
<td><p>()</p></td>
<td><p>群組子運算式。</p></td>
</tr>
<tr class="odd">
<td><p>[]</p></td>
<td><p>定義字元等級。</p></td>
</tr>
<tr class="even">
<td><p>*</p></td>
<td><p>不比對上述運算式或比對更多次。</p></td>
</tr>
<tr class="odd">
<td><p>+</p></td>
<td><p>比對一次或更多次上述運算式。</p></td>
</tr>
<tr class="even">
<td><p>?</p></td>
<td><p>不比對上述運算式或比對一次。</p></td>
</tr>
<tr class="odd">
<td><p>{<em>n</em>}</p></td>
<td><p>比對 <em>n</em> 次上述運算式。</p></td>
</tr>
<tr class="even">
<td><p>{<em>n</em>}</p></td>
<td><p>至少比對 <em>n</em> 次上述運算式。</p></td>
</tr>
<tr class="odd">
<td><p>{<em>n, m</em>}</p></td>
<td><p>至少比對 <em>n</em> 次上述運算式，最多比對 <em>m</em> 次。</p></td>
</tr>
<tr class="even">
<td><p>\d</p></td>
<td><p>比對一位數。</p></td>
</tr>
<tr class="odd">
<td><p>\D</p></td>
<td><p>比對不是位數的字元。</p></td>
</tr>
<tr class="even">
<td><p>\w</p></td>
<td><p>比對字母字元，包含底線。</p></td>
</tr>
<tr class="odd">
<td><p>\W</p></td>
<td><p>比對不是字母字元的字元。</p></td>
</tr>
<tr class="even">
<td><p>\s</p></td>
<td><p>比對一個空白字元（任何 \t、 \n、 \r 或 \f)。</p></td>
</tr>
<tr class="odd">
<td><p>\S</p></td>
<td><p>比對一個非空白字元。</p></td>
</tr>
<tr class="even">
<td><p>\t</p></td>
<td><p>索引標籤。</p></td>
</tr>
<tr class="odd">
<td><p>\n</p></td>
<td><p>新行。</p></td>
</tr>
<tr class="even">
<td><p>\r</p></td>
<td><p>歸位字元。</p></td>
</tr>
<tr class="odd">
<td><p>\f</p></td>
<td><p>換頁字元。</p></td>
</tr>
<tr class="even">
<td><p>\<em>m</em></p></td>
<td><p>逸出<em>m</em>，其中<em>m</em>是其中一個以上所述的中繼字元： ^，。，$、 |、 （）、 []、 *，+ ?，\，或 /。</p></td>
</tr>
</tbody>
</table>


Regex 元素具有會做為相對應的實體或相似性規則中參照 \[識別碼\] 屬性。可在多個實體與親和性規則參照的單一 Regex 元素。Regex 運算式會定義為 Regex 元素的值。

    <Regex id="CCRegex">
         \bcc\#\s|\bcc\#\:\s
    </Regex>
    ...
    <Regex id="ItinFormatted">
        (?:^|[\s\,\:])(?:9\d{2})[- ](?:[78]\d[-  
         ]\d{4})(?:$|[\s\,]|\.\s)
    </Regex>
    ...
    <Regex id="NorthCarolinaDriversLicenseNumber">
        (^|\s|\:)(\d{1,8})($|\s|\.\s)
    </Regex>

## 結合多個比對元素

若要增加相符信賴常用的技術可以定義多個的相符項目之間的語意，例如的一或多個相符項目需要進行。Any 元素允許的邏輯架構符合多個項目之間的定義。子元素的圖樣元素中可用的任何項目。它會包含一或多個相符子元素，並定義符合項目的兩者之間的邏輯。請參閱下方的所有的相符項目、 「 不 」 邏輯及完全相符項目計數任何元素的 XML 程式碼範例。

可以使用選用的 minMatches 屬性 (預設值 = 1) 定義必須符合滿足相符的相符項目數目最小值。同樣地，可以使用選用 maxMatches 屬性 (預設值 = 子系相符項目數目) 定義的相符項目必須符合滿足相符項目數目上限。這些條件結合使用邏輯運算元根據用量之 minMatches 和 maxMatches 屬性，讓下列語意︰

  - 比對所有子比對元素
    
    不比對任何子比對元素
    
    比對任一子比對元素的精確子集

<!-- end list -->

    <Any minMatches="3" maxMatches="3">
        <Match idRef="USDate" />
        <Match idRef="USAddress" />
        <Match idRef="Name" />
    </Any>

    <Any maxMatches="0">
        <Match idRef="USDate" />
        <Match idRef="USAddress" />
        <Match idRef="Name" />
    </Any>

    <Any minMatches="1" maxMatches="1">
        <Match idRef="USDate" />
        <Match idRef="USAddress" />
        <Match idRef="Name" />
    </Any>

## 以更多辨識來增加信賴等級

針對實體基底規則、 的增加信賴的另一個作法是可以定義多個圖樣元素，每個增加佐證性證據數目。作法為使用 minMatches 與 maxMatches 的任何項目建立獨立模式增加信賴等級根據增加佐證性證據數目。例如：

  - 如果找到一段佐證性證據： 信賴等級為 65%

  - 若兩個部分： 信賴等級為 75%

  - 如果第三部分： 信賴等級為 85%

<!-- end list -->

    <Entity id="..." patternsProximity="300" >
        <Pattern confidenceLevel="65">
            <IdMatch idRef="UnformattedSSN" />
            <Any maxMatches="1">
                <Match idRef="USDate" />
                <Match idRef="USAddress" />
                <Match idRef="Name" />
            </Any>
        </Pattern>
        <Pattern confidenceLevel="75">
            <IdMatch idRef="UnformattedSSN" />
            <Any minMatches="2" maxMatches="2">
                <Match idRef="USDate" />
                <Match idRef="USAddress" />
                <Match idRef="Name" />
            </Any>
        </Pattern>
        <Pattern confidenceLevel="85">
            <IdMatch idRef="UnformattedSSN" />
            <Any minMatches="3">
                <Match idRef="USDate" />
                <Match idRef="USAddress" />
                <Match idRef="Name" />
            </Any>
        </Pattern>
    </Entity>

## 範例： 美國證規則

本節包含簡介描述所製作的比對美國社會安全號碼的規則。首先，開始使用我們要如何識別包含社會安全號碼的內容的描述。如果，找到社會安全號碼：

1.  Regex 與格式化 SSN 相符（且在有效的 SSN 範圍內）

2.  確切的辨識   必須在附近出現以下其中一個項目：
    
    1.  關鍵字比對 {社會安全、 Soc Sec、 SSN、SSNS、 SSN \#、 SS\#、 SSID}
    
    2.  代表美國地址的文字
    
    3.  代表日期的文字
    
    4.  代表姓名的文字

接下來，請將說明轉譯為規則架構呈現：

    <Entity id="a44669fe-0d48-453d-a9b1-2cc83f2cba77"
             patternsProximity="300" RecommendedConfidence="85">
        <Pattern confidenceLevel="85">
          <IdMatch idRef="FormattedSSN" />
          <Any minMatches="1">
              <Match idRef="SSNKeywords" />
              <Match idRef="USDate" />
              <Match idRef="USAddress" />
              <Match idRef="Name" />
          </Any>
        </Pattern>
    </Entity>

## 相關資訊

[資料遺失防護](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[定義自己的 DLP 範本和資訊類型](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)

[從檔案匯入自訂的 DLP 原則範本](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)

