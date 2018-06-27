---
title: '啟用或停用目錄查閱服務: Exchange Online Help'
TOCTitle: 啟用或停用目錄查閱服務
ms:assetid: c0768815-8578-4385-8d4c-7d1e40304cec
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee423557(v=EXCHG.150)
ms:contentKeyID: 52062400
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟用或停用目錄查閱服務

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2016-05-10_

您可以使來電者撥打整合通訊 (UM) 自動語音應答可以查詢中使用其電話按鍵之目錄的名稱，但是無法使用搜尋 directory 語音輸入來啟用目錄查閱服務。預設會啟用此設定。如果已停用此設定，來電者將無法使用按鍵式特定人員搜尋目錄或語音命令。

如需與 UM 自動語音應答相關的其他管理工作，請參閱[UM 自動語音應答程序](um-auto-attendant-procedures-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Outlook 語音存取使用者無法使用自動語音辨識 (ASR) 或語音輸入來尋找目錄中的使用者，他們只能使用 DTMF 或按鍵式輸入。</td>
</tr>
</tbody>
</table>


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

## 使用 EAC 來啟用或停用目錄查閱

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。在清單檢視中，選取您要變更的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 **\[UM 撥號對應表\]** 頁面的 **\[UM 自動語音應答\]** 下，選取要啟用或停用目錄查閱的 UM 自動語音應答，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[ **UM 自動語音應答**\] 頁面上 \> **Address book and 運算子存取**，請在**搜尋通訊錄的選項**\] 下選取**允許來電者在搜尋會根據名稱或別名的使用者**啟用來電者在使用者搜尋\] 旁的核取方塊。若要停用從搜尋使用者的來電者，請清除此核取方塊。

4.  按一下 **\[儲存\]**。

## 使用命令介面來啟用或停用目錄查閱

此範例會停用名為 `MyUMAutoAttendant` 之 UM 自動語音應答上的目錄查閱。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -NameLookupEnabled $false

