---
title: 'Active Directory: Exchange 2013 Help'
TOCTitle: Active Directory
ms:assetid: 8e8464df-2d1d-4d68-82de-b0c158c549c3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb123715(v=EXCHG.150)
ms:contentKeyID: 50473711
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Active Directory

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

Microsoft Exchange Server 2013 使用 Active Directory 來儲存並與 Windows 分享目錄資訊。Exchange 2013 的 Active Directory 樹系設計與 Exchange Server 2010 類似 (除了幾項不同外)，說明如下：

## Active Directory 驅動程式

Active Directory驅動程式是核心 Microsoft Exchange元件可允許Exchange services 建立、 修改、 刪除和Active Directory網域服務 (AD DS) 資料的查詢。Exchange 2013，在完成所有的存取權Active Directory使用本身的Active Directory驅動程式。先前， Exchange 2010，DSAccess 提供目錄查閱服務的元件，例如 SMTP、 郵件傳輸代理程式 (MTA) 及Exchange存放區。

Active Directory驅動程式也會使用 Microsoft ExchangeActive Directory拓撲 (MSExchangeADTopology) 允許使用目錄服務存取 (DSAccess) 拓撲資料的Active Directory驅動程式。此資料包括可用網域控制站和可處理Exchange要求的通用類別目錄伺服器的清單。如需Active Directory驅動程式的詳細資訊，請參閱 ＜ [Active Directory 網域服務](https://go.microsoft.com/fwlink/p/?linkid=110942)。

## Active Directory 架構變更

Exchange 2013將新屬性新增至Active Directory網域服務架構，並也讓其他修改現有的類別和屬性。如需Active Directory變更安裝Exchange 2013，請參閱[Exchange 2013 Active Directory 架構變更](exchange-2013-active-directory-schema-changes-exchange-2013-help.md)時詳細資訊。

## 相關資訊

若要深入了解 Active Directory 中 Exchange 2013 的儲存和擷取資訊，以便您計劃對它的存取，請參閱[Active Directory 權](access-to-active-directory-exchange-2013-help.md)。

如需Active Directory樹系設計的詳細資訊，請參閱[AD DS 設計指南](https://go.microsoft.com/fwlink/p/?linkid=264957)。

若要深入了解在 Active Directory 網域中執行 Windows 和在脫離的命名空間部署 Exchange 2013 之電腦的相關資訊，請參閱[斷續的命名空間案例](disjoint-namespace-scenarios-exchange-2013-help.md)。

