---
title: '自動語音應答選取的語言: Exchange Online Help'
TOCTitle: 自動語音應答選取的語言
ms:assetid: 3a1c1ec0-c726-41fb-a294-59faab205609
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa997306(v=EXCHG.150)
ms:contentKeyID: 50553963
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 自動語音應答選取的語言

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2016-12-09_

您可以設定整合通訊 (UM) 自動語音應答上設定預設提示語言。在 UM 自動語音應答上設定可用的語言可讓您的自動語音應答上設定的預設提示的語言。當您使用的預設系統提示的自動語音應答時，這是來電者聽到時的自動語音應答接聽來電的語言。此語言設定會影響僅預設系統提示安裝之後執行 Microsoft Exchange 整合通訊服務的信箱伺服器所提供。此設定不會影響的自動語音應答設定的自訂提示。可用的語言為基礎的信箱伺服器安裝整合通訊語言套件。

建立每個自動語音應答一開始會使用英文 (EN-US) 做為預設語言。英文 (EN-US) 的語言套件上所有版本的Microsoft Exchange 2013 的預設會安裝且無法加以移除。如果您想要選取另一種語言，例如德文 (DE-DE)，您必須先從[Exchange Server 2013 UM 語言套件](https://go.microsoft.com/fwlink/?linkid=266542)下載德文 UM 語言套件.exe 檔案並使用 UMLanguagePack.de de.exe 安裝檔案的 Mailbox server 上安裝 UM 語言套件。您已安裝 UM 語言套件之後，您可以為非英文 (EN-US) 語言 UM 自動語音應答上設定的預設語言。

如需其他與 UM 語言相關的工作，請參閱 [UM 語言、 提示及問候語程序](um-languages-prompts-and-greetings-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 自動語音應答」項目。

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

## 使用 EAC 設定預設語言設定

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。

2.  在清單檢視中，選取欲修改的 UM 撥號對應表，然後按一下工具列上的 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[UM 撥號對應表\] 頁面的 \[UM 自動語音應答\] 下方，選取您要變更的 UM 自動語音應答，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

4.  在 \[一般\] 頁面的 \[自動化語音介面的語言\] 下，從下拉式清單選取所需的語言。

5.  按一下 \[儲存\] 以接受您的變更。

## 使用命令介面設定預設語言設定

此範例會在 UM 自動語音應答 `MyUMAutoAttendant` 上將預設語言設定為英文 (英國)。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -Language en-GB

此範例會在 UM 自動語音應答 `MyUMAutoAttendant` 上將預設語言設定為德文。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -Language de-DE

