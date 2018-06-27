---
title: '使用 Windows Server Backup 來備份 Exchange: Exchange 2013 Help'
TOCTitle: 使用 Windows Server Backup 來備份 Exchange
ms:assetid: 188a8291-0a41-4ca2-b6d2-94242e2b1ffc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd876854(v=EXCHG.150)
ms:contentKeyID: 50472711
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用 Windows Server Backup 來備份 Exchange

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-06-18_

您可以使用 Windows Server Backup 來備份及還原 Exchange 資料庫。Exchange 包含 Windows Server Backup 的外掛程式，可讓您製作 Exchange 資料的大量陰影複製服務 (VSS) 型備份。

## 開始之前有哪些須知？

  - 預估完成時間：1 分鐘，加上備份資料的時間

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「信箱復原」項目。

  - 本機電腦上必須安裝 Windows Server Backup 功能。

  - 在備份作業期間，會執行 Exchange 資料檔的一致性檢查，以確保檔案處於良好狀態且可用於復原。如果一致性檢查成功，Exchange 資料就可用於從該備份復原。如果一致性檢查失敗，Exchange 資料便無法用於復原。Windows Server 在備份用的快照上執行一致性檢查。因此，將檔案從快照中複製到備份媒體前，會知道備份的一致性，而且會通知使用者一致性檢查結果。

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


## 使用 Windows Server Backup 來備份 Exchange

1.  啟動 Windows Server Backup。

2.  選取 **\[本機備份\]**。

3.  在 \[動作\] 窗格中，按一下 **\[一次性備份\]** 來啟動 \[一次性備份精靈\]。

4.  在 **\[備份選項\]** 頁面上，選取 **\[不同選項\]**，然後按 **\[下一步\]**。

5.  在 **\[選取備份設定\]** 頁面上，選取 **\[自訂\]**，然後按 **\[下一步\]**。

6.  在 **\[選取要備份的項目\]** 頁面上，按一下 **\[新增項目\]** 選取要備份的磁碟區，然後按 **\[確定\]**。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>選擇磁碟區，而不是個別的資料夾。唯有選取整個磁碟區，才能執行應用程式層級的備份或還原。</td>
    </tr>
    </tbody>
    </table>


7.  按一下 **\[進階設定\]**。在 **\[排除項目\]** 索引標籤上，按一下 **\[新增排除範圍\]**，新增您要從備份中排除的任何檔案或檔案類型。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>根據預設，包含作業系統元件或應用程式的磁碟區均會納入備份作業中，且無法排除。</td>
    </tr>
    </tbody>
    </table>


8.  在 **\[VSS 設定\]** 索引標籤上，選取 **\[VSS 完整備份\]**，然後按一下 **\[確定\]**，再按 **\[下一步\]**。

9.  在 **\[指定目的地類型\]** 頁面上選取用以儲存備份的位置，然後按 **\[下一步\]**。
    
      - 如果您選擇 **\[本機磁碟機\]**，則會出現 **\[選取備份目的地\]** 頁面。從 **\[備份目的地\]** 下拉式清單中選取選項，然後按 **\[下一步\]**。
    
      - 如果您選擇 **\[遠端共用資料夾\]**，則會出現 **\[指定遠端資料夾\]** 頁面。指定備份檔案的 UNC 路徑，設定存取控制設定。如果只允許透過特定帳戶才能存取備份，請選擇 **\[不要繼承\]**。針對在裝載遠端資料夾的電腦上具有寫入權限的帳戶，提供使用者名稱和密碼，然後按一下 **\[確定\]**。或者，如果要讓可存取遠端資料夾的每個人都可存取備份，請選擇 **\[繼承\]**。按 **\[下一步\]**。

10. 在 **\[確認\]** 頁面上檢閱備份設定，然後按一下 **\[備份\]**。

11. 在 **\[備份進度\]** 頁面上，您可以檢視備份作業的狀態與進度。

12. 隨時可按一下 **\[關閉\]**，結束 **\[備份進度\]** 頁面。正在進行的任何備份將繼續在背景執行。

## 如何才能了解這是否正常運作？

若要驗證您是否已成功備份資料，請執行下列任何動作：

  - 在執行 Windows Server Backup 的伺服器上，將會顯示最新的備份狀態，應該是 \[成功\]。您也可以檢視 Windows Server Backup 記錄檔，以驗證備份順利完成。

  - 開啟事件檢視器並確認備份完成事件已記錄於應用程式事件記錄檔中。

  - 在 Exchange 管理命令介面中執行下列命令，以驗證所選取的磁碟區上的每個資料庫都已成功備份：
    
        Get-MailboxDatabase -Server <ServerName> -Status | fl Name,*FullBackup
    
    資料庫的 *SnapshotLastFullBackup* 和 *LastFullBackup* 屬性指出上次成功備份的時間，以及是否為 VSS 完整備份。

