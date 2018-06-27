---
title: 'UM 語言、 提示及問候語: Exchange 2013 Help'
TOCTitle: UM 語言、 提示及問候語
ms:assetid: d48df962-9669-420b-838f-44bfe1012e2f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124728(v=EXCHG.150)
ms:contentKeyID: 50474332
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# UM 語言、 提示及問候語

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2016-12-09_

您可以安裝並設定語言套件，以支援整合通訊 (UM) 環境中的多種語言。

UM 語言套件可讓來電者和 Outlook 語音存取使用者，以多種語言與語音郵件系統互動。您在信箱伺服器上安裝其他語言之後，來電者及 Outlook 語音存取使用者就能夠以這個語言聽到電子郵件並與語音郵件系統互動。

有數個依賴若要讓使用者與來電者互動有效地整合通訊多種語言的 UM 語言套件的重要元件。每個 UM 語言套件包含文字轉語音 (TTS) engine 預先錄製的提示和支援的特定語言的自動語音辨識 (ASR) 和語音郵件預覽。本主題討論的 UM 語言套件，使用的 UM 語言套件，以及如何 UM 語言套件的 UM 元件 — 他們正在安裝之後 — 可用以設定要使用其他語言的 UM 撥號對應表和 UM 自動語音應答。

Exchange整合的通訊語言套件的特定版本及平台特定。自Exchange Server 2007，已針對包括 RTM 版的Exchange 2007、 Exchange 2007 SP1、 SP2、 及 SP3、 Exchange Server 2010、 Exchange 2010 SP1 和 SP2 及Exchange 2013RTM 版本的 UM 語言套件的多個版本。某些這些版本的 32 位元和 64 位元下載項目，但其他版本的僅限 64 位元下載可用。

它是非常重要的信箱伺服器上安裝正確的版本及 UM 語言套件的平台。請勿執行舊版Exchange信箱伺服器上安裝 UM 語言套件或 32 位元平台所設計。

**目錄**

Overview of UM language packs

UM language components and features

Voice Mail Preview

Unified Messaging languages

Unified Messaging language packs

UM dial plan languages

UM auto attendant languages

Client language selection process

## UM 語言套件的概觀

整合的通訊語言套件可讓說話為來電者的其他語言和當來電者使用 ASR 或語音訊息 transcribed 辨識其他語言的信箱伺服器。UM 語言套件包含：

  - 預先錄製的 UM 語言套件的語言的提示。例如，"音後請記錄您的郵件。當您已完成錄製時，掛斷，或按 \# 鍵的更多選項\]。 」

  - UM 語言套件的語言文法檔案，信箱伺服器會使用這個檔案來查詢指定的使用者在目錄中的名稱。

  - 文字轉語音 (TTS) 轉譯，可以 UM 語言套件的語言向來電者唸出內容 (電子郵件、行事曆、連絡人資訊等等)。

  - 自動語音辨識支援，可讓來電者在語音使用者介面 (VUI) 中，以 UM 語言套件的語言與 UM 互動。

  - 語音信箱預覽支援，可讓使用者從支援的電子郵件用戶端 (例如 Outlook 或 Outlook Web App)，以特定語言閱讀語音信箱訊息的文稿。

UM 語言套件包含預先錄製的提示 TTS 轉換支援特定的語言，並在某些情況下，ASR 的支援。在多語言環境中，您可能因為某些來電者偏好在不同的語言，系統會提示或時接收電子郵件以多種語言安裝額外的 UM 語言套件。您必須安裝多個 UM 語言套件可支援讀取電子郵件因為 TTS 轉換系統必須包含一個以上的語言，指示要讀取郵件的文字為基礎的語言選取信箱伺服器的能力。如果尚未安裝整合通訊語言套件，電子郵件訊息都會不合邏輯與不一致時讀取傳回給使用者。安裝適當的語言套件可讓 TTS 引擎Outlook語音存取使用者讀取電子郵件和行事曆項目使用正確的語言和整合通訊\] 也提供特定語言的預先錄製的提示。在某些情況下，他們也可以提供 ASR 的支援。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>TTS 引擎將轉換成文字轉換語音，但它並不會為文字轉換語音。已啟用 UM 的使用者可以傳送電子郵件已附加至另一位使用者的語音檔案。不過，使用者無法建立與傳送文字型的電子郵件訊息給另一位使用者。</td>
</tr>
</tbody>
</table>


當您安裝語言套件時，安裝程式會執行下列動作：

1.  複製將用來設定 UM 撥號對應表及自動語音應答的語言提示。

2.  允許 TTS 引擎在 Outlook 語音存取使用者存取收件匣時閱讀郵件。

3.  對於安裝的語言，為擁有語音功能的 UM 撥號對應表及自動語音應答啟用 ASR。

4.  為用戶端啟用其他語言的語音信箱預覽。

您可以使用**Setup.exe**命令或您已從[Exchange Server 2013 UM 語言套件](https://go.microsoft.com/fwlink/p/?linkid=266542)下載 UM 語言套件之後執行*\<UMLanguagePack\>*.exe 安裝程式來新增 UM 語言套件。不過，您必須使用 Setup.exe 命令移除 UM 語言套件。有無Exchange Management Shell 指令程式可用於新增或移除語言從信箱伺服器。如需如何安裝 UM 語言套件的詳細資訊，請參閱[安裝 UM 語言套件](install-a-um-language-pack-exchange-2013-help.md)。如需如何移除 UM 語言套件的詳細資訊，請參閱[移除 UM 語言套件](remove-a-um-language-pack-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>根據預設，當您安裝信箱伺服器，美國英文 (EN-US) 安裝語言套件。除非電腦中移除的信箱伺服器即無法予以移除。</td>
</tr>
</tbody>
</table>


回到頁首

下表列出目前可用的整合通訊語言套件。它也會列出每個 UM 語言套件的安裝檔案名稱及 UM 語言的文化特性識別碼。

### UM 語言套件的安裝檔案名稱和文化特性 ID

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>語言</th>
<th>國家/地區</th>
<th>文化特性 ID</th>
<th>安裝檔案名稱</th>
<th>可用性</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>卡達隆尼亞文</p></td>
<td><p>西班牙</p></td>
<td><p>ca-ES</p></td>
<td><p>UMLanguagePack. ca-ES</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">下載可用</a></p></td>
</tr>
<tr class="even">
<td><p>中文 (香港)</p></td>
<td><p>中國</p></td>
<td><p>zh-HK</p></td>
<td><p>UMLanguagePack. zh-HK</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">下載可用</a></p></td>
</tr>
<tr class="odd">
<td><p>中文 (簡體)</p></td>
<td><p>中國</p></td>
<td><p>zh-CHS</p></td>
<td><p>UMLanguagePack.zh-CN</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">下載可用</a></p></td>
</tr>
<tr class="even">
<td><p>中文 (繁體)</p></td>
<td><p>台灣</p></td>
<td><p>zh-TW</p></td>
<td><p>UMLanguagePack.zh-TW</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">下載可用</a></p></td>
</tr>
<tr class="odd">
<td><p>丹麥文</p></td>
<td><p>丹麥</p></td>
<td><p>da-DK</p></td>
<td><p>UMLanguagePack.da-DK</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">下載可用</a></p></td>
</tr>
<tr class="even">
<td><p>荷蘭文</p></td>
<td><p>荷蘭</p></td>
<td><p>nl-NL</p></td>
<td><p>UMLanguagePack.nl-NL</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">下載可用</a></p></td>
</tr>
<tr class="odd">
<td><p>英文</p></td>
<td><p>澳洲</p></td>
<td><p>en-AU</p></td>
<td><p>UMLanguagePack.en-AU</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">下載可用</a></p></td>
</tr>
<tr class="even">
<td><p>英文</p></td>
<td><p>加拿大</p></td>
<td><p>en-CA</p></td>
<td><p>UMLanguagePack. en-CA</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">下載提供</a></p></td>
</tr>
<tr class="odd">
<td><p>英文</p></td>
<td><p>印度</p></td>
<td><p>en-IN</p></td>
<td><p>UMLanguagePack. en-IN</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">下載可用</a></p></td>
</tr>
<tr class="even">
<td><p>英文</p></td>
<td><p>英國</p></td>
<td><p>en-GB</p></td>
<td><p>UMLanguagePack.en-GB</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">下載可用</a></p></td>
</tr>
<tr class="odd">
<td><p>英文</p></td>
<td><p>美國</p></td>
<td><p>en-US</p></td>
<td><p>包含在信箱伺服器的安裝中</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">下載可用</a></p></td>
</tr>
<tr class="even">
<td><p>芬蘭文</p></td>
<td><p>芬蘭</p></td>
<td><p>fi-Fl</p></td>
<td><p>UMLanguagePack.fi-Fl</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">下載提供</a></p></td>
</tr>
<tr class="odd">
<td><p>法文</p></td>
<td><p>加拿大</p></td>
<td><p>fr-CA</p></td>
<td><p>UMLanguagePack.fr-CA</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">下載可用</a></p></td>
</tr>
<tr class="even">
<td><p>法文</p></td>
<td><p>法國</p></td>
<td><p>fr-FR</p></td>
<td><p>UMLanguagePack.fr-FR</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">下載可用</a></p></td>
</tr>
<tr class="odd">
<td><p>德文</p></td>
<td><p>德國</p></td>
<td><p>de-DE</p></td>
<td><p>UMLanguagePack.de-DE</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">下載提供</a></p></td>
</tr>
<tr class="even">
<td><p>義大利文</p></td>
<td><p>義大利</p></td>
<td><p>it-IT</p></td>
<td><p>UMLanguagePack.it-IT</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">下載可用</a></p></td>
</tr>
<tr class="odd">
<td><p>日文</p></td>
<td><p>日本</p></td>
<td><p>ja-JP</p></td>
<td><p>UMLanguagePack.ja-JP</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">下載可用</a></p></td>
</tr>
<tr class="even">
<td><p>韓文</p></td>
<td><p>韓文</p></td>
<td><p>ko-KR</p></td>
<td><p>UMLanguagePack.ko-KR</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">下載可用</a></p></td>
</tr>
<tr class="odd">
<td><p>挪威文 (巴克摩)</p></td>
<td><p>挪威</p></td>
<td><p>nb-NO</p></td>
<td><p>UMLanguagePack.nb-NO</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">下載可用</a></p></td>
</tr>
<tr class="even">
<td><p>波蘭文</p></td>
<td><p>波蘭</p></td>
<td><p>pl-PL</p></td>
<td><p>UMLanguagePack.pl-PL</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">下載可用</a></p></td>
</tr>
<tr class="odd">
<td><p>葡萄牙文</p></td>
<td><p>巴西</p></td>
<td><p>pt-BR</p></td>
<td><p>UMLanguagePack.pt-BR</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">下載可用</a></p></td>
</tr>
<tr class="even">
<td><p>葡萄牙文</p></td>
<td><p>葡萄牙</p></td>
<td><p>pt-PT</p></td>
<td><p>UMLanguagePack.pt-PT</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">下載可用</a></p></td>
</tr>
<tr class="odd">
<td><p>俄文</p></td>
<td><p>俄羅斯</p></td>
<td><p>ru-RU</p></td>
<td><p>UMLanguagePack. ru-RU</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">下載可用</a></p></td>
</tr>
<tr class="even">
<td><p>西班牙文</p></td>
<td><p>西班牙</p></td>
<td><p>es-ES</p></td>
<td><p>UMLanguagePack.es-ES</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">下載提供</a></p></td>
</tr>
<tr class="odd">
<td><p>西班牙文</p></td>
<td><p>墨西哥文</p></td>
<td><p>es-MX</p></td>
<td><p>UMLanguagePack.es-MX</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">下載可用</a></p></td>
</tr>
<tr class="even">
<td><p>瑞典文</p></td>
<td><p>瑞典</p></td>
<td><p>sv-SE</p></td>
<td><p>UMLanguagePack.sv-SE</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">下載可用</a></p></td>
</tr>
</tbody>
</table>


回到頁首

## UM 語言元件及功能

有數個重要元件和整合通訊中的功能可以讓使用者與來電者與多語言語音郵件系統互動。這些元件及正常運作，並啟用來電者與多種語言的系統互動功能、 UM 語言套件必須安裝正確的信箱伺服器上。

## 預錄的提示

包含一組的預設音訊提示檔安裝 Mailbox server role。這些音訊檔包含Outlook語音存取功能表、 語音信箱問候語，及Exchange所使用的數字錄製整合通訊。音訊檔會在信箱伺服器所扮演傳入呼叫端注意事項內部和外部。許多音訊檔所提供的電話使用者介面 (TUI) 和Outlook語音存取使用者所需 TUI 和語音使用者介面 (VUI) 瀏覽資訊的預設提示。提示位於 \<*Program Files*\> \\Microsoft\\Exchange Server\\V15\\UnifiedMessaging\\Prompts\\ \< 語言 \>。不應該取代或變更信箱伺服器所用來幫助來電者瀏覽功能表提示。

在安裝額外的 UM 語言套件時也要安裝之語言的預先錄製的提示。安裝 UM 語言套件之後，該語言的記錄前提示可用的 UM 撥號對應表和自動語音應答。

## TTS 語言

整合的通訊依賴文字轉語音 (TTS) 引擎。TTS 功能是由Microsoft Speech Server 服務所提供。TTS 引擎會讀取和撰寫的文字轉換可以由來電者聽到的音效輸出。TTS 引擎會讀取並將轉換成使用者的信箱中的下列項目：

  - 電子郵件及語音信箱訊息內文、主旨及名稱

  - 行事曆項目內文、主旨、位置及名稱

  - 個人連絡名稱

  - 使用者的預設語音信箱問候語

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在使用者錄製個人化的語音信箱問候之後，將不再使用其語音問候的 TTS 版本。</td>
</tr>
</tbody>
</table>


## 自動語音辨識

除了 TTS、 ASR 支援隨附於整合通訊。ASR 功能是由Microsoft Speech Server 服務所提供。ASR 可讓來電者使用語音命令來功能表瀏覽和互動從其個別的信箱，包括郵件、 個人連絡人和行事曆項目。ASR 支援所含每種語言套件。

回到頁首

## 語音信箱預覽

UM 語言套件也提供語音信箱預覽支援，可讓使用者透過從 Outlook 或 Outlook Web App 之類支援的電子郵件用戶端內讀取其文稿，快速分類其語音訊息。

當來電者留下語音訊息給已啟用 UM 的使用者，語音訊息檔案和語音訊息的文稿會置於傳送到使用者信箱的語音訊息的本文中。

所有的 UM 語言套件是可以下載的單一檔案。這些語言套件包括預先錄製的提示、 文法檔案、 文字轉語音 (TTS) 轉譯及 ASR。不過，不是所有的 UM 語言套件包含語音郵件預覽的支援。

下列 UM 語言套件支援所有元件和功能，包含語音信箱預覽：

  - 英文 (美國) - (en-US)

  - 英文 (加拿大)(en-CA)

  - 法文 (法國) - (fr-FR)

  - 義大利文 - (it-IT)

  - 波蘭文 (pl-PL)

  - 葡萄牙文 (葡萄牙) (pt-PT)

  - 西班牙文 (西班牙) (es-ES)

根據預設，如果安裝支援的 UM 語言套件，則在安裝信箱伺服器後，該伺服器會向啟用 UM 的使用者傳送語音信箱預覽。

有提供增強的記錄支援語音郵件預覽\] 功能的整合通訊語音郵件預覽協力廠商。這些協力廠商採用更正語音郵件 transcriptions 使用 ASR 所建立的人員。每個語音郵件預覽協力廠商必須符合一組認證與整合通訊互通硬體需求。

如果您發現語音郵件預覽傳送給您的使用者不正確足夠、 您可以連絡其中一個認證的語音郵件預覽夥伴列上[的整合通訊的 Microsoft Pinpoint](https://go.microsoft.com/fwlink/p/?linkid=261951)頁面並簽署向上與其在額外的成本。

您可以從[Microsoft 下載中心](https://go.microsoft.com/fwlink/p/?linkid=266542)下載的 UM 語言套件。如需詳細資訊，請參閱[安裝 UM 語言套件](install-a-um-language-pack-exchange-2013-help.md)。

## 整合通訊語言

若要讓來電者在使用整合通訊中的多個語言功能，您必須先安裝 UM 語言套件。然後您必須選擇設定其他 UM 元件。

  - 在您的組織中的信箱伺服器上安裝 UM 語言套件。

  - 視需要設定 UM 撥號對應表的預設語言。這可讓Outlook語音存取使用者相關聯 UM 存取其信箱時的撥號對應表計劃使用新的語言。不過，使用者仍然可以設定其語言設定之Outlook Web App \] 選項。

  - 如果您需要啟用自動語音應答上的多種語言，請在 UM 自動語音應答上設定的語言設定。根據預設，UM 自動語音應答使用 UM 撥號對應表計劃語言。不過，您可以變更此設定並啟用未經過驗證的來電者能夠連線至您的組織並瀏覽自動語音應答功能表您在 UM 自動語音應答所指定的語言。

## 整合通訊語言套件

您使用 Setup.exe 的信箱伺服器上安裝 UM 語言套件。安裝新的語言套件之後，相關聯的語言套件的語言會新增至您可以使用的可用語言清單。您可以檢視Exchange管理命令介面中使用[Get-UMService](https://technet.microsoft.com/zh-tw/library/jj552407\(v=exchg.150\))指令程式已安裝的語言。

當您安裝 UM 語言套件，TTS 引擎所使用的檔案，或所選語言記錄前提示會複製及可供連線到語音信箱系統的使用者。您可以從[Microsoft 下載中心](https://go.microsoft.com/fwlink/p/?linkid=266542)下載的 UM 語言套件。如需詳細資訊，請參閱[安裝 UM 語言套件](install-a-um-language-pack-exchange-2013-help.md)。

## UM 撥號對應表語言

每個 UM 撥號對應表會建立包含預設的語言設定。UM 撥號對應表計劃語言設定，就需要因為整合通訊可能會需要使用 TTS 轉換或播放Outlook標準音訊提示語音存取使用者存取其信箱時。您不需要選取預設撥號計劃語言。

當您第一次安裝 Exchange、 美國英文會的預設語言，與您的撥號計劃的唯一可用的語言選項。在信箱伺服器上安裝 UM 語言套件之後，相關聯的語言套件的語言會被列為可用的選項設定撥號對應表的預設語言時。

預設的語言，請務必為來電者。當Outlook語音存取使用者撥打到語音郵件系統時，所使用的語言根據Outlook Web App的下限設為當使用者第一次登入他們的信箱中的語言設定。整合的通訊會比較在Outlook Web App在撥號對應表與使用者相關聯的可用語言的清單中設定的語言。沒有適當的相符時，會使用預設 UM 撥號對應表的計劃語言。例如，如果您有撥號對應表包含從法國的使用者，您可能要撥號對應表的預設語言設定變更為法文。

## UM 自動語音應答語言

根據預設，UM 自動語音應答與相關聯 UM 撥號對應表正在建立時，因為他們會使用預設的語言設定的相關聯的 UM 撥號。不過，建立 UM 自動語音應答後可變更此設定。

因為整合通訊可能會需要使用 TTS 轉換或來電者播放標準的音訊提示，則需要的 UM 自動語音應答的語言設定。整合的通訊不會檢查的自動語音應答自訂提示的語言是否符合上的自動語音應答的語言設定。不過，最佳作法，請確定自訂提示的語言相符的自動語音應答的語言設定。否則，來電可能會聽到至另一種語言的系統 shift 鍵。

如果您需要對來電者使用數種不同語言特有的自動語音應答，則變更 UM 自動語音應答語言設定也匯很有幫助。

## 用戶端語言選擇程序

UM 語言套件啟用來電者與Outlook語音存取使用者與整合通訊中的系統多種語言進行互動。在信箱伺服器上安裝其他語言套件之後，來電者與Outlook Voice Access 使用者能夠聽到電子郵件和互動的語音信箱系統和Outlook Web App使用者和使用Outlook 2010或更新版本的使用者可以檢視使用中特定語言的語音信箱預覽語音訊息的記錄。

若要支援特定的語言，必須在各個信箱伺服器上安裝該語言的 UM 用戶端語言套件。

在某些情況下，如果針對特定語言的 UM 語言套件尚未已安裝且無法使用，可能會使用用戶端遞補語言。是要取代某些語言使用可用的後援 UM 用戶端語言但為其他語言，沒有遞補語言可供。如果沒有針對特定的語言安裝 UM 語言套件並沒有遞補語言可供該語言，會使用 EN-US （美式英文）。

以下表格包含了在特定的 UM 語言套件未安裝在信箱伺服器上時，將採用的用戶端語言與後援語言的清單。

### UM 的用戶端後援語言

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>語言</th>
<th>國家/地區</th>
<th>文化特性 ID</th>
<th>第一個選擇的語言 (如有安裝)</th>
<th>第二個選擇的語言 (如有安裝)</th>
<th>第三個選擇的語言 (如有安裝)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>卡達隆尼亞文</p></td>
<td><p>西班牙</p></td>
<td><p>ca-ES</p></td>
<td><p>ca-ES</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>中文 (香港)</p></td>
<td><p>中國</p></td>
<td><p>zh-HK</p></td>
<td><p>zh-HK</p></td>
<td><p>zh-CN</p></td>
<td><p>zh-TW</p></td>
</tr>
<tr class="odd">
<td><p>中文 (簡體)</p></td>
<td><p>中國</p></td>
<td><p>zh-CN</p></td>
<td><p>zh-CN</p></td>
<td><p>zh-HK</p></td>
<td><p>zh-TW</p></td>
</tr>
<tr class="even">
<td><p>中文 (繁體)</p></td>
<td><p>台灣</p></td>
<td><p>zh-TW</p></td>
<td><p>zh-TW</p></td>
<td><p>zh-HK</p></td>
<td><p>zh-CN</p></td>
</tr>
<tr class="odd">
<td><p>丹麥文</p></td>
<td><p>丹麥</p></td>
<td><p>da-DK</p></td>
<td><p>da-DK</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>荷蘭文</p></td>
<td><p>荷蘭</p></td>
<td><p>nl-NL</p></td>
<td><p>nl-NL</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>英文</p></td>
<td><p>澳洲</p></td>
<td><p>en-AU</p></td>
<td><p>en-AU</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>英文</p></td>
<td><p>加拿大</p></td>
<td><p>en-CA</p></td>
<td><p>en-CA</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>英文</p></td>
<td><p>印度</p></td>
<td><p>en-IN</p></td>
<td><p>en-IN</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>英文</p></td>
<td><p>英國</p></td>
<td><p>en-GB</p></td>
<td><p>en-GB</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>英文</p></td>
<td><p>美國</p></td>
<td><p>en-US</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>芬蘭文</p></td>
<td><p>芬蘭</p></td>
<td><p>fi-FL</p></td>
<td><p>fi-FL</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>法文</p></td>
<td><p>加拿大</p></td>
<td><p>fr-CA</p></td>
<td><p>fr-CA</p></td>
<td><p>fr-FR</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="even">
<td><p>法文</p></td>
<td><p>法國</p></td>
<td><p>fr-FR</p></td>
<td><p>fr-FR</p></td>
<td><p>fr-CA</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="odd">
<td><p>德文</p></td>
<td><p>德國</p></td>
<td><p>de-DE</p></td>
<td><p>de-DE</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>義大利文</p></td>
<td><p>義大利</p></td>
<td><p>it-IT</p></td>
<td><p>it-IT</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>日文</p></td>
<td><p>日本</p></td>
<td><p>ja-JP</p></td>
<td><p>ja-JP</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>韓文</p></td>
<td><p>韓國</p></td>
<td><p>ko-KR</p></td>
<td><p>ko-KR</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>挪威文 (巴克摩)</p></td>
<td><p>挪威</p></td>
<td><p>nb-NO</p></td>
<td><p>nb-NO</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>波蘭文</p></td>
<td><p>波蘭</p></td>
<td><p>pl-PL</p></td>
<td><p>pl-PL</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>葡萄牙文</p></td>
<td><p>巴西</p></td>
<td><p>pt-BR</p></td>
<td><p>pt-BR</p></td>
<td><p>pt-PT</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="even">
<td><p>葡萄牙文</p></td>
<td><p>葡萄牙</p></td>
<td><p>pt-PT</p></td>
<td><p>pt-PT</p></td>
<td><p>pt-BR</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="odd">
<td><p>俄文</p></td>
<td><p>俄羅斯</p></td>
<td><p>ru-RU</p></td>
<td><p>ru-RU</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>西班牙文</p></td>
<td><p>西班牙</p></td>
<td><p>es-ES</p></td>
<td><p>es-ES</p></td>
<td><p>es-MX</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="odd">
<td><p>西班牙文</p></td>
<td><p>墨西哥文</p></td>
<td><p>es-MX</p></td>
<td><p>es-MX</p></td>
<td><p>es-ES</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="even">
<td><p>瑞典文</p></td>
<td><p>瑞典</p></td>
<td><p>sv-SE</p></td>
<td><p>sv-SE</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


回到頁首

