---
title: '建立協力廠商，套用傳輸層安全性 (TLS) 傳送電子郵件的傳送連接器: Exchange 2013 Help'
TOCTitle: 建立協力廠商，套用傳輸層安全性 (TLS) 傳送電子郵件的傳送連接器
ms:assetid: ff2abefc-dd3e-4431-b947-df942fbf82d9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ657514(v=EXCHG.150)
ms:contentKeyID: 50474669
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 建立協力廠商，套用傳輸層安全性 (TLS) 傳送電子郵件的傳送連接器

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-15_

如果您想要確保安全、 加密與合作夥伴的通訊，您可以建立設定為強制傳輸層安全性 (TLS) 傳送至協力廠商網域的郵件的傳送連接器。TLS 透過網際網路提供安全通訊。

對於案例感興趣一角與使用此程序？請參閱下列主題：

  - [設定郵件流程和用戶端存取](configure-mail-flow-and-client-access-exchange-2013-help.md)

## 開始之前有哪些須知？

  - 預估完成時間：10 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「傳送連接器」項目。

  - 如果您要開始安裝，請參閱[部署 Exchange 2013 的新安裝](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md) 。在安裝之後您可以使用本主題中的步驟來建立輸出連接器。

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


## 使用 EAC 建立傳送連接器，在套用 TLS 的情形下傳送電子郵件給夥伴

若要建立這種情形下的傳送連接器，請登入 EAC 並執行下列步驟：

1.  在 EAC 中，瀏覽至 \[郵件流程\] \> \[傳送連接器\]，然後按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

2.  在 \[**新增傳送連接器**精靈\] 中指定的傳送連接器的名稱，然後選取**協力廠商**的**類型**。當您選取**協力廠商**時，連接器已設定為允許使用 TLS 憑證進行驗證的伺服器連線。按一下 \[**下一步**\]。

3.  確認**MX 記錄相關聯收件者的網域**已選取，這會指定連接器使用網域名稱系統 (DNS) 路由傳送郵件。按一下 \[**下一步**\]。

4.  \[**位址空間**，按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。在 \[**新增網域**\] 視窗中，確定 SMTP 列為**類型**。**完全完整網域名稱 (FQDN)**，輸入您的協力廠商網域的名稱。按一下 \[**儲存**\]。

5.  **來源伺服器**上，按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。在 \[**選取伺服器**\] 視窗中，選取要用來將郵件傳送至網際網路透過用戶端存取伺服器並按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")Mailbox server。您已選取伺服器之後，請按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。按一下 \[**確定\]**。

6.  按一下 \[完成\]。

建立傳送連接器之後，它會出現在 \[傳送連接器\] 清單中。

## 如何才能了解這是否正常運作？

若要確認您已成功建立協力廠商，以套用的 TLS 傳送電子郵件的傳送連接器從您的組織中的使用者傳送郵件給收件者位於協力廠商組織。如果收件者收到郵件，已成功建立連接器。

## 相關資訊

[建立電子郵件傳送至網際網路的傳送連接器](create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md)

[建立傳送連接器路由傳送到智慧主機的外寄電子郵件](create-a-send-connector-to-route-outbound-email-through-a-smart-host-exchange-2013-help.md)

