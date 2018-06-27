---
title: '取得可復原的項目資料夾統計資料: Exchange 2013 Help'
TOCTitle: 取得可復原的項目資料夾統計資料
ms:assetid: dee77958-ee87-4908-85e4-ad053bacd8b0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ff714343(v=EXCHG.150)
ms:contentKeyID: 52062602
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 取得可復原的項目資料夾統計資料

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-01-22_

\[可復原的項目\] 資料夾包含刪除由 Microsoft Outlook和 Microsoft OfficeOutlook Web App使用者或信箱助理員的項目。期間已刪除的項目保留在此資料夾中為基礎的信箱資料庫或信箱設定已刪除的項目保留設定。根據預設，信箱資料庫設定為 14 天內，保留已刪除的項目，並可復原的項目警告配額及配額可復原的項目會設為 20 gb 和 30 GB 分別。不過，如果就地保留或訴訟資料暫留功能已啟用信箱，可復原的項目資料夾可以累計刪除超過指定的保留期限的項目，而且也可維持不同版本之已修改的信箱項目。

當 \[可復原的項目\] 資料夾達到可復原的項目警告配額時，警告事件會記錄於應用程式事件記錄檔。如果信箱不在訴訟暫止狀態，會再中第一個出 (FIFO) 為基礎的第一次移除項目。不過，如果信箱處於訴訟暫止狀態、 信箱永遠不會清空並定即將達到可復原的項目配額，影響信箱功能。

因此，務必監視提醒信箱達到可復原的項目配額時所產生的事件記錄檔。您也可以使用此程序可報告統計資料的 \[可復原的項目\] 資料夾中，特別是針對信箱處於訴訟暫止狀態。

若要深入了解，請參閱下列主題：

  - [可復原的項目資料夾](recoverable-items-folder-exchange-2013-help.md)

  - [就地保留與訴訟暫止](in-place-hold-and-litigation-hold-exchange-2013-help.md)

## 開始之前有哪些須知？

  - 預估完成時間：1 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的 「 信箱資料夾 」 項目。

  - 您無法使用 Exchange 系統管理中心 (EAC) 來取得信箱可復原的項目資料夾統計資料。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

## 您要執行的工作

## 取得可復原的項目資料夾統計資料的信箱

本範例會取得 Soumya Singhi \[可復原的項目\] 資料夾的資料夾統計資料，並以清單格式顯示輸出。

    Get-MailboxFolderStatistics -Identity "Soumya Singhi" -FolderScope RecoverableItems | Format-List

本範例會取得 Soumya Singhi \[可復原的項目\] 資料夾的資料夾統計資料和資料夾與資料夾大小以表格格式顯示資料夾名稱、 資料夾路徑、 的項目數。

    Get-MailboxFolderStatistics -Identity "Soumya Singhi" -FolderScope RecoverableItems | Format-Table Name,FolderPath,ItemsInFolder,FolderAndSubfolderSize

如需詳細的語法及參數資訊，請參閱[Get-MailboxFolderStatistics](https://technet.microsoft.com/zh-tw/library/aa996762\(v=exchg.150\))。

## 取得在訴訟暫止狀態的所有信箱的可復原的項目資料夾統計資料

此範例會擷取所有信箱處於訴訟暫止狀態的清單並擷取可復原的項目\] 資料夾的信箱資料夾統計資料和每個信箱及其子資料夾。**Identity** (信箱資料夾 identity) 和**FolderAndSubfolderSize**屬性會以表格格式顯示。

    Get-Mailbox -ResultSize Unlimited -Filter {LitigationHoldEnabled -eq $true} | Get-MailboxFolderStatistics | Format-Table Identity,FolderAndSubfolderSize

如需詳細的語法及參數資訊，請參閱[Get-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123685\(v=exchg.150\))和[Get-MailboxFolderStatistics](https://technet.microsoft.com/zh-tw/library/aa996762\(v=exchg.150\))。

## 取得可復原的項目配額的信箱

本範例會顯示配額和警告配額以供使用者信箱 \[可復原的項目\] 資料夾。此範例也會擷取是否訴訟暫止狀態或就地保留所在之信箱的相關資訊。

    Get-Mailbox -Identity <identity of mailbox> | Format-List RecoverableItems*,LitigationHoldEnabled,InPlaceHolds

本範例會顯示您組織中的配額和警告配額的所有使用者信箱 \[可復原的項目\] 資料夾。此範例也會擷取保留資訊。

    Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -eq "UserMailbox"} | Format-List Name,RecoverableItems*,LitigationHoldEnabled,InPlaceHolds

