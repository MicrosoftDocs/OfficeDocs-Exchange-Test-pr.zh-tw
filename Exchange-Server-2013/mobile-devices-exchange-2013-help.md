---
title: '行動裝置: Exchange 2013 Help'
TOCTitle: 行動裝置
ms:assetid: 93a949e7-b3ef-43ea-ae0c-6698826fc8d2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb232129(v=EXCHG.150)
ms:contentKeyID: 50473755
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 行動裝置

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-09-24_

Microsoft Exchange ActiveSync可讓使用者為已啟用行動裝置存取大部分Microsoft Exchange信箱資料的任何時候，任何地方。有許多不同的行動電話與裝置啟用Exchange ActiveSync。這些包括Windows電話、 Nokia 行動電話、 Android 電話與平板電腦與 Apple iPhone、 iPod 與 iPad。

雖然電話和非 phone 行動裝置支援Exchange ActiveSync，大部分Exchange ActiveSync文件中，我們會使用該字詞*行動裝置*。除非我們正在討論功能需要 SMS 訊息通知，例如行動電話訊號字詞行動裝置會套用至手機與平板電腦其他行動裝置。

## Exchange ActiveSync

Exchange ActiveSync 是一種通訊協定，可讓行動裝置以無線提供的方式存取電子郵件、排程資料、連絡人及工作。可在 Windows 電話及具有 Exchange ActiveSync 功能的協力廠商電話上使用 Exchange ActiveSync。

Exchange ActiveSync提供 Direct Push 技術。Direct Push 會使用加密的 HTTPS 連線已建立並維護行動裝置與伺服器推入新的電子郵件及其他Exchange之間電話的資料。

若要以 MicrosoftExchange Server 2013 使用 Direct Push，您的使用者必須有支援 Direct Push 的行動裝置。

## Exchange ActiveSync 功能

Exchange ActiveSync提供許多不同的功能可讓您以強制執行安全性原則行動裝置上的存取。藉由使用Exchange 2013，您可以設定多個行動裝置信箱原則和控制哪些行動裝置可以與Exchange伺服器進行同步處理。Exchange ActiveSync可讓您傳送擦去行動裝置的所有資料以防遺失或竊該行動裝置的遠端裝置抹除命令。使用者也可以啟動Outlook Web App從遠端裝置抹除。

Exchange ActiveSync可讓使用者產生的復原密碼。此復原密碼儲存在行動裝置上\] 和 \[使用者忘記其密碼時所使用。使用者會在同一時間產生裝置密碼或 PIN 產生復原密碼。此復原密碼可用來解除鎖定行動裝置。立即使用此復原密碼後，使用者必須建立新的 PIN。

## POP3 及 IMAP4

如果您的行動裝置不支援 Exchange ActiveSync 或您不需要 Exchange ActiveSync 提供豐富的功能集，您可以使用 POP3 或 IMAP4 存取行動裝置上的電子郵件。如需 POP3 和 IMAP4 存取信箱的詳細資訊，請參閱[Exchange Server 2013 中的 POP3 和 IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md)。

