---
title: '啟用 UM IP 閘道: Exchange Online Help'
TOCTitle: 啟用 UM IP 閘道
ms:assetid: 2706ae06-c45d-41b7-abbe-378a9fca104a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa996857(v=EXCHG.150)
ms:contentKeyID: 50472736
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟用 UM IP 閘道

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2012-11-05_

根據預設，建立整合通訊 (UM) IP 閘道器之後，其狀態設為已啟用。不過，您可能需要停用讓離線並不允許其接聽傳入或傳出電話的 UM IP 閘道。建立 UM IP 閘道器之後，您可以藉由設定它的狀態變數\] 以啟用或停用來控制其作業和功能。

如需與 UM IP 閘道相關的其他管理工作，請參閱[UM IP 閘道程序](um-ip-gateway-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM IP 閘道」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

  - 執行這些程序之前，請確認已建立 UM IP 閘道器，且已停用。如需詳細步驟，請參閱[建立 UM IP 閘道器](create-a-um-ip-gateway-exchange-2013-help.md)。

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

## 使用 EAC 來啟用 UM IP 閘道

1.  在 EAC 中，瀏覽至 \[整合通訊\] \[UM IP 閘道\]\> ，選取要變更的 UM IP 閘道，然後按一下 \[向上鍵\]![向上箭號圖示](images/JJ150576.1732c727-328b-4a1a-b84d-6d7252c7dcab(EXCHG.150).gif "向上箭號圖示")s。

2.  在 \[警告\] 頁面上按一下 \[是\]。

## 使用命令介面來啟用 UM IP 閘道

此範例會啟用名為 `MyUMIPGateway` 的 UM IP 閘道。

    Enable-UMIPGateway -Identity MyUMIPGateway

