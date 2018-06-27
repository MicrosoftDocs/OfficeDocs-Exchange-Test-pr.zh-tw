---
title: '建立從網際網路接收電子郵件的接收連接器: Exchange 2013 Help'
TOCTitle: 建立從網際網路接收電子郵件的接收連接器
ms:assetid: 534bbd32-a0db-4d50-9579-4933b156d7b3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ657447(v=EXCHG.150)
ms:contentKeyID: 50473117
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 建立從網際網路接收電子郵件的接收連接器

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-15_

該程序將顯示如何從網際網路設定接收連接器以接收電子郵件。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在大多數情況下，您不需要明確設定的接收連接器從網際網路接收郵件因為為接受來自網際網路的郵件的接收連接器隱含建立時的Exchange安裝。請參閱<a href="receive-connectors-exchange-2013-help.md">接收連接器</a>如需詳細資訊。</td>
</tr>
</tbody>
</table>


對於案例感興趣一角與使用此程序？請參閱下列主題：

  - [設定郵件流程和用戶端存取](configure-mail-flow-and-client-access-exchange-2013-help.md)

## 開始之前有哪些須知？

  - 預估完成時間：15 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md) 主題中的「接收連接器」項目。

  - 如果您要開始安裝，請參閱[部署 Exchange 2013 的新安裝](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md) 。在安裝之後您可以使用步驟本主題中建立您接收連接器。

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


## 使用 EAC 來從網際網路建立接收連接器以接收郵件

1.  在 EAC 中，瀏覽至 \[**郵件流程**\>**接收連接器**。按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")建立的接收連接器。

2.  在**新接收連接器**\] 索引標籤上指定的接收連接器的名稱，然後選取**Fea-frontend-server-role 傳輸角色**。由於您已在此例中從網際網路接收郵件，我們建議您一開始路由郵件給前端伺服器或伺服器，來簡化及合併郵件流程。

3.  選擇 \[**網際網路**\] 類型。接收連接器會接收來自網際網路的寄件者的郵件。

4.  **網路介面卡繫結**，觀察到**所有可用的 IPV4**為清單中所列**的 IP 位址**和**連接埠**是 25。（簡單郵件 Transer 通訊協定 (SMTP) 使用連接埠 25）。這表示連接器會接聽在所有的 IP 位址指派給本機伺服器上的網路介面卡上的連線。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>若您有多個網路介面卡，可在此頁面新增本機伺服器上指派給特定網路介面卡的 IP 位址，但此動作不是必要的。</td>
    </tr>
    </tbody>
    </table>


5.  按一下\[完成\]按鈕以建立您的連接器。

一次您已建立的接收連接器，則會出現在接收連接器清單。如果您想要查看如何利用指令程式建立的接收連接器的範例，請參閱[New-ReceiveConnector](https://technet.microsoft.com/zh-tw/library/bb125139\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要確認您已成功建立從網際網路接收郵件的接收連接器，測試您可以傳送郵件來自外部來源與其中一個使用者可以接收它。您可以收到郵件，如果您知道組態成功數。

## 相關資訊

[建立安全的接收連接器從協力廠商接收電子郵件](create-a-secure-receive-connector-to-receive-email-from-a-partner-exchange-2013-help.md)

[建立未執行 Exchange 系統中接收電子郵件的接收連接器](create-a-receive-connector-to-receive-email-from-a-system-not-running-exchange-exchange-2013-help.md)

