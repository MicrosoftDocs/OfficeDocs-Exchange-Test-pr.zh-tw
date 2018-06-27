---
title: '陰影備援: Exchange 2013 Help'
TOCTitle: 陰影備援
ms:assetid: a40dbe61-2a18-48a8-b2e0-4e81a6678d11
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd351027(v=EXCHG.150)
ms:contentKeyID: 50473878
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 陰影備援

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

陰影備援推出於 Microsoft Exchange Server 2010提供的郵件之備援副本之前所要傳遞至信箱。在Exchange 2010，陰影備援延遲等到伺服器驗證的郵件傳遞路徑中的下一個躍點郵件刪除傳輸伺服器上的資料庫傳輸完成傳遞。如果下一個躍點失敗報告成功傳遞至傳輸伺服器之前，傳輸伺服器需重新提交郵件的下一個躍點。Exchange 2010伺服器會用來通知他們陰影備援支援 XSHADOW 動詞。如果 SMTP 伺服器未支援陰影備援， Exchange 2010使用延遲認可為基礎建立備援複製郵件的接收連接器上設定的時間間隔。

陰影備援 Microsoft Exchange Server 2013至主要改進是傳輸伺服器現在建立它收到它認可成功接收傳送伺服器的訊息之前的任何郵件的重複複本。傳送伺服器支援 」 或 「 缺少的陰影備援支援不重要。這有助於確保Exchange 2013傳輸管線中的所有郵件時傳送過程中會都進行變得多餘。如果Exchange 2013判定原始郵件已遺失傳送過程中，已重新傳遞郵件的重複複本。

**目錄**

陰影備援元件

陰影備援需求

預設會啟用陰影備援

如何建立陰影郵件

SMTP 逾時

陰影郵件維護的方式

處理中斷後的郵件

## 陰影備援元件

下表說明陰影備援的元件。整個主題中所使用這些術語。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>專門用語</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>傳輸伺服器</p></td>
<td><p>Exchange server 訊息佇列及負責路由傳送郵件。在Exchange 2013、 傳輸伺服器會是信箱伺服器 （信箱伺服器上的傳輸服務）。</p></td>
</tr>
<tr class="even">
<td><p>傳輸資料庫</p></td>
<td><p>郵件佇列資料庫Exchange 2013 transport server 上。陰影佇列和安全網也會儲存在傳輸資料庫中。</p></td>
</tr>
<tr class="odd">
<td><p>傳輸高可用性界限</p></td>
<td><p>資料庫可用性群組 (DAG) 中 DAG 環境或非 DAG 環境中的 Active Directory 站台。郵件傳輸伺服器中的傳輸高可用性界限上時，Exchange 會嘗試維持 2 之備援副本的界限內傳輸伺服器上的郵件。當一則訊息離開傳輸高可用性界限時，Exchange 會停止維護備援副本的郵件。</p></td>
</tr>
<tr class="even">
<td><p>主要的郵件</p></td>
<td><p>送出到傳輸管線傳遞的郵件。</p></td>
</tr>
<tr class="odd">
<td><p>陰影郵件</p></td>
<td><p>訊息，直到它會保留在陰影伺服器的備援複本確認主要郵件已成功處理主要伺服器。</p></td>
</tr>
<tr class="even">
<td><p>主要伺服器</p></td>
<td><p>目前正在處理的主要的郵件傳輸伺服器。</p></td>
</tr>
<tr class="odd">
<td><p>陰影伺服器</p></td>
<td><p>傳輸伺服器扮演陰影郵件的主要伺服器。傳輸伺服器可能是一些郵件的主要伺服器和其他郵件的陰影伺服器同時。</p></td>
</tr>
<tr class="even">
<td><p>陰影佇列</p></td>
<td><p>傳遞佇列陰影伺服器儲存陰影郵件的位置。郵件有多個收件者、 主要訊息的每個下一個躍點需要個別的陰影佇列。</p></td>
</tr>
<tr class="odd">
<td><p>捨棄狀態</p></td>
<td><p>傳輸伺服器會維護表示主要郵件的陰影郵件的資訊都已成功處理。</p></td>
</tr>
<tr class="even">
<td><p>捨棄通知</p></td>
<td><p>回應陰影伺服器會接收來自指出陰影郵件已準備好要捨棄主要伺服器。</p></td>
</tr>
<tr class="odd">
<td><p>安全網</p></td>
<td><p>Exchange 2013改善的版本傳輸暫放。郵件已成功處理或傳遞至信箱收件者的信箱伺服器上的傳輸服務已移至安全網。如需詳細資訊，請參閱<a href="safety-net-exchange-2013-help.md">安全網</a>。</p></td>
</tr>
<tr class="even">
<td><p>陰影備援管理員</p></td>
<td><p>管理陰影備援的傳輸元件。</p></td>
</tr>
<tr class="odd">
<td><p>活動訊號</p></td>
<td><p>允許主要伺服器和確認彼此的可用性的陰影伺服器程序。</p></td>
</tr>
</tbody>
</table>


回到頁首

## 陰影備援需求

雖然可能看起來顯而易見，陰影備援需要多個Exchange 2013信箱伺服器。Mailbox server 可以是獨立伺服器或信箱伺服器和用戶端存取伺服器安裝在同一部電腦上。

  - 如果信箱伺服器不是 DAG 成員、 其他信箱伺服器必須是本機 Active Directory 站台。

  - 如果信箱伺服器的 DAG 成員、 其他信箱伺服器必須屬於相同 DAG。其他信箱伺服器屬於 DAG 可以在本機 Active Directory 站台或遠端 Active Directory 網站中。如果 DAG 跨越多個 Active Directory 站台，陰影備援偏好在站台恢復能力遠端 Active Directory 站台建立郵件的重複複本。

這些是其中陰影備援無法保護郵件傳輸的情況：

  - 在單一的 Exchange server 環境中。

  - 在 \[佈建 Dag。

  - 同時伺服器失敗期間的兩個或多個傳輸參與之郵件的陰影備援。

回到頁首

## 預設會啟用陰影備援

根據預設，使用*ShadowRedundancyEnabled*參數**Set-TransportConfig**指令程式上所有信箱伺服器上的傳輸服務中，啟用全域陰影備援。根據預設，如果在信箱伺服器上的傳輸服務無法建立郵件的重複複本郵件未遭拒。不過，您可以設定Exchange 2013如果郵件的重複複本不使用*RejectMessageOnShadowFailure*參數**Set-TransportConfig**指令程式上建立拒絕郵件。郵件被拒絕有暫時性的失敗，但傳送伺服器可以重新傳輸訊息。SMTP 回應碼是`451 4.4.0 Message failed to be made redundant.`應設定Exchange 2013以拒絕無法進行備援只有在您的組織有多個Exchange 2013信箱伺服器可用時的郵件。

下表說明啟用陰影備援的參數。

### 參數可讓陰影備援

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>參數</th>
<th>預設值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ShadowRedundancyEnabled</em> 位於 <strong>Set-TransportConfig</strong></p></td>
<td><p><code>$true</code></p></td>
<td><ul>
<li><p><code>$true</code> 於組織中的所有傳輸伺服器上啟動陰影備援。</p></li>
<li><p><code>$false</code> 於組織中的所有傳輸伺服器上停動陰影備援。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>在<strong>Set-TransportConfig</strong><em>RejectMessageOnShadowFailure</em></p></td>
<td><p><code>$false</code></p></td>
<td><ul>
<li><p><code>$false</code>  無法建立郵件陰影複製，主要的郵件仍會接受組織中傳輸伺服器。這些郵件不備援保存時傳送過程中。</p></li>
<li><p><code>$true</code>  無訊息會接受或認可由組織中任何傳輸伺服器之前已成功建立郵件陰影複製。如果無法建立郵件陰影複製，主要郵件遭拒暫時性錯誤。在組織中的所有郵件備援會都保存時傳送過程中。</p>
<p>您應將此值設<code>$true</code> ，只有當您有多個Exchange 2013 Mailbox server 中建立郵件陰影複製的所在的 DAG 或 Active Directory 網站中。</p></li>
</ul>
<p>此參數只會有意義的<code>$true</code><em>ShadowRedundancyEnabled</em>時。</p></td>
</tr>
</tbody>
</table>


回到頁首

## 如何建立陰影郵件

陰影備援的主要目標是郵件的可以隨時兩份傳輸高可用性界限內傳輸訊息時。何處及何時建立郵件的重複複本取決於訊息是來自以及將要郵件。有三個主要的決定因素：

  - 傳輸高可用性界限之外從接收的郵件。

  - 傳輸高可用性界限之外傳送的郵件。

  - 從 \[從信箱伺服器傳輸高可用性界限內的信箱傳輸提交服務接收的郵件。

*傳輸高可用性界限*可以是下列其中一項：

  - 針對信箱伺服器的 DAG 成員的 DAG。這包括跨越多個 Active Directory 站台的 DAG。

  - 不屬於 DAG 的信箱伺服器的 Active Directory 網站。

陰影備援永遠不會追蹤陰影郵件通過傳輸高可用性邊界。當郵件置於傳輸高可用性界限時，陰影備援開始或重新啟動。這可減少陰影郵件維護流量，可防止發生通過傳輸高可用性邊界陰影郵件 resubmissions。Exchange 2010Hub Transport server 是特殊案例，與本主題稍後的討論。

## 傳輸高可用性界限之外從接收的郵件

時Exchange 2013 Mailbox server 上的傳輸服務會接收來自郵件傳輸高可用性界限之外，信箱伺服器不是由傳送伺服器並有關支援 」 或 「 缺少的陰影備援的支援。只要啟用陰影備援，接收郵件的信箱伺服器複製變得多餘的郵件傳輸高可用性界限內的另一個信箱伺服器上之前認可回至傳送伺服器之郵件的回條。以下是程序的運作方式的範例：

![建立陰影訊息](images/Dd351027.a97d383b-6ae4-458d-af3a-1ac0a41cd52b(EXCHG.150).gif "建立陰影訊息")

1.  SMTP 伺服器會傳輸訊息給信箱伺服器上的傳輸服務。信箱伺服器的主要伺服器，而且郵件是主要的訊息。

2.  原始的 SMTP 工作階段與 SMTP 伺服器仍在作用中時，主要的伺服器上的傳輸服務中建立郵件的重複複本組織之不同信箱伺服器上的傳輸服務會以開啟新的且同時 SMTP 工作階段。
    
      - 如果主要伺服器的 DAG 成員，主要伺服器連接至相同 DAG 中不同的信箱伺服器。如果 DAG 跨越多個 Active Directory 站台，在不同的 Active Directory 站台的信箱伺服器被慣用預設。此設定是由*ShadowMessagePreference*參數控制**Set-TransportService**指令程式上。預設值是`PreferRemote`，但是您可以將其變更為`RemoteOnly`或`LocalOnly`。
    
      - 如果主要伺服器無法 DAG 成員，主要伺服器連接至不同的信箱伺服器在相同的 Active Directory 網站中，無論*ShadowMessagePreference*參數的值。

3.  主要伺服器傳輸至其他 Mailbox server 上的傳輸服務的郵件複本及其他信箱伺服器上的傳輸服務認可已成功建立郵件的副本。郵件的副本陰影郵件，並保留其信箱伺服器是主要伺服器的陰影伺服器。郵件存在於陰影伺服器上的陰影佇列中。

4.  主要伺服器從陰影伺服器收到認可之後，主要伺服器認可為原始的 SMTP 伺服器之主要郵件索取回條原始的 SMTP 工作階段，並關閉 SMTP 工作階段。

## 傳輸高可用性界限之外傳送的郵件

當Exchange 2013傳輸伺服器來傳送訊息傳輸高可用性圖形界限之外，另一邊上的 SMTP 伺服器認可成功接收郵件時，傳輸伺服器會將郵件移至 Safety Net。從 Safety Net 的郵件沒有重新送出主要郵件已成功傳輸通過傳輸高可用性邊界之後會發生。如需 Safety Net 的詳細資訊，請參閱[安全網](safety-net-exchange-2013-help.md)。

## 傳輸高可用性界限內傳送的郵件

郵件路由最佳化Exchange 2013中使 DAG 或 Active Directory 站台中的最終目的地時，不通常需要該 DAG 或 Active Directory 站台中的 Mailbox server 上的傳輸服務之間的多個躍點。保留郵件的最終目的地 DAG 或 Active Directory 站台中的信箱伺服器上的傳輸服務會接受郵件，一旦郵件的下一個躍點通常是本身的最終目的地。陰影備援的即時訊息的兩個複本傳送過程中的目標是要在一個陰影複製郵件的任何地方存 DAG 或 Active Directory 站台內時執行。通常只有容錯移轉案例 DAG 中需要**Redirect-Message**指令程式清空信箱伺服器上作用中的佇列會需要在相同的傳輸高可用性界限內的多個躍點。

## 陰影備援能力與 Exchange 2010 集線傳輸伺服器中的相同的 Active Directory 站台

當Exchange 2010集線傳輸伺服器會傳輸訊息給Exchange 2013信箱中的伺服器相同的 Active Directory 站台時、 Exchange 2010集線傳輸伺服器會通告的陰影備援使用 XSHADOW 命令支援但信箱伺服器不會通知支援陰影備援。這可防止Exchange 2010 Hub Transport server Exchange 2013 Mailbox server 上建立郵件陰影複製。

當Exchange 2013 Mailbox server 上的傳輸服務會傳輸訊息給Exchange 2010相同的 Active Directory 站台中的 Hub Transport 時、 Exchange 2013 Mailbox server 遮蔽Exchange 2010集線傳輸伺服器的郵件。Exchange 2013 Mailbox server 接收從Exchange 2010集線傳輸伺服器已成功接收郵件的認可後， Exchange 2013 Mailbox server 將安全網移成功處理的郵件。不過，安全網中儲存由Exchange 2013信箱已成功處理的郵件永遠不會提交至Exchange 2010 Hub Transport server。

回到頁首

## SMTP 逾時

建立郵件的重複複本嘗試、 期間之間傳送的 SMTP 伺服器和主要伺服器或 SMTP 工作階段的主要伺服器與陰影伺服器之間的 SMTP 連線可能逾時。接收連接器及傳送的連接器兩者都有時資料實際正在傳送連接器上的*ConnectionInactivityTimeOut*參數。接收連接器也有絕對*ConnectionTimeOut*參數。

如果 SMTP 工作階段逾時前的郵件陰影複製的任何已成功建立，認可其結果是由*RejectMessageOnShadowFailure*參數控制**Set-TransportConfig**指令程式上。根據預設，此參數的值會是`$false`，這表示主要訊息接受而建立的陰影複製。如果此參數的值是`$true`主要郵件遭拒與暫時性錯誤`451 4.4.0`。

如果已成功建立郵件陰影複製，但之間傳送的 SMTP 伺服器和主要伺服器的 SMTP 工作階段逾時，主要伺服器接受與處理的主要的郵件。傳送郵件的 SMTP 伺服器會重新未認可的訊息傳遞，但重複訊息偵測會防止 Exchange 信箱使用者就看不到重複的郵件。時傳送的 SMTP 伺服器重新提交郵件，主要伺服器將會建立其他的陰影複製的郵件。所傳送的 SMTP 伺服器建立期間訊息 resubmissions 陰影郵件之間沒有任何關係。

下表說明參數控制陰影郵件的建立

### 陰影郵件建立參數

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>來源</th>
<th>預設值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>在<strong>Set-TransportConfig</strong><em>ShadowMessagePreferenceSetting</em></p></td>
<td><p><code>PreferRemote</code></p></td>
<td><ul>
<li><p><code>PreferRemote</code>  嘗試在不同的 Active Directory 站台信箱伺服器上建立郵件的陰影複製。如果作業失敗，請嘗試在本機 Active Directory 站台的伺服器上建立郵件的陰影複製。</p></li>
<li><p><code>LocalOnly</code>  只應在本機 Active Directory 站台傳輸伺服器上所做之郵件的陰影複製。</p></li>
<li><p><code>RemoteOnly</code>︰ 應該只在不同的 Active Directory 站台傳輸伺服器上所進行之郵件的陰影複製。</p></li>
</ul>
<p>此參數只會有意義的嘗試建立郵件的陰影複製的主要伺服器時的跨越多個 Active Directory 站台的 DAG 成員的信箱伺服器。</p></td>
</tr>
<tr class="even">
<td><p>在<strong>Set-TransportConfig</strong><em>MaxRetriesForRemoteSiteShadow</em></p></td>
<td><p>4</p></td>
<td><p>信箱伺服器時的跨越多個 Active Directory 站台的 DAG 成員會使用此參數。</p>
<ul>
<li><p>如果<em>ShadowMessagePreferenceSetting</em>設為<code>PreferRemote</code>，先 Mailbox server 嘗試建立郵件陰影複製到<em>MaxRetriesForRemoteSiteShadow</em>所指定的次數遠端 Active directory 站台中的另一個信箱伺服器上。如果這個失敗，信箱伺服器會嘗試在本機 Active Directory 網站最多個<em>MaxRetriesForLocalSiteShadow</em>所指定的次數的不同信箱伺服器上建立郵件陰影複製。</p></li>
<li><p>如果<em>ShadowMessagePreferenceSetting</em>設為<code>RemoteOnly</code>，Mailbox server 只會嘗試在最多個<em>MaxRetriesForRemoteSiteShadow</em>所指定的次數遠端 Active Directory 站台信箱伺服器上建立郵件陰影複製。</p></li>
<li><p>該</p></li>
</ul>
<p>當無法成功建立郵件陰影複製 ︰</p>
<ul>
<li><p>如果<code>$true</code><em>RejectMessageOnShadowFailure</em> ，主要郵件遭拒暫時性錯誤。</p></li>
<li><p>如果<code>$false</code><em>RejectMessageOnShadowFailure</em> ，主要的郵件仍、 接受但不備援保存。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>在<strong>Set-TransportConfig</strong><em>MaxRetriesForLocalSiteShadow</em></p></td>
<td><p>2</p></td>
<td><p>在下列情況下使用此參數：</p>
<ul>
<li><p>如果信箱伺服器的跨越多個 Active Directory 站台的 DAG 成員。</p>
<ol>
<li><p>如果<em>ShadowMessagePreferenceSetting</em>設為<code>PreferRemote</code>，先 Mailbox server 嘗試建立郵件陰影複製到<em>MaxRetriesForRemoteSiteShadow</em>所指定的次數遠端 Active directory 站台中的另一個信箱伺服器上。如果這個失敗，信箱伺服器會嘗試在本機 Active Directory 網站最多個<em>MaxRetriesForLocalSiteShadow</em>所指定的次數的不同信箱伺服器上建立郵件陰影複製。</p></li>
<li><p>如果<em>ShadowMessagePreferenceSetting</em>設為<code>LocalOnly</code>，Mailbox server 只會嘗試在本機 Active Directory 網站最多個<em>MaxRetriesForLocalSiteShadow</em>所指定的次數的不同信箱伺服器上建立郵件陰影複製。</p></li>
</ol></li>
<li><p>如果信箱伺服器不是 DAG 成員或 Mailbox server 會是一個 Active Directory 站台的 DAG 成員，Mailbox server 只會嘗試在本機 Active Directory 網站最多個<em>MaxRetriesForLocalSiteShadow</em>所指定的次數的不同信箱伺服器上建立郵件陰影複製。</p></li>
</ul>
<p>當無法成功建立郵件陰影複製 ︰</p>
<ul>
<li><p>如果<code>$true</code><em>RejectMessageOnShadowFailure</em> ，主要郵件遭拒暫時性錯誤。</p></li>
<li><p>如果<code>$false</code><em>RejectMessageOnShadowFailure</em> ，主要的郵件仍、 接受但不備援保存。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>在<strong>Set-ReceiveConnector</strong><em>ConnectionInactivityTimeout</em></p></td>
<td><p>在郵件伺服器上傳輸服務的 5 分鐘</p>
<p>在用戶端存取伺服器上前端傳輸服務的 5 分鐘。</p>
<p>邊際傳輸伺服器上的 1 分鐘。</p></td>
<td><p>此參數會指定之前關閉連線的來源郵件伺服器與開啟的 SMTP 連線可以維持閒置的時間上限。此參數的值必須小於<em>ConnectionTimeout</em>參數所指定的值。</p></td>
</tr>
<tr class="odd">
<td><p>在<strong>Set-ReceiveConnector</strong><em>ConnectionTimeout</em></p></td>
<td><p>在郵件伺服器上傳輸服務的 10 分鐘</p>
<p>在用戶端存取伺服器上前端傳輸服務的 10 分鐘。</p>
<p>邊際傳輸伺服器上的 5 分鐘。</p></td>
<td><p>此參數會指定 SMTP 連線與訊息伺服器來源可以保持開啟，即使來源郵件伺服器傳輸資料的最長時間。此參數的值必須大於<em>ConnectionInactivityTimeout</em>參數所指定的值。</p></td>
</tr>
<tr class="even">
<td><p>在<strong>Set-SendConnector</strong><em>ConnectionInactivityTimeOut</em></p></td>
<td><p>10 分鐘</p></td>
<td><p>此參數指定在關閉連線之前，與目的郵件伺服器的開啟 SMTP 連線可以持續閒置的時間上限。</p></td>
</tr>
</tbody>
</table>


回到頁首

## 陰影郵件維護的方式

陰影郵件已成功建立之後，只有剛開始陰影備援的工作。主要伺服器及陰影伺服器必須保持幫彼此追蹤郵件的進度。

如果主要伺服器已成功傳輸至下一個躍點郵件下一個躍點認可收到郵件，主要伺服器更新*捨棄狀態*的郵件為完整的傳遞。捨棄狀態基本上是清單的包含中的各個受監控的郵件訊息。已成功傳遞的郵件不需要在陰影佇列，因此一旦陰影伺服器知道主要伺服器已成功傳輸至下一個躍點郵件保留、 陰影伺服器會將陰影郵件陰影佇列從移到 Safety Net。

陰影伺服器來查詢的主要伺服器判斷其陰影佇列中的陰影郵件的捨棄狀態。如果陰影伺服器開啟的 SMTP 工作階段的主要伺服器因任何原因包括的其他不相關的郵件傳輸的陰影伺服器發出**XQDISCARD**決定主要郵件的捨棄狀態。如果陰影伺服器尚未開啟預先設定的時間間隔之後的 SMTP 工作階段的主要伺服器，陰影伺服器將會開啟主要伺服器的 SMTP 工作階段並發出**XQDISCARD**命令。由**Set-TransportConfig**指令程式上的*ShadowHeartbeatFrequentcy*參數控制的時間間隔。預設值為 2 分鐘。陰影之後伺服器的主要伺服器，以開啟的 SMTP 工作階段的主要伺服器會回應*捨棄通知*套用至查詢的陰影伺服器的郵件。在Exchange 2013、 捨棄通知會儲存在記憶體中找不到磁碟。因此，如果重新啟動 Microsoft Exchange Transport 服務，會保存捨棄通知。服務開始之後，主要伺服器仍然知道關於成功處理之後，郵件及該資訊會陰影伺服器可用。

陰影伺服器和主要伺服器之間的 SMTP 通訊會做為*活動訊號*，以決定伺服器的可用性。如果陰影伺服器無法開啟主要伺服器使用的 SMTP 工作階段後預先設定的時間間隔\] 中，或者如果主要伺服器的傳輸資料庫具有不同的資料庫識別碼，陰影伺服器會升階本身做為主要伺服器，並且升階作為主要郵件的陰影郵件並傳輸郵件給下一個躍點。由**Set-TransportConfig**指令程式上的*ShadowResubmitTimeSpan*參數控制的時間間隔。預設值為 3 小時。

*陰影備援管理員*是負責管理陰影備援Exchange 2013傳輸伺服器的核心元件。陰影備援管理員負責維護伺服器目前正在處理的所有主要郵件的下列資訊：

  - 陰影伺服器正在處理每個主要訊息。

  - 捨棄傳送給陰影伺服器狀態。

陰影備援管理員負責陰影伺服器有其陰影佇列中的所有陰影郵件的下列項目：

  - 維護每個陰影郵件的主要伺服器的清單。

  - 比較原始資料庫識別碼及儲存郵件的主要複本的佇列資料庫目前的資料庫識別碼。

  - 檢查陰影訊息進入佇列的每個主要伺服器的可用性。

  - 處理捨棄從主要伺服器的通知。

  - 完成所有陰影佇列中移除陰影郵件預期送達 \[放棄通知。

  - 決定陰影伺服器應該發生變成主要伺服器的陰影郵件的擁有權。

  - 追蹤郵件 bifurcations 和其他的側邊效果訊息像是傳遞狀態通知 (Dsn) 及日誌報告確認郵件的重複複本未發行之前完全處理郵件的所有分支。

下表說明控制陰影郵件維護方式的參數。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>參數</th>
<th>預設值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>在<strong>Set-TransportConfig</strong><em>ShadowHeartbeatFrequency</em></p></td>
<td><p>2 分鐘</p></td>
<td><p>陰影伺服器在開啟要檢查郵件的捨棄狀態的主要伺服器的 SMTP 連線的時間長度上限。</p></td>
</tr>
<tr class="even">
<td><p>在<strong>Set-TransportConfig</strong><em>ShadowResubmitTimeSpan</em></p></td>
<td><p>3 小時</p></td>
<td><p>時間伺服器在決定主要伺服器失敗和假設陰影郵件的主要伺服器無法連線的陰影佇列的擁有權。</p></td>
</tr>
<tr class="odd">
<td><p>在<strong>Set-TransportConfig</strong><em>ShadowMessageAutoDiscardInterval</em></p></td>
<td><p>2 天</p></td>
<td><p>Long 伺服器會保留在已成功傳遞郵件的捨棄事件的方式。主要伺服器佇列捨棄事件直到圖形的陰影伺服器。不過，如果陰影伺服器不會查詢這個參數中指定的期間主要伺服器的主要伺服器會刪除已排入佇列的捨棄事件。</p></td>
</tr>
<tr class="even">
<td><p><em>SafetyNetHoldTime</em> 位於 <strong>Set-TransportConfig</strong></p></td>
<td><p>2 天</p></td>
<td><p>成功處理的郵件的保留期限安全網中。未認可的陰影郵件最後期限從 Safety Net <em>SafetyNetHoldTime</em>和<em>MessageExpirationTimeout</em><strong>Set-TransportService</strong>上的總和。</p></td>
</tr>
<tr class="odd">
<td><p><em>MessageExpirationTimeout</em> 位於 <strong>Set-TransportService</strong></p></td>
<td><p>2 天</p></td>
<td><p>訊息在過期前可停留於佇列中停留多長時間。</p></td>
</tr>
</tbody>
</table>


回到頁首

## 處理中斷後的郵件

陰影備援最小化由於伺服器中斷郵件遺失。傳輸伺服器回到線上時之後中斷，有兩種情況：

  - **伺服器上線回以新的傳輸資料庫**  在此案例中，傳輸資料庫是因為資料損毀或硬體故障無法復原。在此例中的傳輸伺服器會有新的資料庫識別碼，因為它會辨識作為新路由由組織中其他 transport server。這也適用於其中無法復原伺服器，與新的伺服器已佈建取代為 「 brad。

  - **伺服器上線回具有相同的傳輸資料庫**  在此案例中，特定傳輸伺服器沒有失敗，但已離線陰影伺服器假設郵件的擁有權並重新提交他們的時間足以。例如，網路卡失敗或長的維護伺服器上將會導致此案例。

下表摘要說明陰影備援對於的應變方式這兩種案例。為避免混淆，假設有中斷的伺服器名為 Mailbox01。

### 處理的復原案例中的郵件

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>復原的案例</th>
<th>採取的動作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mailbox01 回上線以新資料庫。</p></td>
<td><p>Mailbox01 變成無法使用時有的陰影訊息排入佇列的 Mailbox01 每一部伺服器會假設這些訊息的擁有權並重新提交它們。然後取得傳送訊息給他們的目的地。</p>
<p>郵件的最大延遲時間都是<strong>Set-TransportConfig</strong>指令程式上<em>ShadowHeartbeatFrequency</em>參數的值。預設值為 2 分鐘。</p></td>
</tr>
<tr class="even">
<td><p>Mailbox01 回上線具有相同的資料庫。</p></td>
<td><p>Mailbox01 回上線之後，它會傳遞郵件已經傳遞所保留的郵件的陰影複製為 Mailbox01 之伺服器及其佇列中。這會導致重複的這些訊息的傳遞。Exchange 信箱使用者將不會看到因為重複訊息偵測重複的郵件。不過，在非 Exchange 傳訊系統上的收件者可能會收到郵件的重複複本。</p>
<p>郵件的最大延遲時間都是<strong>Set-TransportConfig</strong>指令程式上<em>ShadowResubmitTimeSpan</em>參數的值。預設值為 3 小時。</p></td>
</tr>
</tbody>
</table>


回到頁首

