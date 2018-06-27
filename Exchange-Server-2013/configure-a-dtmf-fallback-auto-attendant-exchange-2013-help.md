---
title: '設定 DTMF 後援自動語音應答: Exchange Online Help'
TOCTitle: 設定 DTMF 後援自動語音應答
ms:assetid: a82d85f7-de30-40db-8ee6-b091ac14da9d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb232158(v=EXCHG.150)
ms:contentKeyID: 50473898
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定 DTMF 後援自動語音應答

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2012-11-30_

您可以設定有雙音多頻 (dtmf) 後援自動語音應答啟用語音功能整合通訊 (UM) 自動語音應答。當 UM 語音啟用自動語音應答無法了解或辨識來電者所提供的語音輸入使用 DTMF 後援自動語音應答。如果已設定 DTMF 後援自動語音應答，將來電者具有使用 DTMF 輸入，也稱為按鍵式輸入來瀏覽自動語音應答功能表系統、 拼字使用者的名稱或使用自訂的功能表提示。如果尚未設定任何 DTMF 後援自動語音應答，而且的語音輸入最大數目超過因為系統沒有瞭解來電者所說，系統將會回應此提示： 「 很抱歉，我無法建立協助。請請稍後再撥。 」

根據預設，自動語音應答未啟用語音的當您建立。您語音啟用功能之後的自動語音應答，來電者可以使用僅限語音命令來瀏覽自動語音應答功能表系統並不能使用按鍵式輸入。雖然不需要是，我們建議您讓來電者可以使用按鍵式輸入啟用語音的自動語音應答無法辨識或不了解這些說出字設定 DTMF 後援自動語音應答每個啟用語音的自動語音應答。也建議的您未啟用語音 DTMF 後援自動語音應答。

如需與 UM 自動語音應答相關的其他管理工作，請參閱[UM 自動語音應答程序](um-auto-attendant-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 自動語音應答」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

  - 執行這些程序之前，請確認已建立 UM 自動語音應答。如需詳細步驟，請參閱[建立 UM 自動語音應答](create-a-um-auto-attendant-exchange-2013-help.md)。

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

## 使用 EAC 設定已啟用語音的自動語音應答搭配 DTMF 後援自動語音應答

1.  在 EAC 中，瀏覽至 \[**整合通訊**\> **UM 撥號對應表**。在清單檢視中，選取您想要變更然後按一下 \[**編輯**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")UM 撥號對應表。

2.  在 \[ **UM 撥號對應表**\] 頁面上 \[ **UM 自動語音應答**，選取您要建立 DTMF 後援自動語音應答的 UM 自動語音應答。在工具列上，按一下 \[**編輯**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[UM 自動語音應答\] 頁面 \> \[一般\] 上，選取 \[當語音命令未正確運作時使用此自動語音應答\] 旁的核取方塊，然後按一下 \[瀏覽\]。

4.  在 \[選取 UM 自動語音應答\] 頁面上，選取要當做 DTMF 後援自動語音應答使用的自動語音應答，然後按一下 \[儲存\]。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您必須先啟用自動語音應答的語音功能，才能瀏覽您所設定的 DTMF 後援自動語音應答。</td>
</tr>
</tbody>
</table>


## 使用命令介面，設定已啟用語音的自動語音應答搭配 DTMF 後援自動語音應答

本範例將名為 `MySpeechEnabledAA` 的 UM 自動語音應答，設定為使用名為 `MyDTMFAA` 的 DTMF 後援自動語音應答。

    Set-UMAutoAttendant -Identity MySpeechEnabledAA -DTMFFallbackAutoAttendant MyDTMFAA

