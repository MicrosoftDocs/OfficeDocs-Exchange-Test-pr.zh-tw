---
title: '了解管理角色範圍: Exchange 2013 Help'
TOCTitle: 了解管理角色範圍
ms:assetid: 24ed4a38-438a-4223-9f9c-5d4dea4b046b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd335146(v=EXCHG.150)
ms:contentKeyID: 50472844
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 了解管理角色範圍

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2015-04-07_

*管理角色範圍*可讓您建立管理角色指派時定義影響特定範圍或管理角色的影響。當您將套用的範圍時，指派給角色的角色受託人只能修改包含在該範圍內的物件。角色受託人可管理角色群組、 管理角色、 管理角色指派原則、 使用者或萬用安全性群組 (USG)。如需管理角色的詳細資訊，請參閱[了解角色型存取控制](understanding-role-based-access-control-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>本主題著重於進階 RBAC 功能。如果您要管理基本 Exchange 2013 權限，例如使用 Exchange 系統管理中心 (EAC) 新增和移除角色群組的成員、建立和修改角色群組，或建立和修改角色指派原則，請參閱<a href="permissions-exchange-2013-help.md">權限</a>。</td>
</tr>
</tbody>
</table>


每個管理角色、 內建角色或自訂的角色，是否具有管理範圍。管理範圍可以是下列其中一項：

  - **規則**  *一般範圍*不是互斥的。它會決定，在Active Directory、 物件可以檢視或修改指派管理角色的使用者。一般而言，管理角色表示什麼您可以建立或修改，並管理角色範圍表示您可以在其中建立或修改。規則的範圍可以是隱含或明確的範圍，這兩種本主題稍後的討論。

  - **獨佔**  *獨佔範圍*的行為與一般範圍幾乎相同。主要差異在於它可讓您拒絕使用者存取如果未指派給這些使用者獨佔範圍相關聯的角色獨佔範圍內包含的物件。所有的獨佔範圍會包含範圍，本主題稍後的討論。
    
    如需獨佔範圍的相關資訊，請參閱 [了解獨佔範圍](understanding-exclusive-scopes-exchange-2013-help.md)。

範圍可以繼承自指定為預先定義的相對範圍上的管理角色指派，或建立使用自訂篩選並且新增至管理角色指派的管理角色。繼承自管理角色的範圍會呼叫*隱含範圍*時預先定義及自訂範圍的呼叫*明確的範圍*。下列各節說明每種類型的範圍：

  - Implicit Scopes

  - Explicit Scopes

  - Predefined Relative Scopes

  - Custom Scopes
    
      - Recipient Filter Scopes
    
      - Configuration Scopes

每個角色都可以有下列類型的範圍：

  - **收件者讀取範圍**   隱含的收件者讀取範圍，決定了被指派管理角色的使用者可從 Active Directory 讀取哪些收件者物件。

  - **收件者寫入範圍**   隱含的收件者寫入範圍，決定了被指派管理角色的使用者可在 Active Directory 中修改哪些收件者物件。

  - **組態讀取範圍**   隱含的組態讀取範圍，決定了被指派管理角色的使用者可從 Active Directory 讀取哪些組態物件。

  - **組態寫入範圍**   隱含的組態寫入範圍，決定了被指派管理角色的使用者可在 Active Directory 中修改哪些組織、資料庫和伺服器物件。

收件者物件包含信箱、 通訊群組、 啟用郵件功能的使用者及其他物件。設定物件包含執行 Microsoft Exchange Server 2013、 和執行Exchange伺服器上的資料庫伺服器。每種類型可以是範圍的隱含範圍或明確的範圍。

## 隱含範圍

不明確的範圍會套用至管理角色類型的預設範圍。由於隱含的範圍與管理角色類型相關聯，因此相同的角色類型與父項及子項管理角色的所有也有相同的隱含範圍。隱含範圍套用至這兩個內建管理角色及自訂管理角色。如需管理角色和管理角色類型的詳細資訊，請參閱[了解管理角色](understanding-management-roles-exchange-2013-help.md)。

下表列出所有可在管理角色上定義的隱含範圍。

### 在管理角色上定義的隱含範圍

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>隱含範圍</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Organization</code></p></td>
<td><p>如果 <code>Organization</code> 出現在角色的收件者寫入範圍內，則該角色可以建立或修改整個 Exchange 組織內的收件者物件。</p>
<p>如果 <code>Organization</code> 出現在角色的收件者讀取範圍內，則該角色可以檢視整個 Exchange 組織內的任何收件者物件。</p>
<p>此範圍僅與收件者讀取和寫入範圍配合使用。</p></td>
</tr>
<tr class="even">
<td><p><code>MyGAL</code></p></td>
<td><p>如果 <code>MyGAL</code> 出現在角色的收件者寫入範圍內，則該角色可以檢視在目前使用者的全域通訊清單 (GAL) 內任何收件者的內容。</p>
<p>如果 <code>MyGAL</code> 出現在角色的收件者讀取範圍內，則該角色可以檢視在目前 GAL 內任何收件者的內容。</p>
<p>此範圍僅與收件者讀取範圍配合使用。</p></td>
</tr>
<tr class="odd">
<td><p><code>Self</code></p></td>
<td><p>如果 <code>Self</code> 出現在角色的收件者寫入範圍內，則該角色只能修改目前使用者信箱的內容。</p>
<p>如果 <code>Self</code> 出現在角色的收件者讀取範圍內，則該角色只能檢視目前使用者信箱的內容。</p>
<p>此範圍僅與收件者讀取和寫入範圍配合使用。</p></td>
</tr>
<tr class="even">
<td><p><code>MyDistributionGroups</code></p></td>
<td><p>如果 <code>MyDistributionGroups</code> 出現在角色的收件者寫入範圍內，則該角色可以建立或修改目前使用者所擁有的通訊清單物件。</p>
<p>如果 <code>MyDistributionGroups</code> 出現在角色的收件者讀取範圍內，則該角色可以檢視目前使用者所擁有的通訊清單物件。</p>
<p>此範圍僅與收件者讀取和寫入範圍配合使用。</p></td>
</tr>
<tr class="odd">
<td><p><code>OrganizationConfig</code></p></td>
<td><p>如果 <code>OrganizationConfig</code> 出現在角色的組態寫入範圍內，則該角色可以建立或修改整個 Exchange 組織內的任何伺服器或資料庫組態物件。</p>
<p>如果 <code>OrganizationConfig</code> 出現在角色的組態讀取範圍內，則該角色可以檢視整個 Exchange 組織內的任何伺服器或資料庫組態物件。</p>
<p>此範圍僅與組態讀取和寫入範圍配合使用。</p></td>
</tr>
<tr class="even">
<td><p><code>None</code></p></td>
<td><p>如果<code>None</code>範圍，該範圍無法使用的角色。例如，在收件者寫入範圍中有<code>None</code>角色無法修改Exchange組織中的收件者物件。</p></td>
</tr>
</tbody>
</table>


如果已將角色指派給角色受託人，而且未指定任何預先定義或自訂的範圍，則會使用在該角色上定義的隱含範圍來控制使用者能夠檢視或修改的收件者或組織物件。

角色隱含寫入範圍一定會等於、 小於比隱含讀取範圍。這表示角色永遠不可以修改見所範圍的物件。

您不能變更的隱含範圍定義在管理角色。您可以，但來覆寫隱含寫入範圍與管理角色上的組態範圍。在角色指派上使用時的預先定義的相對範圍或自訂的範圍，則會覆寫隱含寫入範圍的角色，及新的範圍會優先。隱含讀取的範圍的角色不能覆寫並永遠套用。如需詳細資訊，請參閱預先定義的相對範圍及自訂範圍。

展開下表來查看所有內建管理角色和其隱含範圍的清單。如需每個內建角色的詳細資訊，請參閱[內建管理角色](built-in-management-roles-exchange-2013-help.md)。

## 內建管理角色隱含範圍


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>管理角色</th>
<th>收件者讀取範圍</th>
<th>收件者寫入範圍</th>
<th>組態讀取範圍</th>
<th>組態寫入範圍</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Active Directory Permissions</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Address Lists</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>ApplicationImpersonation</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><code>ArchiveApplication</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Audit Logs</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Cmdlet Extension Agents</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Data Loss Prevention</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Database Availability Groups</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Database Copies</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Databases</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Disaster Recovery</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Distribution Groups</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Edge Subscriptions</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>E-Mail Address Policies</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Exchange Connectors</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Exchange Server Certificates</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Exchange Servers</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Exchange Virtual Directories</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Federated Sharing</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Information Rights Management</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Journaling</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Legal Hold</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><code>LegalHoldApplication</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Mail Enabled Public Folders</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Mail Recipient Creation</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Mail Recipients</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Mail Tips</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Mailbox Import Export</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Mailbox Search</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><code>MailboxSearchApplication</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Message Tracking</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Migration</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Monitoring</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Move Mailboxes</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>OfficeExtensionApplication</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>My Custom Apps</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>My Marketplace Apps</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyAddressInformation</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyBaseOptions</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyContactInformation</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyDiagnostics</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyDisplayName</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyDistributionGroupMembership</code></p></td>
<td><p><code>MyGAL</code></p></td>
<td><p><code>MyGAL</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyDistributionGroups</code></p></td>
<td><p><code>MyGAL</code></p></td>
<td><p><code>MyDistributionGroups</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyMobileInformation</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyName</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyPersonalInformation</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyProfileInformation</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyRetentionPolicies</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyTeamMailboxes</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyTextMessaging</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyVoiceMail</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Organization Client Access</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Organization Configuration</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Organization Transport Settings</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>POP3 And IMAP4 Protocols</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Public Folders</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Receive Connectors</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Recipient Policies</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Remote and Accepted Domains</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Reset Password</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Retention Management</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Role Management</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Security Group Creation and Membership</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Send Connectors</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Support Diagnostics</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>TeamMailboxLifecycleApplication</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Transport Agents</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Transport Hygiene</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Transport Queues</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Transport Rules</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>UM Mailboxes</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>UM Prompts</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Unified Messaging</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>UnScoped Role Management</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>UserApplication</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>User Options</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>View-Only Audit Logs</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><code>View-Only Configuration</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><code>View-Only Recipients</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><code>WorkloadManagement</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
</tbody>
</table>


## 明確的範圍

明確的範圍是您要自行設定控制項的物件管理角色可修改的範圍。雖然隱含範圍定義管理角色上，明確範圍定義管理角色指派上。這可讓隱含的範圍是一致地套用在跨所有管理角色除非您選擇使用覆寫明確的範圍。如需管理角色指派的詳細資訊，請參閱[了解管理角色指派](understanding-management-role-assignments-exchange-2013-help.md)。

明確的範圍會覆寫隱含寫入和組態範圍的管理角色。它們不覆寫隱含讀取的範圍管理角色。若要定義新的管理角色可讀取的物件會繼續隱含讀取的範圍。

管理角色的隱含寫入範圍不符合您的業務需求時，有用明確的範圍。您可以新增要包含幾乎任何您想要為新的範圍不會超過隱含讀取範圍的邊界明確範圍。管理角色的一部分之 cmdlet 必須能夠讀取物件或容器包含物件的 cmdlet 來建立或修改物件的相關資訊。例如，如果在管理角色的隱含讀取的範圍設為`Self`，您無法新增`Organization`明確寫入範圍因為明確的寫入範圍超過隱含讀取範圍的邊界。

如需詳細資訊，請參閱下列各節：

  - Predefined Relative Scopes

  - Custom Scopes

## 預先定義的相對範圍

Exchange 2013提供數個預先定義的相對寫入可用來修改管理角色的範圍的範圍。預先定義的相對範圍提供您更符合您的業務需求而不需要手動建立自訂範圍簡便的方式。他們被呼叫相對範圍因為它們是相對於角色受託人對其指派的相關聯的角色指派。例如， `Self`預先定義的相對範圍限制目前使用者的寫入範圍。`MyDistributionGroups`預先定義的相對範圍只能擁有目前使用者的通訊群組限制寫入範圍。預先定義的相對範圍只可用於範圍收件者物件。預先定義的相對範圍無法用以範圍組態物件。下表列出您可以使用預先定義的相對範圍。

### 預先定義的相對範圍

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>隱含範圍</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Organization</code></p></td>
<td><p>如果 <code>Organization</code> 出現在角色的收件者寫入範圍內，則該角色可以建立或修改整個 Exchange 組織內的收件者物件。</p>
<p>如果 <code>Organization</code> 出現在角色的收件者讀取範圍內，則該角色可以檢視整個 Exchange 組織內的任何收件者物件。</p>
<p>此範圍僅與收件者讀取和寫入範圍配合使用。</p></td>
</tr>
<tr class="even">
<td><p><code>Self</code></p></td>
<td><p>如果 <code>Self</code> 出現在角色的收件者寫入範圍內，則該角色只能修改目前使用者信箱的內容。</p>
<p>如果 <code>Self</code> 出現在角色的收件者讀取範圍內，則該角色只能檢視目前使用者信箱的內容。</p>
<p>此範圍僅與收件者讀取和寫入範圍配合使用。</p></td>
</tr>
<tr class="odd">
<td><p><code>MyDistributionGroups</code></p></td>
<td><p>如果 <code>MyDistributionGroups</code> 出現在角色的收件者寫入範圍內，則該角色可以建立或修改目前使用者所擁有的通訊清單物件。</p>
<p>如果 <code>MyDistributionGroups</code> 出現在角色的收件者讀取範圍內，則該角色可以檢視目前使用者所擁有的通訊清單物件。</p>
<p>此範圍僅與收件者讀取和寫入範圍配合使用。</p></td>
</tr>
</tbody>
</table>


當您建立新的管理角色指派時套用預先定義的相對範圍。期間建立的角色指派，使用**New-ManagementRoleAssignment**指令程式，您可以指定預先定義的相對範圍使用*RecipientRelativeWriteScope*參數。建立新的角色指派之後，新預先定義的角色會覆寫的管理角色的隱含寫入範圍。您不能指定自訂的收件者範圍時您使用預先定義的相對範圍建立角色指派。如果需要不過，可以指定自訂設定範圍。

如需有關如何新增含預先定義相對範圍的管理角色指派，請參閱[將角色新增至使用者或 USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md)。

## 自訂範圍

當不明確的寫入範圍皆預先定義的相對範圍符合您的業務需求時所需自訂範圍。自訂範圍可讓您定義，請在細微的層級，將會套用您的管理角色的範圍。例如，您可能會想要將目標放在特定組織單位 (OU)、 特定類型的收件者，或兩者。或者，您可能只想要讓系統管理員能夠管理信箱資料庫的特定集合的群組。

為預先定義的相對範圍自訂範圍覆寫隱含寫入及組織設定範圍定義在管理角色。隱含閱讀在管理角色的範圍會繼續套用與所產生的自訂範圍不得超過隱含讀取範圍的邊界。您可以建立下列三種類型的自訂範圍 ︰

  - **OU 範圍**  OU 範圍，也就是最簡單的自訂範圍，會建立**New-ManagementRoleAssignment**指令程式上使用*RecipientOrganizationalUnitScope*參數。藉由指定 OU 範圍時指派角色、 指派角色的角色受託人可修改只有該 OU 內的收件者物件。如需如何新增 OU 範圍的管理角色指派的詳細資訊，請參閱[將角色新增至使用者或 USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md)。

  - **收件者篩選器範圍**  收件者篩選器範圍使用篩選，以針對特定收件者類型或部門、 管理員、 位置和更多其他收件者屬性為基礎的收件者。如需詳細資訊，請參閱 \[收件者篩選器範圍\] 區段。

  - **組態範圍**  組態範圍使用篩選器或目標伺服器清單或是可以如Active Directory網站或伺服器角色的伺服器所定義的可篩選屬性為基礎的特定伺服器的清單。組態範圍也可以使用資料庫範圍將目標放在特定資料庫清單或可篩選資料庫內容為基礎的資料庫。如需詳細資訊，請參閱 ＜設定範圍\] 區段。

使用**New-ManagementScope**指令程式可以建立簡單和廣泛或複雜與細微收件者和設定自訂範圍。當您建立的收件者 」 或 「 組態的範圍時，會傳回只收件者、 伺服器或資料庫物件符合其各自的範圍。當這些範圍會套用至使用**New-ManagementRoleAssignment**或**Set-ManagementRoleAssignment** cmdlet 的角色指派可符合範圍的物件可以修改角色 assignees 對其指派的角色。建立自訂範圍之後，您無法變更此範圍類型。收件者範圍一定是收件者範圍和組態範圍一定是組態範圍。

根據預設，自訂範圍可讓角色受託人存取一組符合您所定義的範圍的物件。不過，它們不主動排除存取其他角色 assignees 也未指派的相同或相等的範圍。如果清單或對這些範圍篩選器相符的相同物件任何自訂範圍可以存取的相同的物件。可能會有其中的行為表現方式不想，例如為但如果是高階主管的物件。這些物件，您可以定義獨佔範圍。獨佔範圍規則的範圍但不同於一般範圍的相同方式來使用篩選器或清單、 拒絕存取權給任何人不是屬於相同或同級獨佔範圍的範圍中包含的物件。如需獨佔範圍的詳細資訊，請參閱[了解獨佔範圍](understanding-exclusive-scopes-exchange-2013-help.md)。

## 收件者篩選器範圍

收件者篩選器範圍可讓您控制哪些收件者物件角色 assignees 可以管理評估對您指定篩選陳述式中的值在收件者物件上的一或多個屬性。收件者範圍中包含的收件者的信箱、 擁有郵件功能的使用者、 通訊群組及郵件連絡人。僅收件者的符合您指定的篩選器可以一併管理角色 assignees 指派給該角色指派。篩選陳述式範例是`{ Name -Eq "David" }`其中**Name**是上所評估的收件者物件的屬性而**David**是您想要評估對屬性的值。**-Eq**比較運算子會指出儲存在屬性值必須等於指定的篩選器必須為 true 的值。如果篩選條件為真，該收件者會包含在範圍中。

指定要搭配*RecipientRestrictionFilter*參數**New-ManagementScope**指令程式上的收件者篩選建立收件者篩選器範圍。根據預設， **New-ManagementScope**指令程式會建立規則的範圍。如果您想要建立獨佔範圍，包括*Exclusive*參數搭配*RecipientRestrictionFilter*參數。

當您建立收件者限制篩選時， Exchange評估您預設會提供對組織中每個收件者物件的篩選。如果您想要限制範圍評估哪些收件者，您可以使用*RecipientRoot*參數搭配*RecipientRestrictionFilter*參數。*RecipientRoot*參數可接受的 OU。當您使用*RecipientRoot*參數時， Exchange評估只包含收件者所提供的篩選依據所指定 OU 中。

當您新增的收件者篩選器範圍角色指派時，收件者範圍的名稱參數中指定*CustomRecipientWriteScope*上**New-ManagementRoleAssignment**如果您建立新的角色指派或**Set-ManagementRoleAssignment**指令程式如果您正在更新現有的角色指派。每個角色指派可以有一個收件者的範圍，包括預先定義的相對範圍。您可以將一個組態範圍新增至同一個新增到收件者範圍的角色指派。

如需篩選器語法的詳細資訊，以及收件者上可篩選收件者屬性的完整清單，請參閱[了解管理角色範圍篩選器](understanding-management-role-scope-filters-exchange-2013-help.md)。

## 組態範圍

以下是在Exchange 2013中所提供的組態範圍的兩種類型：

  - **伺服器範圍**  有兩種類型的伺服器範圍、 伺服器篩選器範圍及伺服器清單範圍。若伺服器物件包含伺服器範圍中可管理伺服器組態，包括接收連接器、 傳輸佇列、 伺服器憑證、 虛擬目錄，依此類推、。
    
      - **伺服器篩選範圍**  伺服器篩選器範圍可讓您控制哪些伺服器物件角色 assignees 可以管理評估對您指定篩選陳述式中的值在伺服器物件上的一或多個屬性。若要建立伺服器篩選器範圍，請使用*ServerRestrictionFilter*參數**New-ManagementScope**指令程式上。
    
      - **伺服器清單範圍**  伺服器清單範圍可讓您控制哪些伺服器物件角色 assignees 可以管理所定義的角色受託人可存取的伺服器清單。若要建立的伺服器清單範圍，請使用*ServerList*參數**New-ManagementScope**指令程式上。

  - **資料庫範圍**  有兩種類型的資料庫範圍、 資料庫篩選器範圍及資料庫清單範圍。若資料庫範圍中包含資料庫物件，則可管理的資料庫組態包含資料庫配額限制、 資料庫維護、 公用資料夾複寫是否裝載資料庫，依此類推。除了資料庫組態資料庫範圍也可以用來控制哪些中可以建立資料庫的收件者。如果您在組織中有前Exchange 2010 SP1 伺服器，請參閱本主題稍後的資料庫範圍與舊版 Exchange 的區段。
    
      - **資料庫篩選器範圍**  資料庫篩選器範圍可讓您控制哪些資料庫物件角色 assignees 可以管理評估對您指定篩選陳述式中的值 database 物件上的一或多個屬性。若要建立資料庫篩選器範圍，請使用*DatabaseRestrictionFilter*參數**New-ManagementScope**指令程式上。
    
      - **資料庫清單範圍**  資料庫清單範圍可讓您控制哪些資料庫物件角色 assignees 可以管理所定義的角色受託人可存取的資料庫清單。若要建立的資料庫清單範圍，請使用*DatabaseList*參數**New-ManagementScope**指令程式上。

如需篩選器語法的詳細資訊，以及可篩選伺服器及資料庫屬性的完整清單，請參閱[了解管理角色範圍篩選器](understanding-management-role-scope-filters-exchange-2013-help.md)。

可以藉由指定您想要包含在其各自的範圍中每個伺服器和資料庫定義伺服器和資料庫的清單。多部伺服器或資料庫可以在其各自的範圍內以逗號分隔的伺服器和資料庫名稱來指定。

當伺服器或資料庫組態範圍新增至角色指派時、 伺服器或資料庫組態範圍的名稱參數中指定*CustomConfigWriteScope***New-ManagementRoleAssignment**指令程式如果您正在建立新的角色指派，或**Set-ManagementRoleAssignment**指令程式如果您正在更新現有的角色指派。每個角色指派只能有一個設定範圍。

除了控制哪些資料庫角色 assignees 可管理資料庫範圍也可讓您的資料庫角色 assignees 可以建立信箱上的控制項。這是分開控制哪些角色受託人可管理的收件者。如果角色受託人建立新的信箱、 擁有郵件功能的現有的使用者，或移出信箱的權限，您可以進一步讓其權限使用資料庫範圍控制在其建立信箱、 或哪些資料庫的信箱移至的資料庫中。控制哪些角色受託人可管理的收件者已完成使用收件者範圍參數中所指定*CustomRecipientWriteScope***New-ManagementRoleAssignment**或**Set-ManagementRoleAssignment**指令程式上。控制哪些信箱可在建立或移至的資料庫是使用的相同指令程式*CustomConfigurationWriteScope*參數中指定的資料庫範圍控制。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>可以使用資料庫範圍控制自動信箱發佈。</td>
</tr>
</tbody>
</table>


Exchange功能可能會需要伺服器範圍、 資料庫範圍，或兩者都設為進行管理。如果功能需要伺服器和資料庫範圍來管理，必須建立並指派給角色受託人可以存取管理功能的兩種角色指派。一個角色指派應該要關聯至伺服器範圍，和一個角色指派應資料庫範圍與相關聯。

某些指令程式可以使用立即明顯組態範圍。下表包含 cmdlet 及可用來控制其用法的組態範圍的清單。包含 \[收件者的功能\] 區域中的 cmdlet，設定範圍可讓您控制要在哪些資料庫上建立收件者。它們不會控制可管理哪些收件者。**所需範圍**的資料行可以包含下列項目：

  - **資料庫**   若要執行 Cmdlet，必須將角色指派指定給具有資料庫範圍的角色指派，該資料庫範圍中包含要管理的資料庫，否則角色的隱含組態寫入範圍必須包含要管理的資料庫。

  - **伺服器**   若要執行 Cmdlet，必須將角色指派指定給具有伺服器範圍的角色指派，該伺服器範圍中包含要管理的伺服器，否則角色的隱含組態寫入範圍必須包含要管理的伺服器。

  - **伺服器或資料庫**  若要執行此指令程式，角色受託人必須指派角色指派對於資料庫的範圍包含受管理的資料庫或放置伺服器範圍包括資料庫所在的伺服器。或者，角色隱含組態寫入範圍必須包含要進行管理的資料庫，或包含的伺服器所在之資料庫所在和角色指派不能有自訂寫入範圍。

  - **伺服器和資料庫**  若要執行此指令程式，角色受託人必須被指派兩個角色指派。第一個角色指派必須包含資料庫範圍，其中包含要管理的資料庫。第二個角色指派必須包含包含伺服器資料庫所在伺服器範圍。角色指派可有自訂設定範圍定義，或角色指派可繼承該角色的隱含組態寫入範圍。若要繼承隱含寫入範圍從角色、 角色指派不能有自訂寫入範圍。

### 功能範圍以及適用的資料庫與伺服器範圍

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>功能範圍</th>
<th>Cmdlet</th>
<th>所需的範圍</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>資料庫</p></td>
<td><p><strong>Dismount-Database</strong></p></td>
<td><p>Database</p></td>
</tr>
<tr class="even">
<td><p>資料庫</p></td>
<td><p><strong>Mount-Database</strong></p></td>
<td><p>Database</p></td>
</tr>
<tr class="odd">
<td><p>資料庫</p></td>
<td><p><strong>Move-DatabasePath</strong></p></td>
<td><p>伺服器和資料庫</p></td>
</tr>
<tr class="even">
<td><p>資料庫</p></td>
<td><p><strong>Remove-MailboxDatabase</strong></p></td>
<td><p>伺服器或資料庫</p></td>
</tr>
<tr class="odd">
<td><p>資料庫</p></td>
<td><p><strong>Set-MailboxDatabase</strong></p></td>
<td><p>Database</p></td>
</tr>
<tr class="even">
<td><p>高可用性</p></td>
<td><p><strong>Add-DatabaseAvailabilityGroupServer</strong></p></td>
<td><p>伺服器</p></td>
</tr>
<tr class="odd">
<td><p>高可用性</p></td>
<td><p><strong>Add-MailboxDatabaseCopy</strong></p></td>
<td><p>伺服器</p></td>
</tr>
<tr class="even">
<td><p>高可用性</p></td>
<td><p><strong>Move-ActiveMailboxDatabase</strong></p></td>
<td><p>伺服器</p></td>
</tr>
<tr class="odd">
<td><p>高可用性</p></td>
<td><p><strong>Remove-DatabaseAvailabilityGroupServer</strong></p></td>
<td><p>伺服器</p></td>
</tr>
<tr class="even">
<td><p>高可用性</p></td>
<td><p><strong>Remove-MailboxDatabaseCopy</strong></p></td>
<td><p>伺服器或資料庫</p></td>
</tr>
<tr class="odd">
<td><p>高可用性</p></td>
<td><p><strong>Resume-MailboxDatabaseCopy</strong></p></td>
<td><p>伺服器或資料庫</p></td>
</tr>
<tr class="even">
<td><p>高可用性</p></td>
<td><p><strong>Set-MailboxDatabaseCopy</strong></p></td>
<td><p>伺服器或資料庫</p></td>
</tr>
<tr class="odd">
<td><p>高可用性</p></td>
<td><p><strong>Suspend-MailboxDatabaseCopy</strong></p></td>
<td><p>伺服器或資料庫</p></td>
</tr>
<tr class="even">
<td><p>高可用性</p></td>
<td><p><strong>Update-MailboxDatabaseCopy</strong></p></td>
<td><p>伺服器或資料庫</p></td>
</tr>
<tr class="odd">
<td><p>收件者</p></td>
<td><p><strong>Connect-Mailbox</strong></p></td>
<td><p>Database</p></td>
</tr>
<tr class="even">
<td><p>收件者</p></td>
<td><p><strong>Enable-Mailbox</strong></p></td>
<td><p>Database</p></td>
</tr>
<tr class="odd">
<td><p>收件者</p></td>
<td><p><strong>New-Mailbox</strong></p></td>
<td><p>Database</p></td>
</tr>
<tr class="even">
<td><p>收件者</p></td>
<td><p><strong>New-MoveRequest</strong></p></td>
<td><p>Database</p></td>
</tr>
<tr class="odd">
<td><p>疑難排解</p></td>
<td><p><strong>Test-MapiConnectivity</strong></p></td>
<td><p>Database</p></td>
</tr>
</tbody>
</table>


## 資料庫範圍與舊版 Exchange

資料庫範圍已首次發表於 Microsoft Exchange 2010 Service Pack 1 (SP1) 和支援的Exchange 2013會繼續。ExchangeExchange 2010 SP1 以前的版本支援只有收件者範圍和伺服器組態的範圍。當您Exchange 2010 SP1 或更新版本的伺服器上建立新的資料庫範圍時，則會收到下列警告：

    WARNING: Database management scopes will only be applied when a user connects to a server running Exchange 2010 SP1 or later. Servers running a version of Exchange prior to Exchange 2010 SP1 won't apply any roles from a role assignment linked to a database scope. Database management scopes also won't be visible to the Get-ManagementScope cmdlet when it's run from a pre-Exchange 2010 SP1 server.

當您建立資料庫範圍時，僅套用於連線到執行Exchange 2010 SP1 的伺服器的使用者或更新版本。連線至預先Exchange 2010 SP1 伺服器的使用者不會有任何對它們套用資料庫範圍與相關聯的角色指派。這表示這些角色指派所提供的任何權限不會授與使用者連線至時前Exchange 2010 SP1 的伺服器。資料庫範圍不能建立、 移除、 修改或檢視從預先Exchange 2010 SP1 的伺服器。

資料庫範圍可以包含Exchange組織中的任何資料庫。這包括Exchange Server 2007、 Exchange 2010、 和Exchange 2013伺服器。這可讓您控制哪些資料庫，不論Exchange版本的使用者可以管理。為與其他資料庫範圍包含Exchange 2007和Exchange 2010資料庫的資料庫範圍與相關聯的角色指派會只套用至使用者連線至Exchange 2010 SP1 或更新版本的伺服器時。

連線至預先Exchange 2010 SP1 伺服器的使用者可以檢視和修改資料庫範圍與相關聯的角色指派。這包含變更現有的角色指派上設定範圍的伺服器範圍如果資料庫範圍與目前相關聯。不過，如果在角色指派上的設定範圍變更為 \[伺服器範圍和使用者稍後想要將其變更回資料庫範圍，或者使用者想要變更組態範圍至另一個資料庫範圍，使用者必須進行變更時連線至Exchange 2010 SP1 或更新版本的伺服器。使用者只能指定伺服器範圍時這些變更角色指派上的設定範圍如果他們正在連線至預先Exchange 2010 SP1 伺服器。

