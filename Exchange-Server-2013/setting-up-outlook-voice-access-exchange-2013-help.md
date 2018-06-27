---
title: '設定 Outlook 語音存取: Exchange Online Help'
TOCTitle: 設定 Outlook 語音存取
ms:assetid: 5ce8c877-35f3-4e55-a65e-5ca469aeae99
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd298010(v=EXCHG.150)
ms:contentKeyID: 50553998
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定 Outlook 語音存取

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2015-03-09_

Outlook Voice Access 可讓已啟用 Exchange 整合通訊 (UM) 的使用者透過類比電話、數位電話或行動電話存取其信箱。

Outlook 語音存取使用者 （也稱為 「*訂閱者*」），為使用者啟用整合通訊之組織中。訂閱者存取其信箱的擷取電子郵件、 語音信箱訊息、 個人連絡人和行事曆資訊的電話使用 Outlook 語音存取。

**目錄**

Outlook Voice Access overview

Outlook Voice Access interfaces

Outlook Voice Access scenarios

Distribution groups and contact groups

Choosing a language

Controlling Outlook Voice Access features

## Outlook Voice Access 概觀

在 \[Microsoft Exchange UM、 已啟用 UM 之使用者可撥打 UM 撥號對應表來存取其信箱並使用 Outlook 語音存取功能表系統上所設定的內部或外部的電話號碼。使用此功能表、 已啟用 UM 的使用者可以讀取電子郵件、 聆聽語音訊息、 互動其Outlook行事曆、 存取其個人連絡人，以及執行像是工作設定其Outlook語音存取 PIN 和通話記錄其語音信箱問候語。

兩種類型的使用者驗證且未經驗證的可撥打 Outlook 語音存取號碼。當未經驗證的使用者撥入 UM 撥號對應表上所設定的 Outlook 語音存取號碼時，則它們會僅能執行目錄搜尋使用者。已驗證的使用者所輸入他們的 pin 碼可以執行目錄搜尋並登入他們的信箱來接聽電子郵件、 行事曆項目和語音信箱，並搜尋個人連絡人。他們所之後使用者位於搜尋目錄或個人連絡人中的使用者，他們可以將來電轉接至使用者或撥打給使用者的分機號碼。

## Outlook Voice Access 介面

Outlook 語音存取使用者兩個整合通訊的使用者介面可用： 電話使用者介面 (TUI) 和使用自動語音辨識 (ASR) 語音使用者介面 (VUI)。

使用者可以在 Outlook 語音存取使用 VUI 之前，它會在 UM 撥號對應表和 UM 信箱原則上必須啟用並也可為使用者啟用。根據預設，當您建立撥號對應表和 UM 信箱原則並啟用語音信箱使用者的使用者可以使用 ASR 或 Outlook 語音存取 VUI 瀏覽功能表、 訊息和其他選項。不過，即使使用者能夠使用 VUI，他們必須使用電話鍵台輸入其 PIN、 瀏覽個人選項及執行目錄搜尋。下表列出預設設定。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>UM 元件</th>
<th>預設設定</th>
<th>啟用 VUI 存取的 Exchange 管理命令介面範例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>UM 撥號對應表</p></td>
<td><p>已啟用</p></td>
<td><p><code>Set-UMDialPlan -id MyUMDialPlan -AutomaticSpeechRecognitionEnabled  $true</code></p></td>
</tr>
<tr class="even">
<td><p>UM 信箱原則</p></td>
<td><p>已啟用</p></td>
<td><p><code>Set-UMMaiboxPolicy -id MyUMPolicy -AllowAutomaticSpeechRecognition  $true</code></p></td>
</tr>
<tr class="odd">
<td><p>使用者的信箱</p></td>
<td><p>已啟用</p></td>
<td><p><code>Set-UMMailbox -id tonysmith -AutomaticSpeechRecognitionEnabled $true</code></p></td>
</tr>
</tbody>
</table>


下節包含描述 VUI 功能的案例。

回到頁首

## Outlook Voice Access 案例

以下範例示範如何從電話使用 Outlook Voice Access：

  - **存取電子郵件**  Outlook語音存取使用者撥打 Outlook 語音存取號碼從電話和想要存取其電子郵件。語音提示會說明 「 歡迎使用。您正在連線至MicrosoftExchange。若要存取您的信箱，請輸入您的擴充。若要連絡某人，按下井字鍵。 」使用者輸入信箱分機號碼、 語音提示會說明之後"請輸入您的 PIN 並按下井字鍵。"使用者輸入 PIN 語音提示會說明之後"您有兩個新的語音信箱、 10 新電子郵件訊息，且您下一次會議位於 10:00 A.M.請說的語音信箱、 電子郵件、 行事曆、 個人連絡人、 目錄或個人選項。 」當使用者選取"電子郵件 」 時、 語音郵件系統可讀取的郵件標頭，然後名稱、 主旨、 時間和使用者的信箱中之郵件的優先順序。

  - **存取行事曆**  Outlook語音存取使用者撥打 Outlook 語音存取號碼從電話和想要存取其行事曆。語音提示會說明 「 歡迎使用。您正在連線至MicrosoftExchange。若要存取您的信箱，請輸入您的擴充。若要連絡某人，按下井字鍵。 」使用者輸入信箱分機號碼、 語音提示會說明之後"請輸入您的 PIN 並按下井字鍵。"使用者輸入 PIN 語音提示會說明之後"您有兩個新的語音信箱、 10 新電子郵件訊息，且您下一次會議位於 10:00 A.M.請說的語音信箱、 電子郵件、 行事曆、 個人連絡人、 目錄或個人選項。 」當使用者顯示 「 行事曆，"語音郵件系統指出，"確定，且哪一天應該我 open?"表示使用者，"今天的行事曆 」。語音郵件系統回應的說明，"今天開啟的 \[行事曆。 」語音郵件系統會將使用者讀取那天的每個行事曆約會。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果執行 Microsoft Exchange 整合通訊服務的信箱伺服器在使用者的信箱中遇到損毀的行事曆項目，將無法唸出該項目，而使來電者回到 Outlook Voice Access 主功能表，並且不會唸出排定於當日其餘時間的其他任何會議。</td>
    </tr>
    </tbody>
    </table>


  - **存取語音信箱**  Outlook語音存取使用者撥打 Outlook 語音存取號碼從電話和想要存取語音信箱。語音提示會說明 「 歡迎使用。您正在連線至MicrosoftExchange。若要存取您的信箱，請輸入您的擴充。若要連絡某人，按下井字鍵。 」使用者輸入信箱分機號碼、 語音提示會說明之後"請輸入您的 PIN 並按下井字鍵。"使用者輸入 PIN 語音提示會說明之後"您有兩個新的語音信箱、 10 新電子郵件訊息，且您下一次會議位於 10:00 A.M.請說的語音信箱、 電子郵件、 行事曆、 個人連絡人、 目錄或個人選項。 」使用者顯示 \[現在"Voice mail"和語音郵件系統可讀取的郵件標頭，然後名稱、 主旨、 時間和使用者的信箱中的語音訊息的優先順序。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果已啟用語音辨識，使用者可以存取已啟用 UM 的信箱使用語音輸入。訂閱者也可以使用按鍵式、 也稱為複頻式訊號 (DTMF) 按 0。語音辨識並未啟用 PIN 輸入。</td>
    </tr>
    </tbody>
    </table>


  - **尋找目錄中的使用者**  Outlook語音存取使用者撥打 Outlook 語音存取號碼從電話和想要尋找人員目錄中的拼字檢查其電子郵件別名。語音提示會說明 「 歡迎使用。您正在連線至MicrosoftExchange。若要連絡某人，按下井字鍵。 」使用者按下井字鍵，並再使用按鍵式輸入拼字之人員的 SMTP 位址。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>與 Outlook 語音存取號碼的目錄搜尋功能並未啟用語音功能。使用者可以拼字他們想要只能透過使用按鍵式輸入連絡的人員名稱。</td>
    </tr>
    </tbody>
    </table>
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>在某些 companies （特別是在東亞） office 散可能沒有字母電話的機碼。這會使按鍵介面幾乎無法使用的按鍵對應工作不知情的情況下會使用 「 拼字名稱 」 功能。根據預設，整合通訊使用 E.161 按鍵對應。例如，2 = ABC、 3 = DEF、 4 = GHI，5 = JKL、 6 = MNO，7 = PQRS，8 = TUV，9 = WXYZ。</td>
    </tr>
    </tbody>
    </table>
    
    當輸入的字母和數字，例如 Mike1092 組合數值的數字會對應至其本身。輸入正確的 Mike1092 電子郵件別名，使用者必須按 64531092 的數字。此外，A-Z 和 0-9 以外的字元，沒有電話按鍵相等。因此，不應輸入這些字元。例如，電子郵件別名 jim.wilson 應輸入為 546945766。即使有要輸入的 10 個字元，使用者會進入僅 9 的數字因為會不有任何數字相等的句點 （.）。

回到頁首

## 通訊群組和連絡人群組

使用者可以使用Outlook語音存取傳送或轉寄的語音訊息、 電子郵件訊息或會議邀請。可傳送或轉寄郵件或會議邀請至下列任一項：

  - \[個人通訊錄\] 資料夾中的人員

  - 組織共用通訊錄中的人員

  - 已在 \[連絡人\] 資料夾中建立的連絡人群組

  - 組織共用通訊錄中包含的通訊群組

使用 VUI （如果已開啟 ASR） 或其電話鍵盤上使用按鍵式輸入可以傳送郵件和會議邀請。他們也可以使用Outlook語音存取聆聽的詳細資訊\] 群組中，包括群組的成員。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果使用者嘗試傳送郵件給不包含任何成員群組 （其共用的通訊錄中的通訊群組），或是其個人的 [連絡人] 資料夾中的連絡人群組，語音郵件系統將不會授與 [傳送或轉寄郵件或會議邀請] 選項。如果嘗試將群組新增不含成員為其中一個收件者的郵件或會議邀請中他們建立透過電話、 語音郵件系統將不會將群組新增至郵件和會說&quot;可能不傳送的郵件是因為連絡人似乎不在具有有效的電子郵件地址。 」</td>
</tr>
</tbody>
</table>


## 選擇語言

使用者無法變更語言該Outlook語音存取来立即給他們的用途與他們使用時所回覆給它。語音郵件系統會嘗試尋找及使用最符合的使用者選擇當他們登入MicrosoftOutlook Web App或他們選擇於Outlook Web App的地區設定的語言的語言。如果他們選擇的語言不受支援Outlook語音存取、 語音郵件系統會使用來電者聽到其以留下語音訊息出現提示時的相同語言。

回到頁首

## 控制 Outlook Voice Access 功能

根據預設，當使用者撥入 Outlook 語音存取，他們可以使用電話，以存取其行事曆、 電子郵件、 和個人連絡人及搜尋目錄。您可以使用命令介面來防止使用者存取其信箱 Outlook 語音存取時存取一或多個這些功能。當您修改 UM 信箱原則上的 Outlook 語音存取功能時，您的變更會影響所有與 UM 信箱原則相關聯的使用者。雖然其他功能只可停用 UM 信箱原則上和個別信箱上都無法提供您也可以停用單一使用者的信箱上的一些功能。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您只能使用命令介面來修改已啟用 UM 之使用者或 UM 信箱原則的 Outlook Voice Access TUI 設定。</td>
</tr>
</tbody>
</table>


**UM 信箱原則設定**  您可以停用使用者的存取權的 UM 信箱原則上的下列 Outlook 語音存取功能：

  - 自動語音辨識

  - 以無 PIN 碼的方式存取語音信箱

  - 以語音回應其他訊息

  - 以 TUI 存取其行事曆

  - 以 TUI 存取目錄

  - 以 TUI 存取其電子郵件

  - 以 TUI 存取其個人連絡人

**啟用 UM 功能的信箱設定**   您可以停用使用者存取其信箱上下列 Outlook Voice Access 功能的權限：

  - 以 TUI 存取行事曆

  - 以 TUI 存取電子郵件

  - 自動語音辨識

您可以防止使用者接收語音信箱，但是讓他們能夠存取使用Outlook語音存取其信箱保持不變。您可以啟用 UM 的使用者使用和設定使用者的信箱不目前正在使用的組織中的另一位使用者的分機號碼。

回到頁首

