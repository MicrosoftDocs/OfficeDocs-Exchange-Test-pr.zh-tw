---
title: '擷取語音信箱的 PIN 資訊: Exchange Online Help'
TOCTitle: 擷取語音信箱的 PIN 資訊
ms:assetid: 01517cca-99fe-46b2-b586-19e8d2707728
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa995900(v=EXCHG.150)
ms:contentKeyID: 54652544
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 擷取語音信箱的 PIN 資訊

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-04-03_

您可以擷取已啟用的整合通訊 (UM) 之使用者的 PIN 資訊。使用者已啟用之後已啟用 UM 和 PIN 會產生或建立、 PIN 已加密及儲存在使用者的信箱。

當您擷取已啟用 UM 之使用者的 PIN 資訊時，請使用加密儲存在使用者信箱的 PIN 資料計算傳回給您的資訊。這可讓您檢視資訊從使用者的信箱，而且還會指出移出信箱的使用者是否已鎖定。

如需與 PIN 碼安全性相關的其他工作，請參閱 [PIN 安全性程序](pin-security-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 撥號對應表」項目。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 信箱」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

  - 執行這些程序之前，請確認已建立 UM 信箱原則。如需詳細步驟，請參閱[建立 UM 信箱原則](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 執行這些程序之前，請確認有已啟用 UM 的使用者的信箱。如需詳細步驟，請參閱[啟用使用者的語音信箱](enable-a-user-for-voice-mail-exchange-2013-help.md)。

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

## 使用 EAC 來擷取已啟用 UM 之使用者的 PIN 碼資訊

1.  在 EAC 中，瀏覽至 \[**收件者**。在清單檢視中，選取您要檢視的使用者信箱。

2.  在詳細資料窗格的 **\[電話和語音功能\]** 下方，按一下 **\[檢視詳細資料\]**。

3.  在 \[ **UM 信箱**\] 頁面上 \> \[ **UM 信箱設定**\] 中，檢視**PIN 狀態**的使用者。在此頁面上，您也可以重設使用者的語音信箱 pin 碼。

## 使用命令介面擷取已啟用 UM 之使用者的 PIN 碼資訊

此範例會顯示使用者識別碼、PIN 碼是否到期、UM 信箱是否已鎖定，以及 Tony 是否為新手使用者。

    Get-UMMailboxPIN -identity tony@contoso.com

