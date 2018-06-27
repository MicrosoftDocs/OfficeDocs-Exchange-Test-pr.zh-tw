---
title: '設定信箱的儲存配額: Exchange 2013 Help'
TOCTitle: 設定信箱的儲存配額
ms:assetid: 5f5fe292-c80e-4a0b-b3e6-e193ea5171d0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa998353(v=EXCHG.150)
ms:contentKeyID: 50553999
ms.date: 01/04/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 設定信箱的儲存配額

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-07-07_

**摘要：**使用 EAC 或 Shell 來設定特定信箱的儲存配額。

儲存配額可讓您控制信箱的大小及管理信箱資料庫的成長。當信箱大小到達或超出指定的儲存配額時，Exchange 便會傳送描述性通知給信箱擁有者。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您執行 <code>Get-MailboxStatistics</code> cmdlet 時，儲存配額會套用到 <code>TotalItemSize</code> 屬性所定義的指定信箱大小。如需詳細資訊，請參閱 <a href="https://technet.microsoft.com/zh-tw/library/bb124612(v=exchg.150)">Get-MailboxStatistics</a>。</td>
</tr>
</tbody>
</table>


儲存配額通常是以每個資料庫為基礎來設定。這表示，設定的信箱資料庫配額會套用至該資料庫中的所有信箱。如需管理每個資料庫之信箱設定的詳細資訊，請參閱[管理 Exchange 2013 中的信箱資料庫](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md)。

本主題說明如何自訂特定信箱的儲存設定，而不使用信箱資料庫的儲存設定。關於與使用者信箱相關的其他管理工作，請參閱[管理使用者信箱](manage-user-mailboxes-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：2 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱[收件者權限](recipients-permissions-exchange-2013-help.md) 主題中的「收件者佈建權限」一節。

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

## 使用 EAC 來設定信箱的儲存配額

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[信箱\]。

2.  在使用者信箱清單中，按一下您想變更儲存配額的信箱，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在信箱屬性頁上，按一下 \[信箱使用量\]，然後按一下 \[更多選項\]。

4.  按一下 \[自訂此信箱的設定\]，然後設定下列方塊。對於任何儲存配額設定的值範圍是 0 到 2047 GB。
    
      - \[在 (GB) 時發出警告\]   這個方塊顯示向使用者發出警告前的儲存上限。 如果信箱大小到達或超過指定的值，Exchange 就會傳送警告郵件給使用者。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>除非發出警告配額設定的值大於 [禁止傳送] 配額指定值的 50%，否則不會將與 [發出警告] 配額有關的郵件傳送給使用者。舉例來說，若您將 [禁止傳送] 配額設為 8 MB，您必須將 [發出警告] 配額至少設為 4 MB。否則，則不會傳送 [發出警告] 配額郵件。</td>
        </tr>
        </tbody>
        </table>
    
      - **在 (GB) 時禁止傳送**   這個方塊顯示信箱的*禁止傳送*限制。 如果信箱大小到達或超過指定的限制，Exchange 會阻止使用者傳送新郵件，並會顯示描述性錯誤訊息。
    
      - **在 (GB) 時禁止傳送和接收**   這個方塊顯示信箱的*禁止傳送和接收*限制。 如果信箱大小到達或超過指定的限制，Exchange 會阻止信箱使用者傳送新郵件，且不會將任何新郵件傳遞到信箱。 傳送給信箱的任何郵件都會退回給寄件者，並附帶描述性錯誤訊息。

5.  按一下 \[儲存\] 以儲存變更。

## 使用命令介面來設定信箱的儲存配額

此範例會將 Joe Healy 信箱的發出警告、禁止傳送及禁止收發配額分別設定為 24.5 GB、24.75 GB 及 25 GB。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要確定使用的是信箱自訂設定而非信箱資料庫預設值，必須將 <em>UseDatabaseQuotaDefaults</em> 參數設為 <code>$false</code>。</td>
</tr>
</tbody>
</table>


    Set-Mailbox -Identity "Joe Healy" -IssueWarningQuota 24.5gb -ProhibitSendQuota 24.75gb -ProhibitSendReceiveQuota 25gb -UseDatabaseQuotaDefaults $false

此範例會將 Ayla Kol 信箱的發出警告、禁止傳送及禁止收發配額分別設定為 900 MB、950 MB 及 1 GB，並且設定信箱使用自訂設定。

    Set-Mailbox -Identity "Ayla Kol" -IssueWarningQuota 900mb -ProhibitSendQuota 950mb -ProhibitSendReceiveQuota 1gb -UseDatabaseQuotaDefaults $false

如需詳細的語法及參數資訊，請參閱 [Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\))。

## 如何知道這是否正常運作？

若要確認是否已成功設定信箱的儲存配額，請執行下列其中一項操作：

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[信箱\]。

2.  在使用者信箱清單中，按一下您想確認儲存配額的信箱，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在信箱屬性頁上，按一下 \[信箱使用量\]，然後按一下 \[更多選項\]。

4.  確認已選取 \[自訂此信箱的設定\]。

5.  驗證儲存配額設定。

或

在命令介面中執行下列命令。

    Get-Mailbox <identity> | fl IssueWarningQuota,ProhibitSendQuota,ProhibitSendReceiveQuota,UseDatabaseQuotaDefaults

