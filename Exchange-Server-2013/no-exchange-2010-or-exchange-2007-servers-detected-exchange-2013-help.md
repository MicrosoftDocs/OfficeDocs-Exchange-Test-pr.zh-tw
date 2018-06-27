---
title: '沒有 Exchange 2010 或 Exchange 2007 伺服器偵測到: Exchange 2013 Help'
TOCTitle: 沒有 Exchange 2010 或 Exchange 2007 伺服器偵測到
ms:assetid: 789cabab-c769-4a16-a6c8-3db82cff8861
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.noe14serverwarning(v=EXCHG.150)
ms:contentKeyID: 50473536
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 沒有 Exchange 2010 或 Exchange 2007 伺服器偵測到

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2012-11-08_

因為沒有Exchange Server 2010或Exchange Server 2007伺服器角色存在於組織中 Microsoft Exchange Server 2013安裝程式會顯示這個警告。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您繼續執行Exchange Server 2013安裝，您將不能夠Exchange 2010或Exchange 2007伺服器新增至未來組織。</td>
</tr>
</tbody>
</table>


在部署之前Exchange 2013、 考慮可能需要您部署Exchange 2010或Exchange 2007伺服器後的再部署Exchange 2013下列因素：

  - **協力廠商或內部開發的應用程式**  舊版 Exchange 的應用程式可能無法與Exchange 2013相容。您可能需要維護Exchange 2010或Exchange 2007伺服器可支援這些應用程式。

  - **共存或遷移的需求**  如果您打算將信箱移轉至您的組織，某些解決方案可能需要使用Exchange 2010或Exchange 2007伺服器。

如果您決定需要部署Exchange 2010或Exchange 2007伺服器，您必須先進行安裝部署Exchange 2013。必須以下列順序每個 Exchange 版本準備 active Directory：

1.  Exchange 2007

2.  Exchange 2010

3.  Exchange 2013

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

找到您要的資訊了嗎？請撥冗[提供您的意見](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac)讓我們知道您需要什麼資訊。

