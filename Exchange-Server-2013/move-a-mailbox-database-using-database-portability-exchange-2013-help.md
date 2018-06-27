---
title: '使用資料庫可攜性移動信箱資料庫: Exchange 2013 Help'
TOCTitle: 使用資料庫可攜性移動信箱資料庫
ms:assetid: a765ead1-43bc-4786-ae93-1835cacfc8fc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd876926(v=EXCHG.150)
ms:contentKeyID: 51409204
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用資料庫可攜性移動信箱資料庫

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-06-16_

您可以利用資料庫可攜性在相同組織中的 Exchange Server 2013 Mailbox Server 之間移動 Microsoft Exchange 2013 信箱資料庫。這有助於減少某些失敗狀況的整體復原時間。若要深入了解，請參閱[資料庫可攜性](database-portability-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘，加上還原資料、移動資料庫檔案和等候 Active Directory 複寫完成的時間。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「信箱復原」項目。

  - 您無法使用 EAC 透過資料庫可攜性將使用者信箱移動到已復原的或撥號音資料庫。

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


## 使用命令介面透過資料庫可攜性將使用者信箱移動到已復原的或撥號音資料庫

1.  確認要移動的資料庫是處於正常關閉狀態。如果資料庫未處於正常關機狀態，請執行軟復原。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>執行軟復原時，資料庫會認可任何未認可的記錄檔。如果沒有所有必要的記錄檔，您無法完成軟復原程序。繼續進行步驟 2。</td>
    </tr>
    </tbody>
    </table>
    
    若要資料庫認可所有未認可的記錄檔，請從命令提示字元執行下列命令。
    
        ESEUTIL /R <Enn>
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>&lt;E<em>nn</em>&gt; 指定想要在其中重新顯示記錄檔之資料庫的記錄檔前置詞。&lt;E<em>nn</em>&gt; 指定的記錄檔前置詞是 Eseutil /r 的必要參數。</td>
    </tr>
    </tbody>
    </table>


2.  使用下列語法在伺服器上建立資料庫：
    
        New-MailboxDatabase -Name <DatabaseName> -Server <ServerName> -EdbFilePath <DatabaseFileNameandPath> -LogFolderPath <LogFilesPath>

3.  使用下列語法設定 *This database can be over written by restore* 屬性：
    
        Set-MailboxDatabase <DatabaseName> -AllowFileRestore $true

4.  將原始資料庫檔案 (.edb 檔、記錄檔和 Exchange 搜尋類別目錄) 移至您建立上述新資料庫時所指定的資料庫資料夾。

5.  使用下列語法裝載資料庫：
    
        Mount-Database <DatabaseName>

6.  在裝載資料庫之後，請使用 [Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\)) 指令程式修改使用者帳戶設定，以便帳戶能夠指向新信箱伺服器上的信箱。若要將所有使用者從舊資料庫移動到新資料庫，請使用以下語法進行。
    
        Get-Mailbox -Database <SourceDatabase> |where {$_.ObjectClass -NotMatch '(SystemAttendantMailbox|ExOleDbSystemMailbox)'}| Set-Mailbox -Database <TargetDatabase>

7.  使用下列語法，觸發傳遞任何還留在佇列中的郵件。
    
        Get-Queue <QueueName> | Retry-Queue -Resubmit $true

Active Directory 複寫完成後，所有使用者都可以在新 Exchange 伺服器上存取其信箱。許多用戶端會經由自動探索而重新導向。Microsoft Office Outlook Web App 使用者也會自動重新導向。

## 如何知道這是否正常運作？

若要確認您是否已成功移動信箱，請執行下列動作：

  - 使用 Outlook Web App 開啟信箱。

  - 使用 Microsoft Outlook 開啟信箱。

