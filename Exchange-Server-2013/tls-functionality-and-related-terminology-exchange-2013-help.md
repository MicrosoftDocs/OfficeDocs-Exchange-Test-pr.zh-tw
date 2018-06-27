---
title: 'TLS 功能及相關術語: Exchange 2013 Help'
TOCTitle: TLS 功能及相關術語
ms:assetid: 294ba2a9-892d-4a90-beec-9d298426b5f4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb430753(v=EXCHG.150)
ms:contentKeyID: 52062527
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# TLS 功能及相關術語

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2014-06-18_

Microsoft Exchange Server 2013 提供管理功能及其他增強功能，可改善傳輸層安全性 (TLS) 的整體管理。使用此功能時，需要了解一些 TLS 相關功能。部分術語及概念適用於多個 TLS 相關功能。在本主題中，每個功能都提供了簡短說明，可協助您了解 TLS 及網域安全性功能集的部分相關差異及一般術語：

  - **傳輸層安全性   **TLS 是標準的通訊協定，用以提供網際網路或內部網路的安全 Web 通訊。它可讓用戶端驗證伺服器，或選擇性地讓伺服器驗證用戶端。它也藉由加密通訊，提供了安全的通道。TLS 是最新版本的安全通訊端層 (SSL) 通訊協定。

  - **相互 TLS**   相互 TLS 驗證與 TLS 不同，因為 TLS 通常會經過部署。一般而言，部署 TLS 後，TLS 只會以加密形式提供機密性。傳送端與接收端之間不會進行任何驗證。此外，有時候部署 TLS 後，只會驗證接收伺服器。這類 TLS 部署常見於實作 TLS 的 HTTP。這種只驗證接收伺服器的實作就是 SSL。
    
    利用相互 TLS 驗證，每部伺服器均可透過驗證另一部伺服器所提供的憑證，來確認該伺服器的身分。在此情況下，郵件是在 Exchange 2013 環境中透過驗證的連線接收自外部網域，Microsoft Outlook 會顯示 **\[安全的網域\]** 圖示。

  - **網域安全性**   網域安全性是一組功能，例如憑證管理、連接器功能，以及使相互 TLS 功能成為可管理及有用技術的 Outlook 用戶端行為。當輸出電子郵件透過 Exchange 2013 Client Access Server 傳送時，並不支援網域安全性。

  - **隨機 TLS**   在 Exchange 2013 中，安裝程式會建立自我簽署憑證。預設會啟用 TLS。這可讓任何傳送系統將傳至 Exchange 的傳入 SMTP 工作階段加密。依據預設，Exchange 2013 也會針對所有遠端連線嘗試 TLS。

  - **直接信任**   預設會驗證及加密 Edge Transport Server 與 Mailbox Server 之間的所有流量。而且，驗證及加密的基礎機制為相互 TLS。Exchange 2013 不使用 X.509 驗證，改為使用直接信任來驗證憑證。直接信任表示 Active Directory 中有憑證存在，或 Active Directory 輕量型目錄服務 (AD LDS) 已驗證該憑證。Active Directory 被視為是信任儲存機制。使用直接信任時，憑證是自行簽署或由憑證授權單位簽署都無所謂。當您為 Exchange 組織訂閱 Edge Transport Server 時，Edge 訂閱即會在 Active Directory 中發佈 Edge Transport Server 憑證，讓 Mailbox Server 進行驗證。Microsoft Exchange EdgeSync 服務會使用 Mailbox Server 憑證組來更新 AD LDS，讓 Edge Transport Server 進行驗證。

