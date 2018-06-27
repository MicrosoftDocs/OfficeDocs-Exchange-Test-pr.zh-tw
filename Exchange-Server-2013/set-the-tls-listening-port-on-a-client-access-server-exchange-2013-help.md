---
title: '用戶端存取伺服器上設定 TLS 聆聽連接埠: Exchange 2013 Help'
TOCTitle: 用戶端存取伺服器上設定 TLS 聆聽連接埠
ms:assetid: f4401923-61fa-4dc5-95f8-c0d2f515b2ea
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ673576(v=EXCHG.150)
ms:contentKeyID: 50554108
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 用戶端存取伺服器上設定 TLS 聆聽連接埠

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-17_

您可以設定用來接聽 SIP 要求執行 Microsoft Exchange Unified Messaging Call Router 服務之用戶端存取伺服器上的傳輸層安全性 (TLS) 連接埠。根據預設，當您安裝 Client Access server，SIP TLS 聆聽連接埠號碼設定為 5061。

您可能必須將 TLS 聆聽連接埠設為 5061，如果您想：

  - 將 UM 撥號對應表上的 VoIP 安全性設定設為 \[SIP 安全\]。

  - 將 UM 撥號對應表上的 VoIP 安全性設定設為 \[安全\]。

  - 整合到 MicrosoftOffice Communications Server 2007 R2 或 Microsoft Lync Server。

  - 使用相互「傳輸層安全性」(相互 TLS) 在 Client Access Server、執行「Microsoft Exchange 整合通訊」服務的 Mailbox Server，以及 VoIP 閘道、啟用「工作階段初始通訊協定」(SIP) 的專用交換機 (PBX)、IP PBX 或工作階段邊界控制器 (SBC) 之間加密網路資料。

如果您想要使用 mutual TLS 的 UM IP 閘道和操作在 SIP 安全 」 或 「 安全 」 模式下，當您建立 UM IP 閘道撥號對應表之間必須設定以完整的網域名稱 (FQDN) 並則設定 TLS 連接埠 5061 上接聽的 UM IP 閘道。您也必須確認任何 VoIP 閘道、 Pbx 啟用 SIP、 IP Pbx 或 Sbc 也已設定為接聽連接埠 5061 上的相互 TLS 要求。

您只可以設定用戶端存取伺服器 TCP 與 TLS 連接埠。您無法設定 Exchange 2013 Mailbox server 的連接埠。不過，您可以使用**Set-UMService**指令程式來設定 Exchange 2010 UM 伺服器的 TCP 與 TLS 聆聽連接埠。

如需其他與「整合通訊」和 Client Access Server 相關的工作，請參閱 [UM 服務程序](um-services-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「用戶端存取伺服器 (UM 呼叫路由器服務)」項目。

  - 確認您已正確安裝 Client Access Server 和 Mailbox Server。

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

## 使用 EAC 設定 Client Access Server 上的 TLS 接聽埠

1.  在 EAC 中，瀏覽至 \[伺服器\] \>\[伺服器\]。

2.  在清單檢視中，選取您要修改的 Exchange 伺服器，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 **\[Exchange Server\]** 頁面上，按一下 **\[整合通訊\]**。

4.  在 **\[UM Service 設定\]** 的 **\[TLS 接聽埠\]** 下方，輸入 TLS 連接埠的號碼，然後再按一下 **\[儲存\]**。

## 使用命令介面設定 Client Access Server 上的 TLS 接聽埠

此範例會將 `MyClientAccessServer` Client Access Server 上的 TLS 接聽埠設為 5561。

    Set-UMCallRouterSettings -Server MyClientAccessServer -SipTlsListeningPort 5561

