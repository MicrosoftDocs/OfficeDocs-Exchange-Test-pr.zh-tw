---
title: '設定語音郵件預覽協力廠商地址: Exchange Online Help'
TOCTitle: 設定語音郵件預覽協力廠商地址
ms:assetid: 57fbed1e-1b14-4939-95e6-ef7c072f32a9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ff630917(v=EXCHG.150)
ms:contentKeyID: 51409180
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定語音郵件預覽協力廠商地址

 

_**適用版本：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：** 2013-02-13_

您可以在整合通訊 (UM) 信箱原則上設定語音郵件預覽協力廠商地址。您已設定 UM 信箱原則的語音郵件預覽協力廠商地址後，設定會套用至所有已啟用 UM 之使用者所連結與該信箱原則。


> [!NOTE]  
> 您必須使用命令介面來設定語音信箱預覽協力程式位址。




如需「語音信箱預覽」合作夥伴程式的相關資訊，請參閱 [語音郵件預覽顧問](https://docs.microsoft.com/zh-tw/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/voice-mail-preview-advisor)。

如需與語音信箱預覽相關的其他管理工作，請參閱[語音郵件預覽程序](https://docs.microsoft.com/zh-tw/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/voice-mail-preview-procedures)。

## 開始之前有哪些須知？

  - 預估完成時間： 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 信箱原則」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](https://docs.microsoft.com/zh-tw/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan)。

  - 執行這些程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 信箱原則](https://docs.microsoft.com/zh-tw/exchange/voice-mail-unified-messaging/set-up-voice-mail/create-um-mailbox-policy)。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。


> [!TIP]  
> 有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.




## 使用命令介面在 UM 信箱原則中設定語音信箱預覽協力程式位址

此範例會在名為 *MyUMMailboxPolicy* 的 UM 信箱原則中，將語音信箱預覽協力程式位址設定為 exumvmp@fabrikam.com。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -VoiceMailPreviewPartnerAddress exumvmp@fabrikam.com

