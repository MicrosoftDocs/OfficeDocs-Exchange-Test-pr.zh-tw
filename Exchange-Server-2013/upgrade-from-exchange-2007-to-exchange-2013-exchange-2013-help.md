---
title: '從 Exchange 2007 升級至 Exchange 2013: Exchange 2013 Help'
TOCTitle: 從 Exchange 2007 升級至 Exchange 2013
ms:assetid: a604b96d-2a51-480f-937f-45ad753c2cad
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ898581(v=EXCHG.150)
ms:contentKeyID: 51409229
ms.date: 01/01/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 從 Exchange 2007 升級至 Exchange 2013

 

_**適用版本：**Exchange Online, Exchange Server, Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

Microsoft Exchange Server 2010 和 Exchange Server 2007 具有多個伺服器角色：Client Access、Mailbox、Hub Transport、Unified Messaging 和 Edge Transport。在 Exchange Server 2013 中，我們將伺服器角色的數量從五個減少為三個：Client Access、Mailbox 和 Edge Transport。目前，整合通訊被視為一種元件或 Exchange 2013 中提供之語音相關功能的子功能。(如需相關變更的詳細資訊，請參閱 [Exchange 2013 的新功能](what-s-new-in-exchange-2013-exchange-2013-help.md)中的「Exchange 2013 架構」。)

將現有的 Exchange 2007 組織升級至 Exchange 2013 時，Exchange 2007 和 Exchange 2013 伺服器會有一段時間在組織內共存。您可以無限期保有此模式，或將所有資源從 Exchange 2013 移至 Exchange 2007，再解除 Exchange 2013 伺服器的委派，就可立即完成 Exchange 2007 升級程序。若下列條件成立，就有共存的條件：

  - Exchange 2013 可部署在現有的 Exchange 組織中。

  - 有多個 Microsoft Exchange 版本可為組織提供郵件服務。

您無法將現有的 Exchange 2003 組織直接升級至 Exchange 2013。您必須先將 Exchange 2003 組織升級至 Exchange 2007 或 Exchange 2010 組織，然後才能將 Exchange 2007 或 Exchange 2010 組織升級至 Exchange 2013。我們建議您先將組織從 Exchange 2003 升級至 Exchange 2010，然後再從 Exchange 2010 升級至 Exchange 2013。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您必須先將 Exchange 2003 的所有執行個體都從組織中移除，才能升級至 Exchange 2013。</td>
</tr>
</tbody>
</table>


您可以將所有的 Exchange 2003 信箱都移轉至 Exchange Online。如需此方法的詳細資訊，請參閱[將多個電子郵件帳戶移轉至 Office 365 的方法](https://go.microsoft.com/fwlink/p/?linkid=524030)。

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

## Exchange 2013 和 Exchange 2007 與 Exchange 2010 的混合模式共存

如果 Active Directory 站台同時安裝了 Exchange 2010 和 Exchange 2007，請同時遵循 Exchange 2010 和 Exchange 2007 的升級指示，然後執行兩者所需的升級步驟。

## 升級程序的概觀

為協助您概略了解從 Exchange 2007 升級至 Exchange 2013 的程序，我們在下表中收集各項主要工作的相關資源。如需逐步指引，請參閱[檢查清單：從 Exchange 2007 升級](checklist-upgrade-from-exchange-2007-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>工作</th>
<th>主題</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>深入了解 Exchange 2013 角色和元件</p></td>
<td><p><a href="what-s-new-in-exchange-2013-exchange-2013-help.md">Exchange 2013 的新功能</a></p>
<p><a href="client-access-server-exchange-2013-help.md">Client Access server</a></p>
<p><a href="mailbox-server-exchange-2013-help.md">信箱伺服器</a></p>
<p><a href="mail-flow-exchange-2013-help.md">郵件流程</a></p>
<p><a href="unified-messaging-exchange-2013-help.md">整合通訊</a></p></td>
</tr>
<tr class="even">
<td><p>安裝 Exchange 2013</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">使用安裝精靈安裝 Exchange 2013</a></p>
<p><a href="install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md">使用設定精靈安裝 Exchange 2013 Edge Transport role</a> (選用)</p>
<p><a href="verify-an-exchange-2013-installation-exchange-2013-help.md">確認 Exchange 2013 安裝</a></p></td>
</tr>
<tr class="odd">
<td><p>在 Client Access Server 上新增數位憑證</p></td>
<td><p><a href="exchange-2013-client-access-server-configuration-exchange-2013-help.md">Exchange 2013 用戶端存取伺服器組態</a></p>
<p><a href="digital-certificates-and-ssl-exchange-2013-help.md">數位憑證和 SSL</a></p>
<p><a href="create-a-digital-certificate-request-exchange-2013-help.md">建立數位憑證要求</a></p></td>
</tr>
<tr class="even">
<td><p>設定 Exchange 相關虛擬目錄</p></td>
<td><p><a href="default-settings-for-exchange-virtual-directories-exchange-2013-help.md">Exchange 虛擬目錄的預設設定</a></p></td>
</tr>
<tr class="odd">
<td><p>從 Exchange 2010 移動信箱</p></td>
<td><p><a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">在 Exchange 2013 移動信箱</a></p></td>
</tr>
<tr class="even">
<td><p>設定傳輸元件</p></td>
<td><p><a href="edge-subscriptions-exchange-2013-help.md">Edge 訂閱</a> (只在已安裝 Edge Transport Server 時才需要)</p>
<p><a href="mail-routing-exchange-2013-help.md">郵件路由</a></p>
<p><a href="shadow-redundancy-exchange-2013-help.md">陰影備援</a></p>
<p><a href="delivery-reports-for-administrators-exchange-2013-help.md">系統管理員的傳遞回報</a></p></td>
</tr>
<tr class="odd">
<td><p>設定與部署 UM</p></td>
<td><p><a href="planning-for-unified-messaging-exchange-2013-help.md">整合通訊的規劃</a></p>
<p><a href="deploying-voice-mail-and-um-exchange-2013-help.md">部署語音信箱和 UM</a></p></td>
</tr>
</tbody>
</table>

