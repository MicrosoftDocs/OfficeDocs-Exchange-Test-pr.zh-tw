﻿---
title: '移除 E.164 號碼: Exchange Online Help'
TOCTitle: 移除 E.164 號碼
ms:assetid: 17941918-7dc5-41a0-b540-09f2f907362b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ662759(v=EXCHG.150)
ms:contentKeyID: 50553941
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 移除 E.164 號碼

 

_**適用版本：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：** 2012-11-14_

如果您啟用 UM 的使用者將它們連結到撥號對應表 E.164，會建立兩個 EUM proxy 位址。其中包含使用者的分機號碼與另一個包含使用者的 E.164 號碼。當使用者撥打 Outlook 語音存取號碼使用分機號碼。

您可以移除使用者已啟用 um 時新增主要 E.164 電話號碼或更新版本中，以及使用者 EUM proxy 位址新增次要 E.164 號碼。您新增當使用者已啟用 um 的主要 E.164 號碼會列為主要 EUM proxy 位址。您已新增任何其他 E.164 號碼會列為次要 EUM proxy 位址。當移除 E.164 號碼時，來電者可以不再保留使用者的語音信箱的已移除的 E.164 號碼。

如果您移除主要的 E.164 電話號碼，UM 不能夠將語音郵件傳送給使用者的信箱與通話將不會處理自動答錄服務規則。移除主要的 E.164 電話號碼之後，使用者 EUM proxy 位址會被列為**Null**使用者的信箱在 EAC 中與您在命令介面中執行**Get-Mailbox**指令程式上。此外，當您執行**Get-UMMailbox**指令程式， *Extensions*、 *PhoneNumber*，以及*CallAnsweringRulesExtensions*參數會是空白或 null。

您可以使用 EAC 或命令介面移除主要或次要的 E.164 號碼的使用者。您可以使用 EAC 中的使用者的信箱上的 \[**電子郵件地址**\] 頁面上移除主要或次要的 E.164 號碼。您無法使用 EAC 中的 \[ **UM 信箱**\] 頁面上来移除的主要或次要 E.164 號碼。

您可以在命令介面中使用 **Get-UMMailbox** Cmdlet 或 **Get-Mailbox** Cmdlet，檢視使用者的主要和次要 E.164 號碼。

如需與啟用語音信箱的使用者相關的其他管理工作，請參閱[擁有郵件功能的語音使用者程序](voice-mail-enabled-user-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：3 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 信箱」項目。

  - 執行此程序之前，請確認已建立 E.164 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](https://docs.microsoft.com/zh-tw/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan)。

  - 執行此程序之前，請確認已建立 UM 信箱原則。如需詳細步驟，請參閱[建立 UM 信箱原則](https://docs.microsoft.com/zh-tw/exchange/voice-mail-unified-messaging/set-up-voice-mail/create-um-mailbox-policy)。

  - 執行這些程序之前，請確認使用者的信箱已啟用 UM 和連結至撥號對應表 E.164。如需詳細步驟，請參閱[啟用使用者的語音信箱](https://docs.microsoft.com/zh-tw/exchange/voice-mail-unified-messaging/set-up-voice-mail/enable-a-user-for-voice-mail)。

  - 執行這些程序之前，請確認已為使用者設定主要和次要 E.164 號碼。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。


> [!TIP]  
> 有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.




## 您要執行的工作

## 使用 EAC 以移除主要和次要 E.164 號碼

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[信箱\]。

2.  在清單檢視中，選取您要移除 E.164 號碼的信箱，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[**使用者信箱**\] 頁面上的 \[**電子郵件地址**\] 中，選取您要從清單中移除的 E.164 號碼\] 和 \[**刪除**![刪除圖示](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "刪除圖示")。主要 EUM proxy 位址或 E.164 號碼會列於粗體字母和數字。

4.  按一下 \[儲存\]。

## 使用命令介面以移除主要和次要 E.164 號碼

此範例會從啟用 UM 功能之使用者 Tony Smith 的信箱中移除 E.164 號碼 +14255551010。


> [!NOTE]  
> 使用命令介面 E.164 號碼移除之前，您必須判斷您要修改之 EUM proxy 位址的位置。若要判斷位置，請使用<strong>$mbx.EmailAddresses</strong>命令。在清單中的第一個 EUM proxy 位址會是 0。




    $mbx = Get-Mailbox tony.smith
    $mbx.EmailAddresses.Item(1) -="eum:+14255551010;phone-context=MyDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

