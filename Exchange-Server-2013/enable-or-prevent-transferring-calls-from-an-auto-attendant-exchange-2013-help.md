---
title: '啟用或防止從自動語音應答轉接通話: Exchange Online Help'
TOCTitle: 啟用或防止從自動語音應答轉接通話
ms:assetid: ca961cc8-cc24-4e05-b72d-79979c155cf9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee423558(v=EXCHG.150)
ms:contentKeyID: 52062409
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟用或防止從自動語音應答轉接通話

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-22_

您可以啟用將來電轉接至使用者透過自動語音應答的來電者或防止能力。預設此選項已啟用，且可讓來電者將來電轉接至已啟用 UM 之使用者的整合通訊 (UM) 撥號有關聯的 UM 自動語音應答。

如需與 UM 自動語音應答相關的其他管理工作，請參閱[UM 自動語音應答程序](um-auto-attendant-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 自動語音應答」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在執行這些程序之前，請確認已建立 UM 自動語音應答。 如需詳細步驟，請參閱[建立 UM 自動語音應答](create-a-um-auto-attendant-exchange-2013-help.md)。

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

## 使用 EAC 允許或防止從 UM 自動語音應答將來電轉接給使用者

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。在清單檢視中，選取您要變更的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 **\[UM 撥號對應表\]** 頁面的 **\[UM 自動語音應答\]** 下，選取要設定來電轉接的 UM 自動語音應答，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[ **UM 自動語音應答**\] 頁面上 \>**解決活頁簿及操作員存取權**，\[**連絡使用者的選項**\] 下選取**允許來電者在使用者的撥號對應表**啟用來電轉接\] 旁的核取方塊。若要防止來電轉接、 清除此核取方塊。

4.  按一下 **\[儲存\]**。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您同時清除此核取方塊與 <strong>[允許來電者留下語音訊息給使用者]</strong> 核取方塊，<strong>[搜尋通訊錄的選項]</strong> 將會停用。</td>
</tr>
</tbody>
</table>


## 使用命令介面允許或防止從 UM 自動語音應答將來電轉接給使用者

此範例會在名為 `MyUMAutoAttendant` 的 UM 自動語音應答上防止轉接來電。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -AllowDialPlanSubscribers $false

此範例會在名為 `MyUMAutoAttendant` 的 UM 自動語音應答上允許轉接來電。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -AllowDialPlanSubscribers $true

