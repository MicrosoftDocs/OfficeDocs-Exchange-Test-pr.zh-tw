---
title: '復原資料庫可用性群組成員伺服器: Exchange 2013 Help'
TOCTitle: 復原資料庫可用性群組成員伺服器
ms:assetid: eccd8f61-9706-4bb7-a62a-ec7c166f8019
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd638206(v=EXCHG.150)
ms:contentKeyID: 50474534
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 復原資料庫可用性群組成員伺服器

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

如果資料庫可用性群組 (DAG) 成員的信箱伺服器遺失或否則失敗並無法復原且需要取代，您可以執行伺服器復原作業。Microsoft Exchange Server 2013安裝程式會包含參數*/m:RecoverServer*可以用來執行 server 復原作業。執行安裝程式與*/m:RecoverServer*交換器原因安裝程式以閱讀該伺服器的組態資訊從Active Directory具有相同名稱您正在執行安裝程式之伺服器的伺服器。伺服器設定後從Active Directory、 Exchange原始檔案收集資訊的伺服器上，然後會安裝服務和角色與已儲存在Active Directory設定則套用至伺服器。

要尋找與 DAG 相關的其他管理工作嗎？ 請參閱[管理資料庫可用性群組](managing-database-availability-groups-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：30 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [高可用性和站台回復性權限](high-availability-and-site-resilience-permissions-exchange-2013-help.md)主題中的「信箱資料庫副本」項目。

  - 若 Exchange 安裝在預設位置以外的位置，您必須使用*/TargetDir*安裝程式參數指定 Exchange 程式檔案的位置。如果您不要使用*/TargetDir*交換器、 Exchange 程式檔案會安裝在預設位置 (%programfiles%\\Microsoft\\Exchange Server\\V15)。
    
    若要決定安裝位置，請遵循下列步驟：
    
    1.  開啟 ADSIEDIT.MSC 或 LDP.EXE。
    
    2.  瀏覽至下列位置： **CN=ExServerName、CN=Servers、CN=First Administrative Group、CN=Administrative Groups、CN=ExOrg Name、CN=Microsoft Exchange、CN=Services、CN=Configuration、DC=DomainName、CN=Com**
    
    3.  在 Exchange 伺服器物件上按一下滑鼠右鍵，然後按一下 \[內容\]。
    
    4.  尋找 **msExchInstallPath** 屬性。 此屬性儲存了當前的安裝路徑。

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


## 使用安裝程式 /m:RecoverServer 復原伺服器

1.  請使用 [Get-MailboxDatabase](https://technet.microsoft.com/zh-tw/library/bb124924\(v=exchg.150\)) 指令程式，針對正在復原的伺服器上的任何信箱資料庫副本，擷取其重新顯示延遲時間或截斷延遲時間設定：
    
        Get-MailboxDatabase DB1 | Format-List *lag*

2.  請使用 [Remove-MailboxDatabaseCopy](https://technet.microsoft.com/zh-tw/library/dd335119\(v=exchg.150\)) 指令程式，移除正在復原之伺服器上的所有信箱資料庫副本：
    
        Remove-MailboxDatabaseCopy DB1\MBX1

3.  請使用 [Remove-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/zh-tw/library/dd297956\(v=exchg.150\)) 指令程式，從 DAG 移除失敗的伺服器組態：
    
        Remove-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX1
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>若要移除的 DAG 成員離線，且無法上線，您必須新增<em>ConfigurationOnly</em>參數至以上的命令。如果您使用<em>ConfigurationOnly</em>參數，您必須也手動收回從叢集節點。</td>
    </tr>
    </tbody>
    </table>


4.  重設Active Directory中該伺服器的電腦帳戶。詳細步驟，請參閱[重設為電腦帳戶](http://go.microsoft.com/fwlink/p/?linkid=167188)。

5.  開啟 \[命令提示字元\] 視窗。 使用原始安裝程式媒體，並執行下列命令：
    
        Setup /m:RecoverServer

6.  一旦安裝程式復原程序完成，使用 [Add-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/zh-tw/library/dd298049\(v=exchg.150\)) 指令程式將復原的伺服器新增至 DAG：
    
        Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX1

7.  當伺服器新增至原本的 DAG 之後，您可以使用 [Add-MailboxDatabaseCopy](https://technet.microsoft.com/zh-tw/library/dd298105\(v=exchg.150\)) 指令程式重新設定信箱資料庫副本。 如果正在新增的任何一個資料庫副本先前出現大於 0 的重新顯示延遲或截斷延遲時間，則您可以使用 [Add-MailboxDatabaseCopy](https://technet.microsoft.com/zh-tw/library/dd298105\(v=exchg.150\)) 指令程式的 *ReplayLagTime* 和 *TruncationLagTime* 參數來重新進行這些設定：
    
        Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX1
        Add-MailboxDatabaseCopy -Identity DB2 -MailboxServer MBX1 -ReplayLagTime 3.00:00:00
        Add-MailboxDatabaseCopy -Identity DB3 -MailboxServer MBX1 -ReplayLagTime 3.00:00:00 -TruncationLagTime 3.00:00:00

## 如何知道這是否正常運作？

若要確認您已成功復原 DAG 成員，執行下列動作：

  - 在命令介面中執行下列命令來確認健康狀況和狀態復原的 DAG 成員。
    
        Test-ReplicationHealth <ServerName>
    
        Get-MailboxDatabaseCopyStatus -Server <ServerName>
    
    所有的複寫狀況測試應順利通過，並應狀況良好的資料庫和其內容索引狀態。

