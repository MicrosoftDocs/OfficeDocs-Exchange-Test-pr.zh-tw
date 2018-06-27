---
title: '啟用未接的來電通知的使用者: Exchange Online Help'
TOCTitle: 啟用未接的來電通知的使用者
ms:assetid: aa0cbb60-5422-474f-af16-621aade31c1f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb232159(v=EXCHG.150)
ms:contentKeyID: 52062373
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟用未接的來電通知的使用者

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2012-12-09_

您可以啟用或使用命令介面或 EAC 來停用整合通訊 (UM) 信箱原則的未接的來電通知。未接的來電通知使用者不會接聽來電時，傳送給使用者的電子郵件訊息，且來電者不會留下語音郵件訊息。這是不同的電子郵件訊息包含語音訊息離開使用者的郵件。

當您停用 UM 信箱原則上的未接的來電通知時，您會防止從接收電子郵件訊息的 UM 信箱原則相關聯的所有使用者當他們不接聽來電與來電者不會留下語音訊息。根據預設，會建立每個 UM 信箱原則啟用未接的來電通知。也根據預設，每次您建立 UM 撥號對應表會建立 UM 信箱原則。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您在整合整合通訊與 Microsoft Lync Server 時，信箱位於 Exchange 2007 或 Exchange 2010 Mailbox Server 上的使用者，當使用者在來電尚未傳送給執行 Microsoft Exchange 整合通訊服務的 Mailbox Server 之前中斷連線時，將無法使用未接來電通知。</td>
</tr>
</tbody>
</table>


如需其他與 UM 信箱原則相關的管理工作，請參閱 [管理 UM 信箱原則](manage-a-um-mailbox-policy-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 信箱原則」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

  - 執行這些程序之前，請確認已建立 UM 信箱原則。如需詳細步驟，請參閱[建立 UM 信箱原則](create-a-um-mailbox-policy-exchange-2013-help.md)。

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

## 使用 EAC 啟用 UM 信箱原則的未接來電通知

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。在清單檢視中，選取您要變更的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 **\[UM 撥號對應表\]** 頁面的 **\[UM 信箱原則\]** 下，選取您要管理的 UM 信箱原則，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 **\[UM 信箱原則\]** 頁面 \> **\[一般\]** 上，選取 **\[允許未接來電通知\]** 旁的核取方塊。

4.  按一下 **\[儲存\]**。

## 使用命令介面啟用 UM 信箱原則的未接來電通知

本範例會對名為 `MyUMMailboxPolicy` 的 UM 信箱原則啟用未接來電通知。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowMissedCallNotifications $true

