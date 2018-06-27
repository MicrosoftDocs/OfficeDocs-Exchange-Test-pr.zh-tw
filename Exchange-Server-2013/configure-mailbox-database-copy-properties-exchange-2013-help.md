---
title: '設定信箱資料庫副本屬性: Exchange 2013 Help'
TOCTitle: 設定信箱資料庫副本屬性
ms:assetid: cf186561-ab2c-45c0-90f5-8d3ecfabeeac
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd351151(v=EXCHG.150)
ms:contentKeyID: 50474300
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定信箱資料庫副本屬性

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-11-01_

每個信箱資料庫副本有一些您可以設定自己屬性。重新顯示延遲和截斷延遲和啟動喜好設定號碼的任何包含時間的量。如需重新執行延隔時間、 截斷延遲和啟動喜好設定號碼的詳細資訊，請參閱[管理信箱資料庫副本](managing-mailbox-database-copies-exchange-2013-help.md)。

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

## 使用 EAC 來設定信箱資料庫副本屬性

1.  在 EAC 中，移至 \[伺服器\] \> \[資料庫\]。

2.  選取您想要設定的資料庫。

3.  在詳細資料窗格的**資料庫副本**，按一下 \[**檢視詳細資料**所需的資料庫副本，然後檢視或設定下列項目：
    
      - **資料庫**  會顯示所選的資料庫名稱。
    
      - **信箱伺服器**  會顯示主控所選的資料庫副本的信箱伺服器的名稱。
    
      - **內容索引狀態**  會顯示所選的資料庫副本的內容索引的目前狀態。
    
      - **狀態**  會顯示所選的資料庫副本的目前狀態。
    
      - **複製佇列長度**  表示等待複製到選取的資料庫副本的記錄檔數目。此欄位是僅適用於被動資料庫副本的相關內容。
    
      - **重新顯示佇列長度**  表示等待重新撥放入所選的資料庫副本的記錄檔數目。此欄位是僅適用於被動資料庫副本的相關內容。
    
      - **錯誤訊息**  顯示狀態為`Failed`或`Failed and Suspended`的資料庫副本的任何錯誤訊息。
    
      - **最新可用的記錄檔時間**  會顯示最近產生記錄檔之資料庫的主動副本上的日期和時間戳記。此欄位是僅適用於被動資料庫副本的相關內容。在使用中資料庫副本 （複寫和獨立），此欄位會**永遠不**顯示。
    
      - **上次檢查記錄檔**  會顯示所選取的資料庫副本 LogInspector 由檢查最後一個記錄檔的日期和時間戳記。此欄位是僅適用於被動資料庫副本的相關內容。在使用中資料庫副本 （複寫和獨立），此欄位會**永遠不**顯示。
    
      - **上次複製記錄檔**  會顯示所選取的資料庫副本 LogCopier 已複製最後一個記錄檔的日期和時間戳記。此欄位是僅適用於被動資料庫副本的相關內容。在使用中資料庫副本 （複寫和獨立），此欄位會**永遠不**顯示。
    
      - **上次重新執行的記錄檔**  會顯示最後一個已由 LogReplayer 重新顯示到選取的資料庫副本的記錄檔的日期和時間戳記。此欄位是僅適用於被動資料庫副本的相關內容。在使用中資料庫副本 （複寫和獨立），此欄位會**永遠不**顯示。
    
      - **啟動喜好設定號碼**  會顯示啟動喜好設定。這會做為組件的 Active Manager 之最佳副本選擇程序及平衡 DAG 來轉散發整個 DAG 使用 RedistributeActiveDatabases.ps1 指令碼中的作用中信箱資料庫。啟動喜好設定的值是數字等於或大於 1，其中 1 是在喜好設定順序的最頂端。數目不得大於信箱資料庫的列印份數。
    
      - **重新顯示延遲時間 （天）**  會顯示 Microsoft Exchange Information Store 服務應重新已由 Microsoft Exchange 複寫服務複製到被動資料庫副本的記錄檔之前應該等待的時間量。將此參數設為值大於 0 會建立延遲的資料庫副本。此值的預設值為 0 天。此設定允許的最大值為 14 天。允許的最小值為 0 天，並將此值設定為 0 停用重新執行延隔時間。

## 使用命令介面來設定信箱資料庫副本屬性

此範例會設定和啟動喜好設定號碼 3 的信箱資料庫複本。

    Set-MailboxDatabaseCopy -Identity DB3\EX3 -ActivationPreference 3

本範例會設定與重新顯示延遲時間和截斷延遲時間的 1 天及 2 的啟動喜好設定號碼 Server1 裝載資料庫 DB1 的複本。

    Set-MailboxDatabaseCopy -Identity DB1\Server1 -ReplayLagTime 1.0:0:0 -TruncationLagTime 1.0:0:0 -ActivationPreference 2

## 如何知道這是否正常運作？

若要確認您是否已成功設定信箱資料庫複本，請執行下列其中一項：

  - 在 EAC 中，瀏覽至 \[伺服器\] \> \[資料庫\]。  選擇適當的資料庫，並在 \[詳細資料\] 窗格中檢視資料庫複本屬性。

  - 在命令介面中執行下列命令來顯示資料庫副本的組態資訊。
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List

## 相關資訊

[Set-MailboxDatabaseCopy](https://technet.microsoft.com/zh-tw/library/dd298104\(v=exchg.150\))

[Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/zh-tw/library/dd298044\(v=exchg.150\))

[Get-MailboxDatabase](https://technet.microsoft.com/zh-tw/library/bb124924\(v=exchg.150\))

