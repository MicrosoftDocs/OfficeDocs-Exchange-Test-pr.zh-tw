---
title: '移除通訊錄原則: Exchange Online Help'
TOCTitle: 移除通訊錄原則
ms:assetid: c20c6f82-2f75-4116-9be1-c5af10113f71
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh529946(v=EXCHG.150)
ms:contentKeyID: 50474127
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 移除通訊錄原則

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2014-03-25_

使用此程序移除通訊錄原則 (ABP)。

如需其他 ABP 相關的管理工作資訊，請參閱 [Address book 原則程序](address-book-policy-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：少於 5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [電子信箱地址與通訊錄權限](email-address-and-address-book-permissions-exchange-2013-help.md) 主題中的「通訊錄原則」項目。

  - 若已將 ABP 指派給使用者的信箱或虛刪除的信箱，您就無法將其移除。若要判斷是否將某個 ABP 指派給使用者，請在命令介面中執行下列命令：
    
    `Get-Mailbox | Where $._AddressBookPolicy -eq <AddressBookPolicyName>`
    
    若要判斷是否將 ABP 指派給虛刪除的信箱，請執行下列命令：
    
    `Get-Mailbox -SoftDeletedMailbox | Where $._AddressBookPolicy -eq <AddressBookPolicyName>`

  - 若要從使用者信箱中移除 ABP，您可使用該信箱內容的 \[信箱功能\] 頁面或 **Set-Mailbox** 指令程式。

  - 您無法使用 Exchange 系統管理中心 (EAC) 移除 ABP。您必須使用命令介面。

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


## 使用命令介面移除 ABP

本範例將移除名稱為 ABP\_TailspinToys 的 ABP。

    Remove-AddressBookPolicy -Identity "ABP_TailspinToys"

如需詳細的語法及參數資訊，請參閱 [Remove-AddressBookPolicy](https://technet.microsoft.com/zh-tw/library/hh529929\(v=exchg.150\))。

