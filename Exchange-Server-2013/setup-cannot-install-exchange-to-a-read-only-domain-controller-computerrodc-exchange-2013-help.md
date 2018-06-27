---
title: '安裝程式無法以唯讀網域 controller_ComputerRODC 安裝 Exchange: Exchange 2013 Help'
TOCTitle: 安裝程式無法以唯讀網域 controller_ComputerRODC 安裝 Exchange
ms:assetid: 4934d755-65be-47e2-86b0-6ea1ab148a96
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.computerrodc(v=EXCHG.150)
ms:contentKeyID: 50473173
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 安裝程式無法以唯讀網域 controller\_ComputerRODC 安裝 Exchange

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2012-06-05_

此主題中的內容尚未針對 Microsoft Exchange Server 2013 進行更新。在更新之前，可能還是適用於 Exchange 2013。如果您仍然需要幫助，請查看下方的社群資源。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft Exchange Server 2007 安裝程式無法繼續安裝在目標電腦由於唯讀網域控制站 (RODC)。

唯讀網域控制站的 Windows Server 2008 Active Directory 的功能。RODC 是一種網域控制站安裝可以安裝在可能會有較低層級的實體安全性的遠端站台的選項。

Exchange 安裝程式需要寫入權限的目標安裝電腦。

若要解決此問題，請選取 \[不會指定為 RODC，目標安裝電腦並重新執行安裝程式。

