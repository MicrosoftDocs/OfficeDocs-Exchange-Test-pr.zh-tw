---
title: '設定全域通訊清單屬性: Exchange Online Help'
TOCTitle: 設定全域通訊清單屬性
ms:assetid: 5fd2c96f-fe93-4b5a-8495-70c450511a37
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb232068(v=EXCHG.150)
ms:contentKeyID: 50473314
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定全域通訊清單屬性

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2014-12-16_

此主題解釋修改全域通訊清單 (GAL) 的設定。

如需與通訊清單相關的其他管理工作，請參閱[地址清單程序](address-list-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [電子信箱地址與通訊錄權限](email-address-and-address-book-permissions-exchange-2013-help.md)主題中的「通訊清單」項目。

  - 根據 Exchange Online 的預設，「通訊清單」角色並未指派給任何角色群組。若要使用任何需要「通訊清單」角色的指令程式，您需將此角色新增至角色群組。如需詳細資訊，請參閱＜[管理角色群組](manage-role-groups-exchange-2013-help.md)＞主題的＜將角色新增至角色群組＞一節。

  - 您無法編輯預設 GAL 的設定。

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


## 使用命令介面設定 GAL 內容

此範例會為具有 GUID 96d0c505-eba8-4103-ad4f-577a1bf4ad7b 的 GAL 指派新名稱 FourthCoffee。

    Set-GlobalAddressList -Identity 96d0c505-eba8-4103-ad4f-577a1bf4ad7b -Name FourthCoffee

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若您使用預先定義的條件式篩選器屬性，則 <em>IncludedRecipients</em> 參數的值不能是空的。</td>
</tr>
</tbody>
</table>


此範例會將要包含在 Fourth Coffee 全域 GAL 中的收件者，變更為其公司設為 Fourth Coffee 的收件者。

    Set-GlobalAddressList -Identity Fourth Coffee -RecipientFilter {Company -eq "Fourth Coffee"}

如需詳細的語法及參數資訊，請參閱 [Set-GlobalAddressList](https://technet.microsoft.com/zh-tw/library/bb123877\(v=exchg.150\))。

