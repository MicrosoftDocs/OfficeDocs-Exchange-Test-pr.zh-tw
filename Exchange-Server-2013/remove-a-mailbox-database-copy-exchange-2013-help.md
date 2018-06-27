---
title: '移除信箱資料庫副本: Exchange 2013 Help'
TOCTitle: 移除信箱資料庫副本
ms:assetid: 99fecdde-b158-4dfc-9ca7-ff7c0ada7819
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd298164(v=EXCHG.150)
ms:contentKeyID: 50473795
ms.date: 01/12/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 移除信箱資料庫副本

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-11-06_

下列程序會示範如何移除信箱資料庫的複本。您無法使用這些程序來移除信箱資料庫的最後一個複本。如需如何移除信箱資料庫最後一個副本的詳細步驟，請參閱＜[移除信箱資料庫](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md)＞或＜[Remove-MailboxDatabase](https://technet.microsoft.com/zh-tw/library/aa997931\(v=exchg.150\))＞。

要尋找與信箱資料庫副本相關的其他管理工作嗎？請參閱[管理信箱資料庫副本](managing-mailbox-database-copies-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 完成此工作的預估時間：1 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱[高可用性和站台回復性權限](high-availability-and-site-resilience-permissions-exchange-2013-help.md)主題中的「信箱資料庫副本」項目。

  - 信箱資料庫副本只能從狀況良好的資料庫可用性群組 (DAG) 移除。如果 DAG 狀況不佳 (例如，DAG 的基礎叢集關閉，因爲仲裁遺失)，則無法移除任何信箱資料庫副本。

  - 如果您要移除資料庫的最後一個被動副本，必須為指定的信箱資料庫啟用連續複寫循環記錄 (CRCL)。如果啟用 CRCL，必須先將它停用。在移除信箱資料庫副本之後，便可以啟用循環記錄。一旦為未複寫的信箱資料庫啟用後，就會使用 JET 循環記錄而非 CRCL。如果您不要移除資料庫的最後一個被動副本，則 CRCL 會維持在啟用狀態。

  - 在移除資料庫副本之後，必須手動刪除所移除資料庫副本所在伺服器上的任何資料庫和交易記錄檔。

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

## 使用 EAC 移除信箱資料庫副本

1.  在 EAC 中，移至 \[伺服器\] \> \[資料庫\]。

2.  選擇您想要刪除其副本的信箱資料庫。

3.  在 \[詳細資料\] 窗格中，找出您想要移除的被動副本，然後按一下 \[移除\]。

4.  在警告對話方塊上按一下 \[是\] 以確認移除。

5.  按一下 \[確定\] 以確認預覽任何郵件後移除郵件。

6.  從移除資料庫副本之伺服器中手動刪除任何資料庫和交易記錄檔。

## 使用命令介面移除信箱資料庫副本

此範例會移除信箱伺服器 MBX1 上信箱資料庫 DB1 的副本。

    Remove-MailboxDatabaseCopy -Identity DB1\MBX1 -Confirm:$False

## 如何知道這是否正常運作？

若要驗證您已成功移除信箱資料庫複本，請執行下列任一動作：

  - 在 EAC 中，瀏覽至 \[伺服器\]資料庫。選取適當的資料庫，在 \[詳細資料\] 窗格中就不會再列出移除的被動副本。

  - 在命令介面中，執行下列指令以確認移除複本。
    
        Get-MailboxDatabase <DatabaseName> | Format-List DatabaseCopies
    
    移除的被動副本將不會再列出。

