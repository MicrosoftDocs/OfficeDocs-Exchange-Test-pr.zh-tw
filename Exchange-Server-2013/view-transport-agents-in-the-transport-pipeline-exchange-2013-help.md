---
title: '傳輸管線中檢視傳輸代理程式: Exchange 2013 Help'
TOCTitle: 傳輸管線中檢視傳輸代理程式
ms:assetid: bd715d8e-7b21-48de-8f68-d425d8506e4c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124395(v=EXCHG.150)
ms:contentKeyID: 51409239
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 傳輸管線中檢視傳輸代理程式

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-08_

您可以使用 Exchange 管理命令介面來檢視 Microsoft Exchange Server 2013信箱伺服器與用戶端存取伺服器上的傳輸管線中的傳輸代理程式清單。尤其是**Get-TransportPipeline**指令程式會顯示下列類型的傳輸代理程式的相關資訊傳輸管線中：

  - Mailbox Server 上以「傳輸」服務中的 **SmtpReceiveAgent**、**RoutingAgent**、**DeliveryAgent** 與 **StorageAgent** 類別為基礎的代理程式。

  - Mailbox Server 上以「信箱傳輸傳遞」服務中的 **SmtpReceiveAgentClass** 為基礎的代理程式。

  - Client Access Server 上以「前端傳輸」服務中的 **SmtpReceiveAgentClass** 為基礎的代理程式。

您可以檢視已發生郵件傳輸管線中的所有已啟用的傳輸代理程式和其登錄的 SMTP 事件的清單。如需傳輸代理程式的詳細資訊，請參閱[傳輸代理程式](transport-agents-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「傳輸代理程式」項目。

  - 您只能使用命令介面來執行此程序。

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


## 使用命令介面來檢視傳輸管線中的傳輸代理程式清單

若要使用命令介面來檢視 Exchange 伺服器上傳輸管線中之傳輸代理程式的清單，請執行下列命令：

    Get-TransportPipeline | Format-List

若要將結果匯出至名為 C:\\My Documents\\Transport Agents.txt 的文字檔，請執行下列命令：

    Get-TransportPipeline | Format-List > "C:\My Documents\Transport Agents.txt"

## 如何才能了解這是否正常運作？

指令程式會顯示已發生郵件傳輸服務開始時的時間和**Get-TransportPipeline**指令程式執行的時間的時間之間傳輸管線中的傳輸代理程式。即使啟用該傳輸代理程式尚未遭遇到傳輸管線中的郵件傳輸代理程式將不會出現**Get-TransportPipeline**指令程式，顯示在結果中。

