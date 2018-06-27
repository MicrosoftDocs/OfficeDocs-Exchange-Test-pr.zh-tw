---
title: '網域控制站會覆寫 Registry_ConfigDCHostNameMismatch 中設定: Exchange 2013 Help'
TOCTitle: 網域控制站會覆寫 Registry_ConfigDCHostNameMismatch 中設定
ms:assetid: 3aef5470-d510-4b59-a4b6-36d274a984ae
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.configdchostnamemismatch(v=EXCHG.150)
ms:contentKeyID: 50472894
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 網域控制站會覆寫 Registry\_ConfigDCHostNameMismatch 中設定

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2016-12-15_

此主題中的內容尚未針對 Microsoft Exchange Server 2013 進行更新。在更新之前，可能還是適用於 Exchange 2013。如果您仍然需要幫助，請查看下方的社群資源。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft Exchange Server 2007 安裝程式無法繼續因為嘗試使用指定的網域控制站失敗。在網域控制站已靜態對應登錄中。

Exchange 2007 的安裝程式需要在 setup 命令中指定的網域控制站比對網域控制站已靜態對應使用登錄覆寫。

若要一次解決這個問題，執行安裝程式，指定的靜態對應的網域控制站**/DomainController: \<***FQDN of thestatically mapped domain controller***\>**參數。

如需 DSAccess 與目錄服務偵測，請參閱 Microsoft 知識庫文章 250570，"目錄服務伺服器偵測及 DSAccess 使用量"([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=250570](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=250570)) 的詳細資訊。

