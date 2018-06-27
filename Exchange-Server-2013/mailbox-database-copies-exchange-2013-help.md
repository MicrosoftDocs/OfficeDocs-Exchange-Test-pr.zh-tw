---
title: '信箱資料庫副本: Exchange 2013 Help'
TOCTitle: 信箱資料庫副本
ms:assetid: ce748bca-3e24-493b-b9e6-153157bffd6a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd979802(v=EXCHG.150)
ms:contentKeyID: 50474294
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 信箱資料庫副本

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-07_

Microsoft Exchange Server 2013如何運用資料庫行動力，這是Exchange的概念-受管理的資料庫層級容錯移轉。資料庫行動力中斷資料庫與伺服器的連線、 新增一個資料庫，最多 16 個複本的支援和提供原生功能新增至資料庫的資料庫副本。

## 主要特性

信箱資料庫副本的主要特性為：

  - 最多 16 複本Exchange 2013信箱資料庫可以建立多個 Mailbox server 上、 提供伺服器組成資料庫可用性群組 (DAG)，這是連續複寫界限。僅對 DAG 中其他Exchange 2013信箱伺服器可以複寫Exchange 2013信箱資料庫。您不能複製資料庫以外的 DAG，也可以複製到伺服器執行Exchange 2010或更早版本Exchange 2013信箱資料庫。如需 Dag 的詳細資訊，請參閱[資料庫可用性群組 (DAGs)](database-availability-groups-dags-exchange-2013-help.md)。

  - DAG 中的所有信箱伺服器，必須在相同的 Active Directory 網域內。

  - 信箱資料庫副本支援重新顯示延遲時間和截斷延遲時間的概念。適當規劃必須執行才能啟用這些功能。

  - 所有的資料庫副本，都可以使用 Exchange 感知的磁碟區陰影複製服務 (VSS) 型備份應用程式來備份。

  - 資料庫副本可以只在不裝載資料庫的主動副本的 Mailbox server 上建立。您無法在同一部伺服器上建立兩個相同的資料庫副本。

  - 所有資料庫副本含有複本的每部伺服器上使用相同的路徑。每個信箱伺服器上的資料庫副本的資料庫和記錄檔路徑不必須與任何其他的資料庫路徑衝突。

  - 資料庫副本可建立在相同或不同的 Active Directory 站台上，以及相同或不同的子網路上。

  - 來回網路延遲大於 500 毫秒 (ms) 的信箱伺服器之間，不支援資料庫副本。

## 信箱資料庫副本

您可以隨時建立信箱資料庫複本。信箱資料庫副本可以分散於信箱伺服器的彈性與細微的方式。

您可以使用 Exchange 系統管理中心的 \[新增信箱資料庫副本\] 精靈，或使用 Exchange 管理命令介面的 **Add-MailboxDatabaseCopy** Cmdlet，建立信箱資料庫副本。

建立信箱資料庫副本時，請指定下列參數：

  - *Identity*  此參數會指定要複製的資料庫名稱。資料庫名稱必須是唯一Exchange組織內。

  - *MailboxServer*  此參數會指定主控資料庫副本的信箱伺服器的名稱。此伺服器必須是相同的 DAG 成員與必須未裝載資料庫的複本。

或者，您也可以指定：

  - *ActivationPreference*   此參數會指定當作 Active Manager 之最佳副本選擇程序的一部分使用啟動喜好設定數字。它也用來使用 RedistributeActiveDatabases.ps1 指令碼時轉散佈整個 DAG 的作用中信箱資料庫。啟動喜好設定的值是數字等於或大於的話其中一個是在喜好設定順序的最頂端。位置編號不可超過信箱資料庫副本的數目。

  - *ReplayLagTime * 此參數會指定 Microsoft Exchange複寫服務應重新複製到資料庫副本的記錄檔之前應該等待的時間量。此參數的格式為 (Days.hours)。此值的預設值為 0 秒。此值的最大可允許設定為 14 天。允許的最小值設定為 0 秒。以 0 關閉記錄重新顯示延遲時間的重新顯示延遲時間設定的值。

  - *TruncationLagTime*  此參數會指定 Microsoft Exchange複寫服務應等待截斷已重新顯示到資料庫複本的記錄檔的時間量。時段開始之後記錄順利轉送到資料庫副本。此參數的格式為 (Days.hours)。此值的預設值為 0 秒。此值的最大可允許設定為 14 天。允許的最小值設定為 0 秒。記錄截斷延遲時間的 0 關閉截斷延遲時間設定的值。

  - *SeedingPostponed*   此參數會指定工作自動不應該在指定的信箱伺服器上的資料庫副本植入。當您想要使用現有的被動副本的資料庫 （例如，將第二個特定資料庫複本新增至遠端位置） 植入新的信箱資料庫副本通常使用此選項。當您使用此參數時，則必須手動植入資料庫副本使用[Update-MailboxDatabaseCopy](https://technet.microsoft.com/zh-tw/library/dd335201\(v=exchg.150\))指令程式。

如需建立、使用和管理信箱資料庫副本的詳細資訊，請參閱 [管理信箱資料庫副本](managing-mailbox-database-copies-exchange-2013-help.md)。

