---
title: '啟用 Exchange 2016 的 IMAP4: Exchange 2013 Help'
TOCTitle: 啟用 Exchange 2016 的 IMAP4
ms:assetid: c1ae10dd-14da-4400-b38d-2aeafde8abe6
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124489(v=EXCHG.150)
ms:contentKeyID: 50474185
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟用 Exchange 2016 的 IMAP4

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-06-02_

了解如何啟用 IMAP4 用戶端連線中Exchange 2016使用 Microsoft Management Console (MMC) 或Exchange 管理命令介面 （EMS）。

當您安裝Exchange Server 2016時，並未啟用 IMAP4 用戶端連線。若要啟用 IMAP4 用戶端連線，您需要啟動兩個 IMAP 服務、 Microsoft Exchange IMAP4 服務和 Microsoft Exchange IMAP4 後端服務。當您啟用 IMAP4 時， Exchange 2016接受無安全性的 IMAP4 用戶端通訊連接埠 143 及透過連接埠 993 使用 Secure Sockets Layer (SSL)。

管理 IMAP4 和 IMAP4 後端伺服器上執行 Mailbox server role 的相同Exchange 2016電腦的服務。Exchange 2016，在用戶端存取服務讓您不再服務分開管理是信箱伺服器角色的一部分。

如需如何設定 POP3 和 IMAP4 的詳細資訊，請參閱[Exchange Server 2013 中的 POP3 和 IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 2 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [用戶端和行動裝置權限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主題中的 「 POP3 及 IMAP4 權限 」 一節。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 您要執行的工作

## 使用 Microsoft Management Console (MMC) 來啟用 IMAP4

在電腦上執行信箱伺服器角色：

1.  在 \[服務\] 嵌入式管理單元的主控台樹狀目錄內，按一下 \[服務 (本機)\]。

2.  在結果窗格中的 \[Microsoft Exchange IMAP4\] 上按一下滑鼠右鍵，然後按一下 \[內容\]。

3.  在結果窗格中的 \[Microsoft Exchange IMAP4 後端\] 上按一下滑鼠右鍵，然後按一下 \[內容\]。

4.  在 \[一般\] 索引標籤的 \[啟動類型\] 下，選取 \[自動\]，然後按一下 \[套用\]。

5.  在 \[服務狀態\] 下，按一下 \[啟動\]，然後按一下 \[確定\]。

## 若要啟用 IMAP4 使用Exchange 管理命令介面

在電腦上執行信箱伺服器角色：

1.  設定自動啟動 Microsoft Exchange IMAP4 服務。
    
        Set-service msExchangeIMAP4 -startuptype automatic

2.  啟動 Microsoft Exchange IMAP4 服務。
    
        Start-service msExchangeIMAP4

3.  設定自動啟動 Microsoft Exchange IMAP4 後端服務。
    
        Set-service msExchangeIMAP4BE -startuptype automatic

4.  啟動 Microsoft Exchange IMAP4 後端服務。
    
        Start-service msExchangeIMAP4BE

## 如何才能了解這是否正常運作？

在Exchange 2016信箱伺服器上，開啟 \[Windows 工作管理員\]。\[**服務**\] 索引標籤**MSExchangeIMAP4**和**MSExchangeIMAP4BE**狀態將會顯示為**執行**如果啟用 IMAP4。

