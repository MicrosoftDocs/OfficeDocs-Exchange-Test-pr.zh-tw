---
title: '主要的 DNS 伺服器無法受到 contacted_PrimaryDNSTestFailed: Exchange 2013 Help'
TOCTitle: 主要的 DNS 伺服器無法受到 contacted_PrimaryDNSTestFailed
ms:assetid: 5b39cb64-c8f1-4fd3-843b-ecd23f99fe3a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.primarydnstestfailed(v=EXCHG.150)
ms:contentKeyID: 50473267
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 主要的 DNS 伺服器無法受到 contacted\_PrimaryDNSTestFailed

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2016-12-09_

此主題中的內容尚未針對 Microsoft Exchange Server 2013 進行更新。在更新之前，可能還是適用於 Exchange 2013。如果您仍然需要幫助，請查看下方的社群資源。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft® Exchange Server 2007 安裝程式無法繼續因為無法建立與主要網域名稱系統 (DNS) 伺服器通訊。

Exchange 2007 的安裝程式需要與網域的代表性 DNS 資料庫通訊本機電腦。

Microsoft Exchange 取決於其下的內部或外部目的地伺服器的 IP 位址解析 DNS。

與主要的 DNS 伺服器的通訊可以會基於下列原因而失敗：

  - 本機 TCP/IP 設定未指向正確的 DNS 伺服器。

  - DNS 伺服器會因為網路失敗或其他原因而不向下或無法連線。

若要解決此問題：

  - 請確認本機的 TCP/IP 設定指向正確的 DNS 伺服器。

若要確認本機 TCP/IP 設定

1.  請檢閱本機 TCP/IP 設定：
    
    如需詳細資訊，請參閱"設定為使用 DNS TCP/IP"([https://go.microsoft.com/fwlink/?LinkId=68094](https://go.microsoft.com/fwlink/?linkid=68094))。

<!-- end list -->

  - 確認 DNS 伺服器正在執行，可連絡。

若要確認 DNS 伺服器正在執行，而且可連絡

1.  確認 DNS 伺服器正在執行依照一或多個下列檢查：
    
      - 查看 DNS 伺服器的狀態從 DNS 管理計畫的 DNS 伺服器上。
    
      - 重新啟動 DNS 伺服器。
        
        如需詳細資訊，請參閱"開始、 停止、 暫停、 或重新啟動 DNS 伺服器"([https://go.microsoft.com/fwlink/?LinkId=62999](https://go.microsoft.com/fwlink/?linkid=62999))。
    
      - 使用**nslookup**命令來確認 DNS 伺服器回應速度。
        
        如需詳細資訊，請參閱中的指示 「 確認 DNS 伺服器回應速度使用 nslookup 命令 」 ([https://go.microsoft.com/fwlink/?LinkId=63000](https://go.microsoft.com/fwlink/?linkid=63000))。

