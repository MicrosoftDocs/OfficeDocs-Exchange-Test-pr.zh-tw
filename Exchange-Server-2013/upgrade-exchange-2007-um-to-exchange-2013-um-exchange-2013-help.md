﻿---
title: 'Exchange 2007 UM 升級至 Exchange 2013 UM: Exchange 2013 Help'
TOCTitle: Exchange 2007 UM 升級至 Exchange 2013 UM
ms:assetid: 642c922d-7e85-40f0-bb9b-0f20da692be3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn169227(v=EXCHG.150)
ms:contentKeyID: 54652589
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2007 UM 升級至 Exchange 2013 UM

 

_**適用版本：** Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：** 2016-12-09_

如果您將 Microsoft Exchange 2007 組織與整合通訊 (UM) 升級至 Exchange 2013 Unified Messaging，還有所需的步驟及其他已已經完成 Exchange 2007 UM 部署的一部分的步驟。依據您的電話語音環境和 UM 元件已建立並設定為支援 Exchange 2007 中的 \[整合通訊，您可能需要部署額外的電話語音設備中包括 Voice over IP (VoIP) 閘道、 IP 專用交換機 (Pbx) 或傳統或已啟用 SIP 的 Pbx 然後建立並設定需要 Exchange 2013 UM 的任何其他 UM 元件。

## 開始之前有哪些須知？

  - 完成此工作的預估時間：45-90 分鐘。

  - 確認您在 Exchange 2007 及 Exchange 2013 組織中有適當的權限可建立及設定所有必要元件。

  - 確認您已部署並正確地設定電話語音元件，包括 VoIP 閘道及 PBX、IP PBX 或已啟用工作階段初始通訊協定 (SIP) 的 PBX。

  - 確認您已正確地安裝並設定執行 Microsoft Exchange 整合通訊呼叫路由器 (UM 呼叫路由器) 服務的 Client Access Server，以及執行 Microsoft Exchange 整合通訊 (UM) 服務的 Mailbox Server。若要深入了解 UM 服務，請參閱 [UM 服務](um-services-exchange-2013-help.md)。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。


> [!TIP]  
> 有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.




## 該怎麼做？

## 步驟 1：下載及安裝必要的 UM 語言套件

UM 語言套件可讓來電者和 Outlook 語音存取使用者，以多種語言與語音郵件系統互動。您在 Exchange 2013 Mailbox Server 上額外安裝某個語言之後，來電者及 Outlook 語音存取使用者就能夠以該語言聽取電子郵件內容並與語音信箱系統互動。不過，若要使所有來電都可以使用該語言，您必須在所有 Exchange 2013 Mailbox Server 上安裝必要的 UM 語言套件。這是因為每一部 Exchange 2013 Mailbox Server 都可以接聽整合通訊的來電。

根據預設，安裝 Exchange 2013 Mailbox Server 時，會安裝美式英文 (EN-US) 語言套件。此為撥號對應表唯一可用的語言選項，除非您安裝其他 UM 語言套件(美式英文無法移除，除非您從電腦移除 Mailbox Server)。在 Exchange 2013 Mailbox Server 上安裝 UM 語言套件之後，當設定撥號對應表的預設語言時，與語言套件關聯的語言將列示為可用選項。根據預設，因為 UM 自動語音應答會在建立時連結至 UM 撥號對應表，所以它會使用所連結 UM 撥號對應表的預設語言設定。不過，在建立 UM 自動語音應答之後，可以變更此設定。


> [!NOTE]  
> 若您只要使用美式英文作為撥號對應表的語言，則可跳過此步驟並移至步驟 2。




您可以使用 setup.exe 命令或您已從[Exchange Server 2013 UM 語言套件](https://go.microsoft.com/fwlink/p/?linkid=266542)下載 UM 語言套件之後執行*\<UMLanguagePack\>*.exe 安裝程式來新增的 UM 語言套件。如需詳細資訊，請參閱[安裝 UM 語言套件](install-a-um-language-pack-exchange-2013-help.md)。

此範例使用 setup.exe 來安裝日文 (ja-JP) UM 語言套件。

    setup.exe /AddUmLanguagePack:ja-JP /s:d:\Exchange\UMLanguagePacks /IAcceptExchangeServerLicenseTerms

## 步驟 2： 將 Exchange 2007 的自訂問候語、 宣告、 功能表及提示移至 Exchange 2013 系統信箱

整合通訊撥號對應表及自動語音應答所使用的自訂問候語、 宣告、 功能表及提示。當您安裝 Exchange 2007 或 Exchange 2013 和用以支援的功能，例如郵件核准和多信箱搜尋會建立名為 {e0dc1c29-89c3-4034-b678-e6c29d823ed9} 的系統信箱。此系統信箱也用來儲存撥號對應表計劃和自動語音應答的自訂問候語、 宣告、 功能表及提示。如果系統信箱不存在，您可以使用**Setup /PrepareAD**命令來建立它。

根據預設，在 Exchange 系統管理中心 (EAC) 看不到系統信箱。您可以執行下列其中一個命令，來取得系統信箱清單：

此命令會傳回所有系統信箱的清單。

    Get-Mailbox -Arbitration

此命令會傳回系統信箱的清單，以及其個別內容或設定。

    Get-Mailbox -Arbitration |fl

當您正在匯入的自訂問候語、 宣告、 功能表及提示從 Exchange 2007 到 Exchange 2013 時，您必須使用 MigrateUMCustomPrompts.ps1 指令碼。您無法使用 EAC 匯入的自訂問候語、 宣告、 功能表及提示。MigrateUMCustomPrompts.ps1 指令碼會將一份所有的 Exchange Server 2007 UM 自訂問候語、 宣告、 功能表及提示移轉至 Exchange 2013 UM。根據預設，MigrateUMCustomPrompts.ps1 指令碼位於 Exchange 2013 Mailbox server 上的*\<Program Files\>*\\Microsoft\\Exchange Server\\V15\\Scripts 資料夾而必須執行從 Exchange 2013 Mailbox server。執行指令碼：

1.  按一下 \[開始\] \> \[所有程式\] \> \[Microsoft Exchange Server 2013\] \> \[Exchange 管理命令介面\]。

2.  在 Exchange 管理命令介面，在提示處輸入指令碼的路徑。例如，輸入**cd"D:\\Program Files\\Microsoft\\Exchange Server\\V15\\Scripts"**，並按 Enter。

3.  在命令介面的提示字元下，輸入 **".\\MigrateUMCustomPrompts"**，然後按下 Enter。


> [!NOTE]  
> 使用<strong>Import-UMPrompt</strong>指令程式也匯個別自訂提示。Exchange 2007 UM <strong>Copy-UMCustomPrompt</strong>指令程式不支援將自訂提示複製到 Exchange 2013 UM。




當您執行 MigrateUMCustomPrompts.ps1 指令碼從 Exchange 2013 伺服器時，指令碼所執行的 GUID 或物件的識別碼查閱的撥號對應表或自動語音應答在 Active Directory 與查詢以判斷是否有任何的自訂問候語、 宣告、 功能表或提示。如果找到的自訂問候語、 宣告、 功能表及提示將會匯入名為 {e0dc1c29-89c3-4034-b678-e6c29d823ed9} 的系統信箱。

藉由使用此系統信箱，即可連同資料庫中的其他信箱一起備份及還原自訂問候語、宣告、功能表及提示。這減少了所需的資源數量。將自訂問候語、宣告、功能表及提示儲存在系統信箱中，就可避免任何可能發生的不一致情況。若要深入了解信箱移動，請參閱 [在 Exchange 2013 移動信箱](mailbox-moves-in-exchange-2013-exchange-2013-help.md)。

## 步驟 3： 匯出和匯入憑證

如果您使用 SIP 安全或 Exchange 2007 組織中的 「 安全 」 撥號，您需要匯出及匯入 Exchange 2013 用戶端存取和信箱伺服器所使用的憑證。相互傳輸層安全性 (相互 TLS) 用來加密您的 Exchange 2013 伺服器與 VoIP 閘道、 IP Pbx 之間傳送的資料並已啟用 SIP 的 Pbx。 憑證繫結兩個電子鍵 （公用及私人） 的憑證擁有者用來加密及數位簽署資訊的身分識別。您可以使用其中一個下列憑證 UM 及 UM 呼叫路由器服務：

  - 自我簽署 (Exchange) 憑證

  - 內部公開金鑰基礎結構 (PKI) 憑證

  - 協力廠商商業性憑證

根據預設，在安裝 Exchange 2013 時，會建立兩個自我簽署憑證：** Microsoft Exchange Server Auth Certificate** 及 **Microsoft Exchange**。**Microsoft Exchange** 自我簽署憑證可供 UM 用來加密資料，但是您必須將憑證指派給 UM 及 UM 呼叫路由器服務。此自我簽署憑證可以經複製後，在 VoIP 閘道、IP PBX 及已啟用 SIP 的 PBX 上匯入。不過，在整合 UM 與 Microsoft Lync Server 時則無法使用。

若要讓 UM 可以加密在 Exchange 2013 伺服器與 VoIP 閘道、IP PBX 及已啟用 SIP 的 PBX 之間傳送的資料，您需要執行下列動作：

  - 使用現有的自我簽署 UM 憑證、建立新的自我簽署 Exchange 憑證、提交憑證要求給內部憑證授權單位以取得 PKI 憑證，或購買協力廠商商業性憑證，以用於 Exchange 2013 Mailbox Server 及 Client Access Server 與 VoIP 閘道、IP PBX 及已啟用 SIP 的 PBX 之間的相互 TLS。
    
    使用 EAC 建立 Exchange 自我簽署憑證，如下所示：
    
    1.  在 EAC 中，瀏覽至 **\[伺服器\]** \> **\[憑證\]**，然後按一下 **\[新增\]**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。
    
    2.  在 **\[新增 Exchange 憑證\]** 頁面，選擇 **\[建立自我簽署憑證\]**，然後選取 **\[下一步\]**。
    
    3.  輸入好記的憑證名稱，然後選取 **\[下一步\]**。
    
    4.  按一下 **\[新增\]**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")，選取要套用此憑證的 Exchange 伺服器，然後選取 **\[下一步\]**。
    
    5.  指定要包含在憑證中的網域，然後選取 **\[下一步\]**。如果要新增服務的網域，請按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。
    
    6.  確認您包含的網域正確，然後選取 **\[完成\]**。
    
    > [!IMPORTANT]  
    > 使用 EAC 建立憑證時，不會收到要您啟用憑證服務的提示。憑證建立好後，即可使用 EAC 來啟用服務。如需如何啟用憑證服務的詳細資訊，請參閱<a href="assign-a-certificate-to-the-um-and-um-call-router-services-exchange-2013-help.md">將憑證指派給 UM 及 UM 呼叫路由器服務</a>。
    
    在命令介面中執行下列命令，來建立 Exchange 自我簽署憑證。
    
        New-ExchangeCertificate -Services 'UM, UMCallRouter' -DomainName '*.northwindtraders.com' -FriendlyName 'UMSelfSigned' -SubjectName 'C=US,S=WA,L=Redmond,O=Northwindtraders,OU=Servers,CN= Northwindtraders.com' -PrivateKeyExportable $true
    
    > [!TIP]  
	> 如果您使用 <em>Services</em> 參數指定要啟用的服務，將會收到要您啟用所建立憑證之服務的提示。在此範例中，您會收到要您啟用憑證的整合通訊及整合通訊呼叫路由器服務的提示。如需如何啟用憑證服務的詳細資訊，請參閱<a href="assign-a-certificate-to-the-um-and-um-call-router-services-exchange-2013-help.md">將憑證指派給 UM 及 UM 呼叫路由器服務</a>。


  - 匯入將用於您組織中的所有 Exchange 2013 用戶端存取和信箱伺服器的憑證。如果您使用 Exchange 2013 的自我簽署的憑證，您需要將複製的憑證\]，然後 VoIP 閘道、 IP Pbx 或已啟用 SIP 的 Pbx 上匯入。如果您使用自我簽署的憑證從 Exchange 2007、 主體替代名稱 (SAN) 必須包含所有 Exchange 2013 伺服器的電腦名稱。如果您在組織中有 Exchange 2007 Unified Messaging 伺服器，您可以使用 Exchange 2013 自我簽署的憑證，但您必須將 Exchange 2007 UM 伺服器的電腦名稱新增至 Exchange 2013 憑證的 SAN。

  - 在您組織的 Client Access Server 及 Mailbox Server 上，啟用要使用的憑證或將它指派給 UM 及 UM 呼叫路由器服務。
    
    使用 EAC，讓所有 Exchange 2013 伺服器上的 UM 服務及 UM 呼叫路由器服務使用 Exchange 自我簽署憑證，如下所示：
    
    1.  在 EAC 中，瀏覽至 **\[伺服器\]** \> **\[憑證\]**，選取要在其上啟用服務的憑證，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。
    
    2.  在 **\[程序\]** 頁面上，依序選取 **\[服務\]**、**\[整合通訊\]** 和 **\[整合通訊呼叫路由器\]**。
    
    在命令介面中執行下列命令，來啟用 Exchange 自我簽署憑證。
    
        Enable-ExchangeCertificate -Thumbprint 5113ae0233a72fccb75b1d0198628675333d010e -Services 'UM, UMCallRouter'

  - 將任何新的或現有的 UM 撥號對應表設定為「SIP 安全」或「安全」。

  - 在您組織的 Client Access Server 及 Mailbox Server 上，將 UM 啟動模式設定為 TLS 或雙重。

  - 利用完整網域名稱 (FQDN) 建立及設定新的或現有的 UM IP 閘道。

  - 將 UM IP 閘道上的接聽通訊埠設定為使用 TLS 通訊埠 5061。

  - 重新啟動所有 Exchange 2013 Client Access Server 上的 UM 呼叫路由器服務，以及所有 Exchange 2013 Mailbox Server 上的 UM 服務。若要深入了解 UM 服務，請參閱 [UM 服務](um-services-exchange-2013-help.md)。

## 步驟 4： 在所有 Exchange 2013 Client Access server 上設定 UM 啟動模式

如果您使用 SIP 安全或 「 安全 」 撥號，您必須在 Exchange 2013 Client Access server 上設定 UM 啟動模式。您可以使用 EAC 或命令介面 Exchange 2013 Client Access server 上指定的 UM 呼叫路由器服務的 UM 啟動模式。根據預設，TCP 模式會開始 Exchange 2013 Client Access server，但如果您使用傳輸層安全性 (TLS) 來加密 Voice over IP (VoIP) 流量，您必須設定使用 TLS 或雙重模式的 Exchange 2013 用戶端存取伺服器。我們建議所有 Exchange 2013 Client Access server 都設定為雙作為 UM 啟動模式。這是因為所有 Exchange 2013 Client Access 伺服器可以回覆來電的所有 UM 撥號對應表，及這些撥號對應表可以都有不同的安全性設定。如果您變更 UM 啟動模式，您必須重新 UM 呼叫路由器服務的變更才會生效。深入了解 UM 服務，請參閱 ＜ [UM 服務](um-services-exchange-2013-help.md)。

使用 EAC，在 Exchange 2013 Client Access Server 上設定 UM 啟動模式，如下所示：

1.  在 EAC 中，瀏覽至 \[伺服器\] \> \[伺服器\]。

2.  在清單檢視中，選取您要修改的 Exchange 伺服器，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 **\[Exchange Server\]** 頁面上，按一下 **\[整合通訊\]**。

4.  在 **\[UM 呼叫路由器設定\]** \> **\[UM 啟動模式\]** 下，從下拉式清單中選取下列其中一項：
    
      - **TCP**   如果您不是使用 mTLS，而且所使用的僅是不安全的撥號對應表，請使用此選項。
    
      - **TLS**   如果您是使用 mTLS，而且所使用的僅是「SIP 安全」或「安全」撥號對應表，請使用此選項。
    
      - **雙重**   如果您是使用 mTLS，而且使用「不安全」、「SIP 安全」和「安全」撥號對應表，請使用此選項。

5.  選取 UM 啟動模式之後，按一下 **\[儲存\]**。

在命令介面中執行下列命令，於 Exchange 2013 Client Access Server 上設定 UM 啟動模式。

    Set-UMCallRouterSettings -Server MyUMCallRouter.northwindtraders.com -UMStartupMode Dual

## 步驟 5： 在所有 Exchange 2013 Mailbox server 上設定 UM 啟動模式

如果您要使用「SIP 安全」或「安全」撥號對應表，則必須在 Exchange 2013 Mailbox Server 上設定 UM 啟動模式。您可以使用 EAC 或命令介面，在 Exchange 2013 Mailbox Server 上指定 UM 服務的 UM 啟動模式。根據預設，Exchange 2013 Mailbox Server 將以 TCP 模式啟動，但如果您是使用傳輸層安全性 (TLS) 加密 VoIP (Voice over IP) 流量，則必須將 Exchange 2013 Mailbox Server 設定為使用 TLS 或雙重模式。建議您將所有 Exchange 2013 Mailbox Server 設定為以雙重模式作為 UM 啟動模式。這是因為所有 Exchange 2013 Mailbox Server 都可以接聽所有 UM 撥號對應表的來電，而這些撥號對應表會有不同的安全性設定。如果您變更 UM 啟動模式，則必須重新啟動 UM 服務，變更才會生效。若要深入了解 UM 服務，請參閱 [UM 服務](um-services-exchange-2013-help.md)。

使用 EAC，在 Exchange 2013 Mailbox Server 上設定 UM 啟動模式，如下所示：

1.  在 EAC 中，瀏覽至 \[伺服器\] \> \[伺服器\]。

2.  在清單檢視中，選取您要修改的 Exchange 伺服器，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 **\[Exchange Server\]** 頁面上，按一下 **\[整合通訊\]**。

4.  在 **\[UM 服務設定\]** \> **\[UM 啟動模式\]** 下，從下拉式清單中選取下列其中一項：
    
      - **TCP**   如果您不是使用 mTLS，而且所使用的僅是不安全的撥號對應表，請使用此選項。
    
      - **TLS**   如果您是使用 mTLS，而且所使用的僅是「SIP 安全」或「安全」撥號對應表，請使用此選項。
    
      - **雙重**   如果您是使用 mTLS，而且使用「不安全」、「SIP 安全」和「安全」撥號對應表，請使用此選項。

5.  選取 UM 啟動模式之後，按一下 **\[儲存\]**。

在命令介面中執行下列命令，於 Exchange 2013 Mailbox Server 上設定 UM 啟動模式。

    Set-UMService -Identity MyUMServer -ExternalHostFqdn host.external.contoso.com -IPAddressFamily Any -UMStartupMode Dual

## 步驟 6︰ 建立或設定現有的 UM 撥號計劃

依據您現有的 Exchange 2007 部署，您可能需要建立新的 UM 撥號或設定現有的撥號計劃。UM 撥號對應表代表繁體中文或已啟用 SIP 的專用交換機 (Pbx)、 IP Pbx 或已啟用 SIP 的 Pbx 共用一般使用者的分機號碼的一組。繁體中文或已啟用 SIP 的 Pbx 或 IP Pbx 上常駐撥號對應表的所有使用者的分機包含相同數目的數字。使用者可以撥打彼此的電話分機而擴充附加的特殊的數字或完整的電話號碼來撥號。

UM 撥號對應表會用於整合通訊以確保使用者電話分機是唯一。部分的電話語音網路中多個 IP Pbx、 傳統 Pbx 或已啟用 SIP 的 Pbx 存在。在這些電話語音的網路，可能是兩個使用者具有相同的電話分機號碼。UM 撥號對應表解決所發生此情況。放入兩個不同 UM 撥號對應表的兩個使用者進行其副檔名唯一。如需詳細資訊，請參閱[UM 撥號對應表](https://docs.microsoft.com/zh-tw/exchange/voice-mail-unified-messaging/connect-voice-mail-system/um-dial-plans)。

如有需要，您可以使用 EAC 來建立 UM 撥號對應表：

1.  在 EAC 中，瀏覽至 **\[整合通訊\]** \> **\[UM 撥號對應表\]**，然後按一下 **\[新增\]**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

2.  在 **\[新增 UM 撥號對應表\]** 頁面上，完成下列的資訊：
    
      - **名稱** 輸入撥號對應表的名稱。UM 撥號對應表名稱是必要項目，而且必須是唯一的名稱。不過，您輸入的名稱只能在 EAC 和命令介面中作為顯示用途。UM 撥號對應表的長度上限為 64 個字元，可包含空格。不過不可包含下列任何一個字元：" / \\ \[ \] : ; | = , + \* ? \< \>.
        
        雖然撥號對應表名稱方塊可接受 64 個字元，但撥號對應表名稱不可超過 49 個字元。若嘗試建立包含超過 49 個字元的撥號對應表名稱，就會收到錯誤訊息。訊息指出，因為 UM 撥號對應表名稱太長，所以無法產生 UM 信箱原則。發生此情況的原因是當您建立撥號對應表時，也會建立名稱為「*\<DialPlanName\>***預設原則**」的預設 UM 信箱原則。當預設原則中的 15 個字元新增至撥號對應表的名稱時，總字元數隨即超出限制。UM 撥號對應表與 UM 信箱原則的 *name* 參數長度可為 64 個字元。不過，若撥號對應表名稱超過 49 個字元，則預設 UM 信箱原則名稱會超過 64 個字元，系統並不支援此情況。
    
      - \[分機號碼長度 (數字位數)\]   輸入 UM 撥號對應表中的分機號碼位數。分機號碼位數是以在 PBX 上建立的電話語音撥號對應表為依據。例如，若與電話語音撥號對應表關聯的使用者，要撥打 4 位數的分機來呼叫同一電話語音撥號對應表中的另一位使用者，則選取 4 來作為分機號碼位數。
        
        這是必要方塊，值的範圍為 1 到 20。一般分機號碼的長度為 3 到 7 碼。如果您現有的電話語音環境包含分機號碼，則必須指定與那些分機號碼位數相符的位數。
        
        建立電話分機撥號對應表時，若使用者連結到電話分機撥號對應表，則需要輸入該名使用者的分機號碼。已啟用 UM 的使用者連結到 SIP URI 或 E.164 撥號對應表時，需要工作階段初始通訊協定 (SIP) 撥號對應表或 E.164 撥號對應表的分機號碼。Outlook 語音存取使用者存取自己的 Exchange 信箱時，就會使用此分機號碼。
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(UI\_URI 類型)
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(UI\_VoIP 安全性)
    
      - \[國家/地區碼\]   使用此方塊可輸入用於撥出電話的國家/地區碼。此號碼會自動加在要撥打的電話號碼前面。此方塊接受 1 到 4 位數字。例如，美國的國家/地區碼為 1；英國為 44。

3.  按一下 **\[儲存\]**。

如有需要，您可以在命令介面中執行下列命令來建立 UM 撥號對應表。

    New-UMDialplan -Name MyUMDialPlan -URIType E164 -NumberOfDigitsInExtension 5 -VoIPSecurity Secured

如有需要，您可以使用 EAC 來設定現有的 UM 撥號對應表：

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。

2.  在清單檢視中，選取您要檢視或修改的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[UM 撥號對應表\] 頁面上，按一下 \[設定\]。使用組態選項來檢視特定的撥號對應表設定，以及啟用或停用功能。

如有需要，您可以在命令介面中執行下列命令來設定現有的 UM 撥號對應表。

    Set-UMDialplan -Identity MyDialPlan -AccessTelephoneNumbers 4255551234 -AudioCodec Wma -CallAnsweringRulesEnabled $false -OutsideLineAccessCode 9 -VoIPSecurity SIPSecured

當您部署 Exchange 2007 整合通訊時，您將需要將整合通訊伺服器新增至 UM 撥號對應其接聽來電。這是不再需要。在 Exchange 2013 用戶端存取和信箱伺服器無法連結與電話分機號碼或 E.164 撥號對應表，但必須連結至 SIP URI 撥號對應表。用戶端存取和信箱伺服器會回應所有的傳入呼叫所有類型的撥號對應表。

## 步驟 7： 建立或設定現有的 UM IP 閘道

依據現有的 Exchange 2007 部署，您可能需要新的 UM IP 閘道建立或設定現有的錯誤。如果您使用 SIP 安全或 「 安全 」 撥號，您必須建立 UM IP 閘道 fqdn 和使用命令介面將其設定為連接埠 5061 上接聽。為現有的 UM IP 閘道器，確認其正在使用 FQDN 設定聆聽連接埠 5061 上。如果的 UM IP 閘道不使用 FQDN，使用 EAC 或命令介面來變更地址。如果 UM IP 閘道器不會使用連接埠 5061，使用命令介面來變更連接埠。您可以使用**Get-UMIPGateway**指令程式來檢視 UM IP 閘道的設定。

UM IP 閘道器代表實體 VoIP (Voice over IP) 閘道、IP PBX 或已啟用 SIP 的 PBX。在 VoIP 閘道、IP PBX 或已啟用 SIP 的 PBX 可以用來接聽來電，並為語音信箱使用者傳送撥出電話前，必須在目錄服務中建立 UM IP 閘道器。

結合 UM IP 閘道器與 UM 群組搜尋，可在 VoIP 閘道、IP PBX 或已啟用 SIP 的 PBX 與 UM 撥號對應表之間建立連結。透過建立多個 UM 群組搜尋，您可以將單一 UM IP 閘道器與多個 UM 撥號對應表產生關聯。如需詳細資訊，請參閱 [UM IP 閘道](https://docs.microsoft.com/zh-tw/exchange/voice-mail-unified-messaging/connect-voice-mail-system/um-ip-gateways)。

如有需要，您可以使用 EAC 來建立 UM IP 閘道，如下所示：

1.  在 EAC 中，瀏覽至 **\[整合通訊\]** \> **\[UM IP 閘道\]**，然後按一下 **\[新增\]**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

2.  在 **\[新增 UM IP 閘道\]** 頁面上，輸入下列資訊：
    
      - \[名稱\]   使用此方塊可指定 UM IP 閘道器的唯一名稱。這是出現在 EAC 中的顯示名稱。如果建立 UM IP 閘道器後必須變更它的顯示名稱，您必須先刪除現有的 UM IP 閘道器，然後建立另一個具有適當名稱的 UM IP 閘道器。UM IP 閘道器名稱是必要的，不過僅供顯示之用。由於您的組織可能使用多個 UM IP 閘道器，建議您為 UM IP 閘道器使用有意義的名稱。UM IP 閘道器名稱的長度上限是 64 個字元，且可以包含空格。不過不可包含下列任何一個字元：" / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **位址**   您可以使用 IPv4、IPv6 位址或 FQDN，來設定 UM IP 閘道器。使用此方塊，可指定 VoIP 閘道、IP PBX 或已啟用 SIP 的 PBX 上所設定的 IP 位址或 FQDN。此方塊僅接受有效且格式正確的 FQDN。
        
        您可以輸入字母和數字字元。支援 IPv4 位址、 IPv6 位址及 Fqdn。如果您想要使用的 UM IP 閘道間的相互 TLS 和撥號對應表作業中 SIP 安全或安全模式，您必須設定 UM IP 閘道 fqdn。您也必須設定該連接埠 5061 上接聽，驗證的任何 VoIP 閘道或 IP Pbx 也已經設定聆聽的連接埠 5061 上的相互 TLS 要求。若要設定 UM IP 閘道器，請執行下列命令在介面： `Set-UMIPGateway -identity MyUMIPGateway -Port 5061`
        
        如果您使用 FQDN，還必須確定已正確設定 VoIP 閘道、IP PBX 或已啟用 SIP 的 PBX 的 DNS 主機記錄，這樣主機名稱才會正確解析成 IP 位址。另外，如果您使用 FQDN 而非 IP 位址，並變更 UM IP 閘道器的 DNS 組態，則必須停用然後啟用 UM IP 閘道器，以確保正確更新 UM IP 閘道器的組態資訊。
    
      - **UM 撥號對應表**   按一下 **\[瀏覽\]** 可選取您想要與 UM IP 閘道器關聯的 UM 撥號對應表。當選取要與 UM IP 閘道器建立關聯的 UM 撥號對應表時，同時也會建立預設的 UM 群組搜尋，並將其與您所選取的 UM 撥號對應表建立關聯。若您並未選取 UM 撥號對應表，則必須以手動方式建立 UM 群組搜尋，然後將該 UM 群組搜尋與您已建立的 UM IP 閘道器建立關聯。

3.  按一下 **\[儲存\]**。

如有需要，您可以在命令介面中執行下列命令來建立 UM IP 閘道。

    New-UMIPGateway -Identity MyUMIPGateway -Address "MyUMIPGateway.contoso.com"

如有需要，您可以使用 EAC 來設定現有的 UM IP 閘道：

1.  在 EAC 中，瀏覽至 **\[整合通訊\]** \> **\[UM IP 閘道\]**，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 **\[UM IP 閘道器\]** 頁面上，按一下 **\[設定\]**。使用組態選項來檢視特定的 UM IP 閘道器設定，以及啟用或停用功能。

如有需要，您可以在命令介面中執行下列命令來設定現有的 UM IP 閘道。

    Set-UMIPGateway -Identity MyUMIPGateway -Address fe80::39bd:88f7:6969:d223%11 -IPAddressFamily Any -Status Disabled -OutcallsAllowed $false

## 步驟 8： 建立 UM 群組搜尋

依據您現有的 Exchange 2007 部署，您可能需要建立新 UM 群組搜尋。電話語音群組搜尋提供一種方式來散佈至多個副檔名的電話通話從單一數字或電話號碼。整合通訊中 UM 群組搜尋群組的電話語音搜尋，以邏輯方式呈現，且其連結至 UM 撥號對應表 UM IP 閘道器。

您至少要有一個適用於所有 IP PBX 或 PBX 群組搜尋的 UM 群組搜尋。在您完成下列程序之後，依預設會建立一個 UM 群組搜尋。若您有多個 IP PBX 或 PBX 群組搜尋，則您必須建立其他 UM 群組搜尋。若要深入了解 UM 群組搜尋，請參閱[UM 群組搜尋](https://docs.microsoft.com/zh-tw/exchange/voice-mail-unified-messaging/connect-voice-mail-system/um-hunt-groups)。

如有需要，您可以使用 EAC 來建立 UM 群組搜尋：

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。在清單檢視中，選取您要修改的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 **\[UM 撥號對應表\]** 頁面的 **\[UM 群組搜尋\]** 下，按一下 **\[新增\]**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

3.  在 **\[新增 UM 群組搜尋\]** 頁面上，輸入下列資訊：
    
      - \[名稱\]   使用此方塊可建立 UM 群組搜尋的顯示名稱。UM 群組搜尋名稱是必要項目，而且必須是唯一的，但是，它只能在 EAC 和命令介面中作為顯示用途。如果您在建立群組搜尋之後，必須變更其顯示名稱，則必須先刪除現有的群組搜尋，然後再建立另一個具有適當名稱的群組搜尋。如果您的組織使用多個群組搜尋，建議為您的群組搜尋使用有意義的名稱。UM 群組搜尋名稱的長度上限是 64 個字元，且可以包含空格。不過不可包含下列任何一個字元：" / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **UM IP 閘道器**   使用此方塊來選取 UM IP 閘道器。此方塊會顯示將與 UM 群組搜尋連結之 UM IP 閘道器的名稱。若要將 UM IP 閘道器連結至 UM 群組搜尋，請按一下 **\[瀏覽\]**。
    
      - **引導識別碼**   使用此方塊可指定一個字串，以唯一識別 PBX 或 IP PBX 上所設定的引導識別碼。您可以在此方塊中使用分機號碼或 SIP 統一資源識別碼 (URI)。此方塊可接受英數字元。若為傳統 PBX，則會使用數值來作為引導識別碼。不過，有些 IP PBX 及已啟用 SIP 的 PBX 可以使用 SIP URI。

4.  按一下 **\[儲存\]**。

如有需要，您可以在命令介面中執行下列命令來建立 UM 群組搜尋。

    New-UMHuntGroup -Name MyUMHuntGroup -PilotIdentifier 5551234,55555 -UMDialPlan MyUMDialPlan -UMIPGateway MyUMIPGateway


> [!TIP]  
> 您無法設定或變更 UM 群組搜尋的設定。如果想要變更 UM 群組搜尋的組態設定，您必須刪除它，然後利用正確設定來新增 UM 群組搜尋。




## 步驟 9： 建立或設定 UM 自動語音應答

依據您現有的 Exchange 2007 部署，您可能需要建立新的 UM 自動語音應答。您可以使用 UM 自動語音應答建立可讓語音功能表系統外部與內部的來電者使用的 UM 自動語音應答功能表系統來尋找人員及放置或將來電轉接至公司使用者或組織內的部門。如需詳細資訊，請參閱[自動接聽和路由傳送來電](https://docs.microsoft.com/zh-tw/exchange/voice-mail-unified-messaging/automatically-answer-and-route-calls/automatically-answer-and-route-calls)。

在較小的部署可能僅要部署 UM 使來電者可以留下語音信箱的使用者。在這些部署中，建立自動語音應答並非必要。不過，在大多數情況下，使用自動語音應答時非常有用的外部來電者在他們撥入您的組織。

如有需要，您可以使用 EAC 來建立 UM 自動語音應答，如下所示：

1.      
    在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。選取您要新增自動語音應答的 UM 撥號對應表，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 **\[UM 撥號對應表\]** 頁面的 **\[UM 自動語音應答\]** 下，按一下 **\[新增\]**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

3.  在 **\[新增 UM 自動語音應答\]** 頁面上，填妥下列方塊：
    
      - **名稱**   使用此方塊可建立 UM 自動語音應答的顯示名稱。UM 自動語音應答名稱是必要項目，而且必須是唯一的。但是，它只能在 EAC 和命令介面中作為顯示用途。如果您在建立自動語音應答後必須變更其顯示名稱，必須先刪除現有的 UM 自動語音應答，然後建立另一個具有適當名稱的自動語音應答。如果您的組織使用多個自動語音應答，則建議為 UM 自動語音應答使用有意義的名稱。UM 自動語音應答名稱的最大長度為 64 個字元，可以包含空格。
        
        雖然您可以在命名新的 UM 自動語音應答時包含空白字元，但若您將整合通訊與 Lync Server 進行整合，自動語音應答的名稱就不能包含空白字元。因此，如果您建立自動語音應答時在顯示名稱中使用空白字元，而且將與 Lync Server 進行整合，則您必須先刪除該自動語音應答，然後建立另一個在顯示名稱中不包含空白字元的自動語音應答。
    
      - \[建立此自動語音應答為已啟用\]   完成建立 UM 自動語音應答時，選取此核取方塊可讓自動語音應答接聽來電。預設會將新的自動語音應答建立為已停用。如果您決定將 UM 自動語音應答建立為已停用，在您完成建立後可使用 EAC 或命令介面來啟用自動語音應答。
    
      - \[設定自動應答以回應語音指令\]   選擇此核取方塊以啟用自動語音應答的語音功能。若啟用自動語音應答的語音功能，來電者可使用撥號音或語音輸入，來回應 UM 自動語音應答所使用的系統或自訂提示。依預設，自動語音應答建立後並不支援語音功能。若要讓來電者使用美式英文 (en-US) 以外語言啟用語音的自動語音應答，您必須安裝適當 UM 語言套件，並設定自動語音應答的內容以使用此語言。安裝 Exchange 2013 Mailbox Server 時，會預設安裝 en-US UM 語言套件。
    
      - **存取號碼** 輸入來電者將用於聽取自動語音應答的分機號碼或電話號碼。在方塊中輸入分機號碼或電話號碼，然後按一下 **\[新增\]** 將該號碼新增到清單。您提供的分機號碼或電話號碼的位數，不必符合相關聯之 UM 撥號對應表中所設定的分機號碼位數。這是因為允許 UM 自動語音應答接受直接來電。
        
        可輸入的分機號碼或存取號碼數量沒有限制。然而，您可以建立新的自動語音應答，而不必列出分機號碼或電話號碼。分機號碼或電話號碼不是必要的。您可以編輯或移除現有的分機號碼或引導識別碼。若要編輯現有的分機號碼或電話號碼，請按一下 **\[編輯\]**。若要從清單中移除現有的分機號碼或電話號碼，請按一下 **\[移除\]**。

4.  按一下 **\[儲存\]**。

如有需要，您可以在命令介面中執行下列命令來建立 UM 自動語音應答。

    New-UMAutoAttendant -Name MyUMAutoAttendant -UMDialPlan MyUMDialPlan -PilotIdentifierList 56000,56100 -SpeechEnabled $true -Status Enabled

如有需要，您可以使用 EAC 來設定現有的自動語音應答：

1.  在 EAC 中，瀏覽至 **\[整合通訊\]** \> **\[UM 撥號對應表\]**，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 **\[UM 撥號對應表\]** 頁面的 **\[UM 自動語音應答\]** 下，選取您要檢視或設定的 UM 自動語音應答，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。使用組態選項來檢視特定的自動語音應答設定，以及啟用或停用功能。

如有需要，您可以在命令介面中執行下列命令來設定現有的自動語音應答。

    Set-UMAutoAttendant -Identity MySpeechEnabledAA -DTMFFallbackAutoAttendant MyDTMFAA -OperatorExtension 50100 -AfterHoursTransferToOperatorEnabled $true -StaroutToDialPlanEnabled $true

## 步驟 10： 建立或設定 UM 信箱原則

依據您現有的 Exchange 2007 部署，您可能需要建立新的 UM 信箱原則或設定現有的 UM 信箱原則。當您啟用使用者的整合通訊 UM 信箱原則是必要的。每個已啟用 UM 之使用者的信箱必須連結至單一的 UM 信箱原則。建立 UM 信箱原則之後，您會連結至 UM 信箱原則的一或多個已啟用 UM 的信箱。這可讓您控制 PIN 安全性設定，例如 PIN 的數字數目最小值或連結到的 UM 信箱原則的 UM 啟用使用者的登入嘗試的數目上限。如需詳細資訊，請參閱[UM 信箱原則](https://docs.microsoft.com/zh-tw/exchange/voice-mail-unified-messaging/set-up-voice-mail/um-mailbox-policies)。

如有需要，您可以使用 EAC 來建立 UM 信箱原則：

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。在清單檢視中，選取您要修改的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 **\[UM 撥號對應表\]** 頁面的 **\[UM 信箱原則\]** 底下，按一下 **\[新增\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 **\[新增 UM 信箱原則\]** 頁面的 **\[名稱\]** 方塊中，輸入新 UM 信箱原則的名稱。
    
    > [!NOTE]  
    > 使用這個方塊來指定 UM 信箱原則的唯一名稱。這是出現在 EAC 中的顯示名稱。如果您在建立 UM 信箱原則後必須變更其顯示名稱，必須先刪除現有的 UM 信箱原則，然後建立另一個具有適合名稱的 UM 信箱原則。如果有任何啟用 UM 的使用者與 UM 信箱原則相關聯，則您無法刪除該原則。UM 信箱原則名稱是必要的，但僅供顯示之用。由於您的組織可能使用多個 UM 信箱原則，我們建議您針對 UM 信箱原則使用有意義的名稱。UM 信箱原則名稱的長度上限是 64 個字元，且可以包含空格。不過不可包含下列任一字元：&quot; / \ [ ] : ; | = , + * ? &lt; &gt;.


4.  按一下 **\[儲存\]**。
    
    > [!NOTE]  
    > 將儲存的 UM 信箱原則，則會啟用所有預設設定，包括 PIN 原則、 語音信箱功能，以及受保護的語音信箱設定。如果您要自訂或變更任何預設設定您剛才建立之 UM 信箱原則，請使用<strong>Set-UMMailbox</strong> cmdlet 或 EAC。


如有需要，您可以在命令介面中執行下列命令來建立 UM 信箱原則。

    New-UMMailboxPolicy -Name MyUMMailboxPolicy -UMDialPlan MyUMDialPlan

如有需要，您可以使用 EAC 來設定現有的 UM 信箱原則：

1.  在 EAC 中，瀏覽至 **\[整合通訊\]** \> **\[UM 撥號對應表\]**，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 **\[UM 撥號對應表\]** 頁面的 **\[UM 信箱原則\]** 下，選取您要檢視或設定的 UM 信箱原則，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。使用組態選項來檢視特定的 UM 信箱原則設定，以及啟用或停用功能。

如有需要，您可以在命令介面中執行下列命令來設定現有的 UM 信箱原則。

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 8 -MaxLogonAttempts 12 -MinPINLength 8 -PINHistoryCount 10 -PINLifetime 60 -ResetPINText "The PIN used to allow you access to your mailbox using Outlook Voice Access has been reset."

## 步驟 11： 將現有的啟用 UM 的信箱移至 Exchange 2013

在 Exchange 2007 Unified Messaging 後已啟用組織內的使用者使用 \[語音信箱、 一組預設 UM 屬性會套用至使用者，以便他們可以使用 UM 功能。如需詳細資訊，請參閱[使用者的語音信箱](https://docs.microsoft.com/zh-tw/exchange/voice-mail-unified-messaging/set-up-voice-mail/voice-mail-for-users)。

在升級的過程中，會一段時間的期間您必須已啟用 Exchange 2007 信箱伺服器上與 Exchange 2013 Mailbox server 上的 UM 信箱。不過，如果您正在將所有已啟用 UM 的使用者移至 Exchange 2013 Mailbox server 中，您必須使用 EAC 或**New-MoveRequest**指令程式在命令介面中的 Exchange 2013 伺服器從保留的所有屬性及設定，包括使用者的 PIN。

移動要求是將信箱從一個信箱資料庫移動到另一個的處理程序。本機移動要求指的是在單一樹系中發生的信箱移動作業。如需信箱移動的詳細資訊，請參閱：

  - [在 Exchange 2013 移動信箱](mailbox-moves-in-exchange-2013-exchange-2013-help.md)

  - [New-MoveRequest](https://technet.microsoft.com/zh-tw/library/dd351123\(v=exchg.150\))

  - [New-MigrationBatch](https://technet.microsoft.com/zh-tw/library/jj219166\(v=exchg.150\))

  - [移動信箱](https://go.microsoft.com/fwlink/p/?linkid=296351)

若要使用 EAC 將 Exchange 2007 信箱移至 Exchange 2013 Mailbox Server，請執行下列動作：

1.  在 EAC 中，按一下 **\[收件者\]** \> **\[遷移\]**，然後按一下 **\[新增\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 **\[新本機信箱移動精靈\]** 中，選取您想要移動的使用者，然後依序按一下 **\[確定\]** 和 **\[下一步\]**。

3.  在\[移動組態\] 頁面上，指定新建批次的名稱。為封存信箱及信箱資料庫位置選取您想要的選項，然後按一下 **\[新增\]**。

若要使用命令介面將 Exchange 2007 信箱移至 Exchange 2013 Mailbox Server，請執行下列命令。

    New-MoveRequest -Identity 'tony@alpineskihouse.com' -TargetDatabase "DB01"

## 步驟 12： 新的使用者啟用 um，或設定現有已啟用 UM 之使用者的設定

使用者在啟用信箱的整合通訊前須先擁有信箱。但是根據預設，不會為擁有信箱的使用者啟用 UM。在使用者擁有 UM 功能之後，您才能管理、修改及設定使用者的 UM 屬性與語音信箱功能。您可以使用 EAC 或命令介面，讓使用者啟用 UM。若要深入了解，請參閱 [使用者的語音信箱](https://docs.microsoft.com/zh-tw/exchange/voice-mail-unified-messaging/set-up-voice-mail/voice-mail-for-users)。

讓使用者啟用 UM 時，您至少必須定義一個分機號碼，讓 UM 在提交語音郵件給使用者的信箱時使用，以及允許使用者使用 Outlook 語音存取。讓使用者啟用 UM 後，可以在使用者的信箱上設定 Exchange 整合通訊 (EUM) Proxy 位址以在使用者的信箱新增次要分機號碼，或是在 EAC 中新增或移除使用者的額外或次要分機。若要新增、修改或移除分機號碼、E.164 號碼或 SIP 位址，請參閱[擁有郵件功能的語音使用者程序](https://docs.microsoft.com/zh-tw/exchange/voice-mail-unified-messaging/set-up-voice-mail/voice-mail-enabled-user-procedures)。

若要使用 EAC 讓使用者啟用整合通訊，請執行下列動作：

1.  在 EAC 中，按一下 \[收件者\]。

2.  在清單檢視中，選取您要啟用其信箱之整合通訊功能的使用者。

3.  在 \[詳細資料\] 窗格中，於 \[電話和語音功能\] 下方，按一下 \[啟用\]。

4.  在 **\[啟用 UM 信箱\]** 頁面上，按一下 **\[UI 信箱原則\]** 旁邊的 **\[瀏覽\]** 按鈕，從清單中找出 UM 信箱原則以便指派使用者，然後按一下 **\[確定\]**。

5.  在 \[啟用 UM 信箱\] 頁面上，完成下列方塊：
    
      - **SIP 位址或 E.164 號碼**  輸入使用者的 SIP 位址或 E.164 號碼。當您啟用整合通訊的使用者指派給 UM 信箱原則連結至 SIP URI 或撥號對應表 E.164 則這些選項。新增 SIP 位址或使用者的 E.164 號碼並未提供使用者與電話分機撥號相關聯時。當您將使用者指派給 UM 信箱原則連結至 SIP URI 或撥號對應表 E.164 時，您也必須輸入使用者的分機號碼。當使用者存取使用Outlook語音存取其信箱，會使用此分機號碼。您在此方塊中設定的數字數目必須符合的 SIP URI 上設定的數字數目或撥號對應表 E.164。
    
      - **分機號碼** 輸入您正在啟用 UM 的使用者的分機號碼。
        
        您必須為使用者提供有效的分機號碼，而且其必須符合撥號對應表上指定的位數。您僅能輸入 1 到 20 的數值字元或數字。一般分機號碼的長度為 3 到 7 個數字。分機號碼的位數是在連結到指派給使用者的 UM 信箱原則的撥號對應表上設定。
    
      - 在 \[PIN 碼設定\] 底下，完成下列操作：
        
          - **自動產生 PIN 碼**   按一下此按鈕可為啟用 UM 的使用者自動產生 PIN 碼，以便透過 Outlook Voice Access 存取語音信箱。這是預設設定。按一下此按鈕時，則會根據指派給使用者的 UM 信箱原則上所設定的 PIN 碼原則，自動產生 PIN 碼。建議您使用此設定來協助保護使用者的 PIN 碼。為使用者啟用 UM 後，將以使用者收到的歡迎訊息將 PIN 碼傳送給使用者。依預設，使用者第一次登入信箱取得語音郵件時，必須變更 PIN 碼。
        
          - **輸入 PIN 碼**   按一下此按鈕可手動指定使用者將用來存取語音信箱系統的 PIN 碼。PIN 碼必須符合針對與這個啟用 UM 的使用者相關聯的 UM 信箱原則所設定的 PIN 碼原則設定。例如，如果將 UM 信箱原則設定為只接受七位數 (含) 以上的 PIN 碼，則在此方塊中輸入的 PIN 碼至少必須有七位數。
        
          - **要求使用者第一次登入時必須重設 PIN 碼**   選取此核取方塊可強制使用者第一次從電話使用 Outlook Voice Access 存取語音信箱系統時，重設其語音信箱 PIN 碼。系統會提示使用者輸入他們更熟悉的 PIN 碼。這種安全性最佳實務可強制啟用 UM 的使用者在第一次登入時變更 PIN 碼，有助於防範未經授權而存取使用者的資料和收件匣。預設會選取此核取方塊。

6.  在 \[啟用 UM 信箱\] 頁面上，檢閱您的設定。按一下 **\[完成\]**，讓使用者啟用整合通訊。按一下 **\[上一步\]** 可以變更組態。

在命令介面中對使用者啟用整合通訊，請執行下列命令。

    Enable-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy -Extensions 51234 -PIN 5643892 -NotifyEmail administrator@contoso.com -PINExpired $true

如有需要，您可以使用 EAC 來設定已啟用 UM 的使用者：

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[信箱\]。

2.  在清單檢視中，選擇您要變更 UM 信箱原則的信箱。

3.  在詳細資料窗格中的 \[電話與語音功能\] \> \[整合通訊\] 下方，按一下 \[檢視詳細資料\]。

4.  在 \[UM 信箱\] 頁面上，按一下 \[UM 信箱設定\] 以檢視或變更現有已啟用 UM 功能之使用者的下列 UM 內容：
    
      - **PIN 狀態**   此僅供顯示的方塊可顯示使用者的信箱狀態。根據預設，當使用者啟用 UM 時，PIN 狀態會列示為 **\[未鎖定\]**。不過，如果使用者多次輸入了不正確的 Outlook 語音存取 PIN 碼，狀態就會列為 **\[鎖定\]**。
    
      - **UM 信箱原則**   此方塊可顯示與啟用 UM 的使用者相關聯的 UM 信箱原則名稱。您可以按一下 **\[瀏覽\]**，尋找並指定要與此 UM 信箱相關聯的 UM 信箱原則。
    
      - \[個人操作員分機號碼\]   使用這個方塊來指定使用者的操作員分機號碼。依預設，不會設定分機號碼。分機號碼的長度可以從 1 個到 20 個字元。這樣可讓已啟用 UM 之使用者的來電轉送到您在此方塊中指定的分機號碼。
        
        您可以在撥號對應表及自動語音應答上，設定其他類型的操作員分機號碼。不過，這些分機號碼通常是供全公司的接待員或總機人員使用。當行政助理或個人助理接聽特定使用者的來電時，便會使用到個人操作員分機號碼設定。

5.  在 \[UM 信箱\] 頁面上的 \[其他分機\] 下方，您可以新增、變更與檢視使用者的分機號碼。
    
      - 若要新增分機號碼，按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。在 \[新增其他分機\] 頁面上，使用 \[瀏覽\] 來選取 UM 撥號對應表，接著在 \[分機號碼\] 方塊中輸入分機號碼。
    
      - 若要移除分機號碼，選取您想要移除的分機號碼，接著按一下 \[移除\]![\[移除\] 圖示](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[移除] 圖示")。

6.  如果您做了任何變更，請按一下 \[儲存\]。

如有需要，您可以在命令介面中執行下列命令來設定已啟用 UM 的使用者：

    Set-UMMailbox -Identity tony@contoso.com -CallAnsweringAudioCodec Wma -CallAnsweringRulesEnabled $false -FaxEnabled $false -UMSMSNotificationOption VoiceMail

## 步驟 13： 設定 VoIP 閘道、 IP Pbx 及已啟用 SIP 的 pbx 設定為傳送所有來電至 Exchange 2013 Client Access server

Exchange 2013 Client Access Server 及 Mailbox Server 會在安裝時自動啟用，以便可以接聽撥入及撥出的語音電話，並將語音信箱訊息路由傳送至預定的收件者。您在安裝 Exchange 2013 Client Access Server 及 Mailbox Server 以及部署整合通訊時，不需要將 Exchange 2013 Client Access Server 或 Mailbox Server 連結或新增至 UM 撥號對應表。Exchange 2013 Client Access Server 和 Mailbox Server 會於接聽來電後，使用 UM 撥號對應表找出使用者。

Exchange 2013 Client Access Server 是任何來電或整合通訊之工作階段初始通訊協定 (SIP) 要求的進入點。在 Exchange 2013 Client Access Server 上處理 SIP 要求的服務是 UM 呼叫路由器服務，而且組織中的每一部 Exchange 2013 Client Access Server 都會執行此服務。

您在升級至 Exchange 2013 UM 時，應該已經安裝並設定一個或多個用以在電話語音網路中連接至 PBX 的 VoIP 閘道，或是已經安裝並設定已啟用工作階段初始通訊協定 (SIP) 的 PBX 或 IP PBX。

在升級至 Exchange 2013 UM 的程序中，最後一個步驟是將 VoIP 閘道、IP PBX 或已啟用 SIP 的 PBX 設定為傳送來電 (包括想要留下語音郵件給使用者的來電者、撥打 Outlook 語音存取的啟用 UM 的使用者的來電，以及撥打 UM 自動語音應答的來電者的來電) 至 Exchange 2013 Client Access Server。所有這些來電會先由 VoIP 閘道、IP PBX 或已啟用 SIP 的 PBX 接收，然後轉接給 Exchange 2013 組織中的 Exchange 2013 Client Access Server。如需詳細資訊，請參閱下列資源：

  -  [UM 服務](um-services-exchange-2013-help.md)

  -  [支援 VoIP 閘道、 IP Pbx 和 Pbx 組態注意事項](https://docs.microsoft.com/zh-tw/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/configuration-notes-for-voip-gateways)

  -  [Exchange 2013 的電話語音 advisor](https://docs.microsoft.com/zh-tw/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/telephony-advisor-for-exchange-2013)

## 步驟 14： 停用自動答錄在 Exchange 2007 Unified Messaging server

您可以停用自動答錄服務由 Exchange 2007 Unified Messaging server 上停用 UM 或從撥號對應表移除 UM 伺服器。當您停用 UM 時，您會使整合通訊伺服器從接聽來電。您可以選擇立即中斷連線的所有通話或等待處理中停用整合通訊伺服器之前的現有電話。想要停用自動答錄服務之前，讓它將會完成處理任何傳入呼叫伺服器移除撥號對應表。

若要使用 Exchange 管理主控台來停用 Exchange 2007 UM Server 上的整合通訊，請執行下列動作：

1.  在 EMC 主控台樹狀目錄中，瀏覽至 **\[伺服器組態\]** \> **\[整合通訊\]**。

2.  在結果窗格中，選取要停用的整合通訊伺服器。

3.  在執行窗格中，按一下以下選項：
    
    1.  選取 **\[立即停用\]** 選項時，整合通訊伺服器會中斷所有連接至整合通訊伺服器之呼叫的連線。
    
    2.  若您選取 **\[在完成呼叫之後停用\]** 選項，整合通訊伺服器將不會接受新的呼叫，並且會在處理完所有呼叫之後才會予以停用。

4.  按一下確認對話方塊中的 **\[是\]** 繼續。

若要使用命令介面來停用 Exchange 2007 UM Server 上的整合通訊，請執行下列命令：

    Disable-UMServer -Identity MyUMServer -Immediate $true


> [!TIP]  
> 您可以從 Exchange 2007 UM Server 中使用 <strong>Disable-UMServer</strong> 指令程式，或從 Exchange 2013 Mailbox Server 中使用 <strong>Disable-UMService</strong> 指令程式，來停用自動答錄服務。




## 步驟 15： 從撥號對應表移除 Exchange 2007 Unified Messaging server

若要處理來電，Exchange 2007 UM 伺服器必須新增至至少一個 UM 撥號對應表。在 UM 伺服器可以新增至多個 UM 撥號對應表。您可以從 UM 撥號對應表移除 Exchange 2007 UM 伺服器。當您將在 UM 伺服器移除撥號對應表時、 UM 伺服器將不再接聽來電或程序已啟用 UM 之使用者的 UM 呼叫。

若要使用 Exchange 管理主控台從撥號對應表中移除 Exchange 2007 UM Server，請執行下列動作：

1.  在 EMC 主控台樹狀目錄中，瀏覽至 **\[伺服器組態\]** \> **\[整合通訊\]**。

2.  在結果窗格中，選取 \[Unified Messaging Server\]。

3.  在執行窗格中，按一下 **\[內容\]**。

4.  在 **\[UM 設定\]** 索引標籤的 **\[關聯的撥號對應表\]** 區段中，按一下 **\[移除\]**。

5.  在確認對話方塊中，按一下 **\[是\]** 確認從 UM 撥號對應表中刪除 Exchange 2007 Unified Messaging Server。

6.  按一下 **\[確定\]** 關閉內容視窗。

若要使用命令介面從撥號對應表中移除 Exchange 2007 UM Server，請執行下列命令：

    $dp= Get-UMDialPlan "MySIPDialPlan"
    $s=Get-UMServer -id MyUMServer
    $s.dialplans-=$dp.identity
    Set-UMServer -id MyUMServer -dialplans:$s.dialplans

此範例中有三個 SIP URI 撥號對應表：SipDP1、SipDP2 及 SipDP3。此範例會從 SipDP3 撥號對應表中移除名為 `MyUMServer` 的 UM Server。

    Set-UMServer -id MyUMServer -DialPlans SipDP1,SipDP2

此範例中有兩個 SIP URI 撥號對應表：SipDP1 及 SipDP2。此範例會從 SipDP2 撥號對應表中移除名為 `MyUMServer` 的 UM Server。

    Set-UMServer -id MyUMServer -DialPlans SipDP1


> [!TIP]  
> 您可以在 Exchange 2007 Unified Messaging server 命令介面或 Exchange 2013 Mailbox server 上的<strong>Set-UMService</strong>指令程式中使用<strong>Set-UMServer</strong>指令程式從單一或多個撥號對應表移除 Exchange 2007 UM 伺服器。例如，以移除所有撥號對應表 UM 伺服器，請執行下列命令： <code>Set-UMServer -identity MyUMServer -DialPlan $null</code>




## 如何才能了解這是否正常運作？

在您設定整合通訊之後，請確認下列事項以確保其運作正常：

  - 您已啟用語音信箱的使用者可登入 Outlook Web App 或 Outlook，且可看到整合通訊的歡迎訊息。

  - UM 使用者可以接收語音訊息。

  - UM 使用者可撥打 Outlook 語音存取號碼來接聽電子郵件、行事曆項目和語音郵件。

  - UM 正在路由傳送組織以外的來電，而且您可以撥打電話。

