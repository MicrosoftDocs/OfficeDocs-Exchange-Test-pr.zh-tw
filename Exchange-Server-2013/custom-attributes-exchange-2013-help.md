---
title: '自訂屬性: Exchange 2013 Help'
TOCTitle: 自訂屬性
ms:assetid: 2b043878-0b34-4563-a9c2-28a9efa7447e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee423541(v=EXCHG.150)
ms:contentKeyID: 50472880
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 自訂屬性

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-17_

Microsoft Exchange Server 2013 包含 15 部署擴充屬性。您可以使用這些屬性来新增的收件者，例如 「 員工識別碼、 組織單位 (OU) 或現有的屬性並未一些其他自訂值的相關資訊。這些自訂屬性會在Active Directory標示為透過**ms-Exch-Extension-Attribute15ms-Exch-Extension-Attribute1** 。Exchange管理命令介面，在對應的參數會是透過*CustomAttribute15CustomAttribute1* 。這些屬性不使用任何Exchange元件。因此可用來儲存Active Directory資料不必擴充Active Directory結構描述。

在Exchange Server 2003與舊版若您想要將此資訊儲存在Active Directory，您都來擴充Active Directory結構描述建立屬性。擴充架構需要規劃、 獲得新屬性的物件識別碼 (Oid) 與實際執行環境中實作之前，在測試環境中測試副檔名程序。在 Exchange 2013 架構延伸模組中不能使用收件者地址清單、 電子郵件地址原則和動態通訊群組所使用的篩選器。

**目錄**

Advantages of custom attributes

Custom attributes examples

Custom attributes example with the ConditionalCustomAttributes parameter

Custom attribute example with ExtensionCustomAttributes parameter

## 自訂屬性的優點

使用自訂屬性的優點包括：

  - 避免延伸 Active Directory 架構。

  - 屬性是由 Exchange 安裝程式所建立。

  - 您可以使用Exchange系統管理中心 (EAC) 或Exchange管理命令介面來管理屬性。您不需要建立自訂控制項或撰寫指令碼來填入並顯示這些屬性。

  - 屬性是可與收件者的 cmdlet，例如**Get-Mailbox***Filter*參數中所使用的可篩選屬性。他們也可用 EAC 和命令介面中建立的電子郵件地址原則 」、 「 地址清單和 「 動態通訊群組的篩選器。

## 多值自訂屬性

在 Exchange 2010 Service Pack 2 (SP2)、 五個多重值的自訂屬性已新增至允許您儲存如果傳統的自訂屬性未符合您需求的郵件收件者的其他資訊的交換。*ExtensionCustomAttribute1ExtensionCustomAttribute5*參數可以保留多達 1300 值。您可以指定多個值以逗號分隔清單。以下 cmdlet 支援這些新參數：

  - [Set-DistributionGroup](https://technet.microsoft.com/zh-tw/library/bb124955\(v=exchg.150\))

  - [Set-DynamicDistributionGroup](https://technet.microsoft.com/zh-tw/library/bb123796\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\))

  - [Set-MailContact](https://technet.microsoft.com/zh-tw/library/aa995950\(v=exchg.150\))

  - [Set-MailPublicFolder](https://technet.microsoft.com/zh-tw/library/bb123707\(v=exchg.150\))

  - [Set-RemoteMailbox](https://technet.microsoft.com/zh-tw/library/ff607302\(v=exchg.150\))

如需多值屬性相關資訊，請參閱[修改多重值內容](modifying-multivalued-properties-exchange-2013-help.md)。

## 自訂屬性範例

在許多Exchange部署中，建立的 OU 中的所有收件者的電子郵件地址原則是常見的案例。OU 不是可在電子郵件地址原則或通訊清單的*RecipientFilter*參數可篩選屬性。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>動態通訊群組有額外的參數可用於將它限制在特定 OU 或容器的收件者。</td>
</tr>
</tbody>
</table>


如果該 OU 中的收件者未共用任何進行篩選時可依據的共同內容，例如部門或位置，則您可使用共同的值填入其中一個自訂屬性，如此範例所示。

    Get-Mailbox -OrganizationalUnit Sales | Set-Mailbox CustomAttribute1 "SalesOU"

現在您可以為 *CustomAttribute1* 內容等於 SalesOU 的所有收件者建立電子郵件地址原則，如此範例所示。

    New-EmailAddressPolicy -Name "Sales" -RecipientFilter { CustomAttribute1 -eq "SalesOU"} -EnabledEmailAddressTemplates "SMTP:%s%2g@sales.contoso.com"

## 含 ConditionalCustomAttributes 參數的自訂屬性範例

建立動態通訊群組、 電子郵件地址原則或通訊清單，您不需要使用*RecipeintFilter*參數來指定自訂屬性。您可以改用*ConditionalCustomAttribute1ConditionalCustomAttribute15*參數。

此範例根據 *CustomAttribute1* 設為 SalesOU 的收件者建立動態通訊群組。

    New-DynamicDistributionGroup -Name "Sales Users and Contacts" -IncludedRecipients "MailboxUsers,MailContacts" -ConditionalCustomAttribute1 "SalesOU"

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您必須使用<em>IncludedRecipients</em>參數如果您使用<em>Conditional</em>參數。此外，您無法使用<em>Conditional</em>參數若您使用<em>RecipientFilter</em>參數。如果您想要包含其他篩選器來建立動態通訊群組中，電子郵件地址原則或通訊清單，您應該使用<em>RecipientFilter</em>參數。</td>
</tr>
</tbody>
</table>


## 使用 ExtensionCustomAttributes 參數自訂屬性範例

在這個範例中，Kweku 的信箱會有已更新並反映他註冊下列教育類別*ExtensionCustomAttribute1* : MATH307、 ECON202，以及 ENGL300。

    Set-Mailbox -Identity Kweku -ExtensionCustomAttribute1 MATH307,ECON202,ENGL300

下一步\] 動態通訊群組的所有學生都註冊 MATH307 會建立使用*ExtensionCustomAttribute1*等於 MATH307 *RecipientFilter*參數。使用*ExtentionCustomAttributes*參數時，您可以使用`-eq`運算子，而不是`-like`運算子。

    New-DynamicDistributionGroup -Name Students_MATH307 -RecipientFilter {ExtensionCustomAttribute1 -eq "MATH307"}

在此範例中，Kweku 的 *ExtensionCustomAttribute1* 值將更新以反映他已加入 ENGL210 課程並移除 ECON202 課程。

    Set-Mailbox -Identity Kweku -ExtensionCustomAttribute1 @{Add="ENGL210"; Remove="ECON202"}

