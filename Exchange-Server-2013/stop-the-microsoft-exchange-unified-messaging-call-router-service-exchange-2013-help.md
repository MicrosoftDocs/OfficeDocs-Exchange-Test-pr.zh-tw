---
title: '停止 Microsoft Exchange Unified Messaging Call Router 服務: Exchange 2013 Help'
TOCTitle: 停止 Microsoft Exchange Unified Messaging Call Router 服務
ms:assetid: 79935528-1a8c-4f22-826c-8f9a60f4f6f4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ673535(v=EXCHG.150)
ms:contentKeyID: 50554012
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 停止 Microsoft Exchange Unified Messaging Call Router 服務

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2012-11-16_

您可以在命令提示字元處使用服務嵌入式管理單元Microsoft Management Console (MMC) 中或 cmd.exe，用戶端存取伺服器上停止MicrosoftExchange整合通訊呼叫路由器服務。可能您需要停止這個服務，例如時您必須讓用戶端存取伺服器離線。當您停止MicrosoftExchange Unified Messaging Call Router 服務時、 用戶端存取伺服器將不會能夠接受與處理來電。

如需其他與用戶端存取伺服器相關的管理工作，請參閱 [UM 服務程序](um-services-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

  - 若要執行下列程序，必須使用本機 Administrators 群組之成員的帳戶，登入用戶端存取伺服器。

  - 確認用戶端存取伺服器已經安裝完成，無論是在信箱伺服器的同一部電腦上或位於其他電腦上。

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

## 使用 MMC 服務嵌入式管理單元停止 Microsoft Exchange Unified Messaging Call Router 服務

1.  按一下 \[開始\]，然後按一下 \[控制台\]。

2.  連按兩下 \[控制台\] 中的 \[系統管理工具\]。

3.  連按兩下 \[系統管理工具\] 中的 \[服務\]。

4.  在 \[服務\] 詳細資料窗格中，在 \[Microsoft Exchange Unified Messaging Call Router\] 上按一下滑鼠右鍵，然後按 \[停止\]。

## 使用命令提示字元停止 Microsoft Exchange Unified Messaging Call Router 服務

1.  按一下 \[開始\]，然後按 \[執行\]。

2.  在 \[開啟\] 方塊中，輸入下列命令，然後按 ENTER。
    
        net stop MSExchangeUMCR

