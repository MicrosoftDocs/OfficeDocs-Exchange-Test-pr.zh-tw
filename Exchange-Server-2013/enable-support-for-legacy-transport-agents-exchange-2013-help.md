---
title: '啟用支援的舊版傳輸代理程式: Exchange 2013 Help'
TOCTitle: 啟用支援的舊版傳輸代理程式
ms:assetid: 00617e87-7199-406e-b4a3-94378f657f1f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ591524(v=EXCHG.150)
ms:contentKeyID: 50472443
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟用支援的舊版傳輸代理程式

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

在 Microsoft Exchange Server 2013，預設支援使用 Microsoft.NET Framework 4.0 版所建立的傳輸代理程式。預設不啟用Exchange 2013支援傳輸代理程式使用舊版的.NET Framework 但支援針對下列舊版傳輸代理程式所建立。若要啟用支援的舊版傳輸代理程式，您需要修改適當的 XML 應用程式設定檔。您要修改的檔案傳輸代理程式安裝位置而定：


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>伺服器</th>
<th>應用程式設定檔案</th>
<th>Microsoft Windows 服務</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Client Access server</p></td>
<td><p>%ExchangeInstallPath%Bin\MSExchangeFrontendTransport.exe.config</p></td>
<td><p>Microsoft Exchange 前端傳輸 (MSExchangeFrontendTransport)</p></td>
</tr>
<tr class="even">
<td><p>信箱伺服器</p></td>
<td><ul>
<li><p>%ExchangeInstallPath%Bin\EdgeTransport.exe.config</p></li>
<li><p>%ExchangeInstallPath%Bin\MSExchangeTransport.exe.config</p></li>
</ul></td>
<td><p>Microsoft Exchange Transport (MSExchangeTransport)</p></td>
</tr>
</tbody>
</table>


支援的舊版傳輸代理程式是由應用程式設定檔中的機碼所控制。根據預設，沒有任何必要的機碼是出現在 \[應用程式設定檔。您必須手動新增機碼。下表說明每個索引鍵的更多詳細資訊。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>按鍵</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>useLegacyV2RuntimeActivationPolicy</em></p></td>
<td><p>此機碼啟用或停用舊版傳輸代理程式的支援。此機碼的有效值為<code>true</code>或<code>false</code>。如果未指定此機碼，則預設值為<code>false</code>。</p></td>
</tr>
<tr class="even">
<td><p><em>supportedRuntime version</em></p></td>
<td><p>此索引鍵可指定代理程式所需的 Microsoft.NET Framework 版本。此機碼的有效值如下：</p>
<ul>
<li><p><code>v4.0</code>或<code>v4.0.30319</code></p></li>
<li><p><code>v3.5</code>或<code>v3.5.21022</code></p></li>
<li><p><code>v3.0</code>或<code>v3.0.4506</code></p></li>
<li><p><code>v2.0</code>或<code>v2.0.50727</code></p></li>
</ul>
<p>您使用多個不同的 <em>supportedRuntime version</em> 金鑰執行個體來指定多個值。</p>
<p>當您使用 <em>useLegacyV2RuntimeActivationPolicy</em> 金鑰啟用舊版傳輸代理程式支援時，除了舊版傳輸代理程式所需的值外，應永遠指定 <code>v4.0</code> 值。</p></td>
</tr>
</tbody>
</table>


## 開始之前有哪些須知？

  - 預估完成時間：15 分鐘

  - Exchange 權限無法套用於此主題的程序。在 Exchange 伺服器的作業系統中執行這些程序。

  - 您儲存至應用程式設定檔案的變更將在重新開啟對應服務後套用。

  - 當您重新開啟任何與應用程式設定檔案關聯的服務，伺服器的郵件流程將暫時中斷。

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


## 使用命令提示字元來設定舊版傳輸代理程式支援

使用以下程序來啟用舊版傳輸代理的支援：

1.  在命令提示字元視窗中，在要設定舊版傳輸代理程式支援的 Exchange 2013 伺服器上，執行下列命令來開啟記事本中的適當應用程式：
    
        Notepad %ExchangeInstallPath%Bin\<AppConfigFile>
    
    例如，若要開啟信箱伺服器的 EdgeTransport.exe.config，請執行下列命令：
    
        Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config

2.  在檔案末端找到 *\</configuration\>* 金鑰，並將下列金鑰貼在 *\</configuration\>* 金鑰之前：
    
        <startup useLegacyV2RuntimeActivationPolicy="true">
           <supportedRuntime version="v4.0" />
           <supportedRuntime version="v3.5" />
           <supportedRuntime version="v3.0" />
           <supportedRuntime version="v2.0" />
        </startup>

3.  完成後，儲存並關閉應用程式設定檔案。

4.  重複步驟 1 到 3，修改其他應用程式設定檔案。

5.  執行下列命令，重新開始關聯的 Windows 服務：
    
        net stop <service> && net start <service>
    
    例如，若要修改 EdgeTransport.exe.config 檔案，必須執行下列命令來重新開啟 Microsoft Exchange 傳輸服務：
    
        net stop MSExchangeTransport && net start MSExchangeTransport

6.  重複步驟 5 來重新開啟與其他修改的應用程式設定檔案關聯的服務。

## 如何才能了解這是否正常運作？

您會知道此程序的運作是否舊版傳輸代理程式安裝成功。如果您嘗試安裝舊版的傳輸代理程式沒有執行本主題中的程序，您會收到類似下列的錯誤：

    Mixed mode assembly is built against version '<version>' of the runtime and cannot be loaded in the 4.0 runtime without additional configuration information.

