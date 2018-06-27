---
title: '設定反垃圾郵件代理程式記錄: Exchange 2013 Help'
TOCTitle: 設定反垃圾郵件代理程式記錄
ms:assetid: df157ca3-ad8e-4302-acbc-5fbb8570c21d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb691337(v=EXCHG.150)
ms:contentKeyID: 50474402
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定反垃圾郵件代理程式記錄

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-08_

代理程式記錄會記錄特定 Exchange 反垃圾郵件代理程式所執行的動作。寫入至代理程式記錄檔的資訊取決於代理程式、 SMTP 事件以及在郵件上執行的動作。

## 開始之前有哪些須知？

  - 預估完成時間：15 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「傳輸服務」和「Edge Transport Server」項目。

  - 預設在 Mailbox Server 的 Transport 服務中未啟用反垃圾郵件功能。通常只有在您的 Exchange 組織接受內送郵件之前未進行任何事前的反垃圾郵件篩選的情況下，您才會在 Mailbox Server 上啟用反垃圾郵件功能。如需詳細資訊，請參閱[啟用信箱伺服器上的反垃圾郵件功能](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md)。

  - 您只能使用命令介面來執行此程序。

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


## 使用命令介面設定防垃圾郵件代理程式記錄

執行下列命令：

    Set-TransportService <ServerIdentity> -AgentLogEnabled <$true | $false> -AgentLogMaxAge <dd.hh:mm:ss> -AgentLogMaxDirectorySize <Size> -AgentLogMaxFileSize <Size> -AgentLogPath <LocalFilePath>

此範例會設定名為 Mailbox01 的 Mailbox server 的下列代理程式記錄檔設定：

  -  
    將 D:\\Anti-Spam 代理程式記錄檔位置的代理程式記錄檔。請注意是否資料夾不存在，它會為您建立。

  -  
    將代理程式日誌檔的最大大小設定為 20 MB。

  -  
    將代理程式記錄目錄的最大大小設定為 400 MB。

  -  
    將代理程式日誌檔的最大保留天數設定為 14 天。

<!-- end list -->

    Set-TransportService Mailbox01 -AgentLogPath "D:\Anti-Spam Agent Log" -AgentLogMaxFileSize 20MB -AgentLogMaxDirectorySize 400MB -AgentLogMaxAge 14.00:00:00

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
<li><p>如果您<em>AgentLogPath</em>參數設定為值<code>$null</code>，則有效停用代理程式記錄。不過，如果您設<em>AgentLogPath</em><code>$null</code><code>$true</code><em>AgentLogEnabled</em>參數的值時，會產生事件記錄檔錯誤。若要停用代理程式記錄的慣用的方法是設為<code>$false</code><em>AgentLogEnabled</em> 。</p></li>
<li><p>將 <em>AgentLogMaxAge</em> 參數設定為 <code>00:00:00</code> 值，可防止因保留天數之故而自動移除代理程式記錄檔。</p></li>
</ul></td>
</tr>
</tbody>
</table>


如需詳細的語法及參數資訊，請參閱[Set-TransportService](https://technet.microsoft.com/zh-tw/library/jj215682\(v=exchg.150\))中的 *AgentLog* 參數。

## 如何才能了解這是否正常運作？

若要確認您是否成功設定反垃圾郵件代理程式記錄，請執行下列操作：

1.  在命令介面中，執行下列命令：
    
        Get-TransportService <ServerIdentity> | Format-List AgentLog*

2.  請確認顯示的值是您所設定的值。

