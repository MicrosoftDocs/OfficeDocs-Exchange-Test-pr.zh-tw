---
title: '建立全域通訊清單: Exchange Online Help'
TOCTitle: 建立全域通訊清單
ms:assetid: 59e4955a-8999-4d17-be9f-23a41a23b929
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb232063(v=EXCHG.150)
ms:contentKeyID: 50473261
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 建立全域通訊清單

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2014-12-16_

全域通訊清單 (GAL) 是包含的每個群組、 使用者及組織實作MicrosoftExchange連絡人項目目錄。如果貴組織使用通訊錄原則，您可能會想要建立其他的 Gal。若要深入了解，請參閱[通訊錄原則](address-book-policies-exchange-2013-help.md)。

如需與通訊清單相關的其他管理工作，請參閱[地址清單程序](address-list-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [電子信箱地址與通訊錄權限](email-address-and-address-book-permissions-exchange-2013-help.md)主題中的「通訊清單」項目。

  - 根據 Exchange Online 的預設，「通訊清單」角色並未指派給任何角色群組。若要使用任何需要「通訊清單」角色的指令程式，您需將此角色新增至角色群組。如需詳細資訊，請參閱＜[管理角色群組](manage-role-groups-exchange-2013-help.md)＞主題的＜將角色新增至角色群組＞一節。

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

## 利用命令介面來建立使用條件式篩選器屬性的 GAL

此範例會針對公司列為 Contoso 且是信箱使用者的收件者，建立名為 GAL\_Contoso 的 GAL。

    New-GlobalAddressList -Name "GAL_Contoso" -IncludedRecipients MailboxUsers -ConditionalCompany Contoso

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若您使用預先定義的條件式篩選器屬性，則 <em>IncludedRecipients</em> 參數不能是空的。</td>
</tr>
</tbody>
</table>


如需詳細的語法及參數資訊，請參閱 [New-GlobalAddressList](https://technet.microsoft.com/zh-tw/library/bb123785\(v=exchg.150\))。

## 利用命令介面來建立使用收件者篩選器的 GAL

此範例會針對 *CustomAttribute15* 參數具有 `AgencyA` 值的收件者，建立名為 GAL\_AgencyA 的 GAL。

    New-GlobalAddressList -Name "GAL_AgencyA" -RecipientFilter {CustomAttribute15 -like "AgencyA"}

如需詳細的語法及參數資訊，請參閱 [New-GlobalAddressList](https://technet.microsoft.com/zh-tw/library/bb123785\(v=exchg.150\))。

