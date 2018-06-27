---
title: '組織管理: Exchange 2013 Help'
TOCTitle: 組織管理
ms:assetid: 0bfd21c1-86ac-4369-86b7-aeba386741c8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd335087(v=EXCHG.150)
ms:contentKeyID: 50472542
ms.date: 01/01/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 組織管理

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

組織管理 管理角色群組是組成 Microsoft Exchange Server 2013 中角色型存取控制 (RBAC) 權限模型的其中一個內建角色群組。角色群組會有一或多個管理角色指派，其中包含執行指定工作集所需的權限。角色群組的成員擁有指派給該角色群組的管理角色存取權。如需角色群組的詳細資訊，請參閱[了解管理角色群組](understanding-management-role-groups-exchange-2013-help.md)。

屬於 組織管理 角色群組之成員的系統管理員擁有整個 Exchange 2013 組織的管理存取權，並幾乎可對任何 Exchange 2013 物件執行任何工作，只有少部分例外。根據預設，此角色群組成員無法執行信箱搜尋和未限定範圍的頂層管理角色的管理。如需詳細資訊，請參閱本主題稍後的「只委派角色指派」一節。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>組織管理 角色群組是功能非常強大的角色，因此只有執行可能影響整個 Exchange 組織之組織層級管理工作的使用者或萬用安全性群組 (USG) 才應該是這個角色群組的成員。</td>
</tr>
</tbody>
</table>


這個角色群組相當於 Exchange Server 2007 中的 Exchange 組織系統管理員角色。

如需有關 RBAC 的詳細資訊，請參閱[了解角色型存取控制](understanding-role-based-access-control-exchange-2013-help.md)。

## 角色群組成員資格

用於將 Exchange 2013 安裝在組織中的帳戶預設會新增為 組織管理 角色群組的成員。然後此帳戶便可視需要，將其他成員新增至此角色群組。

如果您要新增或移除此角色群組中的成員，請參閱[管理角色群組成員](manage-role-group-members-exchange-2013-help.md)。

根據預設，只有組織管理角色群組的成員可以新增或移除此角色群組中的成員。如需如何新增其他角色群組委派的詳細資訊，請參閱 [管理角色群組](manage-role-groups-exchange-2013-help.md) 中的「新增或移除角色群組委派」一節。

您可以使用下列命令來檢視屬於此角色群組成員之使用者或 USG 的清單。

    Get-RoleGroupMember "Organization Management"

如需角色群組之成員的詳細資訊，請參閱[管理角色群組](manage-role-groups-exchange-2013-help.md)。

## 角色群組自訂

此角色群組預設會獲派管理角色。＜指派給此角色群組的管理角色＞一節中會列出包含的角色。您可以在新增或移除此角色群組的角色指派，以符合組織的需要。

Exchange 2013 所提供的角色群組旨在於符合更細微的工作。將角色指派給角色群組，即可讓該角色群組的成員執行與角色關聯的工作。例如，\[日誌\] 角色會啟用日誌代理程式的管理功能和日誌規則。如需如何將角色指派給角色群組的詳細資訊，請參閱[了解管理角色指派](understanding-management-role-assignments-exchange-2013-help.md)。

指派給此角色群組的角色會擁有預設的管理範圍。管理範圍決定角色群組的成員可以檢視或修改的 Exchange 物件。您可以變更角色和角色群組之間與指派相關聯的範圍。例如，如果您只想讓角色群組的成員變更特定組織單位下或是特定位置的收件者，則可執行這項操作。如需管理範圍的詳細資訊，請參閱[了解管理角色範圍](understanding-management-role-scopes-exchange-2013-help.md)。

如需如何自訂此角色群組的詳細資訊，請參閱下列主題：

  - [管理角色群組](manage-role-groups-exchange-2013-help.md)

  - [管理角色群組成員](manage-role-group-members-exchange-2013-help.md)

如果您要建立角色群組並且將指派給此角色群組的部分角色指派給新角色群組，請參閱 [管理角色群組](manage-role-groups-exchange-2013-help.md) 中的＜建立角色群組＞一節。

下列是您可以自訂此角色的一些方法：

  - **權限擁有者**   如果您組織中的權限是由 Exchange 管理員之外的特定群組所控制，您可以建立角色群組，然後將角色管理角色的一般及委派管理角色指派移至新的角色群組。這樣做可防止 組織管理 角色群組的成員管理任何 RBAC 權限。

  - **Active Directory 分割權限**   如果組織中安全性主體 (例如使用者帳戶) 的建立是由 Exchange 系統管理員以外的特定群組所控制，您可以建立一個角色群組，然後將「郵件收件者建立」角色與「安全性群組建立及成員資格」角色的一般和委派角色指派移至新的角色群組。這樣做可以防止 組織管理 角色群組的成員建立 Active Directory 物件。不過，他們可以繼續啟用新 Active Directory 物件的郵件功能。如需分割權限的詳細資訊，請參閱[了解分割權限](understanding-split-permissions-exchange-2013-help.md)。

## 自訂限制

任何角色都可新增至此角色群組或從此角色群組移除，但有下列限制：

  - 在委派角色指派可以從此角色群組移除之前，每個角色都必須至少有ㄧ個角色群組或 USG 的委派角色指派。

  - 在可以從此角色群組移除一般角色指派之前，「角色管理」角色必須至少有一個角色群組或 USG 的一般角色指派。

這些限制是為了防止您不小心將自己鎖在系統之外。透過在每個角色與一或多個角色群組或 USG 之間至少需要存在一個委派角色指派，您就永遠可以指派角色給角色受託人。透過在「角色管理」角色與一或多個角色群組或 USG 之間至少需要存在一個一般角色指派，您就永遠可以設定角色群組和角色指派。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>這些限制需要角色群組或 USG 是委派和一般角色指派的目標。如果最後一個指派是指派給使用者，您就無法移除「角色管理」角色的委派角色指派或一般指派。</td>
</tr>
</tbody>
</table>


## 只委派角色指派

組織管理 角色群組和管理角色之間的某些角色指派 (例如「信箱搜尋」和「未限定範圍的角色管理」) 僅委派角色指派。這些角色可讓您存取敏感或個人資訊 (例如信箱的內容)，或讓您建立功能強大的未限定範圍管理角色。

僅委派角色指派可讓 組織管理 角色群組的成員只能將關聯的角色指派給其他角色群組、管理角色指派原則、使用者或 USG。組織管理 角色群組的成員預設不會取得角色所提供的任何權限。這有助於避免意外曝露個人資訊，或造成權限意外提高。

但是，組織管理 角色群組的成員可為自己指定任何角色，藉以讓自己可執行任何工作。例如，組織管理 角色群組的成員可將信箱搜尋指定至 組織管理 角色群組。進行此角色指派之後，組織管理 角色群組的成員可以執行由「信箱搜尋」角色啟用的工作。

如需有關委派角色指派的詳細資訊，請參閱[了解管理角色指派](understanding-management-role-assignments-exchange-2013-help.md)。

## 其他權限

授與 組織管理 角色群組之成員的權限主要是由指派給角色群組的管理角色決定。不過，管理角色並未涵蓋您需要執行的所有工作。某些工作是在 Exchange 管理工具外部進行，因此不適用 RBAC 權限模式。對於這些工作，權限是透過將 組織管理 角色群組新增到某些 Active Directory 物件的存取控制清單 (ACL) 來提供。

下列工作的權限是透過 Active Directory 物件上的 ACL 的方式授與，而不是透過指派給 組織管理 角色群組的管理角色授與：

  - 使用 Setup.exe 執行 DomainPrep 及 ForestPrep

  - 在組織中部署其他伺服器

## 指派給此角色群組的管理角色

下表列出指派給此角色群組的所有管理角色，以及每個角色指派的下列屬性：

  - **一般指派**   可讓角色群組的成員存取相關管管理角色提供的管理角色項目。

  - **委派指派**   讓角色群組的成員能將特定角色指派給其他角色群組、角色指派原則、使用者或 USG。

  - **收件者讀取範圍**   決定角色群組的成員可以從 Active Directory 讀取的收件者物件。

  - **收件者寫入範圍**   決定角色群組的成員可以在 Active Directory 修改的收件者物件。

  - **組態讀取範圍**   決定角色群組的成員可以從 Active Directory 讀取的組態和伺服器物件。

  - **組態寫入範圍**   決定角色群組的成員可以在 Active Directory 修改的組態和伺服器物件。

如需角色指派和管理範圍的詳細資訊，請參閱下列主題：

  - [了解管理角色指派](understanding-management-role-assignments-exchange-2013-help.md)

  - [了解管理角色範圍](understanding-management-role-scopes-exchange-2013-help.md)

### 指派給此角色群組的管理角色

<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>管理角色</th>
<th>一般指派</th>
<th>委派指派</th>
<th>收件者讀取範圍</th>
<th>收件者寫入範圍</th>
<th>組態讀取範圍</th>
<th>組態寫入範圍</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="active-directory-permissions-role-exchange-2013-help.md">Active Directory 權限角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="address-lists-role-exchange-2013-help.md">地址清單角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="applicationimpersonation-role-exchange-2013-help.md">ApplicationImpersonation 角色</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><a href="archiveapplication-role-exchange-2013-help.md">ArchiveApplication 角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="audit-logs-role-exchange-2013-help.md">稽核記錄 」 角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="cmdlet-extension-agents-role-exchange-2013-help.md">Cmdlet 延伸代理程式角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="data-loss-prevention-role-exchange-2013-help.md">資料外洩防護角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="database-availability-groups-role-exchange-2013-help.md">資料庫可用性群組角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="database-copies-role-exchange-2013-help.md">資料庫副本的角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="databases-role-exchange-2013-help.md">資料庫角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="disaster-recovery-role-exchange-2013-help.md">嚴重損壞復原角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="distribution-groups-role-exchange-2013-help.md">通訊群組角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="edge-subscriptions-role-exchange-2013-help.md">Edge 訂閱角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="e-mail-address-policies-role-exchange-2013-help.md">電子郵件地址原則角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="exchange-connectors-role-exchange-2013-help.md">Exchange 連接器角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="exchange-server-certificates-role-exchange-2013-help.md">Exchange Server 憑證角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="exchange-servers-role-exchange-2013-help.md">Exchange 伺服器角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="exchange-virtual-directories-role-exchange-2013-help.md">Exchange 虛擬目錄角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="federated-sharing-role-exchange-2013-help.md">同盟的共用的角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="information-rights-management-role-exchange-2013-help.md">資訊版權管理角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="journaling-role-exchange-2013-help.md">日誌記錄角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="legal-hold-role-exchange-2013-help.md">法律保留角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="legalholdapplication-role-exchange-2013-help.md">LegalHoldApplication 角色</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="mail-enabled-public-folders-role-exchange-2013-help.md">擁有郵件功能的公用資料夾角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="mail-recipient-creation-role-exchange-2013-help.md">郵件建立收件者角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="mail-recipients-role-exchange-2013-help.md">郵件收件者角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="mail-tips-role-exchange-2013-help.md">郵件提示角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="mailbox-import-export-role-exchange-2013-help.md">信箱匯入匯出角色</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="mailbox-search-role-exchange-2013-help.md">信箱搜尋角色</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><a href="mailboxsearchapplication-role-exchange-2013-help.md">MailboxSearchApplication 角色</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="message-tracking-role-exchange-2013-help.md">郵件追蹤角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="migration-role-exchange-2013-help.md">移轉角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="monitoring-role-exchange-2013-help.md">監視角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="move-mailboxes-role-exchange-2013-help.md">移動信箱角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="officeextensionapplication-role-exchange-2013-help.md">OfficeExtensionApplication 角色</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="organization-client-access-role-exchange-2013-help.md">組織用戶端存取角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="organization-configuration-role-exchange-2013-help.md">組織設定角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="organization-transport-settings-role-exchange-2013-help.md">組織傳輸設定角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="pop3-and-imap4-protocols-role-exchange-2013-help.md">POP3 與 IMAP4 通訊協定的角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="public-folders-role-exchange-2013-help.md">公用資料夾角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="receive-connectors-role-exchange-2013-help.md">接收連接器角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="recipient-policies-role-exchange-2013-help.md">收件者原則角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="remote-and-accepted-domains-role-exchange-2013-help.md">遠端和公認的網域角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="reset-password-role-exchange-2013-help.md">重設密碼角色</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="retention-management-role-exchange-2013-help.md">保留管理角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="role-management-role-exchange-2013-help.md">角色管理角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="security-group-creation-and-membership-role-exchange-2013-help.md">安全群組建立與成員資格的角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="send-connectors-role-exchange-2013-help.md">傳送連接器角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="support-diagnostics-role-exchange-2013-help.md">支援診斷角色</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="teammailboxlifecycleapplication-role-exchange-2013-help.md">TeamMailboxLifecycleApplication 角色</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="transport-agents-role-exchange-2013-help.md">傳輸代理程式角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="transport-hygiene-role-exchange-2013-help.md">傳輸檢疫角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="transport-queues-role-exchange-2013-help.md">傳輸佇列角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="transport-rules-role-exchange-2013-help.md">傳輸規則角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="um-mailboxes-role-exchange-2013-help.md">UM 信箱角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="um-prompts-role-exchange-2013-help.md">UM 提示角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="unscoped-role-management-role-exchange-2013-help.md">未限定範圍的角色管理角色</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="unified-messaging-role-exchange-2013-help.md">整合的通訊角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="userapplication-role-exchange-2013-help.md">UserApplication 角色</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="user-options-role-exchange-2013-help.md">使用者選項角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="view-only-audit-logs-role-exchange-2013-help.md">僅檢視稽核記錄 」 角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><a href="view-only-configuration-role-exchange-2013-help.md">僅檢視設定角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="view-only-recipients-role-exchange-2013-help.md">僅檢視收件者角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><a href="workloadmanagement-role-exchange-2013-help.md">WorkloadManagement 角色</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="my-custom-apps-role-exchange-2013-help.md">我自訂應用程式的角色</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="my-marketplace-apps-role-exchange-2013-help.md">我市集應用程式的角色</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="mybaseoptions-role-exchange-2013-help.md">MyBaseOptions 角色</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="mycontactinformation-role-exchange-2013-help.md">MyContactInformation 角色</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="mydiagnostics-role-exchange-2013-help.md">MyDiagnostics 角色</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="mydistributiongroupmembership-role-exchange-2013-help.md">MyDistributionGroupMembership 角色</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>MyGAL</code></p></td>
<td><p><code>MyGAL</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="mydistributiongroups-role-exchange-2013-help.md">MyDistributionGroups 角色</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>MyGAL</code></p></td>
<td><p><code>MyDistributionGroups</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><a href="myprofileinformation-role-exchange-2013-help.md">MyProfileInformation 角色</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="myretentionpolicies-role-exchange-2013-help.md">MyRetentionPolicies 角色</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="myteammailboxes-role-exchange-2013-help.md">MyTeamMailboxes 角色</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="mytextmessaging-role-exchange-2013-help.md">MyTextMessaging 角色</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="myvoicemail-role-exchange-2013-help.md">MyVoiceMail 角色</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
</tbody>
</table>

