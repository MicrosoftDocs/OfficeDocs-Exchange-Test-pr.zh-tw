---
title: '在信箱伺服器上設定來電的數目: Exchange 2013 Help'
TOCTitle: 在信箱伺服器上設定來電的數目
ms:assetid: 419e1de9-2bf8-48a8-824d-2a536b0a6d90
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa997637(v=EXCHG.150)
ms:contentKeyID: 50553970
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 在信箱伺服器上設定來電的數目

 

_**適用版本：**Exchange Server, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-23_

您可以設定執行 Microsoft Exchange 整合通訊服務的信箱伺服器會接受的傳入並行連線數目。這包括所有來電包括 Outlook 語音存取、 來電接聽、 自動語音應答和傳真呼叫。當您增加的信箱伺服器上的並行連線數目時更多的系統資源是必要的比您如果減少並行通話數目。愈低並行通話數目特別重要的是較慢的電腦上安裝整合通訊服務。並行語音通話數目的範圍是 0 到 200。預設值為 100。

如需與整合通訊和信箱伺服器相關的其他工作，請參閱 [UM 服務程序](um-services-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「Mailbox server (UM Service)」項目。

  - 確認已正確安裝用戶端存取和信箱伺服器。

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

## 使用 EAC 設定 Mailbox Server 上的來電數目

1.  在 EAC 中，瀏覽至 \[伺服器\] \> \[伺服器\]。

2.  在清單檢視中，選取您要修改的 Exchange 伺服器，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 **\[Exchange Server\]** 頁面上，按一下 **\[整合通訊\]**。

4.  在 **\[UM 服務設定\]** 的 **\[允許的最大呼叫數目\]** 下方輸入 0 到 200 之間的數值，然後按一下 **\[儲存\]**。

## 使用命令介面設定 Mailbox Server 上的來電數目

此範例會將名爲 `MyMailboxServer1` 的信箱伺服器可接受的傳入語音、Outlook 語音存取和傳真呼叫數目設為 50。

    Set-UMService -Identity MyMailboxServer1 -MaxCallsAllowed 50

