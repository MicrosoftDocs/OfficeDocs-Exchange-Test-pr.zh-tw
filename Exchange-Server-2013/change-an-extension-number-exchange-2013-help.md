---
title: '變更分機號碼: Exchange Online Help'
TOCTitle: 變更分機號碼
ms:assetid: ff22b366-3bfb-4bf7-9f11-62fba48f1caf
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb232208(v=EXCHG.150)
ms:contentKeyID: 50554110
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 變更分機號碼

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2012-11-14_

當您啟用 UM 的使用者並將它們連結到電話分機撥號時，EUM proxy 位址會建立包含使用者的分機號碼的使用者。您必須定義要使用讓語音信箱可傳送至使用者信箱的 UM 至少一個分機號碼。當使用者撥打 Outlook 語音存取號碼也會使用的分機號碼。

您可以變更已新增當使用者已啟用 um 的主要的分機號碼或更新版本中，以及使用者的相關 EUM proxy 位址新增次要分機號碼。您新增當使用者已啟用 um 的主要的分機號碼會列為主要 EUM proxy 位址。您已新增任何其他的次要分機號碼會列為次要 EUM proxy 位址。當分機號碼已變更時，來電者可以將保留使用者的語音信箱所有已設定的新分機號碼。所有的語音訊息將會傳遞至相同的使用者信箱。

您可以使用 EAC 或命令介面來變更主要或次要分機號碼的使用者。您可以使用 EAC 中的使用者的信箱上的 \[**電子郵件地址**\] 頁面上變更主要或次要分機號碼。您無法在 EAC 中使用 \[ **UM 信箱**\] 頁面上變更主要分機號碼，但是您可以使用它來變更第二的分機號碼。如果您想要變更第二的分機號碼，您必須先移除現有的次要分機號碼並再新增使用者的正確的次要分機號碼。

您可以使用命令介面中的 **Get-UMMailbox** Cmdlet 或 **Get-Mailbox** Cmdlet 檢視使用者的主要或次要分機號碼。

如需與啟用語音信箱的使用者相關的其他管理工作，請參閱[擁有郵件功能的語音使用者程序](voice-mail-enabled-user-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：3 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 信箱」項目。

  - 執行這些程序之前，請確認已建立的電話分機 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

  - 執行這些程序之前，請確認已建立 UM 信箱原則。如需詳細步驟，請參閱[建立 UM 信箱原則](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 執行這些程序之前，請確認使用者的信箱已啟用 UM 和連結至電話分機撥號對應表。如需詳細步驟，請參閱[啟用使用者的語音信箱](enable-a-user-for-voice-mail-exchange-2013-help.md)。

  - 執行這些程序之前，請先確認將指派給使用者的分機號碼包含在 UM 撥號對應表上設定的正確位數。

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


## 您要執行的工作

## 使用 EAC 來變更主要或次要分機號碼

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[信箱\]。

2.  在清單檢視中，選取您要變更分機號碼，的信箱\] 和 \[**編輯**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[**使用者信箱**\] 頁面上的 \[**電子郵件地址**\] 中，選取您想要變更的分機號碼\] 和 \[**編輯**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。主要的分機號碼會列於粗體字母和數字。

4.  在 \[**電子郵件地址**\] 頁面上 \[**地址/副檔名**\] 方塊中輸入新的分機號碼的使用者。如果您需要選取新的 UM 撥號對應，您可以按一下 \[**瀏覽\]**。

5.  按一下 **\[儲存\]**。

## 使用命令介面來變更主要或次要分機號碼

本範例會變更至 22222 Tony smith、 已啟用 UM 之使用者的分機號碼。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>變更使用命令介面分機號碼之前，您必須決定要變更的 EUM proxy 位址的位置。若要判斷位置，請使用<strong>$mbx.EmailAddresses</strong>命令。第一個 EUM proxy 位址是預設值 （主要） 的分機號碼和其 0 清單中。</td>
</tr>
</tbody>
</table>


    $mbx=Get-Mailbox tony.smith
    $mbx.EmailAddresses.Item(0)="eum:22222;phone-context=MyDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

