---
title: 使用 Exchange Server 2013 管理組件進行疑難排解
TOCTitle: 使用 Exchange Server 2013 管理組件進行疑難排解
ms:assetid: c9672dad-1e67-4f07-bad9-539a67f2ac70
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn195913(v=EXCHG.150)
ms:contentKeyID: 53276431
ms.date: 08/29/2014
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 使用 Exchange Server 2013 管理組件進行疑難排解

 

_**上次修改主題的時間：**  2013-04-09_

[Exchange Server 2013 管理組件快速入門](getting-started-with-exchange-server-2013-management-pack.md)會提供管理組件儀表板的概觀。本主題會帶領您了解如何使用此儀表板進行問題疑難排解。整個程序用範例最能清楚說明。請考慮下列案例：

Rob Fielder 是 Contoso 的 Exchange 系統管理員。他開啟了 SCOM 主控台，然後按一下 Exchange Server 2013 儀表板中的 **\[伺服器健康狀況\]**，以檢查其 Exchange 伺服器的狀態。他發現其中一部 CAS 伺服器的 **\[服務元件\]** 處於嚴重狀態。

![失敗的 CAS 伺服器](images/Dn195913.32a265d9-68e0-4d8c-9f83-1d10cdda1f84(EXCHG.150).png "失敗的 CAS 伺服器")

Rob 按兩下該伺服器，而開啟了 **\[健全狀況總管\]** 視窗。在此視窗中，他可以看到狀況不良的伺服器元件為 OWA.Proxy 健全設定。他按一下此健全設定，以檢視其相關資訊。

![失敗的 CAS 伺服器健全設定詳細資料](images/Dn195913.8e4d05a6-9128-40d8-b262-e60e9affc973(EXCHG.150).png "失敗的 CAS 伺服器健全設定詳細資料")

提供於「外部知識庫資源」下方的連結，將 Rob 導向至 [疑難排解 OWA.Proxy 健全設定](https://technet.microsoft.com/zh-tw/library/jj737712\(v=exchg.150\))主題。在此文章中，Rob 了解到首要工作是要確認問題是否仍存在。他依循指示在命令介面中執行了下列命令，以確認 OWA.Proxy 健全設定目前的狀態：

```Powershell
    Get-ServerHealth Server1.contoso.com | ?{$_.HealthSetName -eq "OWA.Proxy"}
```

執行此命令後產生了下列輸出：

```Powershell
    Server          State           Name                 TargetResource       HealthSetName   AlertValue ServerComp
                                                                                                         onent
    ------          -----           ----                 --------------       -------------   ---------- ----------
    Server1         Online          OWAProxyTestMonitor  MSExchangeOWAAppPool OWA.Proxy       Unhealthy  OwaProxy
    Server1         Online          OWAProxyTestMonitor  MSExchangeOWACale... OWA.Proxy       Healthy    OwaProxy
```

Rob 發現問題出在 OWA 應用程式集區中。下個步驟是要為狀況不良的監視器重新執行相關聯的探查。他透過「OWA.Proxy 健全設定的疑難排解」主題中的表格，判斷需要重新執行的探查應為 OWAProxyTestProbe。他執行了下列命令：

```Powershell
    Invoke-MonitoringProbe OWA.Proxy\OWAProxyTestProbe -Server Server1.contoso.com | Format-List
```

他掃描了 ResultType 值的輸出，發現探查失敗：

```Powershell
    ResultType : Failed
```

他繼續執行該文章中的「OWAProxyTestMonitor 復原動作」一節。他使用 IIS 管理員連線到 Server1，看看 MSExchangeOWAAppPool 是否在該 IIS 伺服器上執行。確認正在執行後，下個步驟指示他將 MSExchangeOWAAppPool 回收：

```Powershell
    C:\Windows\System32\Inetsrv\Appcmd recycle APPPOOL MSExchangeOWAAppPool
```

確認 MSExchangeOWAAppPool 已成功回收後，他使用 Invoke-MonitoringProbe 指令程式重新執行探查來再次確認問題是否仍存在，而這次他發現結果是成功的。接著，他執行了下列命令，以確認健全設定已重新回報 **\[狀況良好\]** 狀態：

```Powershell
    Get-ServerHealth Server1.contoso.com | ?{$_.HealthSetName -eq "OWA.Proxy"}
```

這次他發現問題已解決。

```Powershell
    Server          State           Name                 TargetResource       HealthSetName   AlertValue ServerComp
                                                                                                         onent
    ------          -----           ----                 --------------       -------------   ---------- ----------
    Server1         Online          OWAProxyTestMonitor  MSExchangeOWAAppPool OWA.Proxy       Healthy    OwaProxy
    Server1         Online          OWAProxyTestMonitor  MSExchangeOWACale... OWA.Proxy       Healthy    OwaProxy
```

他回到 SCOM 主控台，並確認問題已解決。

![伺服器健康狀況](images/Dn195908.c863be83-fc4b-4daf-a18b-27b1aae15b1d(EXCHG.150).png "伺服器健康狀況")

以上的案例簡單說明了您在 SCOM 主控台中發現警示時所應執行的疑難排解工作流程。儘管細節會有差異，但對於主控台中回報的每個問題，大致上都可依循類似的疑難排解工作流程來解決。

