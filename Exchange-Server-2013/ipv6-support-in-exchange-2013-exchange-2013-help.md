---
title: 'Exchange 2013 中的 IPv6 支援: Exchange 2013 Help'
TOCTitle: Exchange 2013 中的 IPv6 支援
ms:assetid: 33543023-eb9a-4102-b990-84a818a52814
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg144561(v=EXCHG.150)
ms:contentKeyID: 50472943
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013 中的 IPv6 支援

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

網際網路通訊協定第 6 版 (IPv6) 是最新版本的網際網路通訊協定 (IP)。IPv6 被為了更正許多 IPv4，已 IP 舊版的缺點。

在 Microsoft Exchange Server 2013，只有時也安裝並啟用 IPv4 支援 IPv6。如果Exchange 2013部署在此組態中，而且網路支援 IPv4 和 IPv6，所有 Exchange 伺服器可以資料從傳送和接收資料裝置、 伺服器和用戶端使用 IPv6 位址。

本主題討論 IPv6 位址Exchange 2013中。如需 IPv6 的其他背景資訊，請參閱[IPv6](https://go.microsoft.com/fwlink/p/?linkid=92582)。

**目錄**

IPv6 support in Exchange 2013 components

Enable or disable protocols in the operating system

IPv6 address basics

## Exchange 2013 元件中的 IPv6 支援

下表說明會受到 IPv6 影響的 Exchange 2013 元件。

### Exchange 2013 功能及 IPv6

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>IPv6 支援</th>
<th>註解</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>連接篩選代理程式中的 IP 允許清單和 IP 封鎖清單</p></td>
<td><p>是</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>連接篩選代理程式中的 IP 允許清單提供者和 IP 封鎖清單提供者</p></td>
<td><p>否</p></td>
<td><p>目前尚無廣泛公認的業界標準通訊協定的 IPv6 位址查閱。大部分的 IP 封鎖清單提供者不支援 IPv6 位址。如果您接收連接器上允許來自不明的 IPv6 位址匿名連線，您增加垃圾郵件寄件將會略過 IP 封鎖清單提供者與成功傳遞至您的組織的垃圾郵件的風險。</p></td>
</tr>
<tr class="odd">
<td><p>通訊協定分析代理程式中的寄件者信譽</p></td>
<td><p>否</p></td>
<td><p>通訊協定分析代理程式不會計算源自 IPv6 的寄件者的郵件的寄件者信譽等級 (SRL)。如需寄件者信譽的詳細資訊，請參閱<a href="sender-reputation-and-the-protocol-analysis-agent-exchange-2013-help.md">寄件者信譽和通訊協定分析代理程式</a>。</p></td>
</tr>
<tr class="even">
<td><p>寄件者識別碼</p></td>
<td><p>是</p></td>
<td><p>如需相關資訊，請參閱<a href="sender-id-exchange-2013-help.md">寄件者識別碼</a>。</p></td>
</tr>
<tr class="odd">
<td><p>接收連接器</p></td>
<td><p>是</p></td>
<td><p>下列元件接受 IPv6 位址：</p>
<ul>
<li><p>本機 IP 位址繫結</p></li>
<li><p>遠端 IP 位址</p></li>
<li><p>IP 位址範圍</p></li>
</ul>
<p>我們強烈建議針對設定的接收連接器為接受匿名連線從不明的 IPv6 位址。如果您的組織必須接收郵件的寄件者使用 IPv6 位址，建立專用的接收連接器限制這些寄件者使用的特定 IPv6 位址遠端的 IP 位址。</p>
<p>如需相關資訊，請參閱<a href="receive-connectors-exchange-2013-help.md">接收連接器</a>。</p></td>
</tr>
<tr class="even">
<td><p>傳送連接器</p></td>
<td><p>是</p></td>
<td><p>下列元件接受 IPv6 位址：</p>
<ul>
<li><p>智慧主機 IP 位址</p></li>
<li><p>在邊際傳輸伺服器上設定傳送連接器的 <em>SourceIPAddress</em> 參數</p></li>
</ul>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您想要指定<em>SourceIPAddress</em>參數 IPv6 位址，請確定已正確設定適當的 DNS AAAA 與郵件交換 (MX) 記錄。這有助於確保傳遞郵件如果遠端郵件伺服器在嘗試任何種類的反向查閱測試指定之 IPv6 位址。</td>
</tr>
</tbody>
</table>

<p>如需相關資訊，請參閱<a href="send-connectors-exchange-2013-help.md">傳送連接器</a>。</p></td>
</tr>
<tr class="odd">
<td><p>內送郵件率限制</p></td>
<td><p>部分</p></td>
<td><p>您可以設定接收連接器，例如<em>MaxInboundConnectionPercentagePerSource</em>參數、 <em>MaxInboundConnectionPerSource</em>參數，而在<em>TarpitInterval</em>參數的內送郵件速率限制僅適用於通用的 IPv6 位址。連結本機 IPv6 位址與網站本機 IPv6 位址不會受到任何指定之傳入訊息率限制。</p></td>
</tr>
<tr class="even">
<td><p>整合通訊</p></td>
<td><p>是</p></td>
<td><p>如需詳細資訊，請參閱 <a href="ipv6-support-in-unified-messaging-exchange-2013-help.md">整合通訊中的 IPv6 支援</a>。</p></td>
</tr>
<tr class="odd">
<td><p>資料庫可用性群組 (DAG) 成員</p></td>
<td><p>是</p></td>
<td><p>支援靜態 IPv6 位址Windows Server和叢集服務。不過，使用靜態 IPv6 位址違反最佳作法。Exchange 2013不支援在安裝期間的靜態 IPv6 位址設定。</p>
<p>容錯移轉叢集支援內部網站自動通道定址通訊協定 (ISATAP)。它們支援動態登錄在 DNS 中允許的 IPv6 位址。無法在叢集中使用連結本機位址。</p>
<p>如需 DAG 網路需求的相關資訊，請參閱<a href="planning-for-high-availability-and-site-resilience-exchange-2013-help.md">規劃高可用性及站台恢復</a>中的「網路需求」一節。</p></td>
</tr>
</tbody>
</table>


回到頁首

## 啟用或停用作業系統中的協定

Exchange 2013伺服器完全支援 IPv6 網路。因此，即使您不使用 IPv6，則您不需要在 Exchange 伺服器上停用 IPv6。

Exchange 2013中的 IPv6 支援需要安裝及Exchange 2013的所有伺服器上啟用 IPv4。從Exchange 2013伺服器解除安裝 IPv4 不支援。

深入了解 Microsoft Windows 中的 IPv6 支援，以查看[Microsoft windows 的 IPv6： 常見問題集](https://go.microsoft.com/fwlink/p/?linkid=147465)。

回到頁首

## IPv6 位址基礎

IPv6 位址長為 128 位元。地址是使用冒號十六進位表示法所述。冒號十六進位標記法描述 128 位元位址使用八個 16 位元、 4 位數的十六進位數字以冒號 （:） 分隔。以分號分隔十六進位標記法 IPv6 位址的範例是 2001:0DB8:0000:0000:02AA:00FF:C0A8:640A。

您可以使用下列方法說明 IPv6 位址：

  - **擱置前置零** 您可以在 IPv6 位址中 8 個 4 位數字十六進位數值的任何一個略過前置零。

  - **雙冒號壓縮**  您可以使用兩個冒號 （:） 來代表連續 16 位元的十六進位數字會包含零。這些全部零的數字可能存在的開頭、 middle、 或 IPv6 位址的結尾。您只能使用雙冒號壓縮一次的 IPv6 位址。

  - **尾端十進位表示法**  您可能會加上句號 （.） 分隔 8 位元數字 express 結尾處的 IPv6 位址十進位中最後的 32 位元。經常使用 IPv4 相容地址尾隨十進位。

下表提供 IPv6 位址表示法與對等 IPv6 位址語法的範例。

### IPv6 位址表示法及語法

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>IPv6 位址表示法</th>
<th>IPv6 位址語法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>完整 IPv6 位址</p></td>
<td><p>2001:0DB8:0000:0000:02AA:00FF:C0A8:640A</p></td>
</tr>
<tr class="even">
<td><p>使用擱置前置零的 IPv6 位址</p></td>
<td><p>2001:DB8:0:0:2AA:FF:C0A8:640A</p></td>
</tr>
<tr class="odd">
<td><p>使用雙冒號壓縮的 IPv6 位址</p></td>
<td><p>2001:DB8::2AA:FF:C0A8:640A</p></td>
</tr>
<tr class="even">
<td><p>使用尾隨點式十進位表示法的 IPv6 位址</p></td>
<td><p>2001:DB8::2AA:FF:192.168.100.10</p></td>
</tr>
</tbody>
</table>


IPv6 位址分為下列類型：

  - **單點廣播位址** 封包傳送到一個介面。

  - **多點廣播位址** 封包傳送到多個介面。

  - **任何傳播位址**  封包傳遞至最接近的多個介面。由路由成本定義介面之間的距離。

IPv6 單點廣播位址具有下列可能的範圍：

  - **本機的連結**  IPv6 位址範圍為本機的子網路。IPv4 連結本機位址用在自動私人 IP 位址 (APIPA) 相較下個 IPv6 連結本機位址。

  - **本機網站**  IPv6 位址的範圍是在當地組織。網站本機位址已被取代的 RFC 3879 同時 RFC 4193 中所定義唯一的本機位址取代。IPv6 網站本機位址及 IPv6 唯一本機位址是 IPv4 私人 IP 位址相較下。

  - **通用**  IPv6 位址的範圍是整個 world。IPv6 通用位址是 IPv4 公用 IP 位址相較下。

下表提供 IPv4 元素與 IPv6 元素的比較。

### IPv4 元素與 IPv6 元素

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>項目</th>
<th>IPv4</th>
<th>IPv6</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>私人 IP 位址</p></td>
<td><p>10.0.0.0/8</p>
<p>172.16.0.0/12</p>
<p>192.168.0.0/16</p></td>
<td><p>FD00::/8</p></td>
</tr>
<tr class="even">
<td><p>連結本機位址</p></td>
<td><p>169.254.0.0/16</p></td>
<td><p>FE80::/64</p></td>
</tr>
<tr class="odd">
<td><p>回送位址</p></td>
<td><p>127.0.0.1</p></td>
<td><p>::1</p></td>
</tr>
<tr class="even">
<td><p>未指定位址</p></td>
<td><p>0.0.0.0</p></td>
<td><p>::</p></td>
</tr>
<tr class="odd">
<td><p>位址解析</p></td>
<td><p>位址解析通訊協定 (ARP)</p></td>
<td><p>芳鄰探索 (ND)</p></td>
</tr>
<tr class="even">
<td><p>網域名稱系統 (DNS) 主機名稱解析</p></td>
<td><p>地址記錄 (A 記錄)</p></td>
<td><p>AAAA 記錄或 A6 記錄</p></td>
</tr>
</tbody>
</table>


如需 IPv6 位址的詳細資訊，請參閱[IPv6 位址類型](https://go.microsoft.com/fwlink/p/?linkid=98357)。

## 支援的 IPv6 位址輸入格式

Exchange 2013 支援以下類型的 IPv6 位址輸入格式：

  - 單一 IPv6 位址

  - IPv6 位址範圍

  - IPv6 位址與子網路遮罩

  - IPv6 位址與使用「無類別網域間路由選擇」(CIDR) 表示法的子網路遮罩

下表提供 Exchange 2013 中可接受的 IPv6 位址輸入格式範例。

### IPv6 位址範例

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>類型</th>
<th>IPv6 位址範例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>單一位址</p></td>
<td><p>2001:DB8::2AA:FF:C0A8:640A</p></td>
</tr>
<tr class="even">
<td><p>位址範圍</p></td>
<td><p>2001:DB8::2AA:FF:C0A8:640A-2001:DB8::2AA:FF:C0A8:6414</p></td>
</tr>
<tr class="odd">
<td><p>位址與子網路遮罩</p></td>
<td><p>2001:DB8::2AA:FF:C0A8:640A(FFFF:FFFF:FFFF:FFFF::)</p></td>
</tr>
<tr class="even">
<td><p>位址與使用 CIDR 表示法的子網路遮罩</p></td>
<td><p>2001:DB8::2AA:FF:C0A8:640A/64</p></td>
</tr>
</tbody>
</table>


在 Exchange 2013 中，支援以下輸入格式：

  - 擱置前置零

  - 雙冒號壓縮

  - 尾隨點式十進位表示法

回到頁首

