---
title: 疑難排解 UM。CallRouter 健全設定
TOCTitle: 疑難排解 UM。CallRouter 健全設定
ms:assetid: 444a9038-0952-4823-98fb-99fa59f4a378
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.scom.um.callrouter(v=EXCHG.150)
ms:contentKeyID: 53276401
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 疑難排解 UM。CallRouter 健全設定

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

Microsoft Exchange 整合通訊 (UM) 呼叫路由器健全設定能監視 UM 呼叫路由器服務的整體健全情況。

若您收到警示指定 UM 是狀況不良，表示可能會防止使用者在組織中使用 UM 服務發生問題。下列的健全設定密切相關之 UM 健全設定：

[疑難排解 UM 健全設定](troubleshooting-um-health-set.md)

[疑難排解 UM。通訊協定健全設定](troubleshooting-um-protocol-health-set.md)

## 說明

使用下列探查和監視器可監視 UM.Protocol 服務


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
        
        例如，若要擷取有關 server1.contoso.com 的 UM.CallRouter 健全設定詳細資料，請執行下列命令：
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "UM.CallRouter"}
    
    2.  檢閱命令輸出，以判斷是哪個監視器回報錯誤。發出警示之監視器的 **AlertValue** 值會是 `Unhealthy`。
    
    3.  處於不健全的狀態監視器，重新執行相關聯的探查。請參閱尋找相關聯的探查 \[說明\] 區段中的表格。若要這樣做，執行下列命令：
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        例如，假設失敗監視是**UMCallRouterTestMonitor**。相關聯的監視探查是**UMCallRouterTestProbe**。若要執行的探查 server1.contoso.com 上，執行下列命令：
        
            Invoke-MonitoringProbe UM.CallRouter\UMCallRouterTestMonitor -Server server1.contoso.com | Format-List
    
    4.  在命令輸出中，檢閱探查的 **\[結果\]** 值。如果值為 **\[成功\]**，表示問題是暫時性錯誤，且已不存在。否則，請參閱以下幾節所列的復原步驟。

## 疑難排解步驟

當您從健全設定收到警示時，電子郵件包含下列資訊：

  - 傳送警示的伺服器名稱

  - 警示的發生日期和時間

  - 所使用的驗證機制及認證資訊

  - 上一個錯誤的完整例外狀況追蹤，包括診斷資料與特定的 HTTP 標頭資訊
    
    **附註**  您可以使用完整的例外狀況追蹤中的資訊，以協助疑難排解問題。探查所產生的例外狀況包含描述探查失敗的原因失敗原因。

**UM 呼叫路由器服務的 SIP 選項已失敗**

判斷是否已停用 UM 呼叫路由器服務。若未啟動或停用 UM 呼叫路由器服務，重新啟動 UM 服務。

**UM 呼叫路由器在過去一小時內拒絕了 50% 以上的輸入呼叫**

檢閱 Client Access Server (CAS) 上的事件記錄，判斷 UM 物件 (如 **umipgateway** 和 **umhuntgroup**) 的設定是否正確。

如果事件記錄提供的資訊不足，您可能需要啟用 \[最高\] 等級的 UM 事件記錄，然後再檢閱 UM 追蹤記錄檔。

**在過去一小時內 UM 呼叫路由器有超過 {0}% 的未接來電通知 Proxy 發生失敗**

檢閱 CAS 上的事件記錄，判斷 UM 物件 (如 **umipgateway** 和 **umhuntgroup**) 的設定是否正確。

如果事件記錄提供的資訊不足，您可能需要啟用 \[最高\] 等級的 UM 事件記錄，然後再檢閱 UM 追蹤記錄檔。

**Microsoft Exchange 整合通訊呼叫路由器憑證即將到期**

檢閱 CAS 上的 UM 呼叫路由器服務憑證。

**其他疑難排解步驟：**

1.  啟動 IIS 管理員，接著連線到報告問題的伺服器以判斷 **MSExchangeServicesAppPool** 應用程式集區是否正在執行。

2.  在 IIS 管理員中，按一下 **\[應用程式集區\]**，然後從命令介面執行下列命令，回收 **MSExchangeServicesAppPool** 應用程式集區：
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeServicesAppPool

3.  重新執行關聯的探查，如Verifying the issue still exists一節中的步驟 2c 所示。

4.  如果問題仍然存在，請使用 IISReset 公用程式或執行下列命令來回收 IIS 服務：
    
        Iisreset /noforce

5.  重新執行關聯的探查，如Verifying the issue still exists一節中的步驟 2c 所示。

6.  如果問題仍然存在，請重新啟動伺服器。

7.  在伺服器重新啟動之後，請重新執行關聯的探查，如Verifying the issue still exists一節中的步驟 2c 所示。

8.  如果探查持續失敗，您可能需要協助解決此問題。請連絡 Microsoft 支援人員以解決此問題。若要連絡 Microsoft 支援人員，請造訪 [Exchange Server 解決方案中心](https://go.microsoft.com/fwlink/p/?linkid=180809)。在功能窗格中按一下 **\[支援選項與資源\]**，並使用列於 **\[取得技術支援\]** 底下的其中一個選項來連絡 Microsoft 支援專業人員。由於您的組織可能擁有直接連絡 Microsoft 產品支援服務的特定程序，因此請務必先檢閱組織的指南。

## 相關資訊

[Exchange 2013 的新功能](https://technet.microsoft.com/zh-tw/library/jj150540\(v=exchg.150\))

[Exchange 2013 指令程式](https://technet.microsoft.com/zh-tw/library/bb124413\(v=exchg.150\))

