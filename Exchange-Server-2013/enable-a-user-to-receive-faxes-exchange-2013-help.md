---
title: '讓使用者接收傳真: Exchange Online Help'
TOCTitle: 讓使用者接收傳真
ms:assetid: a0505001-aac0-41ef-824f-76e5e56d7675
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb201712(v=EXCHG.150)
ms:contentKeyID: 52062379
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 讓使用者接收傳真

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2016-12-09_

您可以啟用整合通訊 (UM) 使用者接收傳真\]。根據預設，當您啟用使用者的整合通訊時所將能夠接收傳真\] 如果您啟用傳真並連結到使用者的 UM 信箱原則上設定傳真協力程式的 URI。傳真可啟用或停用在 UM 撥號對應表計劃、 UM 信箱原則或已啟用 UM 之使用者的信箱。

根據預設，使用者的信箱和連結與該使用者的撥號允許傳入的傳真。不過，使用者接收傳真您必須先啟用已啟用 UM 功能的使用者相關聯並輸入傳真協力程式的 URI 的 UM 信箱原則上輸入傳真。

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

  - 預估完成時間： 2 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 信箱原則」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

  - 執行這些程序之前，請確認已建立 UM 信箱原則。如需詳細步驟，請參閱[建立 UM 信箱原則](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 執行這些程序之前，請先確認指派給使用者的 UM 信箱原則已啟用傳真功能，且已正確設定傳真協力程式的 URI。

  - 執行下列程序之前，請確認使用者已啟用整合通訊。如需詳細步驟，請參閱[啟用使用者的語音信箱](enable-a-user-for-voice-mail-exchange-2013-help.md)。

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


## 使用命令介面讓 UM 使用者能夠接收傳真

本範例能讓 Tony Smith 能夠接收傳入的傳真。

    Set-UMMailbox -Identity tonysmith@contoso.com -FaxEnabled $true

