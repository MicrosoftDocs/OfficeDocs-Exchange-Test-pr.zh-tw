---
title: '允許或防止自動答錄服務用戶端存取伺服器上: Exchange 2013 Help'
TOCTitle: 允許或防止自動答錄服務用戶端存取伺服器上
ms:assetid: 8287bb78-2621-4b80-a128-8f2ccd67923a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb123529(v=EXCHG.150)
ms:contentKeyID: 50554019
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 允許或防止自動答錄服務用戶端存取伺服器上

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2012-11-18_

您可以讓 Microsoft Exchange Unified Messaging Call Router 服務至新的接聽或防止這麼 Client Access server 上。根據預設，用戶端存取伺服器會啟用狀態安裝後。當您正在設定為接受傳入的語音、 傳真、 自動語音應答以及 Outlook Voice Access 電話的 Client Access server 時，您會使用**Set-ServerComponentState**指令程式。

在維護模式設定 Client Access server 可讓您需要停止服務的伺服器。用戶端存取伺服器、 服務 （英文） 表示伺服器不接受任何來電 VoIP 閘道、 IP Pbx、 已啟用 SIP 的 Pbx 或工作階段邊界控制器 (Sbc)。

在Exchange 2007和Exchange 2010，有無法用來控制的整合通訊伺服器的操作狀態的狀態參數。在Exchange 2013、 無狀態參數是提供該**Set-UMCallRouterSettings**指令程式上的用戶端存取伺服器上的目的。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>它不被必要的用戶端存取和信箱伺服器新增至 UM 撥號對應表之前他們可以處理來電整合通訊，除了您正在整合 UM 與 Microsoft Office Communications Server 2007 R2 或 Microsoft Lync Server 時。根據預設，在組織中的所有用戶端存取和信箱伺服器可用來接聽來電。</td>
</tr>
</tbody>
</table>


如需其他與用戶端存取伺服器相關的管理工作，請參閱 [UM 服務程序](um-services-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：3 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「Exchange 伺服器設定」項目。

  - 確認用戶端存取伺服器已經安裝完成，無論是在信箱伺服器的同一部電腦上或位於其他電腦上。

  - 如果您將用戶端存取伺服器放入維護模式，請驗證用戶端存取序列中有足夠良好容量以允許伺服器暫停服務。

  - 暫停伺服器的維護模式之前，請驗證伺服器的狀況並確定伺服器已準備好恢復服務。

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


## 使用命令介面以允許或防止在用戶端存取伺服器上的呼叫回答

此範例啟用用戶端存取伺服器 `UMCallRouter-05x.contoso.com` 回答來自 VoIP 閘道、IP PBX、SIP 啟用 PBX 以及 SBC 的傳入語音、傳真、自動語音回應以及 Outlook 語音存取呼叫，並且會將變更寫入到 UMCallRouter-05x 伺服器上的登錄。

    Set-ServerComponentState -Component UnifiedMessaging -Identity UMCallRouter-05x.contoso.com -Requester Maintenance -State Active -LocalOnly

此範例防止用戶端存取伺服器 `UMCallRouter-05x.contoso.com` 回答來自 VoIP 閘道、IP PBX、SIP 啟用 PBX 以及 SBC 的傳入語音、傳真、自動語音回應以及 Outlook 語音存取呼叫，並且只會將變更寫入到 Active Directory。

    Set-ServerComponentState -Component UnifiedMessaging -Identity UMCallRouter-05x.contoso.com -Requester Maintenance -State Inactive -RemoteOnly

