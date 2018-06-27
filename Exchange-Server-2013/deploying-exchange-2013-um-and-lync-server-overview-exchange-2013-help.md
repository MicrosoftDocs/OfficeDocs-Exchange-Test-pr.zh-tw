---
title: '部署 Exchange 2013 UM 和 Lync Server 概觀 （英文）: Exchange 2013 Help'
TOCTitle: 部署 Exchange 2013 UM 和 Lync Server 概觀 （英文）
ms:assetid: 96fcb0dd-79ee-4e55-9e59-3ee7fbe3c4a1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb676409(v=EXCHG.150)
ms:contentKeyID: 50473825
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 部署 Exchange 2013 UM 和 Lync Server 概觀 （英文）

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2016-12-09_

整合通訊 (UM) 及 Microsoft Lync Server 可部署在一起，為您組織中的使用者提供語音訊息、立即訊息、增強的使用者出席、視聽會議，以及整合的電子郵件和訊息使用體驗。整合通訊可用來提供自動語音答錄服務、Outlook 語音存取及自動語音應答服務。Microsoft Lync Server 提供 Enterprise Voice 更多進階功能，如立即訊息 (IM)、會議管理，以及撥入和撥出電話。本主題討論如何設定整合通訊及 Microsoft Lync Server 以支援這些功能。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Microsoft Office Communications Server 2007 R2 也可以和整合通訊一起部署。本主題中，&amp;quot;Microsoft Lync Server&amp;quot; 係指 Microsoft Lync Server 2010 或 Microsoft Lync Server 2013。</td>
</tr>
</tbody>
</table>


尋找 Microsoft Lync Server 的詳細資訊吗？請參閱[Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752)。

**目錄**

Deploying Exchange UM and Lync Server overview

Certificate configuration recommendations

Deployment steps

For more information

## 部署 Exchange UM 和 Lync 伺服器概述

整合通訊會將語音和電子郵件結合成為單一郵件基礎結構。Microsoft Lync Server Enterprise Voice 善用 UM 基礎結構提供語音郵件、Outlook Voice Access、來電通知和自動語音應答等服務。

以下清單提供 UM 和 Lync 伺服器的簡單部署步驟。本主題後面包含每個步驟的相關詳細資訊。

1.  在執行 Microsoft Exchange 整合通訊呼叫路由器服務之用戶端伺服器的同一個拓撲中安裝 Microsoft Lync Server，接著將會安裝執行 Microsoft Exchange 整合通訊服務的信箱伺服器。確認至少已建立一個 Lync 集區。

2.  安裝有效且由私人或公開之憑證授權單位 (CA) 簽署且受 Lync 伺服器信任的憑證。

3.  安裝用戶端存取伺服器和信箱伺服器。驗證安裝。

4.  安裝您在 Lync 伺服器上安裝且由同一個 CA 所簽署的有效憑證。

5.  建立和設定工作階段初始通訊協定 (SIP) URI 撥號對應表。

6.  將所有用戶端存取和信箱伺服器新增到 SIP URI 撥號對應表。不過，假如您有多個 SIP URI 撥號對應表，您必須將所有用戶端存取和信箱伺服器新增到所有 SIP URl 撥號對應表中。

7.  從信箱伺服器上的 \<Exchange 安裝資料夾\>\\Exchange Server\\Script 資料夾執行 ExchUcUtil.ps1 指令碼。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>ExchUcUtil.ps1 指令碼可為 Lync 整合建立一或多個 UM IP 閘道。您必須在除了指令碼所建立的一個閘道以外的所有 UM IP 閘道上，停用撥出電話。這包括在已於執行指令碼之前就建立的 UM IP 閘道上，停用撥出電話。若要在 UM IP 閘道上停用撥出電話，請參閱<a href="disable-outgoing-calls-on-um-ip-gateways-exchange-2013-help.md">停用 UM IP 閘道器上的撥出電話</a>。</td>
    </tr>
    </tbody>
    </table>


8.  從 Lync 伺服器上的 %CommonProgramFiles%\\Microsoft Lync Server 2013\\Support 資料夾執行 **OcsUmUtil.exe**。

9.  部署中繼伺服器和媒體閘道器。

10. 在您的中繼伺服器上安裝與您在 Lync 伺服器上安裝且由同一個 CA 所簽署的有效憑證。

11. 啟用使用者的 UM 和 Enterprise Voice。

## 憑證設定建議

您必須有一個由執行 Exchange 之電腦和執行 Lync 伺服器之電腦兩者皆信任的憑證。在具有 Lync 伺服器和整合通訊的環境 中，利用下列指南部署信任的憑證：

  - 在您的 Lync 伺服器、用戶端存取伺服器、信箱伺服器 CA、中繼伺服器和媒體閘道器匯入由私人或公開 CA 所簽署的有效憑證。這個憑證必須是受信任的協力廠商商業憑證或是公開金鑰基礎結構 (PKI) 憑證。

  - 匯入每一個 Exchange 伺服器的憑證若是同一個協力廠商商業憑證或 PKI 憑證，則可降低複雜度。同時，請在每一台執行 Microsoft Lync Server 和中繼伺服器的電腦上安裝此一受信任憑證。這不僅會讓您在部署憑證時問題較少，同時可減少部署憑證時的管理負擔。不過，您必須取得支援主體別名 (SAN) 的信任憑證。
    
    當您使用 UM 部署傳輸層安全性 (TLS) 時，用戶端伺服器和信箱伺服器兩者所使用的憑證都必須在憑證的主體名稱中包含本機電腦的完整網域名稱 (FQDN)。若要解決此問題，請使用公開憑證並在所有用戶端存取和信箱伺服器、任何 VoIP 閘道器、IP PBX 和所有 Lync 伺服器上匯入憑證。
    
    如果您的部署含有 VoIP 閘道器或 IP PBX，而且如果您使用 SIP 安全或安全撥號對應表，用戶端存取和信箱伺服器以及 VoIP 閘道器或 IP PBX 之間都必須使用信任憑證。如果使用直接 (SIP) 連線，則也需要信任憑證。如果您使用 SIP 安全或安全撥號對應表，您可以在 Lync 和 Exchange 伺服器上使用與 VoIP 閘道器或 IP PBX 同一個信任憑證。

  - 連接 Exchange 用戶端存取與 Mailbox 伺服器至 Microsoft Lync 伺服器或是第三方 SIP 閘道或專用交換機 (PBX) 電話設備時，您必須使用有效並且由內部或公用、第三方認證單位 (CA) 所簽署的認證。只要憑證的 SAN 清單中具有所有用戶端存取和信箱伺服器的 FQDN，您就可以在所有用戶端存取和信箱伺服器上使用單一憑證。或者，您可使用該伺服器主體一般名稱 (CN) 或憑證的 SAN 清單中出現的本機電腦 FQDN，為每一個用戶端存取和信箱伺服器產生不同的憑證。Exchange UM 不支援 Microsoft Lync Server 使用萬用字元憑證。
    
    Lync 伺服器和 Exchange 若要一同使用，就必須使用非萬用字元主體名稱。UM 和 Lync 伺服器指出信任 SIP 同儕節點的方式就是使用主體名稱。Lync 伺服器還需要在某些電話轉接方案中使用非萬用字元主題名稱。FQDN 必須作為 \[發行給\] 的值使用。
    
    對於 Exchange UM，不支援在 \[憑證名稱\] 中放置萬用字元。但是，您可以在 SAN 中放置萬用字元。

下表顯示安裝和設定 Exchange UM 憑證的憑證要求。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>拓撲</th>
<th>憑證設定</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>同一個伺服器 (沒有 Lync 2010 或 2013；非 SIP 撥號對應表) 上的用戶端存取和信箱</p></td>
<td><p>用戶端存取和信箱伺服器之間需要憑證。這個憑證與用戶端存取和信箱伺服器以及 VoIP 閘道器、IP PBX 或 SBC 之間所用的憑證相同。</p></td>
</tr>
<tr class="even">
<td><p>不同伺服器 (沒有 Lync 2010 或 2013；非 SIP 撥號對應表) 上的用戶端存取和信箱</p></td>
<td><p>需要憑證。用戶端存取和信箱伺服器上的憑證必須相符。用戶端存取和信箱伺服器以及 VoIP 閘道器、IP PBX 或 SBC 之間也需要憑證。這個憑證可以和用戶端和信箱伺服器之間所有的憑證相同或不同。對於用戶端存取和信箱伺服器，您可從這兩個伺服器任何一個執行 <strong>Create-ExchangeCertificate</strong> Cmdlet。</p></td>
</tr>
<tr class="odd">
<td><p>同一個伺服器 (有 Lync 2010 或 2013 和 SIP 撥號對應表) 上的用戶端存取和信箱</p></td>
<td><p>需要憑證。用戶端存取和信箱伺服器必須具備相同的根憑證為 Lync 2010 或 2013年伺服器。</p></td>
</tr>
<tr class="even">
<td><p>不同伺服器 (有 Lync 2010 或 2013 和 SIP 撥號對應表) 上的用戶端存取和信箱</p></td>
<td><p>憑證是必要項目。用戶端存取和信箱伺服器必須具備相同的根憑證為 Lync 2010 或 2013年伺服器。</p></td>
</tr>
</tbody>
</table>


回到頁首

## 部署步驟

在組織中安裝需要的伺服器後，建議您在部署 Exchange 整合通訊和 Lync 伺服器時執行後續步驟，以更正使用者所部署的 Enterprise Voice。

如需有關 Microsoft Lync Server 的詳細資訊，請參閱[Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752)。

您必須完成以下步驟，才能在 Lync 伺服器中設定整合通訊與 Enterprise Voice 功能一同使用：

1.  建立一或多個整合通訊 SIP URI 撥號對應表，各對應至相對應的 Lync 伺服器位置設定檔。您必須為每個 Exchange UM 撥號對應表各建立一個 Enterprise Voice 位置設定檔。您可以使用 **Get-UMDialPlan** Cmdlet 來取得 SIP URI 撥號對應表的 FQDN。如需如何建立 SIP URI 撥號對應表的詳細資訊，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您已經整合了 Exchange UM 與 Lync 伺服器，可能會發現不必在 Exchange UM 中設定撥號規則或撥號規則群組。Lync 伺服器的設計是要為您組織中的使用者執行電話轉接和號碼轉譯，若是由整合通訊代替使用者打電話，也會執行此動作。</td>
    </tr>
    </tbody>
    </table>


2.  在用戶端存取和信箱伺服器上安裝私人或公開 CA 所簽署的有效憑證。這個憑證與 Lync 伺服器所使用的 CA 相同。

3.  藉由將 SIP URI 撥號對應表設定為 \[SIP 安全\] 或 \[安全\]，對 Voice over IP (VoIP) 流量進行加密。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您將安全性設定設定為 [SIP 安全]，以要求僅 SIP 流量加密，當前端集區設定為需要加密 (表示 SIP 和 RTP 流量的集區都需要加密) 時，此撥號對應表上的設定將不足。當撥號對應表和集區安全性設定不相容時，所有從前端集區撥號給 Exchange UM 的來電都將失敗，導致出現一個您有「不相容安全性設定」的錯誤。</td>
    </tr>
    </tbody>
    </table>
    
    雖然 UM 撥號對應表可設定為 \[SIP 安全\] 或 \[安全\]，但建議您將撥號對應表設定為 \[安全\]，讓 Lync Phone Edition 裝置可以正確運作。由於 Lync 伺服器中設定了預設的加密等級設定，所以建議您這麼做。只有在依照下表所示內容設定加密設定後，Lync Phone Edition 裝置才能運作。此表格會顯示 Lync 伺服器與 UM 撥號對應表之間加密設定的關係。
    
    **Lync Phone Edition 的加密設定**
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Lync 伺服器</th>
    <th>UM 撥號對應表</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>需要加密 (預設)</p></td>
    <td><p>安全</p></td>
    </tr>
    <tr class="even">
    <td><p>加密選擇性</p></td>
    <td><p>SIP 安全/安全</p></td>
    </tr>
    <tr class="odd">
    <td><p>未加密</p></td>
    <td><p>SIP 安全</p></td>
    </tr>
    </tbody>
    </table>


4.  將所有的用戶端存取和信箱伺服器新增到 SIP 撥號對應表。若要啟用伺服器接聽來電，您必須將所有 Exchange 伺服器新增到撥號對應表，才能讓 Exchange 伺服器接聽 Lync 伺服器的來電。

5.  在 SIP URI 撥號對應表所新增的用戶端存取和信箱伺服器上將 TLS 接聽連接埠的啟動模式設定為 \[雙重\]，然後重新啟動每一個信箱伺服器上的 MicrosoftExchange 整合通訊以及每一個用戶端存取伺服器上的 MicrosoftExchange 整合通訊呼叫路由器服務。

6.  建立並設定 UM 自動語音應答。如需詳細資訊，請參閱[設定 UM 自動語音應答](set-up-a-um-auto-attendant-exchange-2013-help.md)。

7.  當您啟用使用者的語音郵件時，請為使用 Enterprise Voice 的使用者建立一個 SIP 位址。大部分情況下，此 SIP 位址與使用者啟用 Enterprise Voice 時所用的 SIP 位址一樣。如需詳細資訊，請參閱[啟用使用者的語音信箱](enable-a-user-for-voice-mail-exchange-2013-help.md)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>與 SIP URI 撥號對應表相關聯的使用者無法接收傳入的傳真。這是因為內送的語音和傳真呼叫會透過中繼伺服器來路由傳送，而在使用中繼伺服器時，不支援傳真功能。</td>
    </tr>
    </tbody>
    </table>


8.  開啟 Exchange 管理命令介面，並執行位在 %Program Files%\\Microsoft\\Exchange Server\\V15\\Scripts 資料夾中的 exchucutil.ps1 指令碼。exchucutil.ps1 指令碼可執行下列作業：
    
      - 授與 Lync Server 權限以讀取Exchange UM Active Directory元件，尤其是在之前的工作中所建立的 SIP URI 撥號。如需詳細資訊如何在Active Directory中設定權限，查看[如何將使用 ADSI Edit 來套用權限](https://go.microsoft.com/fwlink/p/?linkid=82751)。
    
      - 針對每個 Lync 伺服器集區，或是每部執行 Lync Server Standard Edition 的伺服器 (主控已啟用 Enterprise Voice 功能的使用者) 建立一個 UM IP 閘道器。如需詳細資訊，請參閱[建立 UM IP 閘道器](create-a-um-ip-gateway-exchange-2013-help.md)。
    
      - 為每個 UM IP 閘道器建立一個 Exchange UM 群組搜尋。此群組搜尋引導識別碼就是播號對應表中與對應的 UM IP 閘道器相關聯的名稱。群組搜尋必須指定與 UM IP 閘道器一起使用的 UM SIP 撥號對應表。

9.  啟用使用者的語音信箱。當您啟用語音信箱時，請確認您已在 SIP 撥號對應表中輸入使用者有效的 SIP 位址和連結。如需詳細資訊，請參閱[啟用使用者的語音信箱](enable-a-user-for-voice-mail-exchange-2013-help.md)。

您同時必須完成下列工作來設定 Lync 伺服器，以使用 Exchange UM：

  - 建立位置設定檔或 Lync 撥號對應表。位置設定檔名稱不必符合對應的 UM 撥號對應表的 FQDN。

  - 將位置設定檔指派給 Lync 伺服器集區。

  - 部署及設定媒體閘道器或中繼伺服器。您也必須將用戶端存取和信箱伺服器及 Lync 伺服器上所用的同一個信任 CA 憑證匯入。

  - 定義電話用法、建立和指派語音原則及輸出呼叫路由。

  - 設定使用者的 Enterprise Voice 並新增 TEL URI 和 SIP 識別碼。

  - 執行 **ocsumutil.exe**，以建立 Outlook Voice Access 和自動語音應答的連絡人物件。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>安裝 Lync 伺服器時，<strong>msRTC-SIPLine</strong> 屬性會新增至 Active Directory。如果您尚未在環境中安裝 Lync 伺服器，則不會將此屬性新增至 Active Directory，同時，除非針對未啟用 UM 的使用者設定整合通訊 Proxy 位址，否則單一樹系和跨樹系情況中，跨撥號對應表的來電者識別碼名稱解析將無法正確運作。</td>
    </tr>
    </tbody>
    </table>


設定好 Lync 伺服器和整合通訊伺服器之後，您必須讓使用者能夠使用 Lync 伺服器，以及將 Lync 伺服器安裝在使用者的用戶端電腦上。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您在整合整合通訊與 Lync 伺服器時，信箱位於 Exchange 2007 或 Exchange 2010 信箱伺服器上的使用者無法使用未接來電通知。未接來電通知需於使用者在來電尚未傳送給信箱伺服器前中斷連接才可產生。</td>
</tr>
</tbody>
</table>


回到頁首

## 相關資訊

如需如何執行 Microsoft Lync Server 必須完成的工作的詳細資訊，請參閱[Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752)。

