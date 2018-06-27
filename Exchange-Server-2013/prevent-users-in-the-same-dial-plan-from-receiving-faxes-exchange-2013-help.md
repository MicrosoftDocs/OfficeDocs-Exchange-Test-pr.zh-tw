---
title: '防止使用者在同一個撥號對應表中接收傳真: Exchange Online Help'
TOCTitle: 防止使用者在同一個撥號對應表中接收傳真
ms:assetid: 4fc66414-c950-4bca-ac20-4e489f288d06
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb201688(v=EXCHG.150)
ms:contentKeyID: 52062301
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 防止使用者在同一個撥號對應表中接收傳真

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2016-12-09_

您可以防止與整合通訊 (UM) 撥號從接收傳真訊息連結已啟用 UM 的使用者。根據預設，會啟用整合通訊和連結與 UM 撥號對應表的使用者可以接收傳真訊息。不過，可能是您想来阻止特定 UM 撥號對應表從接收傳真與相關聯的使用者。

您可以防止啟用 UM 的使用者可以設定 UM 撥號對應表、 UM 信箱原則或已啟用 UM 之使用者的信箱接收傳真\]。如果您停用傳入傳真訊息傳遞在 UM 撥號對應表，所有與撥號對應表相關聯的使用者將會禁止接收傳真訊息。啟用或停用 UM 撥號對應表上的傳真功能會個別啟用 UM 之使用者的設定優先。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您可以使用 EAC UM 信箱原則上設定傳真。不過，您必須使用命令介面來設定傳真或個別使用者撥號對應表上。</td>
</tr>
</tbody>
</table>


如需傳真協力廠商的詳細資訊，請參閱[Microsoft PinPoint 傳真協力廠商](https://go.microsoft.com/fwlink/?linkid=190238)。

如需與傳真相關的其他管理工作，請參閱[傳真程序](faxing-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 撥號對應表」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。 如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

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


## 使用命令介面防止與撥號對應表相連結的使用者接收傳真

此範例會防止與名爲 `MyUMDialPlan` 的 UM 撥號對應表相關聯並已啟用 UM 的使用者接收傳真。

    Set-UMDialPlan -Identity MyUMDialPlan -FaxEnabled $false

