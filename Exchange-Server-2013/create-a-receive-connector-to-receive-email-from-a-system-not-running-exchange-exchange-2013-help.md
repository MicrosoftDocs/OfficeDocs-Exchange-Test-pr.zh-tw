---
title: '建立未執行 Exchange 系統中接收電子郵件的接收連接器: Exchange 2013 Help'
TOCTitle: 建立未執行 Exchange 系統中接收電子郵件的接收連接器
ms:assetid: 85f0864a-6502-49db-8804-16755a7292b4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ657467(v=EXCHG.150)
ms:contentKeyID: 50473676
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 建立未執行 Exchange 系統中接收電子郵件的接收連接器

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-03_

您可能會有您要從未執行 Exchange 系統接收郵件之的情況。例如，如果您有執行網路 appliance 原則會檢查並再將郵件路由傳送至Exchange伺服器。我們在此案例假設 appliance 使用 SMTP。如果不是，您應該使用的外部連接器或傳遞代理程式連接器。

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


## 使用 EAC 建立接收連接器來接收郵件裝置所傳入的郵件

1.  在 EAC 中，瀏覽至 \[**郵件流程**\>**接收連接器**。按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")建立的接收連接器。

2.  在**新接收連接器**\] 索引標籤上指定的接收連接器的名稱，然後選取**集線傳輸角色**。在此例中您想您執行從 appliance 接收郵件的傳輸服務的信箱伺服器。

3.  對於類型請選擇 \[自訂\]，因為接收伺服器將會接收不是執行 Microsoft Exchange Server 2013 裝置所傳入的郵件。

4.  **網路介面卡繫結**，您會看到**所有可用的 IPV4**會列在 \[ **IP 位址**清單。按一下 \[**下一步**\]。

5.  **遠端網路設定**\]，按一下 \[**移除**![\[移除\] 圖示](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[移除] 圖示")**0.0.0.0-255.255.255.255**移除**IP 位址**\] 清單中，由於您想要指定連接器接受來自特定 appliance 的郵件。按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")新增新的 IP 位址，然後在 \[**新增 IP 位址**\] 視窗中，新增您 appliance 的 IP 位址。按一下 \[**儲存**\]。

6.  按一下 \[完成\] 按鈕以建立您的連接器。

一次您已建立的接收連接器，則會出現在接收連接器清單。如果您想要查看如何利用指令程式建立的接收連接器的範例，請參閱[New-ReceiveConnector](https://technet.microsoft.com/zh-tw/library/bb125139\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要確認您已成功建立從訊息 appliance 接收郵件的接收連接器，測試您可以從 appliance 接收郵件。您可以收到郵件，如果您知道組態成功數。

## 相關資訊

[建立從網際網路接收電子郵件的接收連接器](create-a-receive-connector-to-receive-email-from-the-internet-exchange-2013-help.md)

