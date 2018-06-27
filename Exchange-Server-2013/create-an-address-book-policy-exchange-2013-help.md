---
title: '建立通訊錄原則: Exchange Online Help'
TOCTitle: 建立通訊錄原則
ms:assetid: 6359abaf-e6f6-4667-8c2b-3860728b39a9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh529931(v=EXCHG.150)
ms:contentKeyID: 50473339
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 建立通訊錄原則

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2014-12-16_

通訊錄原則 (Abp) 允許您線段使用者到特定群組提供貴組織的全域通訊清單 (GAL) 的自訂的檢視。建立 ABP，您可以對原則指派 GAL、 離線通訊錄 (OAB)、 \[聊天室\] 清單中及一或多個地址清單。然後您可指派 ABP 提供這些到 Outlook 和 Outlook Web App 中的自訂 GAL 存取的信箱使用者。目標是提供簡易的機制來完成需要多個 Gal 的內部部署組織的 GAL 區隔。若要深入了解 Abp，請參閱[通訊錄原則](address-book-policies-exchange-2013-help.md)。

如需其他 ABP 相關的管理工作資訊，請參閱 [Address book 原則程序](address-book-policy-procedures-exchange-2013-help.md)。

並使用此程序的案例的相關資料嗎？請參閱[案例： 部署通訊錄原則](scenario-deploying-address-book-policies-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - Estmated 完成時間： 少於 5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [電子信箱地址與通訊錄權限](email-address-and-address-book-permissions-exchange-2013-help.md) 主題中的「通訊錄原則」項目。

  - 根據 Exchange Online 的預設，「通訊清單」角色並未指派給任何角色群組。若要使用任何需要「通訊清單」角色的指令程式，您需將此角色新增至角色群組。如需詳細資訊，請參閱＜[管理角色群組](manage-role-groups-exchange-2013-help.md)＞主題的＜將角色新增至角色群組＞一節。

  - 建立組織 ABP 是需要規劃多個步驟程序。如需詳細資訊，請參閱[案例： 部署通訊錄原則](scenario-deploying-address-book-policies-exchange-2013-help.md)。

  - 您無法使用 Exchange 系統管理中心 (EAC) 來建立 Abp。您必須使用命令介面。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

  - 有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

## 使用命令介面建立 ABP

這個範例會建立具有下列設定的 ABP：

  - **名稱：** All Fabrikam ABP

  - **GAL：** All Fabrikam

  - **OAB：** Fabrikam 所有 OAB

  - **會議室清單：** 所有 Fabrikam 聊天室

  - **通訊清單：** All Fabrikam、 All Fabrikam Mailboxes、 All Fabrikam DLs、 及 All Fabrikam Contacts

<!-- end list -->

    New-AddressBookPolicy -Name "All Fabrikam ABP" -AddressLists "\All Fabrikam","\All Fabrikam Mailboxes","\All Fabrikam DLs","\All Fabrikam Contacts" -OfflineAddressBook \Fabrikam-All-OAB -GlobalAddressList "\All Fabrikam" -RoomList "\All Fabrikam Rooms"

如需詳細的語法及參數資訊，請參閱 [New-AddressBookPolicy](https://technet.microsoft.com/zh-tw/library/hh529913\(v=exchg.150\))。

## 相關資訊

[通訊錄原則指派給郵件使用者](assign-an-address-book-policy-to-mail-users-exchange-2013-help.md)

