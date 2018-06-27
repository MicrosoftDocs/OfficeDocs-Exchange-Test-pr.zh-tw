---
title: '佈建收件者的離線通訊錄下載: Exchange Online Help'
TOCTitle: 佈建收件者的離線通訊錄下載
ms:assetid: 141751ac-16d3-4e3c-b70c-004aeedcb5a0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa996345(v=EXCHG.150)
ms:contentKeyID: 50472615
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 佈建收件者的離線通訊錄下載

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2013-02-15_

如果您在組織中使用多個離線通訊錄 (OAB)，有幾種方式可以指定哪些收件者下載哪些 OAB：

  - **每個信箱資料庫**   您可使用 EAC 或命令介面，將信箱資料庫連結至 Office Outlook 2007、Outlook 2010 及 Outlook 2013 用戶端的預設 OAB，佈建 OAB 下載的使用者。

  - **每位收件者**   您可以使用命令介面中的 **Set-Mailbox** 指令程式，透過將 OAB 直接連結到收件者的信箱，以指定下載哪個 OAB。

  - **根據多位收件者 **  您可以使用命令介面中的管線命令，根據共同屬性指定多位收件者下載的 OAB。

  - **每個通訊錄原則**  您可以指定通訊錄原則 (ABP) 以指定的信箱使用者的帳戶的 OAB 下載到收件者的信箱。如果您將 ABP 指派給使用者帳戶已有指派的 OAB 時，明確指派給信箱的 OAB 優先。如需詳細資訊，請參閱[通訊錄原則指派給郵件使用者](assign-an-address-book-policy-to-mail-users-exchange-2013-help.md)。

如需與 OAB 相關的其他管理工作，請參閱[離線通訊錄程序](offline-address-book-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘。

  - 您無法使用 Exchange 系統管理中心 (EAC) 來執行這些程序。您必須使用命令介面。

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

## 透過將收件者的信箱資料庫連結到公用資料夾資料庫或連結到預設 OAB，利用命令介面為收件者提供 OAB 下載

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「信箱資料庫」項目。

此範例會為預設信箱資料庫設定 My OAB 的 Web 式發佈。

    Set-MailboxDatabase -Identity "Mailbox Database" -OfflineAddressBook "My OAB"

如需詳細的語法及參數資訊，請參閱 [Set-MailboxDatabase](https://technet.microsoft.com/zh-tw/library/bb123971\(v=exchg.150\))。

## 使用命令介面，透過將 OAB 直接連結到收件者的信箱，以指定下載哪個 OAB

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「收件者佈建權限」一節。

若要透過將 OAB 直接連結到收件者的信箱，來指定下載哪個 OAB，請使用下列語法。

    Set-Mailbox -Identity <MailboxIDParameter> -OfflineAddressBook <OfflineAddressBookIdParameter>

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><em>Identity</em>參數會識別信箱及可接受下列值： GUID ADObjectID、 辨別名稱 (DN)、 <em>domain\account</em>、 使用者主要名稱 (UPN)、 LegacyExchangeDN、 SmtpAddress、 及別名。</td>
</tr>
</tbody>
</table>


此範例會指定使用者 Kim 將下載 OAB My OAB。

    Set-Mailbox -Identity Kim -OfflineAddressBook "My OAB"

如需詳細的語法及參數資訊，請參閱 [Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\))。

## 使用命令介面指定多位收件者將下載的 OAB

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「收件者佈建權限」一節。

此範例會指定 Contoso 在美國的所有使用者信箱都下載 OAB Contoso United States。

    Get-User -ResultSize Unlimited -Filter { Company -eq "Contoso" -and RecipientType -eq "UserMailbox" } | Where { $_.CountryOrRegion -eq "United States"} | Set-Mailbox -OfflineAddressBook "Contoso United States"

如需詳細的語法及參數資訊，請參閱 [Get-User](https://technet.microsoft.com/zh-tw/library/aa996896\(v=exchg.150\)) 與 [Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\))。

