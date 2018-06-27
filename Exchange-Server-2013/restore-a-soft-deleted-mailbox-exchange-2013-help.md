---
title: '還原虛刪除信箱: Exchange 2013 Help'
TOCTitle: 還原虛刪除信箱
ms:assetid: 4f3f5ce4-9d12-4ed8-9f70-d8a6aa8a1b2e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ863435(v=EXCHG.150)
ms:contentKeyID: 50553981
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 還原虛刪除信箱

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2012-11-29_

使用命令介面來連線至 Active Directory 使用者帳戶的虛刪除信箱。信箱後會變成*虛刪除*來源信箱資料庫移至不同的信箱資料庫。移動完成後 Exchange 完全不會從來源信箱資料庫刪除信箱。而是來源信箱資料庫中的信箱會切換到虛刪除的狀態。這可讓您還原的來源信箱以防導致失敗或損毀的信箱的目的地資料庫移動期間發生錯誤。如果發生這種情況，您可以還原的來源信箱並嘗試移動一次。

虛刪除信箱保留在來源資料庫中的已刪除的信箱保留期間到期直到或**Remove-StoreMailbox**指令程式來清除虛刪除信箱。直到虛刪除信箱會永久刪除 Exchange 信箱資料庫，您可以使用命令介面中還原虛刪除信箱的內容至現有的信箱或封存信箱。

若要深入了解虛刪除信箱及執行其他相關管理工作，請參閱下列主題：

  - [中斷連線的信箱](disconnected-mailboxes-exchange-2013-help.md)

  - [連線或還原已刪除的信箱](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)

  - [管理信箱還原要求](manage-mailbox-restore-requests-exchange-2013-help.md)

  - [永久刪除信箱](permanently-delete-a-mailbox-exchange-2013-help.md)

## 開始之前有哪些須知？

  - 預估完成時間：2 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「收件者佈建權限」一節。

  - 本主題中的程序只可以在命令介面中執行。您無法使用 EAC 來還原虛刪除信箱。

  - 執行下列命令可確認您要連接使用者帳戶的虛刪除信箱仍存在信箱資料庫中，而且不是停用的信箱。
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisplayName,DisconnectReason,DisconnectDate
    
    虛刪除信箱必須存在於信箱資料庫中，而且*DisconnectReason*屬性的值已設為`SoftDeleted`。如果已經被從資料庫清除信箱，此命令將不會傳回任何結果。
    
    或者，您可以執行下列命令顯示組織中的所有虛刪除信箱。
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisconnectReason -eq "SoftDeleted" } | fl DisplayName,DisconnectReason,DisconnectDate

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

  - 有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。.

## 使用命令介面還原虛刪除的信箱

您可以使用命令介面中使用**New-MailboxRestoreRequest**指令程式以現有的信箱還原虛刪除信箱。當您還原虛刪除信箱時，其內容都會複製到現有的信箱，會呼叫*的目標信箱*。信箱還原要求已順利完成之後，要求會保留 30 天內，根據預設之前就會被刪除。您可以移除它更早使用**Remove-MailboxRestoreRequest**指令程式。

虛刪除信箱還原後，信箱會保留在信箱資料庫中，直到系統管理員將它永久刪除，或是在刪除的信箱保留期間到期時加以清除。

若要建立信箱還原要求，您必須使用的顯示名稱、 信箱的 GUID，或舊版的辨別名稱 (DN) 虛刪除信箱。使用**Get-MailboxStatistics**指令程式來顯示針對您想要還原虛刪除信箱**DisplayName**、 **MailboxGuid**，以及**LegacyDN**屬性的值。例如，執行下列命令以傳回組織中所有已停用和虛刪除信箱此資訊。

    Get-MailboxDatabase | Get-MailboxStatistics | Where {$_.DisconnectReason -eq "SoftDeleted"} | fl DisplayName,MailboxGuid,LegacyDN,Database

此範例會還原虛刪除信箱，以識別由*SourceStoreMailbox*參數中的顯示名稱以及位於 MBXDB01 信箱資料庫，名為蔡 Garcia 的目標信箱。*AllowLegacyDNMismatch*參數使用因此來源信箱可以還原至都不會有相同的傳統 DN 值作為虛刪除信箱的信箱。

    New-MailboxRestoreRequest -SourceStoreMailbox "Debra Garcia" -SourceDatabase MBXDB01 -TargetMailbox "Debra Garcia" -AllowLegacyDNMismatch

此範例會為 Pilar Pinilla 虛刪除封存信箱的信箱 GUID 識別還原至其目前的封存信箱。因為主要信箱和其對應的封存信箱有相同的傳統 DN *AllowLegacyDNMismatch*參數不必要的。

    New-MailboxRestoreRequest -SourceStoreMailbox dc35895a-a628-4bba-9aa9-650f5cdb9ae7 -SourceDatabase MBXDB02 -TargetMailbox pilarp@contoso.com -TargetIsArchive

如需詳細的語法及參數資訊，請參閱 [New-MailboxRestoreRequest](https://technet.microsoft.com/zh-tw/library/ff829875\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要確認您已順利已還原虛刪除信箱的目標信箱，執行**Get-MailboxRestoreRequest**指令程式或**Get-MailboxRestoreRequestStatistics**指令程式來顯示資訊的還原要求。如果已成功建立的還原要求， *Status*屬性都有**Queued**、 **InProgress**或**Completed**的值。完成的還原要求之後，從虛刪除信箱內容出現在目標信箱。

如需相關資訊，請參閱：

  - [管理信箱還原要求](manage-mailbox-restore-requests-exchange-2013-help.md)

  - [Get-MailboxRestoreRequest](https://technet.microsoft.com/zh-tw/library/ff829907\(v=exchg.150\))

  - [Get-MailboxRestoreRequestStatistics](https://technet.microsoft.com/zh-tw/library/ff829912\(v=exchg.150\))

