---
title: 'Exchange Remote Connectivity Analyzer: Exchange 2013 Help'
TOCTitle: Exchange Remote Connectivity Analyzer
ms:assetid: dd26698e-d00c-47f5-a7aa-c3894fe86c75
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ff701693(v=EXCHG.150)
ms:contentKeyID: 50474396
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange Remote Connectivity Analyzer

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-09-22_

Microsoft Exchange Remote Connectivity Analyzer (ExRCA) 可協助您確定已正確設定 Exchange 伺服器的連線。如果您遇到問題，它也可以協助您尋找並修正這些問題。ExRCA 網站可以執行測試來檢查是否有 MicrosoftExchange ActiveSync、Exchange Web 服務、MicrosoftOutlook 和網際網路電子郵件連線。

## 遠端連線分析程式測試

您可以對 ExRCA 執行幾個測試。下列測試在 Exchange 2007 和更新版本上執行：

  - Exchange ActiveSync

  - Exchange Web 服務

  - Outlook

  - 網際網路電子郵件

## Exchange ActiveSync 測試

您可以針對 Exchange ActiveSync 執行下列測試：

  - **Exchange ActiveSync：**這項測試會使用 Exchange ActiveSync 模擬行動裝置用來連線到 Exchange 伺服器的步驟。

  - **Exchange ActiveSync 自動探索：**這會逐步完成 Exchange ActiveSync 裝置用來向自動探索服務取得設定的步驟。

## Exchange Web 服務連線測試

Exchange Web 服務測試檢查許多Exchange Web 服務的設定。您可以執行下列測試Exchange Web 服務：

  - **同步處理、通知、可用性和自動回覆：**這些測試會逐步完成許多基本 Exchange Web 服務工作來確認這些工作運作中。這適用於想要疑難排解使用 Entourage EWS 或其他 Web 服務用戶端進行外部存取權的 IT 系統管理員。

  - **服務帳戶存取 (開發人員)：**這項測試會驗證服務帳戶是否可以存取指定的信箱、在其中建立和刪除項目，以及透過 Exchange 模擬來存取信箱。這項測試主要由應用程式開發人員用來測試是否可以使用替代認證來存取信箱。

## Microsoft Office Outlook 連線測試

您可以針對 Outlook 連線執行下列測試：

  - **Outlook 無所不在 (RPC over HTTP)：**這項測試會逐步完成 Outlook 用來透過 Outlook 無所不在 (RPC over HTTP) 連線的步驟。

  - **Outlook 自動探索：**這項測試會逐步完成 Outlook 用來向自動探索服務取得設定的步驟。這項測試並不會實際連線到信箱。

## 網際網路電子郵件測試

您可以針對網際網路電子郵件執行下列測試：

  - **輸入 SMTP** **電子郵件：**這項測試會逐步完成網際網路電子郵件伺服器用來將輸入 SMTP 電子郵件傳送至網域的步驟。

  - **輸出 SMTP 電子郵件：**這項測試會檢查您的輸出 IP 位址中是否有特定需求。這包括反向 DNS、寄件者識別碼和 RBL 檢查。

  - **POP 電子郵件：**這項測試會逐步完成電子郵件用戶端用來使用 POP3 連線到信箱的步驟。

  - **IMAP 電子郵件：**這項測試會逐步完成電子郵件用戶端用來使用 IMAP 連線到信箱的步驟。

