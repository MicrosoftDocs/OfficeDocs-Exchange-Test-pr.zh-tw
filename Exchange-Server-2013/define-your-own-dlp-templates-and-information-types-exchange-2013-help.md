---
title: '定義自己的 DLP 範本和資訊類型: Exchange Online Help'
TOCTitle: 定義自己的 DLP 範本和資訊類型
ms:assetid: f4622dba-3347-4758-b4a2-f01b043c908c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ674310(v=EXCHG.150)
ms:contentKeyID: 50474594
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 定義自己的 DLP 範本和資訊類型

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2015-01-14_

您可以在 Microsoft Exchange Server 2013 外部開發防止資料遺失 (DLP) 原則範本做為 XML 檔案，然後使用 Exchange 系統管理中心或 Exchange 管理命令介面匯入這些檔案。本節說明撰寫及調整 DLP XML 檔案以用於 DLP 解決方案的程序和詳細資訊。您不需要自行開發 DLP XML 檔案，因為 Exchange 系統管理中心提供用於掃描郵件的現有 DLP 原則範本和傳輸規則，供您快速入門。

要尋找與 DLP 原則範本相關的管理工作嗎？請參閱[DLP 程序](dlp-procedures-exchange-2013-help.md) (Exchange Server 2013) 或[\[Exchange Online\] 的 DLP 程序](https://technet.microsoft.com/zh-tw/library/jj938003\(v=exchg.150\)) (Exchange Online)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Exchange 2013：DLP 是需要 Exchange 企業版用戶端存取授權 (CAL) 的高階功能。如需 CAL 和伺服器授權的詳細資訊，請參閱 <a href="https://go.microsoft.com/fwlink/p/?linkid=237292">Exchange Server 授權</a>。<br />
Exchange Online：DLP 是付費功能，需要 Exchange Online 計劃 2 授權。如需詳細資訊，請參閱 <a href="https://go.microsoft.com/fwlink/p/?linkid=286154">Exchange Online 授權</a>。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>本文不涵蓋推薦業務模式、檔案封裝的相關資訊或敏感資訊規則的部署方針，或討論如何散佈這些規則。此外，本文也不討論自訂開發規則的保護機制 (例如加密)，以及如何應用此類機制。</td>
</tr>
</tbody>
</table>


## 擴充資訊類型，以滿足您的需求

下列章節說明為了開始建立您自己的 XML 檔案 (以便匯入至 Exchange 2013 做為 DLP 原則，同時用於 DLP 原則範本和敏感資訊規則套件)，您所必須了解的概念和 XML 架構定義。

Microsoft Exchange 中的 DLP 可協助您將組織專屬原則套用至敏感資訊。讓 DLP 解決方案發揮效力的一個重要因素，是要能夠正確識別專屬於組織、法規要求、地理位置或其他業務層面的機密或敏感資訊。Microsoft 的產品內已提供原則範本和敏感資訊類型供您開始使用，但您獨特的業務需求仍需要自訂的防止資料遺失解決方案。因此，Microsoft 也提供方法，讓您可以建立和匯入您自己的 DLP 原則範本，或分類規則套件中建立和匯入您自己的敏感資訊定義。準確的 DLP 解決方案有賴於為敏感資訊偵測引擎設定正確的規則集，讓偵測引擎可以提供高度防護，同時將誤判和漏報率降至最低。

## 開發您自己的 DLP 原則範本

您可以撰寫您自己的 DLP 原則範本 XML 檔案並將其匯入。這個方法可以擴充 Exchange 提供的 DLP 解決方案，讓您建置密切符合您 DLP 需求的 DLP 原則。

管理自訂範本及其相關原則就類似於管理您根據 Microsoft 提供的範本所建立的 DLP 原則一樣。在一般 DLP 原則週期中，您會執行下列動作：

1.  建立您自己的 DLP 原則範本 (自訂的 XML 檔案)。若要深入了解，請參閱[開發 DLP 原則範本檔案](xml-rule-schema-and-rule-structure-guide-for-dlp-policy-files.md)。

2.  匯入您的自訂範本。若要深入了解，請參閱[從檔案匯入自訂的 DLP 原則範本](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)。

3.  根據自訂的範本建立 DLP 原則。若要深入了解，請參閱[從範本建立 DLP 原則](how-to-new-dlp-data-loss-prevention-policy-template.md)。

4.  重複步驟 1 和 2 來更新您的自訂範本。

5.  移除您的自訂範本。若要深入了解，請參閱[Remove-DlpPolicyTemplate](https://technet.microsoft.com/zh-tw/library/jj215739\(v=exchg.150\))。

如需 XML 架構定義和自行開發範本之相關概念的詳細資訊，請參閱[開發 DLP 原則範本檔案](xml-rule-schema-and-rule-structure-guide-for-dlp-policy-files.md)。

## 在分類規則套件中開發您自己的敏感資訊類型和比對邏輯

您可以在分類規則套件 (此為 XML 檔案) 中撰寫自己的敏感資訊定義，然後匯入做為 DLP 解決方案的一部分。敏感資訊偵測引擎能提供深入內容分析功能，可以識別信用卡號碼、身分證字號和公司智慧財產等敏感資訊。引擎由一組掃描和分析內容的可設定指示 (或規則) 控制，規則再組合成分類規則套件，這是一份遵循標準化規則套件 XML 架構定義的 XML 文件。以下說明如何開發您自己的範本。

1.  建立您自己的機密資訊類型 (自訂的 XML 檔案)。若要深入了解，請參閱[開發敏感資訊規則套件](technical-description-of-xml-schema-for-dlp-rule-packages.md)。

2.  匯入您的機密資訊類型。若要深入了解，請參閱[New-ClassificationRuleCollection](https://technet.microsoft.com/zh-tw/library/jj218619\(v=exchg.150\))。

3.  根據您的資訊類型建立自訂範本。若要深入了解，請參閱＜[開發敏感資訊規則套件](technical-description-of-xml-schema-for-dlp-rule-packages.md)＞

4.  重複步驟 1 和 2 來更新您的自訂範本。

5.  移除您的自訂範本。若要深入了解，請參閱＜[Remove-ClassificationRuleCollection](https://technet.microsoft.com/zh-tw/library/jj218670\(v=exchg.150\))＞

如需規則套件的詳細資訊，請參閱[比對方法和規則套件的技術](technical-description-of-xsd-rule-matching-for-dlp-rule-packages.md)和[開發敏感資訊規則套件](technical-description-of-xml-schema-for-dlp-rule-packages.md)。

## 瞭解規則套件中的規則類型

規則套件中的規則會設定定義明確之內容特徵的偵測程序，例如，尋找驅動程式授權號碼的規則。有兩種主要的規則類型可供使用：實體和親和性。

「實體」規則的目標為定義明確 (且通常是受監管) 的識別碼，如美國社會安全號碼。實體由一組可計數模式的集合來代表。模式以明確的主要比對識別碼，來定義比對集合。實體的一個例子是驅動程式的授權。

「相似性」規則的目標為特定的文件類型，如企業財務報表。相似性由一組獨立辨識項的集合來代表。辨識項是在特定近似值中所需配對的彙總。相似性的一個例子是美國沙賓法案 (U.S. Sarbanes-Oxley Act)。

## 相關資訊

[資料遺失防護](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[從檔案匯入自訂的 DLP 原則範本](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)

[New-ClassificationRuleCollection](https://technet.microsoft.com/zh-tw/library/jj218619\(v=exchg.150\))

[郵件流程或傳輸規則](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) Exchange Server 2013

[Exchange Online 中的郵件流程規則 (傳輸規則)](https://technet.microsoft.com/zh-tw/library/jj919238\(v=exchg.150\)) Exchange Online

[在 Exchange 中的敏感資訊類型外觀](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)

