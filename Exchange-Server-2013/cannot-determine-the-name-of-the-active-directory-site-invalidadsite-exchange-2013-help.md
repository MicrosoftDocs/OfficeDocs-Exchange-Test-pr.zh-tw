---
title: '無法判斷 Active Directory site_InvalidADSite 的名稱: Exchange 2013 Help'
TOCTitle: 無法判斷 Active Directory site_InvalidADSite 的名稱
ms:assetid: ef96e077-08a0-4108-9f7d-0d61758abcd4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.invalidadsite(v=EXCHG.150)
ms:contentKeyID: 50474549
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 無法判斷 Active Directory site\_InvalidADSite 的名稱

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2016-12-09_

此主題中的內容尚未針對 Microsoft Exchange Server 2013 進行更新。在更新之前，可能還是適用於 Exchange 2013。如果您仍然需要幫助，請查看下方的社群資源。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft® Exchange Server 2007 安裝程式無法繼續因為此伺服器似乎不在屬於有效的 Active Directory® 目錄服務網站。

Microsoft Exchange 安裝程式需要用於安裝 Exchange 2007 的伺服器屬於有效的 Active Directory 站台。

若要解決此問題，請確認本機伺服器是有效的 Active Directory 站台成員並重新執行 Exchange Server 2007 安裝程式。

您可以使用**/DsGetSite**選項 Nltest.exe 命令列工具的驗證及顯示網站成員資格。如需詳細資訊，請參閱 「 Nltest.exe： NLTest 概觀 」 的 「 工具及設定集合中" *Windows Server 2003 的技術參考*([https://go.microsoft.com/fwlink/?LinkId=27734](https://go.microsoft.com/fwlink/?linkid=27734))。

如需 Active Directory 進行疑難排解的詳細資訊，請參閱 ＜"疑難排解 Active Directory 操作"中*Windows Server 2003： 作業*(<https://go.microsoft.com/fwlink/?linkid=68099>)。

