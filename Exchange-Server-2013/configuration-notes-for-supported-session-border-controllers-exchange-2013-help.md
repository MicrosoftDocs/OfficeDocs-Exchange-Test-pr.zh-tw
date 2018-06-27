---
title: '支援工作階段邊界控制器的組態注意事項: Exchange Online Help'
TOCTitle: 支援工作階段邊界控制器的組態注意事項
ms:assetid: d161f94a-a243-4294-93b3-2bf1dc17b59f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ673565(v=EXCHG.150)
ms:contentKeyID: 50554096
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 支援工作階段邊界控制器的組態注意事項

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2017-07-25_

工作階段邊界控制器 (SBC) 可讓您透過專用的公用 WAN 連線，將內部部署電話網路連接至 Microsoft 資料中心。SBC 用於內部部署 IP 網路的邊界，並用來連線到 Microsoft 資料中心的第二個 SBC。

SBC 需要使用數位憑證來加密內部部署組織與 Microsoft 資料中心之間的所有流量。您必須取得用來與 Exchange 混合與線上部署通訊之網路邊界元素 (例如工作階段邊界控制器) 的數位憑證。數位憑證會建立內部部署組織與 Microsoft 資料中心之間的信任，並啟用相互傳輸層安全性 (相互 TLS)。建立這項信任之後，內部部署組織與 Microsoft 資料中心的網路邊界元素會交換工作階段金鑰，然後使用這些的金鑰來加密後續的資料流量。

在混合或線上部署中，UM IP 閘道器代表 SBC。憑證內的主體一般名稱必須與您在 UM IP 閘道器上之 \[位址\] 方塊中建立的完整網域名稱 (FQDN) 值相符。例如，如果您在 UM IP 閘道器上指定 FQDN 位址 sbcexternal.contoso.com，請確認憑證中的主體名稱和主體別名包含相同的值：您使用的名稱有區分大小寫，因此，請確定憑證與 UM IP 閘道器上的大小寫相同。如果您所使用的是 Acme Packet SBC 而且一般名稱與 IP 閘道的 FQDN 不相符，則呼叫將會遭到 403 錯誤拒絕。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Sbc 的設計用來位於上的網路邊緣，因為它們也能夠運作為防火牆。如果您設定好您的組織防火牆後方 SBC，它會導致設定問題並不支援連線至 Office 365。</td>
</tr>
</tbody>
</table>


## 支援的工作階段邊界控制器

下列工作階段邊界控制器 (SBC) 已順利通過與 Exchange 混合與線上部署交互操作性的測試。請注意，SBC 的功能和相容性可能會不同，而設定 SBC 的方式則會因網路上的其他設備而不同。請洽詢 SBC 製造商以了解在混合或線上部署中是否有整合通訊的特定組態注意事項。

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



<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>廠商</strong></p></td>
<td><p><strong>機型</strong></p></td>
<td><p><strong>組態注意事項</strong></p></td>
<td><p><strong>註解</strong></p></td>
</tr>
<tr class="even">
<td><p><a href="http://www.acmepacket.com">Acme 封包</a></p></td>
<td><p>Net-Net 3820 或 4500</p></td>
<td><p><strong>請連絡硬體廠商如需如何設定使用者的裝置最新的指示。</strong></p></td>
<td><p>專用 SBC</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://www.audiocodes.com">AudioCodes</a></p></td>
<td><p>Mediant 1000B MSBG</p></td>
<td><p><strong>請連絡硬體廠商如需如何設定使用者的裝置最新的指示。</strong></p></td>
<td><p>專用 SBC</p></td>
</tr>
<tr class="even">
<td><p><a href="https://www.audiocodes.com">AudioCodes</a></p></td>
<td><p>Mediant 1000B MSBG</p></td>
<td><p><strong>請連絡硬體廠商如需如何設定使用者的裝置最新的指示。</strong></p></td>
<td><p>SBC 和 IP 閘道</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://www.cisco.com/c/dam/en/us/solutions/collateral/enterprise-networks/unified-access/cube-asr-release-10-0.pdf">cisco</a></p></td>
<td><p>ASR 1000</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>必須要有 IOS 15.4 （3) S3 或稍後安裝。</td>
</tr>
</tbody>
</table>

</td>
<td><p><strong>請連絡硬體廠商如需如何設定使用者的裝置最新的指示。</strong></p></td>
<td><p>專用 SBC</p></td>
</tr>
<tr class="even">
<td><p><a href="https://www.ingate.com/">Ingate</a></p></td>
<td><p>SIParator</p></td>
<td><p><strong>請連絡硬體廠商如需如何設定使用者的裝置最新的指示。</strong></p></td>
<td><p>專用 SBC</p></td>
</tr>
<tr class="odd">
<td><p><a href="http://www.net.com">NET</a></p></td>
<td><p>VX1200 &amp; VX1800</p></td>
<td><p><strong>請連絡硬體廠商如需如何設定使用者的裝置最新的指示。</strong></p></td>
<td><p>VoIP 閘道器產品的 SBC 選項</p></td>
</tr>
<tr class="even">
<td><p><a href="http://www.sonus.net/">Sonus</a></p></td>
<td><p>SBC 1000/2000 2.2.1 或更新版本</p></td>
<td><p><strong>請連絡硬體廠商如需如何設定使用者的裝置最新的指示。</strong></p></td>
<td><p>專用 SBC</p></td>
</tr>
</tbody>
</table>

