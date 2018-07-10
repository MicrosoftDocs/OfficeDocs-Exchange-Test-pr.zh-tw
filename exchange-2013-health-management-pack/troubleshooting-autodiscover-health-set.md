---
title: 疑難排解自動探索健康情況設定
TOCTitle: 疑難排解自動探索健康情況設定
ms:assetid: bc933621-df73-4d1d-bdef-825b98be8e09
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.scom.autodiscover(v=EXCHG.150)
ms:contentKeyID: 53276416
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 疑難排解自動探索健康情況設定

 

_**適用版本：** Exchange Server 2013_

_**上次修改主題的時間：** 2015-03-09_

自動探索健全設定會為用戶端來監視自動探索服務的整體健康狀況。

如果您收到警示，指出自動探索的狀況不良，表示可能有問題令使用者無法使用自動探索處理程序來存取信箱。

## 說明

自動探索服務是透過下列探查與監視器受到監視。


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
<td><p>AutodiscoverCtpProbe</p></td>
<td><p>自動探索</p></td>
<td><p>Active Directory</p></td>
<td><p>AutodiscoverCtpMonitor</p></td>
</tr>
</tbody>
</table>


如需探查與監視器的詳細資訊，請參閱[伺服器健康狀況與效能](https://technet.microsoft.com/zh-tw/library/jj150551\(v=exchg.150\))。

## 常見問題

下列任一常見原因都可能導致此探查失敗：

  - 架設在受監視的 Client Access server (CAS) 的自動探索應用程式集區 (MSExchangeAutodiscoverAppPool) 沒有回應。或者，架設在一個或多個信箱伺服器的自動探索應用程式集區沒有回應。

  - CAS 發生網路問題，無法連線到 Mailbox Server 或網域控制站。

  - 監視帳戶認證不正確。

  - 網域控制站無回應。

## 使用者動作

有可能服務復原之後則發出警示。因此，當您收到警示之健全設定為不健康會指定，先確認問題仍然存在。如果問題不存在，執行下列各節所述的適當的復原動作。

## 確認問題仍然存在

1.  識別警示中的健全設定名稱和伺服器名稱。

2.  訊息詳細資料會提供造成警示確切原因的相關資訊。在大部分情況下，訊息詳細資料會提供足夠的疑難排解資訊來找出根本原因。如果訊息詳細資料不清楚，請執行下列動作：
    
    1.  開啟 Exchange 管理命令介面，然後執行下列命令，以擷取發出警示之健全設定的詳細資料：
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        例如，若要擷取 server1.contoso.com 的自動探索健全設定詳細資料，請執行下列命令：
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "Autodiscover"}
    
    2.  檢閱命令的輸出傳送至決定顯示器回報的錯誤。發出警示監視器**AlertValue**值為`Unhealthy`。
    
    3.  請為不健康狀態監視重新執行相關聯的探查。請參閱尋找相關聯的探查 \[說明\] 區段中的表格。若要這樣做，執行下列命令：
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        例如，假設失敗監視是**AutodiscoverCtpMonitor**。相關聯的監視探查是**AutodiscoverCtpProbe**。若要執行的探查 server1.contoso.com 上，執行下列命令：
        
            Invoke-MonitoringProbe Autodiscover\AutodiscoverCtpProbe -Server server1.contoso.com | Format-List
    
    4.  在命令輸出中，檢閱探查的 **\[結果\]** 值。如果值為 **\[成功\]**，表示問題是暫時性錯誤，且已不存在。否則，請參閱以下幾節所列的復原步驟。

## AutodiscoverCtpMonitor 復原動作

當您收到來自健全設定的警示時，電子郵件會包含下列資訊：

  - 傳送警示的伺服器名稱

  - 探查所監視的 Mailbox Server 名稱

  - 警示的發生日期和時間

  - 所使用的驗證機制及認證資訊

  - 上一個錯誤的完整例外狀況追蹤，包括診斷資料與特定的 HTTP 標頭資訊

您可以使用完整的例外狀況追蹤中的資訊，以協助疑難排解問題。探查所產生的例外狀況包含描述探查失敗的原因失敗原因。例如，失敗原因可能是下列其中一項：

  - **X-FEServer**   指出執行探查的 CAS

  - **X-CalculatedBETarget**   指出要求被路由傳送到的 Mailbox Server

  - **X-DiagInfo**   指出收到要求的 Mailbox Server

若要疑難排解此問題，請遵循下列步驟：

1.  檢閱 CA 與 Mailbox server 上的通訊協定記錄檔。根據預設，在 CA 上的通訊協定記錄檔位於***\<exchange server installation directory\>*\\Logging\\HttpProxy\\Autodiscover**資料夾中。根據預設，在 Mailbox server 上的通訊協定記錄檔位於***\<exchange server installation directory\>*\\Logging\\Autodiscover**資料夾中。

2.  建立測試使用者帳戶，然後再登入 CA 所使用的測試使用者帳戶。例如，使用登入： https://*\<servername\>*/autodiscover/autodiscover.xml。
    
    如果測試使用者帳戶名稱通過驗證，則問題可能出在受監視信箱所在的 Mailbox Server。
    
    嘗試使用的測試帳戶的信箱伺服器上重複上述步驟。如果此嘗試失敗，請嘗試執行測試以確認問題發生在特定的 CAS 和 Mailbox server 上不具有不同 CAS。

3.  確認 CA 與 Mailbox server 之間的網路連線。若要確認每部伺服器在回應使用 ping.exe。

4.  檢查 Autodiscover.Proxy 健全設定上警示可能指出問題影響特定的 Mailbox server。如需詳細資訊，請參閱[疑難排解 Autodiscover.Proxy 健全設定](troubleshooting-autodiscover-proxy-health-set.md)。

5.  檢查 Autodiscover.Protocol 健全設定上警示可能指出有問題影響特定的 Mailbox server。如需詳細資訊，請參閱[疑難排解 Autodiscover.Protocol 健全設定](troubleshooting-autodiscover-protocol-health-set.md)。

6.  啟動 IIS 管理員中，並再連線到回報問題的伺服器。確認**MSExchangeAutodiscoverAppPool**應用程式集區 CA 與 Mailbox server 上執行。

7.  在 \[IIS 管理員\] 中，按一下 **\[應用程式集區\]**，然後從命令介面執行下列命令，以回收 **MSExchangeAutodiscoverAppPool** 應用程式集區：
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeAutodiscoverAppPool

8.  依照Verifying the issue still exists一節中的步驟 2c，重新執行相關聯的探查。

9.  如果問題仍然存在，請使用 IISReset 公用程式或執行下列命令來回收 IIS 服務。
    
        Iisreset /noforce

10. 依照Verifying the issue still exists一節中的步驟 2c，重新執行相關聯的探查。

11. 如果問題仍然存在，請重新啟動伺服器。

12. 伺服器重新啟動後，請依照Verifying the issue still exists一節中的步驟 2c，重新執行相關聯的探查。

13. 如果探查持續失敗，您可能需要協助解決此問題。請連絡 Microsoft 支援人員以解決此問題。若要連絡 Microsoft 支援人員，請造訪 [Exchange Server 解決方案中心](https://go.microsoft.com/fwlink/p/?linkid=180809)。在功能窗格中按一下 **\[支援選項與資源\]**，並使用列於 **\[取得技術支援\]** 底下的其中一個選項來連絡 Microsoft 支援專業人員。由於您的組織可能擁有直接連絡 Microsoft 產品支援服務的特定程序，因此請務必先檢閱組織的指南。

## 相關資訊

[Exchange 2013 的新功能](https://technet.microsoft.com/zh-tw/library/jj150540\(v=exchg.150\))

[Exchange 2013 指令程式](https://technet.microsoft.com/zh-tw/library/bb124413\(v=exchg.150\))

