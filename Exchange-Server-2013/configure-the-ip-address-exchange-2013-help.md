---
title: '設定 IP 位址: Exchange Online Help'
TOCTitle: 設定 IP 位址
ms:assetid: 100541c1-2297-4c46-9602-b304736541a8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb266940(v=EXCHG.150)
ms:contentKeyID: 50472578
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定 IP 位址

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2012-11-11_

建立整合通訊 (UM) IP 閘道器之前，必須先在 VoIP 閘道、 IP PBX 或工作階段邊界控制器 (SBC) 您正在使用設定的 IP 位址或完整的網域名稱 (FQDN)。然後，當您建立 UM IP 閘道，您設定的 IP 位址或 FQDN。稍後可以變更的 IP 位址或 FQDN。

您可以設定的 IP 位址或使用 EAC 或命令介面的 FQDN。在 EAC 中，在 \[ **UM IP 閘道器**\] 頁面的 \[**位址**\] 方塊可接受 IPv4 IP 位址、 IPv6 位址或 FQDN。您也可以使用命令介面中**Set-UMIPGateway**指令程式上的*Address*參數設定 IPv4 IP 位址、 IPv6 位址或 FQDN。如果您建立 UM IP 閘道使用 FQDN，您必須建立 DNS 正向對應區域中的適當的主機 A 記錄。如果變更 UM IP 閘道的 DNS 設定，您必須停用及啟用以確定其組態資訊正確更新的 UM IP 閘道。

如需與 UM IP 閘道相關的其他管理工作，請參閱[UM IP 閘道程序](um-ip-gateway-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 2 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM IP 閘道」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

  - 執行這些程序之前，請確認已建立 UM IP 閘道器。如需詳細步驟，請參閱[建立 UM IP 閘道器](create-a-um-ip-gateway-exchange-2013-help.md)。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 您要執行的工作

## 使用 EAC 在 UM IP 閘道器上設定 IP 位址

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM IP 閘道\]，選取要修改的 UM IP 閘道，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 \[UM IP 閘道\] 頁面上的 \[位址\]方塊中，輸入 VoIP 閘道、IP PBX 或工作階段邊界控制器 (SBC) 的 IP 位址。

3.  按一下 **\[儲存\]** 以儲存變更。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您的 UM IP 閘道器是使用 FQDN 而非 IP 位址，請確認已建立正確的 DNS 記錄。</td>
</tr>
</tbody>
</table>


## 使用命令介面在 UM IP 閘道器上設定 IP 位址

此範例使用 IP 位址 10.10.10.1 設定名為 `MyUMIPGateway` 的 UM IP 閘道。

    Set-UMIPGateway -Identity MyUMIPGateway -Address 10.10.10.1

此範例使用 IP 位址 10.10.10.10 設定名為 `MyUMIPGateway` 的 UM IP 閘道，並接聽 TCP 連接埠 5061 的 SIP 要求。

    Set-UMIPGateway -Identity MyUMIPGateway -Address 10.10.10.10 -Port 5061

此範例將防止名為 `MyUMIPGateway` 的 UM IP 閘道接受來電及輸出通話、設定 IPv6 地址並且允許 UM IP 閘道使用IPv4 與 IPV6 地址。

    Set-UMIPGateway -Identity MyUMIPGateway -Address fe80::39bd:88f7:6969:d223%11 -IPAddressFamily Any -Status Disabled -OutcallsAllowed $false

