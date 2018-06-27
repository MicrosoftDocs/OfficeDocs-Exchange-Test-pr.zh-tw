---
title: '使用收件者篩選器來建立電子郵件地址原則: Exchange 2013 Help'
TOCTitle: 使用收件者篩選器來建立電子郵件地址原則
ms:assetid: e3f446bd-1511-479c-8d87-2dfce5547c90
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb232194(v=EXCHG.150)
ms:contentKeyID: 50474475
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用收件者篩選器來建立電子郵件地址原則

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-16_

您可以使用命令介面來建立電子郵件地址原則使用收件者篩選器。若要深入了解電子郵件地址原則，請參閱[電子郵件地址原則](email-address-policies-exchange-2013-help.md)。

如欲瞭解更多與角色群組相關的管理工作，請參閱 [電子郵件地址原則程序](email-address-policy-procedures-exchange-2013-help.md)。

## 開始前需要瞭解什麼？

  - 預估完成時間：5 分鐘。

  - 若要使用*RecipientFilter*參數來建立自訂篩選，您必須指定篩選條件的字串。命令介面中使用 OPath 篩選語法。OPath 是設計用來查詢物件的資料來源的查詢語言。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您使用的收件者篩選器來建立或編輯的電子郵件地址原則，您無法使用 Exchange 系統管理中心 (EAC) 來編輯電子郵件地址原則。您必須使用命令介面。如需詳細的語法及參數資訊，請參閱<a href="https://technet.microsoft.com/zh-tw/library/bb124517(v=exchg.150)">Set-EmailAddressPolicy</a>。</td>
    </tr>
    </tbody>
    </table>


  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [電子郵件地址和通訊錄](email-addresses-and-address-books-exchange-2013-help.md) 項目中的「電子郵件地址原則」項目。

  - SMTP 地址網域可使用於電子郵件地址原則之前，您必須設定公認的網域。如需詳細資訊，請參閱[公認的網域](accepted-domains-exchange-2013-help.md)。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 使用命令介面透過收件者篩選器建立電子郵件地址原則

若要使用收件者篩選器建立電子郵件地址原則，請使用下列語法。

    New-EmailAddressPolicy -Name <String> -RecipientFilter <String>

此範例建立套用至所有主管的電子郵件地址原則，其中，電子郵件地址的本機部份由其名字的前兩個字母和整個姓氏組成。

    New-EmailAddressPolicy -Name 'Execs' -EnabledEmailAddressTemplates 'SMTP:%2g%s@contoso.com' -RecipientFilter {((RecipientType -eq 'UserMailbox') -and (Title -like 'executive'))}

如需詳細語法及參數的資訊，請參閱 [New-EmailAddressPolicy](https://technet.microsoft.com/zh-tw/library/aa996800\(v=exchg.150\))。

