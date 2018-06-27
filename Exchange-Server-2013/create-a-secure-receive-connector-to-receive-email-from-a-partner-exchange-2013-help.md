---
title: '建立安全的接收連接器從協力廠商接收電子郵件: Exchange 2013 Help'
TOCTitle: 建立安全的接收連接器從協力廠商接收電子郵件
ms:assetid: 06aa692c-7940-4a14-a722-058c47440f85
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ673037(v=EXCHG.150)
ms:contentKeyID: 50472492
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 建立安全的接收連接器從協力廠商接收電子郵件

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-03_

此程序將示範如何設定從協力廠商接收安全的電子郵件的接收連接器。當您需要加密您和受信任的協力廠商之間的通訊時使用此程序。連接器設定為接受只會接受伺服器的驗證與傳輸層安全性 (TLS) 連線。

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


## 使用 EAC 來建立接收伺服器以自合作夥伴接收安全郵件

1.  在 EAC 中，瀏覽至 \[**郵件流程**\>**接收連接器**。按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")來建立新的接收連接器。

2.  在**新接收連接器**\] 索引標籤上指定的接收連接器的名稱，然後選取**Fea-frontend-server-role 傳輸角色**。由於您在此例中會收到郵件從協力廠商，我們建議您一開始路由郵件傳送至前端伺服器，以簡化及合併郵件流程。

3.  選擇**協力廠商**的類型。接收連接器會接收來自信任的協力廠商的郵件。

4.  **網路介面卡繫結**，觀察到**所有可用的 IPV4**為清單中所列**的 IP 位址**和**連接埠**是 25。（簡易郵件傳送通訊協定使用連接埠 25）。這表示連接器會接聽在所有的 IP 位址指派給本機伺服器上的網路介面卡上的連線。按一下 \[**下一步**\]。

5.  如果遠端網路設定\] 頁面會列出 0.0.0.0-255.255.255.255，這表示接收連接器的接收來自所有 IP 位址的連線，按一下 \[**移除**![\[移除\] 圖示](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[移除] 圖示")將其移除。按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")、 新增協力廠商伺服器的 IP 位址並按一下 \[**儲存**\]。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您也可以利用 CIDR 標記法來指定 IP 位址範圍，例如 64.4.6.100/24。</td>
    </tr>
    </tbody>
    </table>


6.  按一下 \[完成\] 以建立連接器。

一次您已建立的接收連接器，則會出現在接收連接器清單。如果您想要查看如何利用指令程式建立的接收連接器的範例，請參閱[New-ReceiveConnector](https://technet.microsoft.com/zh-tw/library/bb125139\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要確認您已成功建立從協力廠商接收郵件的接收連接器，測試協力廠商可以傳送郵件給其中一個您的使用者和該使用者成功接收它。您可以接收加密的郵件 （您可以確認 TLS 用來檢查郵件標頭），如果您知道組態成功數。

## 相關資訊

[接收連接器](receive-connectors-exchange-2013-help.md)

