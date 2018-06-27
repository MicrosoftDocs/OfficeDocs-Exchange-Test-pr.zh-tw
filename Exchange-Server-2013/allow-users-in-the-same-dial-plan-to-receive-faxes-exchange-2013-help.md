---
title: '允許使用者接收傳真] 相同的撥號計劃中: Exchange Online Help'
TOCTitle: 允許使用者接收傳真] 相同的撥號計劃中
ms:assetid: cb245028-0b86-4171-879e-934dd35fa626
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124557(v=EXCHG.150)
ms:contentKeyID: 52062411
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 允許使用者接收傳真\] 相同的撥號計劃中

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2016-12-09_

您可以啟用連結與整合通訊 (UM) 撥號對應至其信箱中接收傳真訊息的所有使用者。根據預設，會啟用整合通訊和連結與 UM 撥號對應表的使用者可以接收傳真訊息。若要允許已啟用 UM 的使用者接收傳真訊息中其信箱，撥號對應表必須設定為接受傳入傳真呼叫。您也必須啟用傳真在 UM 信箱原則及使用者。根據預設，傳真會啟用在撥號對應表 UM 信箱原則與使用者。但有時候可能時這些預設值已變更及已啟用 UM 的使用者無法接收傳真訊息。

如果您可以防止傳真訊息在撥號對應表上所接收、 撥號對應表與相關聯的所有使用者將不會能夠接收傳真訊息，即使您設定要讓其接收傳真訊息的個別使用者的屬性。啟用或停用 UM 撥號對應表上的傳真功能優先於設定為上 UM 信箱原則或個別的啟用 UM 之使用者的傳真功能。

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


## 使用命令介面來允許與撥號對應表連結的使用者接收傳真

此範例可讓與 UM 撥號對應表 `MyUMDialPlan` 連結、且已啟用 UM 的使用者接收內送傳真。

    Set-UMDialPlan -Identity MyUMDialPlan -FaxEnabled $true

