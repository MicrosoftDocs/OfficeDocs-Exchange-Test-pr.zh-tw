---
title: '啟用電話使用者介面使用的自訂提示錄製: Exchange Online Help'
TOCTitle: 啟用電話使用者介面使用的自訂提示錄製
ms:assetid: f2e5c636-2be9-4d48-b5e7-37913ded62d1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb691404(v=EXCHG.150)
ms:contentKeyID: 54652612
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟用電話使用者介面使用的自訂提示錄製

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2014-09-17_

您可使用電話使用者介面 (TUI)，以透過命令介面來記錄「整合通訊」(UM) 撥號對應表與自動語音應答的自訂提示和問候語。 若您想要使用 EAC 或命令介面變更自訂問候語或宣告，或是遇到組織因天候惡劣而關閉等緊急情況，這項功能即可派上用場。 變更 UM 自動語音應答的自訂問候語或宣告時，您必須在 UM 自動語音應答連結的撥號對應表上啟用 TUI 提示錄製。

如需與 UM 撥號對應表相關的其他管理工作，請參閱 [UM 撥號對應表規劃程序](um-dial-plan-procedures-exchange-2013-help.md)。

如需與 UM 自動語音應答相關的其他管理工作，請參閱[UM 自動語音應答程序](um-auto-attendant-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：3 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 撥號對應表」與「UM 自動語音應答」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在執行這些程序之前，請確認已建立 UM 自動語音應答。 如需詳細步驟，請參閱[建立 UM 自動語音應答](create-a-um-auto-attendant-exchange-2013-help.md)。

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

## 使用命令介面錄製使用 TUI 的自訂提示或問候語

若要透過電話使用者介面 (TUI) 錄製自訂提示與問候語，請遵循下列步驟：

1.  建立無法以互動方式登入的網域使用者帳戶。

2.  將 Exchange 組織系統管理員角色委派給網域使用者帳戶。

3.  建立網域使用者的信箱。

4.  為網域使用者信箱啟用整合通訊。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>請只讓管理提示與問候語的系統管理員存取使用者帳戶的分機號碼與 PIN。 此使用者帳戶僅適用於透過電話來管理提示。</td>
    </tr>
    </tbody>
    </table>


5.  建立並儲存 .wav 或 .wma 檔案，以供 UM 撥號對應表或自動語音應答的自訂問候語使用。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>MP3 檔案無法作為自訂提示使用。</td>
    </tr>
    </tbody>
    </table>


6.  透過 EAC 或命令介面，以設定要使用自訂歡迎使用問候語的撥號對應表，或是設定要使用上班時間或非上班時間問候語的自動語音應答。 如需設定撥號對應表的詳細資訊，請參閱[啟用 Outlook 語音存取使用者的自訂的問候語](enable-a-customized-greeting-for-outlook-voice-access-users-exchange-2013-help.md)。 如需設定自動語音應答的詳細資訊，請參閱[啟用自訂的上班時間問候語](enable-a-customized-business-hours-greeting-exchange-2013-help.md)或[啟用自訂非上班時間問候語](enable-a-customized-non-business-hours-greeting-exchange-2013-help.md)。

7.  執行下列指令程式：
    
        Set-UMDialPlan -identity MyUMDialPlan -TUIPromptEditingEnabled $true

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您必須登入錄製提示時設定的信箱，才能啟用自訂提示或問候語錄製功能。 錄製新的提示或問候語後，您必須先登出然後再重新登入，才能在使用 TUI 時聽見新的提示或問候語。</td>
</tr>
</tbody>
</table>


## 在 UM 自動語音應答上執行 TUI 提示錄製

1.  確認已將自動語音應答連結至您為 TUI 提示錄製啟用的撥號對應表。

2.  撥打 UM 自動語音應答上所設定的電話號碼。

3.  聽到自動語音應答播放非上班時間或上班時間問候語時，按下井字鍵 (\#)，然後再按下米字鍵 (\*)。

4.  系統會提示您輸入使用者分機號碼。 輸入具有 UM 功能之使用者的分機號碼，此使用者必須具有執行 TUI 提示錄製的權限。

5.  系統會提示您輸入 PIN 碼。 請輸入使用者PIN 碼。

6.  遵循系統提示，編輯或更新自動語音應答的問候語或資訊性宣告。

## 在 UM 撥號對應表上執行 TUI 提示錄製

1.  撥打您用來登入「Outlook 語音存取」的「Outlook 語音存取」號碼。

2.  聽到撥號對應表的歡迎使用問候語時，按下井字鍵 (\#)，然後再按下米字鍵 (\*)。

3.  如果您是從具有 UM 功能之使用者所用的電話號碼撥打，系統會提示您輸入 PIN 碼。 不要輸入 PIN 碼，請改按 (\*) 鍵。 系統會提示您輸入分機號碼。 輸入具有 UM 功能之使用者的分機號碼，此使用者必須具有執行 TUI 提示錄製的權限。

4.  如果您是從不是具有 UM 功能的使用者所使用的電話號碼撥打，系統會自動提示您輸入分機號碼。 輸入具有 UM 功能之使用者的分機號碼，此使用者必須具有執行 TUI 提示錄製的權限。

5.  系統會提示您輸入 PIN 碼。請輸入使用者PIN 碼。

6.  遵循系統提示，編輯或更新撥號對應表的歡迎使用問候語或資訊性宣告。

