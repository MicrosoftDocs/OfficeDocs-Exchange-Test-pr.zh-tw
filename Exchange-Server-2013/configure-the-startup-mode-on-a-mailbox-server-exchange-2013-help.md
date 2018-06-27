---
title: '設定信箱伺服器上的啟動模式: Exchange 2013 Help'
TOCTitle: 設定信箱伺服器上的啟動模式
ms:assetid: 4457d6a0-52bd-4269-8cb5-d34d7fe9bfc3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee423544(v=EXCHG.150)
ms:contentKeyID: 50553975
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定信箱伺服器上的啟動模式

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-15_

您可以在信箱伺服器上指定的 Microsoft Exchange 整合通訊服務的啟動模式。根據預設，TCP 模式會開始 Mailbox server，但如果您使用傳輸層安全性 (TLS) 來加密 Voice over IP (VoIP) 流量，您必須設定使用 TLS 或雙重模式的信箱伺服器。建議的信箱伺服器設定為雙作為啟動模式。這是因為所有 Client Access server 和 Mailbox server 可以回覆來電所有 um 撥號對應表，並以外的撥號對應表可以都有不同的安全性設定 （「 不安全 」、 SIP 安全 」 或 「 安全 」）。如果您變更的啟動模式，您必須重新啟動 Microsoft Exchange 整合通訊服務的變更才會生效。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>根據預設，Mailbox server 可用來接聽來電。您不需要將信箱伺服器新增至 UM 撥號對應至處理序 UM 呼叫除非您正在整合 UM 與 Microsoft Office Communications Server 2007 R2 或 Microsoft Lync Server。</td>
</tr>
</tbody>
</table>


關於與整合通訊和信箱伺服器相關的其他管理工作，請參閱 [UM 服務程序](um-services-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「Mailbox server (UM Service)」項目。

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

## 使用 EAC 設定 Mailbox Server 上的啟動模式

1.  在 EAC 中，瀏覽至 \[伺服器\] \> \[伺服器\]。

2.  在清單檢視中，選取您要修改的 Exchange 伺服器，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 **\[Exchange Server\]** 頁面上，按一下 **\[整合通訊\]**。

4.  在 **\[UM 服務設定\]** \> **\[UM 啟動模式\]** 下，從下拉式清單中選取下列其中一項：
    
      - **TCP**   如果您不是使用 mTLS，而且所使用的僅是不安全的撥號對應表，請使用此選項。
    
      - **TLS**   如果您是使用 mTLS，而且所使用的僅是「SIP 安全」或「安全」撥號對應表，請使用此選項。
    
      - **雙重**   如果您是使用 mTLS，而且使用「不安全」、「SIP 安全」和「安全」撥號對應表，請使用此選項。

5.  選取 UM 啟動模式之後，按一下 **\[儲存\]**。

## 使用命令介面設定信箱伺服器上的啟動模式

此範例會將名爲 `MyUMServer1` 的 Mailbox Server 啟動模式設為雙重模式。

    Set-UMService -Identity MyUMServer1 -UMStartUpMode Dual

此範例會將名爲 `MyUMServer1` 的 Mailbox Server 啟動模式設為 TLS 模式。

    Set-UMService -Identity MyUMServer1 -UMStartUpMode TLS

