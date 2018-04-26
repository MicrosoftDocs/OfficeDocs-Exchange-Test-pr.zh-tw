---
title: 疑難排解 UM。通訊協定健全設定
TOCTitle: 疑難排解 UM。通訊協定健全設定
ms:assetid: 8dd9a16f-77a1-4a8d-aea4-5e96ab922dd4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.scom.um.protocol(v=EXCHG.150)
ms:contentKeyID: 53276407
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 疑難排解 UM。通訊協定健全設定

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

UM.Protocol 健全設定可以監控 Mailbox Server 上的整合通訊 (UM) 通訊協定。

如果您收到警示指定之 UM。通訊協定是狀況不良，這表示可能會防止使用者在組織中使用 UM 服務發生問題。UM。下列的健全設定密切相關通訊協定健全設定：

[疑難排解 UM 健全設定](troubleshooting-um-health-set.md)

[疑難排解 UM。CallRouter 健全設定](troubleshooting-um-callrouter-health-set.md)

## 說明

系統使用下列探查和監視器來監視 UM.Protocol 服務。


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
        
        例如，若要擷取有關 server1.contoso.com 的 UM.Protocol 健全設定詳細資料，請執行下列命令：
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "UM.Protocol"}
    
    2.  檢閱命令輸出，以判斷是哪個監視器回報錯誤。發出警示之監視器的 **AlertValue** 值會是 `Unhealthy`。
    
    3.  請為不健康狀態監視重新執行相關聯的探查。請參閱尋找相關聯的探查 \[說明\] 區段中的表格。若要這樣做，執行下列命令：
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        例如，假設失敗監視是**UMSelfTestMonitor**。相關聯的監視探查是**UMSelfTestProbe**。若要執行的探查 server1.contoso.com 上，執行下列命令：
        
            Invoke-MonitoringProbe UM.Protocol\UMSelfTestMonitor -Server server1.contoso.com | Format-List
    
    4.  在命令輸出中，檢閱探查的 **\[結果\]** 值。如果值為 **\[成功\]**，表示問題是暫時性錯誤，且已不存在。否則，請參閱以下幾節所列的復原步驟。

## 疑難排解步驟

當您從健全設定收到警示時，電子郵件包含下列資訊：

  - 傳送警示的伺服器名稱

  - 警示的發生日期和時間

  - 所使用的驗證機制及認證資訊

  - 上一個錯誤的完整例外狀況追蹤，包括診斷資料與特定的 HTTP 標頭資訊
    
    **附註**  您可以使用完整的例外狀況追蹤中的資訊，以協助疑難排解問題。探查所產生的例外狀況包含描述探查失敗的原因失敗原因。

如需疑難排解 UJM 警示訊息的詳細資訊，請參閱[疑難排解 UM 健全設定](troubleshooting-um-health-set.md)

## 相關資訊

[Exchange 2013 的新功能](https://technet.microsoft.com/zh-tw/library/jj150540\(v=exchg.150\))

[Exchange 2013 指令程式](https://technet.microsoft.com/zh-tw/library/bb124413\(v=exchg.150\))

