---
title: '系統管理員的傳遞回報: Exchange 2013 Help'
TOCTitle: 系統管理員的傳遞回報
ms:assetid: d98623d3-e0b7-4cb9-93fb-6351b4a06137
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ919241(v=EXCHG.150)
ms:contentKeyID: 51409246
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 系統管理員的傳遞回報

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

您可以使用系統管理員的傳遞回報、 追蹤所傳送或接收來自組織中任何特定信箱的郵件的傳遞資訊。尤其是系統管理員的傳遞回報使用 Exchange 系統管理中心 (EAC) 來執行郵件追蹤記錄檔的目標的搜尋。搜尋一律受限於特定信箱。您可以搜尋的信箱，或信箱傳送郵件及您可篩選搜尋結果的郵件主旨。

郵件內文的內容不傳回在傳遞報告中，但是會顯示在結果中的主旨行。如果您想要搜尋之信箱的郵件內容為基礎的特定電子郵件組織中，查看[就地 eDiscovery](in-place-ediscovery-exchange-2013-help.md)。

下面列舉一些您可能會覺得傳遞回報搜尋很有用的情況：

  - 管理員會提供不良檢閱以實習生因為實習生未開啟對時間工作分派。實習生堅持他具有附加的工作分派傳送一則訊息。管理員會要求您確認郵件的狀態。

  - 安全性公告已傳送給要求他們回覆立即，但無人已回覆的使用者。會忽略郵件或沒有他們只是不會收到它吗？

  - 使用者抱怨無人會接收其訊息。他們檢查其郵件的傳遞狀態，但不能算出項目將要。這可能是因為規則會套用到組織層級的郵件。

所產生的傳遞回報建立傳遞報告搜尋之後，會顯示下列資訊： 郵件已傳送 from 和 to 主旨行並傳送郵件。傳遞報告也會顯示訊息的傳遞狀態並傳遞為何可能延遲或失敗的原因。

## 其他有關傳遞回報的資訊

  - 以下是如何建立新的傳遞回報： [使用傳遞回報追蹤郵件](track-messages-with-delivery-reports-exchange-2013-help.md)。

  - 在內部部署 Exchange 組織可以使用 Exchange 管理命令介面來查詢郵件直接追蹤記錄檔。如需詳細資訊，請參閱[搜尋郵件追蹤記錄檔](search-message-tracking-logs-exchange-2013-help.md)。

  - 使用者可以追蹤自己的郵件。如需詳細資訊，請參閱 ＜[使用者的傳遞回報](https://go.microsoft.com/fwlink/?linkid=279920)。

  - 如果您的組織中包含舊版的 Exchange，則需要注意 Exchange 2013 中的傳遞回報功能如何在各 Exchange 版本間運作。
    
      - Exchange 2013 傳遞回報可以跨相同 Active Directory 站台中的 Exchange 2010 伺服器來追蹤郵件。
    
      - Exchange 2013傳遞報告無法在同一個 Active Directory 站台的Exchange 2007伺服器間追蹤郵件。傳遞報告功能使用遠端程序呼叫並不存在於Exchange 2007中的 web 服務介面。

