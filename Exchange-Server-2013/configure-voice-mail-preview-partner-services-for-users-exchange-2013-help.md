---
title: '設定使用者的語音郵件預覽合作夥伴服務: Exchange Online Help'
TOCTitle: 設定使用者的語音郵件預覽合作夥伴服務
ms:assetid: 7bb914ca-5502-4e64-bae5-555034138d8a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ff630920(v=EXCHG.150)
ms:contentKeyID: 51409219
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定使用者的語音郵件預覽合作夥伴服務

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2016-12-09_

您可以在整合通訊 (UM) 信箱原則上設定語音郵件預覽協力廠商。您已在 UM 信箱原則上設定語音郵件預覽協力廠商設定，例如語音郵件預覽協力廠商識別碼和語音郵件預覽協力廠商地址後，您設定會套用至所有已啟用 UM 之使用者所連結與該信箱原則。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您必須使用命令介面來設定語音信箱預覽協力程式。</td>
</tr>
</tbody>
</table>


如需其他與 UM 信箱原則相關的管理工作，請參閱 [UM 信箱原則程序](um-mailbox-policy-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 信箱原則」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

  - 執行這些程序之前，請確認已建立 UM 信箱原則。如需詳細步驟，請參閱[建立 UM 信箱原則](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 該怎麼做？

## 步驟 1： 註冊與合作夥伴服務

若要尋找認證的合作夥伴和詳細的說明如何註冊的清單，請參閱[語音郵件預覽顧問](voice-mail-preview-advisor-exchange-2013-help.md)或請參閱[Microsoft PinPoint](https://go.microsoft.com/fwlink/p/?linkid=281966)網站。您已註冊之後，您的協力廠商識別碼及 SMTP 地址使用轉寄的語音訊息提供語音郵件預覽協力廠商。

在步驟 2 中，您會將從步驟 1 中取得的協力程式識別碼和 SMTP 位址套用至所需的 UM 信箱原則。

## 步驟 2： 設定語音郵件預覽協力廠商地址和 ID

此範例在名為 *MyUMMailboxPolicy* 的 UM 信箱原則上，將語音信箱預覽協力程式位址設為 exumvmp@fabrikam.com，並將語音信箱預覽協力程式識別碼設為 CON123-2010。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -VoiceMailPreviewPartnerAddress exumvmp@fabrikam.com
    -VoiceMailPreviewPartnerAssignedID CON123-2010

## 步驟 3： 設定進階語音郵件預覽協力廠商設定

如果協力程式需要自訂設定，您可能要為語音信箱預覽協力程式設定其他兩個參數，如下所示：

  - *VoiceMailPreviewPartnerMaxMessageDuration*

  - *VoiceMailPreviewPartnerMaxDeliveryDelay*

此範例在名為 *MyUMMailboxPolicy* 的 UM 信箱原則上，將最長訊息持續時間設為 300 秒 (5 分鐘)，並將最長傳遞延遲設為 600 秒 (10 分鐘)。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -VoiceMailPreviewPartnerMaxMessageDuration 300 -VoiceMailPreviewPartnerMaxDeliveryDelay 600

## 步驟 4： 將啟用 UM 的使用者指派給 UM 信箱原則的語音信箱預覽協力廠商

如果您想要設定一些，但不是所有的語音郵件預覽合作夥伴服務、 已啟用 UM 之使用者的 UM 撥號對應，您必須建立新的 UM 信箱原則及協力廠商進行設定。後完成，您可以套用新的原則選取 um 的使用者。如需如何將已啟用 UM 的使用者指派給 UM 信箱原則的詳細資訊，請參閱下列主題：

  - [UM 信箱原則指派](assign-a-um-mailbox-policy-exchange-2013-help.md)

  - [Set-UMMailbox](https://technet.microsoft.com/zh-tw/library/bb124893\(v=exchg.150\))

如需「語音信箱預覽」合作夥伴程式的相關資訊，請參閱 [語音郵件預覽顧問](voice-mail-preview-advisor-exchange-2013-help.md)。

