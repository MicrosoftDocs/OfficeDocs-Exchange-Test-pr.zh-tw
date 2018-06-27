---
title: 'Exchange 2013 的電話語音 advisor: Exchange Online Help'
TOCTitle: Exchange 2013 的電話語音 advisor
ms:assetid: e9f760f2-5901-4ed2-95a5-724555cc700e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee364753(v=EXCHG.150)
ms:contentKeyID: 50554076
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013 的電話語音 advisor

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2017-07-25_

整合通訊 (UM) 需要與現有的電話系統整合 Microsoft Exchange，您的組織。成功部署需要您以讓您現有的電話語音基礎結構的小心分析和執行部署整合通訊的正確規劃步驟。

規劃階段可以為Exchange管理員已經少或沒有使用的電話語音網路大幅挑戰。為了處理這個挑戰，請參閱本主題稍後的資源以協助您部署 UM 。

若要查看支援的 VoIP 閘道的整合通訊，判斷是否 PBX 支援使用特定的 VoIP 閘道模型或製造商、 是否將 IP PBX 支援使用直接 SIP 連線，或以查看支援工作階段邊界控制器 （Sbc) 的Exchange Online UM，按一下下列連結之一：

  - 支援的 VoIP 閘道器

  - 支援的 pbx 設定時使用 AudioCodes VoIP 閘道

  - 使用 dialogic VoIP 閘道時，支援 Pbx
    
      - Pbx 時使用 DMG1000 系列媒體閘道支援
    
      - Pbx 時使用殺傷力 2000年系列媒體閘道支援
    
      - Pbx 時使用 DMG3000 系列媒體閘道支援

  - 支援的 IP Pbx

  - 使用 SIP 媒體閘道時，支援 IP Pbx

  - Exchange 整合通訊、 Office Communications Server 2007 R2 和 Microsoft Lync Server

## 資源以協助您的 UM 部署

它具挑戰性建立部署電話語音網路的指導方針。因為他們可以使用不同的組態設定、 韌體和需求包括 VoIP 閘道、 IP Pbx 和 Pbx，他們可以與彼此非常不同。不過，多個資源是可用來協助您順利部署整合通訊：

  - **整合通訊專家**UM 專家是系統整合者會收到有關 Exchange 整合通訊Exchange工程小組所進行的技術訓練人員。若要確保順利地轉換至 \[整合通訊從舊版的語音信箱系統， Microsoft建議所有客戶都參與 UM 專家。連絡人資訊，請造訪[Microsoft Exchange Server 2013 整合通訊 (UM) 專家](http://go.microsoft.com/fwlink/p/?linkid=262708)或[整合通訊的 Microsoft Pinpoint](https://go.microsoft.com/fwlink/p/?linkid=261951)。

  - **組態注意事項支援的 VoIP 閘道、 IP Pbx 與 Pbx**  這些組態注意事項包含設定及時很有幫助您正在設定 VoIP 閘道、 IP Pbx 及進行通訊的 Pbx 與您的網路上的整合通訊伺服器的其他資訊。如需詳細資訊，請參閱[支援 VoIP 閘道、 IP Pbx 和 Pbx 組態注意事項](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)。

  - **為支援工作階段邊界控制器組態注意事項**  這些組態注意事項包含設定及時很有幫助您正在設定工作階段邊界控制器 (Sbc) 與整合通訊伺服器通訊的混合式部署和Exchange Online UM 部署的其他資訊。如需詳細資訊，請參閱[支援工作階段邊界控制器的組態注意事項](configuration-notes-for-supported-session-border-controllers-exchange-2013-help.md)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Exchange Online UM 支援透過直接從客戶 21vianet Sbc 連線協力廠商 PBX 系統將會結束年 7 月 2018年中。 請參閱 Exchange 團隊部落格<a href="https://blogs.technet.microsoft.com/exchange/2017/07/18/discontinuation-of-support-for-session-border-controllers-in-exchange-online-unified-messaging/">主題的 Exchange Online 中的工作階段邊界控制器支援的整合通訊</a>如需詳細資訊。</td>
    </tr>
    </tbody>
    </table>


連絡整合通訊專家之前，您應該能夠回答他們將要求的重要問題。有下列問題的答案有助於讓您與 UM 專家之間的對話提高工作效率：

  - 多少現有電話、 語音郵件使用者，或兩者位於您組織中吗？

  - 您想要提供整合通訊多少使用者？

  - 您要用於與整合通訊整合的 PBX 或 Pbx？

  - 您的組織有多少 Pbx？指定廠商、 類型 （電路或 IP-型）、 模型與韌體版本。

  - Pbx 網路，以及它們集中式或位於多個位置吗？

  - 目標語音郵件系統沒有組織目前所使用？指定廠商、 類型、 模型與韌體版本。

  - 如何部署語音信箱系統整合至您的 Pbx (類比、 T1/E1、 PRI、 數位設定模擬、 VoIP 其他)？

  - 您目前使用語音網路吗？

  - 貴組織是否使用何種類型的傳真系統或系統，以及確實傳真系統支援輸入的傳真路由傳送至Exchange？

  - 您的組織是否使用自動語音應答吗？

  - 是否您需要支援僅限電話的使用者，也就是不具有電子郵件使用者？

## 支援的 VoIP 閘道器

含有 Pbx 整合 Unified Messaging 需要使用一或多個 VoIP 閘道翻譯 TDM 型 pbx 設定為使用整合通訊的 IP 型、 封包切換通訊協定所使用的電路切換型通訊協定。支援的整合通訊與已測試 VoIP 閘道廠商與數個模型的 VoIP 和媒體閘道。

現在已與Microsoft Unified Communications 開啟互通性計劃與 VoIP 閘道、 IP Pbx 和 Sbc 的整合通訊互通性測試。如需詳細資訊，請參閱[Microsoft Unified Communications 開啟互通性計劃](http://go.microsoft.com/fwlink/p/?linkid=140722)。

[Microsoft Unified Communications 開啟互通性計劃](http://go.microsoft.com/fwlink/p/?linkid=140722)限定程式 VoIP 閘道、 IP Pbx 及進階的 VoIP 閘道可確保客戶有一致的安裝程式和體驗時的支援他們使用完整的電話語音 VoIP 閘道器、 IP Pbx 與Microsoft整合通訊軟體。符合嚴格且廣泛測試需求並符合的規格及測試計劃產品收到完整名稱。

如需設定支援 VoIP 閘道、 IP Pbx、 Pbx 和 Sbc 的詳細資訊，請參閱下列資源：

  - [支援 VoIP 閘道、 IP Pbx 和 Pbx 組態注意事項](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)

  - [支援工作階段邊界控制器的組態注意事項](configuration-notes-for-supported-session-border-controllers-exchange-2013-help.md)

下列的 VoIP 閘道廠商已驗證的互通性：

  - AudioCodes

  - Dialogic

  - 下表顯示 VoIP 閘道廠商、 VoIP 閘道模型和每個模型所支援的通訊協定。

### 支援的 VoIP 閘道的整合通訊

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>廠商</th>
<th>機型</th>
<th>支援的通訊協定</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AudioCodes</p></td>
<td><p>MediaPack 114/8 FXO</p></td>
<td><ul>
<li><p>使用頻內 DTMF 類比</p></li>
<li><p>使用 SMDI 類比</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000</p></td>
<td><ul>
<li><p>使用頻內 DTMF 類比</p></li>
<li><p>使用 SMDI 類比</p></li>
<li><p>BRI Q.SIG</p></li>
<li><p>T1/E1 Q.SIG</p></li>
<li><p>IP-IP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><ul>
<li><p>T1/E1 CAS</p></li>
<li><p>T1/E1 Q.SIG</p></li>
<li><p>IP-IP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Dialogic</p></td>
<td><p>DMG1000PBXDNIW</p></td>
<td><p>數位組模擬</p></td>
</tr>
<tr class="odd">
<td><p>Dialogic</p></td>
<td><p>DMG1000LSW</p></td>
<td><ul>
<li><p>使用頻內 DTMF 類比</p></li>
<li><p>使用 SMDI 類比</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Dialogic</p></td>
<td><p>DMG2000</p></td>
<td><ul>
<li><p>T1 CAS</p></li>
<li><p>T1/E1 Q.SIG</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Dialogic</p></td>
<td><p>DMG3000</p></td>
<td><ul>
<li><p>BRI Q.SIG</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>NET</p></td>
<td><p>VX1200</p></td>
<td><ul>
<li><p>T1 Q.SIG</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Sonus</p></td>
<td><p>SBC 1000/2000 2.2.1 或更新版本</p></td>
<td><ul>
<li><p>TDM 訊號 (ISDN): 在 &amp; T 4ESS/5ESS、 規則 DMS 100、 歐元 ISDN （以 300 102）、 QSIG、 NTT InsNet （日本）、 ANSI 國民 ISDN-2 (NI-2)</p></li>
<li><p>TDM 訊號 (CAS)： T1 CAS (E &amp; M、 迴圈開始); E1 CAS (R2)</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Quintum</p></td>
<td><p>Tenor DX 系列</p></td>
<td><ul>
<li><p>T1 Q.SIG</p></li>
</ul></td>
</tr>
</tbody>
</table>


## 支援的 pbx 設定時使用 AudioCodes VoIP 閘道

下表顯示支援使用 AudioCodes VoIP 閘道器，包括 MediaPack 114 FXO、 MediaPack 118 FXO 及 Mediant 2000 Pbx。

### Pbx 與 AudioCodes VoIP 閘道支援

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 製造商</th>
<th>PBX 模型/類型</th>
<th>AudioCodes 模型&quot;x&quot;-4 或 8 個需要&quot;y&quot;以取代-取代為 1、 2、 4、 8 或需要在每個 16</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Alcatel</p></td>
<td><p>OmniPCX 4400</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Aastra</p></td>
<td><p>M1000、 M2000</p></td>
<td><ul>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>具體 G3</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Avaya</p></td>
<td><p>Magix/Merlin</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>S8300</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Avaya</p></td>
<td><p>S8700</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>IP Office</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Cisco</p></td>
<td><p>CallManager 4.x</p></td>
<td><ul>
<li><p>Mediant1000/IP 至-IP</p></li>
<li><p>Mediant2000/IP 至-IP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>NEC</p></td>
<td><p>Electra 精銳</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>NEC</p></td>
<td><p>NEAX2400</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
<li><p>Mediant2000/ySpans/SIP/RS232</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>NeXspan</p></td>
<td><p>S</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>規則</p></td>
<td><p>通訊伺服器-1000 M、 1000S、 1000E</p></td>
<td><ul>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>規則</p></td>
<td><p>Meridian 11 c 51 c、 61 c、 81 c</p></td>
<td><ul>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Panasonic</p></td>
<td><p>KX-KX TEA308 TES824</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Panasonic</p></td>
<td><p>KX-KX-TDA100 TDA30 KX TDA200、 KX TDA600</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Shortel</p></td>
<td><p>IP 電話系統</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiCom 150E</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiPath 3550</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiPath 4000</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Tadiran 電信</p></td>
<td><p>珊瑚紅 Flexicom、 珊瑚紅 IPX</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
</tbody>
</table>


## 支援的 pbx 設定時使用 Dialogic VoIP 閘道

每個 Dialogic VoIP 閘道模型支援不同的 Pbx。下列資料表顯示 PBX 製造商及模型和可以用哪些 Dialogic VoIP 閘道。每個 VoIP 閘道使用不同的訊號方法、 密度、 和通訊協定。

## Pbx 時使用 DMG1000 系列媒體閘道支援

下表顯示支援與低 Dialogic 媒體閘道 (DMG1000) Pbx。不過，類比 DMG1000 使用時，補充訊號 (RS232 SMDI、 MD110、 MCI 通訊協定或 Inband DTMF 訊號)，則需要。

### Pbx 時使用低 Dialogic DMG1000 數列 VoIP 閘道支援

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 製造商</th>
<th>PBX 模型/類型</th>
<th>殺傷力模型及其他訊號</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Aastra</p></td>
<td><p>Aastra MD110 (前身為易利信行動 MD110)</p></td>
<td><p>DMG1008LSW</p>
<p>使用 MD110 RS232 通訊協定的類比連線</p></td>
</tr>
<tr class="even">
<td><p>Alcatel</p></td>
<td><p>通用 PCX 4400</p></td>
<td><p>DMG1008LSW</p></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>具體 G3 S8100、 S8300、 S8700 及 S8710 （通訊管理員 SW 2.0 版或更新版本）</p></td>
<td><p>DMG1008DNIW</p></td>
</tr>
<tr class="even">
<td><p>交互通訊</p></td>
<td><p></p></td>
<td><p>DMG1008LSW</p>
<p>使用 SMDI 序列通訊協定的類比連線</p></td>
</tr>
<tr class="odd">
<td><p>Mitel</p></td>
<td><p>SX-200 D、 SX 200 淺、 SX 2000 淺、 SX 2000 S、 SX 2000 VS SX 200 ICP</p></td>
<td><p>DMG1008MTLDNIW</p></td>
</tr>
<tr class="even">
<td><p>NEC</p></td>
<td><p>2000、 2400、 2400 IPX</p></td>
<td><p>DMG1008DNIW</p></td>
</tr>
<tr class="odd">
<td><p>規則</p></td>
<td><p>Meridian 1-選項 11、 21、 21A、 51、 61、 71、 及 81</p>
<p>Meridian SL1-一般 X11 版本 15 或更新版本</p>
<p>規則 Communication Server-1000 M、 1000S、 1000E V3.0 或更新版本</p></td>
<td><p>DMG1008DNIW</p></td>
</tr>
<tr class="even">
<td><p>規則</p></td>
<td><p>SL 100</p></td>
<td><p>DMG1008LSW</p>
<p>使用 SMDI 序列通訊協定的類比連線</p></td>
</tr>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiCom 300E CS</p></td>
<td><p>DMG1008DNIW</p></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiCom 300E （歐洲）</p></td>
<td><p>DMG1008LSW</p>
<p>使用 Inband DTMF 訊號類比連線</p></td>
</tr>
<tr class="odd">
<td><p>Siemens/ROLM</p></td>
<td><p>8000 （西南指向版本 80003 或更新版本）<br />
9000 （所有版本）</p>
<p>9751 （所有版本的 SW 都版本 9005）</p>
<p>9751 （西南指向版本 9006.4 或更新版本）</p></td>
<td><p>DMG1008RLMDNIW</p></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiPath 4000</p></td>
<td><p>DMG1008LSW</p></td>
</tr>
<tr class="odd">
<td><p>地區</p></td>
<td><p>CTX （西南指向版本 AR1ME021.00）</p></td>
<td><p>DMG1008LSW</p></td>
</tr>
<tr class="even">
<td><p>其他人</p></td>
<td><p>各種</p></td>
<td><p>DMG1008LSW</p>
<p>使用 Inband DTMF 或 SMDI 類比連線</p></td>
</tr>
</tbody>
</table>


## Pbx 時使用殺傷力 2000年系列媒體閘道支援

下表顯示支援使用 T1/E1 Dialogic 媒體閘道 (DMG2000) Pbx。在單一範圍 (DMG2030DTIQ) 而言，\[DMG2000 閘道，雙跨 (DMG2060DTIQ)，或四跨越 (DMG2120DTIQ) 密度、 支援下列通訊協定：

  - T1 CAS

  - T1 Q.SIG

  - E1 Q.SIG

  - T1 NI-2

  - T1 5ESS

  - T1 DMS100

如果使用訊號通道相關聯訊號 (CAS) 時，補充訊號 (RS232 SMDI、 MD110、 MCI 通訊協定或 Inband DTMF 訊號)，則需要。如果使用 Q.SIG 訊號，PBX 必須支援的補充服務相關聯呼叫並呼叫方資訊和通話傳輸整合通訊所需的功能。

### Pbx 與 DMG2000 媒體閘道支援

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 製造商</th>
<th>PBX 模型/類型</th>
<th>必要的軟體版本</th>
<th>通訊協定及其他訊號</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Alcatel</p></td>
<td><p>通用 PCX 4400</p></td>
<td><p>版本 3.2.712.5</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Avaya</p></td>
<td><p>具體 G3</p></td>
<td><p>3 或更新版本</p></td>
<td><p>T1 CAS</p></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>S8500</p></td>
<td><p>管理員 SW 2.0 版或更新版本</p></td>
<td><p>T1 CAS</p>
<p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>易利信行動</p></td>
<td><p>MD110</p></td>
<td><p>釋出 MX1 TSW R2A (BC13)</p></td>
<td><p>E1 Q.SIG</p></td>
</tr>
<tr class="odd">
<td><p>交互通訊</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>CAS （具有 SMDI 序列通訊協定）</p></td>
</tr>
<tr class="even">
<td><p>NEC</p></td>
<td><p>2400 /IMX</p></td>
<td><p>釋出 5200 年 12 月 92年 1b 或更新版本</p></td>
<td><p>CAS （具有 MCI 序列通訊協定）</p></td>
</tr>
<tr class="odd">
<td><p>NEC</p></td>
<td><p>2400 IPX</p></td>
<td><p>R17 版本 03.46.001</p></td>
<td><p>T1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>規則</p></td>
<td><p>Meridian 1-選項 11</p></td>
<td><p>版本 15 或更新版本、 和選項 19 46 所需</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="odd">
<td><p>規則</p></td>
<td><p>Communication Server 1000</p></td>
<td><p>版本 2121、 版本 4</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiCom 300E CS</p></td>
<td><p>版本 9006.4 或更新版本 (請注意： 僅 North American 軟體負載)</p></td>
<td><p>T1 CAS</p></td>
</tr>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiPath 4000</p></td>
<td><p>V2 SMR 9 SMPO</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Mitel</p></td>
<td><p>SX 2000 S、 SX 2000 VS</p></td>
<td><p>LW 34</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="odd">
<td><p>Mitel</p></td>
<td><p>3300</p></td>
<td><p>版本 5.1.4.8</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
</tbody>
</table>


## Pbx 時使用 DMG4008BRI 系列媒體閘道支援

媒體閘道隨附數個 TDM 介面選項 DMG4000 數列。DMG4008BRI 支援 4 連接埠/8 通道密度還可支援下列通訊協定：

  - ISDN BRI Q.SIG

  - 以 DSS1 (歐元 ISDN)

  - NET 3 （比利時）

  - VN3 （法國）

  - 1TR6 （德國）

  - 集 64 （日本）

  - 5ESS 自訂 （北美洲-AT & T）

  - 國際 ISDN (NI1-「 北美地區 」)

下表顯示支援使用 Dialogic 4000 媒體閘道數列 (DMG4008) Pbx。

### 支援使用 DMG4008BRI 媒體閘道的 Pbx

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 製造商</th>
<th>PBX 模型/類型</th>
<th>必要的軟體版本</th>
<th>通訊協定及其他訊號</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiCom 300</p></td>
<td><p>SA300-V3.05</p></td>
<td><p>BRI-Q。簽章 (ECMAV2)</p></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiPath 4000</p></td>
<td><p>S.0 B4400</p></td>
<td><p>BRI-Q。簽章 (ECMAV2)</p></td>
</tr>
</tbody>
</table>


## 支援的 IP Pbx

由整合通訊也支援 IP Pbx。下表顯示支援使用直接 SIP 連線至 \[整合通訊 IP Pbx。

### 支援使用直接 SIP 連線時的 IP Pbx

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 製造商</th>
<th>PBX 模型/類型</th>
<th>必要的軟體版本</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Aastra</p></td>
<td><p>MX 一</p></td>
<td><p>4.0</p></td>
</tr>
<tr class="even">
<td><p>Avaya</p></td>
<td><p>靈氣</p></td>
<td><p>5.2.1 含 Service Pack 5 (SP5)</p></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>Communication Server 2100</p></td>
<td><p>CS2100 SE13</p></td>
</tr>
<tr class="even">
<td><p>Cisco</p></td>
<td><p>呼叫管理員] 中，整合的通訊管理員</p></td>
<td><p>5.1, 6.x, 7.0 and8.0</p></td>
</tr>
</tbody>
</table>


## 支援時使用 SIP 媒體閘道的 IP Pbx

使用 SIP 媒體閘道也支援由整合通訊 IP Pbx。下表顯示支援使用 IP 功能 SIP 媒體閘道的 IP 連線至整合通訊 IP Pbx。

### 支援時使用的 SIP 媒體閘道的 IP Pbx

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 製造商</th>
<th>PBX 模型/類型</th>
<th>SIP 閘道模型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cisco</p></td>
<td><p>呼叫管理員 4.x</p></td>
<td><p>AudioCodes Mediant 1000/2000 (IP-至-啟用 IP)</p></td>
</tr>
</tbody>
</table>


## Exchange 整合通訊、 Office Communications Server 2007 R2 和 Microsoft Lync Server

內部部署和混合式 Exchange 整合通訊的部署可以搭配Microsoft Office Communications Server 2007 R2 Microsoft Lync Server 2010 或 Lync Server 2013 提供語音訊息、 立即訊息 (IM)、 部署增強的使用者顯示狀態、 音訊視訊會議和整合式電子郵件及訊息為在組織中的使用者經驗。如需詳細資訊，請參閱：

  - [部署 Exchange 2013 UM 和 Lync Server 概觀 （英文）](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md)

  - [Microsoft Lync Server 2013](https://go.microsoft.com/fwlink/p/?linkid=202010)

若要了解更多有關 Microsoft Unified Communications 開啟互通性計劃企業電話語音基礎結構，包括尋找完整 SIP PSTN 閘道與 IP Pbx 及程序的電話語音基礎結構廠商加入與參與計畫，請參閱[Microsoft Unified Communications 開啟互通性計劃](https://go.microsoft.com/fwlink/p/?linkid=132071)。

