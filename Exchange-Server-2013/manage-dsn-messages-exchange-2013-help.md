---
title: '管理 DSN 郵件: Exchange 2013 Help'
TOCTitle: 管理 DSN 郵件
ms:assetid: 23c9d844-6fc7-44c9-a308-587338281611
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa996803(v=EXCHG.150)
ms:contentKeyID: 50472716
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理 DSN 郵件

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2013-02-20_

Microsoft Exchange Server 2013使用傳遞狀態通知 (DSN) 來提供給郵件寄件者的未傳遞回報 (Ndr) 及其他狀態的郵件。您可以使用內建 Dsn，或是您可以建立自訂 DSN 郵件以符合組織的需求。

## 開始之前有哪些須知？

  - 預估完成時間：15 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「DSN」項目。

  - 您無法移除 Exchange 具有隨附的內建 DSN 郵件。若要變更的內建 DSN 郵件，您需要建立您要自訂的 DSN 代碼的自訂 DSN 郵件。當您移除的自訂 DSN 郵件時，該訊息相關聯的 DSN 代碼會回復成 Exchange 有包含內建 DSN 郵件。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 您要執行的工作

## 使用命令介面來檢視內建與自訂的 DSN 訊息

若要檢視包含於 Exchange 2013 之所有內建的 DSN 訊息摘要，請執行下列命令：

    Get-SystemMessage -Original

若要檢視組織中所有自訂的 DSN 訊息摘要，請執行下列命令：

    Get-SystemMessage

若要檢視 DSN 碼 5.1.2 以英文傳送至內部寄件者的自訂 DSN 訊息，請執行下列命令：

    Get-SystemMessage En\Internal\5.1.2 | Format-List

## 使用命令介面來建立自訂 DSN 訊息

執行下列命令：

    New-SystemMessage -Internal <$true | $false> -Language <Locale> -DSNCode <x.y.z> -Text "<DSN text>"

本範例建立DSN 碼 5.1.2 以英文傳送至內部寄件者的自訂純文字 DSN 訊息。

    New-SystemMessage -Internal $true -Language En -DSNCode 5.1.2 -Text "You tried to send a message to a disabled mailbox that's no longer accepting messages. Please contact the Help Desk at extension 123 for assistance."

本範例建立DSN 碼 5.1.2 以英文傳送至外部寄件者的自訂純文字 DSN 訊息。

    New-SystemMessage -Internal $false -Language En -DSNCode 5.1.2 -Text "You tried to send a message to a disabled mailbox that's no longer accepting messages. Please contact your System Administrator for more information."

本範例建立DSN 碼 5.1.2 以英文傳送至內部寄件者的自訂 HTML DSN 訊息。

    New-SystemMessage -DSNCode 5.1.2 -Internal $true -Language En -Text 'You tried to send a message to a <B>disabled</B> mailbox. Please visit <A HREF="http://it.contoso.com">Internal Support</A> or contact &quot;InfoSec&quot; for more information.'

## 如何才能了解這是否正常運作？

若要驗證您是否已成功建立自訂 DNS 訊息，執行下列操作：

1.  執行下列命令：
    
        Get-SystemMessge -DSNCode <x.y.z> | Format-List Name,Internal,Text,Language

2.  請確認您所看到的值是您所設定的值。

3.  傳送測試郵件，將產生您設定的自訂 DSN。

## 使用命令介面變更自訂 DSN 郵件文字

若要變更自訂 DSN 訊息的文字請執行下列命令：

    Set-SystemMessage <Locale>\<Internal | External>\<DSNcode> -Text "<DSN text>"

本範例變更指定給文字的 DSN 碼 5.1.2 以英文傳送至內部寄件者 DSN 訊息。

    Set-SystemMessage En\Internal\5.1.2 -Text "The mailbox you tried to send an e-mail message to is disabled and is no longer accepting messages. Please contact the Help Desk at extension 123 for assistance."

## 如何才能了解這是否正常運作？

若要驗證您是否已成功變更自訂 DNS 訊息的文字，執行下列操作：

1.  執行下列命令： `Get-SystemMessage`。
    
        Set-SystemMessage <Locale>\<Internal | External>\<DSNcode> | Format-List -Text

2.  請確認顯示的值是您所設定的值。

## 使用命令介面來移除自訂 DSN 訊息

執行下列命令：

    Remove-SystemMessage <Local>\<Internal | External>\<DSNcode>

本範例移除 DSN 碼 5.1.2 以英文傳送至內部寄件者的自訂 DSN 訊息。

    Remove-SystemMessage En\Internal\5.1.2

## 如何才能了解這是否正常運作？

若要驗證您是否已成功移除自訂 DNS 訊息，執行下列操作：

1.  執行命令 ︰ `Get-SystemMessage`。

2.  驗證地點的 DSN、內部或外部收件者、以及您刪除且未列出的 DSN 碼。

## 轉寄 DSN 訊息的複本至 Exchange 收件者信箱

您可以指定您想要監視藉由複製到 Exchange 收件者的信箱 DSN 郵件的 DSN 代碼清單。不過，根據預設，沒有信箱被指派給 Exchange 收件者讓所有 Exchange 收件者會都捨棄傳送郵件。若要將 DSN 郵件的複本傳送至 Exchange 收件者信箱，您需要指派信箱到 Exchange 收件者，然後特定您想要監視的 DSN 代碼。根據預設，會監視下列的 DSN 代碼 ︰ `5.4.8`、 `5.4.6`、 `5.4.4`、 `5.2.4`、 `5.2.0`及`5.1.4`。

## 步驟 1： 使用命令介面來指派給 Exchange 收件者的信箱

若要指定信箱給 Exchange 收件者，請執行以下步驟：

1.  因為可能會大量電子郵件、 考慮建立專用的信箱及 Active Directory 使用者帳戶為 Exchange 收件者。如需詳細資訊，請參閱[建立使用者信箱](create-user-mailboxes-exchange-2013-help.md)。否則請找出您想要與 Exchange 收件者建立關聯的現有信箱。

2.  執行下列命令：
    
        Set-OrganizationConfig -MicrosoftExchangeRecipientReplyRecipient <MailboxIdentity>
    
    例如，若要將名為「Contoso 系統信箱」的現有信箱指派給 Exchange 收件者，請執行下列命令：
    
        Set-OrganizationConfig -MicrosoftExchangeRecipientReplyRecipient "Contoso System Mailbox"

## 步驟 2： 指定您想要監視的 DSN 代碼

## 使用 EAC 來指定 DSN 碼

1.  在 EAC 中，瀏覽至 \[郵件流程\] \> \[接收連接器\] \> \[其他選項\]![更多選項圖示](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "更多選項圖示") \> \[組織傳輸設定\] \> \[傳遞\]。

2.  在 \[ **DNS 代碼**\] 區段中，輸入您要監視使用格式*\<x.y.z\>*中，按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")的 DSN 代碼。選取現有的項目並按一下 \[**編輯**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")進行修改，或按一下 \[**移除**![\[移除\] 圖示](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[移除] 圖示")將其移除。完成時，按一下 \[**儲存**\]。

## 使用命令介面來指定 DSN 碼

若要取代現有的值，請執行下列命令：

    Set-TransportConfig -GenerateCopyOfDSNFor <x.y.z>,<x.y.z>...

此範例會設定 Exchange 組織將所有具有 DSN 代碼 5.7.1、5.7.2 及 5.7.3 的 DSN 郵件轉寄至 Exchange 收件者。

    Set-TransportConfig -GenerateCopyOfDSNFor 5.7.1,5.7.2,5.7.3

若要新增或移除項目而不修改任何現有的值，請執行下列命令：

    Set-TransportConfig -GenerateCopyOfDSNFor @{Add="<x.y.z>","<x.y.z>"...; Remove="<x.y.z>","<x.y.z>"...}

此範例將新增 DSN 碼 5.7.5 並自轉寄給 Exchange 受件者的現有 DSN 訊息清單移除 DSN 碼 5.7.1。

    Set-TransportConfig -GenerateCopyOfDSNFor @{Add="5.7.5"; Remove="5.7.1"}

## 如何才能了解這是否正常運作？

若要驗證您是否已成功設定 DSN 訊息複本發送至 Exchange 收件者的信箱，需監控與 Exchange 收件者相關的信箱，並且驗證 DSN 訊息包含您指定的 DSN 碼。

