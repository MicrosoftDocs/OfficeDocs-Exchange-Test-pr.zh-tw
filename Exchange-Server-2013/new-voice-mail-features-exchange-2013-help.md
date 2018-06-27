---
title: '新的語音信箱功能: Exchange 2013 Help'
TOCTitle: 新的語音信箱功能
ms:assetid: 89faaa97-3485-4704-a56c-d13632f01e2a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ649002(v=EXCHG.150)
ms:contentKeyID: 50473648
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 新的語音信箱功能

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2016-12-09_

整合通訊 (UM) 中 Microsoft Exchange Server 2013包括設為Exchange 2010和Exchange 2007、 一些增強及架構變更的同一個功能。不過，整合通訊不再個別的伺服器角色。現在是在Exchange 2013中所提供的語音相關功能的元件。

## 語音架構的變化

Exchange 2013的語音架構是不同 your Exchange 2010和Exchange 2007中。在舊版的 Exchange UM 整合通訊的所有元件所都包含已安裝 UM server role 的伺服器上。中Exchange 2013、 整合通訊元件會執行 Microsoft Exchange Unified Messaging Call Router 服務的用戶端存取伺服器與執行 Microsoft Exchange 整合通訊服務的信箱伺服器之間分割。大部分的功能，包括整合通訊的服務和工作者處理序位於每個信箱伺服器上。執行 Microsoft Exchange Unified Messaging Call Router 服務、 proxy 來電轉接到 Mailbox server 的用戶端存取伺服器。如需詳細資訊，請參閱[語音的結構變更](voice-architecture-changes-exchange-2013-help.md)。

## 支援 IPv6

網際網路通訊協定第 6 版 (IPv6) 是最新版本的網際網路通訊協定 (IP)。IPv6 被為了更正許多 IPv4，已 IP 舊版的缺點。就如同Exchange 2010沒有、 Exchange 2013 Client Access server 和 Mailbox server 完整支援 IPv6 網路。如需詳細資訊，請參閱[整合通訊中的 IPv6 支援](ipv6-support-in-unified-messaging-exchange-2013-help.md)。

## 支援 UCMA 4.0 API

自Exchange 2010 Service Pack 1 (SP1)、 整合通訊角色具有所依賴的 Unified Communications Managed API 2.0 版 (UCMA) 的訊號和媒體。因此，UCMA 2.0 已Exchange 2010 UM 安裝的必要條件。UCMA 2.0 是分別下載和手動部署執行Exchange 2010 SP1 或更新版本 UM 伺服器上的管理員。

不過，UCMA 2.0 有數個限制。許多這些缺點會由 UCMA 4.0 修正所需之Exchange 2013。現在 UM 伺服器不再是個別的伺服器角色，它是需要 UCMA 4.0 的用戶端存取和信箱伺服器。

UCMA 4.0 支援新功能整合通訊，例如使用文字轉語音 (TTS) 和自動語音辨識 (ASR) 相同的語音引擎版本。用於Exchange 2013, .NET 4.0 的平台包含單一安裝程式檔案，並啟用Exchange 2010和Exchange 2007 UM 伺服器的回溯相容性。

在 Exchange 2010 SP2 與 SP1 中，於整合通訊伺服器上安裝服務套件前需先安裝 UCMA 2.0。

使用 UCMA 4.0 提供了多個好處：

  - 它包含了 Hotfixe 和修補程式。

  - 它支援 IPv6。

  - 部署 UCMA 4.0 已自動化和簡化。

  - UCMA 4.0 安裝程式包括所有 Exchange 2013 的必要條件。

  - UCMA 4.0 跨多種產品提供準確度更高的語音引擎轉譯及延展性更好的語音平台支援。

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

Exchange Server 2013 UM 透過語音引擎 11.0 和 UCMA 4.0 中所包含一些增強語音相關的服務。文法產生工作、 核心語音服務及支援多個語言中已改良。Exchange Server 2013UM 也包含數個記錄服務傳遞給使用者和增加的信賴的增強功能和語音郵件預覽的正確性。如需詳細資訊，請參閱[語音郵件預覽增強功能](voice-mail-preview-enhancements-exchange-2013-help.md)。

## 加強來電顯示協助

在舊版的 Exchange 整合通訊，接收呼叫的 UM 伺服器會用來查閱可能 identity 的撥號方來電者識別碼。遍佈Active Directory此搜尋並儲存在其信箱的 UM 使用者的個人連絡人。

在過去，使用者有時已搖頭來識別 Exchange 或從其來電者 ID 的個人連絡人的語音信箱系統的失敗現在，直到僅預設連絡人資料夾中使用者的 Exchange 信箱具有已用於此搜尋。但是Exchange Server 2013使用者可能有彙總來自外部社交網路或連絡人組織其連絡人時加入到唯一資料夾的連絡人。在Exchange 2013、 UM 延伸至包含使用者搜尋範圍的其他 Exchange 和手動建立的個人連絡人資料夾。Exchange 2013也支援來自外部社交網路連絡人彙總、 提供連結參照相同的人的多個連絡人的智慧並使用該資料呈現人員中心 （而非連絡人中心） 的檢視。這表示會彙總來自外部社交網路的連絡人可以會被放置在儲存在 Microsoft Outlook Web App和Outlook中的使用者信箱中的連絡人資料夾。這些連絡人現在也會新增至任何其他連絡人資料夾的使用者建立。

來電者識別碼查詢整合連絡人的彙總，使其搜尋整個外部連絡人。**PersonID**屬性，其中呈現與值設為 Null，只要可改善使用者經驗的來電者識別碼解析度來隱藏除數重複的相符項目相關聯之相同的人員的連絡人。由於 PersonID 屬性是在這兩個結果相同、 UM 將它視為相符項目至單一連絡人。

## 語音平台與語音辨識的加強功能

Exchange Server 2013 UM 為語音平台與語音辨識導入部分加強功能，包括：

  - 語音郵件預覽的加強功能與更佳精確度。

  - 支援[Microsoft Speech Platform – 執行階段 （版本 11.0）](https://go.microsoft.com/fwlink/p/?linkid=253196)。

  - 使用組織的系統信箱進行語音文法產生作業。

Exchange 整合通訊使用靜態及動態語音文法辨識命令、 全域通訊清單 (GAL) 中的連絡人的名稱及使用者的信箱中的個人連絡人的名稱。今天、 Exchange Server 2013，在執行 Microsoft Exchange 整合通訊服務的每個信箱伺服器產生安裝在其上的所有 UM 語言的文法預先載入並將其儲存在目錄中。每個信箱伺服器儲存每個可能文法，則會產生其中的撥號對應表、 自動語音應答與已安裝 UM 語言數為基礎。

UM 用文法檔案來讓來電者使用語音來尋找在組織中的使用者。檔案的信箱助理員更新每 24 小時。在Exchange 2007和Exchange 2010 GGG.exe 命令進行可以手動更新而不需要等候排定更新的文法檔案。在Exchange Server 2013、 解決 ASR 文法產生擴充性的問題 UM、 GAL 文法產生工作不會再發生之伺服器安裝 Unified Messaging server role 與 speech。而發生情況定期使用信箱助理員，Mailbox server 上執行 Microsoft Exchange 整合通訊服務主控組織的仲裁信箱。GAL 語音文法檔案會儲存在組織的仲裁信箱並稍後下載至 Exchange 組織中所有 Mailbox server。預設會在信箱助理員執行每隔 24 小時。您可以使用**Set-MailboxServer**指令程式來調整頻率。

## 指令程式更新

針對Exchange 2013，許多 UM 指令程式已帶來了從Exchange 2010。不過，變更已出在某些指令程式，並已新增新的指令程式的新功能。如需詳細資訊，請參閱[整合的通訊 cmdlet 更新](unified-messaging-cmdlet-updates-exchange-2013-help.md)。

