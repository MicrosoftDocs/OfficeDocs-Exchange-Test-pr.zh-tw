---
title: '設定已刪除的項目保留及可復原的項目配額: Exchange 2013 Help'
TOCTitle: 設定已刪除的項目保留及可復原的項目配額
ms:assetid: de7d667a-1c93-4364-a4f9-2aa5e3678b12
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee364752(v=EXCHG.150)
ms:contentKeyID: 50554100
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定已刪除的項目保留及可復原的項目配額

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

當使用者會從 \[刪除的郵件\] 預設資料夾刪除項目使用 Delete、 Shift + Delete 或**空刪除項目資料夾**動作時，項目會移至 \[**可復原的 Items\\Deletions** \] 資料夾。期間已刪除的項目保留在此資料夾中為基礎的信箱資料庫或信箱設定已刪除的項目保留設定。根據預設，信箱資料庫設定為 14 天內，保留已刪除的項目並可復原的項目警告配額和配額可復原的項目會設為 20 gb 和 30 GB 分別。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>刪除的項目經過、 Microsoft Outlook和 Microsoft OfficeOutlook Web App的保留時間之前的使用者可以使用復原刪除的郵件功能復原刪除的項目。若要深入了解這些功能，請參閱&quot;復原已刪除的項目 」 主題<a href="https://go.microsoft.com/fwlink/p/?linkid=198206">Outlook</a>或<a href="https://go.microsoft.com/fwlink/p/?linkid=198207">Outlook Web App</a>。</td>
</tr>
</tbody>
</table>


您可以使用命令介面來設定已刪除的項目保留設定和信箱或信箱資料庫的可復原的項目配額。刪除項目設定會略過信箱處於就地保留或訴訟資料暫留時保留。

若要深入了解刪除項目保留、\[可復原的項目\] 資料夾、就地保留和訴訟保留，請參閱[可復原的項目資料夾](recoverable-items-folder-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「通訊記錄管理」項目。

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

## 設定信箱的刪除項目保留

**使用 EAC 來設定信箱的刪除項目保留**

1.  瀏覽至 \[收件者\] \> \[信箱\]。

2.  在清單檢視中，選取 \[信箱\] 和 \[**編輯**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在信箱屬性\] 頁面上，按一下 \[**信箱使用量**、 按一下 \[**更多選項**\]，然後選取下列其中一項
    
      - **使用來自信箱資料庫的預設保留設定**  使用此設定可使用已刪除項目保留設定信箱資料庫。
    
      - **自訂此信箱的設定**  使用此設定來設定信箱已刪除的項目保留設定。
        
        **保留已刪除項目 （天）**  此方塊會顯示前永久刪除，且無法復原之使用者所保留的刪除的郵件的時間長度。建立信箱之後，這個值根據刪除項目保留設定信箱資料庫的設定。根據預設，信箱資料庫被設定為 14 天內保留已刪除的項目。此屬性的值範圍是從 0 到 24,855 天。
    
      - \[不要在備份資料庫前永久刪除項目\]   選取這個核取方塊，可在備份信箱所在的信箱資料庫之後，才刪除信箱和電子郵件。

**使用命令介面來設定信箱的刪除項目保留**

此範例會設定 April Stewart 信箱 30 天保留已刪除的項目。

    Set-Mailbox -Identity - "April Stewart" -RetainDeletedItemsFor 30

如需詳細的語法及參數資訊，請參閱 [Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\))。

## 使用命令介面來設定信箱的可復原的項目配額

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您無法使用 EAC 來設定信箱配額可復原的項目。</td>
</tr>
</tbody>
</table>


此範例會設定警告配額的 12 GB 和 April Stewart 信箱的可復原的項目配額 15 GB 的可復原的項目。

    Set-Mailbox -Identity "April Stewart" -RecoverableItemsWarningQuota 12GB -RecoverableItemsQuota 15GB -UseDatabaseQuotaDefaults $false

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要設定要使用不同的可復原項目比其所在之信箱資料庫的配額的信箱，您必須<em>UseDatabaseQuotaDefaults</em>參數設定為<code>$false</code>。</td>
</tr>
</tbody>
</table>


如需詳細的語法及參數資訊，請參閱 [Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\))。

## 使用命令介面來設定信箱資料庫刪除項目保留

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您無法使用 EAC 來設定信箱資料庫刪除項目保留。</td>
</tr>
</tbody>
</table>


此範例會設定為 10 天的信箱資料庫 MDB2 已刪除的項目保留期間。

    Set-MailboxDatabase -Identity MDB2 -DeletedItemRetention 10

如需詳細的語法及參數資訊，請參閱 [Set-MailboxDatabase](https://technet.microsoft.com/zh-tw/library/bb123971\(v=exchg.150\))。

## 使用命令介面來設定信箱資料庫的可復原的項目配額

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您無法使用 EAC 來設定信箱資料庫的可復原的項目配額</td>
</tr>
</tbody>
</table>


此範例會設定警告配額的 15 GB 與信箱資料庫 MDB2 上 20 GB 的可復原的項目配額可復原的項目。

    Set-MailboxDatabase -Identity MDB2 -RecoverableItemsWarningQuota 15GB -RecoverableItemsQuota 20GB

如需詳細的語法及參數資訊，請參閱 [Set-MailboxDatabase](https://technet.microsoft.com/zh-tw/library/bb123971\(v=exchg.150\))。

