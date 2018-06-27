---
title: '網域: Exchange 2013 Help'
TOCTitle: 網域
ms:assetid: 11748c2d-2e32-43a4-b77d-e0c17db6200b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ673041(v=EXCHG.150)
ms:contentKeyID: 50472606
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 網域

 

_**適用版本：**Exchange Server 2013, Office 365_

_**上次修改主題的時間：**2012-10-11_

網域代表的電子郵件的目錄與信箱已設定的 SMTP 命名空間。藉由使用 Microsoft Exchange Server 2013組織設定之網域的互動，您可以設定Exchange如何處理與不同網域的電子郵件。

## 公認的網域

公認的網域是指Exchange組織傳送或接收電子郵件的任何 SMTP 命名空間。公認的網域包含這些Exchange組織的授權、 以及內部轉送網域的網域和外部轉送網域。它會處理公認的網域中的收件者郵件傳遞時代表性Exchange組織。公認的網域也包含Exchange組織會收到郵件，其再將它轉送至組織外的電子郵件伺服器的網域。

如需公認的網域的相關資訊，請參閱[公認的網域](accepted-domains-exchange-2013-help.md)。

## 遠端網域

在Exchange 2013，您可以建立遠端網域項目以定義Exchange組織與組織外的網域之間的郵件傳輸設定。當您建立的遠端網域項目時，會控制傳送至該網域的郵件的類型。您也可以套用郵件格式原則與可接受的字元組從您組織中使用者傳送至遠端網域的郵件。

設定遠端網域不Exchange組織的通用組態設定。遠端網域設定會套用至郵件分類期間。收件者解析時發生的收件者的網域會進行比對設定的遠端網域。如果遠端網域設定封鎖特定的郵件類型阻止傳送給收件者的網域中，會刪除郵件。如果您指定特定的郵件格式為遠端網域，則會修改的郵件標頭和內容。這些設定套用至Exchange組織所處理的所有郵件。

有关远程域的详细信息，请参阅[遠端網域](remote-domains-exchange-2013-help.md)。

