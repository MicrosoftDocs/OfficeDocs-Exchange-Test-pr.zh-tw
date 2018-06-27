---
title: '使用 Exchange 2010 或 2007 Edge Transport server 在 Exchange 2013: Exchange 2013 Help'
TOCTitle: 使用 Exchange 2010 或 2007 Edge Transport server 在 Exchange 2013
ms:assetid: ce99b4bd-868c-4767-9009-e22c17ac0ac7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ150569(v=EXCHG.150)
ms:contentKeyID: 50474296
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用 Exchange 2010 或 2007 Edge Transport server 在 Exchange 2013

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

Edge Transport Server 可在 Microsoft Exchange Server 2013 Service Pack 1 (SP1) 中取得。不過，您可以繼續使用周邊網路中部署的現有 Exchange Server 2007 或 Exchange Server 2010 Edge Transport Server。或者，對於新的或升級的 Exchange 2007 組織，您可以在周邊網路中安裝新的 Exchange 2010 或 Exchange 2013 Edge Transport Server。

以下是您必須知道的資訊：

  - Exchange 2007 或 Exchange 2010 邊際傳輸伺服器應該連線到集線傳輸伺服器。在 Exchange 2013 中，傳輸服務存在於信箱伺服器。因此，信箱伺服器上的傳輸服務與邊際傳輸伺服器之間存在網際網路郵件流量，能夠有效略過 Exchange 2013 用戶端存取伺服器。

  - 您可以讓 Exchange 2007 或 Exchange 2010 Edge Transport Server 訂閱僅包含 Exchange 2013 伺服器的 Active Directory 站台。您可以在獨立 Exchange 2013 Mailbox Server 上，或是在 Mailbox Server 與 Client Access Server 安裝於同一部電腦的伺服器上，匯入 Edge 訂閱檔案並執行 EdgeSync。您無法在獨立的 Exchange 2013 Client Access Server 上匯入 Edge 訂閱檔案或執行 EdgeSync。

  - 在 Exchange 2007 組織中部署新 Exchange 2010 或 Exchange 2013 Edge Transport Server 的程序基本上與舊版 Exchange 相同。不過，在 Hub Transport Server 上執行的任何程序必須在 Exchange 2013 中的信箱伺服器上執行。程序如下：
    
      - [設定網際網路郵件流程透過訂閱的 Edge Transport Server](https://go.microsoft.com/fwlink/p/?linkid=275859)
    
      - [設定 Edge Transport Server 和 Hub Transport Server 而不使用 EdgeSync 之間的郵件流程](https://go.microsoft.com/fwlink/p/?linkid=276661)

