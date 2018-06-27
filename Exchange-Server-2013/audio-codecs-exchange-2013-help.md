---
title: '音訊轉碼器: Exchange 2013 Help'
TOCTitle: 音訊轉碼器
ms:assetid: 6c39d65c-c2d3-4128-aae9-8596602819c3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa998670(v=EXCHG.150)
ms:contentKeyID: 54652592
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 音訊轉碼器

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2016-12-09_

整合通訊 (UM) 使用音訊轉碼器來儲存語音信箱訊息。VoIP 閘道或 IP Private Branch eXchange (PBX) 與 Mailbox Server (執行 Microsoft Exchange Unified Messaging 服務) 或 Client Access Server (執行 Microsoft Exchange Unified Messaging Call Router 服務) 之間，使用另一種轉碼器。整合通訊可以使用下列四個音訊轉碼器中的任何一個來建立和儲存語音訊息：

  - MP3 (預設值)

  - Windows Media 音訊 (WMA)

  - 群組系統電話 (GSM) 06.10

  - G.711 脈衝碼調制 (PCM) 線性

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>G.711 (PCMA 和 PCMU) 和 G.723.1 轉碼器是 VoIP 閘道與 Client Access Server 和 Mailbox Server 之間使用的 VoIP 轉碼器。</td>
</tr>
</tbody>
</table>


規劃 UM 系統時，需要根據組織的需求來選取正確的音訊轉碼器。本主題討論 UM 可使用的音訊轉碼器，可利用它來協助規劃 UM 部署。

## 轉碼器

英文的 *codec (轉碼器)*一詞是由「coding (編碼)」和「decoding (解碼)」二字所組成，用於數位音訊資料上。轉碼器是一種軟體程式，負責將數位資料轉換成音訊檔案格式或音訊資料流格式。轉碼器可用來將類比音訊信號轉換成數位版本的音訊信號。根據聲音品質，使用所需頻寬以及執行編碼的所需系統需求而定，轉碼器可分成許多種類。

整合通訊中使用兩種轉碼器：

  - VoIP 閘道、IP PBX 或已啟用 SIP 的 PBX 與 Client Access Server 和 Mailbox Server 之間，或 PBX 與 VoIP 閘道之間，所使用的轉碼器。

  - 供使用者用來編碼和儲存語音訊息的轉碼器。

透過公用交換電話網路 (PSTN) 使用普通電話時，您的聲音是以類比格式透過電話線傳輸出去。但使用 VoIP 時，您的聲音就必須轉換成數位信號。此轉換程序稱為編碼。轉碼器會執行編碼。數位化語音到達目的地後，接著必須解碼回到其原始類比格式，如此通話另一端的人才能聽得懂來電者在說什麼。

## VoIP 轉碼器

在 UM 中，VoIP 閘道或 IP PBX 與 Client Access Server 和 Mailbox Server 之間可以使用三種轉碼器：

  - G.711 µ-law

  - G.711 A-law

  - G.723.1

G.711 是專為供音訊轉碼器使用而開發的標準。G.711 標準中有兩種主要演算法定義：µ-law 演算法用於北美洲和日本，而 A-law 演算法用於歐洲和其他國家。G.723.1 音訊轉碼器大部分用於 VoIP 應用程式，而且需要授權才能使用。G.723.1 是高品質、高壓縮類型的轉碼器。

Client Access Server 或 Mailbox Server 和受支援的 VoIP 閘道或 IP PBX 都能同時提供 G.711 和 G.723.1 轉碼器。預設會優先使用 G.723.1 轉碼器。如果您要在 Client Access Server 和 Mailbox Server 與 VoIP 閘道或 IP PBX 之間使用 G.723.1 以外的轉碼器，建議您變更 VoIP 閘道或 IP PBX 上的組態。下表摘要說明一些常見的 VoIP 轉碼器。

### VoIP 轉碼器

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>VoIP 轉碼器</th>
<th>頻寬 (Kbps)</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>G.711</p></td>
<td><p>64</p></td>
<td><p>此轉碼器需要極低的處理能力。雙向通訊需要最少 128 Kbps。</p></td>
</tr>
<tr class="even">
<td><p>G.723.1</p></td>
<td><p>5.3/6.3</p></td>
<td><p>此轉碼器可提供高壓縮率與高品質音訊。所需要的處理能力比 G.711 轉碼器高。G.723.1 轉碼器使用的頻寬較低，但提供較差的音訊品質。</p></td>
</tr>
</tbody>
</table>


## UM 語音訊息儲存轉碼器

整合通訊撥號對應表是 UM 作業的必要部分。當您建立 UM 撥號對應表時，UM 撥號對應表預設會使用 MP3 音訊轉碼器來建立和儲存語音訊息。不過，您可以在建立 UM 撥號對應表後，將它設為使用 WMA、GSM 06.10 或 G.711 PCM 線性音訊轉碼器。

每種音訊轉碼器都有優缺點。MP3 因其聲音品質和壓縮內容，被選為預設的音訊轉碼器。GSM 06.10 和 G.711 PCM 線性音訊轉碼器則因其能夠支援其他類型的訊息系統，而併入可用的選項。

在規劃 UM 時，您必須對針對語音訊息建立的音訊檔案，平衡其大小和相對品質。一般來說，音訊檔案的位元速率越高，品質就越好。您還必須考量是否壓縮音訊檔案。下表顯示 UM 中使用的每個音訊轉碼器的範例位元速率 (位元/秒) 和壓縮內容。

### 預設 UM 語音訊息儲存轉碼器

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>語音訊息儲存轉碼器</th>
<th>位元</th>
<th>壓縮檔案？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MP3</p></td>
<td><p>16 位元</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>WMA</p></td>
<td><p>16 位元</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>G.711 PCM</p></td>
<td><p>16 位元</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>GSM 06.10</p></td>
<td><p>8 位元</p></td>
<td><p>是</p></td>
</tr>
</tbody>
</table>


在 UM 中，為語音訊息建立的檔案類型，取決於用來建立語音訊息音訊檔案的音訊轉碼器。MP3 音訊轉碼器會建立 .mp3 音訊檔案、WMA 音訊轉碼器會建立 .wma 音訊檔案，而 GSM 06.10 和 G.711 PCM 線性音訊轉碼器則會建立 .wav 音訊檔案。所有這些音訊檔案會隨著電子郵件一起傳送給語音訊息收件者。

編碼和解碼數位資料經常會牽涉到壓縮和解壓縮，但並非絕對。音訊壓縮是一種資料壓縮，會讓音訊資料檔案變小。音訊轉碼器所用的音訊壓縮演算法會壓縮成 .wma 或 .wav 音訊檔案。在 UM 中，使用的音訊壓縮演算法類型，取決於 UM 撥號對應表內容中選取的音訊轉碼器類型。建立音訊檔案並進行壓縮後，便會將它附加到語音訊息內。

在壓縮和解壓縮期間，有時候會遺失數位資料的資訊。用來壓縮音訊檔案的壓縮比愈高，在轉換期間所遺失的資訊愈多。不過，因為音訊檔案的大小變小，所以使用的磁碟空間也跟著變小。相反地，壓縮比愈小，遺失的資訊愈少。但是因為每個音訊檔案都變大，所以必須使用較大的磁碟空間。

RTAudio 寬頻或高逼真度音訊錄製語音訊息也是可作為音訊轉碼器。不過，使用 RTAudio 高畫質音訊才可使用您已成功地整合通訊與整合[Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=202010)。若要啟用 RTAudio 做線路轉碼器，縮小或是寬頻、 UM 撥號對應表必須設定為工作階段初始通訊協定 (SIP) URI 類型撥號對應表和您必須設定來電接聽轉碼器上的撥號 MP3 或 WMA 啟用寬頻音訊 (16khz)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>未部署 Lync Server 的環境無法使用 RTAudio。這是因為在未整合 Lync Server 的環境中，撥號對應表會設為電話分機號碼或 E.164，而非 SIP URI。</td>
</tr>
</tbody>
</table>


每通來電都有兩個媒體資料流：輸入至 Client Access Server，以及從 Mailbox Server 輸出。當撥號對應表類型設為 SIP URI 且撥號對應表上的自動答錄轉碼器設為 MP3 或 WMA 時，Client Access Server 會嘗試為輸入媒體資料流選取 RTAudio VoIP 轉碼器。如果交涉成功，輸入資料流的 RTAudio 轉碼器就會用於自動答錄服務通話，或從 Lync 用戶端或伺服器發出的通話。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用「在電話上播放」功能撥出的通話不會使用 RTAudio 轉碼器。使用「在電話上播放」所撥出通話的輸入資料流會使用 G.711 或 G.723.1 轉碼器。</td>
</tr>
</tbody>
</table>


使用 RTAudio 轉碼器時，所錄製的語音訊息會以高逼真度進行錄音，並儲存為具有 .mp3 或 .wma 副檔名的音訊檔案，視如何設定撥號對應表而定。在 Outlook 或 Outlook Web App 中將這些語音訊息播放給使用者時，他們會聽到高逼真度音訊形式的語音訊息。若交涉失敗，則會使用 G.711 或 G.723.1 轉碼器。G.711 和 G.723.1 轉碼器都是窄頻轉碼器，將它們用作 VoIP 轉碼器時，語音訊息會錄製並儲存為窄頻音訊檔案，並具有 mp3 或 .wma 副檔名。

輸出媒體資料流則一律使用 G.711 或 G.723.1 轉碼器進行交涉。這表示來電者在電話中聽到的一定是窄頻音訊。這也適用於使用 Microsoft Lync Server 2010 或更新版本撥出電話的情況。

Mailbox Server 用來儲存語音訊息中音訊的音訊格式和轉碼器，不僅取決於撥號對應表上設定的音訊轉碼器，也取決於 UM 與 SIP 對等交涉的音訊位元速率。如果環境中包含 Lync Server 或 SIP 端點，則 Mailbox Server 也會與 SIP 對等交涉音訊轉碼器。例如，當交涉使用寬頻 RTAudio 做為線路轉碼器時，Mailbox Server 會根據撥號對應表的設定，使用 32 Kbps MP3 或 WMA 9.2 格式建立語音訊息。下表顯示語音訊息儲存音訊轉碼器和 VoIP 或所使用線路音訊轉碼器之間的關係。

### 儲存音訊轉碼器和 VoIP 或線路音訊轉碼器之間的關係

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>UM 撥號對應表上設定的音訊轉碼器</th>
<th>VoIP 或線路轉碼器 (窄頻) - G.723、G.711 或 RTAudio (8KHz)</th>
<th>VoIP 或線路轉碼器 (寬頻) - RTAudio (16KHz)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>G.711</p></td>
<td><p>G.711</p></td>
<td><p>不適用。如果撥號對應表設定為 G.711，Client Access Server 或 Mailbox Server 不會交涉寬頻音訊。</p></td>
</tr>
<tr class="even">
<td><p>WMA</p></td>
<td><p>WMA 9 Voice</p></td>
<td><p>WMA 9.2</p></td>
</tr>
<tr class="odd">
<td><p>GSM</p></td>
<td><p>GSM 6.10</p></td>
<td><p>不適用。如果撥號對應表設定為 GSM，Client Access Server 或 Mailbox Server 不會交涉寬頻音訊。</p></td>
</tr>
<tr class="even">
<td><p>MP3</p></td>
<td><p>MP3 (16 Kbps)</p></td>
<td><p>MP3 (32 Kbps)</p></td>
</tr>
</tbody>
</table>


回到頁首

## 調整 UM 訊息大小

您可以將整合通訊設定為使用下列四種音訊轉碼器的其中一項來建立語音訊息：MP3、WMA、GSM 06.10 和 G.711 PCM 線性。預設會選取 \[MP3\] 格式。

WMA 音訊轉碼器一律會儲存為 Windows 媒體格式，且附件的副檔名為 .wma。使用 GSM 或 G.711 PCM 線性音訊轉碼器編碼的音訊檔案一律會儲存為 RIFF/WAV 格式，且附件的副檔名為 .wav。

UM 語音訊息的大小視附件所包含的語音資料大小而定。而附件大小又視下列因素而定：

  - 語音信箱錄音的時間長短

  - 使用的音訊轉碼器

  - 音訊檔案儲存格式

下圖針對三種您可以在 UM 中使用的音訊轉碼器，說明語音信箱錄音的時間長短對音訊檔案大小的影響。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在此圖中，自動答錄之語音訊息的平均長度大約是 30 秒。</td>
</tr>
</tbody>
</table>


**音訊檔案大小**

![UM\_Message\_Sizing](images/Aa998670.76ca4891-450f-4ffd-9493-aac8d0d23a5d(EXCHG.150).gif "UM_Message_Sizing")

## MP3

根據預設，會選取 MP3 格式，而且 MP3 格式是語音信箱訊息的預設語音檔案格式。MP3 是一般的音訊檔案格式，除了可用來大幅減少音訊檔大小，還是個人音訊裝置或 MP3 播放器最常使用的音訊格式。MP3 是一種跨平台的音訊轉碼器類型，能夠與許多行動電話及裝置和不同電腦作業系統相容。

## WMA

WMA 是三種轉碼器中壓縮比最高的音訊轉碼器。壓縮後，每 10 秒音訊大約需要 11,000 個位元組。不過，.wma 檔案格式的標頭區段遠比 .wav 檔案格式大。.wma 檔案的標頭區段大約是 7 KB，而 .wav 檔案的標頭區段則小於 100 個位元組。雖然 WMA 音訊記錄記錄了超過 15 秒的時間，所需空間卻比 GSM 音訊記錄小。因此，若需要最小但品質最高的音訊檔案，請使用 WMA 音訊轉碼器。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您對裝置的 OWA 使用內部部署的推播通知，則您無法使用 WMA 格式。裝置的 OWA 只支援 MP3 檔案格式。</td>
</tr>
</tbody>
</table>


## G.711 PCM 線性

G.711 PCM 線性音訊轉碼器會建立未壓縮的 .wav 音訊檔案。因此，在時間長短相同的狀況下，與 GSM 和 WMA 音訊轉碼器相比較下，G.711 PCM 線性 .wav 音訊檔案都會佔用最大的空間。G.711 PCM 線性 .wav 音訊檔案每 10 秒的音訊會佔用超過 160,000 個位元組的空間。在 UM 使用的三種音訊轉碼器中，G.711 PCM 線性 .wav 音訊檔案擁有最高的音訊品質。不過，對大部分聽取語音訊息的使用者而言，使用 WMA 和 GSM 音訊轉碼器建立的音訊檔案，其品質都足以滿足他們的需要。

## GSM

GSM 音訊轉碼器會建立壓縮的 .wav 音訊檔案。GSM .wav 音訊檔案每 10 秒的音訊會佔用超過 16,000 個位元組的空間。不過，GSM 建立的音訊檔案會大於使用 WMA 音訊轉碼器建立的音訊檔案。因此，當您需要在語音訊息的品質與大小間取得平衡時，這就不是最佳的選擇。

回到頁首

