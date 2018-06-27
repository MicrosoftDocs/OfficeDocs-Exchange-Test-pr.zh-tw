---
title: '與傳輸規則整合敏感資訊規則: Exchange Online Help'
TOCTitle: 與傳輸規則整合敏感資訊規則
ms:assetid: feb014a7-89dd-4f2d-a06d-52806ce435d4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ150583(v=EXCHG.150)
ms:contentKeyID: 50472436
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 與傳輸規則整合敏感資訊規則

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2015-01-14_

在 Microsoft Exchange，您可以建立的包含規則不只使用傳統郵件分類的和現有傳輸規則，但也結合這些訊息內找到的敏感資訊的規則與 DLP 原則。現有的傳輸規則架構提供豐富的功能定義訊息原則、 涵蓋整個兩端的柔硬碟的控制項。範例包括：

  - 限制的收件者和寄件者，包括組織內的部門群組之間的互動之間的互動。

  - 套用內的組織和外部通訊的個別原則。

  - 防止不適當內容進入或離開組織。

  - 篩選機密資訊。

  - 追蹤或封存已傳送至個人或從特定個人接收的郵件。

  - 重新導向輸入及輸出郵件的傳遞之前進行檢查。

  - 郵件套用免責聲明至通過時組織。

傳輸規則可將郵件原則套用到電子郵件訊息傳輸管線的流程 Mailbox server 及 Edge Transport server 上的傳輸服務中。這些規則讓系統管理員將強制執行郵件原則、 協助保護郵件越安全，協助保護郵件系統，並避免意外資訊遺失。如需傳輸規則的詳細資訊，請參閱[郵件流程或傳輸規則](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) ( Exchange Server 2013) 或[Exchange Online 中的郵件流程規則 (傳輸規則)](https://technet.microsoft.com/zh-tw/library/jj919238\(v=exchg.150\)) (Exchange Online)。

## 傳輸規則架構中的敏感資訊規則

敏感資訊規則的條件，您可以自訂簡介整合與傳輸規則 framework： 如果郵件包含**...\]敏感資訊**。此條件可設定與訊息內所包含的一或多個敏感資訊類型。當多個 DLP 原則或原則內的規則來設定這個條件時、 原則或規則是會滿足任何條件符合時。 Exchange原則規則檢查主旨、 內文和任何附件的郵件。如果規則比對任何這些訊息元件，就會套用規則動作。

敏感資訊條件可能會與任何現有傳輸規則來定義郵件原則結合。如果合併、 條件搭配其他規則，並提供與語意。例如，兩個不同的情況新增 AND 陳述式搭配如此兩者必須符合要套用的巨集指令。傳輸規則動作的任何可設定經過包含敏感資訊類型相符的規則。可以由傳輸規則代理程式，則會掃描郵件以強制執行傳輸規則掃描許多不同的檔案類型。若要深入了解支援的檔案類型，請參閱[使用傳輸規則檢查郵件附件](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md) (Exchange Server 2013) 或[使用檢查 Office 365 中的郵件附件的郵件流程規則](https://technet.microsoft.com/zh-tw/library/jj919236\(v=exchg.150\)) (Exchange Online)。

規則也可用於規則定義的例外狀況部分。其做為內之規則條件的例外狀況定義其使用無關。這可定義為部分的條件和條件中的也受限於較資訊類型指定要套用的多個資訊類型的條件規則的彈性。這可讓原則例如比對特定的傳統郵件分類規則，但不是符合其他敏感資訊類型之前執行您定義原則內的動作。

## 相關資訊

[資料遺失防護](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[在 Exchange 中的敏感資訊類型外觀](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)

[郵件流程或傳輸規則](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) Exchange Server 2013

[Exchange Online 中的郵件流程規則 (傳輸規則)](https://technet.microsoft.com/zh-tw/library/jj919238\(v=exchg.150\)) Exchange Online

[建立自訂的 DLP 原則](create-a-custom-dlp-policy-exchange-2013-help.md)

