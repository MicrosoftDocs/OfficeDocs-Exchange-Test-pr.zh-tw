---
title: '設定語音信箱的 PIN 存留期: Exchange Online Help'
TOCTitle: 設定語音信箱的 PIN 存留期
ms:assetid: d17f0bf6-0ad6-40a4-bdd5-f7098f39250d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124712(v=EXCHG.150)
ms:contentKeyID: 50554067
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定語音信箱的 PIN 存留期

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-22_

您可以設定已啟用的整合通訊 (UM) 之使用者的 PIN 存留期。PIN 存留期為Outlook語音存取 PIN 將會是有效的已啟用 UM 之收件者的最長時間。PIN 存留期設定 UM 信箱原則上設定並套用至所有已啟用 UM 之使用者的 UM 信箱原則相關聯。

可以在 UM 信箱原則上設定 pin 碼相關的數個設定。設定控制項的時間間隔，PIN 存留期天，從日期Outlook語音存取使用者上次變更其 PIN 為他們將強制能夠再次變更他們的 pin 碼的日期。範圍是從 0 到 999 及預設值為 60 天。如果您輸入 0，將不會過期使用者的 PIN。我們建議您不要此設定為 0，因為依照這麼明顯減輕在網路的安全性。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>整合通訊不會通知使用者他們的 PIN 碼即將到期。</td>
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

## 使用 EAC 來設定 PIN 碼存留時間

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。

2.  在清單檢視中，選取您要變更的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[UM 撥號對應表\] 頁面中的 \[UM 信箱原則\] 之下，選取您要變更的 UM 信箱原則，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

4.  按一下 \[強制執行 PIN 碼存留時間 (天)\] 旁邊的 \[PIN 碼原則\]，輸入介於 0 到 999 之間的值。

5.  按一下 \[儲存\]。

## 使用命令介面來設定 PIN 碼存留時間

此範例會針對與名稱為 `MyUMMailboxPolicy` 的 UM 信箱原則相關聯的 Outlook 語音存取使用者，設定其 PIN 的天數為 30 天。

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -PINLifetime 30

此範例會針對與名稱為 `MyUMMailboxPolicy` 的 UM 信箱原則相關聯的 Outlook 語音存取使用者，設定下列 PIN 相關設定：

  - 將使用者 PIN 重設之前的登入失敗次數設定為 3。

  - 將嘗試登入次數上限設定為 5。

  - 將最小 PIN 碼長度設定為 9 位數。

  - 將 PIN 碼設定為 40 天內到期。

<!-- end list -->

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 3
    -MaxLogonAttempts 5 -MinPINLength 9 -PINLifetime 40

