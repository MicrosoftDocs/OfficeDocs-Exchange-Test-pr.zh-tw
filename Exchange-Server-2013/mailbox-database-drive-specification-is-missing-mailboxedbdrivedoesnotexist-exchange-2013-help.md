---
title: '信箱資料庫的磁碟機規格是 missing_MailboxEDBDriveDoesNotExist: Exchange 2013 Help'
TOCTitle: 信箱資料庫的磁碟機規格是 missing_MailboxEDBDriveDoesNotExist
ms:assetid: 0e487aa1-3194-4a14-b255-a8b9f9afbf0e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.mailboxedbdrivedoesnotexist(v=EXCHG.150)
ms:contentKeyID: 50472563
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 信箱資料庫的磁碟機規格是 missing\_MailboxEDBDriveDoesNotExist

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2016-12-09_

此主題中的內容尚未針對 Microsoft Exchange Server 2013 進行更新。在更新之前，可能還是適用於 Exchange 2013。如果您仍然需要幫助，請查看下方的社群資源。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft® Exchange Server 2007 嚴重損壞修復安裝程式無法繼續因為嚴重損壞修復安裝程式無法存取之信箱資料庫中先前安裝的此伺服器使用的磁碟機規格。

相同信箱資料庫的磁碟機規格之前使用此伺服器會提供還原期間要求 Microsoft Exchange 嚴重損壞修復安裝程式。

若要解決此情況下，設定以符合原始的邏輯磁碟機設定與重新執行 Microsoft Exchange 嚴重損壞修復安裝程式的磁碟機。

指派或變更的磁碟機代號

1.  開啟 \[**電腦管理（本機）**\]。

2.  在主控台樹狀目錄中，按一下 \[**電腦管理 （本機）**\]、 \[**儲存**\] 及 \[**磁碟管理**。

3.  磁碟分割、 邏輯磁碟機或磁碟區，以滑鼠右鍵按一下\] 和 \[**變更磁碟機代號和路徑**。

4.  使用下列程序之一：
    
      - 若要指派的磁碟機代號，按一下 \[**新增**\]、 按一下您要使用的磁碟機代號，然後按一下 \[**確定\]**。
    
      - 若要修改的磁碟機代號請按一下該、 按一下 \[**變更**\]、 按一下您要使用的磁碟機代號，然後按一下 \[**確定\]**。

如需如何指派磁碟機代號的詳細資訊，查看 」 指派、 變更或移除的磁碟機代號"([https://go.microsoft.com/fwlink/?LinkId=66764](https://go.microsoft.com/fwlink/?linkid=66764))。

