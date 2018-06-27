---
title: '啟用 Outlook 語音存取使用者的自訂的問候語: Exchange Online Help'
TOCTitle: 啟用 Outlook 語音存取使用者的自訂的問候語
ms:assetid: abd418ec-2c65-4720-859d-c11a2698dc06
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124125(v=EXCHG.150)
ms:contentKeyID: 50554048
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟用 Outlook 語音存取使用者的自訂的問候語

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2016-12-09_

根據預設，每個整合通訊 (UM) 撥號對應表的撥號對應表中已設定為 Outlook 語音存取號碼的語音存取使用者對呼叫者，包括Outlook具有播放歡迎使用問候語使用標準的.wav 檔。不過，您可建立.wav 或.wma 檔案歡迎使用問候語，並啟用 UM 撥號對應表上。

例如，您可能會想要變更預設的歡迎使用問候語，並改用提供專為您的公司，例如 「 歡迎使用Outlook的 Woodgrove Bank 語音存取 「 歡迎使用問候語。為達成此目的，您可以記錄的自訂歡迎使用問候語並將其儲存為.wav 或.wma 檔案。然後您設定要使用的自訂歡迎使用問候語撥號。

如需Outlook語音存取使用者可用的功能表選項的詳細資訊，請參閱適用於Outlook語音存取的快速參考指南是可從[Microsoft 下載中心](https://go.microsoft.com/fwlink/p/?linkid=272767)。

如需與 UM 撥號對應表相關的其他管理工作，請參閱 [UM 撥號對應表規劃程序](um-dial-plan-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 撥號對應表」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。 如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

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

## 使用 EAC 來啟用自訂的歡迎使用問候語

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。

2.  在清單檢視中，選取您要修改的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[UM 撥號對應表\] 頁面上，按一下 \[設定\]。

4.  在 \[Outlook 語音存取\] 的 \[歡迎使用問候語\] 下，按一下 \[變更\]，然後按一下 \[瀏覽\] 以尋找問候語檔案。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>用於歡迎使用問候語的檔案必須是 .wav 或 .wma 檔案。</td>
    </tr>
    </tbody>
    </table>


5.  找到檔案之後，請按一下 \[開啟\]，然後按一下 \[儲存\]。

## 使用命令介面來啟用自訂的歡迎使用問候語

本範例會在名為 `MyUMDialPlan` 的 UM 撥號對應表上，啟用一個使用 C:\\UMPrompts\\welcome.wav 檔案的歡迎使用問候語。

    Set-UMDialPlan -Identity MyUMDialPlan -WelcomeGreetingEnabled $true -WelcomeGreetingFilename c:\UMPrompts\welcome.wav

