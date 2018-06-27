---
title: '停用 Active Directory 站台之間的 TLS: Exchange 2013 Help'
TOCTitle: 停用 Active Directory 站台之間的 TLS
ms:assetid: 1e1a0acf-24e7-4f94-9b33-603a4e0a812c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd876856(v=EXCHG.150)
ms:contentKeyID: 52062521
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 停用 Active Directory 站台之間的 TLS

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2013-02-19_

Microsoft Exchange Server 2013 支援在某些拓撲的 Mailbox Server 之間停用 SMTP 通訊的 TLS，在這些拓撲中，會使用 WAN 最佳化控制器 (WOC) 裝置來壓縮 SMTP 流量。

本主題提供逐步指示如何設定的傳輸服務中受影響的 Mailbox server 上停用 \[TLS\] 並確定您的 Active Directory 路由拓撲設定正確路由傳送的郵件。若要深入了解此案例，請參閱[案例： 將 Exchange 設定為支援 WAN 的最佳化控制站](scenario-configure-exchange-to-support-wan-optimization-controllers-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 完成這項工作預估時間： 60 分鐘。

  - 即使這個案例內的個別設定步驟可以利用較少的權限來完成，但是若要完成整個端對端案例工作，您的帳戶需要是組織管理角色群組的成員。

  - 確定您只對通過 WOC 裝置的連線停用 TLS。

  - 此程序需要 Exchange 2013 部署在多個 Active Directory 站台中，而且至少有一個站台透過 WAN 連結來連線至其他站台。

  - 此程序需要您部署 WOC 裝置，以壓縮通過 WAN 連結的 SMTP 流量。

  - 此程序需要邏輯郵件流程路徑存在，讓 Exchange 通過已部署 WOC 裝置的 WAN 連結。

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


## 您要執行的工作

## 步驟 1： 使用命令介面來設定為使用降級 Exchange Server 驗證的 Mailbox server 上的傳輸服務

若要將 Mailbox Server 上的傳輸服務設定為使用降級的 Exchange 伺服器驗證，請執行下列命令：

    Set-TransportService <ServerIdentity> -UseDowngradedExchangeServerAuth $true

本範例會對名稱為 Mailbox01 的伺服器進行此組態變更。

    Set-TransportService Mailbox01 -UseDowngradedExchangeServerAuth $true

## 步驟 2： 目標 Active Directory 站台信箱伺服器上建立專用的接收連接器

## 使用 EAC 來建立接收連接器

1.  在 Exchange 系統管理中心 (EAC) 中，按一下 **\[郵件流程\]** \> **\[接收連接器\]**，然後按一下 **\[新增\]**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

2.  在 **\[新增接收連接器\]** 精靈的第一頁上，輸入下列值：
    
      - **名稱**   輸入描述值。
    
      - **類型**   內部
    
    完成後，請按 **\[下一步\]**。

3.  在 \[**遠端設定**\] 區段中的 \[**新接收連接器**精靈的第二頁上輸入目標 Active Directory 站台的 IP 位址或 IP 位址範圍。完成時，按一下 \[**完成**\]。

## 使用命令介面建立接收連接器

若要在 Mailbox Server 上建立接收連接器，請執行下列命令：

    New-ReceiveConnector -Name <Name> -Server <ServerIdentity> -RemoteIPRanges <IPAddressRange> -Internal

本範例會利用下列設定，在名稱為 Mailbox01 的伺服器上建立名稱為 WAN 的接收連接器：

  - *RemoteIPRanges*參數設為 10.0.2.0/24。此 IP 位址範圍應該從這個接收連接器將其中接收未加密的連線會對應到遠端 Active Directory 站台。如果該遠端網站有一個以上的 IP 子網路，您可以輸入它們並以逗號。

  - 使用類型會設為「內部」。

<!-- end list -->

    New-ReceiveConnector -Name WAN -Server Hub01 -RemoteIPRanges 10.0.2.0/24 -Internal

## 步驟 3： 使用命令介面來停用的專用的接收連接器上的 TLS

若要停用接收連接器上的 TLS，請執行下列命令：

    Set-ReceiveConnector <ReceiveConnectorIdentity> -SuppressXAnonymousTLS $true

本範例會在名稱為 Mailbox01 的 Mailbox Server 上，停用名稱為 WAN 的接收連接器上的 TLS。

    Set-ReceiveConnector Mailbox01\WAN -SuppressXAnonymousTLS $true

## 步驟 4： 使用命令介面來指定為中樞站台的 Active Directory 站台

若要將 Active Directory 站台指定為中樞站台，請執行下列命令：

    Set-AdSite <ADSiteIdentity> -HubSiteEnabled $true

在每一個有 Mailbox Server 參與未加密流量的 Active Directory 站台中，您需要各執行此程序一次。

本範例會將名稱為 Central Office Site 1 的 Active Directory 站台設定為中樞站台。

    Set-AdSite "Central Office Site 1" -HubSiteEnabled $true

## 步驟 5： 使用命令介面來設定透過 WAN 連線的最低成本路由路徑

根據如何設定 IP 站台連結成本的 Active Directory 中，此步驟可能不需要。您必須確認與部署 WOC 裝置的網路連結 leastcost 路由路徑中。若要檢視 Active Directory 站台連結成本，以及 Exchange 特定站台連結成本，執行下列命令：

    Get-AdSiteLink

如果最低成本路由路徑不是與部署 WOC 裝置的網路連結，您需要將 Exchange 特定成本指派給特定 IP 站台連結以確保正確路由傳送的郵件。若要深入了解此特定問題，請參閱 ＜ 中[案例： 將 Exchange 設定為支援 WAN 的最佳化控制站](scenario-configure-exchange-to-support-wan-optimization-controllers-exchange-2013-help.md)的 「 設定 Exchange 特定 Active Directory 站台連結成本 」 一節。

本範例會在名稱為 Branch Office 2-Branch Office 1 的 IP 站台連結上，設定 Exchange 特有成本 15。

    Set-AdSiteLink "Branch Office 2-Branch Office 1" -ExchangeCost 15

