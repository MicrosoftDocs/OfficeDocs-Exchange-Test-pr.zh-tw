---
title: '設定連線記錄: Exchange 2013 Help'
TOCTitle: 設定連線記錄
ms:assetid: 24e46a79-33ea-44e9-b03c-549db1c86a6f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa996827(v=EXCHG.150)
ms:contentKeyID: 50472730
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定連線記錄

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2013-02-18_

連線記錄會記錄用來傳輸訊息從 Exchange 伺服器上傳輸服務的輸出連線活動。 連線記錄會記錄連線來源、 destination、 訊息與傳輸的位元組數目及連線失敗資訊。

## 開始之前有哪些須知？

  - 預估完成時間：15 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「傳輸服務」、「前端傳輸服務」和「信箱傳輸服務」項目。

  - 您可以使用 Exchange 系統管理中心 (EAC) 來啟用或停用連線記錄或設定傳輸服務的連線記錄檔路徑。所有其他連線記錄選項的其他傳輸服務中，您必須使用命令介面。

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

## 使用 EAC 來設定在傳輸服務中的連線記錄

1.  在 EAC 中，瀏覽至 \[伺服器\] \> \[伺服器\]。

2.  選取要配置的 Mailbox Server，然後按一下 \[確定\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在伺服器內容頁面上，按一下 \[傳輸記錄\]。

4.  在 \[連線記錄檔\] 區段中，變更下列其中一個步驟：
    
      - **啟用連線記錄檔**  若要停用登入伺服器的連線，請清除此核取方塊。若要啟用登入伺服器的連線，請選取此核取方塊。
    
      - **連線記錄檔路徑**  您指定的值必須是本機 Exchange 伺服器上。如果資料夾不存在，它會建立您時按一下 \[**儲存檔案**。
    
    完成後，按一下 **\[儲存\]**。

## 使用命令介面設定連線記錄

若要設定連線記錄，請執行下列命令：

    <Set-TransportService | Set-MailboxTransportService | Set-FrontEndTransportService> <ServerIdentity> -ConnectivityLogEnabled <$true | $false> -ConnectivityLogMaxAge <dd.hh:mm:ss> -ConnectivityLogMaxDirectorySize <Size> -ConnectivityLogMaxFileSize <Size> -ConnectivityLogPath <LocalFilePath>

本範例設定下列在名為 Mailbox01 的信箱伺服器上之傳輸服務之連線記錄檔設定：

  -  
    設定記錄檔位置的連線 D:\\Hub 連線記錄檔。請注意是否資料夾不存在，它會為您建立。

  -  
    將連線記錄檔案的最大大小設定為 20 MB。

  -  
    將連線記錄檔目錄的最大大小設定為1.5 GB。

  -  
    將連線記錄檔案的最長期限設定為 45 天。

<!-- end list -->

    Set-TransportService Mailbox01 -ConnectivityLogPath "D:\Hub Connectivity Log" -ConnectivityLogMaxFileSize 20MB -ConnectivityLogMaxDirectorySize 1.5GB -ConnectivityLogMaxAge 45.00:00:00

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
<li><p>若要設定連線記錄檔設定信箱伺服器上的信箱傳輸服務中，使用<strong>Set-MailboxTransportService</strong>指令程式。若要設定連線記錄檔設定 Client Access server 上 Front End Transport 服務中，使用<strong>Set-FrontEndTransportService</strong>指令程式。</p></li>
<li><p><em>ConnectivityLogPath</em>參數設定為值<code>$null</code>，有效停用連線記錄。不過，如果<code>$true</code><em>ConnectivityLogEnabled</em>參數的值，會產生事件記錄檔錯誤。</p></li>
<li><p>將 <em>ConnectivityLogMaxAge</em> 參數的值設為<code>00:00:00</code>，可以防止因為連線記錄檔的保留天數而自動移除連線記錄檔。</p></li>
</ul></td>
</tr>
</tbody>
</table>


## 如何才能了解這是否正常運作？

若要驗證您是否已成功設定連線記錄，執行下列操作：

1.  在命令介面中，執行下列命令：
    
        <Get-TransportService | Get-FrontEndTransportService | Get-MailboxTransportService> <ServerIdentity> | Format-List ConnectivityLog*

2.  請確認顯示的值是您所設定的值。

