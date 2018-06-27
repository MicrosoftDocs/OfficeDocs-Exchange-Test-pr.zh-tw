---
title: '設定 [聆聽連接埠: Exchange Online Help'
TOCTitle: 設定 [聆聽連接埠
ms:assetid: 200ecbd8-18c3-4594-9cc8-924b3ab4eca1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee633457(v=EXCHG.150)
ms:contentKeyID: 50553949
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定 \[聆聽連接埠

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-22_

您可以設定用來聆聽的整合通訊 (UM) IP 閘道上的工作階段初始通訊協定 (SIP) 要求的 TCP 連接埠。根據預設，當您建立 UM IP 閘道器 TCP 的 SIP 聆聽連接埠號碼是設為 5060。無法設定或使用 EAC 變更 TCP 的 SIP 聆聽連接埠。您必須使用**Set-UMIPGateway**指令程式來設定 TCP 的 SIP 聆聽連接埠號碼。

如果您想要執行下列操作，可能必須將 TCP 接聽連接埠號碼設為 5061：

  - 在 UM 撥號對應表上將 VoIP 安全性設定設為 \[SIP 安全\]。

  - 在 UM 撥號對應表上將 VoIP 安全性設定設為 \[安全\]。

  - 整合到 MicrosoftOffice Communications Server 2007 R2 或 Microsoft Lync Server。

  - 使用相互傳輸層安全性 (相互 TLS) 加密 Exchange Server 與 VoIP 閘道、支援 SIP 的專用交換機 (PBX)、IP PBX 或工作階段邊界控制器 (SBC) 之間的網路資料。

如果您想要在 UM IP 閘道和處於 \[SIP 安全\] 或 \[安全\] 模式的撥號對應表之間使用相互 TLS，當您建立 UM IP 閘道時，必須使用完整網域名稱 (FQDN) 設定它，然後使用命令介面設定 UM IP 閘道在 TCP 連接埠 5061 上接聽。您也必須確認已設定任何 VoIP 閘道、支援 SIP 的 PBX、IP PBX 和 SBC 在連接埠 5061 上接聽相互 TLS 要求。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您建立 UM IP 閘道使用 FQDN 時，您必須建立 DNS 正向對應區域中的適當的主機 (A) 記錄。如果您建立 UM IP 閘道器使用 FQDN] 中，並變更 UM IP 閘道的 DNS 設定，您必須停用及啟用以確定 UM IP 閘道的組態資訊正確更新的 UM IP 閘道。</td>
</tr>
</tbody>
</table>


如需與 UM IP 閘道相關的其他管理工作，請參閱[UM IP 閘道程序](um-ip-gateway-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 2 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM IP 閘道」項目。

  - 執行此程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

  - 執行此程序之前，請確認已建立 UM IP 閘道器。如需詳細步驟，請參閱[建立 UM IP 閘道器](create-a-um-ip-gateway-exchange-2013-help.md)。

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


## 使用命令介面設定 TCP 接聽連接埠

此範例會設定名為 `MyUMIPGateway` 且 FQDN 為 mTLS.MyUMIPGateway.contoso.com 的 UM IP 閘道，並接聽 TCP 連接埠 5061 上的 SIP 要求。

    Set-UMIPGateway -Identity MyUMIPGateway -Address mTLS.MYUMIPGateway.contoso.com -Port 5061

此範例會設定名為 `MyUMIPGateway` 且 FQDN 為 SIPSecured.MyUMIPGateway.contoso.com 的 UM IP 閘道，並接聽 TCP 連接埠 5061 上的 SIP 要求。

    Set-UMIPGateway -Identity MyUMIPGateway -Address SIPSecured.MyUMIPGateway.contoso.com -Port 5061

此範例會設定名為 `MyUMIPGateway` 且 FQDN 為 MyOCSUMIPGateway.contoso.com 的 UM IP 閘道，並接聽 TCP 連接埠 5061 上的 SIP 要求。

    Set-UMIPGateway -Identity MyUMIPGateway -Address MyOCSUMIPGateway.contoso.com -Port 5061

