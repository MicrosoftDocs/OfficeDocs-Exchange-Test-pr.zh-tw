---
title: 'DSN 郵件識別碼: Exchange 2013 Help'
TOCTitle: DSN 郵件識別碼
ms:assetid: 70ffba22-e4fd-4cd3-98f5-8bfca2df89e4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa998835(v=EXCHG.150)
ms:contentKeyID: 50473425
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# DSN 郵件識別碼

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

您可以識別根據其語法的自訂的傳遞狀態通知 (DSN) 郵件。Identity 為自訂的 DSN 郵件的 GUID 或下列值所組成的字串：

  - **地區設定**  此變數指定之語言的 DSN 訊息以顯示地區設定。如需您可以使用**New-SystemMessage**命令的地區設定程式碼的清單，請參閱[支援的語言的系統郵件](supported-languages-for-system-messages-exchange-2013-help.md)。

  - **內部或外部**  此變數會指定是否 DSN 郵件傳送只要將寄件者屬於內部的 Microsoft Exchange Server 2013組織或至 Exchange 組織外部的寄件者。您可以使用 \[內部\] 選項時您想要將特定電子郵件連絡人或解析度納入 DSN 郵件傳送給內部寄件者，但不想要公開給組織外部的寄件者的資訊。

  - **DSN 代碼**  此變數會指定自訂 DSN 郵件的 DSN 代碼。

DSN 郵件 identity 的語法為`<Locale>\<Internal or External>\<DSN code>`。

針對每個 DSN 代碼，您可以建立多個自訂的 DSN 郵件，其內部的寄件者或外部的寄件者和不同地區設定目標。例如下, 表顯示一些的 DSN 代碼 5.1.2 的可能設定及相對應的 DSN 郵件身分識別。

### 範例 DSN 設定及身分識別

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>DSN 組態</th>
<th>DSN 身分識別</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>對內部的寄件者使用英文 (en-us) 地區設定顯示 DSN 郵件</p></td>
<td><p>En\Internal\5.1.2</p></td>
</tr>
<tr class="even">
<td><p>使用英文 (en-us) 地區設定的外部寄件者顯示 DSN 郵件</p></td>
<td><p>En\External\5.1.2</p></td>
</tr>
<tr class="odd">
<td><p>對內部的寄件者的日文 (ja) 地區設定與顯示 DSN 郵件</p></td>
<td><p>Ja\Internal\5.1.2</p></td>
</tr>
<tr class="even">
<td><p>使用日文 (ja) 地區設定的外部寄件者顯示 DSN 郵件</p></td>
<td><p>Ja\External\5.1.2</p></td>
</tr>
</tbody>
</table>

