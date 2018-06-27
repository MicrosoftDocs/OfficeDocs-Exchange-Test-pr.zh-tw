---
title: '傳輸規則的新功能: Exchange 2013 Help'
TOCTitle: 傳輸規則的新功能
ms:assetid: 0c2fc0b5-3cd2-4d79-aa2b-0c7622ae15a8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ150483(v=EXCHG.150)
ms:contentKeyID: 50472551
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 傳輸規則的新功能

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2014-10-03_

在 Microsoft Exchange Server 2013中，傳輸規則新增了數種改善功能。此主題提供部分主要變更與加強功能的簡述概覽。若要深入了解傳輸規則的相關資訊，請參閱[郵件流程或傳輸規則](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)。

## 支援資料外洩防護原則

Exchange 2013 中的資料外洩防護 (DLP) 功能可協助組織減少敏感資料的意外洩漏情況。傳輸規則已更新，用以協助建立可伴隨並加強 DLP 原則的規則。若要了解更多關於傳輸規則中支援的 DLP，請參閱下列主題：

[與傳輸規則整合敏感資訊規則](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md)

[資料遺失防護](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

## 新的述詞和動作

傳輸規則的功能將透過新述詞和動作的加入獲得延伸。列於下方的每個述詞皆將於建立傳輸規則時做為條件或例外使用。

若欲了解關於使用這些新述詞與動作的詳細資訊，請參閱 [傳輸規則條件 （述詞）](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md) 與 [傳輸規則動作](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md)。

## 新述詞

  -  
    **AttachmentExtensionMatchesWords** 用於偵測包含特定副檔名附件的郵件訊息。

  -  
    **AttachmentHasExecutableContent**   用於偵測包含可執行檔附件的郵件訊息。

  -  
    **HasSenderOverride** 用於偵測寄件人選擇覆寫 DLP 原則限制的郵件訊息。

  -  
    **MessageContainsDataClassifications**   用於偵測郵件內文與任何附件中的敏感資訊。如需可用的資料分類清單，請參閱[在 Exchange 中的敏感資訊類型外觀](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)。

  -  
    **MessageSizeOver**   用於偵測整體容量大於或等於指定上限的郵件訊息。

  -  
    **SenderIPRanges**   用於偵測特定 IP 位址範圍中傳送的郵件訊息。

## 新動作

  -  
    **GenerateIncidentReport**   產生傳送至指定 SMTP 地址的附隨報告。動作同時含有稱為 *IncidentReportOriginalMail* 的參數，可接受兩個值之一：IncludeOriginalMail 或 DoNotIncludeOriginalMail。

  -  
    **NotifySender**   控制如何通知違反 DLP 原則的郵件寄件者。可選擇僅通知寄件者並以正常方式路由傳送郵件，或者可選擇拒絕郵件並通知寄件者。

  -  
    **StopRuleProcessing**   停止處理郵件上的所有後續規則。

  -  
    **ReportSeverityLevel**   設定附隨報告中指定的嚴重性。此動作的值為：\[參考\]、\[低\]、\[中等\]、\[高\] 以及 \[關閉\]。

  -  
    **RouteMessageOutboundRequireTLS**   在組織外路由傳送此郵件時需要傳輸層安全性 (TLS) 加密。若不支援 TLS 加密，郵件將被拒絕且不會傳送。

## 傳輸規則中的其他變更

  - **支援擴充規則運算式語法**   Exchange 2013 中的傳輸規則是根據 Microsoft.NET Framework 規則運算式 (regex) 功能發展，現在則支援擴充規則運算式語法。

  - **傳輸規則代理程式叫用**   Exchange 2013 中傳輸規則的主要架構變更為傳輸規則代理程式改於 onResolvedMessage 上叫用。在舊版本的 Exchange 中，規則代理程式是在 onRoutedMessage 上叫用。此變更將允許使用者新增新動作，例如需要 TLS 來變更訊息的路由傳送方式。若要深入了解 Exchange 2013 中的傳輸規則架構，請參閱[郵件流程或傳輸規則](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)。

  - **郵件追蹤記錄中的詳細傳輸規則資訊**   關於傳輸規則的詳細資訊現已包含於郵件追蹤記錄中。該資訊包含規則將因哪些特定郵件觸發，以及處理該規則後採取的動作。

  - **新規則監控功能**   Exchange 2013 將監控設定的傳輸規則，並計算在建立規則與一般操作中執行這些規則的成本。Exchange 可偵測並產生造成郵件傳送延遲的規則警示。

