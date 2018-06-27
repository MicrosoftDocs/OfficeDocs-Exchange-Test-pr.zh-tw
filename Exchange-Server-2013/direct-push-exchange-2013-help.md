---
title: 'Direct Push: Exchange 2013 Help'
TOCTitle: Direct Push
ms:assetid: 373c1629-3d4b-4828-b014-9e103de4ef25
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa997252(v=EXCHG.150)
ms:contentKeyID: 50472853
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Direct Push

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2012-07-11_

Direct Push 是內建於 Microsoft Exchange Server 2013功能。Direct Push 持續在行動裝置目前透過行動電話或無線網路連線。它會通知行動裝置時新內容已準備好要同步處理。

**目錄**

概觀

Direct Push topology

Configuring Direct Push to work through your firewall

## 概觀

Direct Push 運作，行動裝置必須 Direct Push 能夠。這些裝置包括：

  - 所有版本的 Windows Phone

  - Microsoft Exchange ActiveSync 使用人所生產，且特別為與 Direct Push 相容所設計的行動電話

根據預設，在Exchange 2013啟用 Direct Push。行動裝置支援 Direct Push 問題存留期長的 HTTPS 要求執行Microsoft Exchange的伺服器。Exchange 伺服器監視使用者的信箱上的活動及如果有任何變更，例如新增或變更電子郵件、 行事曆、 連絡人或工作項目傳送至行動裝置的回應。如果 HTTPS 要求的週期內發生的變更， Exchange server 問題裝置，指出已發生變更和裝置應啟動同步處理Exchange伺服器回應。裝置然後發出此要求的伺服器。同步處理完成時，請重新啟動程序產生新的存留期長 HTTPS 要求。如此可確保該電子郵件、 行事曆、 連絡人及工作項目已傳送快速至行動裝置與一律同步與Exchange伺服器。

## Direct Push 拓撲

Direct Push 的運作方式如下：

1.  會設定為與Exchange 2013伺服器進行同步處理行動裝置問題 HTTPS 要求的伺服器。此要求稱為 PING。要求會告知通知裝置如果任何項目在下一個 15 分鐘中變更任何設定成同步處理\] 資料夾中的伺服器。否則，伺服器應傳回的 HTTP 200 OK 訊息。然後代表行動裝置。*Heartbeat 間隔*稱為 15 分鐘時間範圍。

2.  如果沒有項目變更 15 分鐘，伺服器就會傳回 HTTP 200 OK 的回應。行動裝置會收到此回應、 繼續活動 （又稱為*喚醒*），並再次發出其要求。這會重新啟動程序。

3.  如果任何項目變更或新項目送達 15 分鐘 heartbeat 間隔內，伺服器會傳送通知的行動裝置會將新的或變更的項目回應，並提供件新的或變更的項目所在的資料夾名稱。行動裝置會收到此回應之後，它會發出有新的或變更的項目資料夾同步處理要求。同步處理完成時，行動裝置發出新 PING 要求和透過啟動整個程序。

Direct Push 支援屆時 HTTPS 要求的網路狀況而定。如果電信業者網路的行動裝置或防火牆不支援屆時 HTTPS 要求、 HTTPS 要求已停止。下列步驟說明如何 Direct Push 運作的行動裝置電信業者網路發生 13 分的逾時值。

1.  在行動裝置問題 HTTPS 要求的伺服器。要求會告知通知裝置如果任何項目在下一個 15 分鐘中變更任何設定成同步處理\] 資料夾中的伺服器。否則，伺服器應傳回的 HTTP 200 OK 訊息。然後代表行動裝置。

2.  如果伺服器沒有回應在 15 分鐘後，行動裝置喚醒並結束 \[伺服器連線的網路逾時。裝置會重新發出 HTTPS 要求，但這次是它會使用活動訊號間隔時間 8 分鐘。

3.  8 分鐘後伺服器傳送 HTTP 200 OK 訊息。裝置會再嘗試發出新 HTTPS 要求已為 12 分鐘 heartbeat 間隔的伺服器以獲得較長的連線。

4.  4 分鐘後接收新的電子郵件和伺服器的回應會告知同步處理裝置 HTTPS 要求傳送。裝置同步處理和 HTTPS 要求具有活動訊號為 12 分鐘會重新發出。

5.  在 12 分鐘後如果沒有任何新增或變更的項目，伺服器會回應透過傳送 HTTP 200 OK 訊息。裝置喚醒並結束網路狀況支援 heartbeat 間隔時間 12 分鐘。裝置會再嘗試以重新簽發的 16 分鐘 heartbeat 間隔 HTTPS 要求取得較長的連線。

6.  16 分鐘後從伺服器接收無回應。裝置喚醒並結束網路狀況不支援的 16 分鐘 heartbeat 間隔。因為這個失敗直接發生之後，裝置嘗試 heartbeat 間隔時間增量值，它會結束 heartbeat 間隔已達到其最大限制。裝置然後發出因為這是最後一個成功 heartbeat 間隔已為 12 分鐘 heartbeat 間隔 HTTPS 要求。

行動裝置會嘗試使用網路支援的最長 heartbeat 間隔。這將延伸的裝置上的電池壽命並減少資料量會透過網路傳送。行動通信業者可以在行動裝置的登錄設定中指定的最大值、 最小，並初始活動訊號值。

## 將 Direct Push 設定成透過防火牆運作

為了讓 Direct Push 能穿過防火牆運作，您必須開放 TCP 連接埠 443。此連接埠為安全通訊端層 (SSL) 所需，且必須在網際網路與 Client Access Server 之間開放。

除了開啟連接埠上防火牆，以獲得最佳的 Direct Push 效能，您應該在您從 15 分鐘的預設值為 30 分鐘的防火牆增加的逾時值。HTTPS 要求的最大長度是由下列設定值決定：

  - 在控制從網際網路到 Client Access Server 之間流量的防火牆上可設定的逾時值上限

  - 由行動服務供應商設定的防火牆逾時值

