---
title: '在 Exchange Online 與 Exchange Server 的預設保留原則: Exchange Online Help'
TOCTitle: 預設保留原則
ms:assetid: bcf31b2d-463b-4623-b488-c8ac40f14f62
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn775046(v=EXCHG.150)
ms:contentKeyID: 62625784
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 在 Exchange Online 與 Exchange Server 的預設保留原則

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

Exchange Exchange Online您在建立保留原則預設 MRM 原則和內部Exchange組織。原則會自動套用至Exchange Online中的新使用者。在內部部署組織中，當您建立封存信箱會套用原則。您可以變更套用至使用者隨時保留原則。

您可以修改中預設 MRM 原則，例如包含變更的保留時間或保留動作的標記、 停用標記或修改原則來新增或移除標記。更新的原則會套用至信箱的下次由受管理的資料夾助理員處理

## 連結至預設 MRM 原則的保留標記

下表列出連結至「預設 MRM 原則」的預設保留標記。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>名稱</th>
<th>類型</th>
<th>保留時間 (天)</th>
<th>保留動作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>預設兩年移至封存</p></td>
<td><p>預設原則標記 (DPT)</p></td>
<td><p>730</p></td>
<td><p>移至封存</p></td>
</tr>
<tr class="even">
<td><p>可復原的項目 14 天移至封存</p></td>
<td><p>可復原的項目資料夾</p></td>
<td><p>14</p></td>
<td><p>移至封存</p></td>
</tr>
<tr class="odd">
<td><p>個人 1 年移至封存</p></td>
<td><p>個人標記</p></td>
<td><p>365</p></td>
<td><p>移至封存</p></td>
</tr>
<tr class="even">
<td><p>個人 5 年移至封存</p></td>
<td><p>個人標記</p></td>
<td><p>1,825</p></td>
<td><p>移至封存</p></td>
</tr>
<tr class="odd">
<td><p>個人永不移至封存</p></td>
<td><p>個人標記</p></td>
<td><p>不適用</p></td>
<td><p>移至封存</p></td>
</tr>
<tr class="even">
<td><p>1 週刪除</p></td>
<td><p>個人標記</p></td>
<td><p>7</p></td>
<td><p>刪除並允許復原</p></td>
</tr>
<tr class="odd">
<td><p>1 個月刪除</p></td>
<td><p>個人標記</p></td>
<td><p>30</p></td>
<td><p>刪除並允許復原</p></td>
</tr>
<tr class="even">
<td><p>6 個月刪除</p></td>
<td><p>個人標記</p></td>
<td><p>180</p></td>
<td><p>刪除並允許復原</p></td>
</tr>
<tr class="odd">
<td><p>1 年刪除</p></td>
<td><p>個人標記</p></td>
<td><p>365</p></td>
<td><p>刪除並允許復原</p></td>
</tr>
<tr class="even">
<td><p>5 年刪除</p></td>
<td><p>個人標記</p></td>
<td><p>1,825</p></td>
<td><p>刪除並允許復原</p></td>
</tr>
<tr class="odd">
<td><p>永不刪除</p></td>
<td><p>個人標記</p></td>
<td><p>不適用</p></td>
<td><p>刪除並允許復原</p></td>
</tr>
</tbody>
</table>


## 您可以使用預設 MRM 原則執行的動作


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>您可以...]</th>
<th>在 Exchange Online...]</th>
<th>Exchange Server 中...]</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>自動套用至新的使用者的預設 MRM 原則</p></td>
<td><p>是，會套用預設。不不需要任何動作。</p></td>
<td><p>如果您也可以建立新的使用者的封存可以套用預設。</p>
<p>如果您建立稍後使用者的封存，則會套用原則會自動只有當使用者都不會有現有的保留原則。</p></td>
</tr>
<tr class="even">
<td><p>修改的保留時間或保留標記連結到該原則的保留動作</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>停用保留標記連結到該原則</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>新增至原則的保留標記</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>從原則移除保留標記</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>將另一個原則設為預設保留原則會自動套用至新的使用者</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
</tr>
</tbody>
</table>


## 其他資訊

  - 保留標記可以連結至多個保留原則。如需有關管理[保留標記和保留原則](retention-tags-and-retention-policies-exchange-2013-help.md)的詳細資訊，請參閱[通訊記錄管理程序](messaging-records-management-procedures-exchange-2013-help.md)。

  - 預設 MRM 原則不包含 DPT 自動刪除的項目 （但沒有含有與使用者可套用至信箱項目刪除保留動作的個人標記）。如果您想要在指定期間之後自動刪除項目，您可以建立 DPT 進行必要的刪除動作並將其新增至原則。如需詳細資訊，請參閱[建立保留原則](create-a-retention-policy-exchange-2013-help.md)和[若要保留標記中新增或移除保留標記的保留原則](add-retention-tags-to-or-remove-retention-tags-from-a-retention-policy-exchange-2013-help.md)。

  - 保留原則會套用至信箱使用者。相同的原則會套用至使用者的信箱和封存。

