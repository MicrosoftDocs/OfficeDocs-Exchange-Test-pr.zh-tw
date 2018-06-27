---
title: '存取公用資料夾與 Outlook 2016 for Mac: Exchange Online Help'
TOCTitle: 存取公用資料夾與 Outlook 2016 for Mac
ms:assetid: bc9b8226-bd8b-4edc-882b-4f19cfe118eb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Mt788631(v=EXCHG.150)
ms:contentKeyID: 74115367
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 存取公用資料夾與 Outlook 2016 for Mac

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016, Office 365_

_**上次修改主題的時間：**2017-05-19_

**摘要：** 支援的最新的 Exchange 拓撲可讓使用者可以存取公用資料夾與 Outlook 2016 for mac。

使用 Mac 用戶端版本的 Outlook 2016[年 4 月 2016年更新](https://go.microsoft.com/fwlink/?linkid=829202) 、 Exchange 2013[累計更新 14 (CU14)](https://go.microsoft.com/fwlink/p/?linkid=849432)與[累計更新 2 (CU 2)](https://go.microsoft.com/fwlink/p/?linkid=849793) for Exchange 2016、 Outlook 2016 for Mac 中的使用者現在已可存取多個類型的拓撲中的公用資料夾比他們無法再。

## Outlook for Mac 限制

所有版本的 Outlook for Mac 可都存取 Exchange 公用資料夾，但直到最近這些用戶端無法都存取下列部署案例中的公用資料夾：

  - **與舊版公用資料夾並行。**Exchange 2013 或 Exchange 2016 伺服器上的使用者信箱時，使用者無法使用 Outlook for Mac 來存取公用資料夾部署在伺服器執行 Exchange 2010 SP3 或更新版本。其他用戶端可以存取這些在此案例中的舊版公用資料夾。

  - **混合式拓撲。**與基礎 in Exchange Online 信箱的內部部署使用者無法使用 Outlook for Mac 來存取內部部署摩登的公用資料夾。同樣地，與 Exchange 2013 或 Exchange 2016 信箱的內部使用者無法使用 Outlook for Mac 存取公用資料夾部署在 Exchange Online。

## Outlook 2016 for Mac

Mac，以及 CU14 for Exchange 2013 和 Exchange 2016 的 CU2 的 Outlook 2016 年 4 月 2016年更新，上述情況現在可 Mac 用戶端的 Outlook 2016 運作。

下表摘要 Mac 用戶端嘗試存取 Exchange 2013、 Exchange 2016 和 Exchange Online 公用資料夾的使用者與 Outlook 2016 支援的拓撲。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>下表所示的案例假設 for Mac Outlook 2016 年 4 月 2016年更新已套用至所有用戶端。</td>
</tr>
</tbody>
</table>



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
<th>公用資料夾部署在...]</th>
<th>使用者信箱已在 Exchange 2010 SP3 或更新版本</th>
<th>使用者信箱已在 Exchange 2013 CU13 或更新版本</th>
<th>使用者信箱已在 Exchange 2016 CU2 或更新版本</th>
<th>使用者信箱處於 [Office 365/Exchange Online</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Server 2010 SP3 或更新版本</p></td>
<td><p>支援</p></td>
<td><p>支援</p></td>
<td><p>支援</p></td>
<td><p>不支援</p></td>
</tr>
<tr class="even">
<td><p>Exchange Server 2013 CU13 或更新版本</p></td>
<td><p>不支援</p></td>
<td><p>支援</p></td>
<td><p>支援</p></td>
<td><p>支援</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server 2016 CU2 或更新版本</p></td>
<td><p>不支援</p></td>
<td><p>支援</p></td>
<td><p>支援</p></td>
<td><p>支援</p></td>
</tr>
<tr class="even">
<td><p>Office 365 / Exchange Online</p></td>
<td><p>不支援</p></td>
<td><p>支援</p></td>
<td><p>支援</p></td>
<td><p>支援</p></td>
</tr>
</tbody>
</table>


下列文章說明如何部署共存或混合式拓撲中部署 Exchange 組織中的公用資料夾。為您的 Outlook 2016 Mac 用戶端安裝年 4 月 2016年更新，他們將能夠存取這些文章中所詳述的組態中的公用資料夾：

  - [使用者信箱位於 Exchange 2013 伺服器上時設定舊版公用資料夾](configure-legacy-public-folders-where-user-mailboxes-are-on-exchange-2013-servers-exchange-2013-help.md)

  - [設定混合式部署的 Exchange 2013 公用資料夾](configure-exchange-2013-public-folders-for-a-hybrid-deployment-exchange-2013-help.md)

  - [設定 Exchange Online 公用資料夾以進行混合部署](configure-exchange-online-public-folders-for-a-hybrid-deployment-exchange-2013-help.md)

