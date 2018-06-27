---
title: '管理郵件提示的組織關係: Exchange Online Help'
TOCTitle: 管理郵件提示的組織關係
ms:assetid: 6e6b48ef-c41c-47ad-8063-66901765c2a5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ649324(v=EXCHG.150)
ms:contentKeyID: 50473453
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理郵件提示的組織關係

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2015-04-08_

您可以使用 Exchange 管理命令介面來設定自訂郵件提示各種組織之間。

建立組織關聯性，您可以以增強兩種組織的使用者經驗共用空閒/忙碌資料、 設定安全的郵件流程及啟用郵件追蹤。如需組織關聯性的詳細資訊，請參閱[透過組織關聯性的郵件提示](mailtips-over-organization-relationships-exchange-2013-help.md)。

您可以使用各種設定來控制已建立組織關聯性的兩個組織之間寄件提醒的使用方式。本節中的程序說明這些不同的控制項。在所有的範例中，內部部署組織為 contoso.com、 遠端組織 online.contoso.com，且組織關聯性名為 Contoso 線上。

您可以使用**Set-OrganizationRelationship**指令程式來設定這些設定。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「郵件提示」項目。

  - 您只能使用命令介面來執行此程序。

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

## 使用命令介面啟用或停用兩個組織之間的郵件提示

此範例會設定組織關聯性，讓郵件提示會傳回給寄件者遠端組織中撰寫郵件給組織中的收件者時。

    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessEnabled $true

此範例會防止寄件提醒撰寫郵件給組織中的收件者時要傳回給寄件者遠端組織中的組織關聯性。

    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessEnabled $false

如需詳細的語法及參數資訊，請參閱[Set-OrganizationRelationship](https://technet.microsoft.com/zh-tw/library/ee332326\(v=exchg.150\))。

## 使用命令介面來設定此郵件提示會傳回至遠端組織

每個組織的關係，您可以決定哪組郵件提示會傳回給其他組織中的寄件者。此範例會設定組織關聯性，讓所有的郵件提示會傳回。

    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessLevel All

此範例會設定組織關聯性，讓僅自動回覆、 「 超過大小訊息、 受限制的收件者及信箱滿 」 郵件提示會傳回。

    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessLevel Limited

此範例會設定組織關聯性，讓沒有郵件提示會傳回。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>請勿停用此關係的郵件提示使用此方法。若要停用寄件提醒、 <em>MailTipsAccessEnabled</em>參數設定為<code>$false</code>。</td>
</tr>
</tbody>
</table>


    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessLevel None

如需詳細的語法及參數資訊，請參閱[Set-OrganizationRelationship](https://technet.microsoft.com/zh-tw/library/ee332326\(v=exchg.150\))。

## 使用命令介面來設定的使用者特定收件者的郵件提示會傳回其特定群組

您可以限制特定收件者的寄件提醒返回特定使用者群組。根據預設，當您的組織關聯性，讓寄件提醒下列特定收件者的郵件提示會傳回所有使用者：

  - 自動回覆

  - 信箱已滿

  - 自訂郵件提示

您可以指定寄件提醒存取群組上的組織關聯性。指定群組之後，特定收件者的郵件提示會僅傳回信箱、 郵件連絡人和郵件使用者屬於該群組的成員。此範例會傳回特定收件者的寄件提醒僅適用於 ShareMailTips@contoso.com 群組之成員的組織關聯性。

    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessScope ShareMailTips@contoso.com

如需詳細的語法及參數資訊，請參閱[Set-OrganizationRelationship](https://technet.microsoft.com/zh-tw/library/ee332326\(v=exchg.150\))。

