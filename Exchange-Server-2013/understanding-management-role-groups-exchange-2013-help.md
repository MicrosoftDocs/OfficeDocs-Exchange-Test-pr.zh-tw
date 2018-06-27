---
title: '了解管理角色群組: Exchange 2013 Help'
TOCTitle: 了解管理角色群組
ms:assetid: 2a92e06c-523e-4fd4-a937-152562b7741d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd638105(v=EXCHG.150)
ms:contentKeyID: 50472883
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 了解管理角色群組

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

*管理角色群組*是一個萬用安全性群組 (USG) 用於 Microsoft Exchange Server 2013中的角色型存取控制 (RBAC) 權限模型。管理角色群組簡化指派的管理角色的使用者群組。角色群組中的所有成員都指派角色相同的一組。系統管理員和專家角色定義Exchange 2013等組織管理、 收件者管理及其他工作中主要的管理工作指派角色群組。角色群組可讓您更輕鬆地指派龐大的一組權限給群組管理員或專家使用者。

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


**目錄**

Role group layers

Role group management

Built-in role groups

Linked role groups

Role group delegation

Role group membership

Role group creation workflow

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您要將權限指派給使用者，讓他們管理其自己的信箱或通訊群組，請參閱<a href="understanding-management-role-assignment-policies-exchange-2013-help.md">了解管理角色指派原則</a>。</td>
</tr>
</tbody>
</table>


## 角色群組層

以下是構成角色群組模型的各個層：

  - **角色群組成員**  *角色群組成員*為信箱、 萬用安全性群組 (USG) 或其他可以新增角色群組的成員身分的角色群組。當信箱、 USG 或其他角色群組新增角色群組的成員身分時，管理角色和角色群組之間進行的工作分派會套用至新的成員。這會授與新成員提供的管理角色的權限的所有。

  - **管理角色群組**  *管理角色群組*是包含信箱的特殊 USG、 Usg，與其他角色群組角色群組的成員。這是其中新增及移除的成員，而它也是已指派的管理角色。角色群組上的所有角色的組合會定義每個項目新增至角色群組的成員可以管理Exchange組織中。

  - **管理角色指派**  *管理角色指派*連結管理角色和角色群組。將管理角色指派給角色群組授與能夠使用 cmdlet 和參數所定義之管理角色的角色群組的成員。角色指派可使用可使用的工作分派至控制項的管理範圍。如需詳細資訊，請參閱[了解管理角色指派](understanding-management-role-assignments-exchange-2013-help.md)。

  - **管理角色範圍**  *管理角色範圍*會影響或角色指派上的影響的範圍。當角色範圍指派給角色群組時、 管理範圍所談的是什麼特別物件來管理可允許工作分派。工作分派以及其範圍，然後指定給角色群組的成員，以限制這些成員可以管理。範圍可以由組成的伺服器或資料庫、 組織單位或 server、 資料庫或收件者物件的篩選清單。如需詳細資訊，請參閱[了解管理角色範圍](understanding-management-role-scopes-exchange-2013-help.md)。

  - **管理角色**  *管理角色*是管理角色項目之群組的容器。角色用以定義可以指派角色的角色群組的成員所執行之特定工作。如需詳細資訊，請參閱[了解管理角色](understanding-management-roles-exchange-2013-help.md)。

  - **管理角色項目**   *管理角色項目*是在管理角色提供存取 cmdlet、 指令碼及其他特殊權限可讓執行特定工作的存取權的個別項目。最常角色項目包含單一 cmdlet 或指令碼和的 「 管理 」 角色可存取的參數與因此對其指派角色的角色群組。

下圖顯示上述清單中的每個角色群組層，以及每個層如何與其他層相關。

**管理角色群組層**

![管理角色群組層](images/Dd638105.a98c237c-7bdb-434b-8c98-22509e46cccf(EXCHG.150).gif "管理角色群組層")

如需有關 RBAC 的詳細資訊，請參閱[了解角色型存取控制](understanding-role-based-access-control-exchange-2013-help.md)。

回到頁首

## 角色群組管理

當您建立角色群組時，建立 USG 扮演的角色群組成員，並建立之間的角色群組與您指定的管理角色指派。或者，您也可以指定要套用至角色指派的管理範圍和您可以新增您想要為新的角色群組成員的任何信箱。

建立角色群組之後，每個圖層會變成獨立物件。若要在其中的所有層級的中央點結合在一起，但每個圖層個別管理會繼續角色群組。例如，若要修改其建立時套用到角色群組的管理範圍，您需要之後建立的角色群組變更每個個別的角色指派上的範圍。使用 cmdlet 可管理角色群組模型的個別層級執行的角色群組模型管理。

下表列出角色群組層以及您可用於管理每一層的程序主題。

### 角色群組管理主題

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>角色群組模型層</th>
<th>管理主題</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>角色群組成員</p></td>
<td><p><a href="manage-role-group-members-exchange-2013-help.md">管理角色群組成員</a></p>
<p></p></td>
</tr>
<tr class="even">
<td><p>角色群組</p></td>
<td><p><a href="manage-role-groups-exchange-2013-help.md">管理角色群組</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>管理角色及指派</p></td>
<td><p><a href="manage-role-groups-exchange-2013-help.md">管理角色群組</a></p></td>
</tr>
<tr class="even">
<td><p>管理角色項目</p></td>
<td><p><a href="add-a-role-entry-to-a-role-exchange-2013-help.md">將角色項目新增至角色</a></p>
<p><a href="change-a-role-entry-exchange-2013-help.md">變更的角色項目</a></p>
<p><a href="remove-a-role-entry-from-a-role-exchange-2013-help.md">從角色移除角色項目</a></p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>變更管理角色的角色群組中的管理角色項目是進階的任務以及通常不需要在大多數情況下。而您可以使用符合您需求的原先既管理角色。如需詳細資訊，請參閱<a href="built-in-role-groups-exchange-2013-help.md">內建角色群組</a>。</td>
</tr>
</tbody>
</table>

</td>
</tr>
</tbody>
</table>


回到頁首

## 內建角色群組

內建角色群組是隨附Exchange 2013的角色。這些提供給您可用來提供不同的層級的管理權限的使用者群組的角色群組的一組。您可以新增或移除使用者或從任何內建角色群組。您也可以新增或移除角色指派至或來自大部分的角色群組。唯一的例外狀況如下所示：

  - 您無法從 組織管理 角色群組移除任何委派角色指派。

  - 您無法從 組織管理 角色群組移除角色管理角色。

下表列出Exchange 2013所含的所有內建角色群組。如需內建角色群組的詳細資訊，請參閱[內建角色群組](built-in-role-groups-exchange-2013-help.md)。

### 內建角色群組

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>角色群組</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p></td>
<td><p>身為組織管理角色群組成員的系統管理員系統管理存取整個Exchange 2013組織而且可執行幾乎任何對任何Exchange 2013物件，某些例外的工作。根據預設，此角色群組的成員不能執行信箱搜尋的與管理未限定範圍的頂層管理角色。</p></td>
</tr>
<tr class="even">
<td><p><a href="view-only-organization-management-exchange-2013-help.md">僅限檢視組織管理</a></p></td>
<td><p>屬於 僅限檢視組織管理 角色群組之成員的系統管理員可在 Exchange 組織中檢視任何物件的內容。</p></td>
</tr>
<tr class="odd">
<td><p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p></td>
<td><p>屬於 收件者管理 角色群組之成員的系統管理員，擁有在 Exchange 2013 組織內建立或修改 Exchange 2013 收件者的系統管理存取權。</p></td>
</tr>
<tr class="even">
<td><p><a href="um-management-exchange-2013-help.md">UM 管理</a></p></td>
<td><p>屬於 UM 管理 角色群組成員的系統管理員可以管理 Exchange 組織中的功能，例如整合通訊 (UM) 服務組態、信箱上的 UM 內容、UM 提示及 UM 自動語音應答組態。</p></td>
</tr>
<tr class="odd">
<td><p><a href="discovery-management-exchange-2013-help.md">探索管理</a></p></td>
<td><p>系統管理員或是屬於 探索管理 角色群組成員的使用者可在 Exchange 組織中執行信箱搜尋，以尋找符合特定準則的資料，並可以對信箱設定訴訟資料暫留。</p></td>
</tr>
<tr class="even">
<td><p><a href="records-management-exchange-2013-help.md">記錄管理</a></p></td>
<td><p>屬於 記錄管理 角色群組成員的使用者可以設定符合性功能，例如保留原則標記、訊息分類、傳輸規則等。</p></td>
</tr>
<tr class="odd">
<td><p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p></td>
<td><p>屬於此角色群組之成員的系統管理員可以設定伺服器特定的傳輸組態、用戶端存取以及信箱功能，例如資料庫複本、憑證、傳輸佇列及傳送連接器、虛擬目錄以及用戶端存取通訊協定。</p></td>
</tr>
<tr class="even">
<td><p><a href="help-desk-exchange-2013-help.md">服務台</a></p></td>
<td><p>屬於服務台角色群組成員的使用者可以執行 Exchange 2013 收件者之受限的收件者管理。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hygiene-management-exchange-2013-help.md">檢疫管理</a></p></td>
<td><p>檢疫管理角色群組成員的使用者可以設定Exchange 2013的反垃圾郵件和反惡意程式碼功能。Exchange 2013與整合協力廠商程式可以將服務帳戶新增至這些 cmdlet 來擷取並設定Exchange設定所需的程式存取權授與此角色群組。</p></td>
</tr>
<tr class="even">
<td><p><a href="compliance-management-exchange-2013-help.md">規範管理</a></p></td>
<td><p>規範管理角色群組中的成員可根據其原則來設定並管理 Exchange 規範組態。</p></td>
</tr>
<tr class="odd">
<td><p><a href="public-folder-management-exchange-2013-help.md">公用資料夾管理</a></p></td>
<td><p>屬於「公用資料夾管理」角色群組成員的系統管理員可以在執行 Exchange 2013 的伺服器上管理公用資料夾。</p></td>
</tr>
<tr class="even">
<td><p><a href="delegated-setup-exchange-2013-help.md">委派安裝</a></p></td>
<td><p>身為「委派安裝」角色群組成員的系統管理員，可部署先前已由 Exchange 2013 角色群組的成員提供的 組織管理 伺服器。</p></td>
</tr>
</tbody>
</table>


回到頁首

## 連結的角色群組

在專用的資源樹系中安裝Exchange 2013並放置在其他、 受信任的外部樹系中的使用者的組織使用連結的角色群組。連結的角色群組顧名思義，建立Exchange樹系中的角色群組和 USG 之間的連結外部樹系中。當您想要管理Exchange的系統管理員Active Directory網域服務 (AD DS) 使用者帳戶不位於相同的資源樹系Exchange，這很有用。連結的角色群組只可關聯一個外部 USG。此外，您不需要建立Exchange樹系與外部樹系之間的雙向信任。Exchange樹系需要信任外部樹系，但不需要外部樹系信任Exchange樹系。

如需多重樹系拓撲中權限的詳細資訊，請參閱[了解多重樹系權限](understanding-multiple-forest-permissions-exchange-2013-help.md)。

連結的角色群組是由兩個部分所組成：

  - **連結的角色群組**   連結的角色群組是一種容器物件，可將外部 USG 與指派給角色群組的管理角色指派相關聯。

  - **外部 USG**   外部 USG 包含的成員應被授與連結的角色群組所提供的權限。

當您建立連結的角色群組時，提供包含您想要管理Exchange樹系之的使用者的外部樹系的網域控制站和存取外部樹系所需的成員、 外部 USG 的名稱，以及認證包含這些使用者 USG。Exchange新增連結的角色群組的外部 USG 的安全性識別碼 (SID)。因為 USG SID 的外部 USG 的唯一識別，我們強烈建議您指定外部的樹系的角色群組的名稱中有多個外部樹系。

連結的角色群組不包含任何成員。該角色群組的成員的所有管理使用的外部 USG。這表示您無法使用**Update-RoleGroupMember**、 **Add-RoleGroupMember**或**Remove-RoleGroupMember** cmdlet 可新增或移除角色群組成員。當您新增成員的外部 USG 時，他們會提供連結的角色群組所提供的權限。

您無法變更標準的角色群組，其中包含其專屬成員、 連結的角色群組，反之亦然。如果您想要從標準的角色群組的角色群組變更為連結的角色群組，您必須建立新的連結的角色群組和複寫存在於連結的角色群組的標準角色群組的管理角色指派。這也是內建角色群組的大小寫因為它們是標準的角色群組。如果您想要執行的Exchange樹系的管理所有來自外部樹系，您需要建立新的連結的角色群組並將存在的管理角色上的內建角色群組新增至新的連結的角色群組。如需如何完成這項作業的詳細資訊，請參閱[建立鏡像內建角色群組的連結的角色群組](create-linked-role-groups-that-mirror-built-in-role-groups-exchange-2013-help.md)。

回到頁首

## 角色群組委派

根據預設， 組織管理角色群組的成員可以新增和移除角色群組的成員。不過，您可能要讓未組織管理角色群組的成員新增及移除角色群組成員的使用者。若是如此，您可以使用角色群組委派。

角色群組委派是由上每個角色群組的**ManagedBy**屬性所控制。**ManagedBy**屬性包含清單中的使用者可以新增和移除該角色群組的成員或變更角色群組的設定。除非它們也角色群組成員的角色群組所提供的任何權限都指派給使用者。

如果**ManagedBy**屬性設定的角色群組、 僅限列為 「 角色群組管理員在屬性可以修改角色群組或角色群組的成員資格預設這些使用者。不過，在修改角色群組或角色群組成員資格的指令程式上的選擇性參數可以覆寫該限制。*BypassSecurityGroupManagerCheck* 參數可用來為組織管理角色的成員或指派，直接或間接角色管理管理角色的使用者。使用此參數時，則會忽略**ManagedBy**屬性和使用者可以修改角色群組或角色群組成員資格。

若未在角色群組上設定 **ManagedBy** 內容，則只有屬於 組織管理 角色成員或是直接或間接被指派角色管理管理角色的使用者，才能修改角色群組或角色群組成員資格。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用委派角色指派可能會指派角色指派給角色群組。使用委派角色指派，已指派委派的角色的角色群組的成員可以將該角色指派給其他角色群組、 指派原則、 使用者或 USG。角色群組的成員可以指派只有該角色並無法委派角色] 群組中，除非他們正在也會新增至<strong>ManagedBy</strong>屬性。如需委派的角色指派的詳細資訊，請參閱<a href="understanding-management-role-assignments-exchange-2013-help.md">了解管理角色指派</a>。</td>
</tr>
</tbody>
</table>


如需如何管理角色群組委派的詳細資訊，請參閱[管理角色群組](manage-role-groups-exchange-2013-help.md)。

回到頁首

## 角色群組成員資格

使用者提出時角色群組的成員，指派給角色群組的管理角色指派給使用者。如果使用者是多個角色群組的成員，每個角色群組的管理角色是彙總及指派給使用者。使用者、 Usg 及其他角色群組可以角色群組的成員。

只有屬於 組織管理 或角色管理角色群組之成員的使用者，以及已被委派在角色群組中新增及移除使用者之能力的使用者，才能管理角色群組成員資格。

如需如何管理角色群組成員的詳細資訊，請參閱[管理角色群組成員](manage-role-group-members-exchange-2013-help.md)。

## 角色群組建立工作流程

如前文所述、 角色群組是由數個圖層組成。若要協助您瞭解什麼建立角色群組時，請考慮下列的範例中，會建立新的角色群組。

    New-RoleGroup -Name "Seattle Recipient Management" -Roles "Mail Recipients", "Distribution Groups", "Move Mailboxes", "UM Mailboxes" -CustomRecipientWriteScope "Seattle Users", -ManagedBy "Brian", "David", "Katie" -Members "Ray", "Jenn", "Maria", "Chris", "Maija", "Carter", "Jenny", "Sam", "Lukas", "Isabel", "Katie"

執行上述命令時會發生下列情況：

1.  會建立新的角色群組物件，該物件是名為「Seattle Recipient Management」的特殊 USG。

2.  信箱光線、 Jenn、 馬利亞、 Chris、 Maija、 Carter、 黎、 Sam、 Lukas、 Isabel、 產業 katie 了新增及角色群組的成員。這些使用者會收到此角色群組所提供的權限。

3.  使用者 Brian 與 David 新增至角色群組的**ManagedBy**屬性。這些使用者可以新增和移除成員與角色群組，但將不會授與因為它們不是成員角色群組所提供的任何權限。產業 katie 了也會新增至角色群組的**ManagedBy**屬性。因為其新增至**ManagedBy**屬性，她則角色群組的成員時可以新增或移除角色群組的成員與時也會收到角色群組所提供的權限。

4.  會建立下列管理角色指派。角色指派指派給角色群組的命令中指定每個管理角色。管理範圍 Seattle 使用者新增至每個角色指派。每個角色指派的名稱是被指派管理角色的組合及角色群組名稱。
    
      - `Mail Recipients_Seattle Recipient Management`
    
      - `Distribution Groups_Seattle Recipient Management`
    
      - `Move Mailboxes_Seattle Recipient Management`
    
      - `UM Mailboxes_Seattle Recipient Management`

如果您比較至管理角色群組層估計本主題中前面此命令的結果，您可以看到每個步驟顯示至角色群組層級的關聯。您可以再參照顯示在 「 管理角色群組 」 中的管理角色群組管理主題稍早中管理每個角色群組層本主題。

回到頁首

