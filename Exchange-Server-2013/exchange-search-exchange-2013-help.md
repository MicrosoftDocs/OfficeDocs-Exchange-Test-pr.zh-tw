---
title: 'Exchange 搜尋: Exchange 2013 Help'
TOCTitle: Exchange 搜尋
ms:assetid: 967e2a13-4e54-486a-ac22-08768674abbb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb232132(v=EXCHG.150)
ms:contentKeyID: 52062577
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 搜尋

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-09-17_

隨著信箱大小和以郵件與附件形式儲存在信箱中的資料量逐漸增加，能夠迅速搜尋和找到需要的郵件，對於使用者而言相當重要。[就地封存 in Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md) 可將舊的和不常存取的項目移至封存，讓您不必再使用 .pst 檔案。如此可讓使用者儲存更多信箱資料，而在使用者的主要和封存信箱中搜尋也能成為重要的產能工具。[就地 eDiscovery](in-place-ediscovery-exchange-2013-help.md) 能讓授權使用者同時搜尋內部部署和雲端式 Exchange 組織中的信箱內容，符合電子化探索 (eDiscovery) 要求、法規稽核或內部調查。就地 eDiscovery 也使用 Exchange 搜尋所建立的內容索引。

Exchange 搜尋與 Exchange Server 2003 提供的全文檢索不同。它在效能、內容索引和搜尋方面都有所改善。新項目會在傳輸管線中建立索引或幾乎在建立或傳遞至信箱之後立即建立索引，以便提供使用者迅速、穩定且更可靠的方式來搜尋信箱資料。內容索引預設為啟用，不需要進行任何初次設定或組態。

如需Exchange搜尋的詳細資訊，請參閱：

  - [依 Exchange 搜尋編製索引的檔案格式](file-formats-indexed-by-exchange-search-exchange-2013-help.md)

  - [依 Exchange 搜尋編製索引編製郵件內容](message-properties-indexed-by-exchange-search-exchange-2013-help.md)

要尋找與 Exchange 搜尋相關的管理工作嗎？請參閱[Exchange 搜尋程序](exchange-search-procedures-exchange-2013-help.md)。

## 新功能

Exchange 2013 對 Exchange 搜尋引入下列變更：

  - 基礎內容索引引擎已更換為 Microsoft Search Foundation，可以提供效能和功能改進，並作為 Exchange 和 SharePoint 的通用基礎內容索引引擎。但管理介面沒有改變。

  - Search Foundation 預設會處理電子郵件附件中最常見的檔案格式。您不再需要安裝 Microsoft Office Filter Packs for Exchange Search。如需 Exchange 搜尋處理的檔案格式清單，請參閱 [依 Exchange 搜尋編製索引的檔案格式](file-formats-indexed-by-exchange-search-exchange-2013-help.md)。
    
    您可以安裝 Ifilter，如同舊版的Exchange新增其他檔案格式的支援。

  - 內容索引現在的效率更高，因為它可處理傳輸管線中的郵件。因此，寄送給多位寄件者或通訊群組的郵件只會處理一次。並會附加註釋資料流至郵件，大幅提高內容索引的速度，而佔用的資源則變少。

