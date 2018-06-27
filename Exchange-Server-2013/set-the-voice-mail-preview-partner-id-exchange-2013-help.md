---
title: '設定語音郵件預覽協力廠商識別碼: Exchange Online Help'
TOCTitle: 設定語音郵件預覽協力廠商識別碼
ms:assetid: ab98c320-9952-47a7-b141-ddfc2c0ad419
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ff630924(v=EXCHG.150)
ms:contentKeyID: 51409231
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定語音郵件預覽協力廠商識別碼

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-13_

您可以在整合通訊 (UM) 信箱原則上設定語音郵件預覽協力廠商識別碼。您已設定 UM 信箱原則的語音郵件預覽協力廠商識別碼之後，設定會套用至所有已啟用 UM 之使用者所連結與該信箱原則。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您必須使用命令介面來設定「語音信箱預覽」合作夥伴識別碼。</td>
</tr>
</tbody>
</table>


如需「語音信箱預覽」合作夥伴程式的相關資訊，請參閱 [語音郵件預覽顧問](voice-mail-preview-advisor-exchange-2013-help.md)。

如需與語音信箱預覽相關的其他管理工作，請參閱[語音郵件預覽程序](voice-mail-preview-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 信箱原則」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

  - 執行這些程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 信箱原則](create-a-um-mailbox-policy-exchange-2013-help.md)。

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


## 使用命令介面在 UM 信箱原則上設定語音信箱預覽合作夥伴識別碼

此範例在名為 *MyUMMailboxPolicy* 的信箱原則上將「語音信箱預覽」合作夥伴識別碼設為 CON123-2010。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy 
    -VoiceMailPreviewPartnerAssignedID CON123-2010

