---
title: '啟用或停用傳送給使用者的語音訊息: Exchange Online Help'
TOCTitle: 啟用或停用傳送給使用者的語音訊息
ms:assetid: faa300d8-2534-40db-8ef9-428be8bb7934
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd351277(v=EXCHG.150)
ms:contentKeyID: 52062443
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟用或停用傳送給使用者的語音訊息

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2012-12-13_

您可以讓來電者在傳送語音訊息給使用者的整合通訊 (UM) 自動語音應答，或防止能力。根據預設，此選項已啟用，且可讓來電者在傳送語音訊息給使用者的 UM 撥號對應表已與之相關聯的 UM 自動語音應答。如果您停用此選項，自動語音應答將不會邀請來電者在系統提示時傳送語音訊息。

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

## 使用 EAC 以允許或禁止來電者傳送語音訊息

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。在清單檢視中，選取您要變更的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 **\[UM 撥號對應表\]** 頁面的 **\[UM 自動語音應答\]** 下方，選取您要管理的 UM 自動語音應答，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[ **UM 自動語音應答**\] 頁面上 \>**解決活頁簿及操作員存取權**，\[**連絡使用者的選項**\] 下選取 \[**允許來電者在留下語音訊息的使用者**啟用來電者在留下語音訊息\] 旁的核取方塊。若要避免來電者留下語音訊息，請清除核取方塊。

4.  按一下 **\[儲存\]**。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若您停用此選項並停用 <strong>[允許來電者撥打給使用者]</strong> 選項，則亦會停用 <strong>[搜尋通訊錄的選項]</strong>。</td>
</tr>
</tbody>
</table>


## 使用命令介面讓來電者能夠傳送語音訊息或阻止來電者傳送

這個範例會阻止來電給名為 `MyUMAutoAttendant` 之 UM 自動語音應答的來電者傳送語音訊息。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -SendVoiceMsgEnabled $false

本範例會允許來電者致電名為 `MyUMAutoAttendant` 的 UM 自動語音應答，以傳送語音訊息。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -SendVoiceMsgEnabled $true

