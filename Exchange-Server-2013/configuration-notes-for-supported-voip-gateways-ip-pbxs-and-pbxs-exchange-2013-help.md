---
title: '支援 VoIP 閘道、 IP Pbx 和 Pbx 組態注意事項: Exchange Online Help'
TOCTitle: 支援 VoIP 閘道、 IP Pbx 和 Pbx 組態注意事項
ms:assetid: 1583674f-5a57-45fd-8125-087d1624e686
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee681657(v=EXCHG.150)
ms:contentKeyID: 50553939
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 支援 VoIP 閘道、 IP Pbx 和 Pbx 組態注意事項

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2016-12-09_

此頁面提供組態注意事項建立及測試Microsoft或 VoIP 閘道協力廠商的連結。Microsoft或協力廠商部署整合通訊與新的 VoIP 閘道及 PBX 或 IP PBX 組態，都記載的先決條件和組態設定。此資訊用來建立組態注意事項。

每個 PBX 組態注意事項包含如何部署整合通訊與特定的電話語音設定的相關資訊及包含製造商、 模型和 VoIP 閘道、 IP Pbx 或 Pbx 的韌體版本。此外，每個 PBX 組態注意事項包含其他資訊，例如：

  - 在製作組態注意事項參與者。

  - 詳細的先決條件，包括下列各項：
    
      - 必須啟用或停用在 PBX 上的功能。
    
      - 已安裝的特定的硬體。
    
      - 是否需要 VoIP 閘道。
    
      - 必須存在於上的 VoIP 閘道，如果其中所需的功能。
    
      - IP 閘道和 PBX 間的特定纜線需求。
    
      - 可能會無法與指定的電話語音設定整合通訊功能的清單。

若要了解更多關於Microsoft Unified Communications 開啟互通性程式 enterprise 電話語音基礎結構需求，包括尋找完整的 SIP PSTN 閘道與 IP Pbx 與程序的電話語音基礎結構廠商可用來加入並參與計畫，請參閱[Microsoft Unified Communications 開啟互通性計劃](https://go.microsoft.com/fwlink/p/?linkid=132071)。

## VoIP 閘道、 IP PBX 和 PBX 組態注意事項

Microsoft運作與 VoIP 閘道協力廠商，AudioCodes 與 Dialogic，可新增至所測試的 Pbx 的清單。因為我們目前要測試的電話語音元件的許多組合，本主題會經常更新。請檢查回若您找不到適當的組態注意事項為您的部署。

可用的下列組態注意事項如下：


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Aastra</p></li>
<li><p>Alcatel</p></li>
<li><p>Avaya</p></li>
<li><p>Cisco</p></li>
<li><p>間 Tel</p></li>
<li><p>Intecom</p></li>
<li><p>Mitel</p></li>
<li><p>NEC</p></li>
</ul></td>
<td><ul>
<li><p>NeXspan</p></li>
<li><p>規則</p></li>
<li><p>Panasonic</p></li>
<li><p>Rolm</p></li>
<li><p>ShoreTel</p></li>
<li><p>Siemens</p></li>
<li><p>Sonus</p></li>
<li><p>Tadiran</p></li>
<li><p>地區</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Aastra


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 模型</th>
<th>PBX 軟體版本</th>
<th>通訊協定</th>
<th>閘道廠商</th>
<th>閘道模型</th>
<th>設定作者</th>
<th>設定檔案下載 （英文）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Aastra MD110 (前身為易利信行動 MD110)</p></td>
<td><p>MX1 TSW R2A (亦即 BC13)</p></td>
<td><p>類比 – 序列 MD110</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008LSW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下載</a></p></td>
</tr>
<tr class="even">
<td><p>Aastra MD110 (前身為易利信行動 MD110)</p></td>
<td><p>MX1 TSW R2A (亦即 BC13)</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下載</a></p></td>
</tr>
<tr class="odd">
<td><p>Aastra MX 對一</p></td>
<td><p>4.0</p></td>
<td><p>直接 SIP 連線</p></td>
<td><p>N.A.</p></td>
<td><p>N.A.</p></td>
<td><p>Aastra</p></td>
<td><p><a href="http://www.aastra.com/cps/rde/aareddownload?file_id=4384-14746-_p06_xml%26dsproject=aastra%26mtype=pdf">下載</a></p></td>
</tr>
</tbody>
</table>


## Alcatel


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 模型</th>
<th>PBX 軟體版本</th>
<th>通訊協定</th>
<th>閘道廠商</th>
<th>閘道模型</th>
<th>設定作者</th>
<th>設定檔案下載 （英文）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>OmniPCX 4400</p></td>
<td><p>R4.2-d2.304-4-h-il-c6s2</p></td>
<td><p>類比 – 頻內 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP 11 x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下載</a></p></td>
</tr>
</tbody>
</table>


## Avaya


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 模型</th>
<th>PBX 軟體版本</th>
<th>通訊協定</th>
<th>閘道廠商</th>
<th>閘道模型</th>
<th>設定作者</th>
<th>設定檔案下載 （英文）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>靈氣</p></td>
<td><p>搭配 SP 5 通訊管理員 5.2.1</p>
<p>工作階段管理員 5.2。</p></td>
<td><p>直接 SIP 連線</p></td>
<td><p>N.A.</p></td>
<td><p>N.A.</p></td>
<td><p>Avaya</p></td>
<td><p><a href="https://support.avaya.com/downloads/">下載</a></p></td>
</tr>
<tr class="even">
<td><p>CS 2100</p></td>
<td><p>CS 2100 SE13</p></td>
<td><p>直接 SIP 連線</p></td>
<td><p>N.A.</p></td>
<td><p>N.A.</p></td>
<td><p>Avaya</p></td>
<td><p><a href="https://support.avaya.com/css/p8/documents/100149819">下載</a></p></td>
</tr>
<tr class="odd">
<td><p>具體 G3</p></td>
<td><p>R009i.05.122.4</p></td>
<td><p>數位組模擬 (DNI7434)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008DNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下載</a></p></td>
</tr>
<tr class="even">
<td><p>具體 G3</p></td>
<td><p>R013i.01.1.628.7</p></td>
<td><p>類比 – 頻內 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP 11 x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下載</a></p></td>
</tr>
<tr class="odd">
<td><p>具體 G3</p></td>
<td><p>R013i.01.1.628.7</p></td>
<td><p>T1 CAS – 頻內 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下載</a></p></td>
</tr>
<tr class="even">
<td><p>具體 G3</p></td>
<td><p>R013i.01.1.628.7</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下載</a></p></td>
</tr>
<tr class="odd">
<td><p>具體 G3</p></td>
<td><p>R013i.01.1.628.7</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下載</a></p></td>
</tr>
<tr class="even">
<td><p>Merlin Magix</p></td>
<td><p>版本 1.5 v.6.0</p></td>
<td><p>類比 – 頻內 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP 11 x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下載</a></p></td>
</tr>
<tr class="odd">
<td><p>S8300</p></td>
<td><p>G3xV11 通訊 Manager 1.3</p></td>
<td><p>類比 – 頻內 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP 11 x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下載</a></p></td>
</tr>
<tr class="even">
<td><p>S8300</p></td>
<td><p>R013x.01.2.632.1</p></td>
<td><p>T1 CAS – 頻內 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下載</a></p></td>
</tr>
<tr class="odd">
<td><p>S8300</p></td>
<td><p>R013x.01.2.632.1</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下載</a></p></td>
</tr>
<tr class="even">
<td><p>S8500</p></td>
<td><p>通訊 Manager 3.0 (R013x00.1.346.0)</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下載</a></p></td>
</tr>
<tr class="odd">
<td><p>S8500</p></td>
<td><p>通訊管理員 3.0 (R013x00.1.346.0)</p></td>
<td><p>T1 CAS – 頻內 DTMF</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下載</a></p></td>
</tr>
<tr class="even">
<td><p>S8500</p></td>
<td><p>通訊 Manager 3.0 (R013x00.1.346.0)</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下載</a></p></td>
</tr>
<tr class="odd">
<td><p>S8700</p></td>
<td><p>R011x.02.0.110.4</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下載</a></p></td>
</tr>
</tbody>
</table>


## Cisco


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 模型</th>
<th>PBX 軟體版本</th>
<th>通訊協定</th>
<th>閘道廠商</th>
<th>閘道模型</th>
<th>設定作者</th>
<th>設定檔案下載 （英文）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cisco 通話 Manager 4.x</p></td>
<td><p>4.x</p></td>
<td><p>IP-IP</p></td>
<td><p>AudioCodes</p></td>
<td><p>AudioCodes</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下載</a></p></td>
</tr>
<tr class="even">
<td><p>Cisco 通話 Manager 5.1</p></td>
<td><p>5.1.0.9921-12</p></td>
<td><p>直接 SIP 連線</p></td>
<td><p>N.A.</p></td>
<td><p>N.A.</p></td>
<td><p>Microsoft</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=225083">下載</a></p></td>
</tr>
<tr class="odd">
<td><p>Cisco 整合通訊 Manager 6.0 和 6.1</p></td>
<td><p>6.x</p></td>
<td><p>直接 SIP 連線</p></td>
<td><p>N.A.</p></td>
<td><p>N.A.</p></td>
<td><p>Microsoft</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=225083">下載</a></p></td>
</tr>
<tr class="even">
<td><p>Cisco 整合通訊 Manager 7.0</p></td>
<td><p>7.0.2.20000-5</p></td>
<td><p>直接 SIP 連線</p></td>
<td><p>N.A.</p></td>
<td><p>N.A.</p></td>
<td><p>Microsoft</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=196361">下載</a></p></td>
</tr>
<tr class="odd">
<td><p>Cisco 整合通訊 Manager 8.0</p></td>
<td><p>8.0.3.20000-5</p></td>
<td><p>直接 SIP 連線</p></td>
<td><p>N.A.</p></td>
<td><p>N.A.</p></td>
<td><p>Microsoft</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=213007">下載</a></p></td>
</tr>
</tbody>
</table>


## 間 Tel


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 模型</th>
<th>PBX 軟體版本</th>
<th>通訊協定</th>
<th>閘道廠商</th>
<th>閘道模型</th>
<th>設定作者</th>
<th>設定檔案下載 （英文）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>5000</p></td>
<td><p>間-Tel 5000 空間 v2.1</p></td>
<td><p>T1 CAS – 頻內 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下載</a></p></td>
</tr>
<tr class="even">
<td><p>Axxess</p></td>
<td><p>Axxess V9.0</p></td>
<td><p>T1 CAS – 頻內 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下載</a></p></td>
</tr>
</tbody>
</table>


## Intecom


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 模型</th>
<th>PBX 軟體版本</th>
<th>通訊協定</th>
<th>閘道廠商</th>
<th>閘道模型</th>
<th>設定作者</th>
<th>設定檔案下載 （英文）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PointSpan M6880</p></td>
<td><p>40PS3.5.K.2</p></td>
<td><p>T1 CAS-SMDI</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下載</a></p></td>
</tr>
</tbody>
</table>


## Mitel


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 模型</th>
<th>PBX 軟體版本</th>
<th>通訊協定</th>
<th>閘道廠商</th>
<th>閘道模型</th>
<th>設定作者</th>
<th>設定檔案下載 （英文）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>3300</p></td>
<td><p>5.1.4.8</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下載</a></p></td>
</tr>
<tr class="even">
<td><p>3300</p></td>
<td><p>5.1.4.8</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下載</a></p></td>
</tr>
<tr class="odd">
<td><p>SX2000</p></td>
<td><p>5.0.24</p></td>
<td><p>數位組模擬 (DNISS430)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008MTLDNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下載</a></p></td>
</tr>
<tr class="even">
<td><p>3300</p></td>
<td><p>7</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下載</a></p></td>
</tr>
</tbody>
</table>


## NEC


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 模型</th>
<th>PBX 軟體版本</th>
<th>通訊協定</th>
<th>閘道廠商</th>
<th>閘道模型</th>
<th>設定作者</th>
<th>設定檔案下載 （英文）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Electra 精銳 192</p></td>
<td><p>SP034V4.5</p></td>
<td><p>類比 – 頻內 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP 11 x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下載</a></p></td>
</tr>
<tr class="even">
<td><p>NEAX2400IMX</p></td>
<td><p>版本 7400</p></td>
<td><p>T1 CAS-序列 MCI</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下載</a></p></td>
</tr>
<tr class="odd">
<td><p>NEAX2400IMX &amp; IPX</p></td>
<td><p>版本 7400</p></td>
<td><p>數位組模擬 (DNIDtermIII)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008DNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下載</a></p></td>
</tr>
<tr class="even">
<td><p>NEAX2400IPX</p></td>
<td><p>版本 R18.06.24.000</p></td>
<td><p>T1 CAS – 序列 MCI</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下載</a></p></td>
</tr>
<tr class="odd">
<td><p>NEAX2400IPX</p></td>
<td><p>版本 R18.06.24.000</p></td>
<td><p>類比 – 序列 MCI</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP 11 x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下載</a></p></td>
</tr>
<tr class="even">
<td><p>NEAX2400IPX</p></td>
<td><p>Ver.17 Rel.03.46.001</p></td>
<td><p>T1 Q.SIG – 序列 MCI</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下載</a></p></td>
</tr>
</tbody>
</table>


## NeXspan


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 模型</th>
<th>PBX 軟體版本</th>
<th>通訊協定</th>
<th>閘道廠商</th>
<th>閘道模型</th>
<th>設定作者</th>
<th>設定檔案下載 （英文）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>S</p></td>
<td><p>RMS1 版本 R1.3 E1TA</p></td>
<td><p>類比 – 頻內 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP 11 x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下載</a></p></td>
</tr>
</tbody>
</table>


## 規則


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 模型</th>
<th>PBX 軟體版本</th>
<th>通訊協定</th>
<th>閘道廠商</th>
<th>閘道模型</th>
<th>設定作者</th>
<th>設定檔案下載 （英文）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CS1000</p></td>
<td><p>3.0 &amp; 4.5</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下載</a></p></td>
</tr>
<tr class="even">
<td><p>Meridian 81 C</p></td>
<td><p>4.5</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下載</a></p></td>
</tr>
<tr class="odd">
<td><p>Meridian 81 C</p></td>
<td><p>4.5</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下載</a></p></td>
</tr>
<tr class="even">
<td><p>Option11c</p></td>
<td><p>版本 25</p></td>
<td><p>數位組模擬 (DNI2616)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008DNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下載</a></p></td>
</tr>
<tr class="odd">
<td><p>Option11c</p></td>
<td><p>版本 25</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下載</a></p></td>
</tr>
<tr class="even">
<td><p>Option11c</p></td>
<td><p>版本 25</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下載</a></p></td>
</tr>
<tr class="odd">
<td><p>ATL-CS-001-1000 M （連續）</p></td>
<td><p>版本 25.40</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下載</a></p></td>
</tr>
</tbody>
</table>


## Panasonic


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 模型</th>
<th>PBX 軟體版本</th>
<th>通訊協定</th>
<th>閘道廠商</th>
<th>閘道模型</th>
<th>設定作者</th>
<th>設定檔案下載 （英文）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>KX TDA200</p></td>
<td><p>001 001</p></td>
<td><p>類比-頻內 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下載</a></p></td>
</tr>
<tr class="even">
<td><p>KX TDA200</p></td>
<td><p>3</p></td>
<td><p>類比-頻內 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP 11 x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下載</a></p></td>
</tr>
<tr class="odd">
<td><p>KX TES824</p></td>
<td><p>2.0.2</p></td>
<td><p>類比-頻內 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP 11 x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下載</a></p></td>
</tr>
</tbody>
</table>


## Rolm


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 模型</th>
<th>PBX 軟體版本</th>
<th>通訊協定</th>
<th>閘道廠商</th>
<th>閘道模型</th>
<th>設定作者</th>
<th>設定檔案下載 （英文）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>9751</p></td>
<td><p>9005</p></td>
<td><p>數位組模擬 (DNIRP400)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008RLMDNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下載</a></p></td>
</tr>
</tbody>
</table>


## ShoreTel


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 模型</th>
<th>PBX 軟體版本</th>
<th>通訊協定</th>
<th>閘道廠商</th>
<th>閘道模型</th>
<th>設定作者</th>
<th>設定檔案下載 （英文）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>IP 電話系統</p></td>
<td><p>6.1</p></td>
<td><p>類比 – SMDI</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP 11 x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下載</a></p></td>
</tr>
<tr class="even">
<td><p>IP 電話系統</p></td>
<td><p>7.5</p></td>
<td><p>類比 – SMDI</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下載</a></p></td>
</tr>
</tbody>
</table>


## Siemens


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 模型</th>
<th>PBX 軟體版本</th>
<th>通訊協定</th>
<th>閘道廠商</th>
<th>閘道模型</th>
<th>設定作者</th>
<th>設定檔案下載 （英文）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>HiCom 150E</p></td>
<td><p>相關 2.2</p></td>
<td><p>類比 – 頻內 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP 11 x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下載</a></p></td>
</tr>
<tr class="even">
<td><p>HiCom 300</p></td>
<td><p>SA300-V3.05</p></td>
<td><p>BRI QSIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG3000</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下載</a></p></td>
</tr>
<tr class="odd">
<td><p>HiCom 300</p></td>
<td><p>9006.4SMR3</p></td>
<td><p>數位組模擬 (DNIOptiset)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008DNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下載</a></p></td>
</tr>
<tr class="even">
<td><p>HiCom 300</p></td>
<td><p>9006.4SMR3</p></td>
<td><p>T1 CAS-頻內 DTMF</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下載</a></p></td>
</tr>
<tr class="odd">
<td><p>HiPath 3550</p></td>
<td><p>相關 3</p></td>
<td><p>類比 – 頻內 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP 11 x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下載</a></p></td>
</tr>
<tr class="even">
<td><p>HiPath 4000</p></td>
<td><p>Tkn-ooty-ver 3.0 SMR5 SMP4</p></td>
<td><p>類比 – 頻內 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP 11 x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下載</a></p></td>
</tr>
<tr class="odd">
<td><p>HiPath 4000</p></td>
<td><p>SA300-V3.05</p></td>
<td><p>BRI QSIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG3000</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下載</a></p></td>
</tr>
<tr class="even">
<td><p>HiPath 4000</p></td>
<td><p>Tkn-ooty-ver 3.0 SMR5 SMP4</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下載</a></p></td>
</tr>
<tr class="odd">
<td><p>HiPath 4000</p></td>
<td><p>版本 2.0 SMR9 SMP0</p></td>
<td><p>類比-頻內 DTMF</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008LSW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下載</a></p></td>
</tr>
<tr class="even">
<td><p>HiPath 4000</p></td>
<td><p>版本 2.0 SMR9 SMP0</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下載</a></p></td>
</tr>
</tbody>
</table>


## Sonus


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
<th>VoIP 閘道模型</th>
<th>VoIP 閘道軟體版本</th>
<th>支援的通訊協定</th>
<th>設定作者</th>
<th>設定檔案下載 （英文）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SBC 1000/2000</p></td>
<td><p>2.2.1 或更新版本</p></td>
<td><ul>
<li><p>TDM 訊號 (ISDN): 在 &amp; T 4ESS/5ESS、 規則 DMS 100、 歐元 ISDN （以 300 102）、 QSIG、 NTT InsNet （日本）、 ANSI 國民 ISDN-2 (NI-2)</p></li>
<li><p>TDM 訊號 (CAS): T1 CAS (E &amp; M、 迴圈開始); E1 CAS (R2)</p></li>
</ul></td>
<td><p>Sonus</p></td>
<td><p><a href="http://www.sonus.net/sites/default/files/sonussbc1k2kconfigo365.pdf">下載</a></p></td>
</tr>
</tbody>
</table>


## Tadiran


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 模型</th>
<th>PBX 軟體版本</th>
<th>通訊協定</th>
<th>閘道廠商</th>
<th>閘道模型</th>
<th>設定作者</th>
<th>設定檔案下載 （英文）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>珊瑚紅 Flexicom</p></td>
<td><p>14.67.49</p></td>
<td><p>類比 – 頻內 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP 11 x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下載</a></p></td>
</tr>
<tr class="even">
<td><p>珊瑚紅 Flexicom</p></td>
<td><p>14.67.49</p></td>
<td><p>BRI QSIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant</p>
<p>1000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下載</a></p></td>
</tr>
<tr class="odd">
<td><p>珊瑚紅 Flexicom</p></td>
<td><p>14.67.49</p></td>
<td><p>E1 CAS-頻內 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下載</a></p></td>
</tr>
<tr class="even">
<td><p>珊瑚紅 Flexicom</p></td>
<td><p>14.67.49</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下載</a></p></td>
</tr>
<tr class="odd">
<td><p>珊瑚紅 IPX</p></td>
<td><p>14.67.49</p></td>
<td><p>類比 – 頻內 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP 11 x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下載</a></p></td>
</tr>
<tr class="even">
<td><p>珊瑚紅 IPX</p></td>
<td><p>14.67.49</p></td>
<td><p>BRI QSIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下載</a></p></td>
</tr>
<tr class="odd">
<td><p>珊瑚紅 IPX</p></td>
<td><p>14.67.49</p></td>
<td><p>E1 CAS – 頻內 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下載</a></p></td>
</tr>
<tr class="even">
<td><p>珊瑚紅 IPX</p></td>
<td><p>14.67.49</p></td>
<td><p>E1 QSIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant</p>
<p>1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下載</a></p></td>
</tr>
</tbody>
</table>


## 地區


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 模型</th>
<th>PBX 軟體版本</th>
<th>通訊協定</th>
<th>閘道廠商</th>
<th>閘道模型</th>
<th>設定作者</th>
<th>設定檔案下載 （英文）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CTX</p></td>
<td><p>AR1ME021.00</p></td>
<td><p>類比 – SMDI</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008LSW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下載</a></p></td>
</tr>
<tr class="even">
<td><p>CTX</p></td>
<td><p>AR1ME021.00</p></td>
<td><p>類比 – 頻內 DTMF</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008LSW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下載</a></p></td>
</tr>
</tbody>
</table>

