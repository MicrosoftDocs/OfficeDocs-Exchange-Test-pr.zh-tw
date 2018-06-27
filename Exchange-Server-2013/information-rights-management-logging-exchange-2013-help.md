---
title: '資訊版權管理記錄: Exchange 2013 Help'
TOCTitle: 資訊版權管理記錄
ms:assetid: e06f57f9-a9e2-43a2-b88c-288b324d71f0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ff461940(v=EXCHG.150)
ms:contentKeyID: 50474409
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 資訊版權管理記錄

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

在 Microsoft Exchange Server 2013、 資訊版權管理 (IRM) 作業會記錄 IRM 記錄檔中。IRM 記錄檔可協助您監視及疑難排解Exchange 2013伺服器上的 Rights Management Services (RMS) 用戶端與您組織中的Active Directory Rights Management Services (AD RMS) 叢集間的互動。

若要深入了解 IRM，請參閱[資訊版權管理](information-rights-management-exchange-2013-help.md)。

**目錄**

IRM 記錄檔的結構

記錄程序

IRM 記錄檔寫入的資訊

管理 IRM 記錄

要尋找與 IRM 相關的管理工作嗎？ 請參閱 [資訊版權管理程序](information-rights-management-procedures-exchange-2013-help.md)。

## IRM 記錄檔的結構

依預設，IRM 記錄位於 C:\\Program Files\\Microsoft\\Exchange Server\\V14\\Logging\\IRMLogs 中。

IRM 記錄檔的命名慣例為 \<*Process*\>\_\<*Process identifier* 或 *IIS AppPool identifier*\>\_IRMLOG*yyyymmdd*-*nnnn*.log，其中：

  - \<*Process*\>= 建立記錄檔的程序。例如上傳輸服務，這會是 EdgeTransport。

  - \<*Process identifier* 或 *IIS AppPool identifier\>* =程序的數值 ID。

  - *yyyymmdd* = 建立記錄檔的國際標準時間 (UTC) 日期。

  - *nnnn* = 從 1 開始且代表每一天的執行個體號碼。

IRM 記錄檔的名稱範例為 EdgeTransport\_1056\_IRMLOG20101201-1.log。

下表顯示在不同伺服器角色上產生的記錄。

### 伺服器角色上的記錄

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>伺服器角色</th>
<th>IRM 記錄檔名稱</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Transport 服務</p></td>
<td><p>EdgeTransport_&lt;<em>Process identifier</em>&gt;_IRMLOG<em>yyyymmdd</em>-<em>nnnn</em>.log</p></td>
<td><p>此記錄來記錄上傳輸服務 （例如傳輸保護規則及日誌報告解密） 傳輸管線所做的所有 RMS 交易。Edgetransport.exe 處理程序的程序識別碼 (PID) 用來產生記錄檔名。</p></td>
</tr>
<tr class="even">
<td><p>信箱</p></td>
<td><p>msftefd_&lt;<em>Process identifier</em>&gt;_IRMLOG<em>yyyymmdd</em>-<em>nnnn</em>.log</p></td>
<td><p>此記錄來記錄搜尋及索引要求期間所發生的所有 RMS 交易。Exchange 2013信箱伺服器為內容編製索引使用 msftefd.exe 程序。Msftefd.exe 程序的 PID 用來產生記錄檔名。</p></td>
</tr>
<tr class="odd">
<td><p>用戶端存取</p></td>
<td><p>w3wp_MSExchangeOWAAppOol_IRMLOG<em>yyyymmdd</em>-<em>nnnn</em>.log</p></td>
<td><p>此記錄可用來記錄 Microsoft OfficeOutlook Web App 中 IRM 的所有交易。</p></td>
</tr>
<tr class="even">
<td><p>所有Exchange 2013伺服器角色</p></td>
<td><p>w3wp_MSExchangePowerShellAppPool_IRMLOG<em>yyyymmdd</em>-<em>nnnn</em>.log</p></td>
<td><p>此記錄可用來記錄從 Windows PowerShell 發出的所有 IRM RMS 交易，例如在發出 <strong>Test-IRMConfiguration</strong> 指令程式時。</p></td>
</tr>
</tbody>
</table>


回到頁首

## 記錄程序

資訊會寫入記錄檔中，直到檔案大小達到指定的上限值為止。 達到大小上限時，會建立具有遞增執行個體號碼的記錄檔。 這個程序會在一天當中不斷地重複。 IRM 記錄目錄達到指定的大小上限時，或記錄檔達到每個伺服器上 IRM 組態所指定的最大保留天數時，循環記錄就會刪除最舊的記錄檔。

回到頁首

## IRM 記錄檔寫入的資訊

IRM 記錄檔是包含逗號分隔 (CSV) 格式資料的文字檔。 每個 IRM 記錄都具有包含下列資訊的標頭：

  - **\#Software** 建立 IRM 記錄檔的軟體名稱。 一般來說，這個值為 `Microsoft Exchange Server`。

  - **\#Version** 建立 IRM 記錄檔的軟體版本號碼。

  - **\#Log-type** 記錄類型值，即 `Rms Client Manager Log`。

  - **\#Date** 建立記錄檔的 UTC 日期和時間。 以 ISO 8601 日期及時間格式表示 UTC 日期和時間： *yyyy*-*mm*-*dd*T*hh*:*mm*:*ss.fff*Z，其中：
    
      - yyyy = 年
    
      - *mm* = 月
    
      - *dd* = 日
    
      - T = 用來顯示時間元件開始的時間指示項
    
      - *hh* = 時
    
      - *mm* = 分
    
      - *ss* = 秒
    
      - *fff* = 秒的分數
    
      - Z = Zulu，表示另一種指出 UTC 的方法

  - **\#Fields** 在 IRM 記錄檔中所使用的以逗點分隔的欄位名稱。
    
    在 IRM 記錄中，每筆 RMS 交易事件會各存一行，並以逗號分隔欄位。 下表列出 IRM 記錄中的欄位，各代表已啟用 IRM 功能的所有伺服器角色。
    
    ### IRM 記錄中使用的欄位
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>欄位</th>
    <th>描述</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>Date-time</strong></p></td>
    <td><p>列出 UTC 時間戳記。</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Feature</strong></p></td>
    <td><p>列出使用的 RMS 用戶端功能。 有效值包括：</p>
    <ul>
    <li><p><code>RacClc</code></p></li>
    <li><p><code>Template</code></p></li>
    <li><p><code>Prelicense</code></p></li>
    <li><p><code>UseLicense</code></p></li>
    <li><p>簽章驗證</p></li>
    <li><p><code>ServerInfo</code></p></li>
    </ul></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Event-Type</strong></p></td>
    <td><p>列出事件類型。 有效值包括：</p>
    <ul>
    <li><p><code>Acquire</code> 要求 RMS 授權或範本。</p></li>
    <li><p><code>Success</code> 成功取得 RMS 授權或範本。</p></li>
    <li><p><code>Exception</code> 發生錯誤。</p></li>
    <li><p><code>Queued</code> 要求擱置中。</p></li>
    </ul></td>
    </tr>
    <tr class="even">
    <td><p><strong>Tenant-Id</strong></p></td>
    <td><p>保留供 Microsoft 內部使用。</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Server-url</strong></p></td>
    <td><p>列出作業期間存取的 RMS 伺服器 URL。</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Context</strong></p></td>
    <td><p>由呼叫程序使用，將多個 RMS 交易繫結在一起。 有效值包括：</p>
    <ul>
    <li><p><code>MessageID: &lt;Actual message ID&gt;</code></p></li>
    <li><p><code>MailboxGuid: &lt;Mailbox GUID&gt;</code></p></li>
    <li><p><code>AttachmentFileName: &lt;File name&gt;</code></p></li>
    </ul></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Transaction-id</strong></p></td>
    <td><p>識別唯一的交易。 在同一個交易期間發生的所有事件都具有相同的交易 ID。</p></td>
    </tr>
    </tbody>
    </table>


回到頁首

## 管理 IRM 記錄

在每個啟用 IRM 功能的伺服器角色上，依預設會啟用 IRM 記錄。 針對每個伺服器角色，您可以使用伺服器角色的對應 **Set** 指令程式來修改下列 IRM 組態。 例如，若要在郵件伺服器上設定 IRM 記錄，請使用 **Set-MailboxServer** 指令程式。

### IRM 記錄的組態參數

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>參數</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>IrmLogEnabled</em></p></td>
<td><p>啟用 IRM 交易的記錄。 預設會啟用 IRM 記錄。 若要停用伺服器角色的 IRM 記錄，請將參數設為 <code>$false</code>。</p></td>
</tr>
<tr class="even">
<td><p><em>IrmLogMaxAge</em></p></td>
<td><p>指定 IRM 記錄檔的最長使用期限。 比指定使用期限舊的檔案會遭到刪除。 預設值是 <code>30.00:00:00</code> (30 天)。</p></td>
</tr>
<tr class="odd">
<td><p><em>IrmLogMaxDirectorySize</em></p></td>
<td><p>指定連線記錄檔目錄中所有 IRM 記錄檔的大小上限。 目錄達到檔案大小上限時，伺服器會先刪除最舊的記錄檔。 預設值為 <code>250 MB</code>。</p></td>
</tr>
<tr class="even">
<td><p><em>IrmLogMaxFileSize</em></p></td>
<td><p>指定單一記錄檔的大小上限。 當檔案達到指定的大小時，會建立一個記錄檔，且執行個體號碼會遞增。 預設值為 <code>10 MB</code>。</p></td>
</tr>
<tr class="odd">
<td><p><em>IrmLogPath</em></p></td>
<td><p>會指定 IRM 記錄檔位置。預設路徑為 %exchangeinstallpath%logging\irmlogs。</p></td>
</tr>
</tbody>
</table>


如需詳細的語法及參數資訊，請參閱下列主題：

  - [Set-MailboxServer](https://technet.microsoft.com/zh-tw/library/aa998651\(v=exchg.150\))

  - [Set-ClientAccessServer](https://technet.microsoft.com/zh-tw/library/bb125157\(v=exchg.150\))

  - [Set-TransportService](https://technet.microsoft.com/zh-tw/library/jj215682\(v=exchg.150\))

回到頁首

