---
title: 疑難排解 ECP 健全設定
TOCTitle: 疑難排解 ECP 健全設定
ms:assetid: 0a1cfcd5-585c-4a0a-9d3c-28dc49e16a6c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.scom.ecp(v=EXCHG.150)
ms:contentKeyID: 53276395
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 疑難排解 ECP 健全設定

 

_**適用版本：**Exchange Server 2013, Project Server 2013_

_**上次修改主題的時間：**2015-03-09_

Exchange 控制台 (ECP) 健全設定監視Exchange系統管理中心 (EAC) 和Outlook Web App (OWA) 使用者設定服務的整體狀況。下列狀況一組密切相關 ECP 健全設定：

[疑難排解 ECP。Proxy 健全設定](troubleshooting-ecp-proxy-health-set.md)

如果您收到警示指定 ECP 健全設定的狀況不良，這表示可能會讓使用者無法存取 EAC 發生問題。

## 說明

EAC 服務是使用下列探查及監視器來監視的。


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
<td><p>EacSelfTestProbe</p></td>
<td><p>ECP</p></td>
<td><p>Active Directory</p></td>
<td><p>EacSelfTestMonitor</p></td>
</tr>
<tr class="even">
<td><p>EacDeepTestProbe</p></td>
<td><p>ECP</p></td>
<td><p>Active Directory</p></td>
<td><p>EacDeepTestMonitor</p></td>
</tr>
</tbody>
</table>


如需探查與監視器的詳細資訊，請參閱[伺服器健康狀況與效能](https://technet.microsoft.com/zh-tw/library/jj150551\(v=exchg.150\))。

## 使用者動作

當您從健全設定收到警示時，電子郵件包含下列資訊：

  - 傳送警示的伺服器名稱

  - 警示的發生日期和時間

  - 驗證及認證資訊

  - 上一個錯誤的完整例外狀況追蹤，包括診斷資料與特定的 HTTP 標頭資訊
    
    **附註**   您可以使用完整例外狀況追蹤中的資訊，協助疑難排解問題。

服務可能在發出警示之後已復原。因此，當您收到警示指出健全設定狀況不良時，請先確認問題仍然存在。如果問題確實存在，請執行以下幾節所列出的適當復原動作。

## 確認問題仍然存在

1.  識別警示中的健全設定名稱和伺服器名稱。

2.  郵件的詳細資訊提供的確切原因的警示的資訊。在大多數情況下，郵件詳細資料會提供足夠識別根本原因的疑難排解資訊。如果不清楚郵件的詳細資訊，請遵循下列步驟：
    
    1.  開啟 Exchange 管理命令介面，然後執行下列命令，以擷取發出警示之健全設定的詳細資料：
        
            Get-ServerHealth -Identity <ServerName> -HealthSet <HealthSetName>
        
        例如，若要擷取 ECP 健全設定詳細 server1.contoso.com，執行下列命令：
        
            Get-ServerHealth -Identity server1.contoso.com -HealthSetName ECP
    
    2.  檢閱命令輸出，以判斷是哪個監視器回報錯誤。發出警示之監視器的 **AlertValue** 值會是 `Unhealthy`。
    
    3.  請為不健康狀態監視重新執行相關聯的探查。請參閱尋找相關聯的探查 \[說明\] 區段中的表格。若要這樣做，執行下列命令：
        
            Invoke-MonitoringProbe <HealthSetName>\<ProbeName> -Server <ServerName> | Format-List
        
        例如，假設失敗監視是**EacSelfTestMonitor**。相關聯的監視探查是**EacSelfTestProbe**。若要執行的探查 server1.contoso.com 上，執行下列命令：
        
            Invoke-MonitoringProbe ECP\EacSelfTestProbe -Server server1.contoso.com | Format-List
    
    4.  在命令輸出中，檢閱探查的 **\[結果\]** 值。如果值為 **\[成功\]**，表示問題是暫時性錯誤，且已不存在。否則，請參閱以下幾節所列的復原步驟。

## EacSelfTestMonitor 及 EacDeepTestMonitor 復原動作

1.  啟動 IIS 管理員中，並再連線到回報問題的伺服器。按一下 \[**應用程式集區**，然後再回收名為**MSExchangeECPAppPool**ECP 應用程式集區。

2.  重新執行關聯的探查，如Verifying the issue still exists一節中的步驟 2c 所示。

3.  如果問題仍然存在，請使用 IISReset 公用程式來回收整個 IIS 服務。

4.  重新執行關聯的探查，如Verifying the issue still exists一節中的步驟 2c 所示。

5.  如果探查失敗，請重新啟動伺服器。

6.  在伺服器重新啟動之後，請重新執行關聯的探查，如Verifying the issue still exists一節中的步驟 2c 所示。

7.  如果探查持續失敗，您可能需要協助解決此問題。請連絡 Microsoft 支援人員以解決此問題。若要連絡 Microsoft 支援人員，請造訪 [Exchange Server 解決方案中心](https://go.microsoft.com/fwlink/p/?linkid=180809)。在功能窗格中按一下 **\[支援選項與資源\]**，並使用列於 **\[取得技術支援\]** 底下的其中一個選項來連絡 Microsoft 支援專業人員。由於您的組織可能擁有直接連絡 Microsoft 產品支援服務的特定程序，因此請務必先檢閱組織的指南。

## 相關資訊

[Exchange 2013 的新功能](https://technet.microsoft.com/zh-tw/library/jj150540\(v=exchg.150\))

[Exchange 2013 指令程式](https://technet.microsoft.com/zh-tw/library/bb124413\(v=exchg.150\))

[Exchange 2013 中的 Exchange 系統管理中心](https://technet.microsoft.com/zh-tw/library/jj150562\(v=exchg.150\))

