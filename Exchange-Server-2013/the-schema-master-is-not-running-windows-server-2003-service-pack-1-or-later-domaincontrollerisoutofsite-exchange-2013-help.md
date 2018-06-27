---
title: 'Windows Server 2003 Service Pack 1 或 later_DomainControllerIsOutOfSite 的架構主機未執行: Exchange 2013 Help'
TOCTitle: Windows Server 2003 Service Pack 1 或 later_DomainControllerIsOutOfSite 的架構主機未執行
ms:assetid: 5edbe0b8-7610-4a52-aaaa-38c6a99e7e53
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.domaincontrollerisoutofsite(v=EXCHG.150)
ms:contentKeyID: 50473309
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Windows Server 2003 Service Pack 1 或 later\_DomainControllerIsOutOfSite 的架構主機未執行

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2016-12-09_

此主題中的內容尚未針對 Microsoft Exchange Server 2013 進行更新。在更新之前，可能還是適用於 Exchange 2013。如果您仍然需要幫助，請查看下方的社群資源。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft Exchange Server 2007 安裝程式無法繼續因為網域控制站指派 Active Directory 目錄服務架構主機角色，也稱為彈性單一主機操作 (FSMO) 未執行 Microsoft Windows Server 2003 Service Pack 1 (SP1) 或更新版本。

Exchange 2007 的安裝程式需要網域控制站中做為結構描述 FSMO 執行 Windows Server 2003 SP1 或更新版本。

FSMO 控制所有的更新和修改的 Active Directory 結構描述。

若要解決這個問題，請勿一或多個動作：

  - 升級至 Windows Server 2003 SP1 或更新版本的 FSMO 網域控制站並重新執行 Microsoft Exchange 安裝程式。

  - 如果執行 Microsoft Windows Server 2003 Service Pack 1 (SP1) 或更新版本的 Exchange 組織中的 FSMO 網域控制站，請使用 /domaincontroller 參數指向該 FSMO 網域控制站執行 Exchange 2007 安裝程式：
    
    \[*/DomainController*或*/dc\<FQDN of domain controller\>*\]
    
    使用*/DomainController*參數來指定讀寫至Active Directory在安裝期間所使用之網域控制站。您可以使用 NetBIOS 或完整的網域名稱 (FQDN) 格式。

若要取得最新 service pack 的 Windows Server 2003，請參閱"Windows Server TechCenter"([https://go.microsoft.com/fwlink/?LinkId=45315](https://go.microsoft.com/fwlink/?linkid=45315))。

如需 Exchange Server 2007 安裝參數的詳細資訊，請參閱 Exchange Server 2007 產品文件中的 「 如何以安裝 Exchange 2007 在自動模式 」 ([https://go.microsoft.com/fwlink/?LinkId=86476](https://go.microsoft.com/fwlink/?linkid=86476))。

