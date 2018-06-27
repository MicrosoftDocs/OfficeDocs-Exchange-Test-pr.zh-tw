---
title: '與 Office Communications Server 2007 R2 和 Lync Server 共存: Exchange 2013 Help'
TOCTitle: 與 Office Communications Server 2007 R2 和 Lync Server 共存
ms:assetid: f12d65c7-0b2c-46a1-a14a-802a76296fa1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ851069(v=EXCHG.150)
ms:contentKeyID: 50554105
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 與 Office Communications Server 2007 R2 和 Lync Server 共存

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2015-03-09_

Communications Server 2007 R2 和 Lync Server 提供許多使用者功能，包括立即訊息 (IM)、 目前狀態、 多方 IM 和其語音信箱功能整合與 Exchange 整合通訊 (UM)。整合 Lync Server 2010 或 2013年的部署，使用者可以啟用 Enterprise voice，可讓使用者啟用語音信箱存取其語音郵件使用 Lync Server 元件。

當您整合 UM 與舊版 Office Communications Server 或 Lync Server 時，不是所有可用功能。為完全利用新增強的使用者功能，例如高解析度相片、 整合連絡人存放區，以及 Lync Archiving 整合的使用者，他們必須使用者帳戶的 Lync Server 2013 與Exchange Server 2013，而且必須使用 Lync 2013 用戶端軟體的最新版本。例如，整合連絡人存放區無法使用已啟用 Lync Server 2010 Enterprise Voice 的使用者。此外，高解析度相片無法顯示在 Lync 2010。

當您正在 Office Communications Server 2007 R2 或 Lync Server 2010 與 Exchange UM 整合時，您可能需要在已部署在組織中的 Office Communications Server 2007 R2 或 Lync 2010 伺服器上安裝其他 hotfix、 彙總套件、 累計更新及 service pack。您是安裝所需取決於您的部署拓撲與您要與 Exchange UM 整合的產品版本。

## 必要的 hotfix、 彙總套件、 累計更新及 service pack

下表顯示修正所需的每個與 UM 整合的產品版本。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Office Communications Server 2007 R2</p></td>
<td><p>Office Communications Server 2007 R2 的累計 10 或更新版本。</p></td>
</tr>
<tr class="even">
<td><p>Lync Server 2010</p></td>
<td><p>Lync Server 2010 累計更新 3 或更新版本。</p></td>
</tr>
<tr class="odd">
<td><p>Lync Server 2013</p></td>
<td><p>未更新是必要的。</p></td>
</tr>
</tbody>
</table>

