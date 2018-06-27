---
title: '使用 Telnet 測試 SMTP 通訊: Exchange 2013 Help'
TOCTitle: 使用 Telnet 測試 SMTP 通訊
ms:assetid: 8a5f6715-baa4-48dd-8600-02c6b3d1aa9d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb123686(v=EXCHG.150)
ms:contentKeyID: 52062561
ms.date: 01/12/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 使用 Telnet 測試 SMTP 通訊

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

本主題說明如何使用 Telnet 來測試郵件伺服器之間的簡易郵件傳送通訊協定 (SMTP) 通訊。SMTP 預設會接聽通訊埠 25。如果您在通訊埠 25 上使用 Telnet，則可輸入用來連接 SMTP 伺服器的 SMTP 命令，並將您的 Telnet 工作階段當成 SMTP 郵件伺服器一樣來傳送郵件。您可以查看連線以及郵件提交程序中每個步驟的成敗。

在以下案例中，您可能想要使用 Telnet 來測試與 Microsoft Exchange 組織中現有傳輸伺服器間的 SMTP 通訊：

  - 從位於周邊網路外的主機連接至組織面向網際網路的 Exchange 伺服器，並傳送測試郵件。

  - 從組織面向網際網路的 Exchange 伺服器連接至遠端郵件伺服器，並傳送測試郵件。

本主題中的程序說明如何使用 Microsoft Windows 隨附的 Telnet 用戶端元件。協力廠商 Telnet 用戶端可能需要與 Windows Telnet 元件不同的語法。

## 開始之前有哪些須知？

  - 預估完成時間：30 分鐘

  - Exchange 權限無法套用於此主題的程序。在 Exchange 伺服器或用戶端電腦的作業系統中執行這些。

  - 本主題中的程序最適合用來連接允許匿名連線之面向網際網路的伺服器。內部 Exchange 伺服器之間的郵件傳輸會進行加密與驗證。。若要使用 Telnet 連接至 Mailbox Server 上的 Hub Transport 服務，您必須建立已設定為允許匿名存取或基本驗證的接收連接器來接收郵件。如果連接器允許基本驗證，則必須要有一個公用程式將使用者名稱及密碼的文字字串轉換成 Base64 格式。由於使用基本驗證時，使用者名稱和密碼很容易辨別，所以建議不要使用沒有加密機制的基本驗證。

  - 如果您連線至遠端郵件伺服器，請考慮在您面向網際網路的 Exchange 伺服器上執行本主題中的程序。這有助於避免遠端郵件伺服器拒絕測試郵件，而遠端郵件伺服器已設定要驗證來源 IP 位址、對應的網域名稱系統 (DNS) 網域名稱，以及嘗試傳送郵件至伺服器之任何網際網路主機的反向查閱 IP 位址。

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


## 該怎麼做？

## 步驟 1：在 Windows 中安裝 Telnet 用戶端

根據預設，Telnet 用戶端並未安裝在大多數用戶端或伺服器版的 Microsoft Windows 作業系統中。若要進行安裝，請參閱[安裝 Telnet 用戶端](https://go.microsoft.com/fwlink/p/?linkid=179054)。

## 步驟 2：使用 Nslookup 在遠端 SMTP 伺服器的 MX 記錄中尋找 FQDN 或 IP 位址

若要在通訊埠 25 上使用 Telnet 連接目的 SMTP 伺服器，您必須使用 SMTP 伺服器的網域全名 (FQDN) 或 IP 位址。如果 FQDN 或 IP 位址未知，尋找此資訊的最簡單方法，就是使用 Nslookup 命令列工具尋找目的網域的 MX 記錄。

1.  在命令提示字元中，輸入 **nslookup**，然後按 ENTER 鍵。此命令會開啟 Nslookup 工作階段。

2.  輸入 **set type=mx**，然後按 ENTER 鍵。

3.  輸入 **set timeout=20**，然後按 ENTER 鍵。Windows DNS 伺服器預設有 15 秒的遞迴 DNS 查詢逾時限制。

4.  輸入要尋找其 MX 記錄的網域名稱。例如，若要尋找 fabrikam.com 網域的 MX 記錄，請輸入 **fabrikam.com.**，然後按 ENTER 鍵。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>尾端的句點 ( <strong>.</strong> ) 表示是 FQDN。使用尾端的句點可防止不小心在網域名稱後面加上任何為網路設定的預設 DNS 字尾。</td>
    </tr>
    </tbody>
    </table>
    
    該命令的輸出如下：
    
        fabrikam.com mx preference=10, mail exchanger = mail1.fabrikam.com
        fabrikam.com mx preference=20, mail exchanger = mail2.fabrikam.com
        mail1.fabrikam.com internet address = 192.168.1.10
        mail2 fabrikam.com internet address = 192.168.1.20
    
    您可以使用與 MX 記錄關聯的任何主機名稱或 IP 位址作為目的 SMTP 伺服器。SMTP 伺服器的喜好設定值愈低表示優先順序愈高。您可以使用多筆 MX 記錄及不同的喜好設定值，以供進行負載平衡及容錯。

5.  準備結束 Nslookup 工作階段時，請輸入 **exit**，然後按 ENTER 鍵。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在組織內部網路上設定的防火牆或網際網路 Proxy 限制，可能會阻擋您使用 Nslookup 工具查詢網際網路上的公用 DNS 伺服器。</td>
</tr>
</tbody>
</table>


## 步驟 3：在通訊埠 25 上使用 Telnet 測試 SMTP 通訊

此範例中使用的值如下：

  - **目的 SMTP 伺服器**   mail1.fabrikam.com

  - **來源網域**   contoso.com

  - **寄件者的電子郵件地址**   chris@contoso.com

  - **收件者的電子郵件地址**   kate@fabrikam.com

  - **郵件主旨**   Contoso 的測試郵件

  - **郵件內文**   這是一封測試郵件

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
<li><p>Telnet 用戶端中的命令不區分大小寫。SMTP 命令動詞會大寫，以方便識別。</p></li>
<li><p>在 Telnet 工作階段中，連接至目的 SMTP 伺服器之後，不能使用退格鍵。如果您在輸入 SMTP 命令時打錯字，則必須按 ENTER，然後重新輸入命令。無法辨識的 SMTP 命令或語法錯誤會產生錯誤訊息，如下所示：</p>
<pre><code>500 5.3.3 Unrecognized command</code></pre></li>
</ul></td>
</tr>
</tbody>
</table>


1.  在命令提示字元中，輸入 **telnet**，然後按 ENTER 鍵。此命令會開啟 Telnet 工作階段。

2.  輸入 **set localecho**，然後按 ENTER 鍵。此選用命令可讓您在輸入字元的同時檢視這些字元。有些 SMTP 伺服器可能會需要此設定。

3.  輸入 **set logfile***\<filename\>*。此選用命令會將 Telnet 工作階段記錄在指定的記錄檔。如果您只有指定檔名，則記錄檔位置為目前的工作目錄。如果您指定路徑及檔名，則該路徑必須在電腦本機上。指定的路徑和檔名都必須以 Microsoft DOS 8.3 格式輸入。必須指定已存在的路徑。如果指定的記錄檔不存在，則系統會為您建立該記錄檔。

4.  輸入 **open mail1.fabrikam.com 25**，然後按 ENTER 鍵。

5.  輸入 **EHLO contoso.com**，然後按 ENTER 鍵。

6.  輸入 **MAIL FROM:chris@contoso.com**，然後按 ENTER 鍵。

7.  輸入 **RCPT TO:kate@fabrikam.com NOTIFY=success,failure**，然後按 ENTER 鍵。選用的 NOTIFY 命令可定義目的 SMTP 伺服器必須提供給寄件者的特定傳遞狀態通知 (DSN) 郵件。DSN 郵件是在 RFC 1891 中定義。在此情況下，您是在要求對方傳回 DSN 郵件表明郵件傳遞成功或失敗。

8.  輸入 **DATA**，然後按 ENTER 鍵。您會收到如下回應：
    
        354 Start mail input; end with <CLRF>.<CLRF>

9.  輸入**主旨：Contoso 的測試郵件**，然後按 ENTER 鍵。

10. 按 ENTER。RFC 2822 規定 `Subject:` 標頭欄位與郵件內文之間必須留一行空白。

11. 輸入**這是測試郵件**，然後按 ENTER。

12. 按 ENTER，輸入一個句點 ( **.** )，然後按 ENTER 鍵。您會收到如下回應：
    
        250 2.6.0 <GUID> Queued mail for delivery

13. 若要中斷與目的 SMTP 伺服器的連線，請輸入 **QUIT**，然後按 ENTER 鍵。您會收到如下回應：
    
        221 2.0.0 Service closing transmission channel

14. 若要關閉 Telnet 工作階段，請輸入 **quit**，然後按 ENTER 鍵。

## 步驟 4：評估 Telnet 工作階段的結果

本節提供以下命令可能得到的回應資訊，這些命令是先前範例中使用的命令：

  - 開啟 mail1.fabrikam.com 25

  - EHLO contoso.com

  - MAIL FROM:chris@contoso.com

  - RCPT TO:kate@fabrikam.com NOTIFY=success,failure
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>RFC 2821 中定義的 3 位數 SMTP 回應碼適用於所有的 SMTP 郵件伺服器。但在某些 SMTP 郵件伺服器中，文字說明部分會稍微不同。</td>
    </tr>
    </tbody>
    </table>


## 開啟 mail1.fabrikam.com 25

**成功回應**   `220 mail1.fabrikam.com Microsoft ESMTP MAIL Service ready at <day-date-time>`

**失敗回應**   `Connecting to mail1.fabrikam.com...Could not open connection to the host, on port 25: Connect failed`

**可能的失敗原因**

  - 目的 SMTP 服務無法使用。

  - 目的防火牆上有所限制。

  - 來源防火牆上有所限制。

  - 所指定之目的 SMTP 伺服器的 FQDN 或 IP 位址不正確。

  - 指定的通訊埠號碼不正確。

## EHLO contoso.com

**成功回應**   `250 mail1.fabrikam.com Hello [<sourceIPaddress>]`

**失敗回應**   `501 5.5.4 Invalid domain name`

**可能的失敗原因**   網域名稱中有無效字元。或者，目的 SMTP 伺服器上有連線限制。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>EHLO 是 RFC 2821 中定義的延伸簡易郵件傳送通訊協定 (ESMTP) 動詞。ESMTP 伺服器會在初始連線期間通告其功能。這些功能包括其可接受的最大郵件大小，以及所支援的驗證方法。HELO 是 RFC 821 中定義的舊 SMTP 動詞。大部分 SMTP 郵件伺服器都支援 ESMTP 及 EHLO。</td>
</tr>
</tbody>
</table>


## MAIL FROM:chris@contoso.com

**成功回應**   `250 2.1.0 Sender OK`

**失敗回應**   `550 5.1.7 Invalid address`

**可能的失敗原因**   寄件者電子郵件地址中有語法錯誤。

**失敗回應**   `530 5.7.1 Client was not authenticated`

**可能的失敗原因**   目的伺服器不接受匿名提交郵件。如果您嘗試使用 Telnet 直接將郵件提交至 Hub Transport server，就會收到此錯誤。

## RCPT TO:kate@fabrikam.com NOTIFY=success,failure

**成功回應**   `250 2.1.5 Recipient OK`

**失敗回應**   `550 5.1.1 User unknown`

**可能的失敗原因**   組織中沒有指定的收件者。

