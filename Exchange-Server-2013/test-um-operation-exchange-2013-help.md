---
title: '測試 UM 作業: Exchange 2013 Help'
TOCTitle: 測試 UM 作業
ms:assetid: 06c9ab4e-8272-47b1-a217-e366f7e9dbaa
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa995957(v=EXCHG.150)
ms:contentKeyID: 56271542
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 測試 UM 作業

 

_**適用版本：**Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-06-25_

本主題說明如何使用命令介面來測試語音信箱系統的作業。當您執行下列程序時，執行 Microsoft Exchange 整合通訊服務的 Mailbox Server 會起始診斷工作階段初始通訊協定 (SIP) 呼叫，然後傳回 UM 服務的健全狀況狀態變數。

此診斷測試僅可在本機 Mailbox Server 上執行，而且您無法使用 EAC 來測試 Mailbox Server 的作業。

如需與 Client Access Server 和 Mailbox Server 相關的其他管理工作，請參閱 [UM 服務程序](um-services-procedures-exchange-2013-help.md)。

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


## 使用命令介面來測試整合通訊服務的作業

本範例在本機 Mailbox Server 上執行連線和操作測試，然後顯示 Voice over IP (VoIP) 連線資訊。

    Test-UMConnectivity

此範例可測試本機 Client Access Server 在 TCP 通訊埠 5060 上接聽傳入之未加密 SIP 要求的能力。

    Test-UMConnectivity -ListenPort 5060

此範例可測試本機 Client Access Server 在 TCP 通訊埠 5061 上接聽傳入之已加密 SIP 要求的能力。

    Test-UMConnectivity -ListenPort 5061

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>-UMIPGateway</code> 參數未指定時，請使用模式 1。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您可以使用小於 5 秒的值來設定 <code>-Timeout</code> 參數。不過，建議您一律將此參數值設為大於或等於 5 秒。</td>
</tr>
</tbody>
</table>

