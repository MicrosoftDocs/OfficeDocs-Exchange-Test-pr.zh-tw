---
title: '允許或防止自動答錄服務在信箱伺服器上: Exchange 2013 Help'
TOCTitle: 允許或防止自動答錄服務在信箱伺服器上
ms:assetid: 4b860c09-6669-4e3d-b3dc-17b8018b3860
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa997908(v=EXCHG.150)
ms:contentKeyID: 50553980
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 允許或防止自動答錄服務在信箱伺服器上

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2012-11-18_

您可以讓 Microsoft Exchange 整合通訊服務至新的接聽或防止能力的信箱伺服器上。根據預設，在信箱伺服器是在啟用狀態安裝後。當您正在設定為接受傳入的語音、 傳真、 自動語音應答以及 Outlook Voice Access 電話的 Mailbox server 時，您會使用**Set-ServerComponentState**指令程式。

設定在維護模式的 Mailbox server 可讓您需要停止服務的伺服器。信箱伺服器的服務 （英文） 表示伺服器將不會主控任何使用中資料庫、 所有傳輸佇列都是空的且伺服器不接受任何來電從用戶端存取伺服器、 VoIP 閘道、 IP Pbx、 已啟用 SIP 的 Pbx 或工作階段邊界控制器 (Sbc)。

在Exchange 2007和Exchange 2010，有無法用來控制的整合通訊伺服器的操作狀態的狀態參數。在Exchange 2013、 無狀態參數是提供該**Set-UMService** cmdlet 針對信箱伺服器上的目的。

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


如需與信箱伺服器相關的其他管理工作，請參閱 [UM 服務程序](um-services-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：3 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「Exchange 伺服器設定」項目。

  - 確認信箱伺服器已經安裝完成，無論是在用戶端存取伺服器的同一部電腦上或位於其他電腦上。

  - 如果您要讓信箱伺服器進入維護模式，請確認所有資料庫副本有足夠的備援可讓伺服器停止服務。

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


## 使用命令介面允許或阻止在信箱伺服器上自動答錄

此範例會啟用信箱伺服器 `UMMBXr-05x.contoso.com` 接聽來自 VoIP 閘道、IP PBX、啟用 SIP 的 PBX 和 SBC 的傳入語音、傳真、自動語音應答和 Outlook Voice Access 通話的功能，並且將變更寫入 UMMBX-05x 伺服器上的登錄。

    Set-ServerComponentState -Component UnifiedMessaging -Identity UMMBX-05x.contoso.com -Requester Maintenance -State Active -LocalOnly

此範例會阻止信箱伺服器 `UMMBX-05x.contoso.com` 接聽來自 VoIP 閘道、IP PBX、啟用 SIP 的 PBX 和 SBC 的傳入語音、傳真、自動語音應答和 Outlook Voice Access 通話的功能，並且僅將變更寫入 Active Directory。

    Set-ServerComponentState -Component UnifiedMessaging -Identity UMMBX-05x.contoso.com -Requester Maintenance -State Inactive -RemoteOnly

