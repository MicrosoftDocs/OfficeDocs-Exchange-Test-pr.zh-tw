---
title: '自訂內建的 DLP 敏感資訊類型: Exchange Online Help'
TOCTitle: 自訂內建的 DLP 敏感資訊類型
ms:assetid: 3f8bf141-2e7c-4ea7-b102-dfd6c41539da
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn781122(v=EXCHG.150)
ms:contentKeyID: 62757558
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 自訂內建的 DLP 敏感資訊類型

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2016-05-26_

尋找電子郵件中的機密資訊，必須以描述該資訊的項目已呼叫*規則*。資料外洩防護 (DLP) 包含最常見敏感資料類型您可以立即使用 51 規則的套件。若要使用這些規則，您必須併入一個原則。您可能會發現您想要調整以符合貴組織的特定需求，這些內建規則與您可以執行的動作來建立自訂的敏感資訊類型。本主題顯示如何將自訂 XML 檔案包含現有規則集合來偵測廣泛的潛在信用卡資訊。

您可以採取此範例並將其套用至其他內建的敏感資訊類型。如需預設敏感資訊類型和 XML 定義的清單，請參閱[在 Exchange 中的敏感資訊類型外觀](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)主題。

本主題將引導您完成 XML 規則自訂下列各節：

  - 匯出 XML 的目前的規則

  - 尋找您要修改在 XML 中的規則

  - 修改 XML 並建立新的敏感資訊類型

  - 需要較少額外的證據可

  - 尋找組織專屬的關鍵字

  - 上傳您的規則

若要了解不同的組件的規則，他們達成，請參閱字詞詞彙本主題的結尾。

## 匯出目前的規則 XML 檔案

若要匯出的 XML，您需要使用Exchange 管理命令介面或。Exchange Server 2013，請參閱[使用 PowerShell 與 Exchange 2013 (Exchange 管理命令介面)](https://technet.microsoft.com/zh-tw/library/bb123778\(v=exchg.150\))。Exchange Online，請參閱[使用遠端 PowerShell 連線到 Exchange Online](https://technet.microsoft.com/zh-tw/library/jj984289\(v=exchg.150\))。

1.  在Exchange 管理命令介面或Exchange Online PowerShell 中，輸入**Get-classificationrulecollection**在螢幕上顯示組織的規則。如果您尚未建立您自己，您僅會看見預設、 內建規則、 標示為 「 Microsoft 規則套件 」。

2.  儲存您的組織中的規則的輸入以變數**$ruleCollections = Get-classificationrulecollection**。將某個項目儲存於變數供輕鬆稍後的適用於遠端 PowerShell 命令格式。

3.  輸入來進行格式化的 XML 檔案與所有這些資料**Set-content-路徑 」 C:\\custompath\\exportedRules.xml"-Encoding Byte-值 $ruleCollections.SerializedClassificationRuleCollection**。（**Set-content**是檔中寫入之 XML 指令程式的一部分）。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>請確定您使用實際儲存規則套件的檔案位置。<strong>C:\custompath\</strong>是預留位置。</td>
    </tr>
    </tbody>
    </table>


## 尋找您要修改在 XML 規則

上述的 cmdlet 匯出整個*規則集合*，其中包含我們所提供的 51 預設規則。您需要特別針對您想要修改之信用卡號規則尋找下一步\]。

1.  使用文字編輯器來開啟您在前一節中匯出的 XML 檔案。

2.  捲動到**\<Rules\>**標記，這是包含 DLP 規則章節的開頭。（因為此 XML 檔案包含整個規則集合的資訊，其中包含您要取得規則捲動過去的頂端的其他資訊。）

3.  尋找**Func\_credit\_card**尋找信用卡號規則定義。（xml 規則名稱不得包含空格，因此通常具有底線取代空格和規則名稱有時候會縮寫。此範例是美國社會安全號碼規則，這是縮寫"SSN"。信用卡號規則 XML 應看來如下列程式碼範例。
    
        <Entity id="50842eb7-edc8-4019-85dd-5a5c1f2bb085"
               patternsProximity="300" recommendedConfidence="85">
              <Pattern confidenceLevel="85">
               <IdMatch idRef="Func_credit_card" />
                <Any minMatches="1">
                  <Match idRef="Keyword_cc_verification" />
                  <Match idRef="Keyword_cc_name" />
                  <Match idRef="Func_expiration_date" />
                </Any>
              </Pattern>
            </Entity>

既然您已在 XML 中找到信用卡號規則定義，您可以自訂以符合您需求的規則的 XML。（如重新整理程式在 XML 定義，請參閱本主題的結尾字詞字彙 （英文） ）。

## 修改 XML 並建立新的敏感資訊類型

首先，您必須建立新的敏感資訊類型，因為您無法直接修改預設規則。您可以使用自訂敏感資訊類型，也就述[開發敏感資訊規則套件](technical-description-of-xml-schema-for-dlp-rule-packages.md)這各種不同項目皆。此範例中，我們將保持簡單只移除佐證性證據和信用卡號規則新增關鍵字。

所有 XML 規則定義之內都建下列一般範本。您必須複製並貼信用卡號定義 XML 範本，修改某些 （請注意"...\\"版面配置區在下列範例） 的值，而然後將修改後的 XML 上傳新規則是可用於原則。

    <?xml version="1.0" encoding="utf-16"?>
    <RulePackage xmlns="http://schemas.microsoft.com/office/2011/mce">
      <RulePack id=". . .">
        <Version major="1" minor="0" build="0" revision="0" />
        <Publisher id=". . ." /> 
        <Details defaultLangCode=". . .">
          <LocalizedDetails langcode=" . . . ">
             <PublisherName>. . .</PublisherName>
             <Name>. . .</Name>
             <Description>. . .</Description>
          </LocalizedDetails>
        </Details>
      </RulePack>
      
     <Rules>
       <!-- Paste the Credit Card Number rule definition here.--> 
    
          <LocalizedStrings>
             <Resource idRef=". . .">
               <Name default="true" langcode=" . . . ">. . .</Name>
               <Description default="true" langcode=". . ."> . . .</Description>
             </Resource>
          </LocalizedStrings>
    
       </Rules>
    </RulePackage>

現在，您必須看起來類似下列 XML 程式碼所示的內容。因為其唯一 Guid 識別規則套件與規則，您需要產生兩個 Guid： 一個規則套件和應用程式，來取代信用卡號規則的 GUID。（如下列程式碼範例中的實體識別碼的 GUID 是您需要取代為一份新我們內建的規則定義，一種）。有數種方式來產生的 Guid，但是您可以進行輕鬆 PowerShell 輸入**\[guid\]::NewGuid()**。

    <?xml version="1.0" encoding="utf-16"?>
    <RulePackage xmlns="http://schemas.microsoft.com/office/2011/mce">
      <RulePack id="8aac8390-e99f-4487-8d16-7f0cdee8defc">
        <Version major="1" minor="0" build="0" revision="0" />
        <Publisher id="8d34806e-cd65-4178-ba0e-5d7d712e5b66" />
        <Details defaultLangCode="en">
          <LocalizedDetails langcode="en">
            <PublisherName>Contoso Ltd.</PublisherName>
            <Name>Financial Information</Name>
            <Description>Modified versions of the Microsoft rule package</Description>
          </LocalizedDetails>
        </Details>
      </RulePack>
      
     <Rules>
        <Entity id="db80b3da-0056-436e-b0ca-1f4cf7080d1f"
           patternsProximity="300" recommendedConfidence="85">
          <Pattern confidenceLevel="85">
            <IdMatch idRef="Func_credit_card" />
            <Any minMatches="1">
              <Match idRef="Keyword_cc_verification" />
              <Match idRef="Keyword_cc_name" />
              <Match idRef="Func_expiration_date" />
            </Any>
          </Pattern>
        </Entity>
    
          <LocalizedStrings>
             <Resource idRef="db80b3da-0056-436e-b0ca-1f4cf7080d1f"> 
    <!-- This is the GUID for the preceding Credit Card Number entity because the following text is for that Entity. -->
               <Name default="true" langcode="en-us">Modified Credit Card Number</Name>
               <Description default="true" langcode="en-us">Credit Card Number that looks for additional keywords, and another version of Credit Card Number that doesn't require keywords (but has a lower confidence level)</Description>
             </Resource>
          </LocalizedStrings>
    
       </Rules>
    </RulePackage>

## 佐證性證據需求移除機密資訊類型

現在您有新的敏感資訊類型，您就可以將上傳至Exchange環境下, 一步就是讓更具體的規則。修改規則，讓它只會尋找 16 位數數字會傳遞總和檢查碼但不需要其他 （佐證性） 證據 （例如關鍵字）。為達成此目的，您需要移除尋找佐證性證據的 xml 組件。佐證性證據是非常實用中降低誤判因為通常有特定關鍵字\] 或 \[到期日附近信用卡號。如果您移除該證據，應調整方式有信心您是您透過降低**confidenceLevel**，這在範例 85 找到信用卡號。

    <Entity id="db80b3da-0056-436e-b0ca-1f4cf7080d1f" patternsProximity="300"
          <Pattern confidenceLevel="85">
            <IdMatch idRef="Func_credit_card" />
          </Pattern>
        </Entity>

## 貴組織專屬的關鍵字的外觀

可能會想要需要佐證性證據但想要不同或其他關鍵字及也許您想要變更要尋找該證據。您可以調整**patternsProximity**即可展開或壓縮佐證性證據周圍 16 位數的視窗。若要新增您自己的關鍵字，您需要定義關鍵字清單並參照在您的規則。下列 XML 程式碼新增的關鍵字 「 公司卡 」 與 「 Contoso 卡片"使任何包含這些片語內之信用卡號 150 個字元的郵件會被識別為信用卡號。

    <Rules>
    <! -- Modify the patternsProximity to be "150" rather than "300." -->
        <Entity id="db80b3da-0056-436e-b0ca-1f4cf7080d1f" patternsProximity="150" recommendedConfidence="85">
          <Pattern confidenceLevel="85">
            <IdMatch idRef="Func_credit_card" />
            <Any minMatches="1">
              <Match idRef="Keyword_cc_verification" />
              <Match idRef="Keyword_cc_name" />
    <!-- Add the following XML, which references the keywords at the end of the XML sample. -->
              <Match idRef="My_Additional_Keywords" />
              <Match idRef="Func_expiration_date" />
            </Any>
          </Pattern>
        </Entity>
    <!-- Add the following XML, and update the information inside the <Term> tags with the keywords that you want to detect. -->
        <Keyword id="My_Additional_Keywords">
          <Group matchStyle="word">
            <Term caseSensitive="false">company card</Term>
            <Term caseSensitive="false">Contoso card</Term>
          </Group>
        </Keyword>

## 上傳您的規則

若要上傳您的規則，您需要執行下列動作。

1.  將其儲存為.xml 檔案使用 Unicode 編碼方式。這是重要的因為此規則將無法運作如果以不同的編碼方式儲存檔案。

2.  連線至Exchange 管理命令介面或Exchange Online PowerShell。Exchange Server 2013，請參閱[使用 PowerShell 與 Exchange 2013 (Exchange 管理命令介面)](https://technet.microsoft.com/zh-tw/library/bb123778\(v=exchg.150\))。Exchange Online，請參閱[使用遠端 PowerShell 連線到 Exchange Online](https://technet.microsoft.com/zh-tw/library/jj984289\(v=exchg.150\))。

3.  在Exchange 管理命令介面或Exchange Online PowerShell 中，輸入**New-classificationrulecollection FileData (Get-content-路徑"C:\\custompath\\MyNewRulePack.xml"-Encoding Byte)**。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>請確定您使用實際儲存規則套件的檔案位置。<strong>C:\custompath\</strong>是預留位置。</td>
    </tr>
    </tbody>
    </table>


4.  若要確認，請輸入**Y**，並按下**Enter**。

5.  確認您的新規則已上傳輸入**Get-dataclassification**、 現在會顯示您規則的名稱。

若要開始使用新的規則來偵測敏感資訊，您需要新增至 DLP 原則的規則。若要了解如何將規則新增至原則，請參閱[管理 DLP 原則](manage-dlp-policies-exchange-2013-help.md)。

## 字詞庫字彙 （英文）

這些是定義字詞您遇到此程序期間。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>術語</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Entity</p></td>
<td><p>實體是我們呼叫敏感資訊的類型，例如信用卡號。每個實體具有唯一 GUID 為它的識別碼。如果您以 XML 複製 GUID 並為其搜尋，您會發現 XML 規則定義及該 XML 規則的所有當地語系化的翻譯。您也可以找到此定義該 GUID 然後搜尋並找出轉譯的 GUID。</p></td>
</tr>
<tr class="even">
<td><p>函數</p></td>
<td><p>XML 檔案會參照<strong>Func_credit_card</strong>，這是一個函數編譯程式碼中。函數可用來執行複雜的 regex 並確認總和檢查碼符合我們內建的規則。）因為發生在程式碼中，變數的一些未出現在 XML 檔案。</p></td>
</tr>
<tr class="odd">
<td><p>IdMatch</p></td>
<td><p>這會是嘗試符合模式的識別碼-例如信用卡號。您可以閱讀更多有關此了解及<a href="technical-description-of-xml-schema-for-dlp-rule-packages.md">實體規則</a>中的<strong>Match</strong>標記。</p></td>
</tr>
<tr class="even">
<td><p>關鍵字清單</p></td>
<td><p>XML 檔案也會參照<strong>keyword_cc_verification</strong>與<strong>keyword_cc_name</strong>，亦即的關鍵字從中我們要尋找的相符項目內<strong>patternsProximity</strong>實體清單。這些目前未出現在 XML。</p></td>
</tr>
<tr class="odd">
<td><p>模式</p></td>
<td><p>圖樣包含機密類型尋找的項目清單。這包含關鍵字、 regex，以及 （執行之工作類似確認總和檢查碼） 的內部功能。敏感資訊類型可以有多個具有唯一 confidences 模式。建立如果找到少或沒有佐證性證據傳回高度信賴如果找到佐證性證據與較低信賴的敏感資訊類型時，這很有用。</p></td>
</tr>
<tr class="even">
<td><p>圖樣 confidenceLevel</p></td>
<td><p>這是信賴 DLP 引擎找到相符項目層級。此層級的信賴與相關聯的模式比對如果符合模式的需求。這會是您應該考慮使用 Exchange 傳輸規則時 (ETRs) 信賴量值。</p></td>
</tr>
<tr class="odd">
<td><p>patternsProximity</p></td>
<td><p>當我們尋找是什麼樣子信用卡號碼模式時、 <strong>patternsProximity</strong>是圍繞該號碼鄰近我們將看起來如佐證性證據。</p></td>
</tr>
<tr class="even">
<td><p>recommendedConfidence</p></td>
<td><p>這是建議您為此規則的信賴等級。建議的信賴適用於實體和相似性。為實體，此數字就會永遠不會對圖樣<strong>confidenceLevel</strong>評估。它是純粹可協助您選擇的信賴等級如果您想要套用一個建議。相似性、 圖樣<strong>confidenceLevel</strong>必須高於 ETR 巨集指令來叫用的<strong>recommendedConfidence</strong>編號。<strong>recommendedConfidence</strong>為預設信賴等級用於 ETRs 建立巨集指令會叫用。如果您希望您可以手動變更要叫用 ETR 改為基礎的圖樣信賴等級、 關閉。</p></td>
</tr>
</tbody>
</table>


## 相關資訊

  - [DLP 規則如何套用至評估郵件](how-dlp-rules-are-applied-to-evaluate-messages-exchange-2013-help.md)

  - [建立自訂的 DLP 原則](create-a-custom-dlp-policy-exchange-2013-help.md)

  - [在 Exchange 中的敏感資訊類型外觀](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)

