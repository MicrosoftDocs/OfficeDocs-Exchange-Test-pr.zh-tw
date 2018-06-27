---
title: '移除 UM 語言套件: Exchange 2013 Help'
TOCTitle: 移除 UM 語言套件
ms:assetid: a2bc2753-2c25-4ea0-a9d5-e3d42a699c6c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124004(v=EXCHG.150)
ms:contentKeyID: 50473897
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 移除 UM 語言套件

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-14_

您可以使用 EAC 或命令介面來管理在執行 Microsoft Exchange 整合通訊服務的 Mailbox server 上的整合通訊 (UM) 語言。不過，從 UM 撥號對應表上的清單中移除的語言，您必須移除適當的 UM 語言套件的信箱伺服器使用**Setup.exe /RemoveUmLanguagePack**命令。從信箱伺服器移除 UM 語言套件之後，語言不是設定 UM 撥號對應表或 UM 自動語音應答時可用。您可以檢視來檢視 Mailbox server 的屬性或使用**Get-UMService**指令程式會安裝 UM 語言套件。

如需其他與 UM 語言相關的工作，請參閱 [UM 語言、 提示及問候語程序](um-languages-prompts-and-greetings-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：少於 5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「Mailbox server (UM Service)」項目。

  - 驗證安裝了 UM 語言套件不是 en-US 版本。

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


## 使用 Setup.exe 移除 UM 語言套件

在命令提示字元中，執行下列命令。

    Setup.exe /RemoveUmLanguagePack:<UmLanguagePackName>

在上述命令中，*\<UmLanguagePackName\>* 是 UM 語言套件的名稱。例如 fr-FR。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您無法使用 Setup.exe 檔案位於您已安裝任何更新之後移除 UM 語言套件的 \Bin 資料夾中。您必須使用 Setup.exe 檔案從Exchange 2013 DVD 或下載的來源檔案。如果您不會看到下列錯誤： 沒有執行的應用程式與安裝的應用程式版本不符。</td>
</tr>
</tbody>
</table>

