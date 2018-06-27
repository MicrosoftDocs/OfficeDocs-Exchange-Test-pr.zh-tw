---
title: '設定通訊協定記錄: Exchange 2013 Help'
TOCTitle: 設定通訊協定記錄
ms:assetid: c81cac9c-b990-492a-b899-5be8d08a6068
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124531(v=EXCHG.150)
ms:contentKeyID: 50474174
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定通訊協定記錄

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2013-03-15_

通訊協定記錄會記錄郵件傳遞的過程中，傳送連接器和接收連接器之間所發生的 SMTP 交談。

## 開始之前有哪些須知？

  - 預估完成時間：15 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「傳輸服務」、「前端傳輸服務」、「信箱傳輸服務」、「接收連接器」和「傳送連接器」項目。

  - 您可以使用 Exchange 系統管理中心 (EAC) 來啟用或停用通訊協定記錄與 Client Access server 上 Front End Transport 服務中的接收連接器的傳送連接器和 Mailbox server 上的傳輸服務中的接收連接器。您也可以使用 EAC 來設定傳輸服務的通訊協定記錄檔路徑。所有其他通訊協定記錄選項，您需要使用命令介面。

  - 通訊協定記錄是啟用還是停用每個個別的連接器。在 Exchange 伺服器上的所有接收連接器都共用相同的通訊協定記錄檔和通訊協定記錄檔選項。這些通訊協定記錄檔設定是分開的傳送連接器通訊協定記錄檔和已在同一部伺服器的通訊協定記錄選項。

  - UNRESOLVED\_TOKENBLOCK\_VAL(ALERT\_Do 不執行此訂閱的 Edge server 上)

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


## 您要執行的工作

## 使用 EAC 來設定通訊協定記錄

若要使用 EAC 來啟用或停用信箱伺服器上傳輸服務中傳送連接器和接收連接器的通訊協定記錄，或是用戶端存取伺服器上前端傳輸服務中接收連接器的通訊協定記錄，請執行下列動作：

1.  在 EAC 中，瀏覽至 \[郵件流程\] \>\[傳送連接器\] 或 \[郵件流程\] \> \[接收連接器\]。

2.  選取要設定的連接器，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[一般\] 索引標籤中的 \[通訊協定記錄等級\] 區段中，選取下列其中一個選項：
    
      - **無**   停用連接器上的通訊協定記錄。
    
      - **詳細資訊**   會啟用連接器上的通訊協定記錄。
    
    完成後，按一下 **\[儲存\]**。

若要使用 EAC 來設定信箱伺服器上傳輸服務中傳送連接器和接收連接器的通訊協定記錄路徑，請執行下列動作：

1.  在 EAC 中，瀏覽至 \[伺服器\] \> \[伺服器\]。

2.  選取要配置的 Mailbox Server，然後按一下 \[確定\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在伺服器內容頁面上，按一下 \[傳輸記錄檔\]。

4.  在 \[通訊協定記錄\] 區段中，變更下列其中一個設定：
    
      - **傳送通訊協定記錄檔路徑**  您指定的值必須是本機 Exchange 伺服器上。如果資料夾不存在，它會建立您時按一下 \[**儲存檔案**。
    
      - **接收通訊協定記錄檔路徑**  您指定的值必須是本機 Exchange 伺服器上。如果資料夾不存在，它會建立您時按一下 \[**儲存檔案**。
    
    完成後，按一下 **\[儲存\]**。

## 如何才能了解這是否正常運作？

若要驗證是否已成功使用 EAC 來設定通訊協定記錄設定，請執行下列動作：

1.  瀏覽至您所指定的傳送連接器或接收連接器通訊協定記錄位置。

2.  如果您啟用通訊協定記錄，確認已建立的記錄檔。如果您停用通訊協定記錄，確認不再更新的最新的記錄檔。

## 使用命令介面來啟用或停用傳送連接器和接收連接器的通訊協定記錄

若要啟用或停用傳送連接器和接收連接器的通訊協定記錄，請執行下列命令：

    <Set-SendConnector |Set-ReceiveConnector> <ConnectorIdentity> -ProtocolLoggingLevel <Verbose | None>

此範例會啟用接收連接器 Connection from Contoso.com 的通訊協定記錄。

    Set-ReceiveConnector "Connection from Contoso.com" -ProtocolLoggingLevel Verbose

## 如何才能了解這是否正常運作？

若要驗證您是否成功啟用或停用通訊協定記錄，請執行下列動作：

1.  在命令介面中，執行下列命令：
    
        <Get-SendConnector |Get-ReceiveConnector> | Format-List Name,ProtocolLoggingLevel

2.  請確認顯示的值是您所設定的值。

## 使用命令介面來啟用或停用組織內部傳送連接器的通訊協定記錄

若要啟用或停用信箱伺服器上傳輸服務中以及用戶端存取伺服器上前端傳輸服務中，隱含與隱藏的組織內部傳送連接器的通訊協定記錄，請執行下列動作：

    <Set-TransportService | Set-FrontEndTransportService> -IntraOrgConnectorProtocolLoggingLevel <Verbose | None>

此範例會啟用信箱伺服器 Mailbox01 上傳輸服務中組織內部傳送連接器的通訊協定記錄。

    Set-TransportService Mailbox01 -IntraOrgConnectorProtocolLoggingLevel Verbose

## 如何才能了解這是否正常運作？

若要驗證您是否成功啟用或停用組織內部傳送連接器的通訊協定記錄，請執行下列動作：

1.  在命令介面中，執行下列命令：
    
        <Get-TransportService | Get-FrontEndTransportService> <ServerIdentity> | Format-List IntraOrgConnectorProtocolLoggingLevel

2.  請確認顯示的值是您所設定的值。

## 使用命令介面來啟用或停用信箱傳遞傳送連接器的通訊協定記錄

若要啟用或停用位於信箱伺服器上信箱傳輸服務中，隱含與隱藏的信箱傳遞傳送連接器的通訊協定記錄，請執行下列動作：

    Set-MailboxTransportService -MailboxDeliveryConnectorProtocolLoggingLevel <Verbose | None>

此範例會啟用信箱伺服器 Mailbox01 上信箱傳輸服務中信箱傳遞接收連接器的通訊協定記錄。

    Set-MailboxTransportService Mailbox01 -MailboxDeliveryConnectorProtocolLoggingLevel Verbose

## 如何才能了解這是否正常運作？

若要驗證您是否成功啟用或停用信箱傳遞連接器的通訊協定記錄，請執行下列動作：

1.  在命令介面中，執行下列命令：
    
        Get-MailboxTransportService <ServerIdentity> | Format-List MailboxDeliveryConnectorProtocolLoggingLevel

2.  請確認顯示的值是您所設定的值。

## 使用命令介面來設定通訊協定記錄設定

若要設定通訊協定記錄設定，請執行下列命令：

    <Set-TransportService | Set-MailboxTransportService | Set-FrontEndTransportService> <ServerIdentity> -ReceiveProtocolLogPath <LocalFilePath> -SendProtocolLogPath <LocalFilePath> -ReceiveProtocolLogMaxFileSize <Size> -SendProtocolLogMaxFileSize <Size> -ReceiveProtocolLogMaxDirectorySize <Size> -SendProtocolLogMaxDirectorySize <Size> -ReceiveProtocolLogMaxAge <dd.hh:mm:ss> -SendProtocolLogMaxAge <dd.hh:mm:ss>

此範例會設定信箱伺服器 Mailbox01 上傳輸服務中的下列通訊協定記錄設定：

  -  
    設定位置的所有接收連接器通訊協定記錄至 D:\\Hub 接收 SMTP 記錄檔和所有傳送連接器通訊協定記錄檔 D:\\Hub 傳送 SMTP 記錄檔。請注意是否資料夾不存在，它會為您建立。

  -  
    將接收連接器通訊協定記錄檔和傳送連接器通訊協定記錄檔大小上限設為 20 MB。

  -  
    將接收連接器通訊協定記錄資料夾和傳送連接器通訊協定記錄資料夾大小上限設為 400 MB。

  -  
    將接收連接器通訊協定記錄檔和傳送連接器通訊協定記錄檔的最大保留天數設為 45 天。

<!-- end list -->

    Set-TransportService Mailbox01 -ReceiveProtocolLogPath "D:\Hub Receive SMTP Log" -SendProtocolLogPath "D:\Hub Send SMTP Log" -ReceiveProtocolLogMaxFileSize 20MB -SendProtocolLogMaxFileSize 20MB -ReceiveProtocolLogMaxDirectorySize 400MB -SendProtocolLogMaxDirectorySize 400MB -ReceiveProtocolLogMaxAge 45.00:00:00 -SendProtocolLogMaxAge 45.00:00:00

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
<li><p>若要在信箱伺服器上的信箱傳輸服務中設定通訊協定記錄檔設定，請使用<strong>Set-MailboxTransportService</strong>指令程式。若要設定的通訊協定記錄檔設定 Client Access server 上 Front End Transport 服務中，使用<strong>Set-FrontEndTransportService</strong>指令程式。</p></li>
<li><p>有效地將<em>SendProtocolLogPath</em>或<em>ReceiveProtocolLogPath</em>參數設定為值<code>$null</code>停用所有的傳送連接器或伺服器上的所有接收連接器的通訊協定記錄。不過，將兩個這些參數都設<code>$null</code>的任何其他連接器的伺服器上啟用通訊協定記錄時，包括組織內傳送連接器或信箱傳遞傳送連接器，就會產生錯誤的事件記錄檔。</p></li>
<li><p>將 <em>ReceiveProtocolLogMaxAge</em> 或 <em>SendProtocolLogMaxAge</em> 參數的值設為 <code>00:00:00</code>，可以防止因為通訊協定記錄檔的保留天數而自動移除通訊協定記錄檔。</p></li>
</ul></td>
</tr>
</tbody>
</table>


## 如何才能了解這是否正常運作？

若要驗證是否已成功設定通訊協定記錄設定，請執行下列動作：

1.  在命令介面中，執行下列命令：
    
        <Get-TransportService | Get-MailboxTransportService | Get-FrontEndTransportService> <ServerIdentity> | Format-List SendConnectorProtocolLog*,ReceiveConnectorProtocolLog*

2.  請確認顯示的值是您所設定的值。

