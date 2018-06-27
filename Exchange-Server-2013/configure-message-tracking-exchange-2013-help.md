---
title: '設定郵件追蹤: Exchange 2013 Help'
TOCTitle: 設定郵件追蹤
ms:assetid: 50eb5213-cf27-4179-b427-38d751ee4a70
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa997984(v=EXCHG.150)
ms:contentKeyID: 51409193
ms.date: 01/04/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 設定郵件追蹤

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2013-02-18_

郵件追蹤能記錄所有在傳輸服務或 Microsoft Exchange Server 2013 信箱伺服器上之信箱間往來傳輸的所有郵件 SMTP 傳輸活動。您可以使用郵件追蹤記錄檔進行郵件鑑識、郵件流程分析、報告及疑難排解等工作。

## 開始之前有哪些須知？

  - 預估完成時間：15 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱[郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「傳輸服務」項目或[收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「Mailbox Server 組態」項目。

  - 您可以使用 Exchange 系統管理中心 (EAC) 來啟用或停用郵件追蹤，或設定郵件追蹤記錄檔路徑。對於其他所有郵件追蹤選項，您需要使用 Exchange 管理命令介面。

  - 在 Exchange 2013 信箱伺服器上，您可以使用 **Set-TransportService** 或 **Set-MailboxServer** 指令程式來設定郵件追蹤選項。本主題中的程序使用 **Set-TransportService** 指令程式。

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


## 使用 EAC 來設定 Mailbox Server 上的郵件追蹤

1.  在 EAC 中，瀏覽至 \[伺服器\] \> \[伺服器\]。

2.  選取要配置的 Mailbox Server，然後按一下 \[確定\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在伺服器內容頁面上，按一下 \[傳輸記錄\]。

4.  在 **\[郵件追蹤記錄檔\]** 區段中，變更以下任一項目：
    
      - **啟用郵件追蹤記錄檔**   若要停用伺服器上的郵件追蹤，請清除核取方塊。若要啟用伺服器上的郵件追蹤，請選取核取方塊。
    
      - **郵件追蹤記錄檔路徑**   您指定的值必須位在本機 Exchange 伺服器上。如果資料夾不存在，將在您按一下 \[儲存\] 時加以建立。

5.  按一下 **\[儲存\]**。

## 使用命令介面設定郵件追蹤

若要設定郵件追蹤，請執行下列命令：

    Set-TransportService <ServerIdentity> -MessageTrackingLogEnabled <$true | $false> -MessageTrackingLogMaxAge <dd.hh:mm:ss> -MessageTrackingLogMaxDirectorySize <Size> -MessageTrackingLogMaxFileSize <Size> -MessageTrackingLogPath <LocalFilePath> -MessageTrackingLogSubjectLoggingEnabled <$true|$false>

此範例會設定名為 Mailbox01 的 Mailbox Server 的下列郵件追蹤記錄檔設定：

  -  
    將郵件追蹤記錄檔的位置設定成 D:\\Message Tracking Log。請注意，如果資料夾不存在，則會加以建立。

  -  
    將郵件追蹤記錄檔的大小上限設定為 20 MB。

  -  
    將郵件追蹤記錄檔目錄的大小上限設定為 1.5 GB。

  -  
    將郵件追蹤記錄檔的最長期限設定為 45 天。

<!-- end list -->

    Set-TransportService Mailbox01 -MessageTrackingLogPath "D:\Hub Message Tracking Log" -MessageTrackingLogMaxFileSize 20MB -MessageTrackingLogMaxDirectorySize 1.5GB -MessageTrackingLogMaxAge 45.00:00:00

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>將 <em>MessageTrackingLogPath</em> 參數的值設為 <code>$null</code> 可立即停用郵件追蹤。但是，若 <em>MessageTrackingLogEnabled</em> 參數的值為 <code>$true</code>，將產生事件記錄錯誤。</p></li>
<li><p>將 <em>MessageTrackingLogMaxAge</em> 參數設定為 <code>00:00:00</code> 值，可防止因保留天數之故而自動移除郵件追蹤記錄檔。</p></li>
<li><p>就 Exchange 2013 信箱伺服器而言，郵件追蹤記錄檔目錄的大小上限為 <em>MessageTrackingLogMaxDirectorySize</em> 參數值的三倍。儘管由四種相異服務產生的郵件追蹤記錄檔有四個不同的名稱前置詞，不過寫入 <strong>MSGTRKMA</strong> 記錄檔之資料的數量和頻率是可忽略的 (與其他三個記錄檔前置詞相較之下)。如需詳細資訊，請參閱<a href="message-tracking-exchange-2013-help.md">郵件追蹤</a>主題的＜郵件追蹤記錄檔的結構＞一節。</p></li>
</ul></td>
</tr>
</tbody>
</table>


此範例會停用名為 Mailbox01 之 Mailbox Server 上郵件追蹤記錄檔中的郵件主旨記錄：

    Set-TransportService Mailbox01 -MessageTrackingLogSubjectLoggingEnabled $false

此範例會停用名為 Mailbox01 之 Mailbox Server 上的郵件追蹤：

    Set-TransportService Mailbox01 -MessageTrackingLogEnabled $false

## 如何才能了解這是否正常運作？

若要確認您是否已成功設定郵件追蹤，請執行下列動作：

1.  在命令介面中，執行下列命令：
    
        Get-TransportService <ServerIdentity> | Format-List MessageTrackingLog*

2.  確認顯示的值是您設定的值。

