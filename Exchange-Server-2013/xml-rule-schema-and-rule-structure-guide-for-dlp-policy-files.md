---
title: '開發 DLP 原則範本檔案: Exchange Online Help'
TOCTitle: 開發 DLP 原則範本檔案
ms:assetid: 4b263547-aef4-4ee8-aa4f-fa64a5863189
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ674703(v=EXCHG.150)
ms:contentKeyID: 50473187
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 開發 DLP 原則範本檔案

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

此概觀說明資料遺失防護 (DLP) 原則範本檔案之 XML 架構定義的元件，並提供 XML 格式的範例原則檔案。此將有助於在開始之前，了解整個 DLP 架構以及規則發展程序。如需詳細資訊，請參閱[資料遺失防護](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)及[定義自己的 DLP 範本和資訊類型](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)。

為了使資料遺失防護解決方案更容易採用與管理，Microsoft Exchange Server 2013 會推出稱為 DLP 原則的概念模型與原則範本。DLP 原則範本為您預期的 DLP 員則提供一個初步設計。為了提高價值，DLP 原則範本必須概括所有必要的指示詞與資料物件，以符合特定的原則目標，如法規或商業需求。此範本不是一種特定環境。它只是一個定義或原則模型，可提供作為產品組態的一部分，或由獨立軟體廠商和協力廠商提供。DLP 原則對另一方面而言，是專用於部署環境之範本的執行時間實例化。現有的訊息原則架構可透過使用傳輸規則結合 DLP 原則。傳輸規則提供了相當大的彈性，適應並表現 DLP 解決方案的豐富性。

## 原則範本來源與架構

DLP 原則範本通常會受到多個來源的影響，例如以伺服器為基礎的處理指示詞、用戶端電腦原則，或其他如下圖所示的原則建構：

![影響原則範本的因素](images/JJ674703.12f48e4f-d7b8-4ddd-87e8-8477983252ec(EXCHG.150).gif "影響原則範本的因素")

DLP 原則範本透過 Exchange 管理命令介面與以網際網路為基礎的介面 (例如 Exchange Administration Center) 提供簡單的管理作業，其包含匯入、匯出、委派，以及查詢功能。DLP 原則藉由參照作為建立程序一部分的 DLP 原則範本而建立。這些參照的 DLP 原則範本可能是安裝在系統中的參照，其儲存在 Active Directory 網域服務中，或是直接從外部提供的原則提供為輸入。

DLP 原則範本會以 XML 文件呈現。單一 XML 架構會用於 Exchange 中提供的原則，外部也是如此。XML 文件的概念架構會在下表呈現，其顯示主要元素。這套原則元件定義有助於達成特定的原則目標，如法規或商業需求。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>結構化元素</th>
<th>意義與範例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>發行者</p></td>
<td><p>Microsoft 或協力廠商</p></td>
</tr>
<tr class="even">
<td><p>版本</p></td>
<td><p>15.0.1.0</p></td>
</tr>
<tr class="odd">
<td><p>原則名稱</p></td>
<td><p>PCI-DSS</p></td>
</tr>
<tr class="even">
<td><p>描述</p></td>
<td><p>PCI-DSS DLP 原則可協助您偵測其目前狀態受限於 PCI 資料安全標準 (PCI DSS) 的資訊包括信用卡或轉帳卡數字的資訊。使用此原則無法確保與任何法規符合性。在測試完成後，變更必要設定 Exchange 中的資訊傳輸符合貴組織的原則與因此。範例包括使用已知的業務合作夥伴設定 TLS 或新增更嚴格的傳輸規則動作，例如新增權限保護到包含這種資料類型的郵件。</p></td>
</tr>
<tr class="odd">
<td><p>中繼資料</p></td>
<td><p>描述當地法規、國家或地區、關鍵字等等的標籤。</p></td>
</tr>
<tr class="even">
<td><p>原則建構集合</p></td>
<td><ol>
<li><p>傳輸規則定義，如條件與動作。</p></li>
<li><p>透過互動式通知控制用戶端體驗的電子郵件用戶端行為定義。</p></li>
<li><p>組態會選擇性地參照需要配合用戶端特定環境的設定。</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>資料分類集合</p></td>
<td><ol>
<li><p>指定分類實體或相似性。</p></li>
<li><p>實體有計數與信賴等級；相似性只有信賴等級。</p></li>
<li><p>隨附其自己的一套屬性與分類架構。</p></li>
</ol></td>
</tr>
</tbody>
</table>


## 原則範本格式定義

原則範本是以遵循以下架構的 XML 文件呈現。請注意，XML 區分大小寫。例如，`dlpPolicyTemplates` 將會運作，但是 `DlpPolicyTemplates` 將不會運作。

    <?xml version="1.0" encoding="UTF-8"?>
    <dlpPolicyTemplates>
      <dlpPolicyTemplate id="F7C29AEC-A52D-4502-9670-141424A83FAB" mode="Audit" state="Enabled" version="15.0.2.0">
        <contentVersion>4</contentVersion>
        <publisherName>Microsoft</publisherName>
        <name>
          <localizedString lang="en">PCI-DSS</localizedString>
        </name>
        <description>
          <localizedString lang="en">Detects the presence of information subject to Payment Card Industry Data Security Standard (PCI-DSS) compliance requirements.</localizedString>
        </description>
        <keywords></keywords>
        <ruleParameters></ruleParameters>
        <ruleParameters/>
        <policyCommands>
          <!-- The contents below are applied/executed as rules directly in PS - -->
          <commandBlock>
            <![CDATA[ new-transportRule "PCI-DSS: Monitor Payment Card Information Sent To Outside" -DlpPolicy "%%DlpPolicyName%%" -SentToScope NotInOrganization -SetAuditSeverity High -MessageContainsDataClassifications @{Name="Credit Card Number"; MinCount="1" } -Comments "Monitors payment card information sent to outside the organization as part of the PCI-DSS DLP Policy."]]>
          </commandBlock>
          <commandBlock>
            <![CDATA[ new-transportRule "PCI-DSS: Monitor Payment Card Information Sent To Within" -DlpPolicy "%%DlpPolicyName%%" -Comments "Monitors payment card information sent inside the organization as part of the PCI-DSS DLP Policy." -SentToScope InOrganization -SetAuditSeverity Low -MessageContainsDataClassifications @{Name="Credit Card Number"; MinCount="1" } ]]>
          </commandBlock>
        </policyCommands>
        <policyCommandsResources></policyCommandsResources>
      </dlpPolicyTemplate>
    </dlpPolicyTemplates>

如果您針對任何元素加入 XML 檔案中的參數含有空格，必須以雙引號包覆該參數，否則會無法正常運作。在以下範例中，`-SentToScope` 之後的參數是可接受的；因為它是不含空格的連續字元字串，因此沒有雙引號。然而，提供給 –`Comments` 的參數將不會出現在 Exchange 系統管理中心內，因為它含有空格但未以雙引號包覆。

    <CommandBlock><![CDATA[ new-transportRule "PCI-DSS: Monitor Payment Card Information Sent To Within" -DlpPolicy "PCI-DSS" -Comments Monitors payment card information sent inside the organization -SentToScope InOrganization -SetAuditSeverity Low -MessageContainsDataClassifications @{Name="Credit Card Number"; MinCount="1" } ]]> </CommandBlock>

## localizedString 元素

此範本格式提供當地語系化可能會呈現給使用者之範本中字串的功能，例如，選擇要安裝哪一個 DLP 原則範本。localizedString 元素可用於為「名稱」與「描述」欄位提供多個定義。

## ruleParameters 節點

這是選用的參數集合，需要在建立 DLP 原則以對應至部署指定物件時的範本實例化階段期間提供。例如，部署中可用的實際通訊群組。

## dlpPolicyTemplate 元素

這是 DLP 原則範本的根元素，而且每一個範本皆需要該元素。下表提供可用屬性：


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>屬性名稱</th>
<th>是否必要？</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>是</p></td>
<td><p>DLP 原則範本文件中使用的版本號碼。</p></td>
</tr>
<tr class="even">
<td><p>狀態</p></td>
<td><p>否</p></td>
<td><p>原則狀態的選用預設組態。</p></td>
</tr>
<tr class="odd">
<td><p>模式</p></td>
<td><p>否</p></td>
<td><p>原則模式的選用預設組態。</p></td>
</tr>
<tr class="even">
<td><p>ID</p></td>
<td><p>否</p></td>
<td><p>GUID 可以下列格式唯一識別此 DLP 原則範本定義：&quot;A29C69BF-4F98-47F1-9A99-5771DFD2C27F&quot;。</p></td>
</tr>
</tbody>
</table>


子項目包含以下元素順序：


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>子元素</th>
<th>(最小，最大)</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PublisherName</p></td>
<td><p>(1, 1)</p></td>
<td><p>範本發行者的中繼資料</p></td>
</tr>
<tr class="even">
<td><p>名稱</p></td>
<td><p>(1, 1)</p></td>
<td><p>此範本的可當地語系化名稱。</p></td>
</tr>
<tr class="odd">
<td><p>描述</p></td>
<td><p>(1, 1)</p></td>
<td><p>此範本的可當地語系化說明。</p></td>
</tr>
<tr class="even">
<td><p>關鍵字</p></td>
<td><p>(1, 1)</p></td>
<td><p>適用於此範本的關鍵字清單。範本可能會有一個空的關鍵字清單。</p></td>
</tr>
<tr class="odd">
<td><p>RuleParameters</p></td>
<td><p>(0, 1)</p></td>
<td><p>原則定義中使用的範本參數清單。</p></td>
</tr>
<tr class="even">
<td><p>原則命令</p></td>
<td><p>(0, 1)</p></td>
<td><p>適用於此原則的傳輸規則定義的清單。這是選用的元素。</p></td>
</tr>
</tbody>
</table>


## DLP 原則範本：原則命令

此部分的原則範本包含用來實例化原則定義之 Exchange 管理命令介面命令的清單。匯入程序將執行每一個命令作為實例化程序的一部分。這裡提供原則命令範例。

    <PolicyCommands>
        <!-- The contents below are applied/executed as rules directly in PS - -->
          <CommandBlock> <![CDATA[ new-transportRule "PCI-DSS: Monitor Payment Card Information Sent To Outside" -DlpPolicy "PCI-DSS" -SentToScope NotInOrganization -SetAuditSeverity High -MessageContainsDataClassifications @{Name="Credit Card Number"; MinCount="1" } -Comments "Monitors payment card information sent to outside the organization as part of the PCI-DSS DLP policy."]]></CommandBlock>
          <CommandBlock><![CDATA[ new-transportRule "PCI-DSS: Monitor Payment Card Information Sent To Within" -DlpPolicy "PCI-DSS" -Comments "Monitors payment card information sent inside the organization as part of the PCI-DSS DLP policy." -SentToScope InOrganization -SetAuditSeverity Low -MessageContainsDataClassifications @{Name="Credit Card Number"; MinCount="1" } ]]> </CommandBlock>
      </PolicyCommands> 

指令程式的格式是指令程式使用的標準 Exchange 管理命令介面指令程式語法。命令會依序執行。每一個命令節點可能包含結合多個命令的指令碼區塊。以下範例說明如何內嵌分類規則套件在 DLP 原則範本中，以及安裝規則套件作為原則建立程序的一部分。分類規則套件內嵌至原則範本中，然後以參數傳遞至範本中的指令程式：

``` 
<CommandBlock>
  <![CDATA[
$rulePack = [system.Text.Encoding]::Unicode.GetBytes('<?xml version="1.0" encoding="utf-16"?>
<rulePackage xmlns="http://schemas.microsoft.com/office/2011/mce">

  <RulePack id="c3f021a3-c265-4dc2-b3a7-41a1800bf518">
    <Version major="1" minor="0" build="0" revision="0"/>
    <Publisher id="e17451d3-9648-4117-a0b1-493a6d5c73ad"/>
    <Details defaultLangCode="en-us">
      <LocalizedDetails langcode="en-us">
        <PublisherName>Contoso</PublisherName>
        <Name>Contoso Sample Rule Pack</Name>
        <Description>This is a sample rule package</Description>
      </LocalizedDetails>
    </Details>
  </RulePack>

  <Rules>
    <Entity id="7cc35258-6b35-4415-baff-a76d1a018980" patternsProximity="300" recommendedConfidence="85" workload="Exchange">     

      <Pattern confidenceLevel="85">
        <IdMatch idRef="Regex_Contoso" />
        <Any minMatches="1">
          <Match idRef="Regex_conf" />
        </Any>
      </Pattern>
    </Entity>

    <Regex id="Regex_Contoso">(?i)(\bContoso\b)</Regex>
    <Regex id="Regex_conf">(?i)(\bConfidential\b)</Regex>

    <LocalizedStrings>
      <Resource idRef="7cc35258-6b35-4415-baff-a76d1a018980">
        <Name default="true" langcode="en-us">
          Confidential Information Rule
        </Name>
        <Description default="true" langcode="en-us">
          Sample rule pack - Detects Contoso confidential information
        </Description>
      </Resource>
    </LocalizedStrings>
  </Rules>

</RulePackage>

')


New-ClassificationRuleCollection -FileData $rulePack 
New-TransportRule -name "customEntity" -DlpPolicy "%%DlpPolicyName%%" -SentToScope NotInOrganization -MessageContainsDataClassifications @{Name="Confidential Information Rule"} -SetAuditSeverity High]]>
</CommandBlock> 
```

子元素包含以下依序排列的元素。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>子元素</th>
<th>(最小，最大)</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CommandBlock</p></td>
<td><p>(1，n)</p></td>
<td><p>在 PowerShell 中執行的命令區塊。依序執行的命令區塊。</p></td>
</tr>
</tbody>
</table>


## 相關資訊

[資料遺失防護](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[定義自己的 DLP 範本和資訊類型](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)

[從檔案匯入自訂的 DLP 原則範本](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)

