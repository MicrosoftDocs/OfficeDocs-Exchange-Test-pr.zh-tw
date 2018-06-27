---
title: '電子郵件地址和通訊錄: Exchange 2013 Help'
TOCTitle: 電子郵件地址和通訊錄
ms:assetid: b97d0f68-691a-42af-9a6c-4dcc37b28a42
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ657488(v=EXCHG.150)
ms:contentKeyID: 50474101
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 電子郵件地址和通訊錄

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

收件者 (包括使用者、資源、連絡人及群組) 是指在 Active Directory 中任何擁有郵件功能的物件，Microsoft Exchange 可以傳遞或路由傳送郵件到該位置。收件者必須擁有一個電子郵件地址，才能夠接收或傳送電子郵件。通訊錄是使用者尋找彼此以傳送電子郵件的方法。有許多不同的方法可用來組織通訊錄。如需 Exchange Server 2013 中通訊錄功能的詳細描述，請參閱Key terminology。

## 重要詞彙

下列詞彙定義與 Exchange 2013 中電子郵件地址和通訊錄相關聯的核心元件。

  - **通訊錄原則**  
    通訊錄原則 (ABP) 允許您將使用者分入特定群組以提供您組織的全域通訊清單 (GAL) 之自訂檢視。建立 ABP 時，您要指定 GAL、離線通訊錄 (OAB)、會議室清單和一個以上的通訊清單給該原則。接著您可以指定 ABP 予信箱使用者，提供他們在 Outlook 和 Outlook Web App 中存取自訂 GAL 的權限。目標在於為需要多個 GAL 的內部部署組織提供更簡單的機制來達成 GAL 分割。

<!-- end list -->

  - **通訊清單**  
    通訊清單是 GAL 的子集。每一個通訊清單都是一種或多種具郵件功能之收件者類型的集合 (例如，使用者、連絡人、群組、公用資料夾、會議及其他資源)。您可以使用通訊清單來組織收件者及資源，讓使用者更容易尋找需要的收件者及資源。通訊清單會動態更新。因此，當新收件者新增至組織時，就會自動新增至適當的通訊清單。

<!-- end list -->

  - **電子郵件地址原則**  
    電子郵件地址原則可為收件者產生主要及次要的電子郵件地址，讓他們能夠接收和傳送電子郵件。根據預設，Exchange 對於每一個擁有郵件功能的使用者都會包含一個電子郵件地址原則。

<!-- end list -->

  - **階層式通訊錄**  
    階層式通訊錄 (HAB) 可讓使用者在通訊錄中利用組織性階層來尋找收件者，例如年資或管理結構。使用者通常受限於預設 (GAL) 與其相關聯的收件者內容，而 GAL 的結構通常無法正確反映出組織中收件者彼此之間的管理或階層關係。如果能夠自訂 HAB，對應到組織獨特的業務結構，就能提供使用者有效的方法來尋找內部收件者。

<!-- end list -->

  - **離線通訊錄**  
    離線通訊錄 (OAB) 是已下載的一份通訊清單集合副本，讓 Microsoft Outlook 使用者可以在與伺服器中斷連線時存取所包含的資訊。

## 電子郵件地址和通訊錄文件

下表包含主題的連結，這些主題可協助您了解及管理 Exchange 2013 中的電子郵件地址和通訊錄。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>主題</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="address-lists-exchange-2013-help.md">通訊清單</a></p></td>
<td><p>深入了解通訊清單和 GAL，做為組織收件者讓使用者輕易存取的方法。</p></td>
</tr>
<tr class="even">
<td><p><a href="address-book-policies-exchange-2013-help.md">通訊錄原則</a></p></td>
<td><p>深入了解如何將通訊清單和 GAL 分成不同的虛擬組織。</p></td>
</tr>
<tr class="odd">
<td><p><a href="details-templates-exchange-2013-help.md">詳細資料範本</a></p></td>
<td><p>深入了解自訂 Outlook 中的地址卡。</p></td>
</tr>
<tr class="even">
<td><p><a href="email-address-policies-exchange-2013-help.md">電子郵件地址原則</a></p></td>
<td><p>深入了解 Proxy 電子郵件地址，讓收件者更容易探索。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hierarchical-address-books-exchange-2013-help.md">階層式通訊錄</a></p></td>
<td><p>深入了解如何自訂 GAL 和通訊清單，以符合組織的唯一商業結構。</p></td>
</tr>
<tr class="even">
<td><p><a href="offline-address-books-exchange-2013-help.md">離線通訊錄</a></p></td>
<td><p>深入了解提供使用者對組織通訊清單的離線存取。</p></td>
</tr>
</tbody>
</table>

