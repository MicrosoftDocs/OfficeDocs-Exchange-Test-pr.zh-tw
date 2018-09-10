﻿---
title: '防止使用者接收傳真: Exchange Online Help'
TOCTitle: 防止使用者接收傳真
ms:assetid: b5d022b9-043a-4324-87fb-074d5e2c2ca3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb201722(v=EXCHG.150)
ms:contentKeyID: 52062393
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 防止使用者接收傳真

 

_**適用版本：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：** 2016-12-09_

防止整合通訊 (UM) 使用者接收傳真\]。了解如何變更為新的和現有的 UM 使用者的傳真設定。

根據預設，當您啟用使用者的整合通訊時所將能夠接收傳真\] 如果您啟用傳真並連結到使用者的 UM 信箱原則上設定傳真協力程式的 URI。傳真可啟用或停用在 UM 撥號對應表計劃、 UM 信箱原則或已啟用 UM 之使用者的信箱。

根據預設，使用者的信箱和連結與該使用者的撥號允許傳入的傳真。不過，使用者接收傳真您必須先啟用已啟用 UM 功能的使用者相關聯並輸入傳真協力程式的 URI 的 UM 信箱原則上輸入傳真。


> [!NOTE]  
> 您可以使用 EAC 設定傳真設定整合通訊信箱原則上。不過，您必須使用命令介面來設定傳真或個別使用者撥號對應表上。




如需傳真協力廠商的詳細資訊，請參閱[Microsoft PinPoint 傳真協力廠商](https://go.microsoft.com/fwlink/?linkid=190238)。

如需與傳真相關的其他管理工作，請參閱[傳真程序](https://docs.microsoft.com/zh-tw/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/faxing-procedures)。

## 開始之前有哪些須知？

  - 預估完成時間： 2 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 信箱原則」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](https://docs.microsoft.com/zh-tw/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan)。

  - 執行這些程序之前，請確認已建立 UM 信箱原則。如需詳細步驟，請參閱[建立 UM 信箱原則](https://docs.microsoft.com/zh-tw/exchange/voice-mail-unified-messaging/set-up-voice-mail/create-um-mailbox-policy)。

  - 執行下列程序之前，請確認使用者已啟用整合通訊。如需詳細步驟，請參閱[啟用使用者的語音信箱](https://docs.microsoft.com/zh-tw/exchange/voice-mail-unified-messaging/set-up-voice-mail/enable-a-user-for-voice-mail)。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。


> [!TIP]  
> 有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.




## 使用命令介面來防止啟用 UM 的使用者接收傳真

此範例會讓已啟用 UM 的使用者 (Tony) 無法在其信箱中接收傳真訊息。

    Set-UMMailbox -Identity tony@contoso.com -FaxEnabled $false

