---
title: '設定語音信箱的最小 PIN 長度: Exchange Online Help'
TOCTitle: 設定語音信箱的最小 PIN 長度
ms:assetid: b2ecab54-42e6-45af-8322-615cc1f68dd9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124271(v=EXCHG.150)
ms:contentKeyID: 50554053
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定語音信箱的最小 PIN 長度

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-22_

您可以設定 Outlook 語音存取使用者已啟用的整合通訊 (UM) 之最小 PIN 長度。您在 UM 信箱原則設定 pin 碼設定會套用至所有已啟用 UM 之使用者的 UM 信箱原則相關聯。

Outlook語音存取已啟用 UM 的使用者用以存取語音信箱、 電子郵件、 行事曆和位於自己的信箱中的個人連絡人資訊。不過，他們就可以存取其信箱之前，他們必須輸入 PIN，以便他們可以驗證語音郵件系統。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您變更的最小 PIN 長度值，現有的 Outlook 語音存取使用者將會提示輸入新的 PIN 前其可以繼續包含新的最小的數字數目。預設值為 6。</td>
</tr>
</tbody>
</table>


如需與 Outlook 語音存取 PIN 碼相關的其他工作，請參閱 [PIN 安全性程序](pin-security-procedures-exchange-2013-help.md)。

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

## 使用 EAC 設定 Outlook 語音存取的最小 PIN 碼長度

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。

2.  在清單檢視中，選取您要變更的撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[UM 撥號對應表\] 頁面中的 \[UM 信箱原則\] 之下，選取您要變更的 UM 信箱原則，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

4.  按一下 \[PIN 碼原則\]，在 \[最小 PIN 碼長度\] 旁輸入 4 到 24 之間的值。

5.  按一下 \[儲存\]。

## 使用命令介面設定 Outlook 語音存取的最小 PIN 碼長度

此範例會將已啟用 Outlook 語音存取之使用者 (與名為 `MyUMMailboxPolicy` 的 UM 信箱原則相關聯) 的最小 PIN 碼長度設為 8 位數。

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -MinPINLength 8

此範例會將最小 PIN 碼長度設為 8 位數，並設定使用者的 PIN 碼重設為 3 之前可以失敗的登入次數。這適用於與名為 `MyUMMailboxPolicy` 之 UM 信箱原則相關聯的已啟用 UM 的使用者。

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 3 -MinPINLength 8

