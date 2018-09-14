﻿---
title: '新增 SIP 位址: Exchange Online Help'
TOCTitle: 新增 SIP 位址
ms:assetid: 40295bcf-c62b-4f26-95ca-a8c4bd210fb3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ662760(v=EXCHG.150)
ms:contentKeyID: 50553972
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 新增 SIP 位址

 

_**適用版本：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：** 2012-11-14_

當您啟用 UM 的使用者並將它們連結到的 SIP URI 撥號對應表時，會建立兩個 EUM proxy 位址。其中包含使用者的分機號碼與另一個包含使用者的 SIP 位址。當使用者撥打 Outlook 語音存取號碼使用分機號碼。

您正在整合 UM 與 Microsoft Office Communications Server 2007 R2 或 Microsoft Lync Server 使用的 SIP URI 撥號對應表和 SIP 位址。SIP 位址是 Communications Server 或 Lync Server 用來路由傳送來電轉接和語音信箱傳送給使用者。根據預設，UM 所使用的 SIP 位址會 Communications Server 或 Lync Server 所使用的 SIP 位址。

您新增當使用者已啟用 um 的主要 SIP 位址會列為主要 EUM proxy 位址。已移除的主要的 SIP 位址，如果您新增包含使用者的 SIP 位址的第一個 EUM proxy 位址會被列為主要 EUM proxy 位址。您新增任何其他 SIP 位址會列為次要 EUM proxy 位址。新增次要的 SIP 位址時, 來電者可以保留使用者的語音信箱的 SIP 端點可以使用的 SIP 位址的使用者登入。所有的語音訊息將會傳遞至相同的使用者信箱。

您可以使用 EAC 或命令介面新增主要或次要 SIP 位址的使用者。您可以使用 EAC 中的使用者的信箱上的 \[**電子郵件地址**\] 頁面上新增主要或次要 SIP 位址。您無法使用 EAC 中的 \[ **UM 信箱**\] 頁面上新增主要或次要 SIP 位址。

您可以在命令介面中使用 **Get-UMMailbox** Cmdlet 或 **Get-Mailbox** Cmdlet，檢視使用者的主要和次要 SIP 位址。

如需與啟用語音信箱的使用者相關的其他管理工作，請參閱[擁有郵件功能的語音使用者程序](voice-mail-enabled-user-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：3 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 信箱」項目。

  - 執行這些程序之前，請確認已建立 UM SIP URI 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](https://docs.microsoft.com/zh-tw/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan)。

  - 執行這些程序之前，請確認已建立 UM 信箱原則。如需詳細步驟，請參閱[建立 UM 信箱原則](https://docs.microsoft.com/zh-tw/exchange/voice-mail-unified-messaging/set-up-voice-mail/create-um-mailbox-policy)。

  - 執行這些程序之前，請確認現有的使用者已啟用 UM 和連結至 SIP URI 撥號對應表。如需詳細步驟，請參閱[啟用使用者的語音信箱](https://docs.microsoft.com/zh-tw/exchange/voice-mail-unified-messaging/set-up-voice-mail/enable-a-user-for-voice-mail)。

  - 執行這些程序之前，請先確認將指派給使用者的 SIP 位址有效且已正確格式化。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。


> [!TIP]  
> 有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.




## 您要執行的工作

## 使用 EAC 以新增主要或次要 SIP 位址

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[信箱\]。

2.  在清單檢視中，選取您要新增 SIP 位址的信箱，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[使用者信箱\] 頁面中，按一下 \[電子郵件地址\] 底下的 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

4.  在 \[新增電子郵件地址\] 頁面中，選取 \[EUM\]，然後在 \[地址/分機\] 方塊中輸入使用者的新 SIP 位址。

5.  在 \[新增電子郵件地址\] 頁面中，按一下 \[撥號對應表\] 底下的 \[瀏覽\]，以選取 SIP URI 撥號對應表，然後按一下 \[確定\]。

6.  按一下 \[儲存\]。

## 使用命令介面新增 SIP 位址

此範例會為已啟用 UM 的使用者 Tony Smith 新增 SIP 位址。


> [!NOTE]  
> 新增使用命令介面的 SIP 位址之前，您必須判斷您想要新增之 EUM proxy 位址的位置。若要判斷位置，請使用<strong>$mbx.EmailAddresses</strong>命令。在清單中的第一個 proxy 位址會是 0。




    $mbx=Get-Mailbox tony.smith
    $mbx.EmailAddresses +="eum:tsmit@contoso.com;phone-context=MyDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

