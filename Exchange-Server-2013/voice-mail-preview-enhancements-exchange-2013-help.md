---
title: '語音郵件預覽增強功能: Exchange 2013 Help'
TOCTitle: 語音郵件預覽增強功能
ms:assetid: 1fcccec1-4edc-40b8-948c-111647d7d770
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ150501(v=EXCHG.150)
ms:contentKeyID: 50472690
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 語音郵件預覽增強功能

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2012-07-05_

語音郵件預覽是一種功能，可用來接收使用 Microsoft Exchange Server 2010或Exchange Server 2013其語音郵件訊息的使用者整合通訊 (UM)。語音郵件預覽增強 UM 語音信箱功能提供音訊錄製的文字版本。語音郵件文字會顯示在 Microsoft Office Outlook Web App、 Outlook 2010 及其他電子郵件程式內的電子郵件訊息。

## 語音信箱預覽增強功能

在Exchange 2013、 UM 包含許多增強Outlook Web App和Outlook用戶端的使用者介面和信賴與正確性加強的語音郵件預覽。此外，提供一些增強功能與語音相關服務的透過 Microsoft Speech Platform (版本 11.0) 和 Unified Communications Managed API (UCMA) 4.0 為了提升文法產生工作與語言支援。

整合的通訊導入Exchange 2010的語音郵件預覽功能。語音郵件預覽使用自動語音辨識 (ASR) 新增至語音訊息的語音郵件音訊檔的文字版本。ASR 不是完全正確，尤其是當它是透過電話，包括未知的聲音及雜音用於錄製音訊時。

有些組織需要的某些、 語音信箱訊息頗為其使用者的所有、 可持續無錯誤或附近-無錯誤的記錄。語音郵件預覽協力廠商程式可幫助這類符合這些需求的組織。語音郵件預覽協力程式的設計目的在於Exchange 2010來改進語音郵件預覽結果的但未使用該Exchange 2010客戶因的額外負荷和成本。若要解決這些問題， Exchange 2013包含語音郵件預覽的下列增強功能：

  - **改善音訊正規化**  音訊正規化為統一增加 （或愈低） 的程序的整個振幅音訊訊號使所產生的尖峰振幅符合指定的目標或 norm。UM 會將它壓縮及傳送給使用者之前錄製的音訊。

  - **增強語音辨識**  藉由收集 （僅適用於Exchange客戶選擇 \[共用此資訊） 的語音信箱郵件、 語音郵件預覽的結果可用來將單字和片語新增到語音引擎。作法上是藉由設定*VoiceMailAnalysisEnabled*參數`$true`**Set-UMMailbox**指令程式，或將*AllowVoiceMailAnalysis*參數設定為`$true`**Set-UMMailboxPolicy**指令程式上。此外， Exchange 2013 UM 使用更有效率地使用 Outlook 語音存取使用者所建立的電子郵件執行緒資訊。這包括參與者 （Active Directory 或個人連絡人） 資訊 （國家/地區、 縣/市、 公司） 和 Outlook 語音存取使用者的電話號碼的相關資訊。

  - **語音郵件預覽信賴**  信賴分數是由整合通訊直接相關的記錄整體正確性指派的號碼。UM 所使用的信賴計算已調整要更精確及代表 transcribed 郵件的實際的正確性。

  - **篩選** 將偵測並篩選冒犯性字詞，而結果會快取儲存於使用者信箱中。

  - **隱藏文字預覽**  如果語音郵件預覽信賴分數是低於指定臨界值，會隱藏的語音郵件預覽文字。如果隱藏的文字，語音訊息將包含文字表示的語音信箱的信賴所要顯示的結果太低。

  - **記錄效能**  語音郵件預覽是 CPU 耗用大量作業需要大致上按兩次處理音訊檔所花費的時間。如果產生的語音郵件預覽文字時間過長、 CPU 節流處理預覽的停駐點。在Exchange 2010、 UM 沒有嘗試同時已超過 75 秒任何語音訊息。在Exchange 2013、 整個語音訊息 transcribed，但如果它擴充超過 75 秒不包含郵件的文字。

  - **色彩配置**   因為用於分變低、中與高信賴度語音信箱預覽的色彩會造成混亂，Outlook Web App 與 Outlook 的色彩配置在 Exchange 2013 中已被移除。

