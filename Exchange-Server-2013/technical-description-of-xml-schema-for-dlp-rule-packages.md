---
title: '開發敏感資訊規則套件: Exchange Online Help'
TOCTitle: 開發敏感資訊規則套件
ms:assetid: c4ab8707-0839-4855-9390-3dbcb43475a7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ674704(v=EXCHG.150)
ms:contentKeyID: 50474211
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 開發敏感資訊規則套件

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2016-07-28_

XML 結構描述及本主題中的指導可協助您開始建立您自己的基本資料遺失防護 (DLP) XML 檔案的分類規則套件中定義您自己的敏感資訊類型。建立正確的 XML 檔案之後，您可以使用 Exchange 系統管理中心或 Exchange 管理命令介面以協助建立 Microsoft Exchange Server 2013 DLP 解決方案匯入它。為自訂的 DLP 原則範本 XML 檔案可以包含為您的分類規則套件的 XML。如需定義您自己的 DLP 範本為 XML 檔案的概觀，請參閱[定義自己的 DLP 範本和資訊類型](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)。

**目錄**

Overview of the rule authoring process

Rule description

Basic rule structure

Using local languages in your XML file

Classification rule pack XML schema definition

For more information

## 編寫規則程序概觀

編寫規則的程序包含下列的一般步驟。

1.  準備一組的代表性的目標環境的測試文件。要考量的測試文件集的主要特性包含： 子集的文件包含的實體或相似性其所製作此規則，並不包含的實體或相似性之規則所製作的子集的文件。

2.  找出符合驗收需求 （precision 和重新叫用） 來識別內容到合格的規則。這可能需要開發的規則，以搭配滿足識別目標文件的最小相符項目需求與布林邏輯繫結內的多個條件。

3.  建立根據驗收需求 （precision 和重新叫用） 規則的建議的信賴等級。建議的信賴元素可以視為規則的預設信賴等級。

4.  具現化與這些原則和監控範例測試內容的驗證規則。根據結果，調整規則或同時減少誤判與負片提高偵測到的內容的信賴等級。繼續驗證和規則調整的週期直到正值與負值範例到達內容偵測夠用層級\]。

如需原則範本檔之 XML 架構定義的詳細資訊，請參閱 [開發 DLP 原則範本檔案](xml-rule-schema-and-rule-structure-guide-for-dlp-policy-files.md)。

## 規則說明

可以製作 DLP 敏感資訊偵測引擎的兩個主要的規則類型︰ 實體與親和性。選擇規則類型為基礎的處理邏輯應套用至內容的處理前文各節所述的類型。規則定義在 XML 文件中所述標準化規則 XSD 格式設定。規則說明這兩個內容類型的相符項目及所述的比對代表目標內容的信賴等級。信賴等級指定如果內容中找到圖樣會出現之實體的機率或要呈現如果內容中找到證據親和性的機率。

## 基本規則結構

規則定義由三個主要元件構成：

1.  **實體**   可定義該規則的比對和計數邏輯

2.  **親和性**   可定義規則的比對邏輯

3.  **當地語系化字串**   當地語系化的規則名稱和說明

三個額外的支援項目所用的定義處理的詳細資料和參照中的主要元件： 關鍵字、 Regex 及函數。藉由使用參考資料，支援的項目，社會安全號碼，例如單一定義可用來在多個實體或相似性規則。以 XML 格式的基本規則結構可以看起來會有如下。

    <?xml version="1.0" encoding="utf-8"?>
    <RulePackage xmlns="http://schemas.microsoft.com/office/2011/mce">
    
      <RulePack id="DAD86A92-AB18-43BB-AB35-96F7C594ADAA">
        <Version major="1" minor="0" build="0" revision="0"/>
        <Publisher id="619DD8C3-7B80-4998-A312-4DF0402BAC04"/>
        <Details defaultLangCode="en-us">
          <LocalizedDetails langcode="en-us">
            <PublisherName>DLP by EPG</PublisherName>
            <Name>CSO Custom Rule Pack</Name>
            <Description>This is a rule package for a EPG demo.</Description>
          </LocalizedDetails>
        </Details>
      </RulePack>
    
      <Rules>
    
        <!-- Employee ID -->
        <Entity id="E1CC861E-3FE9-4A58-82DF-4BD259EAB378" patternsProximity="300" recommendedConfidence="75">
          <Pattern confidenceLevel="75">
            <IdMatch idRef="Regex_employee_id" />
            <Match idRef="Keyword_employee" />
          </Pattern>
        </Entity>
    
        <Regex id="Regex_employee_id">(\s)(\d{9})(\s)</Regex>
        <Keyword id="Keyword_employee">
          <Group matchStyle="word">
            <Term>Identification</Term>
            <Term>Contoso Employee</Term>
          </Group>
        </Keyword>
    
    
        <LocalizedStrings>
    
          <Resource idRef="E1CC861E-3FE9-4A58-82DF-4BD259EAB378">
            <Name default="true" langcode="en-us">
              Employee ID
            </Name>
            <Description default="true" langcode="en-us">
              A custom classification for detecting Employee ID's
            </Description>
          </Resource>
    
        </LocalizedStrings>
      </Rules>
    </RulePackage>

## 實體規則

實體規則所選取的目標向也已定義的識別碼，例如社會安全號碼，並分別代表一群 countable 模式的。實體規則會傳回計數與信賴等級的相符項，其中 Count 是所找到之實體的執行個體的總數而信賴等級為指定的實體存在於指定的文件中的機率。實體包含"id"屬性做為其唯一識別碼。識別碼用於當地語系化、 版本設定及查詢。實體 id 必須是 GUID 並不應重複中其他實體或相似性。參照的當地語系化的字串\] 區段中。

實體規則包含選用 patternsProximity 屬性 (預設值 = 300) 套用布林值來指定多個模式的相鄰關係的邏輯需要滿足比對條件時才會使用。實體元素包含 1 或多個圖樣子項，其中每個模式是信用卡實體或驅動程式的授權實體像實體以不同方式呈現。圖樣元素有 confidenceLevel 代表圖樣精確度根據範例資料集的必要的屬性。圖樣元素可以有三個子元素：

1.  IdMatch - 此為必要的。

2.  Match

3.  任何

如果任何圖樣元素傳回"true"、 被滿足模式。實體元素的數目等於所有偵測到的圖樣計數的總和。

![實體計數的數學公式](images/JJ674704.25309939-98bc-4460-8f89-8560bbad7981(EXCHG.150).gif "實體計數的數學公式")

其中 k 是實體模式元素的數目。

圖樣元素必須具有完全 IdMatch 元素。IdMatch 代表模式是以配合，例如信用卡號或 ITIN 號碼的識別碼。圖樣的計數是 IdMatches 符合為圖樣的元素數目。IdMatch 元素錨定的相符項目鄰近視窗。

圖樣元素的選用子元素另一個是代表佐證性證據所需的對應至支援尋找 IdMatch 元素的相符項目。例如，更高信賴規則可能需要以及尋找信用卡號、 其他成品存在於信用卡 like 位址和名稱的鄰近視窗內的文件。這些額外的成品會透過符合元素或 （說明在比對方法和技術 （英文） 區段中的詳細資料） Any 元素表示。多個符合元素可以包含其中可包括直接在圖樣項目或結合使用的任何項目來定義符合語意圖樣定義中。它會傳回鄰近視窗錨定周圍 IdMatch 內容中找到相符項目，則為 true。

IdMatch 和相符項目執行動作未定義的詳細資料的內容為何需要符合但改用參照到 idRef 屬性。這會升階定義多個圖樣建構中重複使用的性。

    <Entity id="..." patternsProximity="300" > 
        <Pattern confidenceLevel="85">
            <IdMatch idRef="FormattedSSN" />
            <Any minMatches="1">
                <Match idRef="SSNKeyword" />
                <Match idRef="USDate" />
                <Match idRef="USAddress" />
                <Match idRef="Name" />
            </Any>
        </Pattern>  
        <Pattern confidenceLevel="65">
            <IdMatch idRef="UnformattedSSN" />
            <Match idRef="SSNKeyword" />
            <Any minMatches="1">        
                <Match idRef="USDate" />
                <Match idRef="USAddress" />
                <Match idRef="Name" />
            </Any>
        </Pattern>
    </Entity> 

在之前的 XML 中以 \&quot;…\&quot; 呈現的實體識別碼元素應為 GUID，且地語系化的字串區段會參照此識別碼。

## 實體模式近似值視窗

實體保留選用 patternsProximity 屬性值 (整數、 預設值 = 300) 用來尋找模式。每個模式屬性值會定義從 IdMatch 位置的所有其他符合該模式為指定的距離 （以 Unicode 字元）。 IdMatch 位置，使用視窗，延伸至左邊和右邊 IdMatch 錨定鄰近視窗。

![叫出比對元素的文字模式](images/JJ674704.65d52989-f50f-4097-b39a-9612f860d727(EXCHG.150).gif "叫出比對元素的文字模式")

下列範例會說明鄰近\] 視窗會比對出 SSN IdMatch 元素需要至少的地址、 名稱或 corroborating 符合項目的日期的 1 的演算法的影響。只有 SSN1 及 SSN4 符合因為 SSN2 及 SSN3，其中一個否或局部的 corroborating 證據找到鄰近視窗內。

![鄰近規則比對和非比對範例](images/JJ674704.8117deb3-d8c8-4d4e-a011-ac5f9990b08e(EXCHG.150).gif "鄰近規則比對和非比對範例")

請注意郵件內文和每個附件都視為獨立的項目。這表示鄰近視窗不會將以外的每個這些項目的結尾。每個項目 （附件或內文） idMatch 與佐證性證據必須位於每個。

## 實體信賴等級

實體元素信賴等級為所有滿足的圖樣的信賴等級的組合。他們被結合使用下列方程式：

![實體信賴等級的數學公式](images/JJ674704.9b8bb9c8-3ded-4ea5-a609-71d8034b1017(EXCHG.150).gif "實體信賴等級的數學公式")

其中 k 是實體的模式元素數目，而不符合的模式會傳回 0 信賴等級。

請參閱實體元素結構程式碼範例，若兩種模式都符合，就會依據下列計算傳回 94.75% 的實體信賴等級：

CLEntity= 1-\[(1-CLPattern1) x (1-CLPattern1)\]

*= 1-\[(1-0.85) x (1-0.65)\]*

*= 1-(0.15 x 0.35)*

*= 94.75%*

同樣地，若僅有第二種模式符合，就會依據下列計算傳回 65% 的實體信賴等級：

CLEntity= 1 – \[(1 – CLPattern1) X (1 – CLPattern1)\]

*= 1 – \[(1 – 0) X (1 – 0.65)\]*

*= 1 – (1 X 0.35)*

*= 65%*

系統會將這些信賴值指派給個別模式的規則，而這些模式是以規則編寫程序中驗證的測試文件集為依據。

## 親和性規則

親和性規則的目標向沒有定義完善的識別碼，例如沙賓法案或公司的財務內容的內容。為此內容可找到任何單一一致識別碼並改用分析需要決定是否存在一群證據。親和性規則不會傳回計數，請改用傳回如果找到與相關聯的信賴等級。親和性的內容被表示為獨立的辨識項的集合。證據是必要的相符項目內某些鄰近的彙總。親和性規則 evidencesProximity 屬性所定義的鄰近 （預設值為 600） 和 thresholdConfidenceLevel 屬性所的最小的信賴等級。

親和性規則包含用於當地語系化、 版本設定及查詢其唯一識別碼的 id 屬性。不同的實體規則親和性規則不依賴定義完善的識別碼，因為它們不包含 IdMatch 元素。

每個親和性規則包含一或多個的子證據元素定義是要找證據與信賴親和性規則所提供的層級。親和性不會被視為找到如果所產生的信賴等級低於臨界值層級。每個證據就必定表示佐證性證據此"類型"的文件並 confidenceLevel 屬性是該證據上測試資料集的精確度。

證據元素有一或多個相符項目或任何子元素。如果所有的子相符項目與任何項目相符，並找到證據的信賴等級為全球都能提供來規則信賴等級計算。同一個說明適用於相符項目或與實體規則親和性規則的任何項目。

    <Affinity id="..." 
              evidencesProximity="1000"
              thresholdConfidenceLevel="65">
        <Evidence confidenceLevel="40">
            <Any> 
                <Match idRef="AssetsTerms" /> 
                <Match idRef="BalanceSheetTerms" /> 
                <Match idRef="ProfitAndLossTerms" /> 
            </Any> 
        </Evidence>
        <Evidence confidenceLevel="40">
            <Any minMatches="2"> 
                <Match idRef="TaxTerms" /> 
                <Match idRef="DollarAmountTerms" /> 
                <Match idRef="SECTerms" /> 
                <Match idRef="SECFilingFormTerms" /> 
                <Match idRef="DollarTotalRegex" /> 
            </Any> 
        </Evidence>
    </Affinity>

## 親和性近似值視窗

親和性鄰近視窗是有不同於針對計算實體模式。相關性鄰近接滑動視窗模型。親和性鄰近演算法會嘗試尋找指定的視窗中的比對的辨識項數目上限。接近視窗中的辨識項必須大於針對要找的親和性規則所定義的臨界值的信賴等級。

![親和性規則比對的鄰近文字](images/JJ674704.2601ec86-0094-43fa-8d22-9d97f7465942(EXCHG.150).gif "親和性規則比對的鄰近文字")

## 親和性信賴等級

親和性的信賴等級等於親和性規則辨識鄰近視窗內的找到項的組合。雖然類似的實體規則的信賴等級的主要差異是鄰近視窗的應用程式。類似的實體規則親和性的元素信賴等級組合所有滿足證據信賴等級，但是親和性規則它只代表找到鄰近視窗內的證據元素的最高組合。使用下列方程式結合證據信賴等級：

![親和性規則信賴的數學公式](images/JJ674704.8a5da4ca-af02-4c5a-ab60-0072dc7e7a0f(EXCHG.150).gif "親和性規則信賴的數學公式")

其中 k 為近似值視窗內符合親和性之辨識項元素的數目。

請參考並回復圖 4 範例親和性規則結構上所有三個辨識項會符合鄰近滑動視窗內的情況下親和性信賴等級是根據以下計算 85.6%。此超過親和性規則臨界值的 65 中的規則比對結果。

CLAffinity= 1 – \[(1 – CLEvidence 1) X (1 – CLEvidence 2) X (1 – CLEvidence 2)\]

*= 1 – \[(1 – 0.6) X (1 – 0.4) X (1 – 0.4)\]*

*= 1 – (0.4 X 0.6 X 0.6)*

*= 85.6%*

![高信賴的親和性規則比對範例](images/JJ674704.e17b2e22-18c3-40c4-8f19-0993bb556675(EXCHG.150).gif "高信賴的親和性規則比對範例")

使用相同的範例規則定義來看，若由於第二個辨識項位在近似值視窗以外，因此只有第一個辨識項符合時，依據下列計算最高的親和性信賴等級就是 60%，且不會符合親和性規則，因為沒有達到闕值 65。

CLAffinity= 1 – \[(1 – CLEvidence 1) X (1 – CLEvidence 2) X (1 – CLEvidence 2)\]

*= 1 – \[(1 – 0.6) X (1 – 0) X (1 – 0)\]*

*= 1 – (0.4 X 1 X 1)*

*= 60%*

![低信賴的親和性規則比對範例](images/JJ674704.077095b1-6eb0-40df-b254-f33437725720(EXCHG.150).gif "低信賴的親和性規則比對範例")

## 調整信賴等級

其中一個撰寫程序之規則的關鍵方面已調整的實體和親和性規則的信賴等級。之後建立的規則定義，請執行規則代表性的內容並收集資料的正確性。比較每個圖樣或測試文件的針對預期的結果證據傳回的結果。

![比較規則比對證明的資料表](images/JJ674704.25a7d9a1-d02f-447e-a88b-8e78bdc0413a(EXCHG.150).gif "比較規則比對證明的資料表")

若規則符合接受需求，亦即，模式或辨識項具備的信賴率高於建立的闕值 (例如 75%)—就完成符合運算式，且可前往下一個步驟。

若模式或辨識項不符合信賴等級，請重新編寫 (例如，新增更多確實辨識項；移除或新增其他模式/辨識項等等) 然後重複此步驟。

根據前一個步驟的結果在規則中的每個模式或證據中下一步\] 調整的信賴等級。每個模式或證據，彙總的則為 True 測 (TP)，內含的實體或相似性規則所製作的文件的子集的號碼與所導致相符項目和數字的 False 測 (FP)，不包含之實體的文件的子集或親和性的所製作之規則的也以及傳回相符項目。設定使用下列計算每個圖樣/證據信賴等級：

*信賴等級 = True Positive / (True Positive + False Positive)*


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>模式或辨識項</th>
<th>True Positive</th>
<th>False Positive</th>
<th>信賴等級</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>P1或 E1</p></td>
<td><p>4</p></td>
<td><p>1</p></td>
<td><p>80%</p></td>
</tr>
<tr class="even">
<td><p>P2或 E2</p></td>
<td><p>2</p></td>
<td><p>2</p></td>
<td><p>50%</p></td>
</tr>
<tr class="odd">
<td><p>Pn或 En</p></td>
<td><p>9</p></td>
<td><p>10</p></td>
<td><p>47%</p></td>
</tr>
</tbody>
</table>


## 在 XML 檔中使用當地語言

規則結構描述支援儲存的本地化的名稱和描述的每個實體與親和性的元素。每個實體與親和性元素必須包含在 LocalizedStrings\] 區段中的對應元素。若要找出每個元素，包含 Resource 元素儲存名稱與說明每個元素的多個地區 LocalizedStrings 元素的子。Resource 元素包含必要的 idRef 屬性以找出對應 idRef 屬性為正在進行當地語系化每個項目。Resource 元素的地區設定子元素包含的本地化的名稱與說明每個指定的地區設定。

    <LocalizedStrings>
        <Resource idRef="guid">
            <Locale langcode="en-US" default="true"> 
                <Name>affinity name en-us</Name> 
                <Description>
                    affinity description en-us
                </Description> 
            </Locale> 
            <Locale langcode="de"> 
                <Name>affinity name de</Name> 
                <Description>
                    affinity description de
                </Description> 
            </Locale> 
        </Resource>
    </LocalizedStrings>

## 分類規則套件 XML 架構定義

    <?xml version="1.0" encoding="utf-8"?>
    <xs:schema xmlns:mce="http://schemas.microsoft.com/office/2011/mce"
               targetNamespace="http://schemas.microsoft.com/office/2011/mce" 
               xmlns:xs="http://www.w3.org/2001/XMLSchema"
               elementFormDefault="qualified"
               attributeFormDefault="unqualified"
               id="RulePackageSchema">
      <xs:simpleType name="LangType">
        <xs:union memberTypes="xs:language">
          <xs:simpleType>
            <xs:restriction base="xs:string">
              <xs:enumeration value=""/>
            </xs:restriction>
          </xs:simpleType>
        </xs:union>
      </xs:simpleType>
      <xs:simpleType name="GuidType" final="#all">
        <xs:restriction base="xs:token">
          <xs:pattern value="[0-9a-fA-F]{8}\-([0-9a-fA-F]{4}\-){3}[0-9a-fA-F]{12}"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:complexType name="RulePackageType">
        <xs:sequence>
          <xs:element name="RulePack" type="mce:RulePackType"/>
          <xs:element name="Rules" type="mce:RulesType">
            <xs:key name="UniqueRuleId">
              <xs:selector xpath="mce:Entity|mce:Affinity"/>
              <xs:field xpath="@id"/>
            </xs:key>
            <xs:key name="UniqueProcessorId">
              <xs:selector xpath="mce:Regex|mce:Keyword"></xs:selector>
              <xs:field xpath="@id"/>
            </xs:key>
            <xs:key name="UniqueResourceIdRef">
              <xs:selector xpath="mce:LocalizedStrings/mce:Resource"/>
              <xs:field xpath="@idRef"/>
            </xs:key>        
            <xs:keyref name="ReferencedRuleMustExist" refer="mce:UniqueRuleId">
              <xs:selector xpath="mce:LocalizedStrings/mce:Resource"/>
              <xs:field xpath="@idRef"/>
            </xs:keyref>
            <xs:keyref name="RuleMustHaveResource" refer="mce:UniqueResourceIdRef">
              <xs:selector xpath="mce:Entity|mce:Affinity"/>
              <xs:field xpath="@id"/>
            </xs:keyref>
          </xs:element>
        </xs:sequence>
      </xs:complexType>
      <xs:complexType name="RulePackType">
        <xs:sequence>
          <xs:element name="Version" type="mce:VersionType"/>
          <xs:element name="Publisher" type="mce:PublisherType"/>
          <xs:element name="Details" type="mce:DetailsType">
            <xs:key name="UniqueLangCodeInLocalizedDetails">
              <xs:selector xpath="mce:LocalizedDetails"/>
              <xs:field xpath="@langcode"/>
            </xs:key>
            <xs:keyref name="DefaultLangCodeMustExist" refer="mce:UniqueLangCodeInLocalizedDetails">
              <xs:selector xpath="."/>
              <xs:field xpath="@defaultLangCode"/>
            </xs:keyref>
          </xs:element>
          <xs:element name="Encryption" type="mce:EncryptionType" minOccurs="0" maxOccurs="1"/>
        </xs:sequence>
        <xs:attribute name="id" type="mce:GuidType" use="required"/>
      </xs:complexType>
      <xs:complexType name="VersionType">
        <xs:attribute name="major" type="xs:unsignedShort" use="required"/>
        <xs:attribute name="minor" type="xs:unsignedShort" use="required"/>
        <xs:attribute name="build" type="xs:unsignedShort" use="required"/>
        <xs:attribute name="revision" type="xs:unsignedShort" use="required"/>
      </xs:complexType>
      <xs:complexType name="PublisherType">
        <xs:attribute name="id" type="mce:GuidType" use="required"/>
      </xs:complexType>
      <xs:complexType name="LocalizedDetailsType">
        <xs:sequence>
          <xs:element name="PublisherName" type="mce:NameType"/>
          <xs:element name="Name" type="mce:RulePackNameType"/>
          <xs:element name="Description" type="mce:OptionalNameType"/>
        </xs:sequence>
        <xs:attribute name="langcode" type="mce:LangType" use="required"/>
      </xs:complexType>
      <xs:complexType name="DetailsType">
        <xs:sequence>
          <xs:element name="LocalizedDetails" type="mce:LocalizedDetailsType" maxOccurs="unbounded"/>
        </xs:sequence>
        <xs:attribute name="defaultLangCode" type="mce:LangType" use="required"/>
      </xs:complexType>
      <xs:complexType name="EncryptionType">
        <xs:sequence>
          <xs:element name="Key" type="xs:normalizedString"/>
          <xs:element name="IV" type="xs:normalizedString"/>
        </xs:sequence>
      </xs:complexType>
      <xs:simpleType name="RulePackNameType">
        <xs:restriction base="xs:token">
          <xs:minLength value="1"/>
          <xs:maxLength value="64"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:simpleType name="NameType">
        <xs:restriction base="xs:normalizedString">
          <xs:minLength value="1"/>
          <xs:maxLength value="256"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:simpleType name="OptionalNameType">
        <xs:restriction base="xs:normalizedString">
          <xs:minLength value="0"/>
          <xs:maxLength value="256"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:simpleType name="RestrictedTermType">
        <xs:restriction base="xs:string">
          <xs:minLength value="1"/>
          <xs:maxLength value="512"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:complexType name="RulesType">
        <xs:sequence>
          <xs:choice maxOccurs="unbounded">
            <xs:element name="Entity" type="mce:EntityType"/>
            <xs:element name="Affinity" type="mce:AffinityType"/>
          </xs:choice>
          <xs:choice minOccurs="0" maxOccurs="unbounded">
            <xs:element name="Regex" type="mce:RegexType"/>
            <xs:element name="Keyword" type="mce:KeywordType"/>
          </xs:choice>
          <xs:element name="LocalizedStrings" type="mce:LocalizedStringsType"/>
        </xs:sequence>
      </xs:complexType>
      <xs:complexType name="EntityType">
        <xs:sequence>
          <xs:element name="Pattern" type="mce:PatternType" maxOccurs="unbounded"/>
        </xs:sequence>
        <xs:attribute name="id" type="mce:GuidType" use="required"/>
        <xs:attribute name="patternsProximity" type="mce:ProximityType" use="required"/>
        <xs:attribute name="recommendedConfidence" type="mce:ProbabilityType"/>
        <xs:attribute name="workload" type="mce:WorkloadType"/>
      </xs:complexType>
      <xs:complexType name="PatternType">
        <xs:sequence>
          <xs:element name="IdMatch" type="mce:IdMatchType"/>
          <xs:choice minOccurs="0" maxOccurs="unbounded">
            <xs:element name="Match" type="mce:MatchType"/>
            <xs:element name="Any" type="mce:AnyType"/>
          </xs:choice>
        </xs:sequence>
        <xs:attribute name="confidenceLevel" type="mce:ProbabilityType" use="required"/>
      </xs:complexType>
      <xs:complexType name="AffinityType">
        <xs:sequence>
          <xs:element name="Evidence" type="mce:EvidenceType" maxOccurs="unbounded"/>
        </xs:sequence>
        <xs:attribute name="id" type="mce:GuidType" use="required"/>
        <xs:attribute name="evidencesProximity" type="mce:ProximityType" use="required"/>
        <xs:attribute name="thresholdConfidenceLevel" type="mce:ProbabilityType" use="required"/>
        <xs:attribute name="workload" type="mce:WorkloadType"/>
      </xs:complexType>
      <xs:complexType name="EvidenceType">
        <xs:sequence>
          <xs:choice maxOccurs="unbounded">
            <xs:element name="Match" type="mce:MatchType"/>
            <xs:element name="Any" type="mce:AnyType"/>
          </xs:choice>
        </xs:sequence>
        <xs:attribute name="confidenceLevel" type="mce:ProbabilityType" use="required"/>
      </xs:complexType>
      <xs:complexType name="IdMatchType">
        <xs:attribute name="idRef" type="xs:string" use="required"/>
      </xs:complexType>
      <xs:complexType name="MatchType">
        <xs:attribute name="idRef" type="xs:string" use="required"/>
      </xs:complexType>
      <xs:complexType name="AnyType">
        <xs:sequence>
          <xs:choice maxOccurs="unbounded">
            <xs:element name="Match" type="mce:MatchType"/>
            <xs:element name="Any" type="mce:AnyType"/>
          </xs:choice>
        </xs:sequence>
        <xs:attribute name="minMatches" type="xs:nonNegativeInteger" default="1"/>
        <xs:attribute name="maxMatches" type="xs:nonNegativeInteger" use="optional"/>
      </xs:complexType>
      <xs:simpleType name="ProximityType">
        <xs:restriction base="xs:positiveInteger">
          <xs:minInclusive value="1"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:simpleType name="ProbabilityType">
        <xs:restriction base="xs:integer">
          <xs:minInclusive value="1"/>
          <xs:maxInclusive value="100"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:simpleType name="WorkloadType">
        <xs:restriction base="xs:string">
          <xs:enumeration value="Exchange"/>
          <xs:enumeration value="Outlook"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:complexType name="RegexType">
        <xs:simpleContent>
          <xs:extension base="xs:string">
            <xs:attribute name="id" type="xs:token" use="required"/>
          </xs:extension>
        </xs:simpleContent>
      </xs:complexType>
      <xs:complexType name="KeywordType">
        <xs:sequence>
          <xs:element name="Group" type="mce:GroupType" maxOccurs="unbounded"/>
        </xs:sequence>
        <xs:attribute name="id" type="xs:token" use="required"/>
      </xs:complexType>
      <xs:complexType name="GroupType">
        <xs:sequence>
          <xs:choice>
            <xs:element name="Term" type="mce:TermType" maxOccurs="unbounded"/>
          </xs:choice>
        </xs:sequence>
        <xs:attribute name="matchStyle" default="word">
          <xs:simpleType>
            <xs:restriction base="xs:NMTOKEN">
              <xs:enumeration value="word"/>
              <xs:enumeration value="string"/>
            </xs:restriction>
          </xs:simpleType>
        </xs:attribute>
      </xs:complexType>
      <xs:complexType name="TermType">
        <xs:simpleContent>
          <xs:extension base="mce:RestrictedTermType">
            <xs:attribute name="caseSensitive" type="xs:boolean" default="false"/>
          </xs:extension>
        </xs:simpleContent>
      </xs:complexType>
      <xs:complexType name="LocalizedStringsType">
        <xs:sequence>
          <xs:element name="Resource" type="mce:ResourceType" maxOccurs="unbounded">
            <xs:key name="UniqueLangCodeUsedInNamePerResource">
              <xs:selector xpath="mce:Name"/>
              <xs:field xpath="@langcode"/>
            </xs:key>
            <xs:key name="UniqueLangCodeUsedInDescriptionPerResource">
              <xs:selector xpath="mce:Description"/>
              <xs:field xpath="@langcode"/>
            </xs:key>
          </xs:element>
        </xs:sequence>
      </xs:complexType>
      <xs:complexType name="ResourceType">
        <xs:sequence>
          <xs:element name="Name" type="mce:ResourceNameType" maxOccurs="unbounded"/>
          <xs:element name="Description" type="mce:DescriptionType" minOccurs="0" maxOccurs="unbounded"/>
        </xs:sequence>
        <xs:attribute name="idRef" type="mce:GuidType" use="required"/>
      </xs:complexType>
      <xs:complexType name="ResourceNameType">
        <xs:simpleContent>
          <xs:extension base="xs:string">
            <xs:attribute name="default" type="xs:boolean" default="false"/>
            <xs:attribute name="langcode" type="mce:LangType" use="required"/>
          </xs:extension>
        </xs:simpleContent>
      </xs:complexType>
      <xs:complexType name="DescriptionType">
        <xs:simpleContent>
          <xs:extension base="xs:string">
            <xs:attribute name="default" type="xs:boolean" default="false"/>
            <xs:attribute name="langcode" type="mce:LangType" use="required"/>
          </xs:extension>
        </xs:simpleContent>
      </xs:complexType>
    </xs:schema>

## 相關資訊

[資料遺失防護](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[定義自己的 DLP 範本和資訊類型](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)

