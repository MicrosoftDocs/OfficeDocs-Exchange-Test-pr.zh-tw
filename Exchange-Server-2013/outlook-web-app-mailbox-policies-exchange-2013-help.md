---
title: 'Outlook Web App 信箱原則: Exchange Online Help'
TOCTitle: Outlook Web App 信箱原則
ms:assetid: 213b8b7a-1c29-49ee-8c98-d0364ddf4f9d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd335142(v=EXCHG.150)
ms:contentKeyID: 50472696
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook Web App 信箱原則

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2012-10-05_

使用 MicrosoftOutlook Web App信箱原則可建立組織層級原則，以管理對 Outlook Web App 中功能的存取。

**目錄**

Outlook Web App mailbox policies

Creating or deleting Outlook Web App mailbox policies

Configuring Outlook Web App mailbox policies

Applying Outlook Web App mailbox policies

## Outlook Web App 信箱原則

在Exchange 2013，您可以建立多個Outlook Web App信箱原則並套用至個別信箱。當Outlook Web App信箱原則套用到信箱它會覆寫的虛擬目錄的設定。

也可以藉由設定Outlook Web App虛擬目錄管理Outlook Web App功能。虛擬目錄設定將用於信箱原則尚未套用至任何信箱。

## 建立或刪除 Outlook Web App 信箱原則

預設Outlook Web App信箱原則會在安裝Exchange時自動建立。根據預設，所有啟用兩個選項的預設Outlook Web App信箱原則上。您可以視以符合組織的需求建立相同數目的Outlook Web App信箱原則。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>預設的 Outlook Web App 信箱原則不會自動套用到任何信箱。</td>
</tr>
</tbody>
</table>


如需建立或移除信箱原則的相關資訊，請參閱 [建立 Outlook Web App 信箱原則](create-an-outlook-web-app-mailbox-policy-exchange-2013-help.md) 與 [從 Exchange 中移除 Outlook Web App 信箱原則](remove-an-outlook-web-app-mailbox-policy-from-exchange-exchange-2013-help.md)。

## 設定 Outlook Web App 信箱原則

預設Outlook Web App信箱原則具有預設啟用的所有選項。如需設定Outlook Web App信箱原則的資訊，請參閱[檢視或設定 Outlook Web App 信箱原則屬性](view-or-configure-outlook-web-app-mailbox-policy-properties-exchange-2013-help.md)。

## 套用 Outlook Web App 信箱原則

只能將一個 Outlook Web App 信箱原則套用至信箱。

如果沒有套用任何 Outlook Web App 信箱原則至信箱，則會套用虛擬目錄上所定義的設定。

Outlook Web App信箱原則可套用到信箱，使用 Exchange 系統管理中心 (EAC) 來修改現有的信箱，或使用命令介面和[Set-CASMailbox](https://technet.microsoft.com/zh-tw/library/bb125264\(v=exchg.150\))指令程式來套用信箱原則。如需詳細資訊，請參閱[套用或移除信箱上的 Outlook Web App 信箱原則](apply-or-remove-an-outlook-web-app-mailbox-policy-on-a-mailbox-exchange-2013-help.md)。

