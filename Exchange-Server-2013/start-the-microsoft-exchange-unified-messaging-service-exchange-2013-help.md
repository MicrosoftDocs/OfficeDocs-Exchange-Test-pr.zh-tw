---
title: '啟動 Microsoft Exchange 整合通訊服務: Exchange 2013 Help'
TOCTitle: 啟動 Microsoft Exchange 整合通訊服務
ms:assetid: b54008e6-172e-4435-8516-57cff740e89c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124330(v=EXCHG.150)
ms:contentKeyID: 50554054
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟動 Microsoft Exchange 整合通訊服務

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2012-11-16_

您可以在命令提示字元處使用服務嵌入式管理單元中Microsoft Management Console (MMC) 或 cmd.exe，在信箱伺服器上啟動MicrosoftExchange整合通訊服務。根據預設， MicrosoftExchange整合通訊服務已啟動信箱伺服器已經安裝完成之後。不過，可能有要手動重新啟動MicrosoftExchange整合通訊服務，例如，當您已離線 Mailbox server，並使其回復上線時的時間。

當 MicrosoftExchange 整合通訊服務在信箱伺服器上啟動時，信箱伺服器即可接聽及處理傳入的 UM 呼叫。

如需與信箱伺服器相關的其他管理工作，請參閱 [UM 服務程序](um-services-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

  - 若要執行下列程序，必須使用本機 Administrators 群組之成員的帳戶，登入信箱伺服器。

  - 確認信箱伺服器已經安裝完成，無論是在用戶端存取伺服器的同一部電腦上或位於其他電腦上。

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

## 使用 MMC 服務嵌入式管理單元來啟動 Microsoft Exchange 整合通訊服務

1.  按一下 **\[開始\]**，然後按一下 **\[控制台\]**。

2.  連按兩下 \[控制台\] 中的 \[系統管理工具\]。

3.  連按兩下 \[系統管理工具\] 中的 \[服務\]。

4.  在 \[服務\] 詳細資料窗格中，在 \[Microsoft Exchange 整合通訊\] 上按一下滑鼠右鍵，然後按 \[啟動\]。

## 使用命令提示來啟動 Microsoft Exchange 整合通訊服務

1.  按一下 \[開始\]，然後按 \[執行\]。

2.  在 \[開啟\] 方塊中，輸入下列命令，然後按 ENTER。
    
        net start MSExchangeUM

