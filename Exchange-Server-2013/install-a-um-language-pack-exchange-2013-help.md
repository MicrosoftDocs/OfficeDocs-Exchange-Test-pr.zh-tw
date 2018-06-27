---
title: '安裝 UM 語言套件: Exchange 2013 Help'
TOCTitle: 安裝 UM 語言套件
ms:assetid: ed14ffa5-c9b0-4367-b5da-564024b360ff
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd876951(v=EXCHG.150)
ms:contentKeyID: 50474536
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 安裝 UM 語言套件

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2016-12-09_

若要提供一種語言的 UM 撥號對應表或 UM 自動語音應答上的可用整合通訊語言清單中，您必須先安裝適當的 UM 語言套件。您使用特定語言的自我解壓縮可執行檔或**setup.exe /AddUmLanguagePack**命令執行 Microsoft Exchange 整合通訊服務的信箱伺服器上安裝語言套件。您可以安裝 UM 語言套件之前，必須先將它下載至本機資料夾的 Mailbox server 上。您可以從[Exchange Server 2013 UM 語言套件](https://go.microsoft.com/fwlink/p/?linkid=266542)下載的 UM 語言套件。沒有每種語言的個別可執行檔。

安裝適當的 UM 語言套件之後，您可以檢視已安裝 UM 語言套件的清單檢視 UM 撥號對應表或 UM 自動語音應答的 \[**一般**\] 頁面上**的自動的語音介面的語言**下拉式清單的 \[**設定**\] 頁面上的下拉式清單中。您也可以在 UM 撥號對應表和自動語音應答上設定的預設語言是英文 (EN-US) 以外的語言。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Exchange 2013信箱伺服器上無法使用 Microsoft Exchange Server 2007或Exchange 2007 Service Pack 1 (SP1)，SP2、 或 SP3 或 Exchange 2010 Service Pack 1 SP1、 SP2、 或 SP3 的 UM 語言套件。</td>
</tr>
</tbody>
</table>


如需其他與 UM 語言相關的工作，請參閱 [UM 語言、 提示及問候語程序](um-languages-prompts-and-greetings-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)中的 「 mailbox server (UM service) 」 項目。

  - 確認信箱伺服器安裝在與用戶端存取伺服器不同的電腦上或用戶端存取和信箱伺服器位於相同的硬體。

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

## 使用 UM 語言套件安裝 (.exe) 檔案來安裝 UM 語言套件

1.  從[Microsoft 下載中心](https://go.microsoft.com/fwlink/p/?linkid=266542)，下載特定語言的 UM 語言套件 (.exe) 檔案到本機資料夾 Mailbox server 上。

2.  按兩下 \[UMLanguagePack。*\<CultureCode\>.exe*檔案。例如德文 UM 語言套件，您會下載名為 UMLanguagePack.de DE.exe 的檔案。

3.  
    
    Exchange 2013安裝精靈\] 中 \[**授權合約**\] 頁面上的閱讀合約中的條款，選取 \[**我接受授權合約中的條款\]**，並再按 \[**下一步**。

4.  
    
    在 **\[整合通訊語言套件\]** 頁面上，確認正確的語言已列於 **\[將安裝下列整合通訊語言套件\]** 視窗中，然後按一下 **\[安裝\]**。

5.  按一下 **\[完成\]** 來完成 UM 語言套件的安裝。

## 使用 setup.exe 安裝 UM 語言套件

本範例安裝日文 (JA-JP) UM 語言套件的尚未下載到信箱伺服器上的 \[D:\\Exchange\\UMLanguagePacks\] 資料夾。

    setup.exe /AddUmLanguagePack:ja-JP /s:d:\Exchange\UMLanguagePacks /IAcceptExchangeServerLicenseTerms

此範例會安裝墨西哥西班牙文 (ES-MX) 和德文 (DE-DE) UM 語言套件已下載至信箱伺服器上的 \[D:\\Exchange\\UMLanguagePacks\] 資料夾。

    setup.exe /AddUmLanguagePack:es-MX,de-DE /s:d:\Exchange\UMLanguagePacks /IAcceptExchangeServerLicenseTerms

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您未使用 /IAcceptExchangeServerLicenseTerms 參數，您會看見下列錯誤： 歡迎使用 Microsoft Exchange Server 2013 自動安裝。您必須接受授權條款] 以安裝 Microsoft Exchange Server 2013。若要閱讀授權合約，請造訪 http://go.microsoft.com/fwlink/p/?LinkId=150127。若要接受授權合約，將新增至您正在執行命令的 /IAcceptExchangeServerLicenseTerms 參數。如需詳細資訊，請執行安裝程式 /？ ＞。</td>
</tr>
</tbody>
</table>


如需可用的 UM 語言和文化特性代碼的詳細資訊，請參閱[UM 語言、 提示及問候語](um-languages-prompts-and-greetings-exchange-2013-help.md)。

