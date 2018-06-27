---
title: 'Exchange 2013 已中止的功能: Exchange 2013 Help'
TOCTitle: Exchange 2013 已中止的功能
ms:assetid: 0ac0001c-b314-4108-b895-d9c0e271b489
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ619283(v=EXCHG.150)
ms:contentKeyID: 50472528
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013 已中止的功能

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

本主題討論 Microsoft Exchange Server 2013 中已移除、終止或取代的元件或功能。

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
<td>您也可能對下列主題感興趣：
<ul>
<li><p><a href="what-s-new-in-exchange-2013-exchange-2013-help.md">Exchange 2013 的新功能</a>  Exchange Server 2013 中的全新特點與功能資訊。</p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=267479">Exchange 2013 的開發人員藍圖</a>   請參閱 「 開發技術自 Exchange 中移除？Exchange 2013中已終止的 API 與開發功能的相關資訊 」 一節。</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Exchange 2010 到 Exchange 2013 已終止的功能

此章節將列出 Exchange 2013 不再提供使用的 Exchange Server 2010 功能。

## 架構


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>備註與補償方式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Hub Transport server role</p></td>
<td><p>Hub Transport server role 已由 Mailbox 和 Client Access server role 上執行的傳輸服務取代。Mailbox server role 包括 Microsoft Exchange 傳輸、Microsoft Exchange 信箱傳輸傳遞和 Microsoft Exchange 信箱傳輸提交服務。Client Access server role 包括 Microsoft Exchange 前端傳輸服務。如需詳細資訊，請參閱<a href="mail-flow-exchange-2013-help.md">郵件流程</a>。</p></td>
</tr>
<tr class="even">
<td><p>Unified Messaging server role</p></td>
<td><p>Unified Messaging server role 已由 Mailbox 和 Client Access server role 上執行的整合通訊服務取代。Mailbox server role 包括 Microsoft Exchange 整合通訊服務，而 Client Access server role 則包括 Microsoft Exchange 整合通訊呼叫路由器服務。如需詳細資訊，請參閱<a href="voice-architecture-changes-exchange-2013-help.md">語音的結構變更</a>。</p></td>
</tr>
</tbody>
</table>


## 管理介面


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>備註與補償方式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 管理主控台與 Exchange 控制台</p></td>
<td><p>Exchange 管理主控台與 Exchange 控制台已由 Exchange 系統管理中心 (EAC) 取代。EAC 與 Exchange 控制台使用相同的虛擬目錄 (/ecp)。如需詳細資訊，請參閱 <a href="exchange-admin-center-in-exchange-2013-exchange-2013-help.md">Exchange 2013 中的 Exchange 系統管理中心</a>。</p></td>
</tr>
</tbody>
</table>


## 用戶端存取


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>備註與補償方式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>不支援 Outlook 2003</p></td>
<td><p>若要將 Microsoft Outlook 連接至 Exchange 2013，需使用自動探索服務。不過，Microsoft Outlook 2003 不支援使用自動探索服務。</p></td>
</tr>
<tr class="even">
<td><p>Outlook 用戶端的 RPC/TCP 存取</p></td>
<td><p>在 Exchange 2013 中，Microsoft Outlook 用戶端可使用 Exchange 2013 Service Pack 1 或 Outlook 2013 Service Pack 1 和更新版本中的 Outlook 無所不在 (RPC/HTTP) 或 MAPI over HTTP 來連線。如果組織中有 Outlook 用戶端，則需要使用 Outlook 無所不在及/或 HTTP over MAPI。如需詳細資訊，請參閱<a href="outlook-anywhere-exchange-2013-help.md">Outlook 無所不在</a>及<a href="mapi-over-http-exchange-2013-help.md">MAPI over HTTP</a>。</p></td>
</tr>
</tbody>
</table>


## Outlook Web App 及 Outlook


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>備註與補償方式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>拼字檢查</p></td>
<td><p>Outlook Web App 不再提供內建拼字檢查服務，而會改為使用網頁瀏覽器中的拼字檢查功能。</p></td>
</tr>
<tr class="even">
<td><p>可自訂的篩選器</p></td>
<td><p>Outlook Web App 不再具有可自訂的篩選檢視，也不再支援將篩選檢視儲存至 [我的最愛]。可自訂的篩選器已由固定篩選器取代，這些固定篩選器可用來檢視所有郵件、未閱讀的郵件、已傳送給使用者的郵件，或已標示的郵件。</p></td>
</tr>
<tr class="odd">
<td><p>郵件標幟</p></td>
<td><p>Outlook Web App 中無法在郵件標幟上設定自訂日期。您可以使用 Outlook 設定自訂日期。</p></td>
</tr>
<tr class="even">
<td><p>聊天連絡人清單</p>
<p></p></td>
<td><p>Outlook Web App for Exchange 2010 的資料夾清單中所出現的聊天連絡人清單不再可用。</p></td>
</tr>
<tr class="odd">
<td><p>搜尋資料夾</p></td>
<td><p>Outlook Web App 中目前無法讓使用者使用 [搜尋] 資料夾。</p></td>
</tr>
</tbody>
</table>


## 郵件流程


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>備註與補償方式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>連結的連接器</p></td>
<td><p>連接傳送連接器與接收連接器的能力已被移除。尤其，<em>LinkedReceiveConnector</em> 參數已自 <a href="https://technet.microsoft.com/zh-tw/library/aa998936(v=exchg.150)">New-SendConnector</a> 及 <a href="https://technet.microsoft.com/zh-tw/library/aa998294(v=exchg.150)">Set-SendConnector</a> 移除。</p></td>
</tr>
</tbody>
</table>


## 反垃圾郵件和反惡意程式碼


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>備註與補償方式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>在 EMC 中得的反垃圾郵件代理程式管理</p></td>
<td><p>在 Exchange 2010 中，當您已於 Hub Transport Server 上啟動反垃圾郵件代理程式時，您可以在 Exchange 管理主控台 (EMC) 中管理反垃圾郵件代理程式。在 Exchange 2013 中，當您在 Mailbox Server 上啟用反垃圾郵件代理程式時，您無法使用 EAC 來管理代理程式。您僅能使用命令介面。如需了解如何在 Mailbox server 啟用反垃圾郵件代理程式，請參閱 <a href="enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md">啟用信箱伺服器上的反垃圾郵件功能</a>。</p></td>
</tr>
<tr class="even">
<td><p>Hub Transport 伺服器上的連接篩選代理程式</p></td>
<td><p>在 Exchange 2010 中，當您已於 Hub Transport Server 上啟動反垃圾郵件代理程式時，附件篩選代理程式是唯一無法使用的反垃圾郵件代理程式。在 Exchange 2013 中，當您在 Mailbox Server 上啟用反垃圾郵件代理程式時，無法使用附件篩選器代理程式與連接篩選代理程式。連接篩選代理程式提供 IP 允許清單與 IP 封鎖清單功能。如需了解如何在 Mailbox server 啟用反垃圾郵件代理程式，請參閱 <a href="enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md">啟用信箱伺服器上的反垃圾郵件功能</a>。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您無法在 Exchange 2013 Client Access Server 上啟用反垃圾郵件代理程式。因此，取得連線篩選代理程式的唯一方法，就是在周邊網路中安裝 Edge Transport Server。如需詳細資訊，請參閱＜<a href="edge-transport-servers-exchange-2013-help.md">Edge Transport Server</a>＞。</td>
</tr>
</tbody>
</table>

</td>
</tr>
</tbody>
</table>


## 郵件原則及符合性


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>備註與補償方式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>受管理的資料夾</p></td>
<td><p>在Exchange 2010，您可以使用受管理的資料夾通訊保留管理 (MRM)。在Exchange 2013、 受管理的資料夾不受支援。您必須使用保留原則的 MRM。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>與受管理的資料夾相關的指令程式仍然可用。您可建立受管理的資料夾、受管理的內容設定與受管理的資料夾信箱原則，並將受管理的資料夾信箱原則套用至一位使用者，但是 MRM 助理員會略過已套用受管理的資料夾信箱原則的信箱之處理程序。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p>連接埠受管理的資料夾精靈</p></td>
<td><p>在 Exchange 2010 中，您使用 連接埠受管理的資料夾精靈來建立受管理資料夾與受管理內容設定上的保留標記。在 Exchange 2013 中，Exchange 系統管理中心不包含此功能。您可以搭配使用 <strong>New-RetentionPolicyTag</strong> 指令程式與 <em>ManagedFolderToUpgrade</em> 參數，來根據受管理的資料夾建立保留標記。</p></td>
</tr>
</tbody>
</table>


## 整合通訊及語音信箱


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>備註與補償方式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>使用自動語音辨識 (ASR) 進行目錄查閱</p></td>
<td><p>在 Exchange 2010 中，Outlook Voice Access 使用者可以透過自動語音辨識 (ASR) 進行語音輸入，以搜尋目錄中列示的使用者。語音輸入也可用於在 Outlook Voice Access 中瀏覽功能表、郵件和其他選項。但是，即使 Outlook Voice Access 使用者能夠進行語音輸入，他們仍然必須使用電話按鍵來輸入其 PIN 碼及瀏覽個人選項。</p>
<p>在 Exchange 2013 中，已經驗證和未經驗證的 Outlook Voice Access 使用者無法使用任何語言的語音輸入或 ASR 來搜尋目錄中的使用者。不過，來電者被轉到自動語音應答後，可以使用多種語言的語音輸入來瀏覽自動語音應答功能表以及搜尋目錄中的使用者。</p></td>
</tr>
</tbody>
</table>


## 工具


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>備註與補償方式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Best Practice Analyzer</p></td>
<td><p>在Exchange 2010、 Exchange 最佳作法分析程式檢查您的 Exchange 部署並決定組態是否與 Microsoft 的最佳作法。在Exchange 2013、 Exchange 最佳作法分析程式已被取代<a href="https://go.microsoft.com/fwlink/p/?linkid=391077">Office 365 最佳做法分析程式 Exchange Server 2013</a>。</p></td>
</tr>
<tr class="even">
<td><p>郵件流程疑難排解員</p></td>
<td><p>在 Exchange 2010 中，郵件流程疑難排解員協助您進行一般郵件流程問題的疑難排解。在 Exchange 2013 中，郵件流程疑難排解員已遭淘汰。您現在可以使用 Exchange 2013 中 EAC 的郵件追蹤功能。如需詳細資訊，請參閱 <a href="track-messages-with-delivery-reports-exchange-2013-help.md">使用傳遞回報追蹤郵件</a>。</p></td>
</tr>
<tr class="odd">
<td><p>效能監視器</p></td>
<td><p>在 Exchange 2010 中，效能監視器內含於 Exchange 工具箱中，可收集關於郵件系統的效能資訊。效能監視器一般是用來在疑難排解效能問題時檢視重要參數。在 Exchange 2013 中，效能監視器已自工具箱中淘汰。您仍然可在 Windows Server 2008 的 <strong>[系統管理工具]</strong> 下找到效能監視器。</p></td>
</tr>
<tr class="even">
<td><p>效能疑難排解員</p></td>
<td><p>在 Exchange 2013 中，效能疑難排解員已遭淘汰。</p></td>
</tr>
<tr class="odd">
<td><p>路由記錄檢視器</p></td>
<td><p>在 Exchange 2013 中，路由記錄檢視器已遭淘汰。</p></td>
</tr>
</tbody>
</table>


## 信箱資料庫副本


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>備註與補償方式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Update-MailboxDatabaseCopy</p></li>
<li><p>更新信箱資料庫副本精靈</p></li>
</ul></td>
<td><p>植入內容索引類別目錄已不再可能複寫網路;只可以透過 MAPI 網路完成。即使您可以將 Update-mailboxdatabasecopy 指令程式<code>-Network</code>參數也是如此。</p></td>
</tr>
</tbody>
</table>


## Exchange 2007 到 Exchange 2013 已終止的功能

此章節將列出 Exchange 2013 不再提供使用的 Exchange Server 2007 功能。

## API 及開發


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>備註與補償方式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange WebDAV</p></td>
<td><p>使用<a href="https://go.microsoft.com/fwlink/p/?linkid=167197">Exchange Web 服務</a>或<a href="https://go.microsoft.com/fwlink/p/?linkid=157179">EWS Managed API</a>。或者，您可以維護使用 WebDAV 應用程式所管理之信箱的Exchange 2007伺服器。如需詳細資訊，請參閱 ＜ <a href="https://go.microsoft.com/fwlink/p/?linkid=169474">Migrating from WebDAV</a>。</p></td>
</tr>
</tbody>
</table>


## 架構


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>備註與補償方式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>儲存群組</p></td>
<td><p>Exchange 2013 不再使用儲存群組建構，您只需要管理信箱資料庫。如需詳細資訊，請參閱＜<a href="manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md">管理 Exchange 2013 中的信箱資料庫</a>＞。</p></td>
</tr>
<tr class="even">
<td><p>可延伸儲存引擎 (ESE) 資料流備份 API</p></td>
<td><p>Exchange 2013 只支援 Exchange 感知的磁碟區陰影複製服務 (VSS) 型備份。Exchange 2013 包含 Windows Server Backup 的外掛程式，可讓您備份及還原資料。如需詳細資訊，請參閱<a href="backup-restore-and-disaster-recovery-exchange-2013-help.md">備份、還原和嚴重損壞修復</a>。</p></td>
</tr>
<tr class="odd">
<td><p>使用者資料包通訊協定 (UDP) 通知</p></td>
<td><p>Exchange 2013 中已移除對使用者資料包通訊協定 (UDP) 通知的支援。這會影響當 Outlook 2003 用戶端連線到其在 Exchange 2013 伺服器上的信箱時的使用者經驗。如需詳細資訊，請參閱 Microsoft 知識庫文章 2009942：<a href="http://go.microsoft.com/fwlink/?linkid=3052%26kbid=2009942">當 Exchange Server 2010 使用者在線上模式使用 Outlook 2003 時，資料夾的更新時間過長</a>。</p></td>
</tr>
</tbody>
</table>


## 高可用性


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>備註與補償方式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>叢集連續複寫 (CCR)</p></td>
<td><p>Exchange 2013 會使用資料庫可用性群組 (DAG) 及信箱資料庫副本。如需詳細資訊，請參閱<a href="high-availability-and-site-resilience-exchange-2013-help.md">高可用性和站台恢復</a>。</p></td>
</tr>
<tr class="even">
<td><p>本機連續複寫 (LCR)</p></td>
<td><p>Exchange 2013 會使用 DAG 及信箱資料庫副本。如需詳細資訊，請參閱<a href="high-availability-and-site-resilience-exchange-2013-help.md">高可用性和站台恢復</a>。</p></td>
</tr>
<tr class="odd">
<td><p>待命連續複寫 (SCR)</p></td>
<td><p>Exchange 2013 會使用 DAG 及信箱資料庫副本。如需詳細資訊，請參閱<a href="high-availability-and-site-resilience-exchange-2013-help.md">高可用性和站台恢復</a>。</p></td>
</tr>
<tr class="even">
<td><p>單一複本叢集 (SCC)</p></td>
<td><p>Exchange 2013 會使用 DAG 及信箱資料庫副本。如需詳細資訊，請參閱<a href="high-availability-and-site-resilience-exchange-2013-help.md">高可用性和站台恢復</a>。</p></td>
</tr>
<tr class="odd">
<td><p>Setup /recoverCMS</p></td>
<td><p>Exchange 2013 會使用 Setup /m:recoverServer。如需詳細資訊，請參閱<a href="recover-an-exchange-server-exchange-2013-help.md">復原 Exchange Server</a>。</p></td>
</tr>
<tr class="even">
<td><p>叢集信箱伺服器</p></td>
<td><p>Exchange 2013 會使用 DAG 及信箱資料庫副本。如需詳細資訊，請參閱<a href="high-availability-and-site-resilience-exchange-2013-help.md">高可用性和站台恢復</a>。</p></td>
</tr>
</tbody>
</table>


## 用戶端存取


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>備註與補償方式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>使用整合式 Windows 驗證 (NTLM) 進行 POP3 和 IMAP4 使用者的用戶端驗證</p></td>
<td><p>NTLM 不支援在Exchange 2013的 POP3 或 IMAP4 用戶端連線。使用 NTLM 的 POP3 或 IMAP4 用戶端程式的連線將會失敗。如果您正在執行Exchange 2013RTM 版本，建議的替代項為 NTLM 是使用純文字驗證與 SSL。</p>
<p>如果您使用的是 Exchange 2013，若要使用 NTLM，您必須在您的 Exchange 2007 組織中保留 Exchange 2013 伺服器。</p></td>
</tr>
</tbody>
</table>


## Outlook Web App 及 Outlook


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>備註與補償方式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>文件存取</p></td>
<td><p>Outlook Web App 無法用於存取 Microsoft SharePoint 文件庫與 Windows 檔案共享。</p></td>
</tr>
<tr class="even">
<td><p>郵件標幟</p></td>
<td><p>Outlook Web App 2013 中不提供在郵件標幟上設定自訂日期的功能。您可以使用 Outlook 設定自訂日期。</p></td>
</tr>
<tr class="odd">
<td><p>拼字檢查</p></td>
<td><p>Outlook Web App 使用網頁瀏覽器中的拼字檢查功能。</p></td>
</tr>
<tr class="even">
<td><p>搜尋資料夾</p></td>
<td><p>Outlook Web App 中目前無法讓使用者使用 [搜尋] 資料夾。</p></td>
</tr>
<tr class="odd">
<td><p>最大快取檢視</p></td>
<td><p>Exchange 2007 支援的 Outlook 用戶端修改每資料庫 (msExchMaxCachedViews) 參數的快取檢視數目上限。Exchange 2013 不再使用此參數。</p></td>
</tr>
</tbody>
</table>


## 收件者相關功能


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>備註與補償方式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Export-Mailbox</strong> 與 <strong>Import-Mailbox</strong> 指令程式</p></td>
<td><p>在 Exchange 2013 中，使用匯出要求或匯入要求。如需詳細資訊，請參閱 <a href="mailbox-import-and-export-requests-exchange-2013-help.md">信箱匯入及匯出要求</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>Move-Mailbox</strong> 指令程式集</p></td>
<td><p>在 Exchange 2013 中，使用移動要求來移動信箱。如需詳細資訊，請參閱<a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">在 Exchange 2013 移動信箱</a>。</p></td>
</tr>
<tr class="odd">
<td><p>ISInteg</p></td>
<td><p>在 Exchange 2013 中，使用 <a href="https://technet.microsoft.com/zh-tw/library/ff625226(v=exchg.150)">New-MailboxRepairRequest</a>。</p></td>
</tr>
</tbody>
</table>


## 郵件原則及符合性


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>備註與補償方式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>受管理的資料夾</p></td>
<td><p>在 Exchange 2007 中，您為郵件保留受管理 (MRM) 使用受管理的資料夾。Exchange 2013 中不支援受管理的資料夾。MRM 必須使用保留原則。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>與受管理的資料夾相關的指令程式仍然可用。您可建立受管理的資料夾、受管理的內容設定與受管理的資料夾信箱原則，並將受管理的資料夾信箱原則套用至一位使用者，但是 MRM 助理員會略過已套用受管理的資料夾信箱原則的信箱之處理程序。</td>
</tr>
</tbody>
</table>

</td>
</tr>
</tbody>
</table>


## 整合通訊及語音信箱


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>備註與補償方式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>使用 Outlook Voice Access 的自動語音辨識 (ASR) 進行目錄查閱</p></td>
<td><p>在 Exchange 2007 中，Outlook Voice Access 使用者可以透過自動語音辨識 (ASR)，以美式英文 (en-US) 的語音輸入，搜尋目錄中列示的使用者。語音輸入也可用於在 Outlook Voice Access 中瀏覽功能表、郵件和其他選項。但是，即使 Outlook Voice Access 使用者能夠進行語音輸入，他們仍然必須使用電話按鍵來輸入其 PIN 碼及瀏覽個人選項。</p>
<p>在 Exchange 2013 中，已經驗證和未經驗證的 Outlook Voice Access 使用者無法使用任何語言的語音輸入或 ASR 來搜尋目錄中的使用者。不過，來電者被轉到自動語音應答後，可以使用多種語言的語音輸入來瀏覽自動語音應答功能表以及搜尋目錄中的使用者。</p></td>
</tr>
</tbody>
</table>

