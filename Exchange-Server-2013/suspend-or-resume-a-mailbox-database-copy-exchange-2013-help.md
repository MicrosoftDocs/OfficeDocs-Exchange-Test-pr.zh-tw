---
title: '擱置或恢復信箱資料庫副本: Exchange 2013 Help'
TOCTitle: 擱置或恢復信箱資料庫副本
ms:assetid: 96aa1b82-3e15-4215-843e-3d583af9504b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd298159(v=EXCHG.150)
ms:contentKeyID: 50473780
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 擱置或恢復信箱資料庫副本

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-11-02_

您可能需要暫停或繼續資料庫副本的原因，例如磁碟包含資料庫副本，維護各種或暫止的災害復原用途啟用從個別的資料庫副本。

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

## 使用 EAC 來擱置信箱資料庫副本

1.  在 EAC 中，移至 \[伺服器\] \> \[資料庫\]。

2.  選取您想要暫停的副本的資料庫。

3.  在 \[詳細資料\] 窗格中的 \[**資料庫副本**，按一下 \[**擱置**下您想要暫停的資料庫副本。

4.  在 \[**註解**\] 欄位中加入指定的暫停原因的最多 512 個字元的選擇性註解。

5.  若要擱置資料庫副本從自動啟動，請選取 \[**手動介入僅即可啟用此複本**\] 核取方塊。

6.  按一下 \[**儲存**\] 以擱置資料庫副本。

## 使用 EAC 來繼續傳送的信箱資料庫副本

1.  在 EAC 中，移至 \[伺服器\] \> \[資料庫\]。

2.  選取您要繼續執行其複本的資料庫。

3.  在 \[詳細資料\] 窗格中 \[**資料庫副本**，按一下 \[**繼續**下您想要繼續資料庫副本。

4.  按一下 \[**是\]**以繼續資料庫副本。

## 使用命令介面來擱置信箱資料庫副本

此範例會擱置副本 DB1 的 mailbox server MBX1 上主控之資料庫的連續複寫。也已指定選用的註解。

    Suspend-MailboxDatabaseCopy -Identity DB1\MBX1 -SuspendComment "Maintenance on MBX1" -Confirm:$False

此範例會擱置伺服器 MBX2 主控 DB2 之資料庫的副本啟用。

    Suspend-MailboxDatabaseCopy -Identity DB2\MBX2 -ActivationOnly -Confirm:$False

## 使用命令介面來繼續信箱資料庫副本

此範例會繼續的 mailbox server MBX1 上資料庫 DB1 的複本。

    Resume-MailboxDatabaseCopy -Identity DB1\MBX1

此範例會繼續資料庫副本的 DB2 只複寫伺服器 MBX2 上。

    Resume-MailboxDatabaseCopy -Identity DB2\MBX2 -ReplicationOnly

## 如何知道這是否正常運作？

若要確認您已成功擱置或恢復信箱資料庫複本，請執行下列其中一項：

  - 在 EAC 中，瀏覽至 \[伺服器\] \> \[資料庫\]。  選擇適當的資料庫，並在 \[詳細資料\] 窗格中檢視資料庫複本屬性。

  - 在命令介面中，執行下列指令以顯示資料庫副本的狀態資訊。
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List

