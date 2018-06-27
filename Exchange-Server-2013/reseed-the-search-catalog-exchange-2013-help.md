---
title: '重新植入搜尋類別目錄: Exchange 2013 Help'
TOCTitle: 重新植入搜尋類別目錄
ms:assetid: 9d873bd4-0422-4975-b5e2-82a347479115
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee633475(v=EXCHG.150)
ms:contentKeyID: 52062569
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 重新植入搜尋類別目錄

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

如果信箱資料庫副本的內容索引類別目錄損毀，則可能需要重新植入類別目錄。損毀的內容索引會依下列事件在應用程式事件記錄檔中表示。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>事件識別碼</th>
<th>層級</th>
<th>來源</th>
<th>詳細資料</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>123</p></td>
<td><p>錯誤</p></td>
<td><p>ExchangeStoreDB</p></td>
<td><p>在 &lt;<em>timestamp</em>&gt; 上，此伺服器上的 Microsoft Exchange 資訊儲存資料庫 &lt;<em>identity</em>&gt; 副本發生搜尋類別目錄損毀的情形。如需更詳細的失敗資訊，請參閱伺服器上其他 &quot;ExchangeStoreDb&quot; 和 &quot;MSExchange Search Indexer&quot; 事件的事件記錄。建議透過 'Update-MailboxDatabaseCopy' 工作重新植入該類別目錄。</p></td>
</tr>
</tbody>
</table>


如果信箱資料庫副本所在的伺服器屬於資料庫可用性群組 (DAG)，您可以從另一個 DAG 成員來重新植入內容索引類別目錄。

如果信箱資料庫副本是唯一的副本，則您必須手動建立新的內容索引類別目錄。

若要尋找與 Exchange 搜尋相關的其他管理工作，請參閱[Exchange 搜尋程序](exchange-search-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：2 分鐘。根據重新植入的內容索引類別目錄的大小，實際重新植入時間可能會有所不同。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「Exchange 搜尋」項目。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

## 信箱資料庫屬於 DAG 時重新植入內容索引類別目錄

如果信箱資料庫所在的伺服器屬於 DAG，請使用下列其中一個程序。

## 從任何來源重新植入內容索引類別目錄

此範例會從 DAG 中擁有資料庫副本的任何來源伺服器，在 Mailbox Server MBX1 上重新植入資料庫副本 DB1 的內容索引類別目錄。

    Update-MailboxDatabaseCopy -Identity DB1\MBX1 -CatalogOnly

如需詳細的語法及參數資訊，請參閱 [Update-MailboxDatabaseCopy](https://technet.microsoft.com/zh-tw/library/dd335201\(v=exchg.150\))。

## 從特定來源重新植入內容索引類別目錄

此範例會從也擁有資料庫副本的 Mailbox Server MBX2，在 Mailbox Server MBX1 上重新植入資料庫副本 DB1 的內容索引類別目錄。

    Update-MailboxDatabaseCopy -Identity DB1\MBX1 -SourceServer MBX2 -CatalogOnly

如需詳細的語法及參數資訊，請參閱 [Update-MailboxDatabaseCopy](https://technet.microsoft.com/zh-tw/library/dd335201\(v=exchg.150\))。

## 只有一個信箱資料庫副本時重新植入內部索引類別目錄

如果只有一個信箱資料庫副本，則您必須重新建立內容索引類別目錄，以手動重新植入搜尋類別目錄。

1.  執行下列命令，以停止 Microsoft Exchange 搜尋服務和 Microsoft Exchange 搜尋主控制器服務。
    
        Stop-Service MSExchangeFastSearch
    
        Stop-Service HostControllerService

2.  刪除、移動或重新命名包含 Exchange 內容索引目錄的資料夾。此資料夾名為 `%ExchangeInstallPath\Mailbox\<name of mailbox database>_Catalog\<GUID>12.1.Single`。例如，您可能重新命名資料夾 `C:\Program Files\Microsoft\Exchange Server\V15\Mailbox\Mailbox Database 0657134726_Catalog\F0627A72-9F1D-494A-839A-D7C915C279DB12.1.Single_OLD`。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>刪除此資料夾可釋出更多磁碟空間。或者，您可能想要重新命名或移動資料夾，以保留做為疑難排解用途。</td>
    </tr>
    </tbody>
    </table>


3.  執行下列命令，以重新啟動 Microsoft Exchange 搜尋服務和 Microsoft Exchange 搜尋主控制器服務。
    
        Start-Service MSExchangeFastSearch
    
        Start-Service HostControllerService
    
    重新啟動這些服務之後，Exchange 搜尋將會重建內容索引類別目錄。

## 如何才能了解這是否正常運作？

Exchange 搜尋重新植入內容索引類別目錄可能需要一些時間。執行下列命令來顯示重新植入程序的狀態。

    Get-MailboxDatabaseCopyStatus | FL Name,*Index*

當重新植入搜尋類別目錄正在進行中，*ContentIndexState* 屬性的值是**正在編目**。當重新植入完成時，這個值會變更為**狀況良好**。

