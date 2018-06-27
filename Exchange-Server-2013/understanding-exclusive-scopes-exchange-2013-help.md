---
title: '了解獨佔範圍: Exchange 2013 Help'
TOCTitle: 了解獨佔範圍
ms:assetid: 32492622-3b01-4e3b-8288-ed39525eea75
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd638110(v=EXCHG.150)
ms:contentKeyID: 50472812
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 了解獨佔範圍

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

*獨佔範圍*是可與管理角色指派相關聯的明確的管理範圍的特殊類型。獨佔範圍的設計被用來啟用其中 CEO 信箱，如有高價值物件的群組，而您想要緊密控制哪些人可以存取管理這些物件的情況。

具有獨佔範圍的角色指派稱為\[獨佔角色指派\]。

當您建立獨佔範圍時，只會指派該獨佔範圍或對等的獨佔範圍，可以修改符合範圍的物件。即使他們自己的角色已將否則包括物件的範圍的獨佔範圍或同等群組未指派的角色 assignees 無法修改符合範圍的物件。獨佔範圍會覆寫任何其他一般範圍不是互斥的。此行為就類似於如何拒絕存取控制項目 (ACE) Active Directory存取控制清單 (ACL) 的功能。

*對等的獨佔範圍*參照另一個獨佔範圍符合一些其他的獨佔範圍相同的物件。範圍沒有要比對同一組完整的物件。這兩個範圍可以修改某些，或所有符合他們的物件。

## 建立獨佔範圍

您可以像其他明確的範圍建立獨佔範圍。您可以指定預先建置的相對範圍 ；收件者、 資料庫或伺服器的篩選器。或資料庫或伺服器清單。與一般範圍，不要才能生效關聯至管理角色指派的範圍，不同的獨佔範圍拒絕層面會立即生效。這表示一旦建立獨佔範圍時，物件中包含範圍會立即不再由任何使用者可存取之前已建立角色指派。

建立工作分派之後，獨佔範圍會提供存取權那些指派管理角色與範圍。如果其他對等的獨佔範圍符合相同的物件、 角色指派相關聯獨佔範圍是否仍能夠存取物件。

如需管理範圍篩選的相關資訊，請參閱[了解管理角色範圍篩選器](understanding-management-role-scope-filters-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當對任何管理角色元件 (包括獨佔範圍) 進行變更時，Active Directory 複寫時間應予以考慮。</td>
</tr>
</tbody>
</table>


如果您有包含一個以上的獨佔範圍內的物件時，被指派給任一獨佔範圍提供物件的存取權。如需詳細資訊，請參閱本主題稍後的獨佔和定期領域互動。

獨佔範圍控制僅明確收件者或組態寫入範圍的角色指派。隱含的收件者或組態讀取範圍的角色指派給使用者或群組仍適用於。下列適用於這表示：

  - 指派的角色繼續查看符合角色隱含讀取範圍的物件。

  - 這些指派其他角色可以其他角色的讀取的範圍包括物件包含在獨佔範圍內的物件。不過，物件只能由已指派獨佔範圍相關聯的角色的使用者可以修改。

獨佔範圍只用於與系統管理或專家角色並不能與使用者的角色。如需角色的詳細資訊，請參閱[了解管理角色](understanding-management-roles-exchange-2013-help.md)。

## 獨佔和定期領域互動

本章節的結尾圖說明如何獨佔範圍互動與彼此、 及規則的範圍。圖例中之所有使用者都與其相關聯的下列屬性。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>User</th>
<th>City</th>
<th>Title</th>
<th>Department</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Terry</p></td>
<td><p>溫哥華</p></td>
<td><p>會計</p></td>
<td><p>會計</p></td>
</tr>
<tr class="even">
<td><p>David</p></td>
<td><p>溫哥華</p></td>
<td><p>撰稿人</p></td>
<td><p>行銷</p></td>
</tr>
<tr class="odd">
<td><p>Walter</p></td>
<td><p>溫哥華</p></td>
<td><p>Manager</p></td>
<td><p>行銷</p></td>
</tr>
<tr class="even">
<td><p>Bob</p></td>
<td><p>溫哥華</p></td>
<td><p>CEO</p></td>
<td><p>董事會</p></td>
</tr>
<tr class="odd">
<td><p>Christine</p></td>
<td><p>溫哥華</p></td>
<td><p>總經理</p></td>
<td><p>董事會</p></td>
</tr>
<tr class="even">
<td><p>Fred</p></td>
<td><p>溫哥華</p></td>
<td><p>CFO</p></td>
<td><p>主管</p></td>
</tr>
<tr class="odd">
<td><p>Martin</p></td>
<td><p>溫哥華</p></td>
<td><p>CIO</p></td>
<td><p>主管</p></td>
</tr>
<tr class="even">
<td><p>Kim</p></td>
<td><p>溫哥華</p></td>
<td><p>營運副總經理</p></td>
<td><p>主管</p></td>
</tr>
<tr class="odd">
<td><p>Jennifer</p></td>
<td><p>溫哥華</p></td>
<td><p>技術副總經理</p></td>
<td><p>主管</p></td>
</tr>
</tbody>
</table>


圖中的下列三個管理角色指派管理上表中的使用者。每個具有相關聯的範圍，部份只是獨佔範圍。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>角色指派</th>
<th>範圍篩選器</th>
<th>獨佔或一般</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>收件者系統管理員</p></td>
<td><p>城市 = 溫哥華</p></td>
<td><p>Regular</p></td>
</tr>
<tr class="even">
<td><p>VIP 系統管理員</p></td>
<td><p>職稱 = CEO 或 CFO 或 CIO 或總經理</p></td>
<td><p>獨佔</p></td>
</tr>
<tr class="odd">
<td><p>行政人員系統管理員</p></td>
<td><p>部門 = 行政</p></td>
<td><p>獨佔</p></td>
</tr>
</tbody>
</table>


收件者系統管理員角色指派有因為每個使用者位於 Vancouver 會比對的所有使用者的範圍。沒有任何獨佔範圍，這表示 Recipient Administrators 角色指派可管理的任何使用者。不過，此組織已建立兩個獨佔範圍 ︰ VIP 管理員及高階主管的管理員。這些獨佔範圍限制誰可以管理符合其各自的範圍篩選器的使用者。VIP 系統管理員角色指派具有範圍篩選的比對具有標題 CEO、 CFO、 CIO 或總裁的任何使用者。高階主管的系統管理員角色指派具有範圍篩選符合任何高階主管部門中的使用者。

評估一般範圍和獨佔範圍時，其結果如下：

  - 收件者系統管理員角色指派可管理使用者 Terry、 David，與 Walter。此角色指派無法管理其他使用者的任何符合獨佔範圍篩選器的 VIP 管理員及高階主管的系統管理員角色指派。

  - VIP 系統管理員角色指派可管理 Bob、 Christine、 Fred、 及 Martin 的使用者。這是因為此角色指派相關聯的獨佔範圍篩選符合這些物件的屬性。此角色指派無法管理使用者 Kim 與 Jennifer 因為及其屬性不符合此獨佔範圍。

  - 高階主管的系統管理員角色指派可管理使用者 Kim、 Jennifer、 Fred、 與 Martin。這是因為此角色指派相關聯的獨佔範圍篩選符合這些物件的屬性。此角色指派無法管理使用者 Bob 與 Christine 因為及其屬性不符合此獨佔範圍。

請注意這兩個獨佔範圍來確定 Fred 和 Martin 都可以存取。這是因為這些使用者的屬性與這兩個獨佔範圍的篩選器相符。

**獨佔範圍與一般範圍的互動**

![獨佔和定期領域互動](images/Dd638110.0aa26d1d-1fa6-44d8-802d-83d75cd2624c(EXCHG.150).jpg "獨佔和定期領域互動")

如需管理範圍的相關資訊，請參閱[了解管理角色範圍](understanding-management-role-scopes-exchange-2013-help.md)。

