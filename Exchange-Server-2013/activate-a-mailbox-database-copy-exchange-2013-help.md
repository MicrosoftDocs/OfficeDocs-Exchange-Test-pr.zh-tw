---
title: '啟動信箱資料庫副本: Exchange 2013 Help'
TOCTitle: 啟動信箱資料庫副本
ms:assetid: d948269b-c902-4d8d-8c2b-269473359baa
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee364750(v=EXCHG.150)
ms:contentKeyID: 50474364
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟動信箱資料庫副本

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-11-01_

在啟動信箱資料庫副本是指定特定的被動副本作為新的作用中信箱資料庫複本的程序。此程序稱為*資料庫轉換*。資料庫轉換涉及卸載目前使用中資料庫及指定為新的作用中信箱資料庫副本的伺服器上掛載資料庫副本。將成為作用中信箱資料庫的資料庫副本必須正常且目前。

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

## 使用 EAC 來移動使用中信箱資料庫

1.  在 EAC 中，移至 \[伺服器\] \> \[資料庫\]。

2.  選取您要啟動的副本的資料庫。

3.  在 \[詳細資料\] 窗格中，**資料庫副本**下按一下 \[**啟動**下您要啟動的資料庫副本。

4.  按一下 \[**是\]**以啟動資料庫副本。

## 使用命令介面來移動使用中信箱資料庫

本範例會啟動並在 mbx3 上做為新的作用中信箱資料庫裝載 DB4 主控之資料庫的複本。此命令建立的 DB4 新的作用中信箱資料庫，並且它不會覆寫在 mbx3 上的資料庫裝載撥號對應表設定。

    Move-ActiveMailboxDatabase DB4 -ActivateOnServer MBX3 -MountDialOverride:None

本範例會執行轉換的 Mailbox server MBX1 DB2 資料庫。當命令完成時，MBX1 主控 DB2 的主動副本。因為*MountDialOverride*參數設為`None`，MBX1 會裝載資料庫使用其本身定義的資料庫自動裝載撥號對應表設定。

    Move-ActiveMailboxDatabase DB2 -ActivateOnServer MBX1 -MountDialOverride:None

本範例會執行轉換的信箱伺服器 mbx3 上資料庫 DB1。當命令完成時，mbx3 上主控 DB1 的主動副本。因為*MountDialOverride*參數會指定值為`Good Availability`、 mbx3 上裝載資料庫使用自動裝載資料庫的*GoodAvailability*設定撥號對應表。

    Move-ActiveMailboxDatabase DB1 -ActivateOnServer MBX3 -MountDialOverride:GoodAvailability

本範例會將資料庫 DB3 切換至信箱伺服器 MBX4。命令完成時，MBX4 將主控 DB3 的主動複本。由於未指定 *MountDialOverride* 參數，因此 MBX4 會使用 *Lossless* 的資料庫自動裝載撥號設定裝載該資料庫。

    Move-ActiveMailboxDatabase DB3 -ActivateOnServer MBX4

本範例執行名為 MBX1 之信箱伺服器的伺服器轉換。在一或多個其他信箱伺服器 (擁有 MBX1 上健全的主動資料庫複本) 上，將啟動 MBX1 上所有主動信箱資料庫複本。

    Move-ActiveMailboxDatabase -Server MBX1

本範例會執行轉換的信箱伺服器 MBX5 DB4 資料庫。在這個範例中，資料庫副本 MBX5 上的會有超過 6 的重新顯示佇列。因此， *SkipLagChecks*參數必須指定啟動 MBX5 上的資料庫副本。

    Move-ActiveMailboxDatabase DB4 MBX5 -SkipLagChecks

本範例會執行轉換的信箱伺服器 MBX6 DB5 資料庫。在這個範例中，在 MBX6 資料庫副本具有失敗*ContentIndexState* 。因此， *SkipClientExperienceChecks*參數必須指定啟動 MBX6 上的資料庫副本。

    Move-ActiveMailboxDatabase DB5 MBX6 -SkipClientExperienceChecks

## 如何知道這是否正常運作？

若要確認您是否已成功啟動信箱資料庫複本，請執行下列其中一項：

  - 在 EAC 中，瀏覽至 \[伺服器\] \> \[資料庫\]。  選擇適當的資料庫，並在 \[詳細資料\] 窗格中檢視資料庫複本屬性。

  - 在命令介面中，執行下列指令以顯示資料庫副本的狀態資訊。
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List

## 相關資訊

[信箱資料庫副本](mailbox-database-copies-exchange-2013-help.md)

[設定信箱資料庫副本屬性](configure-mailbox-database-copy-properties-exchange-2013-help.md)

