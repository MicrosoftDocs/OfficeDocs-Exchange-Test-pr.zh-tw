---
title: '設定用戶端特定的郵件大小限制: Exchange 2013 Help'
TOCTitle: 設定用戶端特定的郵件大小限制
ms:assetid: fef9ca78-b68f-4342-ada0-881ab985ce3c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Hh529949(v=EXCHG.150)
ms:contentKeyID: 52062613
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定用戶端特定的郵件大小限制

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2017-01-26_

Microsoft Exchange Server 2013 對於通過您 Exchange 組織的郵件設有數種不同的適用郵件大小限制。如需詳細資訊，請參閱 [郵件大小限制](message-size-limits-exchange-2013-help.md)。

但有您可以設定為使用ActiveSync或Exchange Web 服務 (EWS) 的Outlook Web App和電子郵件用戶端的用戶端特定的郵件大小限制。如果您變更 Exchange 全組織的郵件大小限制，您需要驗證郵件大小限制Outlook Web App、 ActiveSync、 及 Exchange Web 服務已設定無誤。您在 Client Access server 和 Mailbox server 上的 web.config 檔案中設定這些值。下表說明這些限制。

### ActiveSync

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>伺服器角色</th>
<th>組態檔</th>
<th>機碼與預設值</th>
<th>大小</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Client Access</p></td>
<td><p><code>%ExchangeInstallPath%FrontEnd\HttpProxy\Sync\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;30000000 bytes&quot;</code>  預設不存在 （請參閱註解）。</p></td>
<td><p>位元組</p></td>
</tr>
<tr class="even">
<td><p>Client Access</p></td>
<td><p><code>%ExchangeInstallPath%FrontEnd\HttpProxy\Sync\web.config</code></p></td>
<td><p><code>maxRequestLength=&quot;10240&quot;</code></p></td>
<td><p>kb</p></td>
</tr>
<tr class="odd">
<td><p>Mailbox</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Sync\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;30000000 bytes&quot;</code>  預設不存在 （請參閱註解）。</p></td>
<td><p>位元組</p></td>
</tr>
<tr class="even">
<td><p>Mailbox</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Sync\web.config</code></p></td>
<td><p><code>maxRequestLength=&quot;10240&quot;</code></p></td>
<td><p>kb</p></td>
</tr>
<tr class="odd">
<td><p>Mailbox</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Sync\web.config</code></p></td>
<td><p><code>&lt;add key=&quot;MaxDocumentDataSize&quot; value=&quot;10240000&quot;&gt;</code></p></td>
<td><p>位元組</p></td>
</tr>
</tbody>
</table>


**ActiveSync限制的註解**

根據預設，沒有*maxAllowedContentLength*機碼中有ActiveSync`web.config`檔案。不過，郵件大小上限為ActiveSync受到**maxAllowedContentLength**值所套用之伺服器上的所有網站。預設值為 30000000 個位元組 (30 MB)。若要查看ActiveSync這些值在 Client Access Server 和 Mailbox server 在 IIS 管理員中，執行下列步驟：

1.  請執行下列步驟之一：
    
      - 用戶端存取伺服器上開啟**IIS 管理員中**，瀏覽至**網站**\>**預設的網站**並選取 \[ **Microsoft Server ActiveSync**。
    
      - 在信箱伺服器上開啟**IIS 管理員中**，瀏覽至**網站**\> **Exchange Back End**和選取 \[ **Microsoft Server ActiveSync**。

2.  確認**功能檢視**已選取，然後按兩下 \[**設定編輯器**的 \[**管理**\] 區段。

3.  按一下 \[**區段**\] 欄位中的下拉式箭號、 瀏覽至 \[ **system.webServer** \>**安全性**與 select **requestFiltering**。

4.  結果中，展開**requestLimits**，而且您會看到**maxAllowedContentLength**和預設值 30000000 （位元組）。

若要變更**maxAllowedContentLength**值，以位元組為單位，輸入新值並按一下 \[**套用\]**。您需要變更 Client Access server 和 Mailbox server 上的值。在 IIS 管理員中將值變更後，新*maxAllowedContentLength*金鑰會寫入相對應的`web.config`檔 (在用戶端存取伺服器上的`%ExchangeInstallPath%FrontEnd\HttpProxy\Sync\web.config` ) 和`%ExchangeInstallPath%ClientAccess\Sync\web.config` Mailbox server 上。

若要變更ActiveSync用戶端的郵件大小上限，您需要變更的 Client Access server 和 Mailbox server 上`web.config`檔案中的*maxRequestLength* 、 *MaxDocumentDataSize*在 Mailbox server 上的`web.config`檔案和*maxAllowedContentLength*在 IIS 管理員中 Client Access server 和 Mailbox server 上的值。

### Exchange Web 服務

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>服務角色</th>
<th>組態檔</th>
<th>機碼與預設值</th>
<th>大小</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Client Access</p></td>
<td><p><code>%ExchangeInstallPath%FrontEnd\HttpProxy\ews\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;67108864&quot;</code></p></td>
<td><p>位元組</p></td>
</tr>
<tr class="even">
<td><p>Mailbox</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\exchweb\ews\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;67108864&quot;</code></p></td>
<td><p>位元組</p></td>
</tr>
<tr class="odd">
<td><p>Mailbox</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\exchweb\ews\web.config</code></p></td>
<td><p><code>maxReceivedMessageSize=&quot;67108864&quot;</code> 14 執行個體</p></td>
<td><p>位元組</p></td>
</tr>
</tbody>
</table>


**Exchange Web 服務限制的註解**

  - 有 14 不同的執行個體值`maxReceivedMessageSize="67108864"`會對應至不同的組合 （http 和 https） 的繫結和驗證方法。

  - 若要變更 Exchange Web 服務用戶端的郵件大小上限，您需要變更*maxAllowedContentLength*`web.config`檔案及所有 14 `maxReceivedMessageSize="67108864"`在信箱伺服器上的`web.config`檔案中的執行個體中的值。

  - 在信箱伺服器上的`web.config`檔案，也有兩個值`maxReceivedMessageSize="1048576"`您不需要修改的**UMLegacyMessageEncoderSoap11Element**繫結的執行個體。

  - *maxRequestLength*是出現在這兩個 web.config 檔案，但不是會使用 Exchange Web 服務，因此您不需要修改它的 ASP.NET 設定。

### Outlook Web App

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>伺服器角色</th>
<th>組態檔</th>
<th>機碼與預設值</th>
<th>大小</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Client Access</p></td>
<td><p><code>%ExchangeInstallPath%FrontEnd\HttpProxy\owa\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;35000000&quot;</code></p></td>
<td><p>位元組</p></td>
</tr>
<tr class="even">
<td><p>Client Access</p></td>
<td><p><code>%ExchangeInstallPath%FrontEnd\HttpProxy\owa\web.config</code></p></td>
<td><p><code>maxRequestLength=&quot;35000&quot;</code></p></td>
<td><p>kb</p></td>
</tr>
<tr class="odd">
<td><p>Mailbox</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Owa\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;35000000&quot;</code></p></td>
<td><p>位元組</p></td>
</tr>
<tr class="even">
<td><p>Mailbox</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Owa\web.config</code></p></td>
<td><p><code>maxRequestLength=&quot;35000&quot;</code></p></td>
<td><p>kb</p></td>
</tr>
<tr class="odd">
<td><p>Mailbox</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Owa\web.config</code></p></td>
<td><p><code>maxReceivedMessageSize=&quot;35000000&quot;</code> 2 執行個體</p></td>
<td><p>位元組</p></td>
</tr>
<tr class="even">
<td><p>Mailbox</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Owa\web.config</code></p></td>
<td><p><code>maxStringContentLength=&quot;35000000&quot;</code> 2 執行個體</p></td>
<td><p>位元組</p></td>
</tr>
</tbody>
</table>


**在Outlook Web App限制的註解**

  - 在信箱伺服器上的`web.config`檔案，有兩種不同的執行個體的值`maxReceivedMessageSize="35000000"`和`maxStringContentLength="35000000"`會對應至 http 和 https 繫結。

  - 若要變更Outlook Web App用戶端的郵件大小上限，您需要在信箱伺服器上的`web.config`檔案中包含這兩個執行個體*maxReceivedMessageSize*和*maxStringContentLength*這兩個檔案，這些值的所有變更。

  - 在信箱伺服器上的`web.config`檔案，還有值`maxStringContentLength="102400"`您不需要修改**MsOnlineShellService**繫結的執行個體。

針對所有郵件大小限制，您必須設定需要強制大於實際大小的值。針對郵件附件以及其他任何採用 Base64 編碼的二進位資料，增加這些值必然會導致郵件大小增加。Base64 編碼會使郵件大小增加約 33%，因此您所指定的任何郵件大小限制值皆會較實際可用郵件大小增加 33%。例如，若您指定的郵件大小上限值為 64 MB，則實際的郵件大小上限值約為 48 MB。

## 開始之前有哪些須知？

  - 預估完成時間：15 分鐘

  - Exchange 權限無法套用於此主題的程序。在 Exchange 伺服器的作業系統中執行這些程序。

  - 您儲存至 Web.config 組態檔的變更將在重新啟動 IIS 後套用。

  - 為了支援因採用 Base64 編碼而增加 33% 的大小，請將需要的新大小上限值 (單位為 MB) 乘以 4/3。將值轉換為 KB (乘以 1024)。將值轉換為位元組 (乘以 1048756 (1024\*1024))。請注意，採用 Base64 編碼可能導致大小增加 33%，且會根據數種因素而定，例如附件檔案大小、類型、壓縮，以及用於撰寫和傳送郵件的電子郵件用戶端等等。

  - 在您安裝 Exchange 累計更新 (CU) 後，將會覆寫您在 Exchange XML 應用程式組態檔 (例如 Client Access Server 上的 web.config 檔案，或 Mailbox Server 上的 EdgeTransport.exe.config 檔案) 中任何自訂的個別伺服器設定。請務必儲存此資訊，以便安裝後能輕易地重新設定伺服器。在安裝 Exchange CU 後，您必須重新配置這些設定。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 使用 \[記事本\] 來設定用戶端特定的郵件大小限制

1.  在 \[記事本\] 開啟適當的 web.config 檔案。例如，若要開啟Exchange Web 服務用戶端的 web.config 檔案，執行下列命令：
    
        Notepad %ExchangeInstallPath%ClientAccess\exchweb\ews\web.config
        Notepad %ExchangeInstallPath%FrontEnd\HttpProxy\ews\web.config

2.  在先前主題中的表格中所述的適當的 web.config 檔案中尋找相關的機碼。例如Exchange Web 服務用戶端*maxAllowedContentLength*機碼中的檔案及所有 14 執行個體值`maxReceivedMessageSize="67108864"`檔中找到`web.config` Mailbox server 上。
    
        <requestLimits maxAllowedContentLength="67108864" />
        ...maxReceivedMessageSize="67108864"...
    
    例如，若要允許的 Base64 編碼郵件大小上限約為 64 MB，請將 `67108864` 的所有執行個體變更為 `89478486` (64\*4/3\*1048756)：
    
        <requestLimits maxAllowedContentLength="89478486" />
        ...maxReceivedMessageSize="89478486"...

3.  完成時，儲存並關閉 web.config 檔案。

4.  執行下列命令以重新啟動 IIS：
    
        IISReset /noforce

## 設定從命令列的特定用戶端的郵件大小限制

您也可以設定從命令列的特定用戶端的郵件大小限制而不是使用 \[記事本\]。開啟已提升權限的命令提示字元處Exchange伺服器 （您可以選取 \[**執行系統管理員身分**開啟命令提示字元視窗） 並執行的適當命令會針對您想要設定的限制。

**附註：**

  - 在命令中的大小值是預設值，因此您需要對其進行變更。

  - 請注意值是否會以位元組或 kb 為單位。

**ActiveSync**

    %windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/Microsoft-Server-ActiveSync/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:30000000
    %windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/Microsoft-Server-ActiveSync/" -section:system.web/httpRuntime /maxRequestLength:10240
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/Microsoft-Server-ActiveSync/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:30000000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/Microsoft-Server-ActiveSync/" -section:system.web/httpRuntime /maxRequestLength:10240
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/Microsoft-Server-ActiveSync/" -section:appSettings /[key='MaxDocumentDataSize'].value:10240000

**Exchange Web 服務**

    %windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/ews/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSAnonymousHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSAnonymousHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSBasicHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSBasicHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSNegotiateHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSNegotiateHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecurityHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecurityHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecuritySymmetricKeyHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecuritySymmetricKeyHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecurityX509CertHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecurityX509CertHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /webHttpBinding.[name='EWSStreamingNegotiateHttpsBinding'].maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /webHttpBinding.[name='EWSStreamingNegotiateHttpBinding'].maxReceivedMessageSize:67108864

**Outlook Web App**

    %windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/owa/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:35000000
    %windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/owa/" -section:system.web/httpRuntime /maxRequestLength:35000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:35000000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.web/httpRuntime /maxRequestLength:35000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.serviceModel/bindings /webHttpBinding.[name='httpsBinding'].maxReceivedMessageSize:35000000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.serviceModel/bindings /webHttpBinding.[name='httpBinding'].maxReceivedMessageSize:35000000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.serviceModel/bindings /webHttpBinding.[name='httpsBinding'].readerQuotas.maxStringContentLength:35000000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.serviceModel/bindings /webHttpBinding.[name='httpBinding'].readerQuotas.maxStringContentLength:35000000

## 如何知道這是否正常運作？

若要確認您已成功設定用戶端特定的郵件大小限制，您需要傳送測試郵件到與受影響的用戶端存取信箱。您可以嘗試幾個較小的附件或一個大型附件，因此測試郵件都大約 33%小於您設定的值。例如，85 MB 的設定的值會導致真實感化的郵件大小上限約為 64 mb。

