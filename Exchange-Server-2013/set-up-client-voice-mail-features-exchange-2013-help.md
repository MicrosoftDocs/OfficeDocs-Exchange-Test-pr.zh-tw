---
title: '設定用戶端語音信箱功能: Exchange 2013 Help'
TOCTitle: 設定用戶端語音信箱功能
ms:assetid: 5e661cfd-d34e-4caa-91a5-967bbecb75eb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ673529(v=EXCHG.150)
ms:contentKeyID: 50553991
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定用戶端語音信箱功能

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-20_

本主題說明授與使用者已啟用 Exchange 整合通訊 (UM) 的存取權的電子郵件和語音信箱訊息在他們的信箱中的用戶端功能。這些功能可讓您提供使用者簡化的存取語音信箱和電子郵件和整體使用者體驗。

**目錄**

Voice mail client support

Outlook Voice Access

Forwarding calls

Voice Mail Preview

Receiving faxes

## 語音信箱用戶端支援

**Exchange ActiveSync 用戶端**  Microsoft Exchange ActiveSync通訊協定用來連線行動用戶端，例如 Exchange 信箱網際網路可使用的行動裝置上。使用者可以使用行動裝置存取其信箱及檢視的電子郵件、 檢視和變更行事曆和連絡人資訊，以及收聽其語音郵件訊息。他們也可以同步處理電子郵件、 語音信箱、 行事曆項目和連絡人資訊與其他裝置。

**與 Outlook 整合**  Microsoft Outlook 可讓使用者存取 Exchange 信箱和檢視其收件匣\] 檢視中的電子郵件及變更行事曆資訊和使用 Microsoft Windows Media Player，這內嵌電子郵件訊息內聆聽語音訊息。藉由使用支援的電子郵件用戶端，使用者會獲得額外的功能，例如上播放 」 電話功能。

**與 Outlook Web App 的整合**  Microsoft Outlook Web App提供使用者與 UM 介面與工具相較下 like Outlook 全功能的電子郵件用戶端設定。使用Outlook Web App，使用者可以使用相容的網頁瀏覽器存取 Exchange 信箱。像 Outlook、 Outlook Web App提供 Windows Media Player 內嵌電子郵件，讓使用者可以接聽語音訊息，並讓使用者存取電話上播放 」 之類的其他功能。

## Outlook 語音存取

在 \[Exchange UM，已啟用 UM 之使用者可撥打 UM 撥號對應表來存取其信箱並使用Outlook語音存取功能表系統上所設定的內部或外部的電話號碼。使用此功能表、 已啟用 UM 的使用者可以讀取電子郵件、 聆聽語音訊息、 互動其Outlook行事曆、 存取其個人連絡人及執行如設定其Outlook語音存取 PIN 或錄製其語音信箱問候語的工作。如需詳細資訊，請參閱[設定 Outlook 語音存取](setting-up-outlook-voice-access-exchange-2013-help.md)。

## 轉接來電

已啟用 UM 的使用者可以建立並設定自動答錄規則使用Outlook或Outlook Web App。呼叫接聽規則可讓使用者控制處理其來電轉接的方式。規則會套用至收件匣規則會套用至內送電子郵件，並與其他使用者的信箱中的語音設定一起儲存的方式類似的來電。最多個九個呼叫接聽規則可以設定每個已啟用 UM 的信箱。這些規則是獨立的收件匣規則並不需要使用者的收件匣規則儲存配額的一部分。如需詳細資訊，請參閱[允許語音郵件使用者可將來電轉接](allow-voice-mail-users-to-forward-calls-exchange-2013-help.md)。

## 語音信箱預覽

語音郵件預覽是一種功能，可接收其語音郵件訊息從 UM 語音信箱系統的使用者。語音郵件預覽增強的語音郵件經驗提供音訊錄製的文字版本。如需詳細資訊，請參閱[允許使用者查看將語音郵件文字記錄](allow-users-to-see-a-voice-mail-transcript-exchange-2013-help.md)。

## 接收傳真

UM 轉寄傳真來電已啟用 UM 之使用者的專用的傳真協力廠商解決方案，以建立傳真寄件者的傳真呼叫以及收到即代表使用者傳真。您已啟用 UM 的使用者可以在他們的信箱中接收傳真訊息之前，您必須執行下列動作：

  - 將 *FaxEnabled* 參數設為 `$true`，藉此在連結至使用者的 UM 撥號對應表上啟用輸入傳真。

  - 將 *Allowfax* 參數設為 `$true`，藉此在連結至使用者的 UM 撥號對應表上啟用輸入傳真。

  - 將 *FaxEnabled* 參數設為 `$true`，藉此啟用使用者的輸入傳真。

  - 將協力程式傳真伺服器 URI 設為允許輸入傳真。

  - 設定在 Mailbox Server 與傳真協力程式伺服器之間的驗證。

