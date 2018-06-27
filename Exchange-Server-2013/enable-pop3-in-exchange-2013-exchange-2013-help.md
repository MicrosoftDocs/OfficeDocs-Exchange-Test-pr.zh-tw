---
title: '在 Exchange 2013 中啟用 POP3: Exchange 2013 Help'
TOCTitle: 啟用 POP3
ms:assetid: e226a5f1-429d-4046-b925-da6cc151709e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124934(v=EXCHG.150)
ms:contentKeyID: 50474418
ms.date: 01/04/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 在 Exchange 2013 中啟用 POP3

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2017-03-28_

了解如何在 Exchange 2016 中使用 Microsoft Management Console (MMC) 或 Exchange 管理命令介面 (EMS) 啟用 POP3 用戶端連線。

安裝 Exchange Server 2016 時，並不會啟動 POP3 用戶端連線。若要啟用 POP3 用戶端連線，您需要啟動兩個 POP3 服務：Microsoft Exchange POP3 服務和 Microsoft Exchange POP3 後端服務。在您啟用 POP3 時，Exchange 2016 會使用安全通訊端層 (SSL) 在通訊埠 110 與通訊埠 995 上接受不安全的 POP3 用戶端通訊。

您在執行信箱伺服器角色的同一部 Exchange 2016 電腦上管理 POP3 和 POP3 後端服務。在 Exchange 2016 中，用戶端存取服務是信箱伺服器角色的一部分，因此您不必再個別管理服務。

如需如何設定 POP3 及 IMAP4 的相關資訊，請參閱＜[Exchange Server 2013 中的 POP3 和 IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md)＞。

## 開始之前有哪些須知？

  - 預估完成時間： 2 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱[用戶端和行動裝置權限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主題中的「POP3 和 IMAP4 權限」一節。

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

## 使用 Microsoft Management Console (MMC) 以啟用 POP3

在電腦上執行信箱伺服器角色：

1.  在 \[服務\] 嵌入式管理單元的主控台樹狀目錄內，按一下 \[服務 (本機)\]。

2.  在結果窗格中的 \[Microsoft Exchange POP3\] 上按一下滑鼠右鍵，然後按一下 \[內容\]。

3.  在結果窗格中的 \[Microsoft Exchange POP3 後端\] 上按一下滑鼠右鍵，然後按一下 \[內容\]。

4.  在 \[一般\] 索引標籤的 \[啟動類型\] 下，選取 \[自動\]，然後按一下 \[套用\]。

5.  在 \[服務狀態\] 下，按一下 \[啟動\]，然後按一下 \[確定\]。

## 使用 Exchange 管理命令介面 來啟用 POP3

在電腦上執行信箱伺服器角色：

1.  設定自動啟動 Microsoft Exchange POP3 服務。
    
        Set-service msExchangePOP3 -startuptype automatic

2.  啟動 Microsoft Exchange POP3 服務。
    
        Start-service msExchangePOP3

3.  設定自動啟動 Microsoft Exchange POP3 後端服務。
    
        Set-service msExchangePOP3BE -startuptype automatic

4.  啟動 Microsoft Exchange POP3 後端服務。
    
        Start-service msExchangePOP3BE

## 如何知道這是否正常運作？

在 Exchange 2016 信箱伺服器上，開啟 \[Windows 工作管理員\]。如果啟用了 POP3，則在 \[服務\] 索引標籤上，**MSExchangePOP3** 和 **MSExchangePOP3BE** 的狀態將顯示為**執行中**。

