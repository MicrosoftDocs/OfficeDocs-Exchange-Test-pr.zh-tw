---
title: '啟動及停止 IMAP4 服務: Exchange 2013 Help'
TOCTitle: 啟動及停止 IMAP4 服務
ms:assetid: a52db4bd-69a6-47b2-acf3-d9d8571c7a87
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124022(v=EXCHG.150)
ms:contentKeyID: 50473920
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟動及停止 IMAP4 服務

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-05_

依預設、 兩個 IMAP4 服務、 Microsoft Exchange IMAP4 服務和 Microsoft Exchange IMAP4 後端服務未執行MicrosoftExchange Server 2013的電腦上啟動。您必須先啟動允許您的電子郵件用戶端連線至 Exchange 使用 IMAP4 這兩項服務。這些服務會執行時， Exchange 2013接受不安全的 IMAP4 用戶端通訊連接埠 143 和透過連接埠 993 使用 Secure Sockets Layer (SSL)。

正在執行的用戶端存取伺服器角色的Exchange 2013電腦上執行 Microsoft Exchange IMAP4 服務。在執行 Mailbox server role Exchange 2013電腦上執行 Microsoft Exchange IMAP4 後端服務。在環境中的用戶端存取和信箱伺服器角色在同一部電腦執行，您可以管理兩種服務都在同一部電腦上。

如需 POP3 與 IMAP4 的詳細資訊，請參閱 [Exchange Server 2013 中的 POP3 和 IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 2 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [用戶端和行動裝置權限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主題中的「POP3 和 IMAP4 權限」一節。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 您要執行的工作

## 使用 Microsoft 管理主控台服務嵌入式管理單元來啟動或停止 IMAP4 服務

若要啟動 IMAP4 服務：

1.  在電腦上執行的用戶端存取伺服器角色，按一下 \[**開始\]**、 指向 \[**程式\]**、 指向 \[**系統管理工具**\] 及 \[**服務**。以滑鼠右鍵按一下 \[ **Microsoft Exchange IMAP4**\] 和 \[**啟動**。

2.  在執行 Mailbox server role 的電腦，按一下 \[**開始\]**、 指向 \[**程式\]**、 指向 \[**系統管理工具**\] 及 \[**服務**。以滑鼠右鍵按一下 \[ **Microsoft Exchange IMAP4 後端**，並按一下 \[**開始**。

若要停止 IMAP4 服務：

1.  在電腦上執行的用戶端存取伺服器角色，按一下 \[**開始\]**、 指向 \[**程式\]**、 指向 \[**系統管理工具**\] 及 \[**服務**。以滑鼠右鍵按一下 \[ **Microsoft Exchange IMAP4**\] 和 \[**停止**。

2.  在執行 Mailbox server role 的電腦，按一下 \[**開始\]**、 指向 \[**程式\]**、 指向 \[**系統管理工具**\] 及 \[**服務**。以滑鼠右鍵按一下 \[ **Microsoft Exchange IMAP4 後端**，並再按一下 \[**停止**\]。

## 使用命令介面來啟動或停止 IMAP4 服務

若要啟動 IMAP4 服務：

1.  在執行用戶端存取伺服器角色的電腦上，從命令介面執行以下命令，以啟動 Microsoft Exchange IMAP4 服務。
    
        Start-service msExchangeIMAP4

2.  在執行信箱伺服器角色的電腦上，從命令介面執行以下命令，以啟動 Microsoft Exchange IMAP4 後端服務。
    
        Start-service msExchangeIMAP4BE

若要停止 IMAP4 服務：

1.  在執行用戶端存取伺服器角色的電腦上，從命令介面執行以下命令，以停止 Microsoft Exchange IMAP4 服務。
    
        Stop-service msExchangeIMAP4

2.  在執行信箱伺服器角色的電腦上，從命令介面執行以下命令，以停止 Microsoft Exchange IMAP4 後端服務。
    
        Stop-service msExchangeIMAP4BE

## 使用 net start 來啟動或停止 IMAP4 服務

若要啟動 IMAP4 服務：

1.  在執行用戶端存取伺服器角色的電腦上，於命令提示字元中執行以下命令，以啟動 Microsoft Exchange IMAP4 服務。
    
        net start msExchangeIMAP4

2.  在執行信箱伺服器角色的電腦上，於命令提示字元中執行以下命令，以啟動 Microsoft Exchange IMAP4 後端服務。
    
        net start msExchangeIMAP4BE

若要停止 IMAP4 服務：

1.  在執行用戶端存取伺服器角色的電腦上，於命令提示字元中執行以下命令，以停止 Microsoft Exchange IMAP4 服務。
    
        Net Stop MSExchangeIMAP4

2.  在執行信箱伺服器角色的電腦上，於命令提示字元中執行以下命令，以停止 Microsoft Exchange IMAP4 後端服務。
    
        Net Stop MSExchangeIMAP4BE

## 如何才能了解這是否正常運作？

1.  在Exchange用戶端存取伺服器上，開啟 \[Windows 工作管理員\]。在 \[**服務**\] 索引標籤上**MSExchangeIMAP4**的狀態會顯示為**執行**Microsoft Exchange IMAP4 服務執行。

2.  在Exchange信箱伺服器上，開啟 \[Windows 工作管理員\]。在 \[**服務**\] 索引標籤上**MSExchangeIMAP4BE**的狀態會顯示為**執行**Microsoft Exchange IMAP4 後端服務執行。

