---
title: '啟用或停用單一項目復原的信箱: Exchange Online Help'
TOCTitle: 啟用或停用單一項目復原的信箱
ms:assetid: 2e7f1bcd-8395-45ad-86ce-22868bd46af0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee633460(v=EXCHG.150)
ms:contentKeyID: 54652554
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟用或停用單一項目復原的信箱

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2015-03-13_

您可以使用命令介面啟用或停用信箱上的單一項目復原。在Exchange Online、 單一項目復原預設會啟用時建立新的信箱。在Exchange 2013、 單一項目復原已停用信箱建立時。如果已啟用單一項目復原，直到刪除項目保留期間到期永久刪除 （清除） 會在使用者的郵件會保留信箱 \[可復原的項目\] 資料夾中。這可讓管理員復原已刪除的項目保留期間到期之前清除由使用者的郵件。此外，如果使用者或程序來變更一則訊息，原始項目的複本時，會也保留啟用單一項目復原。

## 開始之前有哪些須知？

  - 預估完成時間： 2 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中 「 保留與法律保留 」 項目。

  - 您無法使用 Exchange 系統管理中心 (EAC) 來啟用或停用單一項目復原。

  - 在Exchange Online、 刪除項目保留期間是設為 14 天預設。您可以變更此設定最大值為 30 天。如需詳細資訊，請參閱[Exchange Online 信箱之保留時間變更多久永久刪除項目](https://technet.microsoft.com/zh-tw/library/dn163584\(v=exchg.150\))

  - 在Exchange 2013，信箱會使用預設的信箱資料庫刪除項目保留設定。針對信箱資料庫的刪除項目保留期間設為 14 天，但您可以透過設定此設定每個信箱為基礎來覆寫預設值。如需詳細資訊，請參閱[設定已刪除的項目保留及可復原的項目配額](configure-deleted-item-retention-and-recoverable-items-quotas-exchange-2013-help.md)。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。.

## 使用命令介面來啟用單一項目復原

此範例會啟用之信箱的年 4 月獵單一項目復原。

    Set-Mailbox -Identity "April Summers" -SingleItemRecoveryEnabled $true

此範例會啟用單一項目復原之信箱的 Pilar Pinilla 並設定為 30 天保留天數已刪除的項目。

    Set-Mailbox -Identity "Pilar Pinilla" -SingleItemRecoveryEnabled $true -RetainDeletedItemsFor 30

本範例會讓組織中的所有使用者信箱的單一項目復原。

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'UserMailbox')} | Set-Mailbox -SingleItemRecoveryEnabled $true

此範例會啟用組織中設定的天數刪除項目都會保留為 30 天的所有使用者信箱的單一項目復原

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'UserMailbox')} | Set-Mailbox -SingleItemRecoveryEnabled $true -RetainDeletedItemsFor 30

如需詳細的語法及參數資訊，請參閱 [Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\))。

## 使用命令介面來停用單一項目復原

您可能需要停用單一項目復原使用者的信箱。例如，您可以使用**Search-Mailbox –DeleteContent**永久刪除信箱中的內容之前，您必須停用單一項目復原。如需詳細資訊，請參閱[搜尋並刪除郵件 - 管理中心說明](search-for-and-delete-messages-admin-help-exchange-2013-help.md)。

本範例會停用單一項目復原 Ayla Kol 信箱。

    Set-Mailbox -Identity "Ayla Kol" -SingleItemRecoveryEnabled $false

## 如何知道這是否正常運作？

若要確認您已啟用單一項目復原的信箱並顯示 \[刪除的項目 （以天數） 的保留期限的值，請執行下列命令。

    Get-Mailbox <Name> | FL SingleItemRecoveryEnabled,RetainDeletedItemsFor

您可以使用這個相同的命令來確認單一項目復原已停用信箱。

## 其他資訊

  - 若要深入了解單一項目復原，請參閱[可復原的項目資料夾](recoverable-items-folder-exchange-2013-help.md)。若要復原之使用者所清除之前已刪除的項目保留期間的郵件到期，請參閱[復原刪除的郵件使用者的信箱](recover-deleted-messages-in-a-user-s-mailbox-exchange-2013-help.md)。

  - 如果信箱處於就地保留或訴訟資料暫留功能，可復原的項目\] 資料夾中的郵件會保留直到保留期間到期。若無限制保留持續時間，則會保留項目，直到移除保留或變更的保留期間。

