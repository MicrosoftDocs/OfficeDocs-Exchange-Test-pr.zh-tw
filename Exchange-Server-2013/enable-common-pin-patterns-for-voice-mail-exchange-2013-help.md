---
title: '啟用語音信箱的常見 PIN 模式: Exchange Online Help'
TOCTitle: 啟用語音信箱的常見 PIN 模式
ms:assetid: 9940a8c2-f576-4089-ab96-8b318ad3da0f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ673546(v=EXCHG.150)
ms:contentKeyID: 50554044
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟用語音信箱的常見 PIN 模式

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-22_

您可以啟用或停用共同Outlook語音存取使用者的整合通訊 (UM) PIN 模式。如果您啟用或停用 UM 信箱原則上設定的通用 PIN 模式，請設定會套用至所有已啟用 UM 之使用者的 UM 信箱原則相關聯。預設已啟用 UM 的使用者無法使用常見模式時所建立的 PIN。

您可以在 UM 信箱原則上設定 pin 碼相關的數個設定。**允許常見 PIN 模式**設定用來允許或防止使用者建立 PIN 時使用一般的數字模式。根據預設，此設定會停用並讓使用者無法使用下列的號碼模式：

  - **循序號碼**  這些是包含連續的數字的 PIN 值。連續 PIN 號碼的範例會為 1234年與 65432。

  - **重複的數字**  這些是包含重複數字的 PIN 值。重複的數字的範例是 11111 和 22222。

  - **後置詞信箱分機號碼**  這些是 PIN 值包含使用者的信箱分機號碼的後置詞。例如，如果使用者的信箱分機號碼為 36697、 使用者的 PIN 不能 3669712。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果 [允許共同 PIN 碼模式] 設定已啟用，只有信箱分機號碼的尾碼會被拒絕。</td>
</tr>
</tbody>
</table>


如需與 Outlook 語音存取 PIN 碼安全性相關的其他工作資訊，請參閱 [PIN 安全性程序](pin-security-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

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

## 使用 EAC 啟用共同的 PIN 碼模式

1.  在 EAC 中，瀏覽至 \[**整合通訊**\> **UM 撥號對應表**。在清單檢視中，選取您要修改的 UM 撥號，然後按一下工具列上的 \[**編輯**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 \[UM 撥號對應表\] 頁面中的 \[UM 信箱原則\] 之下，選取您要管理的 UM 信箱原則，然後按一下工具列上的 \[編輯\]**Edit**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[UM 信箱原則\] 頁面的 \[PIN 碼原則\] 下，勾選 \[允許共同的 PIN 碼模式\] 旁的核取方塊。

4.  按一下 \[儲存\]。

## 使用命令介面啟用共同的 PIN 碼模式

此範例讓與名為 `MyUMMailboxPolicy` 的 UM 信箱原則關聯的使用者使用包含共同模式的 PIN 碼。

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -AllowCommonPatterns $true

