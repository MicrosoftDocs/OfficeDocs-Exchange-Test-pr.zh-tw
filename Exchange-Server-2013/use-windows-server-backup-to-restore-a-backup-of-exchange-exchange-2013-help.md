---
title: '使用 Windows Server Backup 還原 Exchange 的備份: Exchange 2013 Help'
TOCTitle: 使用 Windows Server Backup 還原 Exchange 的備份
ms:assetid: 2d0f31dc-eb32-451a-8852-591269026506
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd876864(v=EXCHG.150)
ms:contentKeyID: 50472768
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用 Windows Server Backup 還原 Exchange 的備份

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-06-18_

您可以使用 Windows Server Backup 來備份及還原 Exchange 資料庫。Exchange 包含 Windows Server Backup 的外掛程式，可讓您製作和還原 Exchange 資料的大量陰影複製服務 (VSS) 型備份。如需詳細資訊，請參閱[使用 Windows Server Backup 備份及還原 Exchange 資料](using-windows-server-backup-to-back-up-and-restore-exchange-data-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：1 分鐘，加上還原資料的時間。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「信箱復原」項目。

  - 本機電腦上必須安裝 Windows Server Backup 功能。

  - 還原資料庫到其原始位置時，資料庫可以維持在不正常關機狀態，並可由系統裝載。還原至替代位置時 (例如，為了準備使用復原資料庫)，必須使用 Exchange 伺服器資料庫公用程式 (Eseutil.exe)，手動讓資料庫進入正常關閉狀態。

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


## 使用 Windows Server Backup 還原 Exchange 的備份

1.  啟動 Windows Server Backup。

2.  選取 **\[本機備份\]**。

3.  在 \[動作\] 窗格中，按一下 **\[復原...\]** 以啟動復原精靈。

4.  在 \[入門\] 頁面上，執行下列其中一項：
    
      - 如果要復原的資料是在本機伺服器上備份，請選取 **\[這台伺服器 (伺服器名稱)\]**，然後按 **\[下一步\]**。
    
      - 如果要復原的資料來自其他伺服器，或如果要復原的備份位於其他電腦上，請選取 **\[另一台伺服器\]**，然後按 **\[下一步\]**。在 \[指定位置類型\] 頁面，選取 \[本機磁碟機\] 或是 \[遠端共用資料夾\]，然後按 \[下一步\]。如果您選取 \[本機磁碟機\]，則請選取 \[選取備份位置\] 頁面上包含備份的磁碟，然後按 \[下一步\]。如果您選取 \[遠端共用資料夾\]，則在 \[指定遠端資料夾\] 頁面上輸入備份資料的 UNC 路徑，然後按 \[下一步\]。

5.  在 **\[選取備份日期\]** 頁面上，選取您要復原的備份日期與時間，然後按 **\[下一步\]**。

6.  在 **\[選取復原類型\]** 頁面上，選取 **\[應用程式\]**，然後按 **\[下一步\]**。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果沒有 <strong>[應用程式]</strong> 這個選項，則表示選取要還原的備份是資料夾層級備份，而不是磁碟區層級備份。使用 Windows Server Backup 來備份 Exchange 資料時，您必須執行磁碟區層級的備份。</td>
    </tr>
    </tbody>
    </table>


7.  在 **\[選取應用程式\]** 頁面上，確認 **\[應用程式\]** 欄位中已選取 Exchange。按一下 \[檢視詳細資料\] 檢視備份的應用程式元件。如果您正在復原的備份是最近的備份，則會顯示 \[不要向前復原應用程式資料庫\] 核取方塊。如果您要防止 Windows Server Backup 認可所有未認可的交易記錄而將復原的資料庫向前復原，請選取此核取方塊。按 \[下一步\]。

8.  在 **\[指定復原選項\]** 頁面，指定您要將資料復原到何處，然後按 **\[下一步\]**：
    
      - 如果您想要將 Exchange 資料直接還原到原始位置，請選擇 **\[復原到原始位置\]**。如果您使用此選項，則無法選擇還原的資料庫。磁碟區上所有備份的資料庫會還原到其原始位置。
    
      - 如果您想要將個別資料庫及其檔案還原到指定位置，請選擇 **\[復原到另一個位置\]**。按一下 \[瀏覽\] 可指定其他位置。如果使用此選項，您可以選擇要還原的資料庫。還原之後，可使用[資料庫可攜性](database-portability-exchange-2013-help.md)，將資料檔移至復原資料庫中、手動移回至原始位置，或裝載於 Exchange 組織中的其他位置。當您將資料庫還原到另一個位置時，還原的資料庫將處於不正常關閉狀態。完成還原程序之後，您需要使用 Eseutil.exe，手動讓資料庫進入正常關閉狀態。

9.  在 \[確認\] 頁面上檢閱復原設定，然後按一下 \[復原\]。

10. 在 **\[復原進度\]** 頁面上，您可以檢視復原作業的狀態與進度。

11. 復原作業完成時，按一下 **\[關閉\]**。

## 如何才能了解這是否正常運作？

**\[復原進度\]** 頁面會指出復原程序是否順利完成。若要進一步驗證您是否已成功還原資料，請執行下列任何動作：

  - 檢查備份的目標目錄並確認還原的資料存在。

  - 在執行 Windows Server Backup 的伺服器上，檢視備份記錄檔來確認工作是否順利完成。

  - 開啟事件檢視器並確認還原完成事件已記錄於應用程式事件記錄檔中。

