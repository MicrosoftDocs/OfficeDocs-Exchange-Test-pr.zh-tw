---
title: '不使用 EdgeSync 設定 Edge Transport server 到網際網路郵件流程: Exchange 2013 Help'
TOCTitle: 不使用 EdgeSync 設定 Edge Transport server 到網際網路郵件流程
ms:assetid: 6bb98d10-6f12-4b08-a58e-36375f605d65
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb232082(v=EXCHG.150)
ms:contentKeyID: 61180454
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 不使用 EdgeSync 設定 Edge Transport server 到網際網路郵件流程

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2017-01-23_

建議您使用 Edge 訂閱程序，在 Exchange 組織與 Edge Transport Server 之間建立郵件流程。不過，特定情況可能會讓您無法使用 Edge 訂閱程序。將 Edge Transport Server 訂閱至 Exchange 組織。若要手動建立 Exchange 組織與 Edge Transport Server 間的郵件流程，您必須在 Edge Transport Server 上和 Exchange 組織的 Mailbox Server 上，建立並設定傳送連接器及接收連接器。

## 開始之前

  - 完成此工作的預估時間：30 分鐘。

  - [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱「傳送連接器」項目、「傳送連接器 - Edge Transport」項目和「接收連接器 - Edge Transport」項目。

  - 此程序會使用透過傳輸層安全性 (TLS) 的基本驗證，來提供加密及驗證。當您使用透過 TLS 的基本驗證時，接收伺服器必須已安裝 X.509 安全通訊端層 (SSL) 伺服器憑證。接收連接器上設定的網域全名 (FQDN) 值，必須符合 SSL 伺服器憑證上的 FQDN。依預設，接收連接器上 FQDN 的值即為含有接收連接器之伺服器的 FQDN。

  - 您也可以使用以外部方式保護安全的驗證方法。不過，如果您這麼做，Exchange 不會驗證或加密 Edge Transport Server 與 Mailbox Server 間的通訊。建議您只在也使用其他加密方法時，才使用外部保護驗證方法。加密方法可以是網際網路通訊協定安全性 (IPsec) 關聯或虛擬私人網路 (VPN)。

  - Edge Transport Server 通常會有*多重主目錄*。這表示 Edge Transport Server 具有連線至多個網路區段的網路介面卡。每個網路介面卡都具有唯一 IP 組態。連接至外部或公用網路區段的網路介面卡，應設定為使用公用網域名稱系統 (DNS) 伺服器進行名稱解析。這可讓伺服器將 SMTP 網域名稱解析為 MX 資源記錄，並將郵件路由傳送至網際網路。連接至內部或私人網路區段的網路介面卡，應設定為使用周邊網路中的 DNS 伺服器或應有可用的主機檔案。

  - 您需要在 Active Directory 中建立使用者帳戶，並將帳戶新增到 Exchange Server 電腦上的萬用安全性群組。Edge Transport Server 上的傳送連接器會使用這個帳戶，來驗證 Exchange 組織中的目的地 Mailbox Server。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>這個帳戶會獲授與與執行 Exchange Server 的電腦相關的權限。請務必保護帳戶認證，以預防不當使用此帳戶。您可以設定帳戶為僅允許登入特定的電腦。</td>
    </tr>
    </tbody>
    </table>


## Edge Transport Server 程序

Edge Transport Server 上必須要有下列連接器：

  - 設定將郵件傳送至網際網路的傳送連接器

  - 設定將郵件傳送至 Exchange 組織中 Mailbox Server 的傳送連接器

  - 設定只從 Exchange 組織之 Mailbox Server 接收郵件的接收連接器

  - 設定只接受來自網際網路之郵件的接收連接器

依預設，會在 Edge Transport server role 安裝期間建立一個接收連接器。此連接器可用於內送的網際網路郵件，以及來自 Mailbox Server 的內送郵件。一般來說，Edge 訂閱程序會在預設的接收連接器上自動設定正確的權限及驗證。若您未使用 Edge 訂閱程序，則建議您修改 Edge Transport Server 上的預設接收連接器，以便只接收來自網際網路的郵件。接著您應該在 Edge Transport Server 上建立接收連接器，將其設定為僅接受來自內部 Mailbox Server 的郵件。

以下章節將逐步說明準備讓 Edge Transport Server 與 Exchange 組織進行通訊時所需的所有組態步驟。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您只能使用命令介面，在 Edge Transport Server 上執行這些程序。</td>
</tr>
</tbody>
</table>


## 步驟 1：建立設定為將郵件傳送至網際網路的傳送連接器

這個傳送連接器需要下列設定：

  - **名稱**   To Internet (或任何描述性名稱)

  - **使用類型**   網際網路

  - **位址空間**   "\*" (所有網域)

  - **網路設定**   使用 DNS MX 記錄，自動路由傳送郵件。視您的網路組態而定，您也可以經由智慧主機來路由傳送郵件。智慧主機會接著將郵件路由傳送至網際網路。

若要建立設定為將郵件傳送至網際網路的傳送連接器，請執行下列命令。

    New-SendConnector -Name "To Internet" -AddressSpaces * -Usage Internet -DNSRoutingEnabled $true

如需詳細的語法及參數資訊，請參閱 [New-SendConnector](https://technet.microsoft.com/zh-tw/library/aa998936\(v=exchg.150\))。

## 步驟 2：建立設定為將郵件傳送至 Exchange 組織的傳送連接器

使用 **New-SendConnector** 指令程式可以建立傳送連接器。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>建立傳送連接器之前，必須先執行 <strong>Get-Credential</strong> 命令，將要使用的使用者名稱和密碼儲存在暫存變數中。需要這麼做的原因是，<strong>New-SendConnector</strong> 指令程式將不會接受使用純文字的使用者認證。</td>
</tr>
</tbody>
</table>


這個傳送連接器需要下列設定：

  - **名稱**   To Internal Org (或任何描述性名稱)

  - **使用類型**   內部

  - **位址空間**   Exchange 組織的所有公認網域。例如，\*.contoso.com。

  - 已停用 DNS 路由 (已啟用智慧主機路由)

  - **智慧主機**   一或多個作為智慧主機之 Mailbox Server 的 FQDN。例如，mbxserver01.contoso.com 和 mbxserver02.contoso.com。

  - **智慧主機驗證方法**  透過 TLS 的基本驗證

  - **智慧主機驗證認證**   內部網域中使用者帳戶的認證。您需要先在暫存變數中儲存使用者名稱和密碼，因為 **New-SendConnector** 指令程式將不會接受使用純文字的使用者認證。

若要建立設定為將郵件傳送至 Exchange 組織的傳送連接器，請執行下列命令。

    $MailboxCredentials = Get-Credential
    New-SendConnector -Name "To Internal Org" -Usage Internal -AddressSpaces *.contoso.com -DNSRoutingEnabled $false -SmartHosts mbxserver01.contoso.com,mbxserver02.contoso.com -SmartHostAuthMechanism BasicAuthRequireTLS -AuthenticationCredential $MailboxCredentials

如需詳細的語法及參數資訊，請參閱 [New-SendConnector](https://technet.microsoft.com/zh-tw/library/aa998936\(v=exchg.150\))。

## 步驟 3：修改預設的接收連接器，以便只接受來自網際網路的郵件

您應該對預設的接收連接器進行下列的組態變更：

  - 修改名稱以反映連接器將單獨用於接收來自網際網路的電子郵件。預設接收連接器的名稱是「預設內部接收連接器 \<Edge Transport Server 名稱\>」。

  - 變更網路繫結，以便只接受來自可從網際網路存取之網路介面卡的郵件。例如，10.1.1.1 和標準 SMTP TCP 連接埠值 25。

若要修改預設接收連接器，以便只接受來自網際網路的郵件，請執行下列命令。

    Set-ReceiveConnector "Default internal Receive connector Edge01" -Name "From Internet" -Bindings 10.1.1.1:25

如需詳細的語法及參數資訊，請參閱[Set-ReceiveConnector](https://technet.microsoft.com/zh-tw/library/bb125140\(v=exchg.150\))。

## 步驟 4：建立設定為只接受來自 Exchange 組織之郵件的接收連接器

這個接收連接器需要下列設定：

  - **名稱**   From Internal Org (或任何描述性名稱)

  - **使用類型**   內部

  - **區域網路繫結**   內部網路對向的網路介面卡。例如，10.1.1.2 和標準 SMTP TCP 連接埠值 25。

  - **遠端網路設定**   Exchange 組織中一或多部 Mailbox Server 的 IP 位址。例如，192.168.5.10 和 192.168.5.20。

  - **驗證方法**   TLS、基本驗證、透過 TLS 的基本驗證，以及 Exchange Server 驗證。

若要建立設定為只接受來自 Exchange 組織之郵件的接收連接器，請執行下列命令。

    New-ReceiveConnector -Name "From Internal Org" -Usage Internal -AuthMechanism TLS,BasicAuth,BasicAuthRequireTLS,ExchangeServer -Bindings 10.1.1.2:25 -RemoteIPRanges 192.168.5.10,192.168.5.20

如需詳細的語法及參數資訊，請參閱[New-ReceiveConnector](https://technet.microsoft.com/zh-tw/library/bb125139\(v=exchg.150\))。

## 如何才能了解這些步驟是否正常運作？

若要確認您已順利設定必要的傳送連接器和接收連接器，請在 Edge Transport Server 上執行下列命令，並確認顯示的值是設定的值。

    Get-SendConnector | Format-List Name,Usage,AddressSpaces,SourceTransportServers,DSNRoutingEnabled,SmartHosts,SmartHostAuthMechanism
    Get-ReceiveConnector | Format-List Name,Usage,AuthMechanism,Bindings,RemoteIPRanges

## Mailbox Server 程序

組織中的 Mailbox Server 需要傳送連接器設定為將郵件傳送至 Edge Transport Server 以轉送至網際網路。

預設會在 Mailbox server role 安裝期間建立兩個接收連接器。名為「用戶端 *伺服器名稱*」的連接器已設定為接受來自所有 POP3 和 IMAP 通訊用戶端的郵件。名為「預設 *伺服器名稱*」的連接器已設定為接受來自 Edge Transport Server 的郵件。不需要對這些連接器進行任何修改。

## 步驟 5：建立設定為將外寄郵件傳送到 Edge Transport Server 的傳送連接器

這個傳送連接器需要下列設定：

  - **名稱**   To Edge (或任何描述性名稱)

  - **使用類型**   內部

  - **位址空間**   "\*" (所有網域)

  - 已停用 DNS 路由 (已啟用智慧主機路由)

  - **智慧主機**   Edge Transport Server 的 IP 位址或 FQDN。例如，edge01.contoso.net。

  - **來源 Mailbox Server**   一或多部 Mailbox Server 的 FQDN。例如，mbxserver01.contoso.com 和 mbxserver02.contoso.com。

  - **智慧主機驗證方法**  透過 TLS 的基本驗證。

  - **智慧主機驗證認證**   Edge Transport Server 上使用者帳戶的認證。您需要先在暫存變數中儲存使用者名稱和密碼，因為 **New-SendConnector** 指令程式將不會接受使用純文字的使用者認證。

若要建立設定為將外寄郵件傳送至 Edge Transport Server 的傳送連接器，請執行下列命令。

    $EdgeCredentials = Get-Credential
    New-SendConnector -Name "To Edge" -Usage Internal -AddressSpaces * -DNSRoutingEnabled $false -SmartHosts edge01.contoso.com -SourceTransportServers mbxserver01.contoso.com,mbxserver02.contoso.com -SmartHostAuthMechanism BasicAuthRequireTLS -AuthenticationCredential $EdgeCredentials

如需詳細的語法及參數資訊，請參閱 [New-SendConnector](https://technet.microsoft.com/zh-tw/library/aa998936\(v=exchg.150\))。

## 如何才能了解此步驟是否正常運作？

若要確認您已順利建立設定為將外寄郵件傳送至 Edge Transport Server 的傳送連接器，請在 Mailbox Server 上執行下列命令，並確認顯示的值是設定的值。

    Get-SendConnector | Format-List Name,Usage,AddressSpaces,DSNRoutingEnabled,SmartHosts,SourceTransportServers,SmartHostAuthMechanism

