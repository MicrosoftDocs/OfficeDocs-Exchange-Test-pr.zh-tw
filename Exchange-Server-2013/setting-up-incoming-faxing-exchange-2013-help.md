---
title: '設定傳入傳真: Exchange Online Help'
TOCTitle: 設定傳入傳真
ms:assetid: 5d3cae58-1690-424d-9bef-011911d0b608
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee633468(v=EXCHG.150)
ms:contentKeyID: 52062333
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定傳入傳真

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2016-12-09_

MicrosoftExchange 整合通訊 (UM) 依賴認證的傳真協力廠商解決方案的增強的傳真功能，例如外寄傳真或傳真路由。根據預設，Exchange 伺服器未設定為允許傳入的傳真傳送給啟用 um 的使用者。而是 Exchange 伺服器會重新導向至認證的傳真協力廠商解決方案的傳入傳真呼叫。傳真協力程式伺服器會接收傳真資料並再傳送給電子郵件中的使用者的信箱與為.tif 附件包含傳真。

如需傳真協力廠商的詳細資訊，請參閱[傳真協力廠商的 Microsoft Pinpoint](https://go.microsoft.com/fwlink/?linkid=190238)

## 部署和設定傳真

UM 轉寄至專用的傳真協力廠商解決方案，然後建立傳真寄件者的傳真呼叫並接收代表已啟用 UM 之使用者的傳真傳入傳真呼叫。不過，若要允許已啟用 UM 的使用者接收傳真訊息中其信箱，必須先啟用傳入傳真並連結到的啟用 UM 之使用者或使用者的 UM 信箱原則上設定傳真協力程式的 URI。您可以允許或防止傳入傳真 UM 撥號對應表 UM 信箱原則，以及已啟用 UM 之使用者的信箱。如需詳細資訊，請參閱下列主題：

  - [允許使用者接收傳真\] 相同的撥號計劃中](allow-users-in-the-same-dial-plan-to-receive-faxes-exchange-2013-help.md)

  - [防止使用者在同一個撥號對應表中接收傳真](prevent-users-in-the-same-dial-plan-from-receiving-faxes-exchange-2013-help.md)

  - [啟用的一組使用者的傳真功能](enable-faxing-for-a-group-of-users-exchange-2013-help.md)

  - [停用的使用者群組傳真](disable-faxing-for-a-group-of-users-exchange-2013-help.md)

  - [讓使用者接收傳真](enable-a-user-to-receive-faxes-exchange-2013-help.md)

  - [防止使用者接收傳真](prevent-a-user-from-receiving-faxes-exchange-2013-help.md)

## 步驟 1： 部署整合通訊

您可以設定您內部部署或混合式傳真前的組織必須已成功部署用戶端存取和信箱伺服器及設定支援的 Voice over IP (VoIP) 閘道允許傳真。如需如何部署 UM，請參閱[部署 Exchange 2013 UM](deploy-exchange-2013-um-exchange-2013-help.md)的詳細資訊。如需如何部署 VoIP 閘道和 IP 專用交換機 (Pbx) 的詳細資訊，請參閱[UM 連接至電話系統](connect-um-to-your-telephone-system-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在整合了整合通訊及 MicrosoftOffice Communications Server 2007 R2 或 Microsoft Lync Server 的環境中，不支援使用 T.38 或 G.711 來傳送及接收傳真。</td>
</tr>
</tbody>
</table>


## 步驟 2： 設定傳真協力程式伺服器

接下來，必須啟用傳入傳真並需要在組織中每個 UM 信箱原則上設定傳真協力程式的 URI。順利部署傳入傳真，您必須與 Exchange 整合通訊整合認證的傳真協力廠商解決方案。如需詳細資訊，請參閱[傳真 advisor Exchange UM](fax-advisor-for-exchange-um-exchange-2013-help.md)。如需認證的傳真協力廠商的清單，請參閱[傳真協力廠商的 Microsoft Pinpoint](https://go.microsoft.com/fwlink/?linkid=190238)

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>因為您組織外部的傳真協力廠商伺服器即防火牆連接埠必須設定為允許 T.38 通訊協定啟用傳真透過 IP 型網路的連接埠。根據預設，T.38 通訊協定使用 TCP 連接埠 6004。它也可以使用使用者資料包通訊協定 (UDP) 連接埠 6044，但這將會定義硬體廠商。防火牆連接埠必須設定為允許使用 TCP 或 UDP 連接埠或連接埠範圍製造商所定義的傳真資料。</td>
</tr>
</tbody>
</table>


## 步驟 3： 啟用傳真在整合通訊

必須正確設定三個元件，使用者才能使用整合通訊接收傳真：

  - UM 撥號對應表

  - UM 信箱原則

  - UM 信箱

傳真可以啟用或停用 UM 撥號對應表 UM 信箱原則，或上個別已啟用 UM 之使用者的信箱。UM 信箱原則可啟用或停用的傳真使用 Exchange 系統管理中心 (EAC) 或 Exchange 管理命令介面。啟用和停用的撥號對應表和個別的已啟用 UM 的使用者需要完成使用 Exchange 管理命令介面。下表顯示可用的選項和 cmdlet 和啟用及停用傳真使用的參數。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>UM 元件</th>
<th>使用 EAC 來啟用/停用？</th>
<th>啟用傳真的命令介面範例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>撥號對應表</p></td>
<td><p>否</p></td>
<td><p><code>Set-UMDialPlan -id MyUMDialPlan -faxenabled $true</code></p></td>
</tr>
<tr class="even">
<td><p>UM 信箱原則</p></td>
<td><p>是</p></td>
<td><p><code>Set-UMMaiboxPolicy -id MyPolicy -AllowFax $true</code></p></td>
</tr>
<tr class="odd">
<td><p>已啟用 UM 的使用者</p></td>
<td><p>否</p></td>
<td><p><code>Set-UMMailbox -id tonysmith -faxenabled $true</code></p></td>
</tr>
</tbody>
</table>


根據預設，雖然 UM 撥號對應表和使用者的信箱允許傳入傳真，但您必須先在指派給已啟用 UM 之使用者的 UM 信箱原則上啟用輸入傳真，然後輸入傳真協力程式伺服器的 URI。

若要讓已啟用 UM 的使用者接收傳真，您必須執行下列作業：

  - 確認每個 UM 撥號對應表可讓使用者相關聯的撥號對應表接收傳真\]。根據預設，所有與撥號對應表相關聯的使用者可以接收傳真\]。已啟用 UM 的使用者接收傳真訊息在他們的信箱中的每個 VoIP 閘道或 IP PBX 必須設定為接受傳入傳真呼叫。您也必須啟用傳真連結與撥號對應表的使用者所收到的郵件。如需如何讓使用者與撥號對應表連結接收傳真或防止執行此動作的詳細資訊，請參閱[讓使用者接收傳真](enable-a-user-to-receive-faxes-exchange-2013-help.md)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您可以防止傳真訊息所接收撥號對應表上，如果沒有與撥號對應表相關聯的使用者將能夠接收傳真]，即使您設定要讓其接收傳真] 的個別使用者的屬性。啟用或停用 UM 撥號對應表上的傳真功能會個別啟用 UM 之使用者的設定優先。</td>
    </tr>
    </tbody>
    </table>


  - 設定已啟用 UM 功能的使用者相關聯的 UM 信箱原則。UM 信箱原則必須設定為允許傳入的傳真，包括傳真協力程式的 URI 及傳真協力程式伺服器的名稱。*FaxServerURI*參數必須使用下列格式： sip: \<*fax server URI*\>: \<*port*\>; \<*transport*\>，其中"傳真伺服器 URI"為完整的網域名稱 (FQDN) 或傳真協力廠商伺服器的 IP 位址。「 連接埠 」 是連接埠接聽傳入傳真呼叫，傳真伺服器和 「 傳輸 」 是用於傳入傳真 （UDP、 TCP 或傳輸層安全性 (TLS)） 的傳輸通訊協定。例如，您可能會設定 UM 信箱原則來接收傳真，如下所示。
    
        Set-UMMailboxPolicy MyUMMailboxPolicy -AllowFax $true -FaxServerURI "sip:faxserver.abc.com:5060;transport=tcp"

  - 如需詳細資訊，請參閱[設定協力廠商傳真伺服器 URI 允許傳真](set-the-partner-fax-server-uri-to-allow-faxing-exchange-2013-help.md)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb125224.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>雖然您可以納入多個項目<em>FaxServerURI</em>的格式以分號隔開，會使用一個項目。此參數可讓使用只有一個項目並新增多個項目不會讓您的負載平衡傳真要求。</td>
    </tr>
    </tbody>
    </table>


  - 確認已啟用 UM 的信箱可以接收傳真訊息。根據預設，所有與撥號對應表相關聯的使用者可以接收傳真\]。但是可能會有情況時因為能夠接收傳真\] 已在其信箱上停用使用者無法接收傳真\]。如需如何啟用已啟用 UM 的使用者接收傳真\] 的詳細資訊，請參閱[讓使用者接收傳真](enable-a-user-to-receive-faxes-exchange-2013-help.md)。
    
    您可以防止有關聯的撥號對應表從接收傳真訊息的個別使用者。若要這樣做，請使用**Set-UMMailbox**指令程式在命令介面中設定使用者的屬性。您也可以使用**Set-UMMailboxPolicy**指令程式來防止多個使用者接收傳真訊息。如需如何防止使用者接收傳真訊息的詳細資訊，請參閱[防止使用者接收傳真](prevent-a-user-from-receiving-faxes-exchange-2013-help.md)。

## 步驟 4： 設定驗證

除了設定您的 UM 撥號對應表、 UM 信箱原則、 和啟用 UM 的使用者，您必須設定您的 Exchange 伺服器和傳真協力廠商伺服器之間的驗證。Exchange 伺服器必須能夠驗證宣告對從傳真協力廠商伺服器傳入訊息的原點而言。聲稱至傳真協力廠商伺服器有來自任何未經過驗證的訊息將不會由 Exchange 伺服器處理。

若要驗證傳真協力程式伺服器至 Exchange 伺服器的連線，您可以使用：

  - Mutual TLS

  - 寄件者識別碼驗證

  - 專用的接收連接器

接收連接器應足夠驗證在組織中部署傳真協力程式伺服器。接收連接器可確保 Exchange 伺服器會將所有以經過驗證進行傳真協力廠商伺服器傳入的流量。

接收連接器是在傳真協力程式伺服器用來提交 SMTP 傳真訊息的 Exchange 伺服器上設定，且必須設定下列值：

  - *AuthMechanism: ExternalAuthoritative*

  - *PermissionGroups: ExchangeServers, PartnersFax*

  - *RemoteIPRanges: {the fax server's IP address}*

  - *RequireTLS: False*

  - *EnableAuthGSSAPI: False*

  - *LiveCredentialEnabled: False*

如需詳細資訊，請參閱[連接器](connectors-exchange-2013-help.md)。

如果傳真協力廠商伺服器會透過公用網路傳送到 Exchange 伺服器的網路流量，例如服務為基礎的傳真協力廠商伺服器雲端，最好是不錯的選項來驗證使用寄件者識別碼檢查傳真協力廠商伺服器。這種驗證類型可確保傳真訊息是來自 IP 位址已授權可代表郵件宣告有來自傳真協力廠商網域傳送的電子郵件。DNS 用來儲存寄件者識別碼記錄 （或寄件者原則架構 (SPF) 記錄） 和傳真協力廠商必須將其 SPF 記錄發佈 DNS 正向對應區域。Exchange 將會由查詢 DNS 驗證的 IP 位址。不過，寄件者識別碼代理程式必須能夠執行的 DNS 查詢的信箱伺服器上執行。

您也可以使用 TLS 來加密網路流量，或在傳真協力程式伺服器與 Exchange 伺服器之間使用 Mutual TLS 進行加密和驗證。

