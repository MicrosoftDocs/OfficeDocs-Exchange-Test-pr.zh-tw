---
title: 'Exchange 2013 憑證管理 UI: Exchange 2013 Help'
TOCTitle: Exchange 2013 憑證管理 UI
ms:assetid: 8975848d-07f0-4643-9eac-20aece69945f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ984582(v=EXCHG.150)
ms:contentKeyID: 52062570
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013 憑證管理 UI

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-04-21_

管理 Exchange Server 部署中的憑證是其中一個最重要的管理工作。確定已適當安裝和設定憑證，是為企業提供郵件安全傳遞基礎結構的關鍵。在 Exchange 2010 中，Exchange 管理主控台 (EMC) 是管理憑證的主要方法。在 Exchange 2013 中，憑證管理功能是透過 Exchange 管理主控台 (EAC) 這個新的 Exchange 2013 管理使用者介面提供。在 Exchange 2013 中，重點是放在減少系統管理員必須管理的憑證數量、減少系統管理員需與憑證互動的機會，以及允許透過集中位置來管理憑證。

## Client Access Server 憑證

Exchange 2013 中的 Client Access Server 是一部不留狀態、體積輕巧的伺服器，專門設計成接受傳入用戶端連線，並將之 Proxy 處理至正確的 Mailbox Server。Client Access Server 上的 Exchange 憑證管理 UI 可以協助您進行各種工作 (包括要求新的憑證，以及更新過期或即將過期的憑證)。

## 了解憑證管理 UI

您可以在 EAC 中依序選取 \[伺服器\] 和 \[憑證\] 來存取 Exchange 憑證管理 UI。使用管理 UI，您可以執行下列動作：

  - **建立新憑證**   選取 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示") 會啟動 \[新增 Exchange 憑證\] 精靈。

  - **編輯現有憑證**   在有效憑證上選取 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示") 可讓您查看憑證的屬性頁面。

  - **刪除憑證**   如果在選取憑證時選取 \[刪除\]![刪除圖示](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "刪除圖示")，則會啟動刪除確認對話方塊。

  - **執行其他動作**   選取 \[更多選項\]![更多選項圖示](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "更多選項圖示") 可讓您匯出或匯入憑證。如果您想要匯出憑證，則憑證必須有效。

## 憑證到期

在舊版 Microsoft Exchange 中，您無法輕鬆看見數位憑證的到期日為何。在 Exchange 2013 中，任何 Exchange 2013 Client Access Server 上所儲存的憑證即將到期時，通知中心會顯示警告。

## Mailbox Server 憑證

Exchange 2010 與 Exchange 2013 之間的其中一項重要差異是 Exchange 2013 Mailbox Server 上使用的憑證是自我簽署憑證。因為所有用戶端都是透過 Exchange 2013 Client Access Server 連線到 Exchange 2013 Mailbox Server，所以您唯一需要管理的憑證就是 Client Access Server 上的憑證。Client Access Server 會自動信任 Mailbox Server 上的自我簽署憑證，因此，只要 Client Access Server 有來自 Windows 憑證授權單位 (CA) 或信任之協力廠商的非自我簽署憑證，用戶端就不會收到有關自我簽署憑證不受信任的警告。沒有工具或指令程式可用來管理 Mailbox Server 上的自我簽署憑證。正確安裝伺服器之後，您應該永不需要擔心 Mailbox Server 上的憑證。

## 自我簽署憑證到期

Exchange 2013 Mailbox Server 上安裝的自我簽署憑證預設會在安裝那天開始算起的五年後到期。

## 憑證指令程式

您可以在 Exchange Client Access Server 上使用下列指令程式管理數位憑證：

  - Import-ExchangeCertificate   此指令程式用來將憑證匯入至伺服器。您可以匯入 CA 簽署的憑證 (以完成擱置的憑證簽署要求 (CSR)) 或具有私密金鑰的憑證 (PKCS \#12 檔案，一般具有副檔名 .pfx，先前是與私密金鑰一起從伺服器匯出)。

  - Remove-ExchangeCertificate   此指令程式用來從伺服器中移除憑證。

  - Enable-ExchangeCertificate   此指令程式用來將服務指派給憑證。

  - Get-ExchangeCertificate   此指令程式用來根據各種準則來擷取 Exchange 憑證。

  - New-ExchangeCertificate   此指令程式用來建立新的自我簽署憑證或 CSR。

