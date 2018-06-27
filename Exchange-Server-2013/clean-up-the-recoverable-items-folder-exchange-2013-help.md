---
title: '清除 資料夾: Exchange 2013 Help'
TOCTitle: 清除 資料夾
ms:assetid: 82c310f8-de2f-46f2-8e1a-edb6055d6e69
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ff678798(v=EXCHG.150)
ms:contentKeyID: 50554018
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 清除 資料夾

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-09-30_

（此主題適用於Exchange系統管理員的）。

可復原的項目\] 資料夾 (較早版本的Exchange做為已知*暫放*) 存在於防止意外或惡意刪除及探索努力常已採取之前或期間訴訟暫止或調查。若要深入了解可復原的項目\] 資料夾，請參閱[可復原的項目資料夾](recoverable-items-folder-exchange-2013-help.md)。

清除使用者的信箱中 \[可復原的項目\] 資料夾的方式而定信箱處於就地保留或訴訟資料暫留狀態，還是必須啟用單一項目復原：

  - 如果信箱不處於就地保留或訴訟暫止狀態或都不會有已啟用單一項目復原，則您只可以從 \[可復原的項目\] 資料夾刪除項目。之後會刪除您無法復原的項目使用單一項目復原。

  - 如果信箱處於就地保留或訴訟暫止狀態或擁有單一項目復原已啟用，務必要等到移除保留或單一項目復原已停用保留信箱資料。在此例中，您需要執行清理 \[可復原的項目\] 資料夾的詳細的步驟。

若要深入了解就地保留和訴訟暫止狀態，請參閱[就地保留與訴訟暫止](in-place-hold-and-litigation-hold-exchange-2013-help.md)。若要深入了解單一項目復原，請參閱[可復原的項目資料夾](recoverable-items-folder-exchange-2013-help.md)中的 「 單一項目復原 」。

若要深入了解可復原的項目\] 資料夾，請參閱[可復原的項目資料夾](recoverable-items-folder-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 完成此程序預估時間： 30 分鐘。這可能會根據 \[可復原的項目\] 資料夾的大小而有所不同

  - 您必須被指派下列管理角色，才能使用**Search-Mailbox**指令程式來搜尋並刪除使用者信箱中的郵件。
    
      - **信箱搜尋：**這個角色可讓您在組織中的多個信箱之間搜尋郵件。根據預設，系統管理員不會被指派這個角色。若要指派此角色給自己以便搜尋信箱，請將您自己增加為「探索管理」角色群組的成員。請參閱[Exchange 中指派 eDiscovery 權限](assign-ediscovery-permissions-in-exchange-exchange-2013-help.md)。
    
      - **信箱匯入 / 匯出**  此角色可讓您刪除使用者信箱的郵件。根據預設，此角色不被指派給任何角色群組。若要刪除的郵件從使用者的信箱，您可以將信箱匯入 / 匯出角色新增至組織管理角色群組。如需詳細資訊，請參閱 「 將角色新增至角色群組 」 一節中[管理角色群組](manage-role-groups-exchange-2013-help.md) 。

  - 因為不正確地清除 \[可復原的項目\] 資料夾可能會導致資料遺失，務必您已熟悉可復原的項目\] 資料夾及移除其內容的影響。之前執行此程序，我們建議您檢閱[可復原的項目資料夾](recoverable-items-folder-exchange-2013-help.md)中的資訊。

  - 您無法使用 Exchange 系統管理中心 (EAC) 來執行這些程序。您必須使用命令介面。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

## 使用命令介面來刪除不處於保留狀態或不需要啟用單一項目復原信箱 \[可復原的項目\] 資料夾中項目

本範例會永久刪除 Gurinder Singh \[可復原的項目\] 資料夾中的項目和也將項目複製到探索搜尋信箱 （ Exchange安裝程式所建立的探索信箱） 的 GurinderSingh RecoverableItems 資料夾。

    Search-Mailbox -Identity "Gurinder Singh" -SearchDumpsterOnly -TargetMailbox "Discovery Search Mailbox" -TargetFolder "GurinderSingh-RecoverableItems" -DeleteContent

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要刪除信箱中的項目而不將其複製到另一個信箱，使用不含<em>TargetMailbox</em>和<em>TargetFolder</em>參數以上的命令。</td>
</tr>
</tbody>
</table>


如需詳細的語法及參數資訊，請參閱 [Search-Mailbox](https://technet.microsoft.com/zh-tw/library/dd298173\(v=exchg.150\))。

## 使用命令介面來清除保留或已啟用單一項目復原信箱 \[可復原的項目\] 資料夾

如果信箱達到其可復原的項目配額，我們建議您引發配額及未從資料夾刪除項目。您也可以監視可復原的項目警告配額與相關的應用程式記錄檔中的事件，並採取 （例如引發配額或調查達到警告配額的信箱 \[可復原的項目\] 資料夾的增長） 的必要動作。

如果存放區的條件約束或類似問題阻止您引發的可復原的項目配額，且您需要從就地保留或訴訟暫止狀態的信箱 \[可復原的項目\] 資料夾刪除訊息或具有單一項目復原已啟用，我們建議的您先資料從使用者的可復原的項目資料夾複製至另一個信箱。如果您正在刪除因為一個磁碟區上的儲存限制的項目，您可以將項目複製到信箱位於上有足夠的儲存磁碟區中。

此程序會將項目從 Gurinder Singh \[可復原的項目\] 資料夾複製到探索搜尋信箱中的 \[GurinderSingh RecoverableItems\] 資料夾。複製並從 \[可復原的項目\] 資料夾刪除項目之前，您必須先執行數個步驟以確定未從 \[可復原的項目\] 資料夾刪除項目。將項目複製到探索或備份信箱並清除資料夾之後，您可以回復到信箱的先前的設定。

1.  擷取下列配額設定。請務必注意值，則可以回復這些設定之後清除 \[可復原的項目\] 資料夾：
    
      - *RecoverableItemsQuota*
    
      - *RecoverableItemsWarningQuota*
    
      - *ProhibitSendQuota*
    
      - *ProhibitSendReceiveQuota*
    
      - *UseDatabaseQuotaDefaults*
    
      - *RetainDeletedItemsFor*
    
      - *UseDatabaseRetentionDefaults*
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果<em>UseDatabaseQuotaDefaults</em>參數設為<code>$true</code>，不會套用先前的配額設定。在信箱資料庫上設定相對應的配額設定會套用，即使個別信箱設定會填入。</td>
    </tr>
    </tbody>
    </table>
    
        Get-Mailbox "Gurinder Singh" | Format-List RecoverableItemsQuota, RecoverableItemsWarningQuota, ProhibitSendQuota, ProhibitSendReceiveQuota, UseDatabaseQuotaDefaults, RetainDeletedItemsFor, UseDatabaseRetentionDefaults

2.  擷取信箱的信箱存取設定。請務必注意這些設定的更新版本。
    
        Get-CASMailbox "Gurinder Singh" | Format-List EwsEnabled, ActiveSyncEnabled, MAPIEnabled, OWAEnabled, ImapEnabled, PopEnabled

3.  擷取目前可復原的項目\] 資料夾的大小。讓您可以引發的配額步驟 6 中記下大小。
    
        Get-MailboxFolderStatistics "Gurinder Singh" -FolderScope RecoverableItems | Format-List Name,FolderAndSubfolderSize

4.  擷取目前的受管理的資料夾助理員工作週期設定。請務必注意供日後的設定。
    
        Get-MailboxServer "My Mailbox Server" | Format-List Name,ManagedFolderWorkCycle

5.  停用用戶端的信箱存取權以確保可以此程序期間信箱資料進行任何變更。
    
        Set-CASMailbox "Gurinder Singh" -EwsEnabled $false -ActiveSyncEnabled $false -MAPIEnabled $false -OWAEnabled $false -ImapEnabled $false -PopEnabled $false

6.  若要確定會從 \[可復原的項目\] 資料夾刪除任何項目，增加可復原的項目配額、 增加的可復原的項目警告配額，並值設為已刪除的項目保留期間高於目前使用者的 \[可復原的項目\] 資料夾的大小。這是特別重要的保留信箱處於就地保留和訴訟暫止狀態的訊息。我們建議引發這些設定到其目前大小的兩倍。
    
        Set-Mailbox "Gurinder Singh" -RecoverableItemsQuota 50Gb -RecoverableItemsWarningQuota 50Gb -RetainDeletedItemsFor 3650 -ProhibitSendQuota 50Gb -ProhibitSendRecieveQuota 50Gb -UseDatabaseQuotaDefaults $false -UseDatabaseRetentionDefaults $false

7.  停用受管理的資料夾助理員 Mailbox server 上。
    
        Set-MailboxServer MyMailboxServer -ManagedFolderWorkCycle $null
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果信箱位於信箱資料庫上的資料庫可用性群組 (DAG) 中，您必須停用受管理的資料夾助理員裝載資料庫副本的每個 DAG 成員上。如果資料庫容錯移轉至另一部伺服器，這可防止受管理的資料夾助理員該伺服器上刪除信箱資料。</td>
    </tr>
    </tbody>
    </table>


8.  停用單一項目復原並移除信箱訴訟暫止狀態。
    
        Set-Mailbox "Gurinder Singh" -SingleItemRecoveryEnabled $false -LitigationHoldEnabled $false
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>執行此命令之後，可能需要一小時停用單一項目復原或訴訟暫止狀態。我們建議您在此期間經過之後才執行下一個步驟。</td>
    </tr>
    </tbody>
    </table>


9.  將項目從 \[可復原的項目\] 資料夾複製到 \[探索搜尋信箱中的資料夾及刪除來源信箱中的內容。
    
        Search-Mailbox -Identity "Gurinder Singh" -SearchDumpsterOnly -TargetMailbox "Discovery Search Mailbox" -TargetFolder "GurinderSingh-RecoverableItems" -DeleteContent
    
    如果您需要刪除符合指定的條件的郵件，請使用*SearchQuery*參數以指定的條件。此範例會刪除 \[**主旨**\] 欄位中含有"Your bank statement"字串的郵件。
    
        Search-Mailbox -Identity "Gurinder Singh" -SearchQuery "Subject:'Your bank statement'" -SearchDumpsterOnly -TargetMailbox "Discovery Search Mailbox" -TargetFolder "GurinderSingh-RecoverableItems" -DeleteContent
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>它不被必要項目複製到 [探索搜尋信箱。您可以將郵件複製到任何信箱。不過，若要防止敏感性信箱資料存取，建議將郵件複製到已授權的記錄管理員限制存取的信箱。根據預設，預設探索搜尋信箱存取僅限於至探索管理角色群組的成員。如需詳細資訊，請參閱<a href="in-place-ediscovery-exchange-2013-help.md">就地 eDiscovery</a>。</td>
    </tr>
    </tbody>
    </table>


10. 如果信箱處於訴訟暫止狀態或鎖稍早啟用單一項目復原，重新啟用這些功能。
    
        Set-Mailbox "Gurinder Singh" -SingleItemRecoveryEnabled $true -LitigationHoldEnabled $true
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>執行此命令之後，可能需要一小時啟用單一項目復原] 或 [訴訟暫止狀態。建議您啟用受管理的資料夾助理員並允許用戶端存取 （步驟 11 和 12） 只是在這之後經過期間。</td>
    </tr>
    </tbody>
    </table>


11. 將回復為步驟 1 中記下值的下列配額：
    
      - *RecoverableItemsQuota*
    
      - *RecoverableItemsWarningQuota*
    
      - *ProhibitSendQuota*
    
      - *ProhibitSendReceiveQuota*
    
      - *UseDatabaseQuotaDefaults*
    
      - *RetainDeletedItemsFor*
    
      - *UseDatabaseRetentionDefaults*
    
    在這個範例中，從保留移除信箱、 刪除項目保留期間屬性重設為預設值為 14 天，和可復原的項目配額設定成使用相同的值做為信箱資料庫。如果您在步驟 1 中記下的值不同，您必須使用上述參數指定每個值並將*UseDatabaseQuotaDefaults*參數設為`$false`。如果*RetainDeletedItemsForand UseDatabaseRetentionDefaults*參數先前已設為不同的值，則也必須回復這些步驟 1 中記下的值。
    
        Set-Mailbox "Gurinder Singh" -RetentionHoldEnabled $false -RetainDeletedItemsFor 14 -RecoverableItemsQuota unlimited -UseDatabaseQuotaDefaults $true

12. 啟用受管理的資料夾助理員將工作週期後述步驟 4 的值。本範例會將一天的工作週期。
    
        Set-MailboxServer MyMailboxServer -ManagedFolderWorkCycle 1

13. 啟用用戶端存取。
    
        Set-CASMailbox -ActiveSyncEnabled $true -EwsEnabled $true -MAPIEnabled $true -OWAEnabled $true -ImapEnabled $true -PopEnabled $true

如需詳細的語法及參數資訊，請參閱下列主題：

  - [Get-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123685\(v=exchg.150\))

  - [Get-CASMailbox](https://technet.microsoft.com/zh-tw/library/bb124754\(v=exchg.150\))

  - [Get-MailboxFolderStatistics](https://technet.microsoft.com/zh-tw/library/aa996762\(v=exchg.150\))

  - [Get-MailboxServer](https://technet.microsoft.com/zh-tw/library/bb123539\(v=exchg.150\))

  - [Set-CASMailbox](https://technet.microsoft.com/zh-tw/library/bb125264\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\))

  - [Set-MailboxServer](https://technet.microsoft.com/zh-tw/library/aa998651\(v=exchg.150\))

  - [Search-Mailbox](https://technet.microsoft.com/zh-tw/library/dd298173\(v=exchg.150\))

## 如何知道這是否正常運作？

若要確認您已順利清除向上信箱 \[可復原的項目\] 資料夾，請使用[Get-MailboxFolderStatistics](https://technet.microsoft.com/zh-tw/library/aa996762\(v=exchg.150\))指令程式\] 核取 \[可復原的項目\] 資料夾的大小。

此範例會擷取可復原的項目\] 資料夾的大小和及其子資料夾和項目計數資料夾與每一個子資料夾中。

    Get-MailboxFolderStatistics -Identity "Gurinder Singh" -FolderScope RecoverableItems | Format-Table Name,FolderAndSubfolderSize,ItemsInFolderAndSubfolders -Auto

