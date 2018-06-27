---
title: 'Exchange 2013 系統需求: Exchange 2013 Help'
TOCTitle: Exchange 2013 系統需求
ms:assetid: 1e80857c-b870-4a6d-a0f4-ff7b3a7be037
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa996719(v=EXCHG.150)
ms:contentKeyID: 50472788
ms.date: 02/12/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 系統需求

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

了解在安裝 Exchange 2013 之前，您需要知道的 Exchange 2013 需求。例如，您將了解硬體、 網路及作業系統需求。

安裝 Microsoft Exchange Server 2013 之前，建議您先檢閱本主題，以確保您的網路、硬體、軟體、用戶端及其他元素都符合 Exchange 2013 的需求。此外，請確認您了解 Exchange 2013 和舊版 Exchange 所支援的共存案例。

## 支援的共存案例

下表列出支援 Exchange 2013 與舊版 Exchange 共存的案例。

### Exchange 2013 與舊版 Exchange 伺服器共存

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange 版本</th>
<th>Exchange 組織共存</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Server 2003 和更早版本</p></td>
<td><p>不支援</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2007</p></td>
<td><p>支援下列 Exchange 最低版本：</p>
<ul>
<li><p>1組織中所有 Exchange 2007 伺服器 (包括 Edge Transport server) 上的 Exchange 2007 Service Pack 3 (SP3) 適用的更新彙總套件 10。</p></li>
<li><p>組織中所有 Exchange 2013 伺服器上的 Exchange 2013 累計更新 2 (CU2) 或更新版本。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Exchange 2010</p></td>
<td><p>支援下列 Exchange 最低版本：</p>
<ul>
<li><p>2組織中所有 Exchange 2010 伺服器 (包括 Edge Transport server) 上的 Exchange 2010 SP3。</p></li>
<li><p>組織中所有 Exchange 2013 伺服器上的 Exchange 2013 CU2。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>混合的 Exchange 2010 與 Exchange 2007 組織</p></td>
<td><p>支援下列 Exchange 最低版本：</p>
<ul>
<li><p>1組織中所有 Exchange 2007 伺服器 (包括 Edge Transport server) 上的 Exchange 2007 SP3 適用的更新彙總套件 10。</p></li>
<li><p>2組織中所有 Exchange 2010 伺服器 (包括 Edge Transport server) 上的 Exchange 2010 SP3。</p></li>
<li><p>組織中所有 Exchange 2013 伺服器上的 Exchange 2013 CU2。</p></li>
</ul></td>
</tr>
</tbody>
</table>


1   如果您想在 Exchange 2007 Hub Transport Server 與 Exchange 2013 SP1 Edge Transport Server 之間建立 EdgeSync 訂閱，則必須在 Exchange 2007 Hub Transport Server 上安裝 Exchange 2007 SP3 的更新彙總套件 13 或更新版本。

2   如果您想在 Exchange 2010 Hub Transport Server 與 Exchange 2013 SP1 Edge Transport Server 之間建立 EdgeSync 訂閱，則必須在 Exchange 2010 Hub Transport Server 上安裝 Exchange 2010 SP3 的更新彙總套件 5 或更新版本。

## 支援的混合部署案例

對於已升級到最新版 Office 365 的 Office 365 承租人，Exchange 2013 支援混合式部署。如需混合部署的相關資訊，請參閱[混合部署必要條件](https://technet.microsoft.com/zh-tw/library/hh534377\(v=exchg.150\))。

## 網路及目錄伺服器

下表列出您的 Exchange 2013 組織中，網路及目錄伺服器的需求。

**Exchange 2013 的網路和目錄伺服器需求**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>元件</th>
<th>需求</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>架構主機</p></td>
<td><p>依預設，架構主機是在樹系中所安裝的第一部 Active Directory 網域控制站上執行。架構主機必須執行下列其中一項：</p>
<ul>
<li><p>Windows Server 2012 R2 Standard 或 Datacenter1</p></li>
<li><p>Windows Server 2012 Standard 或 Datacenter</p></li>
<li><p>Windows Server 2008 R2 Standard 或 Enterprise</p></li>
<li><p>Windows Server 2008 R2 Datacenter RTM 或更新版本</p></li>
<li><p>Windows Server 2008 Standard 或 Enterprise (32 位元或 64 位元)</p></li>
<li><p>Windows Server 2008 Datacenter RTM 或更新版本</p></li>
<li><p>Windows Server 2003 Standard Edition Service Pack 2 (SP2) 或更新版本 (32 位元或 64 位元)</p></li>
<li><p>Windows Server 2003 Enterprise Edition SP2 或更新版本 (32 位元或 64 位元)</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>通用類別目錄伺服器</p></td>
<td><p>在您計劃安裝 Exchange 2013 的每個 Active Directory 站台中，必須至少有一個執行下列其中一個軟體的通用類別目錄伺服器：</p>
<ul>
<li><p>Windows Server 2012 R2 Standard 或 Datacenter1</p></li>
<li><p>Windows Server 2012 Standard 或 Datacenter</p></li>
<li><p>Windows Server 2008 R2 Standard 或 Enterprise</p></li>
<li><p>Windows Server 2008 R2 Datacenter RTM 或更新版本</p></li>
<li><p>Windows Server 2008 Standard 或 Enterprise (32 位元或 64 位元)</p></li>
<li><p>Windows Server 2008 Datacenter RTM 或更新版本</p></li>
<li><p>Windows Server 2003 Standard Edition Service Pack 2 (SP2) 或更新版本 (32 位元或 64 位元)</p></li>
<li><p>Windows Server 2003 Enterprise Edition SP2 或更新版本 (32 位元或 64 位元)</p></li>
</ul>
<p>如需通用類別目錄伺服器的詳細資訊，請參閱<a href="http://go.microsoft.com/fwlink/p/?linkid=178996">什麼是通用類別目錄</a>。</p></td>
</tr>
<tr class="odd">
<td><p>網域控制站</p></td>
<td><p>在您計劃安裝 Exchange 2013 的每個 Active Directory 站台中，至少必須有一部執行下列其中一項的可寫入網域控制站：</p>
<ul>
<li><p>Windows Server 2012 R2 Standard 或 Datacenter1</p></li>
<li><p>Windows Server 2012 Standard 或 Datacenter</p></li>
<li><p>Windows Server 2008 R2 Standard 或 Enterprise SP1 或更新版本</p></li>
<li><p>Windows Server 2008 R2 Datacenter RTM 或更新版本</p></li>
<li><p>Windows Server 2008 Standard 或 Enterprise SP1 或更新版本 (32 位元或 64 位元)</p></li>
<li><p>Windows Server 2008 Datacenter RTM 或更新版本</p></li>
<li><p>Windows Server 2003 Standard Edition Service Pack 2 (SP2) 或更新版本 (32 位元或 64 位元)</p></li>
<li><p>Windows Server 2003 Enterprise Edition SP2 或更新版本 (32 位元或 64 位元)</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Active Directory 樹系</p></td>
<td><p>Active Directory 必須位於 Windows Server 2003 樹系功能模式或更高2。</p></td>
</tr>
<tr class="odd">
<td><p>DNS 命名空間支援</p></td>
<td><p>Exchange 2013 支援下列網域名稱系統 (DNS) 命名空間：</p>
<ul>
<li><p>連續</p></li>
<li><p>不連續</p></li>
<li><p>單一標籤網域</p></li>
<li><p>斷續</p></li>
</ul>
<p>如需有關 Exchange 所支援 DNS 命名空間的詳細資訊，請參閱 Microsoft 知識庫文章 2269838：<a href="http://go.microsoft.com/fwlink/?linkid=3052%26kbid=2269838">單一標籤網域、斷續命名空間和不連續命名空間與 Microsoft Exchange 的相容性</a>。</p></td>
</tr>
<tr class="even">
<td><p>IPv6 支援</p></td>
<td><p>在 Exchange 2013 中，只有同時安裝並啟用 IPv4 時才會支援 IPv6。如果在此組態中部署 Exchange 2013，且網路支援 IPv4 和 IPv6，則所有 Exchange 伺服器都可以對使用 IPv6 位址的裝置、伺服器及用戶端傳送和接收資料。如需詳細資訊，請參閱 <a href="ipv6-support-in-exchange-2013-exchange-2013-help.md">Exchange 2013 中的 IPv6 支援</a>。</p></td>
</tr>
</tbody>
</table>


1   只有 Exchange 2013 SP1 或更新版本支援 Windows Server 2012 R2。

2   只有 Exchange 2013 SP1 或更新版本支援 Windows Server 2012 R2 樹系功能模式。

## 目錄伺服器架構

使用 64 位元的 Active Directory 網域控制站能夠提高 Exchange 2013 的目錄服務效能。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在多網域環境中，於 Active Directory 語言地區設定設為日文的 Windows Server 2008 網域控制站上，伺服器可能無法接收於輸入複寫期間儲存在物件上的某些屬性。如需詳細資訊，請參閱 Microsoft 知識庫文章 949189：<a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=949189">設定為日文語言地區設定的 Windows Server 2008 網域控制站，可能無法在輸入複寫期間將更新套用至物件上的屬性</a>。</td>
</tr>
</tbody>
</table>


## 在目錄伺服器上安裝 Exchange 2013

基於安全和效能原因，我們建議您只將 Exchange 2013 安裝在成員伺服器上，而不要安裝在 Active Directory 目錄伺服器上。不過，您不能在執行 Exchange 2013 的電腦上執行 DCPromo。安裝 Exchange 2013 之後，就不支援將它的角色從成員伺服器變更為目錄伺服器，反之亦然。

## 硬體

Exchange 2013 伺服器的建議硬體需求會因許多因素而有所不同，這些因素包括安裝的伺服器角色，以及將放在伺服器上的預期負載。

如需如何適當地調整大小及設定部署的詳細資訊，請參閱 [Exchange 2013 大小和設定建議](exchange-2013-sizing-and-configuration-recommendations-exchange-2013-help.md)。

如需虛擬環境中部署 Exchange 的資訊，請參閱[Exchange 2013 虛擬化](exchange-2013-virtualization-exchange-2013-help.md)。

**Exchange 2013 的硬體需求**


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>元件</th>
<th>需求</th>
<th>附註</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>處理器</p></td>
<td><ul>
<li><p>x64 架構電腦與 Intel 處理器 (支援 Intel 64 架構，以前稱為 Intel EM64T)</p></li>
<li><p>AMD 處理器 (支援 AMD64 平台)</p></li>
<li><p>不支援 Intel Itanium IA64 處理器</p></li>
</ul></td>
<td><p>請參閱此主題後的「作業系統」章節以瞭解支援的作業系統。</p></td>
</tr>
<tr class="even">
<td><p>記憶體</p></td>
<td><p>視所安裝的 Exchange 角色而有所不同：</p>
<ul>
<li><p><strong>信箱：</strong>最低 8GB</p></li>
<li><p><strong>用戶端存取：</strong>最低 4GB</p></li>
<li><p><strong>信箱與用戶端存取合計：</strong>最低 8GB</p></li>
<li><p><strong>Edge Transport：</strong>最低 4GB</p></li>
</ul></td>
<td><p>無。</p></td>
</tr>
<tr class="odd">
<td><p>分頁檔大小</p></td>
<td><p>分頁檔大小上限和下限必須設定為實體 RAM 加 10 MB，如果您使用超過 32 GB 的 RAM，大小上限為 32778MB。</p></td>
<td><p>如需詳細的分頁檔建議，請參閱＜<a href="exchange-2013-sizing-and-configuration-recommendations-exchange-2013-help.md">Exchange 2013 大小和設定建議</a>＞中的＜分頁檔＞一節。</p></td>
</tr>
<tr class="even">
<td><p>磁碟空間</p></td>
<td><ul>
<li><p>安裝 Exchange 的磁碟至少要 30 GB</p></li>
<li><p>您計劃要安裝的每個整合通訊 (UM) 語言套件，都需要額外 500 MB 的可用磁碟空間</p></li>
<li><p>系統磁碟上有 200 MB 的可用磁碟空間</p></li>
<li><p>儲存郵件佇列資料庫的硬碟擁有至少 500 MB 可用空間。</p></li>
</ul></td>
<td><p>如需儲存建議的詳細資訊，請參閱 <a href="exchange-2013-storage-configuration-options-exchange-2013-help.md">Exchange 2013 儲存裝置組態選項</a>。</p></td>
</tr>
<tr class="odd">
<td><p>磁碟機</p></td>
<td><p>本機或透過網路存取的 DVD-ROM 光碟機</p></td>
<td><p>無。</p></td>
</tr>
<tr class="even">
<td><p>螢幕解析度</p></td>
<td><p>1024 x 768 像素以上</p></td>
<td><p>無。</p></td>
</tr>
<tr class="odd">
<td><p>檔案格式</p></td>
<td><p>磁碟分割格式為 NTFS 檔案系統，適用於下列磁碟分割：</p>
<ul>
<li><p>系統磁碟分割</p></li>
<li><p>儲存 Exchange 二進位檔或 Exchange 診斷記錄所產生之檔案的磁碟分割</p></li>
</ul>
<p>包含下列檔案類型的磁碟分割可以格式化成 ReFS：</p>
<ul>
<li><p>包含交易記錄檔的磁碟分割</p></li>
<li><p>包含資料庫檔案的磁碟分割</p></li>
<li><p>包含內容索引檔案的磁碟分割</p></li>
</ul></td>
<td><p>無。</p></td>
</tr>
</tbody>
</table>


## 作業系統

下表列出 Exchange 2013 所支援的作業系統。

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>我們不支援在執行 Windows Server Core 模式的電腦上安裝 Exchange 2013。電腦需執行 Windows Server 的完整安裝。若您想要在執行 Windows Server Core 模式的電腦上安裝 Exchange 2013，需透過下列方法將伺服器轉換為 Windows Server 的完整安裝：
<ul>
<li><p><strong>Windows Server 2008 R2：</strong>重新安裝 Windows Server 並選擇 [完整安裝] 選項。</p></li>
<li><p><strong>Windows Server 2012 R2</strong> 或 <strong>Windows Server 2012：</strong>執行下列指令，將您的 Windows Server Core 模式伺服器轉換為完整安裝。</p>
<pre><code>Install-WindowsFeature Server-Gui-Mgmt-Infra, Server-Gui-Shell -Restart</code></pre></li>
</ul></td>
</tr>
</tbody>
</table>


**Exchange 2013 所支援的作業系統**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>元件</th>
<th>需求</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mailbox server role、Client Access server role 和 Edge Transport server role</p></td>
<td><p>下列其中一項：</p>
<ul>
<li><p>Windows Server 2012 R2 Standard 或 Datacenter1</p></li>
<li><p>Windows Server 2012 Standard 或 Datacenter</p></li>
<li><p>Windows Server 2008 R2 Standard 與 Service Pack 1 (SP1)</p></li>
<li><p>Windows Server 2008 R2 Enterprise 與 Service Pack 1 (SP1)</p></li>
<li><p>Windows Server 2008 R2 Datacenter RTM 或更新版本</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>管理工具</p></td>
<td><p>下列其中一項：</p>
<ul>
<li><p>Windows Server 2012 R2 Standard 或 Datacenter1</p></li>
<li><p>Windows Server 2012 Standard 或 Datacenter</p></li>
<li><p>Windows Server 2008 R2 Standard 與 SP1</p></li>
<li><p>Windows Server 2008 R2 Enterprise 與 SP1</p></li>
<li><p>Windows Server 2008 R2 Datacenter RTM 或更新版本</p></li>
<li><p>64 位元版本的 Windows 8.12</p></li>
<li><p>64 位元版本的 Windows 8</p></li>
<li><p>64 位元版本的 Windows 7 與 Service Pack 1</p></li>
</ul></td>
</tr>
</tbody>
</table>


1   只有 Exchange 2013 SP1 或更新版本支援 Windows Server 2012 R2。

2   只有 Exchange 2013 SP1 或更新版本支援 Windows 8.1。

**Exchange 2013 支援的 Windows Management Framework 版本**

Exchange 2013 僅支援您要安裝 Exchange 的 Windows 版本中所內建的 Windows 管理架構版本。請勿安裝在執行 Exchange 的伺服器上做為獨立下載項目提供的 Windows 管理架構版本。

## .NET Framework

強烈建議您使用最新版的 .NET Framework，但您正要安裝的 Exchange 版本必須支援此版本。


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
<th>Exchange 版本</th>
<th>.NET Framework 4.7.1</th>
<th>.NET Framework 4.6.2</th>
<th>.NET Framework 4.6.1</th>
<th>.NET Framework 4.5.2</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2013 CU19</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013 CU16 - CU18</p></td>
<td><p></p></td>
<td><p> X</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## 支援的用戶端

Exchange 2013支援下列版本的 Outlook 和 Entourage for Mac：

  - Outlook 2016

  - Outlook 2013

  - Outlook 2010

  - Outlook 2007

  - Entourage 2008 for Mac，Web Services Edition

  - Outlook for Mac for Office 365

  - Outlook for Mac 2011

如需 Exchange 支援的 Outlook 版本清單，請參閱 [Outlook 更新](https://go.microsoft.com/fwlink/p/?linkid=513459)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>強烈建議您安裝可用的最新版 Service Packs 與更新，才能讓您的使用者在連接至 Exchange 時獲得最佳使用體驗。</td>
</tr>
</tbody>
</table>


不支援使用早於 Outlook 2007 的 Outlook 用戶端。不支援需要 DAV 的 Mac 作業系統電子郵件用戶端，例如 Entourage 2008 for Mac RTM 以及 Entourage 2004。

Outlook Web App 支援各作業系統與裝置中的各種瀏覽器。如需詳細資料，請參閱[Exchange 2013 中 Outlook Web App 的新功能](what-s-new-for-outlook-web-app-in-exchange-2013-exchange-2013-help.md)。

