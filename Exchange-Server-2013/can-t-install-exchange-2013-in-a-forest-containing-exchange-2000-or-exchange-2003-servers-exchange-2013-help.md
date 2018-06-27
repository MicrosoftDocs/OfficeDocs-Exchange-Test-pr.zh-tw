---
title: '無法在 Exchange 2000 或 Exchange 2003 伺服器所在樹系中安裝 Exchange 2013。: Exchange 2013 Help'
TOCTitle: 無法在 Exchange 2000 或 Exchange 2003 伺服器所在樹系中安裝 Exchange 2013。
ms:assetid: a115b182-cbd2-4d31-aa0e-375240939301
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.exchange2000or2003presentinorg(v=EXCHG.150)
ms:contentKeyID: 50473856
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 無法在 Exchange 2000 或 Exchange 2003 伺服器所在樹系中安裝 Exchange 2013。

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2016-12-09_

Microsoft Exchange Server 2013無法繼續因為 Active Directory 樹系中找不到執行Exchange 2000 Server或Exchange Server 2003的一或多部電腦。您可以安裝Exchange 2013之前，所有Exchange 2000和Exchange 2003伺服器必須先都移除樹系。信箱、 公用資料夾及所有其他 Exchange 物件或元件必須升級至Exchange Server 2007或Exchange Server 2010。您無法從Exchange 2000或Exchange 2003將直接升級至Exchange 2013。

您必須遵循在組織中安裝Exchange 2013的路徑取決於您目前已安裝在您的樹系中的 Exchange 版本。請參閱下的表如需詳細資訊。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>如果您在組織中安裝了下列項目</th>
<th>您必須根據此路徑升級至 Exchange 2013</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2000</p></td>
<td><ol>
<li><p>將 Exchange 2007 安裝至 Exchange 2000 組織。</p></li>
<li><p>設定 Exchange 2007 與 Exchange 2000 共存。</p></li>
<li><p>將 Exchange 2000 信箱、公用資料夾和其他元件遷移至 Exchange 2007。</p></li>
<li><p>解除委任並移除所有 Exchange 2000 伺服器。</p></li>
<li><p>將 Exchange 2013 安裝至 Exchange 2007 組織。</p></li>
<li><p>設定 Exchange 2013 與 Exchange 2007 共存。</p></li>
<li><p>將 Exchange 2007 信箱、公用資料夾和其他元件遷移至 Exchange 2013。</p></li>
<li><p>解除委任並移除所有 Exchange 2007 伺服器。</p></li>
</ol>
<p>如需詳細資訊，請參閱<a href="https://go.microsoft.com/fwlink/p/?linkid=103281">升級至 Exchange 2007</a>和<a href="upgrade-from-exchange-2007-to-exchange-2013-exchange-2013-help.md">從 Exchange 2007 升級至 Exchange 2013</a>。</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2003</p></td>
<td><ol>
<li><p>將 Exchange 2010 安裝至 Exchange 2003 組織。</p></li>
<li><p>設定 Exchange 2010 與 Exchange 2003 共存。</p></li>
<li><p>將 Exchange 2003 信箱、公用資料夾和其他元件遷移至 Exchange 2010。</p></li>
<li><p>解除委任並移除所有 Exchange 2003 伺服器。</p></li>
<li><p>將 Exchange 2013 安裝至 Exchange 2010 組織。</p></li>
<li><p>設定 Exchange 2013 與 Exchange 2010 共存。</p></li>
<li><p>將 Exchange 2010 信箱、公用資料夾和其他元件遷移至 Exchange 2013。</p></li>
<li><p>解除委任並移除所有 Exchange 2010 伺服器。</p></li>
</ol>
<p>如需詳細資訊，請參閱<a href="https://go.microsoft.com/fwlink/p/?linkid=268414">Exchange 2003-規劃升級及共存的藍圖</a>和<a href="upgrade-from-exchange-2010-to-exchange-2013-exchange-2013-help.md">從 Exchange 2010 升級至 Exchange 2013</a>。</p></td>
</tr>
</tbody>
</table>


升級至Exchange 2010或Exchange 2013，您可以使用 Exchange 部署助理可協助您完成您的部署。如需詳細資訊，請參閱下列連結：

  - [Exchange 2010 部署助理](https://go.microsoft.com/fwlink/p/?linkid=171086)

  - [Exchange 2013 部署助理](https://go.microsoft.com/fwlink/p/?linkid=277105)

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

找到您要的資訊了嗎？請撥冗[提供您的意見](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac)讓我們知道您需要什麼資訊。

