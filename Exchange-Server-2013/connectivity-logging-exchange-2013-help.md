---
title: '連線記錄: Exchange 2013 Help'
TOCTitle: 連線記錄
ms:assetid: c31fd710-4ae4-4d9a-8936-d056e7ca2748
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124500(v=EXCHG.150)
ms:contentKeyID: 50474195
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 連線記錄

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

連線記錄會記錄用來傳輸訊息從 Exchange 伺服器上傳輸服務的輸出連線活動。要追蹤的個別電子郵件傳輸不是連線記錄的目的。而是連線記錄檔來追蹤連線活動從來源至目的地，不論傳送多少訊息。使用用戶端存取伺服器、 信箱伺服器上的傳輸服務及 Mailbox server 上的 Mailbox Transport service 的前端傳輸服務中連線記錄。 下列清單說明在連線記錄中的資訊類型：

  - 來源

  - Destination

  - DNS 解析資訊

  - 連線失敗的詳細資訊

  - 傳輸的郵件數及位元組數

您使用**Set-TransportService**、 **Set-FrontEndTransportService**和**Set-MailboxTransportService** cmdlet 在 Exchange 管理命令介面中執行所有連線記錄檔設定工作。下列選項都可供連線記錄檔：

  - 啟用或停用連線記錄。預設會啟用。

  - 指定連線記錄檔的位置。

  - 指定之個別連線記錄檔的大小上限。預設大小為 10 mb (MB)。

  - 指定包含連線記錄檔之目錄的大小上限。預設大小為 1000 MB。

  - 指定連線記錄檔的保留時間上限。預設存留期為 30 天。

Exchange 預設會使用循環記錄，根據檔案大小及檔案保留天數來限制連線記錄檔，以協助控制連線記錄檔所使用的硬碟空間。

**目錄**

Structure of the connectivity log files

Information written to the connectivity log

## 連線記錄檔的結構

連線記錄檔預設會位於下列位置：

  - **Transport service**   %ExchangeInstallPath%TransportRoles\\Logs\\Hub\\Connectivity

  - **Front End Transport service**   %ExchangeInstallPath%TransportRoles\\Logs\\FrontEnd\\Connectivity

  - **Mailbox Transport service**   %ExchangeInstallPath%TransportRoles\\Logs\\Mailbox\\Connectivity

連線記錄檔的命名慣例是 CONNECTLOG*yyymmdd-nnnn*。 記錄檔。預留位置表示下列資訊：

  - 版面配置區*yyyymmdd*是建立記錄檔的國際標準時間 (UTC) 日期。版面配置區*yyyy* = year， *mm* = 月和*dd* = 日。

  - 預留位置 *nnnn* 是每天都從 1 開始的執行個體號碼。

資訊寫入記錄檔之前的檔案大小到達其最大的指定的值，並開啟新的記錄檔有依遞增的執行個體數。重複此程序在一天。當連線記錄檔目錄達到指定的大小上限，或是在記錄檔達到其最大指定保留時間下限循環記錄會刪除最舊的記錄檔。

連線記錄檔為文字檔包含逗點分隔值 (CSV) 檔案格式的資料。每個連線記錄檔有標頭包含下列資訊：

  - **\#Software**  軟體所建立的連線記錄檔的名稱。一般而言，此值為 Microsoft Exchange Server。

  - **\#Version**  建立連線記錄檔的軟體版本號碼。目前的值是 15.0.0.0。

  - **\#Log-Type**   記錄檔類型值，為傳輸連線記錄。

  - **\#Date**  建立記錄檔時 UTC 的日期時間。以 ISO 8601 日期時間格式表示 UTC 日期時間：*yyyy-mm-dd*T*hh:mm:ss.fff*Z，其中 *yyyy* = 年、*mm* = 月、*dd* = 日，T 表示時間元件的開頭，*hh* = 時、*mm* = 分、*ss* = 秒、*fff* = 秒的分數，以及另外一個表示 UTC 的方法 Z 代表 Zulu。

  - **\#Fields**   連線記錄檔中所使用之以逗號分隔的欄位名稱。

回到頁首

## 寫入連線記錄檔的資訊

連線記錄檔儲存在連線記錄檔在單一行上每個輸出傳輸服務連線事件。儲存在每行上的資訊被依據的欄位。這些欄位用逗號隔開。下表說明用來分類每個傳出連線事件的欄位。

### 用於分類各連線事件的欄位

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
<td><p>UTC 的日期-時間的連線事件。以 ISO 8601 日期時間格式表示 UTC 日期時間：<em>yyyy-mm-dd</em>T<em>hh:mm:ss.fff</em>Z，其中 <em>yyyy</em> = 年、<em>mm</em> = 月、<em>dd</em> = 日，T 表示時間元件的開頭，<em>hh</em> = 時、<em>mm</em> = 分、<em>ss</em> = 秒、<em>fff</em> = 秒的分數，以及另外一個表示 UTC 的方法 Z 代表 Zulu。</p></td>
</tr>
<tr class="even">
<td><p><strong>session</strong></p></td>
<td><p>每個 SMTP 工作階段是唯一但與該 SMTP 工作階段相關聯的每個事件的相同的 GUID。MAPI 工作階段的信箱傳輸服務中，[工作階段] 欄位是空白的。</p></td>
</tr>
<tr class="odd">
<td><p><strong>source</strong></p></td>
<td><p><strong>SMTP</strong> 用於 SMTP 連線，<strong>MAPI</strong> 用於本機信箱資料庫的信箱傳輸服務連線。</p></td>
</tr>
<tr class="even">
<td><p><strong>destination</strong></p></td>
<td><p>目的地的名稱。</p></td>
</tr>
<tr class="odd">
<td><p><strong>direction</strong></p></td>
<td><p>代表開始、 middle、 或結尾之連線的單一字元。[方向] 欄位的可能值如下：</p>
<ul>
<li><p><strong>+</strong>   Connect</p></li>
<li><p><strong>-</strong>   Disconnect</p></li>
<li><p><strong>&gt;</strong>   Send</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>description</strong></p></td>
<td><p>連線事件相關聯的文字資訊。下列的值為 [描述] 欄位值的範例：</p>
<ul>
<li><p>已傳輸的郵件數及郵件大小</p></li>
<li><p>目的地網域的 DNS MX 資源記錄解析資訊</p></li>
<li><p>目的地 Mailbox Server 的 DNS 解析資訊</p></li>
<li><p>連線建立郵件</p></li>
<li><p>連線失敗郵件</p></li>
</ul></td>
</tr>
</tbody>
</table>


當傳輸服務建立的連線至目的地時的傳輸服務可能會準備傳送一封郵件或數個訊息。連線與郵件傳輸程序產生寫入連線記錄檔中的多行上的多個事件。同時連線到不同的目的地建立連線到不同的目的地交錯相關的記錄項目。不過，您可以使用日期-時間、 工作階段、 來源與方向欄位的每個個別連接從開始到完成排列連線記錄項目。

回到頁首

