---
title: '匯入及匯出的自訂問候語、 宣告、 功能表及提示: Exchange 2013 Help'
TOCTitle: 匯入及匯出的自訂問候語、 宣告、 功能表及提示
ms:assetid: e82da5d5-625f-4d8b-8d31-ac45513aacfd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee681667(v=EXCHG.150)
ms:contentKeyID: 54652605
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 匯入及匯出的自訂問候語、 宣告、 功能表及提示

 

_**適用版本：**Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2015-04-08_

您可以匯入及匯出您已記錄在整合通訊 (UM) 撥號對應表和自動語音應答上使用的音訊檔案。例如，可能會想要匯出並儲存的音訊檔案複本如果您從舊版 Exchange 的升級。或者，您可能需要匯入一份錄製的音訊提示之前設定撥號對應表或自動語音應答。

音訊檔案適合下列用途：

  - 在 UM 撥號對應表音訊檔可用於自訂的歡迎使用問候語和資訊性的宣告。他們被播放時 Outlook 語音存取使用者撥打 Outlook 語音存取號碼。

  - 在 UM 自動語音應答、 音訊檔可用於非上班與上班時間的自訂的問候語、 資訊性宣告、 功能表提示及導覽功能表。他們被播放來電者撥入 UM 自動語音應答時。

自訂問候語、宣告、功能表和提示支援下列音訊檔案格式：

  - 以 Windows Media Audio 9.2 - 96 kbps/44 kHz/立體聲 1-pass CBR (Windows 錄音機) 進行編碼的 .wma 檔案

  - Windows Media Audio Voice 9 - 8 kbps/8 kHz/單聲道以及 Linear PCM (16 位元/取樣)、8 千赫 (kHz) 音訊轉碼器進行編碼的 .wav 檔案。

您匯入音訊檔會使用 UM 撥號對應表及自動語音應答到名為 {e0dc1c29-89c3-4034-b678-e6c29d823ed9} 的系統信箱以及從這個系統信箱中匯出的音訊檔案。音訊檔案可匯入及匯出使用**Import-UMPrompt**和**Export-UMPrompt** cmdlet。

如需與 UM 撥號對應表相關的其他管理工作，請參閱 [UM 撥號對應表規劃程序](um-dial-plan-procedures-exchange-2013-help.md)。

如需與 UM 自動語音應答相關的其他管理工作，請參閱[UM 自動語音應答程序](um-auto-attendant-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：3 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱「 UM 撥號對應表 」 和 「 UM 自動語音應答？[整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

  - 執行這些程序之前，請確認已建立 UM 自動語音應答。如需詳細步驟，請參閱[建立 UM 自動語音應答](create-a-um-auto-attendant-exchange-2013-help.md)。

  - 您只能使用命令介面來執行此程序。

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

## 使用命令介面來匯入 UM 撥號對應表和自動語音應答的自訂問候語、宣告、功能表和提示

本範例會將歡迎使用問候語檔案 welcomegreeting.wav 從 d:\\UMPrompts 匯入至 UM 撥號對應表 `MyUMDialPlan` 中。

    [byte[]]$c = Get-content -Path "d:\UMPrompts\welcomegreeting.wav" -Encoding Byte -ReadCount 0
    Import-UMPrompt -UMDialPlan MyUMDialPlan -PromptFileName "welcomegreeting.wav" -PromptFileData $c

本範例會將歡迎使用問候語檔案 welcomegreeting.wav 從 d:\\UMPrompts 匯入至 UM 自動語音應答 `MyUMAutoAttendant` 中。

    [byte[]]$c = Get-content -Path "d:\UMPrompts\welcomegreeting.wav" -Encoding Byte -ReadCount 0
    Import-UMPrompt -UMAutoAttendant MyUMAutoAttendant -PromptFileName "welcomegreeting.wav" -PromptFileData $c

## 使用命令介面從 UM 撥號對應表和自動語音應答匯出自訂問候語、宣告、功能表和提示

本範例會匯出 UM 撥號對應表 `MyUMDialPlan` 的歡迎使用問候語，並將其儲存為名為 welcomegreeting.wav 的檔案。

    $prompt = Export-UMPrompt -PromptFileName "customgreeting.wav�? -UMDialPlan MyUMDialPlan
    set-content -Path "d:\DialPlanPrompts\welcomegreeting.wav" -Value $prompt.AudioData -Encoding Byte

本範例會匯出 UM 自動語音應答 `MYUMAutoAttendant` 的上班時間歡迎使用問候語，並將其儲存為名為 BusinessHoursWelcomeGreeting.wav 的檔案。

    $prompt = Export-UMPrompt -BusinessHoursWelcomeGreeting -UMAutoAttendant MyUMAutoAttendant
    set-content -Path "d:\UMPrompts\BusinessHoursWelcomeGreeting.wav" -Value $prompt.AudioData -Encoding Byte

