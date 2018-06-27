---
title: '部署 Exchange 2013 UM: Exchange 2013 Help'
TOCTitle: 部署 Exchange 2013 UM
ms:assetid: d147d4b1-32d7-476b-b76f-ee3c0b35ba49
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ673564(v=EXCHG.150)
ms:contentKeyID: 50474314
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 部署 Exchange 2013 UM

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2016-12-09_

整合通訊 (UM) 要求您整合 Exchange Server 部署與您組織的現有電話語音系統。成功的部署需要仔細分析您現有的電話基礎結構，並執行正確的規劃步驟以部署和管理整合通訊中的語音信箱。

**目錄**

Before you deploy

Deploying Unified Messaging

Post-deployment tasks for Unified Messaging

## 部署之前

在您部署整合通訊之前，建議您先熟悉下列主題中的概念：

  - [UM 撥號對應表](um-dial-plans-exchange-2013-help.md)

  - [UM IP 閘道](um-ip-gateways-exchange-2013-help.md)

  - [UM 服務](um-services-exchange-2013-help.md)

  - [UM 群組搜尋](um-hunt-groups-exchange-2013-help.md)

  - [自動接聽和路由傳送來電](automatically-answer-and-route-incoming-calls-exchange-2013-help.md)

  - [UM 信箱原則](um-mailbox-policies-exchange-2013-help.md)

  - [使用者的語音信箱](voice-mail-for-users-exchange-2013-help.md)

## 部署整合通訊

無論您使用 IP Private Branch eXchange (IP PBX)、VoIP 閘道或 Microsoft Lync Server 部署 UM，整合通訊所有的部署選項都有幾個共通的步驟。建立可延展及高可用系統以支援大量整合通訊使用者時需要這些步驟。這些步驟如下：

1.  部署及設定整合通訊的電話語音元件。

2.  確定您已正確安裝執行 Microsoft Exchange 整合通訊呼叫路由器服務的 Client Access Server，以及執行 Microsoft Exchange 整合通訊服務的 Mailbox Server。

3.  建立並設定所需的整合通訊元件。

4.  執行整合通訊的任何部署後工作。

## 部署及設定電話語音元件

若要在 Exchange 組織中成功部署整合通訊，Exchange 系統管理員必須了解資料網路功能概念以及電話語音的術語與概念，而且能夠正確地設定 UM 所需的電話語音元件。執行新部署或升級舊版語音信箱系統時，需要對電話語音網路與整合通訊有深入了解。

一般而言，您必須完成三項工作才能成功設定 UM 所需的電話語音元件：

1.  **提供 PBX 線路**   若要部署可延展的 UM 解決方案，首先必須提供 PBX 線路。

2.  **組織頻道**   在提供 PBX 型語音頻道後，即可將頻道組織成群組搜尋。

3.  **部署 VoIP 閘道**   將語音頻道組織成群組搜尋後，必須讓這些頻道在 IP 閘道器處結束。VoIP 閘道器可與傳統 PBX 搭配使用，將在電話語音網路上的電路交換通訊協定轉換為 IP 封包交換通訊協定。

在部署整合通訊期間，當您在整合組織的電話語音及資料網路時，必須正確設定電話語音及資料網路功能元件。您還必須設定下列元件或介面，才能成功部署整合通訊：

  - **設定組織中與 VoIP 閘道進行通訊的 PBX 連線。**如需詳細資訊，請參閱[Connect a VoIP 閘道與 PBX 通訊](connect-a-voip-gateway-to-communicate-with-a-pbx-exchange-2013-help.md)。

  - **設定 VoIP 閘道介面到 PBX 的連線。**如需如何設定 PBX 介面以便與支援的 VoIP 閘道進行通訊的詳細資訊，請參閱您 PBX 專屬的產品文件，或參閱[Connect a VoIP 閘道與 PBX 通訊](connect-a-voip-gateway-to-communicate-with-a-pbx-exchange-2013-help.md)。

  - **設定 VoIP 閘道介面到 Client Access Server 及 Mailbox Server 的連線。**如需詳細資訊，請參閱[連線至 UM VoIP 閘道、 IP PBX 或工作階段邊界控制器](connect-a-voip-gateway-ip-pbx-or-session-border-controller-to-um-exchange-2013-help.md)。

  - **設定 Client Access Server 及 Mailbox Server 到 VoIP 閘道介面的連線。**如需詳細資訊，請參閱[連線至受支援的 VoIP 閘道的 UM](connect-um-to-a-supported-voip-gateway-exchange-2013-help.md)。

回到頁首

## 安裝 Mailbox Server 和 Client Access Server

不同的部署路徑可供計劃部署 Exchange 整合通訊的組織使用。儘管這些路徑都會通到相同的結果 — 順利部署整合通訊，不過每條路徑會稍有不同，因為每個客戶的需求和起點都不同。但是，通常會有涵蓋所有支援部署案例的通用起點和路徑，包含新安裝和升級。請依照下列步驟部署 Client Access Server 和 Mailbox Server：

1.  確認現有的基礎結構滿足某些必要條件。如需詳細資訊，請參閱[Exchange 2013 必要條件](exchange-2013-prerequisites-exchange-2013-help.md)。

2.  部署新的 Exchange 2013 組織。如需詳細資訊，請參閱[使用安裝精靈安裝 Exchange 2013](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb125224.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您必須先至少在組織中部署一個 Exchange 2013 Mailbox Server，才能將 VoIP 閘道或 IP PBX 設定為將 UM SIP 和 RTP 流量傳送至 Exchange 2013 Client Access Server。</td>
    </tr>
    </tbody>
    </table>


3.  確認已正確安裝用戶端存取和信箱伺服器。在安裝伺服器之後，建議您驗證安裝並檢閱伺服器安裝記錄檔。如需詳細資訊，請參閱[確認 Exchange 2013 安裝](verify-an-exchange-2013-installation-exchange-2013-help.md)。

## 新增所需的 UM 語言套件

UM 語言套件可讓來電者和 Outlook 語音存取使用者，以多種語言與語音郵件系統互動。您在 Mailbox Server 上安裝其他語言套件之後，來電者及 Outlook 語音存取使用者就能夠以這個語言聽到電子郵件並與語音郵件系統互動。

當您第一次安裝 Exchange 時，美式英文會是預設語言，並且是唯一可用於撥號對應表的語言選項。在 Mailbox server 上安裝 UM 語言套件之後，當設定撥號對應表的預設語言時，與語言套件關聯的語言將列示為可用選項。根據預設，因為 UM 自動語音應答會在建立時與 UM 自動語音應答產生關聯，所以 UM 自動語音應答會使用關聯之 UM 撥號對應表的預設語言設定。不過，在建立 UM 自動語音應答之後，可以變更此設定。

您可以使用 Setup.exe 命令或您已從[Exchange Server 2013 UM 語言套件](https://go.microsoft.com/fwlink/p/?linkid=266542)下載 UM 語言套件之後執行*\<UMLanguagePack\>*.exe 安裝程式來新增 UM 語言套件。不過，您必須使用 Setup.exe 命令移除 UM 語言套件。沒有任何Exchange管理命令介面指令程式可用來新增或移除信箱伺服器的語言。如需如何安裝 UM 語言套件的詳細資訊，請參閱[安裝 UM 語言套件](install-a-um-language-pack-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>根據預設，安裝信箱伺服器時，會安裝美式英文語言 (EN-US)。必須自電腦移除 Mailbox server 才能將它移除。</td>
</tr>
</tbody>
</table>


回到頁首

## 建立和設定 UM 元件

整合通訊的部署與運作需要數項 UM 元件。整合通訊元件會連接電話語音基礎結構與整合通訊環境。成功安裝用戶端存取和信箱伺服器後，請進行下列步驟。

## 步驟 1：建立和設定 UM 撥號對應表

UM 撥號對應表對於整合通訊操作極為重要，有它才能在網路上成功部署整合通訊。在您成功安裝用戶端存取和信箱伺服器之後，UM 撥號對應表將是您建立的第一個元件。

根據預設，UM 撥號對應表以及與該撥號對應表關聯的信箱伺服器不會使用加密來收發資料。在「不安全」模式下，不會將 VoIP 及 SIP 流量加密。在您建立撥號對應表當時或之後，請使用相互傳輸層安全性 (Mutual TLS) 來設定撥號對應表，以加密 VoIP 和 SIP 流量。如果您要使用 Mutual TLS，您必須將撥號對應表設為 \[SIP 安全\] 或 \[安全\]、將 UM 啟動模式設為 \[TLS\] 或 \[雙重\]，然後建立信任的憑證並配送給 Exchange 伺服器與 VoIP 閘道、IP PBX 或工作階段邊界控制器 (SBC)。在您設定 VoIP 安全性設定之後，必須設定用戶端存取和信箱伺服器的啟動模式。如需詳細資訊，請參閱[設定信箱伺服器上的啟動模式](configure-the-startup-mode-on-a-mailbox-server-exchange-2013-help.md)或[設定用戶端存取伺服器上的啟動模式](configure-the-startup-mode-on-a-client-access-server-exchange-2013-help.md)。

執行下列程序，以建立新的 UM 撥號對應表。

## 建立 UM 撥號對應表

1.  在 Exchange 系統管理中心 (EAC) 中，瀏覽至 **\[整合通訊\]** \> **\[UM 撥號對應表\]**，然後按一下 **\[新增\]**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

2.  在 **\[新增 UM 撥號對應表\]** 頁面上，填妥下列方塊：
    
      - **名稱** 輸入撥號對應表的名稱。UM 撥號對應表名稱是必要項目，而且必須是唯一的名稱。您輸入的名稱只能在 EAC 和命令介面中作為顯示用途。UM 撥號對應表的長度上限為 64 個字元，可包含空格。不過不可包含下列任何一個字元：" / \\ \[ \] : ; | = , + \* ? \< \>.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>雖然撥號對應表名稱方塊可接受 64 個字元，但撥號對應表名稱不可超過 49 個字元。這是因為當您建立撥號對應表時，還會建立名稱為「<em>&lt;DialPlanName&gt;</em> 預設原則」的預設 UM 信箱原則。UM 撥號對應表與 UM 信箱原則的 <em>name</em> 參數長度可為 64 個字元。</td>
        </tr>
        </tbody>
        </table>
    
      - \[分機號碼長度 (數字位數)\]   輸入 UM 撥號對應表中的分機號碼位數。分機號碼位數是以在 PBX 上建立的電話語音撥號對應表為依據。例如，若與電話語音撥號對應表關聯的使用者，要撥打 4 位數的分機來呼叫同一電話語音撥號對應表中的另一位使用者，則選取 4 來作為分機號碼位數。
        
        這是必要方塊，值的範圍為 1 到 20。一般分機號碼的長度為 3 到 7 碼。如果您現有的電話語音環境包含分機號碼，則必須指定與那些分機號碼位數相符的位數。
        
        建立電話分機撥號對應表時，您需要輸入使用者連結到電話分機撥號對應表時所對應的分機號碼。已啟用 UM 的使用者連結到 SIP URI 或 E.164 撥號對應表時，需要工作階段初始通訊協定 (SIP) 撥號對應表或 E.164 撥號對應表的分機號碼。Outlook 語音存取使用者存取自己的 Exchange 信箱時，就會使用此分機號碼。
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(UI\_URI 類型)
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(UI\_VoIP 安全性)
    
      - \[國家/地區碼\]   使用此方塊可輸入用於撥出電話的國家/地區碼。此號碼會自動加在要撥打的電話號碼前面。此方塊接受 1 到 4 位數字。例如，美國的國家/地區碼為 1；英國為 44。

3.  按一下 \[儲存\]。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>在舊版的 Exchange 中，必須將整合通訊伺服器新增到 UM 撥號對應表中。在 Exchange 2013 中，用戶端存取及信箱伺服器無法與電話分機或 E.164 撥號對應表產生關聯。用戶端存取及信箱伺服器將接聽全部類型的撥號對應表所有的來電。不過，如果將 UM 與 Microsoft Lync Server 相互整合，必須將所有的用戶端存取及信箱伺服器新增到所有的 SIP URI 撥號對應表，才能使 Lync Server 正確處理電話轉接。</td>
    </tr>
    </tbody>
    </table>


回到頁首

## 步驟 2：建立並設定 UM IP 閘道器

UM IP 閘道器代表 VoIP 閘道器硬體裝置或 IP PBX。結合 UM IP 閘道器與 UM 群組搜尋，可在 VoIP 閘道或 IP PBX 與 UM 撥號對應表之間建立連結。

若您已在撥號對應表上建立或啟用 VoIP 安全性，則您使用下列其中一個程序建立的 UM IP 閘道器，將會與使用 VoIP 安全性的 UM 撥號對應表相關聯。在此情况下，必須使用網域全名 (FQDN) 來建立 UM IP 閘道器，而不能使用 IP 地址。您還必須將 UM IP 閘道器設定為在 TCP 通訊埠 5061 上接聽。若要設定 UM IP 閘道器在 TCP 通訊埠 5061 上接聽，請執行下列命令：`Set-UMIPGateway -identity MyUMIPGateway -Port 5061`。您也必須確認任何 VoIP 閘道器或 IP PBX 都已設定為在通訊埠 5061 上接聽 Mutual TLS。

執行下列程序，以建立新的 UM IP 閘道器。

## 建立 UM IP 閘道器

1.  
    
    在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM IP閘道\]，然後按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

2.  在 \[新增 UM IP 閘道器\] 頁面上，輸入下列資訊：
    
      - \[名稱\]   使用此方塊可指定 UM IP 閘道器的唯一名稱。這是出現在 EAC 中的顯示名稱。如果建立 UM IP 閘道器後必須變更它的顯示名稱，您必須先刪除現有的 UM IP 閘道器，然後建立另一個具有適當名稱的 UM IP 閘道器。UM IP 閘道器名稱是必要的，不過僅供顯示之用。由於您的組織可能使用多個 UM IP 閘道器，建議您為 UM IP 閘道器使用有意義的名稱。UM IP 閘道器名稱的長度上限是 64 個字元，且可以包含空格。不過不可包含下列任何一個字元：" / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - \[地址\]   您可以使用 IP 位址或完整網域名稱 (FQDN) 設定 UM IP 閘道器。使用此方塊指定設定於 VoIP 閘道、SIP-enabled PBX、IP PBX 或 SBC 上的 IP 位址或 FQDN。此方塊僅接受有效且格式正確的 FQDN。
        
        您可以在此方塊中輸入字母和數字字元。支援 IPv4 位址、IPv6 位址和 FQDN。如果您要在 UM IP 閘道器和撥號對應表 (於 \[SIP 安全\] 或 \[安全\] 模式中操作) 之間使用相互 TLS，則必須使用 FQDN 設定 UM IP 閘道器。此外還必須將它設定為在通訊埠 5061 上接聽，並且確認任何 VoIP 閘道或 IP PBX 都已設定為針對相互 TLS 要求在通訊埠 5061 上接聽。若要設定 UM IP 閘道器，請執行以下命令：`Set-UMIPGateway -identity MyUMIPGateway -Port 5061`.
        
        如果您使用 FQDN，也必須確定已正確設定 VoIP 閘道的 DNS 主機記錄，這樣主機名稱才能正確解析成 IP 位址。另外，如果您使用 FQDN 而非 IP 位址，並變更 UM IP 閘道器的 DNS 組態，則必須停用然後啟用 UM IP 閘道器，以確保正確更新 UM IP 閘道器的組態資訊
    
      - \[UM 撥號對應表\]   按一下 \[瀏覽\] 可選取您想要與 UM IP 閘道器關聯的 UM 撥號對應表。當選取要與 UM IP 閘道器建立關聯的 UM 撥號對應表時，同時也會建立預設的 UM 群組搜尋，並將其與您所選取的 UM 撥號對應表建立關聯。若您並未選取 UM 撥號對應表，那麼必須以手動方式建立 UM 群組搜尋，然後將該 UM 群組搜尋與您建立的 UM IP 閘道器建立關聯。

3.  
    
    按一下 **\[儲存\]**。

## 步驟 3：建立並設定 UM 群組搜尋 (選用)

「群組搜尋」一詞用來描述使用者共用的一組 PBX 或 IP PBX 資源或分機號碼。群組搜尋是用來有效地將來電分送至特定商業單位或從中分送出去。

如果您已經建立 UM IP 閘道器，並使 UM IP 閘道器與 UM 撥號對應表產生關聯，則已經建立預設 UM 群組搜尋。視您已建立的 UM IP 閘道器數目而定，您可讓其他 UM 群組搜尋與相同或不同的 UM IP 閘道器產生關聯。

在您建立 UM 群組搜尋時，會讓 UM 撥號對應表內指定的所有信箱伺服器能夠與 VoIP 閘道器進行通訊。如需詳細資訊，請參閱[UM 群組搜尋](um-hunt-groups-exchange-2013-help.md)。

## 建立 UM 群組搜尋

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。在清單檢視中，選取您要變更的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 **\[UM 撥號對應表\]** 頁面的 **\[UM 群組搜尋\]** 下方，按一下 **\[新增\]**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

3.  在 \[新增 UM 群組搜尋\] 頁面上，填妥下列方塊：
    
      - \[關聯的 UM IP 閘道器\]   此僅供顯示方塊會顯示將與 UM 群組搜尋產生關聯的 UM IP 閘道器所用的名稱。
    
      - \[名稱\]   使用此方塊可建立 UM 群組搜尋的顯示名稱。UM 群組搜尋名稱是必要項目，而且必須是唯一的，但是，它只能在 EAC 和命令介面中作為顯示用途。如果您在建立群組搜尋之後，必須變更其顯示名稱，則必須先刪除現有的群組搜尋，然後再建立另一個具有適當名稱的群組搜尋。
        
        如果您的組織使用多個群組搜尋，建議為您的群組搜尋使用有意義的名稱。UM 群組搜尋名稱的長度上限是 64 個字元，且可以包含空格。不過不可包含下列任何一個字元：" / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - \[撥號對應表\]   按一下 \[瀏覽\]，選取將與 UM 群組搜尋產生關聯的撥號對應表。您必須使群組搜尋與撥號對應表產生關聯。一個 UM 群組搜尋只能與一個 UM IP 閘道器和一個 UM 撥號對應表關聯。
    
      - \[引導識別碼\]   使用此方塊可指定一個字串，唯一識別 PBX 或 IP PBX 上設定的引導識別碼或引導 ID。
        
        您可以在此方塊中使用分機號碼，或使用工作階段初始通訊協定 (SIP) 統一資源識別碼 (URI)。此方塊可接受英數字元。若為傳統 PBX，則會使用數值來作為引導識別碼。不過，有些 IP PBX 可以使用 SIP URI。

4.  按一下 \[儲存\]。

回到頁首

## 步驟 4：建立並設定 UM 信箱原則

當您開啟使用者使用整合通訊時，必須使用 UM 信箱原則。每個已啟用 UM 之使用者的信箱都必須連結到單一 UM 信箱原則。建立 UM 信箱原則後，就可以將一或多個啟用 UM 的信箱連結到 UM 信箱原則。這樣可讓您控制 PIN 碼安全性設定，如 PIN 碼最小位數，或是與 UM 信箱原則關聯的已啟用 UM 之使用者的登入嘗試失敗次數上限。

每次建立 UM 撥號對應表時，也會同時建立 UM 信箱原則。此 UM 信箱原則的名稱將為 \<*DialPlanName*\> 預設原則。但是，如果您必須建立新的 UM 信箱原則，請執行下列程序。

## 建立 UM 信箱原則

1.  
    
    在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。在清單檢視中，選取您要修改的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 **\[UM 撥號對應表\]** 頁面的 **\[UM 信箱原則\]** 底下，按一下 **\[新增\]**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

3.  在 \[新增 UM 信箱原則\] 頁面的 \[名稱\] 文字方塊中，輸入新 UM 信箱原則的名稱。
    
    使用這個方塊來指定 UM 信箱原則的唯一名稱。這是出現在 EAC 中的顯示名稱。如果您在建立 UM 信箱原則後必須變更其顯示名稱，則必須先刪除現有的 UM 信箱原則，然後建立另一個具有適當名稱的 UM 信箱原則。如果有任何啟用 UM 的使用者與 UM 信箱原則相關聯，則您無法刪除該原則。
    
    UM 信箱原則名稱是必要的，但只用於顯示。由於您的組織可能使用多個 UM 信箱原則，我們建議您針對 UM 信箱原則使用有意義的名稱。UM 信箱原則名稱的長度上限是 64 個字元，且可以包含空格。不過不可包含下列任一字元：" / \\ \[ \] : ; | = , + \* ? \< \>.

4.  按一下 \[儲存\] 儲存新的 UM 信箱原則。儲存 UM 信箱原則時，將啟用所有預設設定，包括 PIN 原則、語音信箱功能，以及受保護的語音信箱設定。如果要自訂或變更任何預設設定，請使用 **Set-UMMailbox** 指令程式，針對您剛才建立的 UM 信箱原則變更設定。

## 步驟 5：建立和設定 UM 自動語音應答 (選用)

整合通訊可以讓您根據組織的需求，建立一或多個 UM 自動語音應答。當您建立 UM 自動語音應答時，會建立組織的語音功能表系統。讓組織外部或內部來電者得以瀏覽功能表系統，以便尋找及撥打 (或轉接) 電話給組織內的使用者或部門。

來電者可使用雙音多頻 (DTMF) 輸入 (亦稱為按鍵) 或語音輸入來瀏覽功能表系統。若要使自動語音辨識 (ASR) 正確運作，以讓使用者能夠使用語音輸入，您必須啟用 UM 自動語音應答的語音功能。

建立和使用自動語音應答在整合通訊中是選用的。但是，如果您要建立新的 UM 自動語音應答，請執行下列程序。

## 建立 UM 自動語音應答

1.  
    
    在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]，選擇要新增自動應答的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 \[UM 撥號對應表\] 頁面的 \[UM 自動應答\]下方，按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

3.  在 **\[新增 UM 自動語音應答\]** 頁面上，填妥下列方塊：
    
      - **名稱**   使用此方塊可建立 UM 自動語音應答的顯示名稱。UM 自動語音應答名稱是必要項目，而且必須是唯一的。但是，它只能在 EAC 和命令介面中作為顯示用途。
        
        如果您在建立自動語音應答後必須變更其顯示名稱，必須先刪除現有的 UM 自動語音應答，然後建立另一個具有適當名稱的自動語音應答。如果您的組織使用多個自動語音應答，則建議為 UM 自動語音應答使用有意義的名稱。UM 自動語音應答名稱的最大長度為 64 個字元，可以包含空格。
        
        雖然您命名新的 UM 自動語音應答時可包含空白，若是您將整合通訊與 Office Communications Server 2007 R2 或 Microsoft Lync Server 進行整合，則自動語音應答的名稱不可包含空白。因此，若是您所建立的自動語音應答在顯示名稱內包含空白，且您正在與 Office Communications Server 2007 R2 或 Lync Server 2010 進行整合，您首先必須刪除該自動語音應答，接著再建立另一個其顯示名稱中不包含空白的自動語音應答。
    
      - \[建立此自動語音應答為已啟用\]   完成建立 UM 自動語音應答時，選取此核取方塊可讓自動語音應答接聽來電。預設會將新的自動語音應答建立為已停用。
        
        如果您決定將 UM 自動語音應答建立為已停用，在您完成建立自動語音應答後可使用 EAC 或命令介面來啟用自動語音應答。
    
      - \[設定自動應答以回應語音指令\]   選擇此核取方塊以啟用自動語音應答的語音功能。若啟用自動語音應答的語音功能，來電者可使用撥號音或語音輸入，來回應 UM 自動語音應答所使用的系統或自訂提示。依預設，在建立自動語音應答時不會啟用語音。
        
        若要讓來電者使用美式英文 (en-US) 以外語言啟用語音的自動語音應答，您必須安裝適當 UM 語言套件，並設定自動語音應答的內容以使用此語言。安裝信箱伺服器時，預設安裝 en-US UM 語言套件。
    
      - \[存取號碼\]   使用此方塊，可輸入來電者將用於聽取自動語音應答的分機號碼或電話號碼。在方塊中輸入分機號碼或電話號碼，然後按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示") 將該號碼新增到清單。您提供的分機號碼或電話號碼的位數，不必符合相關聯之 UM 撥號對應表中所設定的分機號碼位數。這是因為允許 UM 自動語音應答接受直接來電。
        
        可輸入的分機號碼或引導識別碼的數目沒有限制。然而，您可以建立新的自動語音應答，而不必列出分機號碼或電話號碼。分機號碼或電話號碼不是必要的。
        
        您可以編輯或移除現有的分機號碼或引導識別碼。若要編輯現有的分機號碼或電話號碼，請按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。若要從清單中移除現有的分機號碼或電話號碼，請按一下 \[移除\]![\[移除\] 圖示](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[移除] 圖示")。

4.  按一下 \[儲存\]。

回到頁首

## 整合通訊的部署後工作

完成 Client Access Server 及 Mailbox Server 的全新安裝，並且成功部署整合通訊之後，應該完成部署後的工作。部署後工作將協助您啟用使用者的整合通訊功能、保護您的 UM 部署，並為已啟用 UM 的使用者部署傳入傳真。

## 啟用使用者的語音信箱

在您已部署 VoIP 閘道或 IP PBX、安裝 Client Access Server 及 Mailbox Server，並建立整合通訊所需的元件後，必須為使用者啟用整合通訊。如需詳細資訊，請參閱[啟用使用者的語音信箱](enable-a-user-for-voice-mail-exchange-2013-help.md)。

## 保護語音信箱

整合通訊 (UM) 可以設定為使用 Active Directory Rights Management Service (AD RMS) 來保護組織的語音訊息。此功能稱為「受保護的語音信箱」。當語音訊息受到保護時，收件者不僅無法轉寄訊息，UM 也會確保只有訊息的一或多個預定收件者才能存取訊息的內容。使用 Microsoft Outlook 2010 (或更新版本)、Outlook Web App 或 Outlook Voice Access 可以存取受保護的語音訊息。如需詳細資訊，請參閱[保護語音信箱](protect-voice-mail-exchange-2013-help.md)。

## UM 的 Mutual TLS

若要使用 Mutual TLS 來加密由用戶端存取及信箱伺服器所傳送和接收的 SIP 和即時傳輸通訊協定 (RTP) 流量，請執行下列工作：

  - 執行 Exchange 憑證精靈。如需詳細資訊，請參閱[部署 UM 憑證](deploying-certificates-for-um-exchange-2013-help.md)。

  - 在 Client Access Server 與 Mailbox Server 上匯入憑證。

  - 在組織中的 VoIP 閘道器、IP PBX 以及用戶端存取和信箱伺服器上匯入必要的憑證。

  - 在 UM 撥號對應表上設定 VoIP 安全性。如需詳細資訊，請參閱[設定 VoIP 安全性設定](configure-the-voip-security-setting-exchange-2013-help.md)。

  - 設定用戶端存取及信箱伺服器的啟動模式。如需詳細資訊，請參閱 [設定信箱伺服器上的啟動模式](configure-the-startup-mode-on-a-mailbox-server-exchange-2013-help.md)與 [設定用戶端存取伺服器上的啟動模式](configure-the-startup-mode-on-a-client-access-server-exchange-2013-help.md)。

  - 將 UM IP 閘道器設定為在通訊埠 5061 上接聽。如需詳細資訊，請參閱[設定 \[聆聽連接埠](configure-the-listening-port-exchange-2013-help.md)。

## 已啟用 UM 的使用者相關的 PIN 碼原則

在整合通訊中，PIN 碼原則是定義及設定於 UM 信箱原則中。當您為使用者啟用整合通訊時，可以使該使用者與現有的 UM 信箱原則關聯。在 UM 信箱原則中設定的 UM PIN 碼原則應該以組織的安全需求為基礎。如需如何為已啟用 UM 的使用者設定 PIN 碼設定的詳細資訊，請參閱[設定 Outlook 語音存取 PIN 安全性](set-outlook-voice-access-pin-security-exchange-2013-help.md)。

## 設定用戶端語音信箱功能

在部署伺服器與必要的 UM 元件後，您可以設定幾項選用的語音信箱相關功能。如需相關資訊，請參閱下列各主題：

  - [設定 Outlook 語音存取](setting-up-outlook-voice-access-exchange-2013-help.md)

  - [允許語音郵件使用者可將來電轉接](allow-voice-mail-users-to-forward-calls-exchange-2013-help.md)

  - [允許使用者查看將語音郵件文字記錄](allow-users-to-see-a-voice-mail-transcript-exchange-2013-help.md)

  - [啟用語音信箱使用者接收傳真](enable-voice-mail-users-to-receive-faxes-exchange-2013-help.md)

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>整合您的整合通訊環境和 Microsoft Lync Server 時，還有一些額外的規劃考量。如需詳細資訊，請參閱<a href="deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md">部署 Exchange 2013 UM 和 Lync Server 概觀 （英文）</a>。</td>
</tr>
</tbody>
</table>


回到頁首

