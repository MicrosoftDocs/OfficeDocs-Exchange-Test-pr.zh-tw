---
title: '變更通訊錄原則的設定: Exchange Online Help'
TOCTitle: 變更通訊錄原則的設定
ms:assetid: ba1ca350-71c2-4c60-a612-33bfa9320b5e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh529941(v=EXCHG.150)
ms:contentKeyID: 50474051
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 變更通訊錄原則的設定

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2016-03-30_

建立通訊錄原則 (ABP) 之後，您可以檢視或修改名稱及指派全域通訊清單 (GAL)、 離線通訊錄 (OAB)、 會議室清單及通訊清單。

Abp 相關的其他管理工作，請參閱[Address book 原則程序](address-book-policy-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - Estmated 完成時間： 少於 5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [電子信箱地址與通訊錄權限](email-address-and-address-book-permissions-exchange-2013-help.md) 主題中的「通訊錄原則」項目。

  - 建立組織 ABP 是需要規劃多個步驟程序。如需詳細資訊，請參閱[案例： 部署通訊錄原則](scenario-deploying-address-book-policies-exchange-2013-help.md)

  - 您無法使用 Exchange 系統管理中心 (EAC) 來設定 Abp。您必須使用命令介面。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

  - 有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

## 您想怎麼做？

## 變更 OAB、 會議室清單和 GAL 的 ABP

本範例會變更 OAB、 聊天室\] 清單中，並將對其指派 ABP 信箱使用者所使用的 GAL 名為所有 Fabrikam ABP.

    Set-AddressBookPolicy -Identity "All Fabrikam ABP" -OfflineAddressBook \Fabrikam-OAB-2 -GlobalAddressList "\All Fabrikam GAL" -RoomList "\All Fabrikam Rooms"

## 取代 ABP 通訊清單

將現有的 ABP 您指定的地址清單取代 ABP.中的所有通訊清單

這個範例會將現有的通訊清單取代為名為政府機構 A ABP 分別名為 GovernmentAgencyA Atlanta 和 GovernmentAgencyA 莫斯科通訊清單

    Set-AddressBookPolicy -Identity "Government Agency A" -AddressLists "GovernmentAgencyA-Atlanta","GovernmentAgencyA-Moscow"

## 將地址清單新增至 ABP

若要保留在 ABP 中已定義的通訊清單，您需要時您加入新的 ABP.指定這些地址清單

此範例會將名為 Contoso-伊利諾至 ABP 的地址清單名為 ABP Contoso，已設定為使用名為 Contoso 西雅圖的地址清單。

    Set-AddressBookPolicy -Identity "ABP Contoso" -AddressLists "Contoso-Chicago","Contoso-Seattle"

## 通訊清單移除 ABP

若要移除 ABP 中已定義的現有通訊清單，您需要指定您要保留的地址清單。

例如，名為 ABP Fabrikam ABP 會使用名為 Fabrikam HR 和 Fabrikam Finance 通訊清單。若要移除 ABP Fabrikam HR 通訊清單，指定您要保留的 Fabrikam Finance 通訊清單。

    Set-AddressBookPolicy -Identity "ABP Fabrikam" -AddressLists Fabrikam-Finance

## 相關資訊

如需詳細的語法及參數資訊，請參閱[Set-AddressBookPolicy](https://technet.microsoft.com/zh-tw/library/hh529945\(v=exchg.150\))。

