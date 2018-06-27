---
title: '解除安裝整合通訊語言 Packs_AdditionalUMLangPackExists: Exchange 2013 Help'
TOCTitle: 解除安裝整合通訊語言 Packs_AdditionalUMLangPackExists
ms:assetid: 3a7e2621-0553-44f5-8029-c72fea25af3c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.additionalumlangpackexists(v=EXCHG.150)
ms:contentKeyID: 50472988
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 解除安裝整合通訊語言 Packs\_AdditionalUMLangPackExists

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2016-12-09_

此主題中的內容尚未針對 Microsoft Exchange Server 2013 進行更新。在更新之前，可能還是適用於 Exchange 2013。如果您仍然需要幫助，請查看下方的社群資源。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft Exchange Server 2007 安裝程式無法繼續因為 Unified Messaging server role 升級失敗。

Exchange 安裝程式需要的所有整合通訊伺服器角色、 以外美國英文的語言套件解除安裝語言套件才可繼續 Unified Messaging server role 升級。

包含在 Exchange 2007 的整合通訊 (UM) 語言套件包含預先錄製的提示，特定語言的文字轉換語音 (TTS) 轉換支援。

Exchange 2007 UM 語言套件可讓來電者與 Outlook Voice Access 使用者與 Unified Messaging system 中多種語言進行互動。

如此可安裝新的語言套件要解除安裝需要現有的非-美國英文語言套件。

若要解決此問題，解除安裝所有整合通訊伺服器角色語言套件，除了美國英文的語言套件，然後重新執行 Exchange 2007 的安裝程式。

如需解除安裝 Unified Messaging server role 語言套件的詳細資訊，請參閱 Exchange 2007 產品文件中的[如何移除整合通訊語言套件的整合通訊伺服器](https://go.microsoft.com/fwlink/?linkid=85973) 。

