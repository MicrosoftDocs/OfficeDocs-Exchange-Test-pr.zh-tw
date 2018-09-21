﻿---
title: '建立電子郵件傳送至網際網路的傳送連接器: Exchange 2013 Help'
TOCTitle: 建立電子郵件傳送至網際網路的傳送連接器
ms:assetid: 6deaefa8-1152-40d9-b1ba-9c19bdf8a928
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ657457(v=EXCHG.150)
ms:contentKeyID: 50473449
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 建立電子郵件傳送至網際網路的傳送連接器

 

_**適用版本：** Exchange Server 2013_

_**上次修改主題的時間：** 2015-01-23_

根據預設，Microsoft Exchange Server 2013不允許您將您的網域外部傳送郵件。若要將郵件傳送您的網域之外，您需要建立的傳送連接器。下圖說明郵件流程當您建立將郵件傳送至網際網路的傳送連接器。

![connector\_send\_onprem\_internet](images/JJ657457.e8963e4f-7dce-461f-bbcf-660278cefa35(EXCHG.150).gif "connector_send_onprem_internet")

對於案例感興趣一角與使用此程序？請參閱下列主題：

  - [設定郵件流程和用戶端存取](configure-mail-flow-and-client-access-exchange-2013-help.md)

## 開始之前有哪些須知？

  - 預估完成時間：15 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「傳送連接器」項目。

  - 如果您要開始安裝，請參閱[部署 Exchange 2013 的新安裝](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md) 。在安裝之後您可以使用本主題中的步驟來建立輸出連接器。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。


> [!TIP]  
> 有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。




## 您要執行的工作

## 使用 EAC 來建立電子郵件傳送至網際網路的傳送連接器

1.  在 EAC 中，瀏覽至 \[郵件流程\] \> \[傳送連接器\]，然後按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

2.  在 \[**新增傳送連接器**精靈\] 中指定的傳送連接器的名稱，然後選取**網際網路**的**類型**。按一下 \[**下一步**\]。

3.  確認**MX 記錄相關聯收件者的網域**已選取，這會指定連接器使用網域名稱系統 (DNS) 路由傳送郵件。按一下 \[**下一步**\]。

4.  \[**位址空間**，按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。在 \[**新增網域**\] 視窗中，確定 SMTP 列為**類型**。針對 \[**完全完整網域名稱 (FQDN)**\] 中，輸入 \*，這表示這個傳送連接器適用於寄給任何網域的郵件。按一下 \[**儲存**\]。

5.  請確定未選取**範圍內傳送連接器**\] 和 \[**下一步**。

6.  **來源伺服器**上，按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。在 \[**選取伺服器**\] 視窗中，選取要用來將郵件傳送至網際網路透過用戶端存取伺服器並按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")Mailbox server。您已選取伺服器之後，請按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。按一下 \[**確定\]**。

7.  按一下 \[完成\]。

建立傳送連接器之後，它會出現在 \[傳送連接器\] 清單中。

## 使用命令介面來路由傳送郵件到用戶端存取伺服器

在Exchange 2013您可以使用**Set-SendConnector**指令程式的*FrontendProxyEnabled*參數來路由傳送到用戶端存取伺服器的外寄郵件。此參數不設為`$true`根據預設，但在許多情況下可將合併及簡化郵件流程，特別是如果您正在處理大量的郵件伺服器的環境。

本範例會將傳送連接器上設定為`$true`的*FrontendProxyEnabled*參數。

```powershell
Set-SendConnector "Contoso.com Send Connector" -FrontendProxyEnabled $true
```

## 如何知道這是否正常運作？

若要確認您已成功建立電子郵件傳送至網際網路的傳送連接器，一對使用者傳送郵件給外部收件者，並確認郵件已成功送達。

## 相關資訊

[傳送連接器](send-connectors-exchange-2013-help.md)

[建立傳送連接器路由傳送到智慧主機的外寄電子郵件](create-a-send-connector-to-route-outbound-email-through-a-smart-host-exchange-2013-help.md)

