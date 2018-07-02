---
title: 疑難排解 OWA。Protocol.Dep 健全設定
TOCTitle: 疑難排解 OWA。Protocol.Dep 健全設定
ms:assetid: f39c63d5-f161-4eee-9415-05f3355e7cc7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.scom.owa.protocol.dep(v=EXCHG.150)
ms:contentKeyID: 54652653
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 疑難排解 OWA。Protocol.Dep 健全設定

 

_**適用版本：** Exchange Server 2013, Project Server 2013_

_**上次修改主題的時間：** 2016-12-09_

**OWA.Protocol.DEP**健全設定監視立即訊息 (IM) 服務中Outlook Web AppLync 2013和Exchange 2013之間整合的整體的狀況。如需啟用立即訊息中Outlook Web App的詳細資訊，請參閱 ＜[整合 Microsoft Lync Server 2013 與 Microsoft Outlook Web App 2013](https://go.microsoft.com/fwlink/p/?linkid=280418)。

若您收到警示，指出**OWA.Protocol.DEP**健全設定的狀況不良，表示可能會防止立即訊息中Outlook Web App正常運作的問題。

## 說明

**OWA.Protocol.DEP**服務是使用下列探查與監視器來監視。


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
<td><p>OWA.Protocol.DEP</p></td>
<td><p>OwaIMInitializationFailedMonitor</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>OWA.Protocol.DEP</p></td>
<td><p>WacDiscoveryFailureEventMonitor</p></td>
</tr>
</tbody>
</table>


如需探查與監視器的詳細資訊，請參閱[伺服器健康狀況與效能](https://technet.microsoft.com/zh-tw/library/jj150551\(v=exchg.150\))。

## 使用者動作

有可能服務復原之後則發出警示。因此，當您收到警示指定**OWA.Protocol.DEP**健全設定的狀況不良，先確認問題仍然存在。如果問題不存在，執行下列各節所述的適當的復原動作。

## 復原動作的錯誤： 「 InstantMessageOCSProvider.InitializeEndpointManager。沒有登錄設定 IM 提供者。 」

此錯誤指出所需的登錄機碼是遺漏的 Mailbox server 上。此登錄機碼在伺服器上安裝 Microsoft Unified Communications Managed API (UCMA) 4.0 時應該已設定。遺失的登錄機碼是：

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\MSExchange OWA\InstantMessaging

此機碼應該包含指向`Microsoft.Rtc.Internal.Ucweb` DLL **ImplementationDLLPath**字串。預設位置為`C:\Program Files\Microsoft UCMA 4.0\Runtime\SSP\Microsoft.Rtc.Internal.Ucweb.dll`。

若要修正此問題，重新安裝 UCMA 4.0 或手動建立登錄機碼。您可以下載 UCMA 4.0 這裡： [Unified Communications Managed API 4.0 Runtime](https://go.microsoft.com/fwlink/p/?linkid=260990)。

## 復原動作的錯誤： 「 InstantMessageOCSProvider.InitializeEndpointManager。IM 提供者找不到。 」

此錯誤指出`Microsoft.Rtc.Internal.Ucweb` DLL 檔案已遺失的 Mailbox server 上。此檔案在伺服器上已安裝的 UCMA 4.0 時應該已安裝。預設位置是`C:\Program Files\Microsoft UCMA 4.0\Runtime\SSP`。

若要修正此問題，重新安裝 UCMA 4.0。如需詳細資訊，請參閱[Unified Communications Managed API 4.0 Runtime](https://go.microsoft.com/fwlink/p/?linkid=260990)。

## 復原動作的錯誤： 「 立即訊息伺服器名稱設為 null 或空在 web.config。"

此錯誤表示Lync 2013伺服器不是檔案中定義Outlook Web App應用程式設定 (web.config) Mailbox server 上。此`web.config`檔案位於`%ExchangeInstallPath%ClientAccess\Owa`，且包含名為**IMServerName**指定Lync 2013伺服器的 FQDN 的機碼。若要修正此問題，請遵循下列步驟：

1.  在命令提示字元視窗中開啟Outlook Web App web.config 檔案在 \[記事本\] 中執行下列命令：
    
        Notepad %ExchangeInstallPath%ClientAccess\Owa\web.config

2.  搜尋名為**IMServerName**機碼。如果找到，確認Lync 2013伺服器的 FQDN。如果找不到金鑰，請執行下列步驟，以新增。
    
    1.  尋找名為**\<appSettings\>**標記。
    
    2.  在 \[ **\<appSettings\>** \] 節點中新增下列行：
        
            <add key="IMServerName" value="Lync Server FQDN" />
        
        例如：
        
            <add key="IMServerName" value="lync01.contoso.com" />
    
    3.  若要套用Outlook Web App中的變更，請執行下列命令：
        
            %windir%\system32\inetsrv\appcmd.exe recycle apppool /apppool.name:"MSExchangeOWAAppPool"

## 復原動作的錯誤： 「 立即通訊憑證指紋是 null 或空 web.config 上 」。

此錯誤指出整合Lync 2013與Outlook Web App所使用的憑證不是檔案中定義Outlook Web App應用程式設定 (web.config) 的信箱伺服器上。此`web.config`檔案位於`%ExchangeInstallPath%ClientAccess\Owa`，且包含名為**IMCertificateThumbprint**指定憑證的指紋 （雜湊） 金鑰。

您可以使用**Get-ExchangeCertificate**指令程式或**伺服器**在 Exchange 系統管理中心 (EAC) 中取得的憑證指紋值 \>**憑證**。

若要修正此問題，請遵循下列步驟：

1.  在命令提示字元視窗中開啟Outlook Web App web.config 檔案在 \[記事本\] 中執行下列命令：
    
        Notepad %ExchangeInstallPath%ClientAccess\Owa\web.config

2.  搜尋名為**IMCertificateThumbprint**機碼。如果找到，驗證憑證指紋值是否正確。如果找不到金鑰，請將其新增藉由執行下列步驟：
    
    1.  尋找名為**\<appSection\>**的標籤。
    
    2.  在 \[ **\<appSection\>** \] 節點中新增下列行：
        
            <add key="IMCertificateThumbprint" value="thumbprint"/>
        
        例如：
        
            <add key="IMCertificateThumbprint" value="35CB4C441D55506C88E59B7946B567A4F45B3B5C" />
    
    3.  若要套用Outlook Web App的變更，請執行下列命令：
        
            %windir%\system32\inetsrv\appcmd.exe recycle apppool /apppool.name:"MSExchangeOWAAppPool"

## 復原動作的錯誤： 「 IM 憑證指紋為 \< 值 \> 找不。 」

此錯誤指出信箱伺服器上找不到整合Lync 2013和Outlook Web App所使用的憑證。此憑證必須安裝在 Mailbox server 和Lync 2013伺服器上，而且必須由兩部伺服器信任。如需憑證需求的詳細資訊，請參閱 Outlook Web App\] 區段中的[整合 Microsoft Lync Server 2013 與 Microsoft Outlook Web App 2013](https://go.microsoft.com/fwlink/p/?linkid=280418)上啟用立即訊息。

您可以比對他錯誤的憑證指紋值使用**Get-ExchangeCertificate**指令程式或**伺服器**在 Exchange 系統管理中心 (EAC) 中 \>**憑證**。

## 復原動作的錯誤： 「 IM 憑證已過期 」。

此錯誤指出用來整合Lync 2013和Outlook Web App的憑證已過期。若要解決此錯誤，您需要更新的憑證。

您可以比對他錯誤的憑證指紋值使用**Get-ExchangeCertificate**指令程式或**伺服器**在 Exchange 系統管理中心 (EAC) 中 \>**憑證**。

## 復原動作的錯誤： 「 IM 憑證具有不會成為有效尚未。 」

此錯誤指出用來整合Lync 2013的憑證而Outlook Web App有無效的日期。若要解決此錯誤，您必須設定新的憑證，並需要新增新的憑證指紋值中`%ExchangeInstallPath%ClientAccess\Owa\web.config`**IMCertificateThumbprint**機碼。如需憑證需求的詳細資訊，請參閱在 Outlook Web App\] 區段中的[整合 Microsoft Lync Server 2013 與 Microsoft Outlook Web App 2013](https://go.microsoft.com/fwlink/p/?linkid=280418)啟用立即訊息。

## 復原動作的錯誤： 「 IM 憑證沒有私密金鑰。 」

此錯誤指出用來整合Lync 2013和Outlook Web App的憑證沒有私密金鑰。要解決此錯誤，您必須設定新的憑證已私密金鑰\]，並需要在`%ExchangeInstallPath%ClientAccess\Owa\web.config`**IMCertificateThumbprint**機碼中新增新的憑證指紋值。如需憑證需求詳細資訊，請參閱在 Outlook Web App\] 區段中[整合 Microsoft Lync Server 2013 與 Microsoft Outlook Web App 2013](https://go.microsoft.com/fwlink/p/?linkid=280418)啟用立即訊息。

