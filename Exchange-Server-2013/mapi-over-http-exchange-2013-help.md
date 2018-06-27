---
title: 'MAPI over HTTP: Exchange 2013 Help'
TOCTitle: MAPI over HTTP
ms:assetid: 4663b5db-5b30-4a5a-a302-be6fef7fe5da
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn635177(v=EXCHG.150)
ms:contentKeyID: 61204226
ms.date: 01/01/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# MAPI over HTTP

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2017-05-10_

Messaging Application Programming Interface (MAPI) over HTTP 是 MicrosoftExchange Server 2013 Service Pack 1 (SP1) 所實作的新式傳輸通訊協定。MAPI over HTTP 將傳輸層提升為符合業界標準的 HTTP 模型，因而改善了 Outlook 和 Exchange 連線的可靠性與穩定性。這可更清楚地檢視傳輸錯誤，並可增強復原能力。此外，也具有支援明確暫停和繼續功能的能力。這讓受支援的用戶端能夠變更網路或從休眠狀態恢復，同時保有相同的伺服器內容。

實作 MAPI over HTTP，並不表示這是唯一可供 Outlook 用來存取 Exchange 的通訊協定。不具 MAPI over HTTP 功能的 Outlook 用戶端，仍可使用 Outlook Anywhere (RPC over HTTP)，透過擁有 MAPI 功能的 Client Access Server 來存取 Exchange。

## MAPI over HTTP 的優點

MAPI over HTTP 可為支援它的用戶端提供下列優點：

  - 採用以 HTTP 為基礎的通訊協定，可支應未來在驗證方面的創新能力。

  - 縮短通訊中斷後所需的重新連線時間，因為只需重新建立 TCP 連線即可，而不需要 RPC 連線。通訊中斷的範例包括：
    
      - 裝置休眠
    
      - 從有線網路變更為無線或行動數據網路

  - 提供無需依賴連線的工作階段內容。伺服器可在設定的時段內保有工作階段內容，即便使用者變更網路亦然。

## 部署 MAPI over HTTP

請考量下列啟用 MAPI over HTTP 的需求。

  - **支援能力**   確認您預定使用的組態版本受到支援。

  - **必要條件**   確認您的環境已升級，並已做好使用 MAPI over HTTP 的準備。

  - **組態**   設定虛擬目錄，並為您的組織啟用 MAPI。

## 支援能力

請使用下列矩陣，確認您的用戶端與伺服器皆支援 MAPI over HTTP。


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>產品</th>
<th>Exchange 2013 SP1</th>
<th>Exchange 2013 RTM</th>
<th>Exchange 2010 SP3</th>
<th>Exchange 2007 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2013 SP1</p></td>
<td><ul>
<li><p>MAPI over HTTP</p></li>
<li><p>Outlook 無所不在</p></li>
</ul></td>
<td><p>Outlook 無所不在</p></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook 無所不在</p></li>
</ul></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook 無所不在</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Outlook 2013 RTM</p></td>
<td><p>Outlook 無所不在</p></td>
<td><p>Outlook 無所不在</p></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook 無所不在</p></li>
</ul></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook 無所不在</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Outlook 2010 SP2 與更新 KB2956191 和 KB2965295 (2015 年 4 月 14 日)</p></td>
<td><ul>
<li><p>MAPI over HTTP<span></span></p></li>
<li><p>Outlook 無所不在</p></li>
</ul></td>
<td><p>Outlook 無所不在</p></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook 無所不在</p></li>
</ul></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook 無所不在</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Outlook 2010 SP2 及更早版本</p></td>
<td><p>Outlook 無所不在</p></td>
<td><p>Outlook 無所不在</p></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook 無所不在</p></li>
</ul></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook 無所不在</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Outlook 2007</p></td>
<td><p>Outlook 無所不在</p></td>
<td><p>Outlook 無所不在</p></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook 無所不在</p></li>
</ul></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook 無所不在</p></li>
</ul></td>
</tr>
</tbody>
</table>


## 必要條件

完成下列步驟，為用戶端和伺服器完成支援 MAPI over HTTP 的準備工作。

1.  將 Outlook 用戶端升級至 Outlook 2013 SP1 或 Outlook 2010 SP2，以及更新 KB2956191 和 KB2965295 (2015 年 4 月 14 日).

2.  將 Client Access Server 和信箱伺服器升級至 Exchange 2013 SP1。如需如何升級的相關資訊，請參閱[將 Exchange 2013 升級至最新的累計或服務套件](upgrade-exchange-2013-to-the-latest-cumulative-update-or-service-pack-exchange-2013-help.md)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>所有 Client Access Server 都必須升級至 Exchange 2013 SP1，才能啟用 MAPI over HTTP。否則，Outlook 將無法連接到信箱。<br />
    若未能升級資料庫可用性群組 (DAG) 中的所有信箱伺服器，可能會導致電子郵件延遲，並致使用戶端在資料庫進行容錯移轉時必須重新啟動 Outlook。</td>
    </tr>
    </tbody>
    </table>


3.  在所有 Exchange 2013 伺服器上，您必須安裝 Microsoft.NET Framework 4.5.2。如需詳細資訊，請參閱 [安裝 .NET Framework 4.5](https://go.microsoft.com/fwlink/p/?linkid=518380)。

4.  在所有 Exchange 2013 SP1 Client Access Server 上，執行下列步驟來新增 **COMPLUS\_DisableRetStructPinning** Windows 環境變數。
    
    1.  在命令提示字元視窗中，執行 `systempropertiesadvanced` 並按一下 **\[環境變數\]**。
    
    2.  在 **\[系統變數\]** 區段中，按一下 **\[新增\]**，並輸入下列資訊。
        
          - **變數名稱**   `COMPLUS_DisableRetStructPinning`
        
          - **變數值**   1
    
    3.  完成後，請按一下 **\[確定\]**。

## 組態

完成下列步驟，為您的組織設定 MAPI over HTTP。

1.  **虛擬目錄組態**   根據預設，Exchange 2013 SP1 會為 MAPI over HTTP 建立一個虛擬目錄。您可以使用 **Set-MapiVirtualDirectory** 指令程式來設定虛擬目錄。您必須設定內部 URL 和 (或) 外部 URL。如需詳細資訊，請參閱[Set-MapiVirtualDirectory](https://technet.microsoft.com/zh-tw/library/dn595082\(v=exchg.150\))。
    
    例如，若要將內部 URL 值設為 https://contoso.com/mapi，並將驗證方法設為 `Negotiate`，以在本機 Exchange 伺服器上設定預設 MAPI 虛擬目錄，請執行下列命令：
    
        Set-MapiVirtualDirectory -Identity "Contoso\mapi (Default Web Site)" -InternalUrl https://Contoso.com/mapi -IISAuthenticationMethods Negotiate

2.  **憑證組態**   您的 Exchange 環境所使用的數位憑證，必須包含與 MAPI 虛擬目錄上的定義相同的 *InternalURL* 和 *ExternalURL* 值。如需 Exchange 2013 憑證管理的相關資訊，請參閱[數位憑證和 SSL](digital-certificates-and-ssl-exchange-2013-help.md)。請確定 Exchange 憑證在 Outlook 用戶端工作站上受到信任，而且沒有任何憑證錯誤，尤其是在您存取 MAPI 虛擬目錄上設定的 URL 時。

3.  **更新伺服器規則**   確認您的負載平衡器、反向 Proxy 和防火牆均已適當設定，而允許存取 MAPI over HTTP 虛擬目錄。

4.  **在您的 Exchange 組織中啟用 MAPI over HTTP**
    
    執行下列命令：
    
        Set-OrganizationConfig -MapiHttpEnabled $true

## 測試 MAPI over HTTP 連線

您可以使用 **Test-OutlookConnectivity** 指令程式來測試端對端的 MAPI over HTTP 連線。若要使用 **Test-OutlookConnectivity** 指令程式，必須要啟動 Microsoft Exchange Health Manager (MSExchangeHM) 服務。

下列範例將測試從 Exchange 伺服器 ContosoMail 連出的 MAPI over HTTP 連線。

    Test-OutlookConnectivity -RunFromServerId ContosoMail -ProbeIdentity OutlookMapiHttpSelfTestProbe

成功的測試會傳回類似下列範例的輸出：

    MonitorIdentity                                          StartTime              EndTime                Result      Error     Exception
    ---------------                                          ---------              -------                ------      -----     ---------
    OutlookMapiHttp.Protocol\OutlookMapiHttpSelfTestProbe    2/14/2014 7:15:00 AM   2/14/2014 7:15:10 AM   Succeeded

如需詳細資訊，請參閱[Test-OutlookConnectivity](https://technet.microsoft.com/zh-tw/library/dd638082\(v=exchg.150\))。

MAPI over HTTP 活動的記錄位於下列位置：

  - %ExchangeInstallPath%Logging\\MAPI Address Book Service\\

  - %ExchangeInstallPath%Logging\\MAPI Client Access\\

  - %ExchangeInstallPath%Logging\\HttpProxy\\Mapi\\

## 管理 MAPI over HTTP

您可以使用下列指令程式來管理 MAPI over HTTP 的組態：

  - [Set-MapiVirtualDirectory](https://technet.microsoft.com/zh-tw/library/dn595082\(v=exchg.150\))

  - [Get-MapiVirtualDirectory](https://technet.microsoft.com/zh-tw/library/dn595080\(v=exchg.150\))

  - [New-MapiVirtualDirectory](https://technet.microsoft.com/zh-tw/library/dn595081\(v=exchg.150\))

  - [Remove-MapiVirtualDirectory](https://technet.microsoft.com/zh-tw/library/dn595083\(v=exchg.150\))

