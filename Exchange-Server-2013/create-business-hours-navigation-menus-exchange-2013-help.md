﻿---
title: '建立營業時間導覽功能表: Exchange Online Help'
TOCTitle: 建立營業時間導覽功能表
ms:assetid: f76472fd-aa1a-4cd8-8e26-cc674421d375
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb232203(v=EXCHG.150)
ms:contentKeyID: 50474617
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 建立營業時間導覽功能表

 

_<strong>適用版本：</strong> Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>上次修改主題的時間：</strong> 2012-11-05_

您可以啟用整合通訊 (UM) 自動語音應答的營業時間的按鍵對應。建立 UM 自動語音應答後，預設系統提示將用於營業時間主功能表提示問候語來電者聽到之後上班時間歡迎使用問候語播放。預設上班時間主功能表提示會說明 「 歡迎使用Microsoft Exchange自動語音應答 」。因為沒有按鍵對應未定義預設，沒有功能表選項會提供給來電者，且他們聽到僅預設主功能表提示。

當您設定按鍵對應時，會定義選項及作業，當來電者在使用有語音功能的自動語音應答時說出某個詞，或是來電者在使用沒有語音功能的自動語音應答時按電話鍵台上的按鍵，便會執行這些選項及作業。

如需與 UM 自動語音應答相關的其他管理工作，請參閱[UM 自動語音應答程序](um-auto-attendant-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 自動語音應答」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

  - 執行這些程序之前，請確認已建立 UM 自動語音應答。如需詳細步驟，請參閱[建立 UM 自動語音應答](create-a-um-auto-attendant-exchange-2013-help.md)。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。


> [!TIP]  
> 有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.




## 您要執行的工作

## 使用 EAC 啟用 UM 自動語音應答的上班時間按鍵對應

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。在清單檢視中，選取您要變更的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 \[ <strong>UM 撥號對應表</strong>\] 頁面上 \[ <strong>UM 自動語音應答</strong>，選取您要建立上班時間導覽功能表的 UM 自動語音應答。在工具列上，按一下 \[<strong>編輯</strong>![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[UM 自動語音應答\] 頁面上，按一下 \[功能表導覽\]，在 \[上班時間功能表導覽\] 下方選取 \[啟用上班時間功能表導覽\]，然後按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

4.  在\[新增功能表導覽項目\] 頁面中，使用下列選項來建立新的功能表導覽項目：
    
      - <strong>提示</strong>  使用此方塊可輸入新的瀏覽功能表的名稱。只顯示適用於導覽功能表名稱。這是必要的欄位。
        
        若要指定多個新的瀏覽功能表，因為我們建議您使用您的按鍵對應的有意義的名稱。按鍵對應名稱的最大長度是 64 個字元，而且它可以包含空格。不過，它不能包含任何下列字元："/ \\ \[\]:; |= , + \* ?\< \>。
    
      - <strong>當按下此按鍵</strong>  若要啟用關鍵對應使用此清單。按鍵對應是來電者按下有執行特定作業，例如的自動語音應答轉接來電者至另一個自動語音應答或操作員的數字金鑰。根據預設，不定義任何項目。
        
        您可以使用下拉式清單中的選取 \[來電者必須按下的數字鍵 （從 1 到 9)。零 (0) 保留為自動語音應答運算子。
        
        如果您從下拉式清單中選取<strong>逾時時間</strong>，它可讓來電者轉接至分機號碼或另一個自動語音應答如果它們不在電話鍵盤上按下某個按鍵。例如，「 請保持在列上與將會由下一個可用的人接聽您的來電 」。預設值為 5 秒。如果您啟用此選項時，會建立空白的按鍵對應。
    
      - <strong>播放下列音訊檔案</strong>  使用此選項的來電者選取先前錄製的音訊檔案。按一下 \[<strong>變更</strong>\] 及 \[<strong>瀏覽\]</strong>找出的音訊檔案。如果您保留預設 \< 無 \> 的音訊檔案，整合通訊 TTS （文字轉換語音） 引擎會合成上班時間主功能表提示。或者，您可以建立自訂的音訊檔可用於上班時間主功能表提示啟用語音的自動語音應答。例如，它可能之後，「 至留下語音訊息給銷售、 說 1。若要留下語音訊息給技術支援，說 2。若要留下語音訊息權限管理，說 3。 」
    
      - <strong>執行此額外動作</strong>   選取下列其中一個選項，定義您要自動語音應答針對來電者執行的動作：
        
          - \[無\]   若您不希望自動語音應答將來電轉接到分機或其他自動語音應答，或留下訊息給使用者，請使用該選項。
        
          - <strong>轉接到這個分機</strong>  選取此選項可讓來電轉接至分機號碼。如果您啟用此選項，請使用 \[\] 方塊中輸入分機號碼會將轉接通話。此欄位可讓僅限數字的字元。它不能包含任何下列字元："/ \\ \[\]:; |= , + \* ?\< \>。
        
          - <strong>轉接到這個 UM 自動語音應答</strong>  選取此選項可將電話轉接到自動語音應答。按一下 \[<strong>瀏覽\]</strong>找出您想要使用的自動語音應答。啟用此選項之前，您必須先建立及設定的自動語音應答。當您建立 UM 自動語音應答的父/子結構時使用此選項。
        
          - <strong>留下語音訊息給這位使用者</strong>  選取此選項可讓來電者留下語音郵件訊息的使用者而言是在同一個撥號對應作為您正在設定 UM 自動語音應答。當來電者的自動語音應答功能表選擇這個選項時，系統會提示他們將留下語音訊息所選使用者。按一下 \[<strong>瀏覽\]</strong>找出已啟用 UM 的使用者。
        
          - <strong>宣告公司地點</strong>  選取此選項可讓來電者選擇一個自動語音應答功能表選項和聽到公司的 UM 自動語音應答上設定的位置。若要啟用此選項可正常運作，您必須先將公司地點<strong>商務位置</strong>\] 方塊中輸入 \[<strong>一般</strong>\] 頁面上的 UM 自動語音應答。
        
          - <strong>宣告的營業時間</strong>  選取此選項可讓來電者選擇一個自動語音應答功能表選項和聽到的作業已在 UM 自動語音應答設定營業時間。若要啟用此選項可正常運作，您必須先在<strong>上班時間</strong>\] 頁面上的 UM 自動語音應答上設定營業時間。

5.  按一下 \[確定\] 來建立新的功能表導覽。

6.  在 \[UM 自動語音應答\] 頁面上，按一下 \[儲存\] 儲存您的變更。

## 使用命令界面啟用 UM 自動語音應答的上班時間按鍵對應

本範例設定名為`MyAutoAttendant` UM 自動語音應答並啟用上班時間按鍵對應如此當來電者按下 1\] 時要轉接至另一個名為`SalesAutoAttendant`的 UM 自動語音應答。當他們按下 2 時\] 他們正在支援，轉接至分機號碼 12345 並時所按下 \[3\] 他們正在傳送到另一個自動語音應答播放音訊檔。

    Set-UMAutoAttendant -Identity MyAutoAttendant - BusinessHoursKeyMappingEnabled $true -BusinessHoursKeyMapping "1,Sales,,SalesAutoAttendant","2,Support,12345","3,Directions,,,directions.wav"

