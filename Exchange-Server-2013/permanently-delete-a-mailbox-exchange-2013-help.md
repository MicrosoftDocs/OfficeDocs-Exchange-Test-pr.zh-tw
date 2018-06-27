---
title: '永久刪除信箱: Exchange 2013 Help'
TOCTitle: 永久刪除信箱
ms:assetid: df35765a-0bef-4561-9846-d91d69c0269c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ863440(v=EXCHG.150)
ms:contentKeyID: 50554101
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 永久刪除信箱

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2012-11-16_

當您永久刪除作用中信箱和中斷連線的信箱從 Exchange 信箱資料庫，會清除所有的信箱內容和資料遺失是永久性動作。當您永久刪除作用中的信箱時，也會刪除相關聯的 Active Directory 使用者帳戶。

若要永久刪除信箱的替代項是中斷它。中斷預設的連線信箱後，它會保留在信箱資料庫 30 天。這讓您有機會重新連線或還原它會從資料庫清除之前的信箱。

若要深入了解中斷連線信箱與執行其他相關管理工作的詳細資訊，請參閱以下主題：

  - [中斷連線的信箱](disconnected-mailboxes-exchange-2013-help.md)

  - [停用或刪除信箱](disable-or-delete-a-mailbox-exchange-2013-help.md)

  - [連線已停用的信箱](connect-a-disabled-mailbox-exchange-2013-help.md)

  - [連線或還原已刪除的信箱](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您無法使用 EAC 永久刪除作用中的信箱或中斷連線的信箱。</td>
</tr>
</tbody>
</table>


## 開始之前有哪些須知？

  - 預估完成時間：2 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md) 主題中的「收件者佈建權限」一節。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 您要執行的工作

## 永久刪除作用中的信箱

## 若要永久地刪除作用中的信箱使用命令介面

執行下列命令以永久刪除作用中信箱和相關聯的 Active Directory 使用者帳戶。

    Remove-Mailbox -Identity <identity> -Permanent $true

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您未包含<em>Permanent</em>參數，刪除的信箱會保留信箱資料庫中 30 天內，預設會永久刪除之前。</td>
</tr>
</tbody>
</table>


如需詳細語法及參數的資訊，請參閱 [Remove-Mailbox](https://technet.microsoft.com/zh-tw/library/aa995948\(v=exchg.150\))。

## 如何知道這是否正常運作？

若要確認您是否已永久刪除作用中的信箱，請執行下列動作：

1.  確認信箱已不再列出在 EAC 中。

2.  確認關聯的使用者帳戶不再列在 \[Active Directory 使用者及電腦。

3.  執行下列命令來確認信箱已成功清除從 Exchange 信箱資料庫。
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" }
    
    如果您已順利將清除信箱，此命令將不會傳回任何結果。如果未清除信箱，此命令會傳回信箱的相關資訊。

## 永久刪除已中斷連線的信箱

## 使用命令介面永久刪除中斷連線的信箱

有兩種類型的中斷連線信箱 ︰ 已停用和虛刪除。您必須指定其中一個這類執行 cmdlet 可永久刪除信箱時。如果您指定的類型不符合中斷連線的信箱的實際類型，此命令將會失敗。

執行下列命令以判斷是否已中斷連線的信箱已停用或虛刪除。

    Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisplayName,MailboxGuid,Database,DisconnectReason

中斷連線信箱*DisconnectReason*屬性的值將會是`Disabled`或`SoftDeleted`。

您可以執行下列命令以顯示您組織中所有已中斷連線信箱的類型。

    Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisconnectReason -ne $null } | fl DisplayName,MailboxGuid,Database,DisconnectReason

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您要永久刪除 [中斷連線的信箱使用<strong>Remove-StoreMailbox</strong>指令程式時，及其所有內容會從信箱資料庫都清除及資料遺失是永久性動作。</td>
</tr>
</tbody>
</table>


這個範例會從信箱資料庫 MBD01 中，永久刪除 UID 為 2ab32ce3-fae1-4402-9489-c67e3ae173d3 的已停用信箱。

    Remove-StoreMailbox -Database MBD01 -Identity "2ab32ce3-fae1-4402-9489-c67e3ae173d3" -MailboxState Disabled

此範例會永久刪除的虛刪除信箱 Dan 跳轉的信箱資料庫 mbd01。

    Remove-StoreMailbox -Database MBD01 -Identity "Dan Jump" -MailboxState SoftDeleted

這個範例會從信箱資料庫 MBD01 中，永久刪除所有虛刪除信箱。

    Get-MailboxStatistics -Database MBD01 | where {$_.DisconnectReason -eq "SoftDeleted"} | ForEach {Remove-StoreMailbox -Database $_.Database -Identity $_.MailboxGuid -MailboxState SoftDeleted}

如需詳細的語法及參數資訊，請參閱 [Remove-StoreMailbox](https://technet.microsoft.com/zh-tw/library/ff829913\(v=exchg.150\)) 與 [Get-MailboxStatistics](https://technet.microsoft.com/zh-tw/library/bb124612\(v=exchg.150\))。

## 如何知道這是否正常運作？

若要確認您是否已永久刪除已中斷連線的信箱和成功已清除從 Exchange 信箱資料庫，請執行下列命令。

    Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" }

如果您已順利將清除信箱，此命令將不會傳回任何結果。如果未清除信箱，此命令會傳回信箱的相關資訊。

