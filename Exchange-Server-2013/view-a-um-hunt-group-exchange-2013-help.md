---
title: '檢視 UM 群組搜尋: Exchange Online Help'
TOCTitle: 檢視 UM 群組搜尋
ms:assetid: f038f7b4-4de9-4373-bd58-09d49e37a3ed
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb125167(v=EXCHG.150)
ms:contentKeyID: 50554104
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 檢視 UM 群組搜尋

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2012-11-05_

整合通訊 (UM) 群組搜尋的內容檢視時，您可以檢視使用單一的 UM 群組搜尋或所有 UM 群組搜尋相關聯的單一的 UM IP 閘道相關聯的屬性。如果指定這兩個參數，則會傳回所有 UM 群組搜尋。您無法使用 EAC 來檢視 UM 搜尋群組內容 ；您必須使用命令介面。

建立 UM 群組搜尋之後，就無法變更設定的設定。如果您想要變更組態設定，例如引導識別碼在 UM 群組搜尋，您必須刪除現有的 UM 群組搜尋並建立新 UM 群組搜尋已正確設定。

如需與 UM IP 群組搜尋相關的其他管理工作，請參閱 [UM 群組搜尋的程序](um-hunt-group-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 群組搜尋」項目。

  - 執行此程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

  - 執行此程序之前，請確認已建立 UM 閘道。如需詳細步驟，請參閱[建立 UM IP 閘道器](create-a-um-ip-gateway-exchange-2013-help.md)。

  - 執行此程序之前，請確認已建立 UM 群組搜尋。如需詳細步驟，請參閱[建立 UM 群組搜尋](create-a-um-hunt-group-exchange-2013-help.md)。

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


## 使用命令介面來檢視的 UM 群組搜尋屬性

此範例會顯示 Active Directory 樹系中所有的 UM 群組搜尋。

    Get-UMHuntGroup

本範例會顯示 UM 群組搜尋名為`MyUMHuntGroup`以格式化清單的詳細資料。

    Get-UMHuntGroup -identity MyUMIPGateway\MyUMHuntGroup | Format-List

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您使用<strong>Get-UMHuntGroup</strong>指令程式時，您無法輸入 UM 群組搜尋的名稱。您也必須包含與 UM 群組搜尋關聯的 UM IP 閘道的名稱。</td>
</tr>
</tbody>
</table>

