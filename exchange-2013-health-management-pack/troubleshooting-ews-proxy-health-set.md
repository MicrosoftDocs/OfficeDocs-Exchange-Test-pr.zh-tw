---
title: 疑難排解 EWS。Proxy 健全設定
TOCTitle: 疑難排解 EWS。Proxy 健全設定
ms:assetid: 5bfbf7e9-d52d-4a3d-91ac-72427c6cb37d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.scom.ews.proxy(v=EXCHG.150)
ms:contentKeyID: 53276403
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 疑難排解 EWS。Proxy 健全設定

 

_**適用版本：** Exchange Server 2013_

_**上次修改主題的時間：** 2015-03-09_

EWS。Proxy 健全設定監視用戶端存取伺服器 (CAS) 上的Exchange Web 服務 (EWS) proxy 基礎結構的可用性。EWS。下列狀況一組密切相關 proxy 健全設定：

[疑難排解 ClientAccess.Proxy 健全設定](troubleshooting-clientaccess-proxy-health-set.md)

如果您收到警示，指出 EWS.Proxy 的狀況不良，表示可能有問題令使用者無法存取 EWS 服務。

## 說明

EWS 服務是透過下列探查與監視器受到監視。


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
<td><p>EWSProxyTestProbe</p></td>
<td><p>EWS.Proxy</p></td>
<td><p>Active Directory</p></td>
<td><p>EWSProxyTestMonitor</p></td>
</tr>
</tbody>
</table>


如需探查與監視器的詳細資訊，請參閱[伺服器健康狀況與效能](https://technet.microsoft.com/zh-tw/library/jj150551\(v=exchg.150\))。

## 常見問題

下列任一常見原因都可能導致此探查失敗：

  - 位於受監視 CAS 上的應用程式集區未正常運作。

  - 監視帳戶認證不正確。

  - 網域控制站無回應。

## 使用者動作

服務可能在發出警示之後已復原。因此，當您收到警示指出健全設定狀況不良時，請先確認問題仍然存在。如果問題確實存在，請執行以下幾節所列出的適當復原動作。

## 確認問題仍然存在

1.  識別警示中的健全設定名稱和伺服器名稱。

2.  訊息詳細資料會提供造成警示確切原因的相關資訊。在大部分情況下，訊息詳細資料會提供足夠的疑難排解資訊來找出根本原因。如果訊息詳細資料不清楚，請執行下列動作：
    
    1.  開啟 Exchange 管理命令介面，然後執行下列命令，以擷取發出警示之健全設定的詳細資料：
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        例如，若要擷取 server1.contoso.com 的 EWS.Proxy 健全設定詳細資料，請執行下列命令：
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "EWS.Proxy"}
    
    2.  檢閱命令輸出，以判斷是哪個監視器回報錯誤。發出警示之監視器的 **AlertValue** 值會是 `Unhealthy`。
    
    3.  處於不健全的狀態監視器，重新執行相關聯的探查。請參閱尋找相關聯的探查Verifying 問題仍然存在\] 區段中的表格。若要這樣做，執行下列命令：
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        例如，假設失敗監視是**EWSProxyTestMonitor**。相關聯的監視探查是**EWSProxyTestProbe**。若要執行的探查 server1.contoso.com 上，執行下列命令：
        
            Invoke-MonitoringProbe EWS.Proxy\EWSProxyTestProbe -Server server1.contoso.com | Format-List
    
    4.  在命令輸出中，檢閱探查的 **\[結果\]** 值。如果值為 **\[成功\]**，表示問題是暫時性錯誤，且已不存在。否則，請參閱以下幾節所列的復原步驟。

## EWSProxyTestMonitor 復原動作

當您收到來自健全設定的警示時，電子郵件會包含下列資訊：

  - 傳送警示之 CAS 的名稱

  - 上一個錯誤的完整例外狀況追蹤，包括診斷資料與特定的 HTTP 標頭資訊
    
    您可以使用完整例外狀況追蹤中的資訊，協助疑難排解問題。

  - 發生問題的時間和日期

若要疑難排解此問題，請遵循下列步驟：

1.  檢閱 CA 伺服器上的通訊協定記錄檔。通訊協定記錄檔位於上之 CAS 的*\<exchange server installation directory\>*\\Logging\\HttpProxy*\\\<protocol\>*資料夾中。

2.  建立測試使用者帳戶，然後再登入 CA 所使用的測試使用者帳戶。例如，使用下列登入地址： https:// *\<servername\>*/owa

3.  啟動 \[IIS 管理員\]，然後連線到回報問題的伺服器，以判斷 CAS 上是否正在執行 **MSExchangeServicesAppPool** 應用程式集區。

4.  按一下 **\[應用程式集區\]**，然後在命令介面中執行下列命令，以重複使用 **MSExchangeServicesAppPool** 應用程式集區：
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeServicesAppPool

5.  依照Verifying the issue still exists一節中的步驟 2c，重新執行相關聯的探查。

6.  如果問題仍然存在，請使用 IISReset 公用程式回收 IIS 服務。

7.  依照Verifying the issue still exists一節中的步驟 2c，重新執行相關聯的探查。

8.  如果問題仍然存在，請重新啟動伺服器。

9.  伺服器重新啟動後，請依照Verifying the issue still exists一節中的步驟 2c，重新執行相關聯的探查。

10. 如果探查持續失敗，您可能需要協助解決此問題。請連絡 Microsoft 支援人員以解決此問題。若要連絡 Microsoft 支援人員，請造訪 [Exchange Server 解決方案中心](https://go.microsoft.com/fwlink/p/?linkid=180809)。在功能窗格中按一下 **\[支援選項與資源\]**，並使用列於 **\[取得技術支援\]** 底下的其中一個選項來連絡 Microsoft 支援專業人員。由於您的組織可能擁有直接連絡 Microsoft 產品支援服務的特定程序，因此請務必先檢閱組織的指南。

## 相關資訊

[Exchange 2013 的新功能](https://technet.microsoft.com/zh-tw/library/jj150540\(v=exchg.150\))

[Exchange 2013 指令程式](https://technet.microsoft.com/zh-tw/library/bb124413\(v=exchg.150\))

