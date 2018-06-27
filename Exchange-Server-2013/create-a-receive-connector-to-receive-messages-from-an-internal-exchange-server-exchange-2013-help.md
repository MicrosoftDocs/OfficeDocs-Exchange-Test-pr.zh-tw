---
title: '建立從內部 Exchange 伺服器接收郵件的接收連接器: Exchange 2013 Help'
TOCTitle: 建立從內部 Exchange 伺服器接收郵件的接收連接器
ms:assetid: 546cead9-7a2d-4332-a5f6-35343d56c619
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ657448(v=EXCHG.150)
ms:contentKeyID: 50473127
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 建立從內部 Exchange 伺服器接收郵件的接收連接器

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-03_

當您想要從Exchange伺服器接收郵件時建立**Internal**類型的接收連接器。若要控制郵件路由傳送組織內使用這種連接器類型： 例如，當您想要到另一個路由傳送郵件從特定的 Edge Transport server\]，在信箱伺服器上的傳輸服務或從一個信箱伺服器。

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


## 建立接收連接器以自內部 Exchange 伺服器接收郵件

1.  在 EAC 中，瀏覽至 \[**郵件流程**\>**接收連接器**。按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")來建立新的接收連接器。

2.  在**新接收連接器**\] 索引標籤上指定的接收連接器的名稱，然後選取**集線傳輸角色**。在此案例假設您想要不入及登出組織路由傳送您的網路內的郵件。

3.  選擇**內部**的類型。連接器的設定Exchange伺服器驗證。

4.  如果遠端網路設定\] 頁面會列出 0.0.0.0-255.255.255.255，這表示接收連接器的接收來自所有 IP 位址的連線，按一下 \[**移除**![\[移除\] 圖示](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[移除] 圖示")將其移除。按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")、 新增您想要接收 192.168.1.1，例如、 郵件伺服器的 IP 位址並按一下 \[**儲存**\]。

5.  按一下 \[完成\] 以建立連接器。

一次您已建立的接收連接器，則會出現在接收連接器清單。如果您想要查看如何利用指令程式建立的接收連接器的範例，請參閱[New-ReceiveConnector](https://technet.microsoft.com/zh-tw/library/bb125139\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要確認您已成功建立從內部伺服器接收郵件的接收連接器，測試郵件傳送伺服器旅行社成功的收件者的伺服器。若要執行這項作業的其中一個方法是使用Exchange管理命令介面來設定使用[Set-ReceiveConnector](https://technet.microsoft.com/zh-tw/library/bb125140\(v=exchg.150\))指令程式來`Verbose`、 您建立的接收連接器*ProtocolLoggingLevel*並檢查記錄檔以確保傳遞郵件。

## 相關資訊

[建立從網際網路接收電子郵件的接收連接器](create-a-receive-connector-to-receive-email-from-the-internet-exchange-2013-help.md)

[建立安全的接收連接器從協力廠商接收電子郵件](create-a-secure-receive-connector-to-receive-email-from-a-partner-exchange-2013-help.md)

