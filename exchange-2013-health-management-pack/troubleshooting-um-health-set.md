---
title: 疑難排解 UM 健全設定
TOCTitle: 疑難排解 UM 健全設定
ms:assetid: db947791-63ce-45dd-8634-1dfa5f55e2c2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.scom.um(v=EXCHG.150)
ms:contentKeyID: 53276417
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 疑難排解 UM 健全設定

 

_**適用版本：**Exchange Server 2013, Project Server 2013_

_**上次修改主題的時間：**2015-03-09_

整合通訊 (UM) 健全設定會監視您組織中 UM 服務的整體健康狀況。

若您收到警示指定 UM 是狀況不良，表示可能會防止使用者在組織中使用 UM 服務發生問題。下列的健全設定密切相關之 UM 健全設定：

[疑難排解 UM。CallRouter 健全設定](troubleshooting-um-callrouter-health-set.md)

[疑難排解 UM。通訊協定健全設定](troubleshooting-um-protocol-health-set.md)

## 說明

UM 服務是透過下列探查與監視器受到監視。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Probe</th>
<th>健全設定</th>
<th>相依性</th>
<th>關聯的監視器</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>UMSelfTestProbe</p></td>
<td><p>UM.Protocol</p></td>
<td><p>Active Directory 網域服務 (AD DS)</p></td>
<td><p>UMSelfTestMonitor</p></td>
</tr>
<tr class="even">
<td><p>UMCallRouterTestProbe</p></td>
<td><p>UM.CallRouter</p></td>
<td><p>Active Directory 網域服務 (AD DS)</p></td>
<td><p>UMCallRouterTestMonitor</p></td>
</tr>
</tbody>
</table>


如需探查與監視器的詳細資訊，請參閱[伺服器健康狀況與效能](https://technet.microsoft.com/zh-tw/library/jj150551\(v=exchg.150\))。

## 使用者動作

服務可能在發出警示之後已復原。因此，當您收到警示指出健全設定狀況不良時，請先確認問題仍然存在。如果問題確實存在，請執行以下幾節所列出的適當復原動作。

## 確認問題仍然存在

1.  識別警示中的健全設定名稱和伺服器名稱。

2.  訊息詳細資料會提供造成警示確切原因的相關資訊。在大部分情況下，訊息詳細資料會提供足夠的疑難排解資訊來找出根本原因。如果訊息詳細資料不清楚，請執行下列動作：
    
    1.  開啟 Exchange 管理命令介面，然後執行下列命令，以擷取發出警示之健全設定的詳細資料：
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        例如，若要擷取 server1.contoso.com 的 UM.Protocol 健全設定詳細資料，請執行下列命令：
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "UM.Protocol"}
    
    2.  檢閱命令輸出，以判斷是哪個監視器回報錯誤。發出警示之監視器的 **AlertValue** 值會是 `Unhealthy`。
    
    3.  處於不健全的狀態監視器，重新執行相關聯的探查。請參閱尋找相關聯的探查 \[說明\] 區段中的表格。若要這樣做，執行下列命令：
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        例如，假設失敗監視是**UMSelfTestMonitor**。相關聯的監視探查是**UMSelfTestProbe**。若要執行的探查 server1.contoso.com 上，執行下列命令：
        
            Invoke-MonitoringProbe UM.Protocol\UMSelfTestMonitor -Server server1.contoso.com | Format-List
    
    4.  在命令輸出中，檢閱探查的 **\[結果\]** 值。如果值為 **\[成功\]**，表示問題是暫時性錯誤，且已不存在。否則，請參閱以下幾節所列的復原步驟。

## 疑難排解步驟

當您收到來自健全設定的警示時，電子郵件會包含下列資訊：

  - 傳送警示的伺服器名稱

  - 警示的發生日期和時間

  - 所使用的驗證機制及認證資訊

  - 上一個錯誤的完整例外狀況追蹤，包括診斷資料與特定的 HTTP 標頭資訊
    
    **附註** 您可以使用完整的例外狀況追蹤中的資訊，以協助疑難排解問題。探查所產生的例外狀況包含描述探查失敗的原因失敗原因。

**UM 服務的 SIP 選項已失敗 (Sip Options to UM Service have failed)**

判斷是否已停用 UM 服務。若未啟動或停用 UM 服務、 重新啟動 UM 服務。

**過去一小時內有高於 {0}% 的輸入呼叫被 UM 服務拒絕 (More than {0}% of Inbound Calls were Rejected by the UM Service Over the Last Hour)**

檢閱 Client Access Server (CAS) 上的事件記錄，判斷 UM 物件 (如 **umipgateway** 和 **umhuntgroup**) 是否設定正確。

如果事件記錄中包含的資訊不足，您可能需要啟用 \[專家\] 等級的 UM 事件記錄，然後再檢閱 UM 追蹤記錄檔。

**過去一小時內有高於 {0}% 的輸入呼叫被 UM 工作者處理序拒絕 (More than {0}% of Inbound Calls were Rejected by the UM Worker Process Over the Last Hour)**

檢閱 CAS 上的事件記錄，判斷 UM 物件 (如 **umipgateway** 和 **umhuntgroup** 物件) 是否設定正確。

如果事件記錄中包含的資訊不足，您可能需要啟用 \[專家\] 等級的 UM 事件記錄，然後再檢閱 UM 追蹤記錄檔。

**過去一小時內成功處理的郵件低於 {0}% (Less than {0}% of Messages were Successfully Processed Over the Last Hour)**

檢閱 CAS 上的事件記錄，判斷 UM 物件 (如 **umipgateway** 和 **umhuntgroup** 物件) 是否設定正確。

如果事件記錄中包含的資訊不足，您可能需要啟用 \[專家\] 等級的 UM 事件記錄，然後再檢閱 UM 追蹤記錄檔。

**Microsoft Exchange 整核通訊服務因為 UM 管線已滿而拒絕某個呼叫 (The Microsoft Exchange Unified Messaging service rejected a call because the UM pipeline is full)**

檢閱 CAS 上的事件記錄，判斷 UM 物件 (如 **umipgateway** 和 **umhuntgroup** 物件) 是否設定正確。

如果事件記錄中包含的資訊不足，您可能需要啟用 \[專家\] 等級的 UM 事件記錄，然後再檢閱 UM 追蹤記錄檔。

**A/V Edge 服務設得不當或未在執行 (The A/V Edge service is misconfigured or is not running)**

1.  檢閱嘗試以決定從 Lync server 通話失敗的原因的信箱伺服器上的事件記錄。然後執行下列動作：
    
      - 確定 UM 服務所選取的 Lync 集區正常運作。
    
      - 若要使用特定的 Lync 伺服器，請執行下列命令：
        
            Set-UMServer ExchangeUMServer -SIPAccessService <ServerName>

**UM 伺服器無法向通訊伺服器 A/V Edge 服務取得認證 (The UM server was unable to acquire credentials successfully with the Communications Server A/V Edge service)**

檢閱事件記錄來調查選取的是哪個 Lync 集區，並確認選取的 Lync 集區正常運作。

**通訊伺服器音訊/視訊 Edge 在嘗試建立工作階段時，無法開啟連接埠或配置資源 (The Communications Server Audio/Video Edge was unable to open a port or allocate resources while attempting to establish a session)**

檢閱事件記錄來調查選取的是哪個 Lync 集區，並確認選取的 Lync 集區正常運作。

**Microsoft Exchange 整合通訊服務認證快要到期 (The Microsoft Exchange Unified Messaging service certificate is nearing its expiration date)**

更新 Mailbox Server 上的 UM 服務認證。

**其他疑難排解步驟：**

1.  啟動 \[IIS 管理員\]，然後連線到回報問題的伺服器，以判斷 **MSExchangeServicesAppPool** 應用程式集區是否正在執行。

2.  在 IIS 管理員中，按一下 \[**應用程式集區**，並再回收**MSExchangeServicesAppPool**應用程式集區。若要這樣做，請從Exchange 管理命令介面執行下列命令：
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeServicesAppPool

3.  依照Verifying the issue still exists一節中的步驟 2c，重新執行相關聯的探查。

4.  如果問題仍然存在，請使用 IISReset 公用程式或執行下列命令來回收 IIS 服務。
    
        Iisreset /noforce

5.  依照Verifying the issue still exists一節中的步驟 2c，重新執行相關聯的探查。

6.  如果問題仍然存在，請重新啟動伺服器。

7.  伺服器重新啟動後，請依照Verifying the issue still exists一節中的步驟 2c，重新執行相關聯的探查。

8.  如果探查持續失敗，您可能需要協助解決此問題。請連絡 Microsoft 支援人員以解決此問題。若要連絡 Microsoft 支援人員，請造訪 [Exchange Server 解決方案中心](https://go.microsoft.com/fwlink/p/?linkid=180809)。在功能窗格中按一下 **\[支援選項與資源\]**，並使用列於 **\[取得技術支援\]** 底下的其中一個選項來連絡 Microsoft 支援專業人員。由於您的組織可能擁有直接連絡 Microsoft 產品支援服務的特定程序，因此請務必先檢閱組織的指南。

## 相關資訊

[Exchange 2013 的新功能](https://technet.microsoft.com/zh-tw/library/jj150540\(v=exchg.150\))

[Exchange 2013 指令程式](https://technet.microsoft.com/zh-tw/library/bb124413\(v=exchg.150\))

