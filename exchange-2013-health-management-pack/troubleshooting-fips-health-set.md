---
title: 疑難排解 FIPS 健全設定
TOCTitle: 疑難排解 FIPS 健全設定
ms:assetid: 96e1b096-9cb5-426f-a84e-50d5599e4bbb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.scom.fips(v=EXCHG.150)
ms:contentKeyID: 54652639
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 疑難排解 FIPS 健全設定

 

_**適用版本：**Exchange Server 2013, Project Server 2013_

_**上次修改主題的時間：**2016-12-09_

**FIPS**健全設定監視Exchange的伺服器上的美國聯邦資訊處理標準 (FIPS) 設定的整體狀況。如需 FIPS 140 的詳細資訊，請參閱 ＜ [FIPS 140 驗證](https://go.microsoft.com/fwlink/p/?linkid=521913)。

若您收到警示，指出**FIPS**健全設定的狀況不良，表示可能會防止您Exchange伺服器使用 FIPS 140 cls-compliant 元件及流程發生問題。

## 說明

**FIPS**服務是使用下列探查與監視器來監視。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Probe</th>
<th>健全設定</th>
<th>關聯的監視器</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>FIPS</p></td>
<td><p>CrashEvent.scanningprocess</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>FIPS</p></td>
<td><p>MaintenanceFailureMonitor.FIPS</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>FIPS</p></td>
<td><p>MaintenanceTimeoutMonitor.FIPS</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>FIPS</p></td>
<td><p>PrivateWorkingSetWarning.scanningprocess</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>FIPS</p></td>
<td><p>PrivateWorkingSetError.scanningprocess</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>FIPS</p></td>
<td><p>ProcessProcessorTimeWarning.scanningprocess</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>FIPS</p></td>
<td><p>ProcessProcessorTimeError.scanningprocess</p></td>
</tr>
</tbody>
</table>


如需探查與監視器的詳細資訊，請參閱[伺服器健康狀況與效能](https://technet.microsoft.com/zh-tw/library/jj150551\(v=exchg.150\))。

## 使用者動作

有可能服務復原之後則發出警示。因此，當您收到警示指定**FIPS**健全設定的狀況不良，先確認問題仍然存在。如果問題不存在，執行下列一節所述的適當的復原動作。

## 確認問題

1.  識別警示中提供的健全設定名稱與伺服器名稱。

2.  郵件的詳細資訊提供的確切原因的警示的資訊。在大多數情況下，郵件詳細資料會提供足夠來協助識別根本原因的疑難排解資訊。如果不清楚郵件的詳細資訊，請執行下列動作：
    
    1.  開啟 Exchange 管理命令介面，然後執行下列命令，以擷取發出警示之健全設定的詳細資料：
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        例如，若要擷取**FIPS**健全設定詳細 server1.contoso.com，執行下列命令：
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "FIPS"}
    
    2.  檢閱命令的輸出傳送至決定顯示器回報的錯誤。發出警示監視器**AlertValue**值會是**Unhealthy**。

