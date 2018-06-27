---
title: '移動通訊清單: Exchange 2013 Help'
TOCTitle: 移動通訊清單
ms:assetid: c843bbd5-6c0e-41e1-b749-7ae87c1beb25
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124534(v=EXCHG.150)
ms:contentKeyID: 50474214
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 移動通訊清單

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-14_

本主題說明如何將現有的通訊清單移至根通訊清單下的新容器中。

如需與通訊清單相關的其他管理工作，請參閱[地址清單程序](address-list-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [電子信箱地址與通訊錄權限](email-address-and-address-book-permissions-exchange-2013-help.md)主題中的「通訊清單」項目。

  - 您無法使用 Exchange 系統管理中心 (EAC) 執行此程序。您必須使用命令介面。

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


## 使用命令介面來移動通訊清單

這個範例使用通訊清單的 GUID，將通訊清單移動至 All Users\\Sales 容器的 Building 4 容器。

    Move-AddressList -Identity c3fffd8e-026b-41b9-88c4-8c21697ac8ac -Target "\All Users\Sales\Building4"

輸入 **Y** 以確認您要移動此通訊清單，然後按 ENTER。

如需詳細語法及參數的資訊，請參閱 [Move-AddressList](https://technet.microsoft.com/zh-tw/library/bb124520\(v=exchg.150\))。

