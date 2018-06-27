---
title: '新增信箱資料庫副本: Exchange 2013 Help'
TOCTitle: 新增信箱資料庫副本
ms:assetid: 784bf48f-8af5-422c-a63f-2f01fc0cf151
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd298080(v=EXCHG.150)
ms:contentKeyID: 50473558
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 新增信箱資料庫副本

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-30_

當您新增信箱資料庫複本時，連續複寫會自動啟用現有的資料庫和資料庫副本之間。資料庫副本自動指派給 identity 的格式為 \<*DatabaseName*\> \\ \<*HostMailboxServerName*\>。例如，伺服器 MBX3 裝載 DB1 的複本是資料庫的 DB1\\MBX3。

要尋找與信箱資料庫副本相關的其他管理工作嗎？請參閱[管理信箱資料庫副本](managing-mailbox-database-copies-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 完成這項工作預估時間： 2 分鐘，加上的時間來植入資料庫副本，這取決於在各種因素，如資料庫、 速度、 可用頻寬和延遲的網路、 大小和儲存速度。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [高可用性和站台回復性權限](high-availability-and-site-resilience-permissions-exchange-2013-help.md)主題中的「信箱資料庫副本」項目。

  - 必須裝載作用中副本的資料庫。

  - 指定的信箱伺服器必須未裝載資料庫的複本。

  - 必須選取信箱伺服器上的可用資料庫副本和記錄檔的路徑。

  - 裝載作用中副本及伺服器主控被動副本的伺服器必須位於相同的資料庫可用性群組 (DAG)。DAG 也必須有仲裁及狀況良好。

  - 若要新增第二個資料庫副本的 （例如，建立第一個資料庫的被動副本），指定的信箱資料庫不必須啟用循環記錄。如果已啟用循環記錄，必須先停用服務。已新增信箱資料庫複本之後，可啟用循環記錄。複寫的信箱資料庫啟用循環記錄之後，連續複寫循環記錄 (CRCL) 是用來取代 JET 循環記錄。若要新增資料庫的第三個或後續複本，可保留已啟用 CRCL。

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

## 使用 EAC 來新增信箱資料庫副本

1.  
    
    在 EAC 中，移至 \[伺服器\] \> \[資料庫\]。

2.  選取您要複製的資料庫，然後按一下 \[ ![加入資料庫複本](images/Dd298080.435c15ff-abf2-4de8-b280-f053db1afa13(EXCHG.150).gif "加入資料庫複本")。

3.  
    
    在 \[**新增信箱資料庫複本**\] 頁面上，按一下 \[**瀏覽...**、 選取信箱伺服器將裝載資料庫副本，並再按一下 \[**確定\]**。

4.  （選用） 設定資料庫副本的**啟動喜好設定數字**。

5.  按一下 \[**其他選項\]**來指定為延遲的資料庫副本的資料庫副本設定重新顯示延遲時間，或是延後自動植入資料庫副本。

6.  按一下 \[**儲存**\] 以儲存設定變更，並新增信箱資料庫副本。

7.  按一下**\[確定\]**確認出現任何訊息。

## 使用命令介面來新增信箱資料庫副本

本範例會新增到信箱伺服器 mbx3 上信箱資料庫 DB1 的複本。重新顯示延遲時間和截斷延遲時間仍維持預設值為零，並啟動喜好設定設定值為 2。

    Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX3 -ActivationPreference 2

本範例會新增到信箱伺服器 MBX4 DB2 的信箱資料庫複本。重新顯示延遲時間和截斷延遲時間仍維持預設值為零，並啟動喜好設定已`5`的值。此外，植入已被延遲此複本以便其可以植入而不是從 MBX4 遠距目前作用中資料庫副本使用本機的來源伺服器。

    Add-MailboxDatabaseCopy -Identity DB2 -MailboxServer MBX4 -ActivationPreference 5 -SeedingPostponed

本範例會新增到信箱伺服器 MBX5 信箱資料庫 DB3 的副本。重新顯示延遲時間設為 3 天、 截斷延遲時間維持預設值為零，並啟動喜好設定會設定與`4`的值。

    Add-MailboxDatabaseCopy -Identity DB3 -MailboxServer MBX5 -ReplayLagTime 3.00:00:00 -ActivationPreference 4

## 如何知道這是否正常運作？

若要確認您已成功建立信箱資料庫複本，請執行下列其中一項：

  - 在 EAC 中，瀏覽至 \[**伺服器**\>**資料庫**。選取 \[複製的資料庫。在 \[詳細資料\] 窗格中會顯示的資料庫副本和其內容索引狀態，以及目前的複製佇列長度。

  - 在命令介面中，執行下列指令以確認已建立信箱資料庫副本與其狀況：
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName>
    
    狀態與內容索引狀態皆應為 \[正常\]。

## 相關資訊

[信箱資料庫副本](mailbox-database-copies-exchange-2013-help.md)

[管理信箱資料庫副本](managing-mailbox-database-copies-exchange-2013-help.md)

