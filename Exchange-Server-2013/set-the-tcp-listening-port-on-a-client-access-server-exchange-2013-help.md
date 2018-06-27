---
title: '用戶端存取伺服器上設定 TCP 聆聽連接埠: Exchange 2013 Help'
TOCTitle: 用戶端存取伺服器上設定 TCP 聆聽連接埠
ms:assetid: 5f48f21a-d8d4-48b2-868f-9a3647693841
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ673530(v=EXCHG.150)
ms:contentKeyID: 50553990
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 用戶端存取伺服器上設定 TCP 聆聽連接埠

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-04-09_

您可以設定用來接聽執行 Microsoft Exchange Unified Messaging Call Router 服務之用戶端存取伺服器上的 SIP 要求的 TCP 連接埠。根據預設，當您安裝用戶端存取伺服器、 SIP TCP 聆聽連接埠號碼設定為 5060 和 Client Access server 在 TCP 模式中啟動。無法使用 EAC 設定 SIP TCP 聆聽連接埠。您必須設定使用**Set-UMCallRouterSettings**指令程式的 SIP TCP 聆聽連接埠號碼。

如果您的 VoIP 閘道、IP PBX 或工作階段邊界控制器 (SBC) 設定為使用 SIP 標準 5060 以外的 TCP 通訊埠，則可能需要將 TCP 接聽通訊埠設定為 5061。

您只可以設定用戶端存取伺服器 TCP 與 TLS 連接埠。您無法設定 Exchange 2013 Mailbox server 的連接埠。不過，您可以使用**Set-UMService**指令程式來設定 Exchange 2010 UM 伺服器的 TCP 與 TLS 聆聽連接埠。

如需其他與 Unified Messaging Server 和 Client Access Server 相關的工作，請參閱 [UM 服務程序](um-services-procedures-exchange-2013-help.md)。

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

## 使用 EAC 設定 Client Access Server 上的 TCP 接聽通訊埠

1.  在 EAC 中，瀏覽至 \[伺服器\] \> \[伺服器\]。

2.  在清單檢視中，選取您要修改的 Exchange 伺服器，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 **\[Exchange Server\]** 頁面上，按一下 **\[整合通訊\]**。

4.  在 **\[UM 呼叫路由器設定\]** 下的 **\[TCP 接聽通訊埠\]** 下，輸入 TCP 通訊埠號碼，然後按一下 **\[儲存\]**。

## 使用命令介面設定 Client Access Server 上的 TCP 接聽通訊埠

此範例會將名為 `MyClientAccessServer` 的 Client Access Server 上的 TCP 接聽通訊埠設為 5566。

    Set-UMCallRouterSettings -Server MyClientAccessServer -SipTCPListeningPort 5566

