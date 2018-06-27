---
title: '啟用 UM 自動語音應答: Exchange Online Help'
TOCTitle: 啟用 UM 自動語音應答
ms:assetid: 16667a8f-50ab-4bb8-9a05-0389511974b1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa996379(v=EXCHG.150)
ms:contentKeyID: 50472680
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟用 UM 自動語音應答

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2012-11-05_

根據預設，當建立整合通訊 (UM) 自動語音應答時，其狀態設為 \[停用。建立 UM 自動語音應答後，您可以變更其狀態以允許它將接聽來電。

如需與 UM 自動語音應答相關的其他管理工作，請參閱[UM 自動語音應答程序](um-auto-attendant-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 自動語音應答」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

  - 執行這些程序之前，請確認已建立 UM 自動語音應答。如需詳細步驟，請參閱[建立 UM 自動語音應答](create-a-um-auto-attendant-exchange-2013-help.md)。

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

## 使用 EAC 來啟用 UM 自動語音應答

1.  在 EAC 中，瀏覽至 \[**整合通訊**\> **UM 撥號對應表**。在清單檢視中，選取您想要變更然後按一下 \[**編輯**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")UM 撥號對應表。

2.  在 \[ **UM 撥號對應表**\] 頁面上 \[ **UM 自動語音應答**，選取您想要啟用的 UM 自動語音應答。在工具列上，按一下 \[**向上箭號**![向上箭號圖示](images/JJ150576.1732c727-328b-4a1a-b84d-6d7252c7dcab(EXCHG.150).gif "向上箭號圖示")。

3.  在 \[警告\] 頁面上按一下 \[是\]。

## 使用命令介面來啟用 UM 自動語音應答

此範例會啟用名為 `MyUMAutoAttendant` 的 UM 自動語音應答來接聽來電。

    Enable-UMAutoAttendant -Identity MyUMAutoAttendant

