---
title: '在 [撥號對應表上設定的預設語言: Exchange Online Help'
TOCTitle: 在 [撥號對應表上設定的預設語言
ms:assetid: 7a1d2e7e-4053-40af-9ec1-ec714df12ad4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa998914(v=EXCHG.150)
ms:contentKeyID: 50554013
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 在 \[撥號對應表上設定的預設語言

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2016-12-09_

您可以設定整合通訊 (UM) 撥號對應表的預設語言。每個撥號對應表建立一開始會使用英文 (EN-US) 做為預設語言。英文 (EN-US) 的語言套件安裝在所有版本的MicrosoftExchange Server 2013上並不能移除。

如果您想要選取另一種語言做為預設語言，例如德文 (DE-DE)，首先必須從[Exchange Server 2013 UM 語言套件](https://go.microsoft.com/fwlink/p/?linkid=266542)下載德文 UM 語言套件.exe 檔案並使用 UMLanguagePack.de de.exe 安裝檔案的信箱伺服器上安裝該語言套件。您已安裝的語言套件之後，您可以在您的 UM 撥號設定非英文 (EN-US) 的語言的預設語言。

如需其他與 UM 語言相關的工作，請參閱 [UM 語言、 提示及問候語程序](um-languages-prompts-and-greetings-procedures-exchange-2013-help.md)。

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

## 使用 EAC 設定 UM 撥號對應表上的預設語言

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。

2.  在清單檢視中，選取您想要修改的 UM 撥號對應表，然後在工具列上，按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[UM 撥號對應表\] 頁面上，按一下 \[設定\]。

4.  在 \[設定\] 頁面的 \[音訊語言\] 下，從下拉式清單選取您想設定的語言。

5.  按一下 \[儲存\] 以接受您的變更。

## 使用命令介面設定 UM 撥號對應表上的預設語言

此範例會將名爲 `MyUMDialPlan` 的 UM 撥號對應表上的預設語言設定為德文。

    Set-UMDialPlan -Identity MyUMDialPlan -DefaultLanguage de-DE

此範例會將名爲 `MyUMDialPlan` 的 UM 撥號對應表上的預設語言設定為日文。

    Set-UMDialPlan -Identity MyUMDialPlan -DefaultLanguage ja-JP

此範例會將名爲 `MyUMDialPlan` 的 UM 撥號對應表上的預設語言設定為澳洲英文。

    Set-UMDialPlan -Identity MyUMDialPlan -DefaultLanguage en-AU

