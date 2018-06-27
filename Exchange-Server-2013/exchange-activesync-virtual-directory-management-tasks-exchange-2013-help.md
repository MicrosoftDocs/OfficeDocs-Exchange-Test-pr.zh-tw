---
title: 'Exchange ActiveSync 虛擬目錄的管理工作: Exchange 2013 Help'
TOCTitle: Exchange ActiveSync 虛擬目錄的管理工作
ms:assetid: f0b339b7-e184-4392-a133-20523183459d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb125170(v=EXCHG.150)
ms:contentKeyID: 50474561
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange ActiveSync 虛擬目錄的管理工作

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-05_

您可以管理數個Exchange ActiveSync應用程式中設定Exchange Server 2013透過Exchange ActiveSync虛擬目錄。虛擬目錄用來允許存取像是Exchange ActiveSync的 web 應用程式的網際網路資訊服務 (IIS)。您可以針對Exchange ActiveSync來管理虛擬目錄設定的一些包括驗證、 安全性及報告。

## Exchange ActiveSync 虛擬目錄設定

您可以在 Exchange ActiveSync 虛擬目錄上修改下列內容和設定：

  - **InternalURL** InternalURL 是內部用戶端可用來存取虛擬目錄的 URL。它通常是在格式 https://servername/Microsoft-Server-ActiveSync。例如，如果該伺服器的 NetBIOS 名稱為 Sequoia\] InternalURL 是 https://sequoia/Microsoft-Server-ActiveSync。

  - **ExternalURL** ExternalURL 是可用於外部用戶端存取虛擬目錄的 URL。此 URL 應該是可從內部網路之外存取。例如，您 ExternalURL 可能是 https://www.contoso.com/。

  - **驗證設定** 您可為 Exchange ActiveSync 虛擬目錄設定的兩個驗證方法是：基本驗證和用戶端憑證驗證。

