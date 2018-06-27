---
title: '執行撥號音復原: Exchange 2013 Help'
TOCTitle: 執行撥號音復原
ms:assetid: 158817fa-4b17-4fa9-8341-a86609e6a388
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd979810(v=EXCHG.150)
ms:contentKeyID: 51409158
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 執行撥號音復原

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-06-27_

在還原或修復使用者的原始信箱期間，使用撥號音可攜性能讓使用者有暫時信箱可用於傳送及接收電子郵件。暫時信箱可以位於同一部 Exchange 2013 信箱伺服器上，或位於組織中的任何其他 Exchange 2013 信箱伺服器上。使用撥號音可攜性的處理程序稱為撥號音復原，該程序牽涉到在信箱伺服器上建立空的資料庫以取代失敗的資料庫。若要深入了解，請參閱[撥號音可攜性](dial-tone-portability-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘，加上還原及移動資料所花的時間。

  - 您已部署的資料庫數目必須未達上限才能建立撥號音資料庫。Exchange 2013 Standard Edition 針對每部伺服器最多可支援五個資料庫。Exchange 2013 Enterprise Edition 的 RTM 和 CU1 版可支援每部伺服器最多 50 個資料庫，而 CU2 和更新版本則支援每部伺服器最多 100 個資料庫。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「信箱復原」項目。

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


## 使用命令介面在單一伺服器上執行撥號音復原

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您無法使用 EAC 在單一伺服器上執行撥號音復原。</td>
</tr>
</tbody>
</table>


1.  請確認保留要復原之資料庫的任何現有檔案，以防日後執行其他復原作業時需要這些檔案。

2.  使用 [New-MailboxDatabase](https://technet.microsoft.com/zh-tw/library/aa997976\(v=exchg.150\)) 指令程式來建立撥號音資料庫，如本範例中所示。
    
        New-MailboxDatabase -Name DTDB1 -EdbFilePath D:\DialTone\DTDB1.EDB

3.  使用 [Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\)) 指令程式來重新隸屬位於要復原之資料庫上的使用者信箱，如本範例中所示。
    
        Get-Mailbox -Database DB1 | Set-Mailbox -Database DTDB1

4.  使用 [Mount-Database](https://technet.microsoft.com/zh-tw/library/aa998871\(v=exchg.150\)) 指令程式來裝載資料庫，以便用戶端電腦可以存取資料庫，且可傳送及接收郵件，如本範例中所示。
    
        Mount-Database -Identity DTDB1

5.  建立復原資料庫 (RDB)，並還原或複製資料庫與記錄檔，其中包含要復原到 RDB 中的資料。如需詳細步驟，請參閱[建立復原資料庫](create-a-recovery-database-exchange-2013-help.md)。

6.  將資料複製到 RDB 之後，但在裝載還原的資料庫之前，將任何記錄檔從失敗的資料庫複製到復原資料庫記錄檔資料夾，以便可以針對還原的資料庫重新顯示這些記錄檔。

7.  裝載 RDB，然後使用 [Dismount-Database](https://technet.microsoft.com/zh-tw/library/bb124936\(v=exchg.150\)) 指令程式卸載 RDB，如本範例中所示。
    
        Mount-Database -Identity RDB1
        Dismount-Database -Identity RDB1

8.  在卸載 RDB 之後，將 RDB 資料夾中目前的資料庫和記錄檔移至安全的位置。完成此動作以準備使用撥號音資料庫來交換復原的資料庫。

9.  卸載撥號音資料庫，如本範例中所示。請注意，當您卸載此資料庫時，使用者會遇到服務中斷問題。
    
        Dismount-Database -Identity DTDB1

10. 將資料庫和記錄檔從撥號音資料庫資料夾移到 RDB 資料夾中。

11. 從包含復原之資料庫的安全位置，將資料庫和記錄檔移至撥號音資料庫資料夾中，然後裝載該資料庫，如本範例中所示。
    
        Mount-Database -Identity DTDB1
    
    這會結束使用者遇到的服務中斷情況。使用者將可存取其原始實際生產資料庫，並傳送及接收郵件。

12. 裝載 RDB，如本範例中所示。
    
        Mount-Database -Identity RDB1

13. 使用 [Get-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123685\(v=exchg.150\)) 和 [New-MailboxRestoreRequest](https://technet.microsoft.com/zh-tw/library/ff829875\(v=exchg.150\)) 指令程式，從 RDB 匯出資料，然後將該資料匯入復原的資料庫，如本範例中所示。這會將所有使用撥號音資料庫傳送及接收的郵件匯入實際生產資料庫中。
    
        $mailboxes = Get-Mailbox -Database DTDB1
    
        $mailboxes | %{ New-MailboxRestoreRequest -SourceStoreMailbox $_.ExchangeGuid -SourceDatabase RDB1 -TargetMailbox $_ }

14. 完成還原作業後，可以卸載並移除 RDB，如本範例中所示。
    
        Dismount-Database -Identity RDB1
        Remove-MailboxDatabase -Identity RDB1

如需詳細的語法及參數資訊，請參閱下列主題：

  - [New-MailboxDatabase](https://technet.microsoft.com/zh-tw/library/aa997976\(v=exchg.150\))

  - [Get-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123685\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\))

  - [Mount-Database](https://technet.microsoft.com/zh-tw/library/aa998871\(v=exchg.150\))

  - [Dismount-Database](https://technet.microsoft.com/zh-tw/library/bb124936\(v=exchg.150\))

  - [Remove-MailboxDatabase](https://technet.microsoft.com/zh-tw/library/aa997931\(v=exchg.150\))

## 如何知道這是否正常運作？

若要確認您是否已成功移動信箱，請執行下列動作：

  - 使用 Microsoft Office Outlook Web App 開啟信箱。

  - 使用 Microsoft Outlook 開啟信箱。

