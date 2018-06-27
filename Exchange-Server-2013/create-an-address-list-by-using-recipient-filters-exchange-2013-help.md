---
title: '使用收件者篩選器來建立通訊清單: Exchange Online Help'
TOCTitle: 使用收件者篩選器來建立通訊清單
ms:assetid: 8eabea64-97c6-40af-b61c-9b6a125cbdf1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb123718(v=EXCHG.150)
ms:contentKeyID: 50473713
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用收件者篩選器來建立通訊清單

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2014-12-16_

本主題說明如何使用收件者篩選器來建立通訊清單。若要深入了解通訊清單，請參閱[通訊清單](address-lists-exchange-2013-help.md)。

如需與通訊清單相關的其他管理工作，請參閱[地址清單程序](address-list-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [電子信箱地址與通訊錄權限](email-address-and-address-book-permissions-exchange-2013-help.md)主題中的「通訊清單」項目。

  - 根據 Exchange Online 的預設，「通訊清單」角色並未指派給任何角色群組。若要使用任何需要「通訊清單」角色的指令程式，您需將此角色新增至角色群組。如需詳細資訊，請參閱＜[管理角色群組](manage-role-groups-exchange-2013-help.md)＞主題的＜將角色新增至角色群組＞一節。

  - 若要使用*RecipientFilter*參數來建立自訂篩選，您必須指定篩選條件的字串。命令介面中使用 OPATH 篩選語法。OPATH 是設計用來查詢物件的資料來源的查詢語言。

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


## 使用命令介面以收件者篩選器建立通訊清單

此範例會為所有在 Washington 或 Oregon 中擁有 Exchange 信箱之使用者建立通訊清單。

    New-AddressList -Name "Pacific Northwest Mailboxes" -RecipientFilter {((RecipientType -eq 'UserMailbox') -and ((StateOrProvince -eq 'Washington') -or (StateOrProvince -eq 'Oregon')))}

此範例為具有 Exchange 信箱且 *CustomAttribute15* 參數值為 `AgencyB` 的所有使用者建立一份通訊清單。

    New-AddressList -Name "AgencyB" -RecipientFilter {(RecipientType -eq 'UserMailbox') -and (CustomAttribute15 -like *AgencyB*)}

如需詳細的語法及參數資訊，請參閱 [New-AddressList](https://technet.microsoft.com/zh-tw/library/aa996912\(v=exchg.150\))。

