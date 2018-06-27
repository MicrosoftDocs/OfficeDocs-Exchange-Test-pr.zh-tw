---
title: '傳輸高可用性: Exchange 2013 Help'
TOCTitle: 傳輸高可用性
ms:assetid: e9ec6d05-f441-4cca-8592-8f7469948299
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ657506(v=EXCHG.150)
ms:contentKeyID: 50474508
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 傳輸高可用性

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-15_

在 Microsoft Exchange Server 2013 中，傳輸高可用性負責在成功傳遞郵件之前和之後，保留郵件的備援副本。Exchange 2013 改進了 Exchange Server 2010 推出的傳輸高可用性功能 (例如陰影備援和傳輸暫放)，協助確保郵件在傳輸途中不會遺失。

以下摘要說明 Exchange 2013 的主要傳輸高可用性改進功能：

  - 陰影備援另一部伺服器上建立郵件的重複複本郵件會接受或認可之前。傳送伺服器支援 」 或 「 缺少的陰影備援支援為不相關。

  - 陰影備援識別資料庫可用性群組 (Dag) 和 Active Directory 站台作為傳輸高可用性界限。這可減少可以保留備援副本的郵件，並不必要的多餘郵件維護流量 across DAGs 或 Active Directory 伺服器的數目的網站。
    
    如需詳細資訊，請參閱[陰影備援](shadow-redundancy-exchange-2013-help.md)。

  - 傳輸暫放已改善並立即命名為*安全網*。安全網儲存已成功處理的 Mailbox server 上的傳輸服務的郵件。安全網最適用於信箱伺服器的 DAG，但安全網也適用於多個信箱伺服器相同的 Active Directory 站台的 DAG 不屬於。

  - 另一部伺服器上安全網本身是現在進行變得多餘。這是可避免在Exchange 2013、 失敗的單一資料點的重要，因為的傳輸服務與信箱資料庫兩者位於 Mailbox server 上。
    
    如需詳細資訊，請參閱[安全網](safety-net-exchange-2013-help.md)。

下圖提供傳輸高可用性在 Exchange 2013 中運作方式的高層次概述。

![傳輸高可用性概觀](images/JJ657506.88f2284d-8afe-4c8f-94a6-cd4c097a55d8(EXCHG.150).gif "傳輸高可用性概觀")

1.  名為 Mailbox01 的Exchange 2013信箱伺服器收到郵件的 SMTP 伺服器的傳輸高可用性界限之外。*傳輸高可用性界限*為 DAG 或非 DAG 環境中的 Active Directory 站台。郵件無法來自協力廠商 SMTP 伺服器、 從網際網路 SMTP 伺服器代理透過用戶端存取伺服器，或從另一部 Exchange 2013 伺服器。

2.  之前認可收到郵件，Mailbox01 起始至名為傳輸高可用性圖形界限內的 mailbox03 等其他Exchange 2013 Mailbox server 的新 SMTP 工作階段並 mailbox03 等之郵件的陰影複製。DAG 環境中遠端 Active Directory 站台的陰影伺服器是慣用。Mailbox01 是保留主要郵件的主要伺服器及 mailbox03 等是保留陰影郵件的陰影伺服器。

3.  Mailbox01 上的傳輸服務會處理主要郵件。
    
    1.  在這個範例中，收件者信箱位於 Mailbox01 上，所以傳輸服務會將郵件傳輸至本機信箱傳輸服務。
    
    2.  信箱傳輸服務再將郵件傳遞到本機信箱資料庫。
    
    3.  Mailbox01 佇列表示已成功處理主要的訊息，而且 Mailbox01 移動主要郵件複製到本機主要 Safety Net 的 mailbox03 等的捨棄狀態。郵件佇列中相同的佇列資料庫之間移動的附註。

4.  Mailbox03 會定期輪詢 Mailbox01 關於主要郵件的捨棄狀態。

5.  當 mailbox03 等決定 Mailbox01 成功處理主要訊息時、 mailbox03 等移動陰影郵件到本機陰影安全網。郵件佇列中相同的佇列資料庫之間移動的附註。

郵件會保留在主要 Safety Net 及陰影 Safety Net 直到郵件到期根據可設定的逾時值。如果信箱資料庫容錯移轉發生郵件到期之前，在 Mailbox01 主要 Safety Net 重新提交郵件。如果 Mailbox01 無法使用，在 mailbox03 等陰影 Safety Net 是透過並重新提交郵件。

## 用戶端存取伺服器上前端傳輸服務的郵件備援

用戶端存取伺服器有無訊息佇列。它會使用接受傳入 SMTP 連線和 proxy 他們傳輸服務的 Mailbox server Front End Transport 服務無狀態的 proxy 伺服器。Front End Transport 服務持續傳送伺服器 SMTP 工作階段開啟主要的郵件傳輸至 Mailbox server 上的傳輸服務以及陰影複製的郵件進行傳輸高可用性界限內之不同信箱伺服器上的傳輸服務時。只有主要的郵件和陰影郵件已成功建立之後，資料 SMTP 命令結尾會傳送回透過用戶端存取伺服器傳送的 SMTP 伺服器。

