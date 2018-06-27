---
title: '通訊協定記錄: Exchange 2013 Help'
TOCTitle: 通訊協定記錄
ms:assetid: 40da446b-bcc3-4a97-ace7-a54f6ddebd79
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa997624(v=EXCHG.150)
ms:contentKeyID: 50473011
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 通訊協定記錄

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

通訊協定記錄會記錄郵件傳遞的一部分的郵件伺服器之間發生的 SMTP 交談。傳送連接器和用戶端存取伺服器、 信箱伺服器上的傳輸服務及 Mailbox server 上的 Mailbox Transport service 的前端傳輸服務中存在的接收連接器上發生這些 SMTP 交談。您可以使用通訊協定記錄診斷郵件流程問題。

根據預設，會停用所有的傳送連接器和接收連接器上的通訊協定記錄。通訊協定記錄是啟用還是停用每個個別的連接器。其他通訊協定記錄選項所設定的所有接收連接器或每個個別伺服器上傳輸服務中存在的所有傳送連接器。傳輸服務中的所有接收連接器都共用相同的通訊協定記錄檔和通訊協定記錄檔選項。這些通訊協定記錄檔和通訊協定記錄檔選項是分開的傳送連接器通訊協定記錄檔和通訊協定記錄檔選項的傳輸服務中的同一部伺服器。

下列選項可供 Exchange 伺服器上個個傳輸服務的所有傳送連接器或所有接收連接器的通訊協定記錄檔使用：

  - 指定傳送連接器或接收連接器通訊協定記錄檔的位置。

  - 指定的傳送連接器\] 或 \[接收連接器通訊協定記錄檔的大小上限。預設大小為 10 mb (MB)。

  - 指定目錄包含的傳送連接器或接收連接器通訊協定記錄檔的大小上限。預設大小為 250 MB。

  - 指定保留時間上限的傳送連接器或接收連接器通訊協定記錄檔。預設存留期為 30 天。

根據預設，Exchange 會使用循環記錄以根據檔案大小與檔案保留天數來限制通訊協定記錄，藉以控制記錄檔所使用的硬碟空間

在每個信箱伺服器上的傳輸服務中與每個 Client Access server 上 Front End Transport 服務中已存在名為組織內傳送連接器的特殊傳送連接器。此連接器隱含建立，看不見，而且需要沒有管理。組織內傳送連接器會使用下列 transport 服務：

  - **在 Mailbox Server 上的運輸服務**
    
      - 轉送郵件至組織中其他 Exchange 2013 信箱伺服器上的傳輸服務以及信箱傳輸服務。
    
      - 轉送郵件至其他組織中的 Exchange 2007 或 Exchange 2010 Hub Transport Server。
    
      - 轉送郵件至周邊網路中的 Edge Transport Server。

  - **用戶端存取伺服器上的前端傳輸服務**   轉送郵件至組織中 Exchange 2013 信箱伺服器上的傳輸服務。

每個信箱伺服器上的信箱傳輸服務中存在名為信箱傳遞傳送連接器的對等傳送連接器。此連接器也隱含建立，看不見，而且需要沒有管理。信箱傳遞傳送連接器，用於轉送訊息傳輸服務，以及在組織中的其他信箱伺服器上的信箱傳輸服務。

根據預設，信箱傳遞傳送連接器通訊協定記錄也會停用。您可以啟用或停用信箱傳遞傳送連接器的通訊協定記錄**Set-MailboxTransportService**指令程式上使用*MailboxDeliveryConnectorProtocolLoggingLevel*參數。如果您啟用信箱傳遞傳送連接器通訊協定記錄，則會在 Mailbox server 上 Mailbox Transport service 的傳送連接器通訊協定記錄檔中會記錄。

**目錄**

Structure of the protocol log files

Information written to the protocol log

## 通訊協定記錄檔的結構

通訊協定記錄檔預設會存在下列位置：

  - **為信箱伺服器上的傳輸服務接收連接器通訊協定記錄檔**   %ExchangeInstallPath%TransportRoles\\Logs\\Hub\\ProtocolLog\\SmtpReceive

  - **為信箱伺服器上的信箱傳輸服務接收連接器通訊協定記錄檔**   %ExchangeInstallPath%TransportRoles\\Logs\\Mailbox\\ProtocolLog\\SmtpReceive

  - **為用戶端存取伺服器上的前端服務接收連接器通訊協定記錄檔**   %ExchangeInstallPath%TransportRoles\\Logs\\FrontEnd\\ProtocolLog\\SmtpReceive

  - **為信箱伺服器上的傳輸服務傳送器通訊協定記錄檔**   %ExchangeInstallPath%TransportRoles\\Logs\\Hub\\ProtocolLog\\SmtpSend

  - **為信箱伺服器上的信箱傳輸服務傳送連接器通訊協定記錄檔**   %ExchangeInstallPath%TransportRoles\\Logs\\Mailbox\\ProtocolLog\\SmtpSend

  - **為用戶端存取伺服器上的前端服務傳送連接器通訊協定記錄檔**   %ExchangeInstallPath%TransportRoles\\Logs\\FrontEnd\\ProtocolLog\\SmtpSend

記錄檔中的每個通訊協定記錄檔目錄的命名慣例是*prefixyyyymmdd-nnnn*。 記錄檔。預留位置表示下列資訊：

  - 預留位置 *prefix* 如果是 SEND，則代表「傳送連接器」，如果是 RECV，則代表「接收連接器」。

  - 版面配置區*yyyymmdd*是在其建立的記錄檔的國際標準時間 (UTC) 日期。版面配置區*yyyy* = year， *mm* = 月和*dd* = 日。

  - 預留位置 *nnnn* 是每天都從 1 開始的執行個體號碼。

資訊寫入記錄檔之前的檔案大小到達其最大的指定的值，並開啟新的記錄檔有依遞增的執行個體數。重複此程序在一天。循環記錄刪除舊的記錄檔當通訊協定記錄檔目錄達到指定的大小上限，或是在記錄檔達到其最大指定保留天數。

通訊協定記錄檔為文字檔包含逗點分隔值 (CSV) 檔案格式的資料。每個通訊協定記錄檔有標頭包含下列資訊：

  - **\#Software**  軟體所建立的通訊協定記錄檔的名稱。一般而言，此值為 Microsoft Exchange Server。

  - **\#Version**  建立通訊協定記錄檔的軟體版本號碼。目前的值是 15.0.0.0。

  - **\#Log-Type**   這個欄位的記錄類型值，可以是 SMTP 接收通訊協定記錄或 SMTP 傳送通訊協定記錄。

  - **\#Date**  建立記錄檔時 UTC 的日期時間。以 ISO 8601 日期時間格式表示 UTC 日期時間：*yyyy-mm-dd*T*hh:mm:ss.fff*Z，其中 *yyyy* = 年、*mm* = 月、*dd* = 日，T 表示時間元件的開頭，*hh* = 時、*mm* = 分、*ss* = 秒、*fff* = 秒的分數，以及另外一個表示 UTC 的方法 Z 代表 Zulu。

  - **\#Fields**   在通訊協定記錄檔中所使用的以逗點分隔的欄位名稱。

回到頁首

## 寫入通訊協定記錄檔的資訊

通訊協定記錄檔儲存中的通訊協定記錄檔在單一行上每個 SMTP 通訊協定事件。儲存在每行上的資訊被依據的欄位。這些欄位用逗號隔開。下表說明用來分類每個通訊協定的欄位。

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
<td><p><strong>date-time</strong></p></td>
<td><p>通訊協定事件的 UTC 日期及時間。以 ISO 8601 日期時間格式表示 UTC 日期時間：<em>yyyy-mm-dd</em>T<em>hh:mm:ss.fff</em>Z，其中 <em>yyyy</em> = 年、<em>mm</em> = 月、<em>dd</em> = 日，T 表示時間元件的開頭，<em>hh</em> = 時、<em>mm</em> = 分、<em>ss</em> = 秒、<em>fff</em> = 秒的分數，以及另外一個表示 UTC 的方法 Z 代表 Zulu。</p></td>
</tr>
<tr class="even">
<td><p><strong>connector-id</strong></p></td>
<td><p>與 SMTP 事件關聯的連接器辨別名稱 (DN)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>session-id</strong></p></td>
<td><p>對每個 SMTP 工作階段都是唯一的，但是對與該 SMTP 工作階段關聯的每個事件則都相同的 GUID。</p></td>
</tr>
<tr class="even">
<td><p><strong>sequence-number</strong></p></td>
<td><p>在相同的 SMTP 工作階段中，從 0 開始且會依每個事件而遞增的計數器。</p></td>
</tr>
<tr class="odd">
<td><p><strong>local-endpoint</strong></p></td>
<td><p>本機的 SMTP 工作階段的端點。這個項目包含的 IP 位址和 TCP 連接埠號碼格式化為<em>&lt;IP address&gt;</em>:<em>&lt;port&gt;</em>。</p></td>
</tr>
<tr class="even">
<td><p><strong>remote-endpoint</strong></p></td>
<td><p>遠端 SMTP 工作階段的端點。這個項目包含的 IP 位址和 TCP 連接埠號碼格式化為<em>&lt;IP address&gt;</em>:<em>&lt;port&gt;</em>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>event</strong></p></td>
<td><p>代表此通訊協定事件的單一字元。此事件的可能值如下：</p>
<ul>
<li><p><strong>+</strong>   Connect</p></li>
<li><p><strong>-</strong>   Disconnect</p></li>
<li><p><strong>&gt;</strong> Send</p></li>
<li><p><strong>&lt;</strong> Receive</p></li>
<li><p><strong>*</strong>   資訊</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>data</strong></p></td>
<td><p>與 SMTP 事件關聯的文字資訊。</p></td>
</tr>
<tr class="odd">
<td><p><strong>context</strong></p></td>
<td><p>可能與 SMTP 事件關聯之其他內容資訊。</p></td>
</tr>
</tbody>
</table>


單一 SMTP 交談表示傳送或接收的單一電子郵件訊息就會產生多個 SMTP 事件。這些 SMTP 事件造成通訊協定記錄檔寫入的多行。多個 SMTP 交談代表傳送或接收的多個電子郵件會同時發生。這會建立通訊協定記錄項目從不同的位置顛倒的 SMTP 交談。您可以用來排序 SMTP 交談通訊協定記錄項目使用的工作階段識別碼和順序數字欄位。

回到頁首

