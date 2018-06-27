---
title: '設定 Outlook 語音存取 PIN 原則: Exchange Online Help'
TOCTitle: 設定 Outlook 語音存取 PIN 原則
ms:assetid: 5b2800b7-bfa6-4282-975c-0706ae25ad64
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa998285(v=EXCHG.150)
ms:contentKeyID: 50553996
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定 Outlook 語音存取 PIN 原則

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-22_

您可以在整合通訊 (UM) 信箱原則上設定 PIN 原則。UM 信箱原則可用來增加使用 Outlook 語音存取所需以符合組織的預先定義的 PIN 原則的使用者啟用 UM 之使用者的安全性層級。

若要設定 Outlook 語音存取使用者的 PIN 原則，您可以建立新的 UM 信箱原則或修改現有的 UM 信箱原則。建立新的 UM 信箱原則之後，您可以再 PIN 設定下列設定 UM 信箱原則：

  - `MinPasswordLength`

  - `PINLifetime`

  - `LogonFailuresBeforePINReset`

  - `MaxLogonAttempts`

  - `AllowCommonPatterns`

  - `PINHistoryCount`

它是安全性的最佳作法來實作強式的 UM 使用者的 pin 碼需求。這可以透過建立需要 6 或多個字的 Pin，並增加為您的網路安全性層級的 UM PIN 原則強制執行。

變更的 PIN 原則後，新的 pin 碼設定會套用到目前關聯的 UM 信箱原則的使用者。例如，如果您修改的 UM 信箱原則並將最小 PIN 長度從 7 變更為 10 的數字下, 一次使用者登入他們將強制變更其 PIN 遵守已變更的 pin 碼需求。

如需了解與 Outlook 語音存取 PIN 碼安全性相關的其他工作，請參閱 [PIN 安全性程序](pin-security-procedures-exchange-2013-help.md)。

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


## 您要執行的工作

## 使用 EAC 設定 Outlook 語音存取使用者的 PIN 碼原則

1.  在 EAC 中，瀏覽至 \[**整合通訊**\> **UM 撥號對應表**。在清單檢視中，按一下您想要編輯的 UM 撥號對應表計劃和 \[**編輯**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 \[UM 撥號對應表\] 頁面的 \[UM 信箱原則\] 下方，選取您要編輯的 UM 信箱原則，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  按一下 \[內容\]。

4.  在 \[UM 信箱原則\] 頁面上，按一下 \[PIN 碼原則\]。

5.  在 \[PIN 碼原則\] 頁面上，設定與此 UM 信箱原則相關聯之 Outlook Voice Access 使用者的 PIN 碼設定，然後按一下 \[儲存\]。

## 使用命令介面設定 Outlook 語音存取使用者的 PIN 碼原則

這個範例可為與 UM 信箱原則 `MyUMMailboxPolicy` 相關聯的使用者設定 PIN 碼設定。

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 8 -MaxLogonAttempts 12 -MinPINLength 8 -PINHistoryCount 10 -PINLifetime 60 -ResetPINText "The PIN used to allow you access to your mailbox using Outlook Voice Access has been reset."

