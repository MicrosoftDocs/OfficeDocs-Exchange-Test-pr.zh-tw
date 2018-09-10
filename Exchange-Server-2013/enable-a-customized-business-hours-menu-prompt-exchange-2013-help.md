﻿---
title: '啟用自訂的上班時間功能表提示: Exchange Online Help'
TOCTitle: 啟用自訂的上班時間功能表提示
ms:assetid: 89053e84-3490-4dc6-ade3-9b6c5dbf4020
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb232116(v=EXCHG.150)
ms:contentKeyID: 50554025
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟用自訂的上班時間功能表提示

 

_**適用版本：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：** 2013-04-19_

您可以自訂在營業時間使用整合通訊 (UM) 自動語音應答功能表提示。建立 UM 自動語音應答後，預設系統提示 （「 歡迎使用整合通訊 」） 會做為來電者聽到歡迎使用問候語播放營業時間之後功能表提示。雖然我取代或變更系統提示字元中，您可以自訂問候語和功能表提示所使用的 UM 自動語音應答。建立自訂的上班時間功能表提示音訊檔之後，您必須啟用功能表導覽項目上的 UM 自動語音應答的上班時間。

如果您只想要包含組織或商務一部分的預設系統提示的名稱，您可以在**企業名稱**\] 方塊中輸入名稱上的 UM 自動語音應答。如需詳細資訊，請參閱[輸入企業名稱](https://docs.microsoft.com/zh-tw/exchange/voice-mail-unified-messaging/automatically-answer-and-route-calls/enter-a-business-name)。


> [!IMPORTANT]  
> 您必須在自動語音應答上設定營業時間。如需詳細資訊，請參閱<a href="https://docs.microsoft.com/zh-tw/exchange/voice-mail-unified-messaging/automatically-answer-and-route-calls/configure-business-hours">設定營業時間</a>。




如需與 UM 自動語音應答相關的其他管理工作，請參閱[UM 自動語音應答程序](https://docs.microsoft.com/zh-tw/exchange/voice-mail-unified-messaging/automatically-answer-and-route-calls/um-auto-attendant-procedures)。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 自動語音應答」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](https://docs.microsoft.com/zh-tw/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan)。

  - 執行這些程序之前，請確認已建立 UM 自動語音應答。如需詳細步驟，請參閱[建立 UM 自動語音應答](create-a-um-auto-attendant-exchange-2013-help.md)。

  - 建立要用於功能表提示的 .wav 或 .wma 檔案。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。


> [!TIP]  
> 有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.




## 您要執行的工作

## 使用 EAC 啟用自訂的上班時間功能表提示

1.  在 EAC 中，瀏覽至 \[**整合通訊**\> **UM 撥號對應表**。在清單檢視中，選取您想要變更 UM 撥號對應表\] 和 \[**編輯**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 \[UM 撥號對應表\] 頁面的 \[UM 自動語音應答\] 下，選取您想為其啟用自訂之上班時間功能表提示的 UM 自動語音應答，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 **\[UM 自動語音應答\]** 頁面 \> **\[功能表導覽\]**，按一下 **\[上班時間功能表導覽\]** 下的 **\[變更\]**，然後按 **\[瀏覽\]** 找到自訂的上班時間功能表提示檔案。
    
    > [!IMPORTANT]  
    > 用於功能表提示的檔案必須是 .wav 或 .wma 檔案。


4.  找到檔案之後，請按一下 \[開啟\]，然後按一下 \[儲存\]。

## 使用命令介面啟用自訂的上班時間功能表提示

此範例會在 UM 自動語音應答 `businesshoursprompts.wav` 中啟用上班時間主功能表提示，並使用名為 `MyUMAutoAttendant` 的自訂提示。

    Command Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursMainMenuCustomPromptEnabled $true -BusinessHoursMainMenuCustomPromptFilename BusinessHoursPrompts.wav

此範例會設定名為 `MyUMAutoAttendant` 的 UM 自動語音應答，其上班時間已設為 10:45 到 13:15 (星期日)、09:00 到 17:00 (星期一) 和 09:00 到 16:30 (星期六)，而假日時間及其關聯的問候語則設為 2013 年 1 月 2 日的「`New Year`」，以及從 2013 年 4 月 24 日到 2013 年 4 月 28 日的「`Building Closed for Construction`」。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursSchedule 0.10:45-0.13:15,1.09:00-1.17:00,6.09:00-6.16:30 -HolidaySchedule "New Year,newyrgrt.wav,1/2/2013","Building Closed for Construction,construction.wav,4/24/2013,4/28/2013"

本範例設定名為`MyAutoAttendant` UM 自動語音應答並啟用如此當來電者按下 1\] 時要轉接至另一個名為`SalesAutoAttendant`的 UM 自動語音應答的上班時間導覽功能表。當他們按下 2 時\] 他們正在轉接至分機號碼 12345 `Support`，並時所按下 \[3\] 他們正在傳送到播放音訊檔的另一個自動語音應答。

    Set-UMAutoAttendant -Identity MyAutoAttendant - BusinessHoursKeyMappingEnabled $true -BusinessHoursKeyMapping "1,Sales,,SalesAutoAttendant","2,Support,12345","3,Directions,,,directions.wav"

