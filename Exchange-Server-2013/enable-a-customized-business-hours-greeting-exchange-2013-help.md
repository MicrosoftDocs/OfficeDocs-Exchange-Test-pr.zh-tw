---
title: '啟用自訂的上班時間問候語: Exchange Online Help'
TOCTitle: 啟用自訂的上班時間問候語
ms:assetid: a2272b7d-de88-4d3f-81e6-ad81f0ee6c5e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb232152(v=EXCHG.150)
ms:contentKeyID: 50554041
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟用自訂的上班時間問候語

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-04-19_

您可以啟用整合通訊 (UM) 自動語音應答問候語自訂的營業時間。營業時間問候語是第一件事來電者聽到 UM 自動語音應答時接聽其來電在營業時間。您可能需要自訂問候語。

整合的通訊會包含在營業時間期間使用的預設系統提示。雖然我取代或變更預設的系統提示，您可能會想要提供自訂的問候語。您可以在來電者撥入 UM 自動語音應答在營業時間時所使用的.wav 或.wma 檔案格式中建立的自訂的問候語。例如，"您已達到 Woodgrove Bank。 」

如果您想要包含組織或商務預設問候語的一部分的名稱，您可以在**企業名稱**\] 方塊中輸入名稱上的 UM 自動語音應答。如需詳細資訊，請參閱[輸入企業名稱](enter-a-business-name-exchange-2013-help.md)。

如需與 UM 自動語音應答相關的其他管理工作，請參閱[UM 自動語音應答程序](um-auto-attendant-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 自動語音應答」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

  - 執行這些程序之前，請確認已建立 UM 自動語音應答。如需詳細步驟，請參閱[建立 UM 自動語音應答](create-a-um-auto-attendant-exchange-2013-help.md)。

  - 建立要用於問候語的 .wav 或.wma 檔。

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

## 使用 EAC 啟用自訂的上班時間問候語

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。在清單檢視中，選取您要變更的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 \[UM 撥號對應表\] 頁面的 \[UM 自動語音應答\] 下，選取您想為其啟用自訂之上班時間問候語的 UM 自動語音應答，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 **\[UM 自動語音應答\]** 頁面 \> **\[問候語\]**，按一下 **\[上班時間問候語\]** 下的 **\[變更\]**，然後按一下 **\[瀏覽\]** 找到您在開始此程序前已經建立的自訂上班時間問候語檔案。
    
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

## 使用命令介面啟用自訂的上班時間問候語

本範例會對 UM 自動語音應答 `GreetingFile.wav` 啟用上班時間問候語，此問候語使用名為 `MyUMAutoAttendant` 的自訂問候語。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursWelcomeGreetingEnabled $true -BusinessHoursWelcomeGreetingFilename GreetingFile.wav

此範例會設定名為 `MyUMAutoAttendant` 的 UM 自動語音應答，其上班時間已設為 10:45 到 13:15 (星期日)、09:00 到 17:00 (星期一) 和 09:00 到 16:30 (星期六)，而假日時間及其關聯的問候語則設為 2013 年 1 月 2 日的「`New Year`」，以及從 2013 年 4 月 24 日到 2010 年 4 月 28 日的「`Building Closed for Construction`」。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursSchedule 0.10:45-0.13:15,1.09:00-1.17:00,6.09:00-6.16:30 -HolidaySchedule "New Year,newyrgrt.wav,1/2/2013","Building Closed for Construction,construction.wav,4/24/2013,4/28/2013"

本範例設定名為`MyAutoAttendant` UM 自動語音應答並啟用上班時間按鍵對應如此當來電者按下 1\] 時要轉接至另一個名為`SalesAutoAttendant`的 UM 自動語音應答。當他們按下 2 時\] 他們正在轉接至分機號碼 12345 `Support`，並時所按下 \[3\] 他們正在傳送到播放音訊檔的另一個自動語音應答。

    Set-UMAutoAttendant -Identity MyAutoAttendant - BusinessHoursKeyMappingEnabled $true -BusinessHoursKeyMapping "1,Sales,,SalesAutoAttendant","2,Support,12345","3,Directions,,,directions.wav"

