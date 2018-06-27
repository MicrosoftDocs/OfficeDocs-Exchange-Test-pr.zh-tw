---
title: '設定信箱資料庫複本的啟動原則: Exchange 2013 Help'
TOCTitle: 設定信箱資料庫複本的啟動原則
ms:assetid: 6b37ed6e-2e36-4688-b485-8fdbb8193ec8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd298046(v=EXCHG.150)
ms:contentKeyID: 50473400
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定信箱資料庫複本的啟動原則

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-11-02_

*啟用*會變更作用中副本的被動副本從信箱資料庫複本的程序。啟用自動發生系統為資料庫或伺服器的容錯移轉作業的一部分並它可以手動由管理員執行資料庫或伺服器轉換作業的一部分。封鎖的資料庫進行啟用防止從資料庫或伺服器容錯移轉期間變成作用中副本。

要尋找與信箱資料庫副本相關的其他管理工作嗎？請參閱[管理信箱資料庫副本](managing-mailbox-database-copies-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 完成這項工作預估時間： 1 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [高可用性和站台回復性權限](high-availability-and-site-resilience-permissions-exchange-2013-help.md)主題中的「信箱資料庫副本」項目。

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

## 使用 EAC 設定信箱資料庫副本的啟動原則

1.  
    
    在 EAC 中，移至 \[伺服器\] \> \[資料庫\]。

2.  選取想要設定的資料庫。

3.  
    
    在 \[詳細資料\] 窗格的 \[資料庫副本\] 下方，找出想要設定的資料庫副本，然後按一下 \[擱置\]。

4.  可選擇性加入備註，然後選取 \[此副本僅能以手動操作方式啟動\] 核取方塊。

5.  按一下 \[儲存\]，以儲存信箱資料庫副本的組態變更。

## 使用命令介面擱置或繼續啟動資料庫副本

此範例會在伺服器 MBX2 上封鎖啟動資料庫 DB1 的副本。

    Suspend-MailboxDatabaseCopy -Identity DB1\MBX2 -ActivationOnly

此範例會在伺服器 MBX2 上繼續啟動資料庫 DB1 的副本。

    Resume-MailboxDatabaseCopy -Identity DB1\MBX2

如需詳細的語法及參數資訊，請參閱 [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/zh-tw/library/dd351074\(v=exchg.150\)) 或 [Resume-MailboxDatabaseCopy](https://technet.microsoft.com/zh-tw/library/dd335220\(v=exchg.150\))。

## 使用命令介面設定伺服器的啟動原則

此範例會將伺服器 MBX2 上的資料庫副本設定為封鎖啟動。

    Set-MailboxServer -Identity MBX2 -DatabaseCopyAutoActivationPolicy Blocked

此範例會將伺服器 MBX3 上的資料庫副本設定為封鎖站台外部啟動。

    Set-MailboxServer -Identity MBX3 -DatabaseCopyAutoActivationPolicy IntrasiteOnly

此範例會將伺服器 MBX4 上的資料庫副本設定為解除封鎖啟動。

    Set-MailboxServer -Identity MBX4 -DatabaseCopyAutoActivationPolicy Unrestricted

如需詳細的語法及參數資訊，請參閱 [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/zh-tw/library/dd351074\(v=exchg.150\))、[Resume-MailboxDatabaseCopy](https://technet.microsoft.com/zh-tw/library/dd335220\(v=exchg.150\)) 或 [Set-MailboxServer](https://technet.microsoft.com/zh-tw/library/aa998651\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要確認是否已成功設定啟動原則，請執行下列其中一項操作：

  - 在命令介面中，執行以下命令來驗證資料庫副本的啟動設定。
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List ActivationSuspended

  - 在命令介面中，執行以下命令來驗證 DAG 成員的啟動設定。
    
        Get-MailboxServer <ServerName> | Format-List DatabaseCopyAutoActivationPolicy

