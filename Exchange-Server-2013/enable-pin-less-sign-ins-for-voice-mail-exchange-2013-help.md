---
title: '啟用 PIN 較不登入的語音信箱: Exchange 2013 Help'
TOCTitle: 啟用 PIN 較不登入的語音信箱
ms:assetid: 54133753-317c-42ef-9b0d-ca9f2d2d6bd7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg602127(v=EXCHG.150)
ms:contentKeyID: 54652583
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟用 PIN 較不登入的語音信箱

 

_**適用版本：**Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2015-04-08_

您可以設定整合通訊 (UM) 設定您的使用者可以登入其語音郵件而不需使用 PIN。根據預設，會提示Outlook語音存取使用者輸入來登入其信箱並存取其語音信箱、 電子郵件、 行事曆、 個人連絡人、 目錄和個人選項的 PIN。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>對於啟用語音信箱的單一使用者或使用者群組來說，啟用不需 PIN 碼登入會降低語音信箱的安全性等級，對組織造成安全性風險。</td>
</tr>
</tbody>
</table>


若要啟用 PIN 較不登入，您必須`$true`參數*AllowPinlessVoiceMailAccess*設在 UM 信箱原則並將參數*PinlessAccessToVoiceMailEnabled*設定 UM 信箱`$true` 。根據預設，這兩個參數會設為`$false`，需要Outlook語音存取使用者存取其語音信箱時輸入其 PIN。

將這兩個參數設定為`$true`可讓您啟用 PIN 較不登入語音大型群組相關聯的 UM 信箱的使用者信箱並也啟用 PIN 較不登入的單一的 UM 信箱\] 或 \[UM 信箱的子集。即使您啟用 PIN 較不登入群組已啟用 UM 的使用者或單一已啟用 UM 之使用者的語音信箱存取電子郵件、 行事曆、 個人連絡人、 目錄或個人選項時，他們將會提示您輸入他們的 pin 碼。

若要讓使用者不需 PIN 碼即可登入語音信箱，必須滿足以下條件：

  - 您是否已在 UM 信箱原則上執行下列 cmdlet： `Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowPinlessVoiceMailAccess $true`

  - 您是否已啟用 UM 之使用者的信箱上執行下列 cmdlet： `Set-UMMailbox -id tonys@contoso.com -PinlessAccessToVoiceMailEnabled $true`

  - 已啟用 UM 功能的使用者與您啟用不需 PIN 碼登入的 UM 信箱原則相關聯。

  - 已啟用 UM 功能的使用者是從指派的電話號碼撥入 Outlook Voice Access。

  - 您只能使用命令介面來執行此程序。 若要了解如何在內部部署 Exchange 組織中開啟 Exchange 管理命令介面，請參閱[開啟命令介面。](https://technet.microsoft.com/zh-tw/library/dd638134\(v=exchg.150\))。 若要了解如何使用 Windows PowerShell 連線到 Exchange Online，請參閱[連線到 Exchange Online Protection PowerShell](https://go.microsoft.com/fwlink/p/?linkid=396554)。

如需其他與 UM 信箱原則相關的管理工作，請參閱[UM 信箱原則程序](um-mailbox-policy-procedures-exchange-2013-help.md)。

如需與 UM 信箱相關的其他工作，請參閱[擁有郵件功能的語音使用者程序](voice-mail-enabled-user-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：3 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 信箱原則」項目。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 信箱」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

  - 執行這些程序之前，請確認已建立 UM 信箱原則。如需詳細步驟，請參閱[建立 UM 信箱原則](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 執行這些程序之前，請確認該使用者已啟用 UM 和語音信箱。如需詳細步驟，請參閱[啟用使用者的語音信箱](enable-a-user-for-voice-mail-exchange-2013-help.md)。

## 您要執行的工作

## 使用命令介面針對 UM 信箱原則上已啟用 UM 功能的使用者啟用不需 PIN 碼的語音信箱存取

這個範例會針對與信箱原則相關聯且撥入 Outlook 語音存取的使用者，在名為 `MyUMMailboxPolicy` 的 UM 信箱原則上啟用不需 PIN 碼的語音信箱存取。

    Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowPinlessVoiceMailAccess $true

## 使用命令介面在已啟用 UM 功能的使用者信箱上啟用不需 PIN 碼的語音信箱存取

這個範例會針對撥入 Outlook Voice Access 以存取 `tonys@contoso.com` 信箱的使用者，啟用不需 PIN 碼的語音信箱存取。

    Set-UMMailbox -id tonys@contoso.com -PinlessAccessToVoiceMailEnabled $true

