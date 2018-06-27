---
title: 'SMTP 位址格式不 Supported_SMTPAddressLiteral: Exchange 2013 Help'
TOCTitle: SMTP 位址格式不 Supported_SMTPAddressLiteral
ms:assetid: b8b55917-d81f-4c0a-ad65-7bb10ac58df8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.smtpaddressliteral(v=EXCHG.150)
ms:contentKeyID: 50474045
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# SMTP 位址格式不 Supported\_SMTPAddressLiteral

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2016-12-09_

此主題中的內容尚未針對 Microsoft Exchange Server 2013 進行更新。在更新之前，可能還是適用於 Exchange 2013。如果您仍然需要幫助，請查看下方的社群資源。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft Exchange Server 2007 與 Exchange Server 2010 安裝程式無法繼續因為指定的收件者原則使用不受支援的簡易郵件傳送通訊協定 (SMTP) 位址格式。

Exchange 2007 和 Exchange 2010 安裝程式需要的所有電子郵件地址原則所使用的 SMTP 位址不包含 IP 位址常值，例如： *user@\[10.10.1.1\]*。

若要解決此問題，變更收件者原則中的 SMTP 位址的值，讓它不包含常值的 IP 位址。取代為括號 (\[\]) 及常值的 IP 位址的數字 (10.10.1.1) 的網域名稱系統 (DNS) 命名格式，例如： *user@contoso.com*，，然後重新執行 Exchange 安裝程式。

如需管理 Exchange Server 2007 中的收件者原則的詳細資訊，請參閱 「 管理電子郵件地址原則 」 ([https://go.microsoft.com/fwlink/?LinkId=86653](https://go.microsoft.com/fwlink/?linkid=86653))。

如需管理 Exchange Server 2010 中的收件者原則的詳細資訊，請參閱 「 管理電子郵件地址原則 」 ([https://go.microsoft.com/fwlink/?LinkId=179519](https://go.microsoft.com/fwlink/?linkid=179519))。

