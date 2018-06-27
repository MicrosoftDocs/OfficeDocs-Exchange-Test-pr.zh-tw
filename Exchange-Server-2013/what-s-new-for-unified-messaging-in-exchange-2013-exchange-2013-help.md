---
title: '什麼是整合通訊新 Exchange 2013: Exchange 2013 Help'
TOCTitle: 什麼是整合通訊新 Exchange 2013
ms:assetid: a444ef2d-d893-408e-adf9-c9d8a8b07593
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ150545(v=EXCHG.150)
ms:contentKeyID: 50473917
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 什麼是整合通訊新 Exchange 2013

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

在 Microsoft Exchange Server 2013，我們正在使用舊版 Exchange 增強所引進的新功能和基礎結構變更。整合通訊 (UM) Exchange 2013中包含相同的功能集所Exchange 2010以及Exchange 2007，不過整合通訊不再是個別的伺服器角色。現在是在Exchange 2013中所提供的語音相關功能的元件。

## 語音架構的變化

Exchange 2013的架構是不同 your Exchange 2010和Exchange 2007。在舊版的 Exchange UM 整合通訊的所有元件所都包含已安裝 UM server role 的伺服器上。在Exchange 2013，所有整合通訊的元件所執行之 Microsoft Exchange Unified Messaging Call Router 服務用戶端存取伺服器與執行之 Microsoft Exchange 整合通訊服務的 Mailbox server 之間分割。每部信箱伺服器上，除了執行 Microsoft Exchange Unified Messaging Call Router 服務之信箱伺服器的 proxy 來電的用戶端存取伺服器位於所有功能，包括整合通訊的服務和工作者處理序。如需詳細資訊，請參閱[語音的結構變更](voice-architecture-changes-exchange-2013-help.md)。

## 支援 IPv6

網際網路通訊協定第 6 版 (IPv6) 是網際網路通訊協定的最新版本。IPv6 被為了更正許多 IPv4，已 IP 舊版的缺點。如同Exchange 2010、 Exchange 2013 Client Access server 和 Mailbox server 完整支援 IPv6 網路。如需詳細資訊，請參閱[整合通訊中的 IPv6 支援](ipv6-support-in-unified-messaging-exchange-2013-help.md)。

## 支援 UCMA 4.0 API

自Exchange 2010的 Service Pack 1 整合通訊角色具有所依賴的訊號和媒體的 Unified Communications Managed API 2.0 版 (UCMA)。因此，UCMA 2.0 是Exchange 2010 UM 安裝的必要條件。UCMA 2.0 會分別下載和執行Exchange 2010 SP1 或更新版本的整合通訊伺服器上的系統管理員手動部署。針對Exchange 2013，則需要 UCMA 4.0。但假設 UM server 便不再Exchange 2013中的個別的伺服器角色，現在是需要 UCMA 4.0 的用戶端存取和信箱伺服器。

UCMA 4.0 支援新功能整合通訊，例如使用文字轉語音 (TTS) 和自動語音辨識 (ASR) 相同的語音引擎版本。用於Exchange 2013, .NET 4.0 的平台包含單一安裝程式檔案，並啟用Exchange 2010和Exchange 2007 UM 伺服器的回溯相容性。

Exchange 2010 SP2 及 SP1、 UCMA 2.0 中安裝是必要的整合通訊伺服器上安裝 service pack 之前。不過，UCMA 2.0 有數個限制。UCMA 4.0 修正許多缺點。中Exchange Server 2013、 UM 會繼續使用 UCMA。不過，移至最新版本的 UCMA 可提供下列優點：

  - UCMA 的最新版本包含了 Hotfix 和修補程式。

  - UCMA 需要.NET 4.0，它是Exchange Server 2013所使用的平台。（UCMA 2.0 不支援.NET 4.0）。

  - UCMA 4.0 支援 IPv6。

  - 簡化並自動部署的 UCMA 4.0。Exchange 2013安裝程式會執行單一核取的 UCMA 4.0。

  - UCMA 4.0 安裝程式包括所有 Exchange 2013 的必要條件。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您要安裝Exchange 2013安裝 UCMA 4.0。如需 UCMA 4.0 和安裝需求的詳細資訊，請參閱<a href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 必要條件</a>。若要升級至 UCMA 最新版本，您必須先解除安裝任何舊版 UCMA 安裝使用 [新增/移除程式]。</td>
</tr>
</tbody>
</table>


## 語音郵件預覽改良功能

針對Exchange Server 2013 UM 語音引擎 11.0 和 UCMA 4.0 透過提供的一些增強功能的語音相關的服務。改良的文法產生與語言都包含在內。此外， Exchange Server 2013 UM 包含許多增強使用者介面和信賴的增強功能和語音郵件預覽的正確性。如需詳細資訊，請參閱[語音郵件預覽增強功能](voice-mail-preview-enhancements-exchange-2013-help.md)。

## 加強來電顯示協助

在舊版的 Exchange 整合通訊，萬一呼叫的 UM 伺服器用於來電者識別碼嘗試查閱撥號方的身分識別。此搜尋遍佈 Active Directory 與 UM 信箱中儲存的使用者的個人連絡人。

Exchange 使用者會經常困擾失敗識別 Exchange 或個人連絡人從其來電者識別碼。到目前為止，僅預設連絡人資料夾的 Exchange UM 使用此搜尋。但Exchange Server 2013使用者可能有彙總來自外部社交網路或連絡人已手動建立使用者的唯一資料夾中的連絡人。Exchange 2013支援來自外部社交網路連絡人的彙總、 提供智慧連結多名連絡人參照相同的人員，並使用該資料呈現人員為中心 （而非連絡人中心） 的檢視。彙總從外部網路的連絡人會放在與任何其他連絡人資料夾的連絡人資料夾中建立該使用者。Exchange 2013 UM 的功能擴充範圍之搜尋包含使用者的其他 Exchange 和手動建立的個人連絡人資料夾。

來電者識別碼查詢整合連絡人的彙總，使其搜尋整個外部連絡人。PersonID 屬性，其中有使用此參數與非 null 值，以改善來電者識別碼解決方法的使用者經驗來隱藏除數重複的相符項目相關聯之相同的人員的連絡人。由於 PersonID 屬性是在這兩個結果相同、 UM 將它視為相符項目至單一連絡人。

## 語音平台與語音辨識的加強功能

Exchange Server 2013 UM 為語音平台與語音辨識導入部分加強功能，包括：

  - 語音郵件預覽的加強功能與更佳精確度。

  - 支援[Microsoft Speech Platform – 執行階段 （版本 11.0）](https://go.microsoft.com/fwlink/p/?linkid=253196)。

  - 使用組織的系統信箱進行語音文法產生作業。

Exchange 整合通訊使用靜態及動態語音文法辨識命令、 全域通訊清單中，連絡人的名稱及使用者的信箱中的個人連絡人的名稱。今天、 Exchange Server 2013，在執行 Microsoft Exchange 整合通訊服務的每個信箱伺服器產生安裝在其上的所有 UM 語言的文法預先載入並將其儲存在目錄中。每個信箱伺服器儲存每個可能文法，則會產生其中的撥號對應表、 自動語音應答與已安裝 UM 語言數為基礎。

文法檔案做為輸入語音辨識程序並產生定期為基礎。在Exchange 2007和Exchange 2010 GGG.exe 命令允許您可以手動文法檔案而不需要等候已排程的更新。Exchange Server 2013，在解決 ASR 文法產生工作延展性問題 um、 語音 GAL 文法產生不再發生的情況的伺服器上已安裝整合通訊伺服器角色。而發生情況定期使用信箱助理員，Mailbox server 上執行 Microsoft Exchange 整合通訊服務主控組織的仲裁信箱。GAL 語音文法檔案是儲存在組織的仲裁信箱，然後稍後下載至該 Exchange 組織中所有 Mailbox server。預設會在信箱助理員執行每隔 24 小時。您可以使用**Set-MailboxServer**指令程式來調整頻率。

## 指令程式更新

Exchange 2013、 的許多 UM cmdlet 已帶來了從Exchange 2010，但有中已變更這些 cmdlet 的部分和新指令程式已新增新功能。如需詳細資訊，請參閱[整合的通訊 cmdlet 更新](unified-messaging-cmdlet-updates-exchange-2013-help.md)。

