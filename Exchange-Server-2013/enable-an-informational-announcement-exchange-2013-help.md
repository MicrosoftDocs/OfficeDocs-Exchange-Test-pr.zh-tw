---
title: '啟用資訊的宣告: Exchange Online Help'
TOCTitle: 啟用資訊的宣告
ms:assetid: 07f6c13e-3781-4127-9321-f0f85f054259
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb266918(v=EXCHG.150)
ms:contentKeyID: 50553929
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟用資訊的宣告

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-04-19_

您可以啟用整合通訊 (UM) 自動語音應答的資訊的宣告。資訊性宣告啟用時，它會播放後面的商務或非上班時間問候語。根據預設，不被設定資訊的宣告。若要啟用資訊的宣告，建立.wav 或.wma 檔案做為參考的宣告，然後再設定要使用此聲音檔的自動語音應答。

如需與 UM 自動語音應答相關的其他管理工作，請參閱[UM 自動語音應答程序](um-auto-attendant-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 自動語音應答」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在執行這些程序之前，請確認已建立 UM 自動語音應答。 如需詳細步驟，請參閱[建立 UM 自動語音應答](create-a-um-auto-attendant-exchange-2013-help.md)。

  - 建立要用於資訊性宣告的 .wav 或 .wma 檔案。

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

## 使用 EAC 啟用資訊性宣告

1.  在 EAC 中，瀏覽至 \[**整合通訊**\> **UM 撥號對應表**。在清單檢視中，選取您想要變更 UM 撥號對應表\] 和 \[**編輯**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 \[UM 撥號對應表\] 頁面的 \[UM 自動語音應答\] 下，選取您想為其啟用資訊性宣告的 UM 自動語音應答，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 **\[UM 自動語音應答\]** 頁面 \> **\[問候語\]** 的 **\[資訊性宣告\]** 下方，按一下 **\[變更\]**，然後按一下 **\[瀏覽\]** 找出在開始此程序之前建立的資訊性宣告檔。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您用於問候語的檔案必須是 .wav 或 .wma 檔案。</td>
    </tr>
    </tbody>
    </table>


4.  找到檔案之後，請按一下 \[開啟\]，然後按一下 \[儲存\]。

## 使用命令介面來啟用資訊性宣告

此範例會針對名為 `MyInfoAnnouncement.wav` 的 UM 自動語音應答啟用使用 `MyUMAutoAttendant` 檔案的資訊性宣告。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -InfoAnnouncementEnabled $true -InfoAnnouncementFilename MyInfoAnnouncement.wav

