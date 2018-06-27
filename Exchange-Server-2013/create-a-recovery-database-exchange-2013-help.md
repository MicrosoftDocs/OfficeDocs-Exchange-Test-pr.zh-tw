---
title: '建立復原資料庫: Exchange 2013 Help'
TOCTitle: 建立復原資料庫
ms:assetid: 34d87491-b7b7-44a9-8d69-e1a9c1fe5852
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee332321(v=EXCHG.150)
ms:contentKeyID: 50472951
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 建立復原資料庫

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2013-01-21_

您可以使用命令介面來建立復原資料庫，一種特殊的信箱資料庫是用以裝載並解壓縮資料中的已還原的資料庫復原作業的一部分。建立復原資料庫之後，您可以復原或已還原的信箱資料庫移到復原資料庫，並再使用[New-MailboxRestoreRequest](https://technet.microsoft.com/zh-tw/library/ff829875\(v=exchg.150\)) cmdlet 可從復原資料庫擷取資料。擷取、 之後將資料可以然後匯出至資料夾或合併到現有的信箱。使用復原資料庫，您可以資料從備份或復原資料庫複本而不干擾使用者存取目前資料。

要尋找復原資料庫相關的其他管理工作嗎？取出[復原資料庫](recovery-databases-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 完成這項工作預估時間： 1 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的 「 信箱復原 」 項目。

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


## 使用命令介面來建立復原資料庫

此範例會在信箱伺服器 MBX2 上建立復原資料庫 RDB1。

    New-MailboxDatabase -Recovery -Name RDB1 -Server MBX2

此範例會使用資料庫檔案和記錄檔資料夾的自訂路徑，在信箱伺服器 MBX1 上建立復原資料庫 RDB2。

    New-MailboxDatabase -Recovery -Name RDB2 -Server MBX1 -EdbFilePath "C:\Recovery\RDB2\RDB2.EDB" -LogFolderPath "C:\Recovery\RDB2"

如需詳細的語法及參數資訊，請參閱 [New-MailboxDatabase](https://technet.microsoft.com/zh-tw/library/aa997976\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要確認是否已成功建立復原資料庫，請執行下列其中一項操作：

  - 在命令介面中，執行下列命令以顯示復原資料庫的設定資訊。
    
        Get-MailboxDatabase <RecoveryDatabaseName> | Format-List

## 其他工作

建立復原資料庫之後，您可能也想要使用復原資料庫還原資料。如需詳細步驟，請參閱[使用復原資料庫還原資料](restore-data-using-a-recovery-database-exchange-2013-help.md)。

