---
title: '準備跨樹系移動要求的信箱: Exchange 2013 Help'
TOCTitle: 準備跨樹系移動要求的信箱
ms:assetid: fdbed4fc-a77e-40d5-a211-863b05d74784
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee633491(v=EXCHG.150)
ms:contentKeyID: 50474663
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 準備跨樹系移動要求的信箱

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2017-11-22_

**摘要：** 了解的跨樹系移動Exchange 2013中準備信箱。

Microsoft Exchange 2013支援信箱移動和移轉使用 Exchange 管理命令介面中，特別是**New-MoveRequest**和**New-MigrationBatch**指令程式。您也可以移動信箱透過 Exchange 系統管理中心 (EAC)。請注意您可以將 Exchange 2010 和 Exchange 2013 信箱移至 Exchange 2013 樹系。

若要從Exchange樹系的信箱移至Exchange 2013樹系中， Exchange 2013目標樹系必須包含有效擁有郵件功能的使用者與指定之設定的Active Directory屬性。如果沒有部署樹系中至少一個Exchange 2013用戶端存取伺服器，樹系會被視為Exchange 2013樹系。

若要準備信箱移動，您必須建立具有郵件功能的使用者與目標樹系中使用的必要屬性。以下是兩種建議的方法來建立啟用郵件功能的使用者使用的必要屬性：

  - 如果您為跨樹系全域通訊清單 (GAL) 同步處理部署 Microsoft Identity Lifecycle Manager (ILM)，建立啟用郵件功能的使用者的建議的方法是使用 Service Pack 1 (SP1) 的是 ILM 2007 Feature Pack 1 (FP1)。我們已建立您可以使用了解如何自訂 ILM 同步處理的來源信箱使用者和目標郵件使用者的範例程式碼。
    
    如需詳細資訊，包括如何下載範例程式碼，請參閱[準備使用程式碼範例的跨樹系移動信箱](prepare-mailboxes-for-cross-forest-moves-using-sample-code-exchange-2013-help.md)。

  - 如果您建立目標郵件使用者使用以外的是 ILM/MIIS Active Directory工具，用以**Update-Recipient**指令程式搭配*Identity*參數執行產生**LegacyExchangeDN**目標郵件使用者的通訊清單服務。我們已建立範例Windows PowerShell 指令碼會從讀取與寫入Active Directory並呼叫**Update-Recipient**指令程式。
    
    如需使用範例指令碼的詳細資訊，請參閱[使用命令介面中準備 MoveRequest.ps1 指令碼的跨樹系移動準備信箱](prepare-mailboxes-for-cross-forest-moves-using-the-prepare-moverequest-ps1-script-in-the-shell-exchange-2013-help.md)。

建立目標郵件使用者之後，您可以執行 **New-MoveRequest** 或 **New-MigrationBatch** Cmdlet，將信箱移動到目標 Exchange 2013 樹系。

如需遠端移動要求的詳細資訊，請參閱下列主題：

  - [New-MigrationBatch](https://technet.microsoft.com/zh-tw/library/jj219166\(v=exchg.150\))

  - [New-MoveRequest](https://technet.microsoft.com/zh-tw/library/dd351123\(v=exchg.150\))

如需遠端信箱移動和遠端傳統移動的詳細資訊，請參閱[在 Exchange 2013 移動信箱](mailbox-moves-in-exchange-2013-exchange-2013-help.md)。

本主題的其餘部分說明所需的信箱移動Active Directory郵件使用者的屬性。當您準備信箱移動使用程式碼或指令碼時為您設定這些屬性。不過，您可以手動複製Active Directory這類編輯器中使用這些屬性。

## 信箱移動的必要 Active Directory 使用者屬性

若要支援遠端信箱移動，目標 Exchange 2013 樹系中的郵件使用者物件必須具有本節所描述的 Active Directory 屬性。

  - 必要屬性

  - 選用屬性

  - 連結的屬性

  - 連結的使用者屬性

  - 資源信箱屬性

  - 其他屬性

## 必要屬性

下表會列出最少的一組屬性，您必須在目標郵件使用者上的 ILM 中設定這些屬性，**New-MoveRequest** 指令程式才會正常運作。

### 郵件使用者的屬性

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>郵件使用者的 Active Directory 屬性</th>
<th>動作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>displayName</strong></p></td>
<td><p>複製來源信箱的對應屬性，或產生新值。</p></td>
</tr>
<tr class="even">
<td><p><strong>Mail</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>mailNickname</strong></p></td>
<td><p>複製來源信箱的對應屬性，或產生新值。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchArchiveGUID and msExchArchiveName</strong></p></td>
<td><p>直接將複製的來源信箱的對應屬性。只會可用的來源信箱時Exchange 2010屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchMailboxGUID</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchRecipientDisplayType</strong></p></td>
<td><p>-2147483642 (十進位) //等於 0x80000006 (十六進位)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchRecipientTypeDetails</strong></p></td>
<td><p>128 (十進位) /0x80 (十六進位)。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchUserCulture</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchVersion</strong></p></td>
<td><p>44220983382016 (十進位)。</p></td>
</tr>
<tr class="even">
<td><p><strong>cn</strong></p></td>
<td><p>複製來源信箱的對應屬性，或產生新值。</p></td>
</tr>
<tr class="odd">
<td><p><strong>proxyAddresses</strong></p></td>
<td><p>複製來源信箱<strong>proxyAddresses</strong>屬性。此外，複製來源信箱的<strong>LegacyExchangeDN</strong>以 X500 的目標信箱使用者<strong>proxyAddresses</strong>屬性中的地址。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>proxyAddresses</strong>來源信箱使用者必須包含符合目標樹系的授權網域的 SMTP 地址。這可讓<strong>New-MoveRequest</strong>指令程式以正確選取<strong>targetAddress</strong>來源啟用郵件功能之使用者 （從轉換的來源信箱使用者的信箱移動要求完成後） 以確保該郵件路由是仍正常運作。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p><strong>sAMAccountName</strong></p></td>
<td><p>複製來源信箱的對應屬性，或產生新值。</p>
<p>請確定值在目標郵件使用者所屬目標樹系網域內是唯一的。</p></td>
</tr>
<tr class="odd">
<td><p><strong>targetAddress</strong></p></td>
<td><p>設定為來源信箱之 <strong>proxyAddresses</strong> 屬性中的 SMTP 位址。</p>
<p>這個 SMTP 位址必須屬於來源樹系的授權網域。</p></td>
</tr>
<tr class="even">
<td><p><strong>userAccountControl</strong></p></td>
<td><p>常數： 以 0x202、 ACCOUNTDISABLE 514 //equivalent |NORMAL_ACCOUNT。</p></td>
</tr>
<tr class="odd">
<td><p><strong>userPrincipalName</strong></p></td>
<td><p>複製來源信箱的對應屬性或產生新的值。因為郵件使用者登入已停用，不會使用此<strong>userPrincipalName</strong> 。</p></td>
</tr>
</tbody>
</table>


## 選用屬性

不是必要的下列屬性已設定為**New-MoveRequest**指令程式可正常運作;不過，同步處理其可提供更妥善地端對端使用者經驗移動信箱之後。因為 GAL 目標樹系中的會顯示此目標郵件使用者，您應設定下列 GAL 相關的屬性。

### GAL 相關的屬性

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>郵件使用者的 Active Directory 屬性</th>
<th>Action</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>c</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>co</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>countryCode</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>company</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>department</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>facsimileTelephoneNumber</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>givenName</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>homePhone</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>info</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>initials</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>l</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>mobile</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchAssistantName</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchHideFromAddressLists</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>otherHomePhone</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>otherTelephone</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>pager</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>physicalDeliveryOfficeName</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>postalCode</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>sn</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>st</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>streetAddress</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>telephoneAssistant</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>telephoneNumber</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>title</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
</tbody>
</table>


## 連結的屬性

連結的屬性是在本機樹系中的其他Active Directory物件會參照Active Directory屬性。您不能直接將連結的屬性值從來源樹系中的信箱複製至目標樹系中的郵件使用者。首先，您必須在來源信箱屬性是指來源樹系中找到Active Directory物件。然後，您必須找出對應的Active Directory物件目標樹系中上述Active Directory物件的來源樹系中。與最後，請設定 \[目標樹系中的Active Directory物件參照的目標信箱使用者的屬性。

### 連結的屬性

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>郵件使用者的 Active Directory 屬性</th>
<th>Action</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>altRecipient</strong></p></td>
<td><p>對應到來源信箱的 <strong>altRecipient</strong> 屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>deliverAndRedirect</strong></p></td>
<td><p>直接將複製的來源信箱的對應屬性。此屬性是應該搭配<strong>altRecipient</strong>設定 Boolean 值。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Manager</strong> (及其返回連結)</p></td>
<td><p>對應到來源信箱的管理員屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>MemberOf</strong> (反向連結)</p></td>
<td><p>這是群組成員屬性的反向連結。</p></td>
</tr>
<tr class="odd">
<td><p><strong>publicDelegates</strong> (及其反向連結)</p></td>
<td><p>對應到來源信箱的 <strong>publicDelegates</strong> 屬性。</p></td>
</tr>
</tbody>
</table>


## 連結的使用者屬性

如果您想要將信箱移至Exchange 2013資源樹系、 資源樹系中的信箱會被視為*連結的信箱*。在此案例中，您需要建立連結的郵件使用者 （目標） 資源樹系中。若要建立連結的郵件使用者，您需要將下表所示的屬性。

### 連結的郵件使用者屬性

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>郵件使用者的 Active Directory 屬性</th>
<th>Action</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>msExchMasterAccountHistory</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchMasterAccountSid</strong></p></td>
<td><p>如果來源信箱<strong>msExchMasterAccountSid</strong>，將檔案複製。否則請複製來源信箱<strong>objectSid</strong>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchRecipientDisplayType</strong></p></td>
<td><p>常數：-1073741818 (十進位) //等於 *不帶正負號* 0xC0000006。</p></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>只有當來源樹系和目標樹系之間存在樹系信任時，才能建立連結的信箱。</td>
</tr>
</tbody>
</table>


如果已停用來源物件，而且 **msExchMasterAccountSid** 屬性設定為本身 (資源信箱、共用信箱)，請不要在目標使用者上加註任何戳記。

如果已停用來源物件，而且未設定 **msExchMasterAccountSid** 屬性，則信箱為無效。

如果已啟用來源物件，而且已設定 **msExchMasterAccountSid** 屬性，則信箱為無效。

## 資源信箱屬性

如果想要將資源信箱移到 Exchange 2013 樹系，您必須在目標郵件使用者上設定下表顯示的屬性。

### 資源信箱屬性

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>郵件使用者的 Active Directory 屬性</th>
<th>Action</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>msExchRecipientDisplayType</strong></p></td>
<td><p>如果來源信箱是一間會議室：</p>
<ul>
<li><p><strong>常數</strong>   -2147481850 (十進位) //等於 *不帶正負號* 0x80000706。</p></li>
</ul>
<p>如果來源信箱是設備信箱：</p>
<ul>
<li><p><strong>常數</strong>   -2147481594 (十進位) //等於 *不帶正負號* 0x80000806。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>msExchResourceCapacity</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchResourceDisplay</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchResourceMetaData</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchResourceSearchProperties</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
</tbody>
</table>


## 其他屬性

在Exchange 2007、 **Move-Mailbox**指令程式也會複製移動信箱時，如下表所顯示的屬性。如果貴組織所需的您可以選擇性地複製這些屬性。

### 資源信箱屬性

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>郵件使用者的 Active Directory 屬性</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>comment</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>deletedItemFlags</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>delivContLength</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>departmentNumber</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>description</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>division</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>employeeID</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>employeeNumber</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>employeeType</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>extensionAttribute1-15</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>homePostalAddress</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>internationalISDNNumber</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ipPhone</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>language</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>lmPwdHistory</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>localeID</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>mAPIRecipient</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>middleName</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msDS-PhoneticCompanyName</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>msDS-PhoneticDepartment</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msDS-PhoneticDisplayName</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>msDS-PhoneticFirstName</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msDS-PhoneticLastName</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchBlockedSendersHash</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchELCExpirySuspensionEnd</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchELCExpirySuspensionStart</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchELCMailboxFlags</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchExternalOOFOptions</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchMessageHygieneFlags</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchMessageHygieneSCLDeleteThreshold</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchMessageHygieneSCLJunkThreshold</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchMessageHygieneSCLQuarantineThreshold</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchMessageHygieneSCLRejectThreshold</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchMDBRulesQuota</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchPoliciesExcluded</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchSafeRecipientsHash</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchSafeSendersHash</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchUMSpokenName</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>otherFacsimileTelephoneNumber</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>otherIpPhone</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>otherMobile</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>otherPager</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>preferredDeliveryMethod</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>personalPager</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>personalTitle</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>photo</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>pOPCharacterSet</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>pOPContentFormat</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>postalAddress</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>postOfficeBox</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>primaryInternationalISDNNumber</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>primaryTelexNumber</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>showInAdvancedViewOnly</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>street</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>terminalServer</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>textEncodedORAddress</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>thumbnailLogo</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>thumbnailPhoto</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>url</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>userCert</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>userCertificate</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="even">
<td><p><strong>userSMIMECertificate</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>wWWHomePage</strong></p></td>
<td><p>直接複製來源信箱的對應屬性。</p></td>
</tr>
</tbody>
</table>

