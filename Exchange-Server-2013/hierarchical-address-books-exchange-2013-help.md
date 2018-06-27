---
title: '階層式通訊錄: Exchange Online Help'
TOCTitle: 階層式通訊錄
ms:assetid: a1d277a0-5437-40af-aade-e4730a0d1308
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ff629379(v=EXCHG.150)
ms:contentKeyID: 50473896
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 階層式通訊錄

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-03-26_

階層式通訊錄 (HAB) 可讓使用者使用組織階層，在其通訊錄中尋找收件者。使用者通常受限於預設全域通訊清單 (GAL) 與其收件者內容，而 GAL 的結構通常無法反映出組織中收件者彼此之間的管理或階層關係。如果能夠自訂 HAB，對應到組織獨特的業務結構，就能提供使用者有效的方法來尋找內部收件者。

## 使用階層式通訊錄

在 HAB 中，根組織 (例如 Contoso, Ltd) 位於最上層。在最上層底下，您可以新增幾個子層來建立自訂的 HAB，分成事業單位、部門或其他任何想指定的組織層。下圖顯示 Contoso, Ltd 的 HAB，結構如下：

  - 最上層代表根組織 Contoso, Ltd。

  - 第二層子層代表 Contoso, Ltd 內的事業單位：Corporate Office、Product Support Organization 和 Sales & Marketing Organization。

  - 第三層子層代表 Corporate Office 事業單位內的部門：Human Resources、Accounting Group 和 Administration Group。

**Contoso, Ltd 的 HAB 範例**

![階層式通訊錄對話方塊](images/Ff629379.d8cc782f-61cd-44c4-9c74-432ebea0c3db(EXCHG.150).gif "階層式通訊錄對話方塊")

您可以使用 *SeniorityIndex* 參數，在階層結構另外再新增一層。建立 HAB 時，請使用 *SeniorityIndex* 在這些組織層依階級排列個別收件者或組織群組。此排名會指定收件者或群組顯示在 HAB 中的順序。例如，在前面的範例中，針對 Corporate Office 事業單位中的收件者，*SeniorityIndex* 參數設定如下：

  - David Hamilton 為 `100`

  - Rajesh M. Patel 為 `50`

  - Amy Alberts 為 `25`

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果 <em>SeniorityIndex</em> 參數未設定，或對於兩個或多個使用者來說是相等，則 HAB 排序順序會使用 <em>PhoneticDisplayName</em> 參數值以遞增英文字母順序來列出使用者。如果 <em>PhoneticDisplayName</em> 參數值未設定，則 HAB 排序順序預設為 <em>DisplayName</em> 參數值，並以遞增英文字母順序列出使用者。</td>
</tr>
</tbody>
</table>


## 設定階層式通訊錄

[啟用或停用階層式通訊錄](enable-or-disable-hierarchical-address-books-exchange-2013-help.md)主題提供建立 HAB 的詳細指示。一般步驟如下：

1.  建立將用於根組織 (最上層) 的通訊群組。您可以視需要使用 Exchange 樹系中現有的組織單位作為通訊群組。

2.  為子層建立通訊群組，並將它們指定為 HAB 的成員。修改這些群組的 *SeniorityIndex* 參數，讓它們以正確的階層順序列在根組織內。

3.  新增組織成員。修改成員的 *SeniorityIndex* 參數，讓它們以正確的階層順序列在子層內。

4.  為提供無障礙支援，您可以使用 *PhoneticDisplayName* 參數，指定 *DisplayName* 參數的語音讀法。

