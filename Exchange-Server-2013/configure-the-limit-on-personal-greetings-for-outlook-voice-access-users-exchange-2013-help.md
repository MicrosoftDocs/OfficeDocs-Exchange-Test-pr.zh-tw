---
title: '設定 Outlook 語音存取使用者的個人問候語上的限制: Exchange Online Help'
TOCTitle: 設定 Outlook 語音存取使用者的個人問候語上的限制
ms:assetid: d400f250-0f55-45f5-9918-5f1d7819fbdf
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb201731(v=EXCHG.150)
ms:contentKeyID: 50554098
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定 Outlook 語音存取使用者的個人問候語上的限制

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2012-11-05_

**限制個人問候語 （分鐘）**設定可讓您輸入的整合通訊 (UM) 信箱原則相關聯的使用者可以使用記錄其語音信箱問候語的分鐘數上限。此設定會套用到其標準的語音信箱和其不在辦公室語音信箱問候語。根據預設，問候語期間的最大值設為 5 分鐘。不過，您可以設定問候語介於 1 到 10 分鐘之間的任何設定的持續期間的最大值。

如需其他與 UM 信箱原則相關的管理工作，請參閱 [UM 信箱原則程序](um-mailbox-policy-procedures-exchange-2013-help.md)。

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

## 使用 EAC 來變更問候語期間的最大值

1.  在 EAC 中，瀏覽至 \[**整合通訊**\> **UM 撥號對應表**。在清單檢視中，選取您要修改的 UM 撥號，然後按一下工具列上的 \[**編輯**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 \[UM 撥號對應表\] 頁面中的 \[UM 信箱原則\] 之下，選取您要管理的 UM 信箱原則，然後按一下工具列上的 \[編輯\]**Edit**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[ **UM 信箱原則**\] 頁面上 \>**一般**、**限制個人問候語 （分鐘） 上的**、 下輸入的時間，以分鐘為單位，允許的語音郵件使用者的個人問候語。

4.  按一下 **\[儲存\]**。

## 使用命令介面來變更問候語期間的最大值

此範例會在 UM 信箱原則`MyUMMailboxPolicy`為 3 分鐘問候語期間的最大值。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy MaxGreetingDuration 3

