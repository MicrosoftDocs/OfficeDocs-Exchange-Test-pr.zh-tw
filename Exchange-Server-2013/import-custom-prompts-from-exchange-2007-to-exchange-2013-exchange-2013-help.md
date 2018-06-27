---
title: '匯入自訂提示從 Exchange 2007 到 Exchange 2013: Exchange 2013 Help'
TOCTitle: 匯入自訂提示從 Exchange 2007 到 Exchange 2013
ms:assetid: 70c0b0bc-c0de-4e3c-8144-1fe59f86ebf4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg309147(v=EXCHG.150)
ms:contentKeyID: 54652590
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 匯入自訂提示從 Exchange 2007 到 Exchange 2013

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2015-04-08_

您可以匯入音訊檔包含的自訂問候語、 宣告、 功能表及提示從Exchange 2007整合通訊 (UM) 至 Exchange 2013 Unified Messaging。使用命令介面指令碼、 提示會匯入 Exchange 系統信箱名為 {e0dc1c29-89c3-4034-b678-e6c29d823ed9} 當您安裝 Microsoft Exchange 2013 中所建立。此系統信箱整合通訊中用以儲存撥號對應表和自動語音應答的自訂問候語、 宣告、 功能表、 提示及 UM 報告。

音訊檔案 (.wav 或 .wma 格式) 的使用方式如下：

  - 在 UM 撥號對應表音訊檔可用於自訂的歡迎使用問候語和資訊性的宣告。他們被播放時 Outlook 語音存取使用者撥打 Outlook 語音存取號碼。

  - 在 UM 自動語音應答、 音訊檔可用於非上班與上班時間的自訂的問候語、 資訊性宣告、 功能表提示及導覽功能表。他們被播放來電者撥入 UM 自動語音應答時。

您可使用 MigrateUMCustomPrompts.ps1 指令碼，將所有 Exchange Server 2007 UM 自訂問候語、宣告、功能表和提示的副本遷移至所有 Exchange 2007 UM 撥號對應表和 UM 自動語音應答的 Exchange 2013 UM。

依據預設，MigrateUMCustomPrompts.ps1 指令碼位於 Exchange 2013 伺服器的 \<Program Files\>\\Microsoft\\Exchange Server\\V15\\Scripts 資料夾中。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>MigrateUMCustomPrompts.ps1 指令碼所含Exchange 2013。其必須與Exchange 2007 UM 伺服器位於相同組織Exchange 2013 」 的信箱伺服器上執行。</td>
</tr>
</tbody>
</table>


如需與 UM 撥號對應表相關的其他管理工作，請參閱 [UM 撥號對應表規劃程序](um-dial-plan-procedures-exchange-2013-help.md)。

如需與 UM 自動語音應答相關的其他管理工作，請參閱[UM 自動語音應答程序](um-auto-attendant-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：3 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱「 UM 撥號對應表 」 和 「 UM 自動語音應答？[整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

  - 執行這些程序之前，請確認已建立 UM 自動語音應答。如需詳細步驟，請參閱[建立 UM 自動語音應答](create-a-um-auto-attendant-exchange-2013-help.md)。

  - 您只能使用命令介面來執行此程序。 若要了解如何在內部部署 Exchange 組織中開啟 Exchange 管理命令介面，請參閱[開啟命令介面。](https://technet.microsoft.com/zh-tw/library/dd638134\(v=exchg.150\))。

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


## 使用 MigrateUMCustomPrompts.ps1 指令碼，以遷移 UM 撥號對應表及 UM 自動語音應答的所有自訂提示副本

1.  按一下 \[開始\] \> \[所有程式\] \> \[Microsoft Exchange Server 2013\] \> \[Exchange 管理命令介面\]。

2.  在命令介面中的 \[在提示處輸入指令碼的路徑。例如，輸入**cd"D:\\Program Files\\Microsoft\\Exchange Server\\V15\\Scripts"**，並按 Enter。

3.  在命令介面的提示字元下，輸入 **".\\MigrateUMCustomPrompt",**，然後按下 Enter。

