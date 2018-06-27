---
title: '測試 UM 與 VoIP 閘道和 Pbx 的連線: Exchange 2013 Help'
TOCTitle: 測試 UM 與 VoIP 閘道和 Pbx 的連線
ms:assetid: 2aca8631-a99a-4e29-aff0-e462385f03b2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa996906(v=EXCHG.150)
ms:contentKeyID: 56271546
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 測試 UM 與 VoIP 閘道和 Pbx 的連線

 

_**適用版本：**Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2014-09-17_

您可以測試整合通訊 (UM) 和相關連線電話語音設備的作業。執行下列程序時，Client Access Server 和 Mailbox Server 會測試語音信箱系統的完整端對端作業。這包含連接到 Client Access Server 和 Mailbox Server 的電話語音元件，包括 VoIP 閘道、專用交換機 (PBX)、IP PBX 和佈線。

與疑難排解 UM 相關的其他管理工作，請參閱[UM 服務程序](um-services-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：3 分鐘。

  - [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱「Mailbox Server (UM 服務)」和「Client Access Server (UM Call Router 服務)」項目。

  - 若要執行下列程序，您必須使用本機 Administrators 群組成員的帳戶登入 Mailbox Server。

  - 確認信箱伺服器已經安裝完成，無論是在用戶端存取伺服器的同一部電腦上或位於其他電腦上。

  - 確認用戶端存取伺服器已經安裝完成，無論是在信箱伺服器的同一部電腦上或位於其他電腦上。

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


## 使用命令介面來測試整合通訊和電話語音元件的作業

此範例會測試 UM IP 閘道在 TCP 通訊埠 5060 上接聽傳入 SIP 要求的能力。

    Test-UMConnectivity -ListenPort 5060 -UMIPGateway MyIPGateway

本範例會使用電話號碼 56780，測試本機 Mailbox Server 使用不安全的 TCP 連線 (而非安全的相互 TLS 連線)，透過名為 `MyUMIPGateway` 的 UM IP 閘道撥打電話的能力。

    Test-UMConnectivity -UMIPGateway MyUMIPGateway -Phone 56780 -Secured $false

此範例會使用 SIP URI，測試撥號對應表上的 Outlook 語音存取號碼。本範例可以用於包含 Lync Server 的環境中。

    Test-UMConnectivity -UMIPGateway OCSGateway1 -Phone "sip:SIPdialplan.contoso.com@contoso.com"

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您可以使用小於 5 秒的值來設定 <code>-Timeout</code> 參數。不過，建議您一律將此參數值設為大於或等於 5 秒。當命令列語法中有指定 <code>­UMIPGateway</code> 參數時，請使用模式 2。</td>
</tr>
</tbody>
</table>

