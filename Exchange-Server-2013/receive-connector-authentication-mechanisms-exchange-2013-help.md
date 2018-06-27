---
title: '接收連接器的驗證機制: Exchange 2013 Help'
TOCTitle: 接收連接器的驗證機制
ms:assetid: 926424e1-83e3-4c4b-b2dd-bf814d81e877
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ657472(v=EXCHG.150)
ms:contentKeyID: 50473747
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 接收連接器的驗證機制

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_


接收連接器的驗證機制如下：


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>驗證機制</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>無</p></td>
<td><p>不使用驗證。</p></td>
</tr>
<tr class="even">
<td><p>TLS</p></td>
<td><p>Advertise STARTTLS。需要伺服器憑證來提供 TLS 的可用性。</p></td>
</tr>
<tr class="odd">
<td><p>整合式</p></td>
<td><p>NTLM 及 Kerberos (整合式 Windows 驗證)。</p></td>
</tr>
<tr class="even">
<td><p>BasicAuth</p></td>
<td><p>基本驗證。需要驗證登入。</p></td>
</tr>
<tr class="odd">
<td><p>BasicAuthRequireTLS</p></td>
<td><p>透過 TLS 的基本驗證。需要伺服器憑證。</p></td>
</tr>
<tr class="even">
<td><p>ExchangeServer</p></td>
<td><p>Exchange 伺服器驗證 (一般安全性服務應用程式設計介面 (GSSAPI) 和相互 GSSAPI)。</p></td>
</tr>
<tr class="odd">
<td><p>ExternalAuthoritative</p></td>
<td><p>連線會被視為外部保護使用外部Exchange安全性機制。連線可能是網際網路通訊協定安全性 (IPsec) 關聯或虛擬私人網路 (VPN)。或者，伺服器可能位於受信任的實體控制網路中。<code>ExternalAuthoritative</code>驗證方法需要<code>ExchangeServers</code>權限群組。此組合的驗證方法及安全性] 群組，允許匿名寄件者電子郵件地址接收透過此連接器的郵件的解析度。</p></td>
</tr>
</tbody>
</table>


如需接收連接器的驗證機制的詳細資訊，請參閱[New-ReceiveConnector](https://technet.microsoft.com/zh-tw/library/bb125139\(v=exchg.150\))。

