---
title: '地址清單中新增或移除的通訊清單的離線通訊錄: Exchange Online Help'
TOCTitle: 地址清單中新增或移除的通訊清單的離線通訊錄
ms:assetid: 86bd5651-ad41-4516-bf23-6579f4e4da03
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb123563(v=EXCHG.150)
ms:contentKeyID: 50473630
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 地址清單中新增或移除的通訊清單的離線通訊錄

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2014-12-16_

您可以使用命令介面來新增或移除離線通訊錄 (OAB) 的通訊清單。根據預設，沒有 OAB 名為預設離線通訊錄包含全域通訊清單 (GAL)。根據其所包含的地址清單產生 Oab。若要建立自訂使用者可以下載的 Oab，您可以新增或移除 Oab 中的地址清單。

如需與 OAB 相關的其他管理工作，請參閱[離線通訊錄程序](offline-address-book-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「離線通訊錄」項目。

  - 根據 Exchange Online 的預設，「通訊清單」角色並未指派給任何角色群組。若要使用任何需要「通訊清單」角色的指令程式，您需將此角色新增至角色群組。如需詳細資訊，請參閱＜[管理角色群組](manage-role-groups-exchange-2013-help.md)＞主題的＜將角色新增至角色群組＞一節。

  - 地址清單變更不適用於用戶端下載 （英文） 直到之後件地址清單所在的 OAB 產生之後。如需詳細資訊，請參閱[更新離線通訊錄](update-an-offline-address-book-exchange-2013-help.md)。

  - 您無法使用 Exchange 系統管理中心 (EAC) 執行此程序。您必須使用命令介面。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 您要執行的工作

## 使用命令介面將通訊清單新增到 OAB

當使用*AddressLists*參數時，就會覆寫目前存在任何地址清單。您必須加入現有的通訊清單中您 OAB 產生這些地址清單會繼續使用*AddressLists*參數時。此範例中，您有 AddressList1 和 AddressList2、 新增 AddressList3。

    Set-OfflineAddressBook -Identity "My OAB" -AddressLists AddressList1,AddressList2,AddressList3

如需詳細的語法及參數資訊，請參閱 [Set-OfflineAddressBook](https://technet.microsoft.com/zh-tw/library/aa996330\(v=exchg.150\))。

## 使用命令介面從 OAB 中移除通訊清單

若要移除 OAB 的通訊清單，只要省略該清單中的通訊清單的地址清單。此範例中，您有 AddressList1、 AddressList2，以及 AddressList3，會移除 AddressList3。

    Set-OfflineAddressBook -Identity "My OAB" -AddressLists AddressList1,AddressList2

如需詳細的語法及參數資訊，請參閱 [Set-OfflineAddressBook](https://technet.microsoft.com/zh-tw/library/aa996330\(v=exchg.150\))。

