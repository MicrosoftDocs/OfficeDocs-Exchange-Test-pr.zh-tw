---
title: 'DNS 資料庫中找不到本機電腦的主機記錄: Exchange 2013 Help'
TOCTitle: DNS 資料庫中找不到本機電腦的主機記錄
ms:assetid: 2f18cb65-29fe-4b72-8d68-52fd503d5673
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.hostrecordmissing(v=EXCHG.150)
ms:contentKeyID: 50472914
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# DNS 資料庫中找不到本機電腦的主機記錄

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2016-12-09_

因為在網域名稱系統 (DNS) 資料庫中找不到此電腦的主機 (A) 記錄，所以 Microsoft Exchange Server 2013 安裝程式無法繼續。

Exchange 2013 安裝程式需要本機電腦具有一個已向網域的授權 DNS 資料庫註冊的有效主機 (A) 記錄。

Exchange 依賴 DNS 主機 (A) 記錄來取得下一個內部或外部目的伺服器的 IP 位址。

若要解決此問題：

  - 請確認本機的 TCP/IP 設定指向正確的 DNS 伺服器。如需詳細資訊，請參閱[設定 TCP/IP 設定](https://go.microsoft.com/fwlink/p/?linkid=108281)。

  - 若要驗證的主機 (A) 記錄存在 DNS 伺服器上使用 Nslookup.exe。如需詳細資訊，請參閱[驗證資源記錄存在於 DNS](https://go.microsoft.com/fwlink/?linkid=63001)。

如需 DNS 名稱解析、疑難排解及主機 (A) 記錄的相關資訊，請參閱：

  - [DNS 疑難排解](https://go.microsoft.com/fwlink/p/?linkid=294828)

  - [管理資源記錄](https://go.microsoft.com/fwlink/p/?linkid=294829)

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

找到您要的資訊了嗎？請撥冗[提供您的意見](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac)讓我們知道您需要什麼資訊。

