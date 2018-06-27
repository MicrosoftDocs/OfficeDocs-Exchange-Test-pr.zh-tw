---
title: '手動設定 Edge Transport server 郵件流程: Exchange 2013 Help'
TOCTitle: 手動設定 Edge Transport server 郵件流程
ms:assetid: cb4cc165-6c09-44ab-a95f-167ae8ed2485
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn606261(v=EXCHG.150)
ms:contentKeyID: 61180459
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 手動設定 Edge Transport server 郵件流程

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-02-21_

本主題說明對 Edge Transport Server 管理郵件流程的方式進行手動組態變更的程序。這些程序旨在處理特定案例；除非您的組織對於進行手動組態變更有特定的需求，否則最好在訂閱 Edge Transport Server 時使用預設組態。

**目錄**

Manually configure Send connectors

Intra-Organization Send Connectors

Create additional Send connectors after Edge subscription

Reasons to suppress automatic creation of Send connectors

Partition mail flow

Route outbound email to a smart host

Configure Send connectors for external relay domains

## 手動設定傳送連接器

您可以手動修改傳送連接器的組態。例如，如需透過智慧主機路由傳送輸出電子郵件，您可以抑制自動建立傳送連接器，並將傳送連接器手動設定為網際網路。

## 組織內傳送連接器

組織內傳送連接器是隱含且隱藏的傳送連接器，是由 Exchange 自動計算而來，而且會讓相同組織中 Mailbox Server 上的傳輸服務彼此轉送郵件，而不需要使用明確的傳送連接器。因為 Edge 訂閱的 Active Directory 中內含具有 Active Directory 站台關聯的組態物件，所以也會使用組織內傳送連接器將郵件轉送至該 Edge Transport Server。

只有位於訂閱的 Active Directory 站台中的 Mailbox Server 可以在訂閱的 Edge Transport Server 直接收發電子郵件。如果您擁有多站台 Active Directory 樹系，而且 Exchange 已部署在多個站台中，則非訂閱站台中的 Mailbox Server 會將輸出電子郵件路由傳送至訂閱的站台。已訂閱站台中的 Mailbox Server 會將輸出電子郵件路由傳送至 Edge Transport Server。

## 在 Edge 訂閱後建立其他傳送連接器

在 Active Directory 站台訂閱 Edge Transport Server 後，就會停用在 Edge Transport Server 上建立及修改傳送連接器的 Cmdlet。如果想要建立 Edge Transport Server 是其來源伺服器的傳送連接器，則可以在 Exchange 組織內建立傳送連接器。您可以指定一個或多個 Edge 訂閱做為傳送連接器的來源伺服器。您不能同時指定 Mailbox Server 和 Edge 訂閱做為同一個傳送連接器的來源伺服器。下次 EdgeSync 同步處理組態資料時，就會將傳送連接器複寫至已設定為來源伺服器的 Edge Transport Server 上的 AD LDS 執行個體。如果您將多個 Edge 訂閱列為來源伺服器，則會平衡已訂閱 Edge Transport Server 間與該傳送連接器之連線的負載。相同 Active Directory 站台必須訂閱 Edge Transport Server，才能進行負載平衡。如果將不同 Active Directory 站台中的 Edge 訂閱設定為相同傳送連接器的來源伺服器，則 Edge Transport Server 只會路由傳送至最接近的來源伺服器。

在下列情況下，您必須手動建立傳送連接器：

  - 您抑制了自動建立網際網路或輸入傳送連接器。

  - 您的組織中有設定為外部轉送網域的公認網域。

## 抑制自動建立傳送連接器的原因

根據您 Exchange 組織的拓撲，可能會決定抑制自動建立傳送連接器。下列範例說明需要您抑制自動建立傳送連接器的案例。

## 分割郵件流程

如果您決定分割兩個 Edge Transport Server 之間的輸入和輸出郵件處理，一個 Edge Transport Server 負責處理輸出郵件流程，另一個 Edge Transport Server 負責處理輸入郵件流程。若要這麼做，請依下列方式設定 Edge 訂閱：

  - 對於輸出 Edge Transport Server，在 Mailbox Server 上執行下列命令。
    
        New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "C:\EdgeServerSubscription.xml" -Encoding Byte -ReadCount 0)) -Site "Site-A" -CreateInboundSendConnector $false -CreateInternetSendConnector $true

  - 對於輸入 Edge Transport Server，在 Mailbox Server 上執行下列命令。
    
        New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "C:\EdgeServerSubscription.xml" -Encoding Byte -ReadCount 0)) -Site "Site-A" -CreateInboundSendConnector $true -CreateInternetSendConnector $false

## 將輸出電子郵件路由傳送到智慧主機

如果 Exchange 組織透過智慧主機路由傳送所有輸出電子郵件，則自動建立的傳送連接器不會有正確的組態。

在 Mailbox Server 上執行下列命令，抑制自動建立網際網路的傳送連接器。

    New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "C:\EdgeServerSubscription.xml" -Encoding Byte -ReadCount 0)) -Site "Site-A" -CreateInternetSendConnector $false

完成 Edge 訂閱處理程序之後，請手動建立至網際網路的傳送連接器。請在 Exchange 組織內建立傳送連接器，並將 Edge 訂閱選為連接器的來源伺服器。選取 `Custom` 用法類型，並設定一或多個智慧主機。這樣下次 EdgeSync 同步處理組態資料時，就會將這個新的傳送連接器複寫至 Edge Transport Server 上的 AD LDS 執行個體。您可以在 Mailbox Server 上執行 **Start-EdgeSynchronization** Cmdlet，強制立即進行 EdgeSync 同步處理。

範例：使用命令介面為訂閱的 Edge Transport Server 設定傳送連接器，以透過智慧主機路由傳送所有網際網路位址空間的郵件。請在 Exchange 組織內的 Mailbox Server 上執行這項工作，而非在 Edge Transport Server 上執行。

    New-SendConnector -Name "EdgeSync - Site-A to Internet" -Usage Custom -AddressSpaces SMTP:*;100 -DNSRoutingEnabled $false -SmartHosts 192.168.10.1 -SmartHostAuthMechanism None -SourceTransportServers EdgeSubscriptionName

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>此範例不會指定任何智慧主機驗證機制。請確定設定正確的驗證機制，並在您於自己的 Exchange 組織中建立智慧主機連接器時提供所有必要認證。</td>
</tr>
</tbody>
</table>


## 設定外部轉送網域的傳送連接器

如果您 Exchange 組織中的公認網域設定為外部轉送網域，則必須手動建立那些位址空間的傳送連接器。而 Edge Transport Server 會轉送正在傳遞至外部轉送網域的郵件。Edge 訂閱處理程序不會自動建立及設定外部轉送網域的傳送連接器。因此，您必須設定那些網域的傳送連接器，並將一或多個 Edge 訂閱指定為那些傳送連接器的來源伺服器。

外部轉送網域的 DNS MX 資源記錄會解析為 Edge Transport Server。您可以設定將電子郵件轉送至外部轉送網域的傳送連接器，以使用智慧主機進行路由傳送。將外部轉送網域的傳送連接器設定成使用 DNS 路由，則會建立路由迴圈。如需外部轉送網域的詳細資訊，請參閱[公認的網域](accepted-domains-exchange-2013-help.md)。

回到頁首

