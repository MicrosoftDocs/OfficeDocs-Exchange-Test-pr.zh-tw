---
title: '啟動 Microsoft Exchange Unified Messaging Call Router 服務: Exchange 2013 Help'
TOCTitle: 啟動 Microsoft Exchange Unified Messaging Call Router 服務
ms:assetid: 8b7e1a4c-87b3-4477-a95f-6b41cf2d38f0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ673542(v=EXCHG.150)
ms:contentKeyID: 50554027
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟動 Microsoft Exchange Unified Messaging Call Router 服務

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2012-11-16_

您可以在命令提示字元處使用服務嵌入式管理單元中Microsoft Management Console (MMC) 或 cmd.exe，在用戶端存取伺服器上啟動MicrosoftExchange Unified Messaging Call Router 服務。根據預設，用戶端存取伺服器已經安裝完成之後，會啟動MicrosoftExchange整合通訊呼叫路由器服務。不過，可能有要重新啟動或MicrosoftExchange Unified Messaging Call Router 服務以手動方式停止，例如，當您已離線用戶端存取伺服器，並使其回復上線時的時間。

在用戶端存取伺服器上啟動 MicrosoftExchange Unified Messaging Call Router 服務時，用戶端存取伺服器就可回答與處理傳入的 UM 呼叫。

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

## 使用 MMC Services 內建以啟動 Microsoft Exchange Unified Messaging Call Router 服務

1.  按一下 \[開始\]，然後按一下 \[控制台\]。

2.  連按兩下 \[控制台\] 中的 \[系統管理工具\]。

3.  連按兩下 \[系統管理工具\] 中的 \[服務\]。

4.  在 \[服務\] 詳細資料窗格中，用滑鼠右鍵按一下 \[Microsoft Exchange Unified Messaging Call Router\]，然後按一下 \[開始\]。

## 使用指令提示以啟動 Microsoft Exchange Unified Messaging Call Router 服務

1.  按一下 \[開始\]，然後按 \[執行\]。

2.  在 \[開啟\] 方塊中，輸入下列命令，然後按 ENTER。
    
        net start MSExchangeUMCR

