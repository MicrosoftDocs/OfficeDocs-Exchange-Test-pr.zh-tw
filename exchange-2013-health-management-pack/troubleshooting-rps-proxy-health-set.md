---
title: 疑難排解 RPS。Proxy 健全設定
TOCTitle: 疑難排解 RPS。Proxy 健全設定
ms:assetid: a5058323-5d86-438a-ad4a-fa4292310e98
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.scom.rps.proxy(v=EXCHG.150)
ms:contentKeyID: 53276409
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 疑難排解 RPS。Proxy 健全設定

 

_**適用版本：** Exchange Server 2013_

_**上次修改主題的時間：** 2015-03-09_

RPS.Proxy 健全設定會監控遠端 PowerShell 服務的整體健康狀況。

如果您收到警示，指出 RPS.Proxy 狀況不良，這可能代表發生讓您無法使用遠端 PowerShell 存取 Exchange 的問題。

## 說明

系統使用下列探查和監視器來監視 RPS 服務：


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
<td><p>RPSProxyTestProbe</p></td>
<td><p>RPS.Proxy</p></td>
<td><p>Active Directory</p></td>
<td><p>RPSProxyTestMonitor</p></td>
</tr>
</tbody>
</table>


如需探查與監視器的詳細資訊，請參閱[伺服器健康狀況與效能](https://technet.microsoft.com/zh-tw/library/jj150551\(v=exchg.150\))。

## 常見問題

此探查失敗時可以有多個問題的原因。一些較常見問題包括下列：

  - 所監控之 CAS 伺服器上主控的應用程式集區未正常運作。

  - 監控帳戶認證不正確。

  - 網域控制站無回應。

## 使用者動作

有可能服務已無法復原後發出警示。因此，當您收到警示之健全設定為不健康，，的最先應該做的是確認問題仍然存在。若是如此，然後執行下列各節所述的適當的復原動作。

## 確認問題仍然存在

1.  識別警示中的健全設定名稱和伺服器名稱。

2.  郵件的詳細資訊提供資訊項目完全造成會引發通知。在大多數情況下，郵件詳細資料會提供足夠識別根本原因的疑難排解資訊。如果不清楚郵件的詳細資訊，請執行下列動作：
    
    1.  開啟 Exchange 管理命令介面，然後執行下列命令以擷取發出警示之健全設定的詳細資料：
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        例如，若要擷取 server1.contoso.com 上 RPS.Proxy 健全設定的詳細資料，請執行下列命令：
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "RPS.Proxy"}
    
    2.  檢閱命令輸出，並決定獲報錯誤的監視器。發出警示監視器**AlertValue**會讀取`Unhealthy`。
    
    3.  不健康狀態監視請重新執行相關聯的探查。請參閱尋找相關聯的探查 \[說明\] 區段中的表格。若要這樣做，執行下列命令：
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        例如，假設失敗監視已**RPSProxyTestMonitor**。相關聯的監視探查是**RPSProxyTestProbe**。若要執行的探查伺服器 server1.contoso.com 上，執行下列命令：
        
            Invoke-MonitoringProbe RPS.Proxy\RPSProxyTestProbe -Server server1.contoso.com | Format-List
    
    4.  命令輸出中，檢閱**結果**的探查。如果值為**成功**，問題是暫時性錯誤與不存在。否則，請參閱下列各節所述的復原步驟。

## RPSProxyTestMonitor 復原動作

從健全設定收到警示時，電子郵件會包含下列資訊：

  - 傳送警示之 CAS 伺服器的名稱。

  - 完整例外狀況追蹤包括 eroor 訊息、 診斷資料與特定的 HTTP 標頭資訊。在完整例外狀況追蹤資訊可用來協助疑難排解問題。

  - 問題的發生日期和時間。

若要解決此問題，請執行下列步驟：

1.  檢閱在 CAS 伺服器上的通訊協定記錄檔。通訊協定記錄檔位於 CAS 伺服器上的 \[ *\<exchange server installation directory\>*\\Logging\\HttpProxy*\\\<protocol\>* \] 資料夾。

2.  建立測試使用者帳戶，然後使用此測試使用者帳戶登入 CAS 伺服器，例如 https:// *\<伺服器名稱\>*/owa

3.  啟動 IIS 管理員並連線到回報問題的伺服器，確認 MSExchangePowerShellFrontEndAppPool 有在 CAS 伺服器上執行。

4.  按一下 **\[應用程式集區\]**，然後從 Exchange 管理命令介面執行下列命令，回收 **MSExchangePowerShellFrontEndAppPool** 應用程式集區：
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangePowerShellFrontEndAppPool

5.  重新執行關聯的探查，如Verifying the issue still exists一節中的步驟 2.c. 所示。

6.  如果問題仍然存在，請使用 IISReset 公用程式來回收 IIS 服務。

7.  重新執行關聯的探查，如Verifying the issue still exists一節中的步驟 2.c. 所示。

8.  如果問題仍然存在，請重新啟動伺服器。

9.  在伺服器重新啟動之後，請重新執行關聯的探查，如Verifying the issue still exists一節中的步驟 2.c. 所示。

10. 如果探查持續失敗，您可能需要協助解決此問題。請連絡 Microsoft 支援人員以解決此問題。若要連絡 Microsoft 支援人員，請造訪 [Exchange Server 解決方案中心](https://go.microsoft.com/fwlink/p/?linkid=180809)。在功能窗格中按一下 **\[支援選項與資源\]**，並使用列於 **\[取得技術支援\]** 底下的其中一個選項來連絡 Microsoft 支援專業人員。由於您的組織可能擁有直接連絡 Microsoft 產品支援服務的特定程序，因此請務必先檢閱組織的指南。

## 相關資訊

[Exchange 2013 的新功能](https://technet.microsoft.com/zh-tw/library/jj150540\(v=exchg.150\))

[Exchange 2013 指令程式](https://technet.microsoft.com/zh-tw/library/bb124413\(v=exchg.150\))

