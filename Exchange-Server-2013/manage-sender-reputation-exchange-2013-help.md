---
title: '管理寄件者信譽: Exchange 2013 Help'
TOCTitle: 管理寄件者信譽
ms:assetid: f2716bd9-e3ac-46d9-9264-4e3dabfa0f38
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb125186(v=EXCHG.150)
ms:contentKeyID: 50474574
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理寄件者信譽

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-08_

寄件者信譽通訊協定分析代理程式所提供。寄件者信譽封鎖根據寄件者的各種特性的郵件。寄件者信譽依賴持續性來決定何種巨集指令，內送郵件採取的任何寄件者的相關資料。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘

  - [反垃圾郵件和反惡意程式的權限](anti-spam-and-anti-malware-permissions-exchange-2013-help.md)主題中的您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱「反垃圾郵件功能」項目。

  - 您只能使用命令介面來執行此程序。

  - 預設在 Mailbox Server 的 Transport 服務中未啟用反垃圾郵件功能。通常只有在您的 Exchange 組織接受內送郵件之前未進行任何事前的反垃圾郵件篩選的情況下，您才會在 Mailbox Server 上啟用反垃圾郵件功能。如需詳細資訊，請參閱[啟用信箱伺服器上的反垃圾郵件功能](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md)。

  - 通訊協定分析代理程式為基礎的代理程式的寄件者信譽功能。當您停用寄件者信譽時、 通訊協定分析代理程式仍會啟用。

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

## 使用命令介面啟用或停用寄件者信譽

此範例會停用寄件者信譽。

    Set-SenderReputationConfig -Enabled $false

此範例會啟用寄件者信譽。

    Set-SenderReputationConfig -Enabled $true

## 如何才能了解這是否正常運作？

若要確認您是否已成功啟用或停用寄件者信譽，請執行下列操作：

1.  執行下列命令，確認 \[通訊協定分析\] 代理程式已安裝並啟用：
    
        Get-TransportAgent

2.  執行下列命令，驗證您設定的寄件者信譽值：
    
        Get-SenderReputationConfig | Format-List Enabled,*MailEnabled

## 使用命令介面，對內部或外部郵件啟用或停用寄件者信譽

根據預設，寄件者信譽會對外部郵件啟用和停用內部郵件的。郵件會被視為外部如果它是來自未經過驗證連線至 Exchange 組織外部的。郵件會被視為內部，如果它是來自已驗證連線，且寄件者的網域設定為 Exchange 組織中授權網域。

若要對外部郵件停用寄件者信譽，請執行下列命令：

    Set-SenderReputationConfig -ExternalMailEnabled $false

若要對外部郵件啟用寄件者信譽，請執行下列命令：

    Set-SenderReputationConfig -ExternalMailEnabled $true

若要對內部郵件停用寄件者信譽，請執行下列命令：

    Set-SenderReputationConfig -InternalMailEnabled $false

若要對內部郵件啟用寄件者信譽，請執行下列命令：

    Set-SenderReputationConfig -InternalMailEnabled $true

## 如何才能了解這是否正常運作？

若要確認您是否已成功啟用或停用內部及外部郵件的寄件者信譽，請執行下列操作：

1.  執行下列命令：
    
        Get-SenderReputationConfig | Format-List Enabled,*MailEnabled

2.  請確認顯示的值符合您所設定的值。

## 使用命令介面來設定寄件者信譽內容

若要設定寄件者信譽內容，請執行下列命令：

    Set-SenderReputationConfig -SrlBlockThreshold <Value> -SenderBlockingPeriod <Hours>

本範例會將寄件者信譽等級 (SRL) 封鎖閾值設成 6 並且設定寄件者信譽，以將違規寄件者加入到 36 小時的 IP 封鎖清單中：

    Set-SenderReputationConfig -SrlBlockThreshold 6 -SenderBlockingPeriod 36

## 如何才能了解這是否正常運作？

若要確認您是否已成功設定收件者信譽內容，請執行下列操作：

1.  執行下列命令：
    
        Get-SenderReputationConfig

2.  請確認顯示的值符合您所設定的值。

## 使用命令介面來設定輸出存取，用於偵測開放式 Proxy 伺服器

您可能需要執行其他步驟以允許寄件者信譽周遊網際網路和執行通訊協定分析代理程式 Exchange server 之間的任何防火牆。下表列出所需的寄件者信譽的撥出連接埠。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>通訊協定</th>
<th>通訊埠</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SOCKS4、SOCKS5</p></td>
<td><p>1081, 1080</p></td>
</tr>
<tr class="even">
<td><p>Wingate、Telnet、Cisco</p></td>
<td><p>23</p></td>
</tr>
<tr class="odd">
<td><p>HTTP CONNECT、HTTP POST</p></td>
<td><p>6588, 3128, 80</p></td>
</tr>
</tbody>
</table>


若要設定輸出存取以偵測開放式 Proxy 伺服器，請執行下列命令：

    Set-SenderReputationConfig -ProxyServerName <String> -ProxyServerPort <Port> -ProxyServerType <String>

本範例會設定寄件者信譽來使用名為 SERVER01 的開放式 Proxy 伺服器，此伺服器將使用連接埠 80 上的 HTTP CONNECT 通訊協定。

    Set-SenderReputationConfig - ProxyServerName SERVER01 -ProxyServerPort 80 -ProxyServerType HttpConnect

## 如何才能了解這是否正常運作？

若要確認您是否已成功設定輸出存取以偵測開放式 Proxy 伺服器，請執行下列操作：

1.  執行下列命令：
    
        Get-SenderReputationConfig | Format-List ProxyServer*

2.  請確認顯示的值是您所設定的值。

