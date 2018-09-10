﻿---
title: '啟用或防止從 Outlook 語音存取轉接通話: Exchange Online Help'
TOCTitle: 啟用或防止從 Outlook 語音存取轉接通話
ms:assetid: b80c57f1-394c-4608-8ad3-52a3e6d697db
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee423554(v=EXCHG.150)
ms:contentKeyID: 52062398
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟用或防止從 Outlook 語音存取轉接通話

 

_**適用版本：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：** 2013-02-22_

您可以讓 Outlook 語音存取使用者可將來電轉接至整合通訊 (UM) 撥號有關聯的使用者或防止能力。根據預設，同時啟用此選項並**留下語音訊息而響鈴使用者的電話**\] 選項，使 Outlook 語音存取使用者可以傳輸通話中相同的 UM 的使用者撥號對應表為其留下語音訊息。此設定僅適用於 Outlook 語音存取使用者已輸入其 PIN 和驗證。

如需與 UM 撥號對應表相關的其他工作，請參閱[UM 撥號對應表規劃程序](um-dial-plan-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 撥號對應表」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。 如需詳細步驟，請參閱[建立 UM 撥號對應表](https://docs.microsoft.com/zh-tw/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan)。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。


> [!TIP]  
> 有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.




## 您要執行的工作

## 使用 EAC 讓 Outlook 語音存取使用者能夠或無法轉接來電

1.  在 EAC 中，瀏覽至 \[**整合通訊**\> **UM 撥號對應表**。在清單檢視中，選取您想要變更 UM 撥號對應表\] 和 \[**編輯**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 \[UM 撥號對應表\]頁面上，按一下 \[設定\]。

3.  在**傳輸與搜尋**、 \[**允許來電者**，選取 \[啟用將來電轉接至撥號對應表內的其他使用者的來電者**轉接給使用者**旁的核取方塊。若要防止 Outlook 語音存取使用者傳送給使用者的通話，請清除此核取方塊。

4.  按一下 **\[儲存\]**。

## 使用命令介面讓 Outlook 語音存取使用者能夠或無法轉接來電

此範例會讓 Outlook 語音存取使用者能夠在名為 `MyUMDialPlan` 的 UM 撥號對應表上，將來電轉接給相同對應表中的使用者。

    Set-UMDialPlan -identity MyUMDialPlan -AllowDialPlanSubscribers $true

此範例會使 Outlook 語音存取使用者無法在名為 `MyUMDialPlan` 的 UM 撥號對應表上，將來電轉接給相同對應表中的使用者。

    Set-UMDialPlan -identity MyUMDialPlan -AllowDialPlanSubscribers $false

