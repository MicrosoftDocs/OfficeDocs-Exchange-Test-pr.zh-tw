---
title: '設定遠端網域外出回覆: Exchange 2013 Help'
TOCTitle: 設定遠端網域外出回覆
ms:assetid: 0c1e56be-7a29-4294-9762-600f9f788741
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ657713(v=EXCHG.150)
ms:contentKeyID: 50472538
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定遠端網域外出回覆

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-08_

您可以使用 Exchange 管理命令介面來設定電子郵件的傳送和接收透過遠端網域的方式。下列示範如何使用 Exchange 管理命令介面來設定方式Exchange外出回覆的控點。

## 開始之前有哪些須知？

  - 預估完成時間：10 分鐘

  - 您只能使用命令介面來執行此程序。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「遠端網域」項目。

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


## 使用命令介面來設定外出回覆

您可以使用 **Set-RemoteDomain** 指令程式，設定遠端網域的內容。

本範例為名為 Contoso 的遠端網域停用外出訊息。

    Set-RemoteDomain Contoso -AllowedOOFType None

此範例只允許外部郵件答錄機訊息。

    Set-RemoteDomain Contoso -AllowedOOFType External

