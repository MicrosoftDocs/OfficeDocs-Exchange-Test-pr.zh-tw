---
title: 'Outlook 保護規則: Exchange 2013 Help'
TOCTitle: Outlook 保護規則
ms:assetid: 569fc3be-b269-43f5-8797-73ab0691e685
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee633467(v=EXCHG.150)
ms:contentKeyID: 50473238
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook 保護規則

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

使用 Microsoft Outlook保護規則，您可以套用Outlook 2010[Active Directory Rights Management Services (AD RMS)](https://technet.microsoft.com/en-us/library/hh831364.aspx)範本之前傳送的郵件保護使用資訊版權管理 (IRM) 的郵件。若要防止Outlook保護規則套用，您可以停用規則。移除Outlook保護規則會移除規則定義Active Directory。

若欲瞭解更多與 IRM 相關的管理工作，請參閱 [資訊版權管理程序](information-rights-management-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「版權保護」項目。

  - 您無法使用 Exchange 系統管理中心 (EAC) 來移除Outlook保護規則。您必須使用命令介面。

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

## 使用命令介面移除 Outlook 保護規則

本範例移除 Outlook 保護規則 OPR-DG-Finance。

    Remove-OutlookProtectionRule -Identity "OPR-DG-Finance"

如需詳細的語法及參數資訊，請參閱 [Remove-OutlookProtectionRule](https://technet.microsoft.com/zh-tw/library/dd297961\(v=exchg.150\))。

## 使用命令介面移除所有的 Outlook 保護規則

本範例移除 Exchange 組織中的所有 Outlook 保護規則。

    Get-OutlookProtectionRule | Remove-OutlookProtectionRule

如需詳細的語法及參數資訊，請參閱 [Get-OutlookProtectionRule](https://technet.microsoft.com/zh-tw/library/dd298004\(v=exchg.150\)) 與 [Remove-OutlookProtectionRule](https://technet.microsoft.com/zh-tw/library/dd297961\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要驗證您已成功移除 Outlook 保護規則，使用[Get-OutlookProtectionRule](https://technet.microsoft.com/zh-tw/library/dd298004\(v=exchg.150\))指令程式可擷取 Outlook 保護規則。如何擷取 Outlook 保護規則的範例，請參閱**Get-OutlookProtectionRule**中的[範例](https://technet.microsoft.com/zh-tw/dd298004\(exchg.150\)#examples)。

