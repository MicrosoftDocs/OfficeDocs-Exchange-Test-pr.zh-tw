---
title: 'Exchange 2013 儲存裝置組態選項: Exchange 2013 Help'
TOCTitle: Exchange 2013 儲存裝置組態選項
ms:assetid: 37cdeacf-74f9-4399-9860-4d1dbec12bb1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee832792(v=EXCHG.150)
ms:contentKeyID: 50472857
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013 儲存裝置組態選項

 

_**適用版本：**Exchange Online, Exchange Server, Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

了解 Microsoft Exchange Server 2013 中信箱伺服器角色的儲存選項和需求，是信箱伺服器儲存設計解決方案的重要部分。

**目錄**

Storage architectures

Physical disk types

Best practices for supported storage configurations

## 儲存結構

下表描述支援的存放結構，並提供各種適用存放結構類型的最佳作法指南。

### 支援的存放結構

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>存放結構</th>
<th>描述</th>
<th>最佳作法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>直接附加儲存 (DAS)</p></td>
<td><p>DAS 是一種數位儲存系統，直接附加在伺服器或工作站，而不需要中介的儲存網路。例如，DAS 傳輸包括序列連結小型電腦系統介面 (SCSI) 和序列連結進階技術附加裝置 (ATA)。</p></td>
<td><p>無。</p></td>
</tr>
<tr class="even">
<td><p>儲存區域網路 (SAN)：Internet Small Computer System Interface (iSCSI)</p></td>
<td><p>SAN 是一種將遠端電腦儲存裝置 (例如磁碟陣列和磁帶庫) 附加至伺服器的架構，藉由這種方式，裝置將顯示為於本機端附加於作業系統之下 (例如，區塊儲存)。iSCSI SAN 會將 SCSI 命令封裝於 IP 封包中，並使用標準網路基礎結構做為儲存傳輸 (例如，乙太網路)。</p></td>
<td><p>不要與其他應用程式共用實體磁碟備份 Exchange 資料。</p>
<p>使用專用的儲存網路。</p>
<p>將多個網路路徑用於獨立組態。</p></td>
</tr>
<tr class="odd">
<td><p>SAN：光纖通道</p></td>
<td><p>光纖通道 SAN 會將 SCSI 命令封裝在光纖通道封包中，而且通常會使用專屬光纖通道網路作為儲存傳輸。</p></td>
<td><p>不要與其他應用程式共用實體磁碟備份 Exchange 資料。</p>
<p>將多個光纖通道網路路徑用於獨立組態。</p>
<p>遵循存放裝置廠商的最佳作法來微調光纖通道主匯流排介面卡 (HBA)，例如佇列深度和佇列目標。</p></td>
</tr>
</tbody>
</table>


網路連接儲存 (NAS) 裝置是連接至網路包含本身的電腦，其唯一目的是提供網路上其他裝置檔案型的資料儲存服務。NAS 裝置上的作業系統和其他軟體提供資料儲存、檔案系統和存取檔案等功能，以及這些功能的管理 (例如，檔案儲存)。

Exchange 用於儲存 Exchange 資料的所有儲存裝置必須是區塊層級的儲存裝置，因為 Exchange 2013 不支援使用 NAS 磁碟區，但 [Exchange 2013 虛擬化](exchange-2013-virtualization-exchange-2013-help.md)主題中概述的 SMB 3.0 案例除外。此外，在虛擬化環境中，不支援透過 Hypervisor 向來賓顯示作為區塊層級儲存裝置的 NAS 儲存裝置。

不建議使用儲存層，因為它可能有不良影響系統效能。此原因，不允許自動移到 「 更快 」 儲存區的 \[最存取的檔案儲存控制站。

回到頁首

## 實體磁碟類型

下表提供支援的實體磁碟類型的清單，並提供各種適用實體磁碟類型的最佳作法指南。

### 支援的實體磁碟類型

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>實體磁碟類型</th>
<th>描述</th>
<th>支援的或最佳作法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Serial ATA (SATA)</p></td>
<td><p>SATA 是 ATA 及整合式電子裝置 (IDE) 磁碟的序列介面。SATA 磁碟有各種外觀尺寸、速度和容量。</p>
<p>一般而言，當您有下列設計需求時，可以選擇 SATA 磁碟作為 Exchange 2013 信箱儲存使用：</p>
<ul>
<li><p>高容量</p></li>
<li><p>中等效能</p></li>
<li><p>中等電源使用率</p></li>
</ul></td>
<td><p>支援：在 Windows Server 2008 與 Windows Server 2008 R2 中的 512 位元組磁區磁碟。此外，在下列條件下的 Windows Server 2008 R2 中支援 512e 磁碟：</p>
<ul>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=982018">Microsoft 知識庫文章 982018</a> 中所述的 Hotfix，此更新可改善 Windows 7 和 Windows Server 2008 R2 與進階格式磁碟的相容性。</p></li>
<li><p>Windows Server 2008 R2 Service Pack 1 (SP1) 和 Exchange Server 2010 SP1。</p></li>
</ul>
<p>Exchange 2013 和更新版本支援原生 4 KB 磁區磁碟和 512e 磁碟。資料庫的所有複本都必須位於相同的實體磁碟類型上，才受到支援。例如，某個資料庫在 512 位元組磁區磁碟機上有一個複本，在 512e 磁碟或 4K 磁碟上有另一個複本，這就是不支援的組態。</p>
<p>最佳作法：考慮採用企業級 SATA 磁碟，這類磁碟通常有較好的耐熱、震動和可靠度特性。</p></td>
</tr>
<tr class="even">
<td><p>Serial Attached SCSI</p></td>
<td><p>Serial Attached SCSI 是 SCSI 磁碟的序列介面。Serial Attached SCSI 磁碟有各種外觀尺寸、速度和容量。</p>
<p>一般而言，當您有下列設計需求時，可以選擇 Serial Attached SCSI 磁碟作為 Exchange 2013 信箱儲存使用：</p>
<ul>
<li><p>中等容量</p></li>
<li><p>高效能</p></li>
<li><p>中等電源使用率</p></li>
</ul></td>
<td><p>支援：在 Windows Server 2008 與 Windows Server 2008 R2 中的 512 位元組磁區磁碟。此外，在下列條件下的 Windows Server 2008 R2 中支援 512e 磁碟：</p>
<ul>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=982018">Microsoft 知識庫文章 982018</a> 中所述的 Hotfix，此更新可改善 Windows 7 和 Windows Server 2008 R2 與進階格式磁碟的相容性。</p></li>
<li><p>Windows Server 2008 R2 Service Pack 1 (SP1) 和 Exchange Server 2010 SP1。</p></li>
</ul>
<p>Exchange 2013 和更新版本支援原生 4 KB 磁區磁碟和 512e 磁碟。資料庫的所有複本都必須位於相同的實體磁碟類型上，才受到支援。例如，某個資料庫在 512 位元組磁區磁碟機上有一個複本，在 512e 磁碟或 4K 磁碟上有另一個複本，這就是不支援的組態。</p>
<p>最佳作法：不搭配 UPS 使用時，必須停用實體磁碟寫入快取功能。</p></td>
</tr>
<tr class="odd">
<td><p>光纖通道</p></td>
<td><p>光纖通道是用來將磁碟連接至光纖通道型 SAN 的電子介面。光纖通道磁碟有各種不同的速度和容量。</p>
<p>一般而言，當您有下列設計需求時，可以選擇光纖通道磁碟作為 Exchange 2013 信箱儲存使用：</p>
<ul>
<li><p>中等容量</p></li>
<li><p>高效能</p></li>
<li><p>SAN 連線能力</p></li>
</ul></td>
<td><p>支援：在 Windows Server 2008 與 Windows Server 2008 R2 中的 512 位元組磁區磁碟。此外，在下列條件下的 Windows Server 2008 R2 中支援 512e 磁碟：</p>
<ul>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=982018">Microsoft 知識庫文章 982018</a> 中所述的 Hotfix，此更新可改善 Windows 7 和 Windows Server 2008 R2 與進階格式磁碟的相容性。</p></li>
<li><p>Windows Server 2008 R2 Service Pack 1 (SP1) 和 Exchange Server 2010 SP1。</p></li>
</ul>
<p>Exchange 2013 和更新版本支援原生 4 KB 磁區磁碟和 512e 磁碟。資料庫的所有複本都必須位於相同的實體磁碟類型上，才受到支援。例如，某個資料庫在 512 位元組磁區磁碟機上有一個複本，在 512e 磁碟或 4K 磁碟上有另一個複本，這就是不支援的組態。</p>
<p>最佳作法：不搭配 UPS 使用時，必須停用實體磁碟寫入快取功能。</p></td>
</tr>
<tr class="even">
<td><p>固態磁碟機 (SSD) (快閃磁碟)</p></td>
<td><p>SSD 是一種使用固態記憶體來儲存持續性資料的資料儲存裝置。SSD 會模擬硬碟機介面。SSD 磁碟有各種速度 (不同的 I/O 效能) 和容量。</p>
<p>一般而言，當您有下列設計需求時，可以選擇 SSD 磁碟作為 Exchange 2013 信箱儲存使用：</p>
<ul>
<li><p>低容量</p></li>
<li><p>非常高的效能</p></li>
</ul></td>
<td><p>支援：在 Windows Server 2008 與 Windows Server 2008 R2 中的 512 位元組磁區磁碟。此外，在下列條件下的 Windows Server 2008 R2 中支援 512e 磁碟：</p>
<ul>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=982018">Microsoft 知識庫文章 982018</a> 中所述的 Hotfix，此更新可改善 Windows 7 和 Windows Server 2008 R2 與進階格式磁碟的相容性。</p></li>
<li><p>Windows Server 2008 R2 Service Pack 1 (SP1) 和 Exchange Server 2010 SP1。</p></li>
</ul>
<p>Exchange 2013 和更新版本支援原生 4 KB 磁區磁碟和 512e 磁碟。資料庫的所有複本都必須位於相同的實體磁碟類型上，才受到支援。例如，某個資料庫在 512 位元組磁區磁碟機上有一個複本，在 512e 磁碟或 4K 磁碟上有另一個複本，這就是不支援的組態。</p>
<p>最佳作法：不搭配 UPS 使用時，必須停用實體磁碟寫入快取功能。</p>
<p>一般而言，Exchange 2013 信箱伺服器不需要 SSD 儲存的效能特性。</p></td>
</tr>
</tbody>
</table>


## 選擇磁碟類型時考慮的因素

為 Exchange 2013 儲存體選擇磁碟類型時有數種取捨。合適的磁碟是在效能 (包括連續性與隨機效能) 與容量、可靠性、電源使用率和資金成本之間取得均衡的磁碟。以下支援的實體磁碟類型資料表提供的資訊，可協助您考慮這些因素。

從效能觀點來看，使用大型、 較慢磁碟 Exchange 儲存區的外觀是否可以，提供磁碟可以維持平均讀取和寫入 20 毫秒的延遲或更少的負載下。

### 選擇磁碟類型的因素

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
<th>磁碟速度 (轉速)</th>
<th>磁碟的外觀尺寸</th>
<th>介面或傳輸</th>
<th>容量</th>
<th>隨機 I/O 效能</th>
<th>連續性 I/O 效能</th>
<th>電源使用率</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>5,400</p></td>
<td><p>2.5-inch</p></td>
<td><p>SATA</p></td>
<td><p>一般</p></td>
<td><p>很差</p></td>
<td><p>很差</p></td>
<td><p>極佳</p></td>
</tr>
<tr class="even">
<td><p>5,400</p></td>
<td><p>3.5-inch</p></td>
<td><p>SATA</p></td>
<td><p>極佳</p></td>
<td><p>很差</p></td>
<td><p>很差</p></td>
<td><p>一般水準以上</p></td>
</tr>
<tr class="odd">
<td><p>7,200</p></td>
<td><p>2.5-inch</p></td>
<td><p>SATA</p></td>
<td><p>一般</p></td>
<td><p>一般</p></td>
<td><p>一般</p></td>
<td><p>極佳</p></td>
</tr>
<tr class="even">
<td><p>7,200</p></td>
<td><p>2.5-inch</p></td>
<td><p>Serial Attached SCSI</p></td>
<td><p>一般</p></td>
<td><p>一般</p></td>
<td><p>一般水準以上</p></td>
<td><p>極佳</p></td>
</tr>
<tr class="odd">
<td><p>7,200</p></td>
<td><p>3.5-inch</p></td>
<td><p>SATA</p></td>
<td><p>極佳</p></td>
<td><p>一般</p></td>
<td><p>一般水準以上</p></td>
<td><p>一般水準以上</p></td>
</tr>
<tr class="even">
<td><p>7,200</p></td>
<td><p>3.5-inch</p></td>
<td><p>Serial Attached SCSI</p></td>
<td><p>極佳</p></td>
<td><p>一般</p></td>
<td><p>一般水準以上</p></td>
<td><p>一般水準以上</p></td>
</tr>
<tr class="odd">
<td><p>7,200</p></td>
<td><p>3.5-inch</p></td>
<td><p>光纖通道</p></td>
<td><p>極佳</p></td>
<td><p>一般</p></td>
<td><p>一般水準以上</p></td>
<td><p>一般</p></td>
</tr>
<tr class="even">
<td><p>10,000</p></td>
<td><p>2.5-inch</p></td>
<td><p>Serial Attached SCSI</p></td>
<td><p>低於一般水準</p></td>
<td><p>極佳</p></td>
<td><p>一般水準以上</p></td>
<td><p>一般水準以上</p></td>
</tr>
<tr class="odd">
<td><p>10,000</p></td>
<td><p>3.5-inch</p></td>
<td><p>SATA</p></td>
<td><p>一般</p></td>
<td><p>一般</p></td>
<td><p>一般水準以上</p></td>
<td><p>一般水準以上</p></td>
</tr>
<tr class="even">
<td><p>10,000</p></td>
<td><p>3.5-inch</p></td>
<td><p>Serial Attached SCSI</p></td>
<td><p>一般</p></td>
<td><p>一般水準以上</p></td>
<td><p>一般水準以上</p></td>
<td><p>低於一般水準</p></td>
</tr>
<tr class="odd">
<td><p>10,000</p></td>
<td><p>3.5-inch</p></td>
<td><p>光纖通道</p></td>
<td><p>一般</p></td>
<td><p>一般水準以上</p></td>
<td><p>一般水準以上</p></td>
<td><p>低於一般水準</p></td>
</tr>
<tr class="even">
<td><p>15,000</p></td>
<td><p>2.5-inch</p></td>
<td><p>Serial Attached SCSI</p></td>
<td><p>很差</p></td>
<td><p>極佳</p></td>
<td><p>極佳</p></td>
<td><p>一般</p></td>
</tr>
<tr class="odd">
<td><p>15,000</p></td>
<td><p>3.5-inch</p></td>
<td><p>Serial Attached SCSI</p></td>
<td><p>一般</p></td>
<td><p>極佳</p></td>
<td><p>極佳</p></td>
<td><p>低於一般水準</p></td>
</tr>
<tr class="even">
<td><p>15,000</p></td>
<td><p>3.5-inch</p></td>
<td><p>光纖通道</p></td>
<td><p>一般</p></td>
<td><p>極佳</p></td>
<td><p>極佳</p></td>
<td><p>很差</p></td>
</tr>
<tr class="odd">
<td><p>SSD：企業級</p></td>
<td><p>不適用</p></td>
<td><p>SATA、Serial Attached SCSI、光纖通道</p></td>
<td><p>很差</p></td>
<td><p>極佳</p></td>
<td><p>極佳</p></td>
<td><p>極佳</p></td>
</tr>
</tbody>
</table>


回到頁首

## 支援的儲存裝置組態的最佳作法

本節提供支援的磁碟和陣列控制器組態有關的最佳作法資訊。

獨立磁碟容錯陣列 (RAID) 的使用通常可兼顧個別磁碟的效能特性 (方法是對多個磁碟進行等量分割)，以及提供個別磁碟的故障防護。由於 Exchange 2013 在高度可用性方面的進步，RAID 不是 Exchange 2013 儲存設計的必要組件。但是，RAID 仍是 Exchange 2013 單機伺服器與需要儲存錯容錯之解決方案的基本元件。

**作業系統、系統或分頁檔磁碟區**

對於作業系統、系統或分頁檔磁碟區，建議的組態為利用 RAID 技術來保護此資料類型。建議的 RAID 組態為 RAID-1 或 RAID-1/0，不過，所有的 RAID 類型皆受支援。

**分開的信箱資料庫與記錄檔磁碟區**

如果您在部署獨立 Mailbox server role 架構，則信箱資料庫與記錄檔磁碟區需採用 RAID 技術。信箱磁碟區的建議 RAID 組態為 RAID-1/0 (尤其是您使用 5.4K 或 7.2K 磁碟時)；不過，所有的 RAID 類型皆受支援。至於記錄檔磁碟區，則建議的 RAID 組態為 RAID-1 或 RAID-1/0。

讓作業系統、分頁檔或 Exchange 資料磁碟區使用 RAID-5 或 RAID-6 組態時，請注意下列事項：

  - 在 RAID-5 組態 (包括 RAID-50 和 RAID-51 等變化種類) 中，每個陣列群組的磁碟不應超過 7 個，且應啟用陣列控制器高優先順序刪除和表面掃描。

  - 在 RAID-6 組態中，應啟用陣列控制器高優先順序刪除和表面掃描。

雖然在具有 3 個 (含) 以上高度可用資料庫副本的高可用性架構中可支援 JBOD，但因為記錄檔與信箱資料庫磁碟區是分開的，所以不建議使用 JBOD。

**信箱資料庫與記錄檔磁碟區共置**

在獨立架構中，不建議讓信箱資料庫與記錄檔磁碟區共置。在高可用性架構中，此案例有兩種可能：

1.  每個磁碟區單一資料庫

2.  每個磁碟區多個資料庫

**每個磁碟區單一資料庫**

從 Exchange 觀點，JBOD 表示將資料庫及其關聯的記錄檔都儲存在單一磁碟上。若要在 JBOD 上部署，您必須至少部署三個高度可用的資料庫副本。利用單一磁碟是單一失敗點，因為當磁碟失敗時，位在該磁碟上的資料庫副本會遺失。如果至少有三個資料庫副本，可確保一個副本 (或一個磁碟) 發生失敗時，能透過另外兩個副本提供容錯。不過，放置三個高度可用的資料庫副本，以及使用延遲的資料庫副本，可能會影響儲存設計。下表顯示 RAID 或 JBOD 考量的指導方針。

### RAID 或 JBOD 考量

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>資料中心伺服器</th>
<th>兩個高度可用的副本 (總計)</th>
<th>三個高度可用的副本 (總計)</th>
<th>每個資料中心兩個 (含) 以上高度可用的副本</th>
<th>一個延遲的副本</th>
<th>每個資料中心兩個 (含) 以上延遲的副本</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>主要資料中心伺服器</p></td>
<td><p>RAID</p></td>
<td><p>RAID 或 JBOD (兩個副本)</p></td>
<td><p>RAID 或 JBOD</p></td>
<td><p>RAID</p></td>
<td><p>RAID 或 JBOD</p></td>
</tr>
<tr class="even">
<td><p>次要資料中心伺服器</p></td>
<td><p>RAID</p></td>
<td><p>RAID (1 個副本)</p></td>
<td><p>RAID 或 JBOD</p></td>
<td><p>RAID</p></td>
<td><p>RAID 或 JBOD</p></td>
</tr>
</tbody>
</table>


若要使用主要資料中心伺服器在 JBOD 上部署，DAG 中需要有三個 (含) 以上高度可用的資料庫副本。如果在裝載高度可用資料庫副本的相同伺服器上混合延遲的副本 (例如，不使用專用的延遲資料庫副本伺服器)，則至少需要兩個延遲的資料庫副本。

若要讓次要資料中心伺服器使用 JBOD，則次要資料中心內至少要有兩個高度可用的資料庫副本。如果次要資料中心內的副本遺失，將不需要跨 WAN 進行重新植入，也不會在啟動次要資料中心時造成單一失敗點。如果在裝載高度可用資料庫副本的相同伺服器上混合延遲的資料庫副本 (例如，不使用專用的延遲資料庫副本伺服器)，則至少需要兩個延遲的資料庫副本。

針對專用的延遲的資料庫副本伺服器，資料中心內至少必須有兩個延遲的資料庫副本，才能使用 JBOD。否則，遺失磁碟會導致遺失延遲的資料庫副本，以及失去防護機制。

**每個磁碟區多個資料庫**

每個磁碟區多個資料庫是 Exchange 2013 提供的新 JBOD 案例，允許在單一磁碟上混合主動與被動副本 (包含延遲的副本)，以達到更好的磁碟使用率。但是，若要以此方式部署延遲的副本，則必須啟用自動延遲的副本記錄檔減少。下表顯示每個磁碟區多個資料庫的 JBOD 考量指導方針。

### JBOD 考量

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>資料中心伺服器</th>
<th>3 個 (含) 以上副本 (總計)</th>
<th>每個資料中心兩個 (含) 以上副本</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>主要資料中心伺服器</p></td>
<td><p>JBOD</p></td>
<td><p>JBOD</p></td>
</tr>
<tr class="even">
<td><p>次要資料中心伺服器</p></td>
<td><p>不適用</p></td>
<td><p>JBOD</p></td>
</tr>
</tbody>
</table>


下表提供有關 Exchange 2013 儲存體陣列組態的指南。

### 支援的 Exchange 2013 Mailbox server role 的 RAID 類型

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>RAID 類型</th>
<th>描述</th>
<th>支援的或最佳作法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>磁碟陣列 RAID 等量大小 (KB)</p></td>
<td><p>等量大小是 RAID 集合中資料分佈的每個磁碟單位。等量大小也稱為<em>區塊大小</em>。</p></td>
<td><p>最佳作法：256 KB 或更大。遵循存放裝置廠商的最佳作法。</p></td>
</tr>
<tr class="even">
<td><p>儲存體陣列快取設定</p></td>
<td><p>快取設定是由電池供電快取陣列控制器所提供。</p></td>
<td><p>最佳作法： 100%寫入快取 （電池或 flash 供電快取） DAS 儲存控制站中選擇其一 RAID 或 JBOD 組態。75%寫入快取、 25%的其他類型的儲存解決方案例如 SAN 讀取快取 （電池或 flash 供電快取）。如果 SAN 廠商及其平台上有不同的快取設定的最佳作法，請遵循的 SAN 廠商的指引。</p></td>
</tr>
<tr class="odd">
<td><p>實體磁碟寫入快取</p></td>
<td><p>快取設定位於每個個別的磁碟上。</p></td>
<td><p>支援：不搭配 UPS 使用時，必須停用實體磁碟寫入快取功能。</p></td>
</tr>
</tbody>
</table>


下表提供有關資料庫及記錄檔選擇的指南。

### Exchange 2013 Mailbox server role 的資料庫和記錄檔選擇

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>資料庫和記錄檔選項</th>
<th>描述</th>
<th>獨立伺服器：支援的或最佳作法</th>
<th>高可用性：支援的或最佳作法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>檔案放置:每個記錄隔離的資料庫</p></td>
<td><p>每個記錄隔離的資料庫是指將資料庫檔案和記錄從相同的信箱資料庫，放置到由不同的實體磁碟提供儲存的不同磁碟區。</p></td>
<td><p>最佳作法：為達到復原性，可將資料庫 (.edb) 檔案和記錄檔從相同的資料庫移至由不同的實體磁碟提供儲存的不同磁碟區。</p></td>
<td><p>支援：記錄和資料庫的隔離並非必要。</p></td>
</tr>
<tr class="even">
<td><p>檔案放置:每個磁碟區的資料庫檔案</p></td>
<td><p>每個磁碟區的資料庫檔案是指在磁碟磁碟區內或跨越不同磁碟磁碟區分佈資料庫檔案的方式。</p></td>
<td><p>最佳作法：依您的備份方法而定。</p></td>
<td><p>支援：使用 JBOD 時，建立含有不同目錄存放資料庫和記錄檔的單一磁碟區。</p></td>
</tr>
<tr class="odd">
<td><p>檔案放置:每個磁碟區的記錄資料流</p></td>
<td><p>每個磁碟區的記錄資料流是指在磁碟磁碟區內或跨越不同磁碟磁碟區分佈資料庫記錄檔的方式。</p></td>
<td><p>最佳作法：依您的備份方法而定。</p></td>
<td><p>支援：使用 JBOD 時，建立含有不同目錄存放資料庫和記錄檔的單一磁碟區。</p>
<p>最佳作法：使用 JBOD 時，充分利用每個磁碟區的多個資料庫。</p></td>
</tr>
<tr class="even">
<td><p>資料庫大小</p></td>
<td><p>資料庫大小指的是磁碟資料庫 (.edb) 檔案大小。</p></td>
<td><p>支援：大約 16 TB。</p>
<p>最佳作法：</p>
<ul>
<li><p>200 GB 或更少。</p></li>
<li><p>提供計算出最大資料庫大小的 120%。</p></li>
</ul></td>
<td><p>支援：大約 16 TB。</p>
<p>最佳作法：</p>
<ul>
<li><p>2 TB 或更少。</p></li>
<li><p>提供計算出最大資料庫大小的 120%。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>記錄截斷方法</p></td>
<td><p>記錄截斷方法是截斷和刪除舊資料庫記錄檔的程序。其中有兩個機制：</p>
<ul>
<li><p>循環記錄，透過這個機制 Exchange 會刪除記錄。</p></li>
<li><p>記錄截斷，通常在完整或增量磁碟區陰影複製服務 (VSS) 備份成功之後發生。</p></li>
</ul></td>
<td><p>最佳作法：</p>
<ul>
<li><p>使用備份進行記錄截斷 (例如，循環記錄已停用)。</p></li>
<li><p>提供三天份的記錄產生容量。</p></li>
</ul></td>
<td><p>最佳作法：</p>
<ul>
<li><p>啟用循環記錄進行使用 Exchange 原生資料保護功能的部署。</p></li>
<li><p>提供三天記錄產生容量延遲設定外的重新顯示。</p></li>
</ul></td>
</tr>
</tbody>
</table>


下表提供有關 Windows 磁碟類型的指南。

### 適用於 Exchange 2013 Mailbox server role 的 Windows 磁碟類型

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Windows 磁碟類型</th>
<th>描述</th>
<th>獨立伺服器：支援的或最佳作法</th>
<th>高可用性：支援的或最佳作法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>基本磁碟</p></td>
<td><p>針對基本存放裝置初始化的磁碟稱為基本磁碟。基本磁碟包含主要磁碟分割、延伸磁碟分割及邏輯磁碟機等基本磁碟區。</p></td>
<td><p>支援。</p>
<p>最佳作法：使用基本磁碟。</p></td>
<td><p>支援。</p>
<p>最佳作法：使用基本磁碟。</p></td>
</tr>
<tr class="even">
<td><p>動態磁碟</p></td>
<td><p>針對動態儲存裝置初始化使用的磁碟稱為動態磁碟。動態磁碟包含簡單磁碟區、跨距磁碟區、等量磁碟區、鏡像磁碟區及 RAID-5 磁碟區等動態磁碟區。</p></td>
<td><p>支援。</p></td>
<td><p>支援。</p></td>
</tr>
</tbody>
</table>


下表提供有關磁碟區組態的指南。

### Exchange 2013 Mailbox server role 的磁碟區組態

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>磁碟區組態</th>
<th>描述</th>
<th>獨立伺服器：支援的或最佳作法</th>
<th>高可用性：支援的或最佳作法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>GUID 磁碟分割表格 (GPT)</p></td>
<td><p>GPT 是可延伸舊版主開機記錄 (MBR) 磁碟分割配置的磁碟架構。最大的 NTFS 格式化磁碟分割大小是 256 TB。</p></td>
<td><p>支援。</p>
<p>最佳作法：使用 GPT 磁碟分割。</p></td>
<td><p>支援。</p>
<p>最佳作法：使用 GPT 磁碟分割。</p></td>
</tr>
<tr class="even">
<td><p>MBR</p></td>
<td><p>MBR 也稱為磁碟分割磁區，是指已分割的資料儲存裝置 (如硬碟) 中作為第一個磁區 (LBA Sector 0) 的 512 位元組開機磁區。最大的 NTFS 格式化磁碟分割大小是 2 TB。</p></td>
<td><p>支援。</p></td>
<td><p>支援。</p></td>
</tr>
<tr class="odd">
<td><p>磁碟分割對齊</p></td>
<td><p>磁碟分割對齊是指對齊磁碟分割的磁區界限以達到最佳效能。</p></td>
<td><p>支援：Windows Server 2008R2 和 Windows Server 2012 的預設值是 1 MB。</p></td>
<td><p>支援： Windows Server 2008R2 和 Windows Server 2012 預設為 1 MB。</p></td>
</tr>
<tr class="even">
<td><p>磁碟區路徑</p></td>
<td><p>磁碟區路徑是指存取磁碟區的方式。</p></td>
<td><p>支援：磁碟機代號或掛接點。</p>
<p>最佳作法：掛接點主機磁碟區必須是已啟用的 RAID。</p></td>
<td><p>支援：磁碟機代號或掛接點。</p>
<p>最佳作法：掛接點主機磁碟區必須是已啟用 RAID。</p></td>
</tr>
<tr class="odd">
<td><p>檔案系統</p></td>
<td><p>檔案系統是儲存和組織電腦檔案和電腦所包含的資料，使其便於尋找和存取那些檔案的方法。</p></td>
<td><p>支援：NTFS 和 ReFS。</p></td>
<td><p>支援：NTFS 和 ReFS。</p></td>
</tr>
<tr class="even">
<td><p>NTFS 磁碟重組</p></td>
<td><p>NTFS 磁碟重組是可以降低 Windows 檔案系統中分散程度的程序。它會實際組織磁碟的內容，並將每一個檔案以並排和連續的方式儲存在一起。</p></td>
<td><p>支援。</p>
<p>最佳作法：非必要，不建議使用。在 Windows Server 2012，我們也建議停用自動磁碟最佳化和磁碟重組功能。</p></td>
<td><p>支援。</p>
<p>最佳作法：非必要，不建議使用。在 Windows Server 2012，我們也建議停用自動磁碟最佳化和磁碟重組功能。</p></td>
</tr>
<tr class="odd">
<td><p>NTFS 配置單位大小</p></td>
<td><p>NTFS 配置單位大小代表可配置用於保留檔案的最小磁碟空間數量。</p></td>
<td><p>支援：所有配置單位大小。</p>
<p>最佳作法：.edb 和記錄檔磁碟區均為 64 KB。</p></td>
<td><p>支援：所有配置單位大小。</p>
<p>最佳作法：.edb 和記錄檔磁碟區均為 64 KB。</p></td>
</tr>
<tr class="even">
<td><p>NTFS 壓縮</p></td>
<td><p>NTFS 壓縮是將檔案在硬碟上實際的儲存大小加以減少的程序。</p></td>
<td><p>支援：不支援 Exchange 資料庫或記錄檔。</p></td>
<td><p>支援：不支援 Exchange 資料庫或記錄檔。</p></td>
</tr>
<tr class="odd">
<td><p>NTFS 加密檔案系統 (EFS)</p></td>
<td><p>EFS 可讓使用者加密個別檔案、資料夾或整個資料磁碟機。因為 EFS 透過業界標準運算法和公開金鑰加密方式提供堅強的加密措施，因此，即使攻擊者避開系統安全措施，加密的檔案仍然沒有洩密之虞。</p></td>
<td><p>支援：不支援 Exchange 資料庫或記錄檔。</p></td>
<td><p>不支援 Exchange 資料庫或記錄檔。</p></td>
</tr>
<tr class="even">
<td><p>Windows BitLocker (磁碟區加密)</p></td>
<td><p>Windows BitLocker 是 Windows Server 2008 中的資料保護功能。電腦遺失或遭竊時，BitLocker 可防止資料遭竊或暴露，而且當電腦除役時，它提供更安全的資料刪除。</p></td>
<td><p>支援：所有 Exchange 資料庫和記錄檔。</p></td>
<td><p>支援：所有 Exchange 資料庫和記錄檔。Windows 容錯移轉叢集需要 Windows Server 2008 R2 或 Windows Server 2008 R2 SP1，以及下列 Hotfix：<a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=2446607">如果電腦為容錯移轉叢集節點，則不能在 Windows Server 2008 R2 的磁碟區上啟用 BitLocker</a>。執行舊版 Exchange 的 Windows 容錯移轉叢集不支援啟用 Bitlocker 的 Windows 磁碟區。</p>
<p>如需Windows 7 BitLocker 加密的詳細資訊，請參閱<a href="https://go.microsoft.com/fwlink/p/?linkid=220898">Windows 7 中的 BitLocker 磁碟加密： 常見問題集</a>。</p></td>
</tr>
<tr class="odd">
<td><p>伺服器訊息區 (SMB) 3.0</p></td>
<td><p>伺服器訊息區塊 (SMB) 傳輸協定為一個網路檔案共用通訊協定 (在 TCP/IP 或其他網路通訊協定之上)，可允許電腦上的應用程式存取遠端伺服器的檔案與資源。也可讓應用程式與任何設為接收 SMB 用戶端請求的伺服器程式通訊。Windows Server 2012 導入全新 SMB 通訊協定 3.0 版本，內含下列功能：</p>
<ul>
<li><p>SMB 通透性與容錯移轉能力</p></li>
<li><p>SMB 延展</p></li>
<li><p>SMB 多重通道</p></li>
<li><p>SMB 直接傳輸</p></li>
<li><p>SMB 加密</p></li>
<li><p>SMB 檔案共用的 VSS</p></li>
<li><p>SMB 目錄租賃</p></li>
<li><p>SMB PowerShell</p></li>
</ul></td>
<td><p>有限支援。支援以 SMB 3.0 共用的 VHD 代管磁碟的硬碟虛擬部署。這些 VHD 透過 Hypervisor 向主機呈現。如需詳細資訊，請參閱 <a href="exchange-2013-virtualization-exchange-2013-help.md">Exchange 2013 虛擬化</a>。</p></td>
<td><p>有限支援。支援以 SMB 3.0 共用的 VHD 代管磁碟的硬碟虛擬部署。這些 VHD 透過 Hypervisor 向主機呈現。如需詳細資訊，請參閱 <a href="exchange-2013-virtualization-exchange-2013-help.md">Exchange 2013 虛擬化</a>。</p></td>
</tr>
<tr class="even">
<td><p>存放空間</p></td>
<td><p>存放空間是一種新的儲存解決方案提供的 Windows Server 2012 的虛擬化功能。存放空間可儲存集區]，可以輕鬆地展開的只新增磁碟將組織的實體磁碟。透過 USB、 SATA 或 SAS 可連接這些磁碟。它也會使用其行為就像實體磁碟，例如細佈建、 以及恢復能力的基礎實體的媒體失敗相關聯的強大功能的虛擬磁碟 （含空白）。如需有關存放空間的詳細資訊，請參閱<a href="https://technet.microsoft.com/en-us/library/hh831739.aspx">儲存空格概觀 （英文)</a>。</p></td>
<td><p>支援。與本主題中說明的實體磁碟類型限制相同。</p></td>
<td><p>支援。與本主題中說明的實體磁碟類型限制相同。</p></td>
</tr>
<tr class="odd">
<td><p>彈性檔案系統 (ReFS)</p></td>
<td><p>ReFS 是新工程的檔案系統的 NTFS 基礎內建的 Windows Server 2012 的。 ReFS 維護與 NTFS 相容性的高程度同時提供增強的資料驗證和自動校正技術為以損毀尤其是當一起使用的儲存空間功能整合式端對端恢復能力。如需有關 ReFS 的詳細資訊，請參閱 ＜<a href="https://technet.microsoft.com/en-us/library/hh831724.aspx">彈性檔案系統概觀</a>。</p></td>
<td><p>支援包含 Exchange 資料庫檔案、 記錄檔和內容索引檔案的磁碟區。如果部署 Windows Server 2012 上，確定 Windows Server 2012 上安裝下列 hotfix：</p>
<ul>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717874">Windows 8 和 Windows Server 2012 更新彙總套件： 2013 年 4 月</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717877">虛擬磁碟服務或應用程式的使用虛擬磁碟服務損毀或 Windows Server 2012 中凍結</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717879">Windows 8 或 Windows Server 2012 為基礎的電腦凍結時執行 ReFS 磁碟區上的 'dir' 命令</a></p></li>
</ul>
<p>OS 磁碟區不支援 reFS。</p>
<p>最佳作法： 資料完整性功能必須停用 Exchange 資料庫 (.edb) 檔案或主控這些檔案的磁碟區。</p></td>
<td><p>支援包含 Exchange 資料庫檔案、 記錄檔和內容索引檔案的磁碟區。如果在 Windows Server 2012 上部署，請確定 Windows Server 2012 上安裝下列 hotfix：</p>
<ul>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717874">Windows 8 和 Windows Server 2012 更新彙總套件： 2013 年 4 月</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717877">虛擬磁碟服務或應用程式的使用虛擬磁碟服務損毀或 Windows Server 2012 中凍結</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717879">Windows 8 或 Windows Server 2012 為基礎的電腦凍結執行 ReFS 磁碟區上的 'dir' 命令時</a></p></li>
</ul>
<p>OS 磁碟區不支援 reFS。</p>
<p>最佳作法： 資料完整性功能必須停用 Exchange 資料庫 (.edb) 檔案或主控這些檔案的磁碟區。</p></td>
</tr>
<tr class="even">
<td><p>重複資料刪除</p></td>
<td><p>重複資料刪除是一種最佳化 Windows Server 2012 儲存空間利用率的新技術。這種方法可在資料內尋找並移除重複資料的方法，同時又無損於資料的精確度或完整性。其目標是藉由將檔案分段成為小型的可變大小區塊、找出重複的區塊，並維護每個區塊的單一複本，在較少的空間儲存較多資料。多餘的區塊複本會取代為對單一複本的參照，區塊會組織成為容器檔案，而容器會予以壓縮，以便達到進一步的空間最佳化。</p></td>
<td><p>不支援 Exchange 資料庫檔案。附註：可以用於完全離線 (用來當作備份或封存檔案) 的 Exchange 資料庫檔案。</p></td>
<td><p>不支援 Exchange 資料庫檔案。附註：可以用於完全離線 (用來當作備份或封存檔案) 的 Exchange 資料庫檔案。</p></td>
</tr>
</tbody>
</table>


回到頁首

