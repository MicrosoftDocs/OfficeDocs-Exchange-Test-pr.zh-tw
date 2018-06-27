---
title: 'POP3 與 IMAP4 通訊協定記錄: Exchange 2013 Help'
TOCTitle: POP3 與 IMAP4 通訊協定記錄
ms:assetid: 212ed3d5-0c98-4346-a860-1cfcac5d73c4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd335141(v=EXCHG.150)
ms:contentKeyID: 50553954
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# POP3 與 IMAP4 通訊協定記錄

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

您可以使用通訊協定記錄檢閱Exchange環境中的 POP3 和 IMAP4 連線。這可以是如果您正在進行疑難排解相關 POP3 或 IMAP4 的效能問題。

## 啟用 POP3 與 IMAP4 通訊協定記錄

您可以啟用、 停用或變更使用Exchange管理命令介面的通訊協定記錄。如果您啟用通訊協定記錄使用命令介面，將會使用預設通訊協定記錄設定。在大多數情況下，將足夠的預設設定。

或者，您可以啟用、 停用及修改通訊協定記錄選項來編輯 Microsoft.Exchange.Pop3.exe.config 和 Microsoft.Exchange.Imap4.exe.config 設定檔位於您MicrosoftExchange Server 2013 Client Access server。如需如何管理 POP3 與 IMAP4 通訊協定設定的詳細資訊，請參閱[設定 POP3 與 IMAP4 通訊協定記錄](configure-protocol-logging-for-pop3-and-imap4-exchange-2013-help.md)。

## 檢閱通訊協定記錄檔

通訊協定記錄檔為文字檔包含逗點分隔值 (CSV) 檔案格式的資料。通訊協定記錄檔會儲存在單一行上的每個通訊協定事件。 儲存在每行上的資訊被依據的欄位。 這些欄位用逗號隔開。下表說明用來分類每個通訊協定事件的欄位。

### 用於分類各通訊協定事件的欄位

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>欄位名稱</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>date-time</p></td>
<td><p>日期和通訊協定事件的時間。此值會格式化為<em>yyyy-mm-ddhh:mm:ss.fffZ</em>，其中<em>yyyy</em> = year， <em>mm</em> = 月、 <em>dd</em> = 日、 <em>hh</em> = 小時、 <em>mm</em> = 分鐘、 <em>ss</em> = 第二、 <em>fff</em> = 分數的第二、 和<em>Z</em>代表祖魯文。祖魯文是另一種方式來指出國際標準時間 (UTC)。</p></td>
</tr>
<tr class="even">
<td><p>連接器識別碼</p></td>
<td><p>此欄位不會使用 POP3 與 IMAP4 通訊協定記錄。</p></td>
</tr>
<tr class="odd">
<td><p>工作階段識別碼</p></td>
<td><p>唯一識別 SMTP 工作階段與通訊協定事件相關聯的 GUID。</p></td>
</tr>
<tr class="even">
<td><p>序號-</p></td>
<td><p>效能計數器的開始 0，而在相同的工作階段中每個事件會遞增。</p></td>
</tr>
<tr class="odd">
<td><p>本機端點</p></td>
<td><p>本機 POP3 或 IMAP4 的工作階段結束點。這個項目包含的 IP 位址和 TCP 連接埠號碼，格式如下： <em>&lt;IP address&gt;</em>:<em>&lt;port&gt;</em>。</p></td>
</tr>
<tr class="even">
<td><p>遠端端點</p></td>
<td><p>POP3 或 IMAP4 的工作階段之遠端端點。這個項目包含的 IP 位址和 TCP 連接埠號碼，格式如下： <em>&lt;IP address&gt;</em>:<em>&lt;port&gt;</em>。</p></td>
</tr>
<tr class="odd">
<td><p>事件</p></td>
<td><p>單一字元代表通訊協定事件。此事件的可能值如下：</p>
<ul>
<li><p>+   Connect</p></li>
<li><p>-   Disconnect</p></li>
<li><p>&gt; 傳送</p></li>
<li><p>&lt; 接收</p></li>
<li><p>*   資訊</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>資料</p></td>
<td><p>文字有相關聯的 POP3 或 IMAP4 事件的資訊。</p></td>
</tr>
<tr class="odd">
<td><p>快顯</p></td>
<td><p>此欄位不會使用 POP3 與 IMAP4 通訊協定記錄。</p></td>
</tr>
</tbody>
</table>

