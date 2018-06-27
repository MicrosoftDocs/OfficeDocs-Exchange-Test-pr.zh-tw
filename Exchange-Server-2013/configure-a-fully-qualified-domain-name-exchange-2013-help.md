---
title: '設定的完整的網域名稱: Exchange Online Help'
TOCTitle: 設定的完整的網域名稱
ms:assetid: af093f87-59b7-44a8-a9a2-8f17f0cc7db8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee423553(v=EXCHG.150)
ms:contentKeyID: 50473972
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定的完整的網域名稱

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2012-11-09_

您可以設定整合通訊 (UM) IP 閘道 IP 位址或完整的網域名稱 (FQDN)。當您建立 UM IP 閘道時，您必須定義的 IP 位址或 FQDN 上的 VoIP 閘道、 IP PBX 或您正在使用的工作階段邊界控制器 (SBC) 設定。您可以變更的 IP 位址或 FQDN 之後建立 UM IP 閘道。

如果您建立 UM IP 閘道使用 FQDN，您必須建立 DNS 正向對應區域中的適當的主機 (A) 記錄。如果您建立 UM IP 閘道器使用 FQDN\] 中，並變更 UM IP 閘道的 DNS 設定，您必須停用及啟用以確定其組態資訊正確更新的 UM IP 閘道。

如果您想要使用共同的 UM IP 閘道和撥號對應表的其中一個作業系統之間的傳輸層安全性 (相互 TLS) SIP 安全或安全模式，您必須設定 UM IP 閘道 fqdn。您也必須設定該連接埠 5061 上接聽並確認 VoIP 閘道、 IP PBX 或 SBC 也已設定聆聽的連接埠 5061 上的相互 TLS 要求。若要設定 UM IP 閘道器，請執行下列命令： `Set-UMIPGateway -identity MyUMIPGateway -Port 5061`。

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

## 使用 EAC 來設定 FQDN

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM IP 閘道\]，選取要修改的 UM IP 閘道，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 \[ **UM IP 閘道器**\] 頁面在**位址**\] 中輸入 FQDN 如 VoIP 閘道、 PBX 啟用 SIP、 IP PBX 或 SBC。

3.  按一下 **\[儲存\]**。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您使用 FQDN，而非 IP 位址的 UM IP 閘道上時，確認已建立正確的 DNS 記錄。</td>
</tr>
</tbody>
</table>


## 使用命令介面來設定 FQDN

此範例會設定名為名為 voipgateway.contoso.com FQDN `MyUMIPGateway` UM IP 閘道器。

    Set-UMIPGateway -Identity MyUMIPGateway -Address voipgateway.contoso.com

本範例會設定名為`MySBC` sbc.contoso.com FQDN 與 UM IP 閘道器，並會接聽的 TCP 連接埠 5061 上的 SIP 要求。

    Set-UMIPGateway -Identity MySBC -Address sbc.contoso.com -Port 5061

