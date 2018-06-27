---
title: '停用使用者的語音信箱: Exchange Online Help'
TOCTitle: 停用使用者的語音信箱
ms:assetid: cecc9c0d-377d-489e-9db4-d487e9c0b552
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124691(v=EXCHG.150)
ms:contentKeyID: 50474247
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 停用使用者的語音信箱

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2012-11-05_

您可以停用已啟用 UM 的使用者的整合通訊 (UM)。當您這麼做時，使用者無法再使用整合通訊中的語音信箱功能。如果您偏好，當您停用 UM 的使用者，您可以保留使用者的 UM 設定。

如需與啟用語音信箱之使用者相關的其他管理工作，請參閱[擁有郵件功能的語音使用者程序](voice-mail-enabled-user-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 信箱」項目。

  - 執行此程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

  - 執行此程序之前，請確認已建立 UM 信箱原則。如需詳細步驟，請參閱[建立 UM 信箱原則](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 執行這些程序之前，請確認現有使用者目前已啟用整合通訊。如需詳細步驟，請參閱[啟用使用者的語音信箱](enable-a-user-for-voice-mail-exchange-2013-help.md)。

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

## 使用 EAC 為使用者停用整合通訊及語音信箱

1.  在 EAC 中，按一下 \[收件者\]。

2.  在清單檢視中，選取您要對於整合通訊停用信箱的使用者。

3.  在 \[詳細資料\] 窗格中，於 \[電話和語音功能\] 的 \[整合通訊\] 下方，按一下 \[停用\]。

4.  在 \[警告\] 方塊中，按一下 \[是\] 確認要停用該使用者的整合通訊。

## 使用命令介面為使用者停用整合通訊及語音信箱

此範例會停用使用者 tonysmith@contoso.com 的整合通訊及語音信箱，但保留 UM 信箱設定。

    Disable-UMMailbox -Identity tonysmith@contoso.com -KeepProperties $True

