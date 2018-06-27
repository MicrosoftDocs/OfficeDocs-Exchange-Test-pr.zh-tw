---
title: 'DLP 原則範本: Exchange Online Help'
TOCTitle: DLP 原則範本
ms:assetid: c7b1a8e4-30d9-4409-85c5-f85ae023737d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ657730(v=EXCHG.150)
ms:contentKeyID: 50474170
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# DLP 原則範本

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2015-01-14_

您可以使用的資料遺失防護 (DLP) 原則範本開始使用中 Microsoft Exchange 2013DLP 解決方案。DLP 原則範本是一種模式原則。您可以選取至開始建立您自己的自訂的 DLP 原則的程序的範本。在您的 DLP 原則，您可以自訂規則，以確保符合您的業務需求的資料外洩防護。由 Microsoft 所提供數個原則範本，但這些不是唯一的方式在Exchange中實作的資料遺失防護解決方案。

要尋找與 DLP 原則範本相關的管理工作嗎？請參閱 [DLP 程序](dlp-procedures-exchange-2013-help.md)。

**目錄**

Extend the templates and information types to meet your needs

Create your own new DLP policy template

Include DLP functionality with existing transport rules

Use DLP policies created by Microsoft

For more information

## 擴充範本和資訊類型，以符合您的需要

您可合併來自 Microsoft 合作夥伴或您自己開發之檔案的機密內容定義和原則範本，以做為 Exchange 2013 中所提供之 DLP 原則範本、資訊類型以及規則的延伸。此處會說明您可新增專用的唯一 DLP 內容以及擴充 DLP 功能的多種方式。Microsoft 已提供的範本是您開始使用 DLP 解決方案的便利方式。若要使用您專用的唯一 DLP 原則範本檔案來擴充 DLP 功能，您必須了解獨立於 Exchange 所建立之原則範本的 XML 架構需求。如欲瞭解更多與 DLP 原則範本關聯的管理命令介面指令程式請參閱[原則及符合性命令指令程式](https://technet.microsoft.com/zh-tw/library/dd298082\(v=exchg.150\))中與 `Get-DlpPolicyTemplate`相關的指令程式。此外，您可在了解合併的格式和程序之後，再定義專用的機密內容類型。如欲瞭解更多與 DLP 原則範本關聯的管理命令介面指令程式請參閱[原則及符合性命令指令程式](https://technet.microsoft.com/zh-tw/library/dd298082\(v=exchg.150\))中與 `Get-ClassificationRuleCollection`相關的指令程式。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在生產環境中執行 DLP 原則之前，您應該先在測試模式中開啟這些原則。在這類測試期間，建議您設定範例使用者信箱，然後傳送叫用測試原則的測試郵件，以便確認結果。</td>
</tr>
</tbody>
</table>


## 在分類規則套件中，建立您專用的新 DLP 原則範本或專用的機密資訊類型

您可獨立於 Exchange 並以符合 Microsoft 所提供的特定 XML 架構，來建立 DLP 原則範本檔案，然後將該檔案匯入您的系統，以用來建立 DLP 原則。藉由建立自己的範本檔案，您可定義 Microsoft 沒有提供但您專用的 DLP 原則模型。這和使用 Exchange 系統管理中心來建立的 DLP 原則不同，其通常是在原則範本可供使用之後才能進行此作業。若您是獨立於 Exchange 來建立原則範本，您就必須匯入原則範本，才能用來掃描郵件。您也可以建立不同於 Microsoft 在 Exchange 所定義的專用機密資訊定義。針對 DLP 原則範本檔案和分類規則套件，各有不同的 XML 架構定義。若要開始進行，請參閱下列資訊：

  -  
    [定義自己的 DLP 範本和資訊類型](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)

  -  
    [從檔案匯入自訂的 DLP 原則範本](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)

## 以現有傳輸規則來包含 DLP 功能

您可合併 DLP 偵測功能和傳統的傳輸規則，而不需建立新的 DLP 原則。若您已在舊版 Exchange 中建立了複雜規則組，且您想要將其複製到 Exchange 2013 或在其中新增機密資訊偵測，則可使用 Exchange 系統管理中心或 Exchange 管理命令介面中的傳輸規則編輯器，來合併這兩種功能。若要開始進行，請參閱下列資訊：

  -  
    [郵件流程或傳輸規則](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange Server 2013)

  -  
    [Exchange Online 中的郵件流程規則 (傳輸規則)](https://technet.microsoft.com/zh-tw/library/jj919238\(v=exchg.150\)) (Exchange Online)

  -  
    [管理郵件流程規則](manage-mail-flow-rules-exchange-2013-help.md)
    
    [原則及符合性命令指令程式](https://technet.microsoft.com/zh-tw/library/dd298082\(v=exchg.150\))

## 使用 Microsoft 所建立的 DLP 原則

Microsoft 提供了許多 DLP 原則。此為使用 DLP 解決方案的最簡易方法，既靈活又易於實作。您總是可以使用所提供的原則做為起點，然後再進一步自訂，使其符合您的需求。若要開始進行，請參閱下列資訊：

  - [Exchange 中提供的 DLP 原則範本](dlp-policy-templates-supplied-in-exchange-exchange-2013-help.md)

  - [從範本建立 DLP 原則](how-to-new-dlp-data-loss-prevention-policy-template.md)

## 相關資訊

[資料遺失防護](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

