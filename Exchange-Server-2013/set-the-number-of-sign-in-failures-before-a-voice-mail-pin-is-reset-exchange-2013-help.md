---
title: '設定 pin 碼重設語音信箱前的登入失敗的次數: Exchange Online Help'
TOCTitle: 設定 pin 碼重設語音信箱前的登入失敗的次數
ms:assetid: 4de38499-0a6f-4f00-8697-eeff805d7266
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa997939(v=EXCHG.150)
ms:contentKeyID: 50553986
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定 pin 碼重設語音信箱前的登入失敗的次數

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-22_

您可以將重設 Outlook Voice Access 使用者的 PIN 碼之前允許的登入失敗次數設定為介於 1 到 998 之間的數字。預設值為 5。重設 PIN 碼之前允許的登入失敗次數是在整合通訊 (UM) 信箱原則上設定，並且套用至與該 UM 信箱原則相關聯的所有 Outlook Voice Access 使用者。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您可以將 [重設 PIN 碼前允許的登入失敗次數] 設定為小於 5 的數字，以提高安全性。將該設定設定為大於 5 的數字，則會降低安全性。</td>
</tr>
</tbody>
</table>


如需與 Outlook 語音存取 PIN 碼安全性相關的其他工作資訊，請參閱 [PIN 安全性程序](pin-security-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：3 分鐘。

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

## 使用 EAC 設定重設 PIN 碼之前的登入失敗次數

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。

2.  在清單檢視中，選取您要變更的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[UM 撥號對應表\] 頁面中的 \[UM 信箱原則\] 之下，選取您要變更的 UM 信箱原則，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

4.  按一下 \[PIN 碼原則\]，然後在 \[重設 PIN 碼前允許的登入失敗次數\] 旁輸入介於 0 和 999 之間的值。

5.  按一下 \[儲存\]。

## 使用命令介面設定重設 PIN 碼之前的登入失敗次數

此範例會針對與名為 `MyUMMailboxPolicy` 的 UM 信箱原則相關聯並已啟用 UM 的使用者，將使用者 PIN 碼重設之前的登入失敗次數設定為 3。

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 3

此範例針對與名為 `MyUMMailboxPolicy` 之 UM 信箱原則相關聯的已啟用 UM 使用者，將重設使用者 PIN 碼前的登入失敗次數設定為 3、登入嘗試次數上限設定為 5，且 PIN 碼長度下限設定為 9。

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 3 -MaxLogonAttempts 5 -MinPINLength 9

