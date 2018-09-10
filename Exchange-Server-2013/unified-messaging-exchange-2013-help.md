﻿---
title: '整合通訊: Exchange 2013 Help'
TOCTitle: 整合通訊
ms:assetid: 004b5d1a-cae8-4034-ab65-db41bd2f7b97
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ150478(v=EXCHG.150)
ms:contentKeyID: 50472445
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 整合通訊

 

_**適用版本：** Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：** 2016-12-09_

整合通訊 (UM) 可讓使用者使用的語音信箱和其他功能，包括 Outlook Voice Access 和通話自動答錄服務規則。UM 結合語音訊息和電子郵件訊息到一個可從許多不同的裝置存取的信箱。使用者可以從其電子郵件收件匣或從任何電話使用 Outlook 語音存取聆聽自己的郵件。可控制使用者如何將撥出電話從 UM，與經驗時在他們撥入貴組織有人員。

今天、 it 專業人員適用經常管理語音信箱或的電話語音網路和其組織的電子郵件系統或資料網路為不同的系統。語音信箱和電子郵件位於不同架設在不同的伺服器存取透過電子郵件的桌面以及透過電話的語音信箱的收件匣。

整合的通訊會可能Exchange管理員結合語音訊息和電子郵件訊息到一個信箱讓使用者可以收聽其收件匣中或從任何電話使用 Outlook Voice Access 其語音信箱訊息。它會使用 Exchange 儲存區的電子郵件和語音訊息。

**目錄**

New features

Unified Messaging features

Planning and deploying UM

Managing UM with the EAC and the Shell

Unified Messaging documentation

## 新功能

整合通訊 (UM) 功能最初使用在 Microsoft Exchange Server 2007和也Exchange 2010中提供。舊版的Exchange等同Exchange 2013中設定整合通訊功能。不過，已新增新功能與已架構變更。整合的通訊現在會被視為Exchange 2013中提供的語音相關功能的元件或子功能。在 Exchange 管理命令介面 cmdlet 及 UM 相關服務及所有整合通訊元件仍廣泛使用*整合通訊*的詞 — 包括撥號計劃、 自動語音應答、 UM 信箱原則，以及 UM IP 閘道器 — 能夠管理這些 UM 元件，以及位於內功能窗格的 Exchange 系統管理中心 (EAC) 中的 \[整合通訊\] 節點。

下列主題是 Exchange 2013 整合通訊中找到的新功能或加強功能之相關資訊的入門：

  - [語音的結構變更](voice-architecture-changes-exchange-2013-help.md)

  - [整合通訊中的 IPv6 支援](ipv6-support-in-unified-messaging-exchange-2013-help.md)

  - [語音郵件預覽增強功能](voice-mail-preview-enhancements-exchange-2013-help.md)

  - [整合的通訊 cmdlet 更新](unified-messaging-cmdlet-updates-exchange-2013-help.md)

回到頁首

## 整合通訊功能

整合通訊中找到的語音信箱功能為使用者與 IT 系統管理員提供各種好處。

## 適用於使用者的功能

當您部署整合通訊時，使用者可以存取語音信箱、 電子郵件、 和例如位在電子郵件用戶端從其信箱的行事曆資訊、 Outlook或MicrosoftOutlook Web App，從MicrosoftExchange ActiveSync設向上、 Windows電話，例如行動電話或從電話。此外，使用者可以使用下列功能：

  - **Exchange 資訊的存取權**Um 使用者可以從網際網路能夠行動電話、 MicrosoftOffice Outlook 2007或更新版本、 和Outlook Web App存取一組完整的語音信箱功能。這些功能包括許多語音郵件設定選項及 \[讀取窗格中，使用整合式的Windows Media Player\] 或 \[訊息\] 清單中，使用電腦的喇叭播放語音訊息的能力。

  - **在電話上播放**  Phone 功能上的播放讓啟用 UM 的使用者可以透過電話播放語音訊息。如果使用者在 office 隔間的運作方式、 使用在公用電腦或未啟用進行多媒體，或者接聽的是機密的語音郵件的電腦，他們可能不想要或能夠收聽透過電腦的喇叭語音訊息。它們可播放使用任何電話，包括住家、 辦公室或行動電話語音訊息。

  - **語音郵件表單**  語音郵件表單的格式類似於預設電子郵件表單。它提供使用者介面執行動作，例如播放、 停止或暫停語音訊息、 電話上播放語音訊息和新增與編輯附註。
    
    語音郵件表單包含內嵌的Windows Media Player 和音訊附註\] 欄位。內嵌的Windows Media Player 和附註\] 欄位會顯示 \[讀取窗格\] 中的使用者預覽語音訊息時或在不同的視窗中開啟語音訊息時。如果使用者未啟用整合通訊，或在支援的電子郵件用戶端尚未已安裝在用戶端電腦上，檢視做為電子郵件附件的語音郵件和語音郵件表單無法使用。

  - **使用者設定**  啟用整合通訊的使用者可以設定整合通訊使用Outlook Web App的數個語音信箱選項。例如，使用者可以設定電話存取號碼和語音郵件播放電話號碼，然後重設語音信箱存取 PIN。

  - **自動答錄服務**   自動答錄服務包括代表使用者接聽來電、播放他們的個人問候語、錄下訊息，並以電子郵件形式將其提交傳遞至他們的收件匣。

  - **自動答錄服務規則**  自動答錄服務規則可讓使用者已啟用語音信箱可讓您決定應如何處理其來電接聽的來電。自動答錄規則會套用至來電轉接的方式呼叫會類似收件匣規則會套用至內送電子郵件訊息的方式。根據預設，會設定沒有通話自動答錄服務規則。如果來電的信箱伺服器被接聽來電者會被提示留下語音訊息的呼叫方。使用自動答錄規則，來電者可以：
    
      - 為已啟用 UM 的使用者保留語音訊息。
    
      - 轉接至已啟用 UM 的使用者的其他連絡人。
    
      - 轉接至其他連絡人的語音信箱。
    
      - 轉接至已啟用 UM 的使用者設定的其他電話號碼。
    
      - 使用 \[尋找我\] 功能或透過轉接尋找已啟用 UM 的使用者。

  - **語音郵件預覽**  Mailbox server 會使用自動語音辨識 (ASR) 上新建立的語音信箱訊息。當使用者接收語音訊息時、 郵件包含錄製和與電話錄音會建立的文字。使用者看到從Outlook Web App或其他支援的電子郵件用戶端中的電子郵件訊息中顯示的語音訊息文字。

  - **訊息等待指示器**  訊息等待指示器是最舊版的語音信箱系統中找到的功能和指出新郵件存在任何機制可以參照。Exchange 2007，在這項功能是以新的語音訊息的回條光源燈電話機上的第三方應用程式所提供。此功能已新增至Exchange 2010，而且不再需要協力廠商軟體。在使用者的信箱或 UM 信箱原則上完成啟用或停用郵件等待指示器。

  - **未接使用 SMS 電話和語音信箱簡訊通知**  當使用者混合式或 Office 365 部署的一部分，且其行動電話號碼與設定其語音郵件設定及設定來電轉接時、 可以接聽需未接的來電和新的語音訊息儲存格電話上的通知中的文字訊息透過短訊息服務 (SMS)。不過，接收這些類型的通知，使用者必須先設定 \[簡訊，而且也啟用其帳戶的通知。

  - **受保護的語音信箱**  受保護的語音信箱是可讓使用者將私人郵件傳送的整合通訊功能。此郵件受到 Active Directory Rights Management Services (AD RMS) 和使用者無法轉寄、 複製或語音檔案擷取電子郵件。受保護的語音信箱會增加的整合通訊機密性，並讓使用者可以限制語音訊息的對象。這項功能是私人的電子郵件訊息會處理在Exchange 2007不過現在它也適用於到語音郵件訊息的方式類似。

  - **Outlook 語音存取**有兩個整合通訊的使用者介面已啟用 UM 之使用者可︰ 電話的使用者介面 (TUI) 和語音使用者介面 (VUI)。下列兩個介面一起呼叫Outlook語音存取。Outlook 語音存取使用者可以使用Outlook語音存取語音信箱系統存取來自外部或內部的電話時。Um 使用者撥入語音信箱系統可以存取使用Outlook語音存取其信箱。透過電話、 已啟用 UM 的使用者可以：
    
      - 存取語音信箱
    
      - 聆聽、轉寄或回覆電子郵件
    
      - 聆聽行事曆資訊
    
      - 存取或撥號給儲存在組織目錄中的聯絡人，或位於其個人連絡資料中的單一聯絡人或聯絡人群組。
    
      - 接受或取消會議邀請
    
      - 傳送語音訊息，讓來電者知道受話方目前不在
    
      - 設定使用者安全性喜好設定及個人選項

  - **使用 Outlook Voice Access 的群組位址**  在Exchange 2007，使用者可以使用的電話使用者介面 (TUI) 或語音使用者介面 (VUI) Outlook語音存取時登入其信箱傳送電子郵件和語音訊息。不過，使用者只有無法傳送單一電子郵件訊息給單一使用者在其個人連絡人，至多個收件者從目錄新增每個收件者個別，或是從您的組織將目錄新增通訊群組清單的名稱。在Exchange 2013，當使用者登入使用Outlook語音存取其信箱他們也可以傳送電子郵件和語音訊息儲存在其個人連絡人群組的使用者。

回到頁首

## 管理功能

目前，大部分的使用者和 IT 部門管理其語音信箱分開的電子郵件。語音信箱和電子郵件存在於為不同的收件匣存取透過電子郵件的桌面以及透過電話的語音信箱的不同伺服器上主控。整合的通訊提供整合式儲存區的所有郵件及透過電腦和電話內容的存取權。

Exchange系統管理員可以管理整合通訊使用相同介面他們使用管理Exchange、 的其餘部分使用Exchange系統管理中心 (EAC) 和Exchange管理命令介面。他們可以：

  - 從單一平台管理語音信箱和電子郵件

  - 使用可編寫指令碼的命令來管理整合通訊

  - 建立高可用及可靠的整合通訊基礎結構

Exchange 2013 整合通訊功能讓系統管理員：

  - **完整的語音郵件系統。**  整合的通訊提供完整的語音郵件解決方案使用單一存放區、 傳輸及 directory 基礎結構。在信箱伺服器所提供之儲存區和轉寄的來電 VoIP 閘道或 IP PBX 可處理由用戶端存取伺服器。您可以從單一管理點、 使用單一的管理介面和工具組管理所有電子郵件和語音信箱訊息。

  - **Exchange 安全性模式**   信箱伺服器上的 MicrosoftExchange 整合通訊服務與用戶端存取伺服器上的 MicrosoftExchange 整合通訊呼叫路由器服務是以單一 Exchange 伺服器帳戶執行。

  - **語音信箱系統的彙總**  目前，最多的語音郵件系統需要在組織中每一個實際辦公室位置安裝的所有語音訊息元件。在這種排列、 語音訊息的分支辦公室位於外中央 office 而必須在系統管理站。此經常產生增加的管理成本和複雜性。整合的通訊可讓您從集中位置管理您的語音郵件系統。若要建立的集中式的管理系統的整合通訊，您可以利用 Exchange 伺服器的一些資料中心或其他位置，與 Exchange 伺服器的其餘部分內部部署，然後將 VoIP 閘道、 IP Pbx 或工作階段邊界控制器 (Sbc) 中每個您要取代語音訊息系統為每個分公司分公司部署。部署集中式的語音訊息系統本方法可能會造成重大節省硬體與管理成本。

  - **內建整合通訊管理角色**   管理整合通訊與語音信箱功能的 UM 專用管理角色包含以下項目：
    
      - UM 信箱
    
      - UM 提示
    
      - 整合通訊

  - **傳入傳真支援**   Exchange 2013提供使用者已啟用 UM 的信箱建傳入的傳真支援。他們可以接收傳真訊息透過撥打至其分機號碼的電話。
    
    需要的傳真解決方案客戶必須部署傳真協力廠商解決方案。傳真協力廠商解決方案均可在幾傳真協力廠商。傳真協力廠商解決方案的設計被用來與 Exchange 變得更密切整合，並啟用 UM 功能的使用者接收傳入傳真訊息。您可以藉由造訪[Microsoft Pinpoint 傳真協力廠商](https://go.microsoft.com/fwlink/?linkid=190238)找到傳真協力廠商解決方案。

  - **多語系支援**  所有可用的語言套件包含文字轉語音 (TTS) 引擎和指定的語言及 ASR 支援預先錄製的提示。不過，只有某些語言套件包含語音郵件預覽的支援。美國英文 (EN-US) 的語言套件包含安裝媒體上與其他的 UM 語言套件可從[Microsoft 下載中心](https://go.microsoft.com/fwlink/p/?linkid=266542)下載。

  - **自動語音應答**  自動語音應答是一組語音提示的語音郵件系統提供外部和內部使用者存取。使用者可以使用電話鍵盤或語音輸入來瀏覽自動語音應答功能表、 撥打電話給使用者，或尋找在組織中的使用者並再撥打給他們。自動語音應答讓系統管理員能夠：
    
      - 建立適用於外部使用者的自訂功能表。
    
      - 定義資訊性問候語、上班時間問候語及非上班時間問候語。
    
      - 定義假日排程。
    
      - 描述如何搜尋組織的目錄。
    
      - 描述如何連接至使用者的分機，讓外部來電者可以透過指定使用者的分機來打電話給該使用者。
    
      - 描述如何搜尋組織的目錄，讓外部來電者可以搜尋組織的目錄，以及打電話給特定使用者。
    
      - 讓外部使用者打給操作員。

回到頁首

## 規劃與部署 UM

整合的通訊需要與現有的電話系統整合您的 Exchange Server 部署，您的組織。成功部署需要您以讓您現有的電話語音基礎結構的小心分析和執行正確的規劃步驟來部署及管理整合通訊中的語音信箱。

當您規劃整合通訊部署時，您必須考慮設計和其他問題可能會影響您能夠當您部署整合通訊達到組織目標。通常比較簡單的整合通訊拓撲、 更輕鬆地整合通訊是以部署及維護。安裝少的 Client Access server 和 Mailbox server 及建立整合通訊的幾個元件，像是 UM 撥號對應表計劃、 自動語音應答和 UM 信箱原則視需要以支援您的業務與組織目標。與複雜網路和電話語音的環境、 多個業務單位或其他複雜性的大型企業將會需要較複雜的規劃較小型組織具有較簡單的整合通訊需求。

有多個區域，您必須考量及評估能夠順利部署整合通訊。您必須了解整合通訊和每個元件和功能的不同層面，您可以適當地規劃整合通訊基礎架構與部署。配置時間規劃及完成這些問題可協助您部署在組織中的 \[整合通訊時防止發生的問題。下列是您應考慮及評估組織中規劃整合通訊時方面的部分：

  - 組織需求。

  - 組織中的安全性需求。

  - 您的現有電話語音、電路交換網路，以及目前的語音郵件系統。

  - 將目前封包切換 IP 網路設計。這包括您的區域網路 (LAN) 及 WAN 連線點和裝置。

  - 您目前的 Active Directory 環境。

  - 您往後所需支援的使用者數目。

  - 您往後所需的 Client Access Server 與 Mailbox Server 的數目。

  - 未來您是否會將 UM 與 Microsoft Lync Server 整合以啟用 Enterprise Voice。

  - VoIP 閘道、電話語音設備，以及用戶端存取與信箱伺服器的設置。

  - UM 部署的類型： 內部部署或混合式。

  - 語音信箱使用者的儲存需求。

回到頁首

## 使用 EAC 或命令介面來管理 UM

**EAC 管理**

Exchange 2013提供包含所有 UM 元件及功能貴組織的單一整合的管理主控台。Exchange 系統管理中心 (EAC) 提供流暢、 最佳化介面的內部部署、 線上、 管理或混合部署。中Exchange 2013 EAC 取代 Exchange 管理主控台 (EMC) 與 Exchange 控制台 (ECP) 在 \[Exchange 2010。一些 EAC 中功能包括：

  - **清單檢視**  在 EAC 中的 \[清單\] 檢視已經設計 ECP 中移除存在的限制。ECP 已限制為顯示最多 500 個物件及若您想要檢視詳細資料窗格中未列出的物件，您需要使用搜尋和篩選尋找這些特定的物件。在Exchange 2013，從 EAC 的 \[清單\] 檢視內的檢視限制為約 20000 的物件。此外，以便您可以\] 頁面上的結果已新增分頁。您也可以設定頁面大小及匯出至 CSV 檔案。

  - **新增/移除收件者清單檢視中的欄**   您可以選擇要檢視哪些欄，並且可儲存您的自訂清單檢視。

  - **安全 ECP 虛擬目錄**  您可以分割從網際網路和從內部網路內 ECP IIS 虛擬目錄，若要允許或禁止管理功能的存取。使用這項功能，您可以允許或拒絕權限給使用者嘗試從您組織的環境外部網際網路存取 EAC 時仍可讓使用者的 Outlook Web App 選項來存取。

  - **公用資料夾管理**  在 Exchange 2010 和 Exchange 2007 中，公用資料夾是透過公用資料夾系統管理主控台進行管理。公用資料夾現在則位於 EAC 中，不需要另外的工具來管理這些資料夾。

  - **通知**   在 Exchange 2013 中，EAC 現在有通知檢視器，讓您檢視長時間執行程序的狀態，而且您可以選擇在程序完成時透過電子郵件訊息收到通知。

  - **角色型存取控制 (RBAC) 使用者編輯器**  在Exchange 2010您可以使用 RBAC 使用者編輯器中新增使用者至管理角色群組。在Exchange 2013，RBAC 使用者編輯器功能是現在在 EAC 中，而不需要另一項工具來管理 RBAC。

  - **整合通訊的工具**  Exchange 2010中無法使用通話統計資料與使用者通話記錄工具可協助提供已啟用 UM 之使用者的 UM 統計資料和特定的通話的相關資訊。 在Exchange 2013、 通話統計資料和使用者通話記錄工具皆已在 EAC 中，您不需要另一項工具來管理它們。

**命令介面管理**

Exchange管理命令介面內建Windows PowerShell 技術上是功能強大的命令列介面，可讓自動化管理工作。使用命令介面中，您可以管理Exchange的每個層面。您可以啟用新的電子郵件帳戶、 建立傳送和接收連接器、 設定資料庫內容、 管理整合通訊與更多的所有層面。命令介面可以在 EAC 中執行每個任務的可執行的 EAC 中加上無法完成的工作。事實上，當您執行在 EAC 中，它會是執行幕後工時命令介面。

回到頁首

## 整合通訊說明文件

下表包含的主題連結有助於了解並管理 Exchange 整合通訊。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>主題</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="new-voice-mail-features-exchange-2013-help.md">新的語音信箱功能</a></p></td>
<td><p>了解 Microsoft Exchange 2013 中的新功能。</p></td>
</tr>
<tr class="even">
<td><p><a href="planning-for-unified-messaging-exchange-2013-help.md">整合通訊的規劃</a></p></td>
<td><p>了解您需要規劃整合通訊部署的概念與資訊。</p></td>
</tr>
<tr class="odd">
<td><p><a href="deploying-voice-mail-and-um-exchange-2013-help.md">部署語音信箱和 UM</a></p></td>
<td><p>了解涉及部署語音信箱與 UM 的需求與步驟。</p></td>
</tr>
<tr class="even">
<td><p><a href="um-languages-prompts-and-greetings-exchange-2013-help.md">UM 語言、 提示及問候語</a></p></td>
<td><p>了解 UM 語言套件及語言設定。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/zh-tw/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/telephone-system-integration-with-um">UM 電話系統整合</a></p></td>
<td><p>了解如何整合您的電話語音網路與 UM。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/zh-tw/exchange/voice-mail-unified-messaging/connect-voice-mail-system/connect-voice-mail-system">連線至您的電話網路的語音郵件系統</a></p></td>
<td><p>了解如何使用與設定 UM 元件以將電話語音網路連線至 Exchange UM。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/zh-tw/exchange/voice-mail-unified-messaging/automatically-answer-and-route-calls/automatically-answer-and-route-calls">自動接聽和路由傳送來電</a></p></td>
<td><p>了解如何建立 UM 自動語音應答，以及如何管理導覽功能表、問候語，以及上班與非上班時間的設定。</p></td>
</tr>
<tr class="even">
<td><p><a href="set-up-https://docs.microsoft.com/zh-tw/exchange/voice-mail-unified-messaging/set-up-voice-mail/voice-mail-for-users">設定使用者的語音信箱</a></p></td>
<td><p>了解如何建立及管理 UM 信箱原則，以及如何為使用者啟用 UM。</p></td>
</tr>
<tr class="odd">
<td><p><a href="set-up-client-voice-mail-features-exchange-2013-help.md">設定用戶端語音信箱功能</a></p></td>
<td><p>了解如何設定用戶端功能，以讓使用者可以存取及管理其語音信箱訊息。</p></td>
</tr>
<tr class="even">
<td><p><a href="set-outlook-voice-access-pin-security-exchange-2013-help.md">設定 Outlook 語音存取 PIN 安全性</a></p></td>
<td><p>了解如何設定 Outlook 語音存取使用者的 PIN 碼需求。</p></td>
</tr>
<tr class="odd">
<td><p><a href="protect-voice-mail-exchange-2013-help.md">保護語音信箱</a></p></td>
<td><p>了解如何使用 UM 來保護語音訊息。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/zh-tw/exchange/voice-mail-unified-messaging/run-voice-mail-call-reports/run-voice-mail-call-reports">針對語音信箱通話執行的報告</a></p></td>
<td><p>了解 UM 通話報告。</p></td>
</tr>
</tbody>
</table>

