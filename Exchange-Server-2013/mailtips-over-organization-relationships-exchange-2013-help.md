---
title: '透過組織關聯性的郵件提示: Exchange Online Help'
TOCTitle: 透過組織關聯性的郵件提示
ms:assetid: 1784256f-abe1-4503-b8c4-26d544b73452
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ670165(v=EXCHG.150)
ms:contentKeyID: 50472687
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 透過組織關聯性的郵件提示

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

Microsoft Exchange Server 2013可讓您設定 Microsoft Exchange Online 或其他Exchange組織的組織關係。建立組織關聯性可讓您有其他組織處理時提升使用者經驗。例如，您可以共用空閒或忙碌資料、 設定安全的郵件流程及啟用跨兩個組織的郵件追蹤。

## 控制郵件提示存取層級

若要限制特定類型的郵件提示。您也可以讓所有的郵件提示會傳回或允許只有一組有限的一般防止 Ndr。您可以搭配*MailTipsAccessLevel*參數**Set-OrganizationRelationship**指令程式上設定此設定。下表顯示的郵件提示會傳回透過組織關聯性。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>郵件提示</th>
<th>存取層級設為 [所有] 時 MailTip 是否可用？</th>
<th>存取層級設為 [有限] 時 MailTip 是否可用？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>大型對象</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>自動回覆</p></td>
<td><p>是</p>
<p>若為內部指定收件者的遠端網域，則會顯示內部的自動回覆。否則會顯示外部的自動回覆。</p></td>
<td><p>是</p>
<p>顯示外部自動回覆。</p></td>
</tr>
<tr class="odd">
<td><p>仲裁收件者</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>超過大小的郵件</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>限制的收件者</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>信箱已滿</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>自訂郵件提示</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>外部收件者</p></td>
<td><p>是</p>
<p>如果指定做為內部收件者的遠端網域，則會隱藏此郵件提示。否則會傳回 「 外部 」 郵件提示。</p></td>
<td><p>是</p>
<p>如果指定做為內部收件者的遠端網域，則會隱藏此郵件提示。否則會傳回 「 外部 」 郵件提示。</p></td>
</tr>
</tbody>
</table>


如需如何設定郵件提示存取層級的詳細步驟，請參閱[管理郵件提示的組織關係](manage-mailtips-for-organization-relationships-exchange-2013-help.md)。

## 控制郵件提示存取範圍

如果您啟用組織關聯性上的 \[寄件提醒設定的存取層級`All`、 特定收件者的寄件提醒、 信箱已滿、 自動回覆及自訂郵件提示時，會傳回所有使用者。不過，您可能只想允許這些寄件提醒的一組特定的使用者。例如，如果您與協力廠商設定組織關聯性，您可能要允許這些郵件提示僅針對該夥伴與搭配使用的使用者。

若要達到此目的，您需要先建立群組並新增您要共用特定收件者的寄件提醒給該群組的所有使用者。然後您可以指定該群組組織關聯性。

實作此限制之後，您的用戶端存取伺服器會先確認其時收到的郵件提示查詢的收件者是否屬於此群組。如果收件者是此群組的成員，用戶端存取伺服器會回復 proxy 包括特定收件者的寄件提醒的所有郵件提示。否則他們將不會在其回應中包含特定收件者的郵件提示。

如需如何設定郵件提示存取層級的詳細步驟，請參閱[管理郵件提示的組織關係](manage-mailtips-for-organization-relationships-exchange-2013-help.md)。

