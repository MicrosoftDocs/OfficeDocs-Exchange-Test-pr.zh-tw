---
title: '授權使用撥號規則的通話: Exchange Online Help'
TOCTitle: 授權使用撥號規則的通話
ms:assetid: 4c18bc07-f55c-42b7-81c1-729878aa93aa
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ898499(v=EXCHG.150)
ms:contentKeyID: 51409192
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 授權使用撥號規則的通話

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2015-03-09_

根據預設，使用者都可以撥撥出電話。若要指定類型的電話使用者可以進行，您先建立撥號規則，然後授權的 UM 撥號對應表、 UM 信箱原則或 UM 自動語音應答上這些撥號規則群組。您可以授權撥號規則群組之前，您必須定義撥號規則上的 UM 撥號對應表。如需詳細資訊，請參閱[建立使用者的撥號規則](create-dialing-rules-for-users-exchange-2013-help.md)。

您建立的每一個撥號規則將會包含的通話類型或您想要授與使用者的號碼模式的存取權。您可以讓不同類型的使用者進行不同類型的通話。允許來電可內的國家或地區\]，或者可以為國際。

若要授權或限制撥號，您必須正確地設定以下項目：

  - **撥號規則**  撥號規則定義已啟用 UM 的使用者撥打的號碼和將寄件者整合通訊與專用交換機 (PBX) 或 IP PBX 所撥打的號碼。您可以建立撥號規則群組藉由新增撥號規則。建立撥號規則群組之後，您將其新增至授權呼叫的國家/地區或國際撥號規則群組的清單。

  - **撥號規則群組**   撥號規則群組決定隸屬於某撥號群組的使用者能撥打的電話類型。

  - **撥號授權**   撥號授權可用來決定要套用的限制，以防止使用者帶來不必要的電話費，或防止使用者撥打長途電話。

## 如何授權撥號規則群組？

您用來授權撥號規則群組取決於您要允許進行撥出電話的來電者的類型。例如，如果您想僅限 Outlook 語音存取使用者會放置在撥出電話，會建立撥號規則，然後授權 UM 信箱原則的 Outlook 語音存取使用者連結至那些撥號規則群組。下表顯示如何將不同類型的來電者授權的通話。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>來電者類型</th>
<th>在這裡授權撥號規則群組</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>撥打 Outlook 語音存取號碼且未輸入 PIN 碼的未驗證通話者。</p></td>
<td><p>UM 撥號對應表。如需詳細資訊，請參閱<a href="authorize-calls-for-users-in-a-dial-plan-exchange-2013-help.md">在 [撥號對應表授權之使用者的通話</a>。</p></td>
</tr>
<tr class="even">
<td><p>撥打 Outlook 語音存取號碼且輸入 PIN 碼的驗證通話者。</p></td>
<td><p>來電者的 UM 信箱原則。如需詳細資訊，請參閱<a href="authorize-calls-for-a-group-of-users-exchange-2013-help.md">授權的使用者群組的電話</a>。</p></td>
</tr>
<tr class="odd">
<td><p>撥打設定於 UM 自動語音應答上之電話號碼的未驗證通話者</p></td>
<td><p>UM 自動語音應答。如需詳細資訊，請參閱<a href="authorize-calls-for-auto-attendant-callers-exchange-2013-help.md">自動語音應答來電者的授權的通話</a>。</p></td>
</tr>
</tbody>
</table>


根據要授與撥出電話之權限的使用者，您可以在 Exchange 系統管理中心 (EAC) 中使用 **\[撥號授權\]** 頁面來設定撥號對應表、自動語音應答及 UM 信箱原則。

