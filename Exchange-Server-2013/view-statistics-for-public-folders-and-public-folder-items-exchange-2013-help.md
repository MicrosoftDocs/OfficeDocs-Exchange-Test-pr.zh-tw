---
title: '公用資料夾和公用資料夾項目的檢視統計資料: Exchange Online Help'
TOCTitle: 公用資料夾和公用資料夾項目的檢視統計資料
ms:assetid: 4e412710-9a74-4649-ab01-502e969a7eda
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa997949(v=EXCHG.150)
ms:contentKeyID: 50473202
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 公用資料夾和公用資料夾項目的檢視統計資料

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-14_

本主題說明如何擷取公用資料夾，例如顯示名稱、 建立時間、 上次修改的使用者、 最後一個使用者存取\] 和項目大小相關的統計資料。您可以使用這項資訊以進行刪除或保留 \[公用資料夾的相關決策。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在 Exchange 系統管理中心 (EAC)，您可以檢視由瀏覽至 [<strong>公用資料夾</strong>的公用資料夾的配額及使用方式資訊的一些 &gt;<strong>編輯</strong><img src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="編輯圖示" alt="編輯圖示" /> &gt;<strong>信箱使用量</strong>。不過，這項資訊不完整，因此建議您使用命令介面來檢視公用資料夾統計資料。</td>
</tr>
</tbody>
</table>


如需與管理公用資料夾相關的其他管理工作，請參閱[公用資料夾程序](public-folder-procedures-exchange-2013-help.md)。

如需與公用資料夾相關的其他管理工作，請參閱 [Office 365 和 Exchange Online 中公用資料夾程序](https://technet.microsoft.com/zh-tw/library/jj966272\(v=exchg.150\))。

## 開始之前有哪些須知？

  - 預估完成時間： 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [共用和協同作業的權限](sharing-and-collaboration-permissions-exchange-2013-help.md)主題中的「公用資料夾」項目。

  - 您無法使用 EAC 擷取公用資料夾統計資料。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 您要執行的工作

## 使用命令介面擷取公用資料夾統計資料

此範例會使用管線傳輸命令來格式化清單，傳回公用資料夾的統計資料。

    Get-PublicFolderStatistics -Identity \Marketing | Format-List

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><em>Identity</em>參數的值必須包含公用資料夾的路徑。例如，如果 Marketing 父系資料夾商務下已經存在的公用資料夾，會提供下列值： <code>\Business\Marketing</code></td>
</tr>
</tbody>
</table>


如需詳細的語法及參數資訊，請參閱 [Get-PublicFolderStatistics](https://technet.microsoft.com/zh-tw/library/aa998663\(v=exchg.150\))。

## 使用命令介面來檢視公用資料夾項目的統計資料

您可以檢視下列關於公用資料夾內項目的資訊：

  - 項目類型

  - 主旨

  - 上次使用者修改時間

  - 上次使用者存取時間

  - 建立時間

  - 附件

  - 郵件大小

您可以使用這項資訊以做出決定您的公用資料夾，例如若要刪除的公用資料夾需要採取的動作。例如，可能會想要刪除的公用資料夾若要轉換作為另一個用戶端存取應用程式的文件存放庫的公用資料夾或項目尚未已經超過兩個年度的存取。

此範例會傳回路徑 \\Marketing\\2013 下的公用資料夾 Pamphlets 中所有項目的預設統計資料。預設資訊包括項目識別碼、建立時間和主旨。

    Get-PublicFolderItemStatistics -Identity "\Marketing\2013\Pamphlets"

此範例會傳回公用資料夾 Pamphlets，例如主旨、 上次修改時間、 建立時間、 附件、 郵件大小和項目類型內的項目相關的其他資訊。它也包含傳送的命令，以格式化清單。

    Get-PublicFolderItemStatistics -Identity "\Marketing\2010\Pamphlets" | Format-List

如需詳細的語法及參數資訊，請參閱 [Get-PublicFolderItemStatistics](https://technet.microsoft.com/zh-tw/library/ee332344\(v=exchg.150\))。

## 使用命令介面來匯出 Get-PublicFolderItemStatistics 指令程式的輸出為 .csv 檔

此範例會將指令程式的輸出匯出至 PFItemStats.csv 檔案，而該檔案中包含公用資料夾 \\Marketing\\Reports 內所有項目的下列資訊：

  - 郵件主旨 (`Subject`)

  - 上次修改項目的日期與時間 (`LastModificationTime`)

  - 項目是否含有附件 (`HasAttachments`)

  - 項目類型 (`ItemType)`)

  - 項目大小 (`MessageSize`)

<!-- end list -->

    Get-PublicFolderItemStatistics -Identity "\Marketing\Reports" | Select Subject,LastModificationTime,HasAttachments,ItemType,MessageSize | Export-CSV C:\PFItemStats.csv

如需詳細的語法及參數資訊，請參閱 [Get-PublicFolderItemStatistics](https://technet.microsoft.com/zh-tw/library/ee332344\(v=exchg.150\))。

