---
title: '了解管理角色: Exchange 2013 Help'
TOCTitle: 了解管理角色
ms:assetid: 887b0a64-84b1-4b8c-9547-e456ea6f5dbd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd298116(v=EXCHG.150)
ms:contentKeyID: 50473689
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 了解管理角色

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-07_

管理角色是用於 Microsoft Exchange Server 2013 的角色存取控制 (Role Based Access Control，RBAC) 權限模式的一部分。角色可當作指令程式邏輯群組的一部分整合，提供您存取權限來檢視或修改 Exchange 2013 元件 (如信箱、傳輸規則和收件者) 的組態。管理角色可進一步整合到稱為管理角色群組和管理角色指派原則的較大群組中，以便管理功能範圍和接收者組態。角色群組和角色指派原則會分別將權限指派給系統管理員和一般使用者。如需管理角色群組和管理角色指派原則的詳細資訊，請參閱[了解角色型存取控制](understanding-role-based-access-control-exchange-2013-help.md)。

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

Built-in management roles

Unscoped top-level management roles

Custom management roles

Management role hierarchy

Management role entries

Unscoped top-level role entries

Management role types

For more information

管理角色範圍和管理角色指派是操作管理角色的重要元件。如需這些元件的詳細資訊，請參閱下列主題：

  - [了解管理角色範圍](understanding-management-role-scopes-exchange-2013-help.md)

  - [了解管理角色指派](understanding-management-role-assignments-exchange-2013-help.md)

要尋找與管理角色相關的管理工作嗎？請參閱[權限](permissions-exchange-2013-help.md)。

## 內建管理角色

Exchange 2013 提供許多可用於管理組織的內建管理角色。每個角色都包含可讓使用者用來管理特定 Exchange 元件的指令程式和參數。下列是一些內建管理角色的範例：

  - **郵件收件者**   可讓系統管理員管理信箱、連絡人和郵件使用者。

  - **傳輸規則**   可讓指派角色的系統管理員或專家使用者管理傳輸規則功能。

  - **通訊群組**   可讓指派角色的系統管理員或專家使用者管理通訊群組和通訊群組成員。

  - **MyPersonalInformation**   可讓使用者修改其自己的住家電話號碼和網站位址。

如需 Exchange 2013 隨附管理角色的完整清單，請參閱[內建管理角色](built-in-management-roles-exchange-2013-help.md)。

您可以取得 Exchange 2013 所提供的內建角色，並以任何方式將其合併以建立適用於您企業的權限模式。例如，如果您要角色群組的成員管理收件者和公用資料夾，可將「郵件收件者」和「公用資料夾」角色都指派給角色群組。通常是將角色指派給角色群組或角色指派原則。如果您要控制細微層次的權限，還可以直接將管理角色指派給使用者。我們建議您使用角色群組和角色指派原則 (而非直接使用者角色指派) 以簡化您的權限模式。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您僅可將一般使用者管理角色指派給角色指派原則。</td>
</tr>
</tbody>
</table>


無法變更內建的管理角色。但您可根據內建管理角色來建立管理角色，然後將這些新角色指派給角色群組或角色指派原則。然後您可變更新的管理角色以符合您的需求。這應為只有在必要時才進行的少數進階工作。

如需根據內建 Exchange 角色建立自訂角色的詳細資訊，請參閱本主題稍後說明的Custom Management Roles。

您必須指派管理角色，它們才會生效。通常是將管理角色指派給角色群組與角色指派原則。在某些情況下，也可直接將角色指派給使用者，雖然這是只有在必要時才進行的少數進階工作。

如需指派管理角色的詳細資訊，請參閱下列主題：

  - [管理角色群組](manage-role-groups-exchange-2013-help.md)

  - [管理角色指派原則](manage-role-assignment-policies-exchange-2013-help.md)

  - [將角色新增至使用者或 USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

如需管理角色指派的詳細資訊，請參閱[了解管理角色指派](understanding-management-role-assignments-exchange-2013-help.md)。

回到頁首

## 未限定範圍的頂層管理角色

未限定範圍的頂層管理角色是一種特殊類型的管理角色，可讓您將自訂指令碼和非 Exchange指令程式的存取權授與使用 RBAC 的使用者。一般管理角色只提供 Exchange指令程式的存取權。如果必須提供在 Exchange 伺服器上執行非 Exchange指令程式的存取權，或如果需要發行可由使用者執行的指令碼，就必須將它們新增至未限定範圍的角色。它們之所以稱爲頂層角色，是因爲如果建立的未限定範圍角色並非衍生自上層角色，它就沒有上層項目，而且是 Exchange 2013 所提供的對等內建管理角色。若要表示您想建立未限定範圍頂層角色的項目，必須搭配 **New-ManagementRole** 指令程式來使用 *UnscopedTopLevel* 參數。

未限定範圍角色之所以如此命名，是因為並不像一般的管理角色那樣，無法將其納入特定目標的範圍。未限定範圍的角色一律適用於全組織。這表示被指派未限定範圍角色者可以修改 Exchange 2013 組織中的任何物件。基於這個理由，您必須特別注意確保徹底測試透過未限定範圍角色提供的指令碼與指令程式，以便知道它們會修改什麼內容，如此才能謹慎指派未限定範圍的角色。

可將未限定範圍角色指派給諸如角色群組、管理角色、使用者和萬用資訊安全群組 (USG) 等角色受託人。不可將它們指派給管理角色指派原則。

雖然無法將 Exchange 指令程式新增為未限定範圍角色上的管理角色項目，但可將它們包含在新增為角色項目的指令碼中。這可讓您建立執行 Exchange 工作的自訂指令碼，然後可指派給使用者。一項實用的案例是當使用者必須執行通常在所屬管理層級以外的高權限工作時，以及建構新管理角色或角色群組有問題時。您可建立執行此特定函數的指令碼，將其新增到未限定範圍角色，然後將未限定範圍角色指派給使用者。使用者就僅能執行由指令碼提供的特定函數。

您還必須將新增至未限定範圍角色的角色項目指定為未限定範圍的頂層角色項目。如需未限定範圍的頂層角色項目的詳細資訊，請參閱本主題稍後說明的Unscoped Top-Level Role Entries。

根據預設，組織管理 角色群組沒有建立或管理未限定範圍角色群組的權限。這是要避免錯誤建立或修改未限定範圍的角色群組。組織管理 角色群組可將「未限定範圍角色管理」的管理角色委派給自己和其他角色受託人。如需如何建立未限定範圍頂層管理角色的詳細資訊，請參閱[建立未限定範圍的角色](create-an-unscoped-role-exchange-2013-help.md)。

回到頁首

## 自訂管理角色

當內建管理角色不符合您使用者的需求時，可根據內建 Exchange 角色建立自訂管理角色。當您建立自訂管理角色時，新下層角色會繼承上層角色的所有管理角色項目。然後您可選擇在自訂管理角色中要保留哪些管理角色項目，並移除所有不要的項目。

自訂角色成為用於建立新角色的下層角色。您只能使用存在於上層角色中之新下層角色中的管理角色項目。如需詳細資訊，請參閱本主題稍後的小節：

  - Management Role Hierarchy

  - Management Role Entries

必須執行多個步驟才能建立自訂管理角色，而且這是只有在必要時才進行的少數進階工作。在您建立自訂管理角色之前，請先確保其中一個現有的內建管理角色並未提供您所需的權限。如需內建管理角色的詳細資訊，或者如果您要建立自訂管理角色，請參閱以下主題：

  - [內建管理角色](built-in-management-roles-exchange-2013-help.md)

  - [進階權限](advanced-permissions-exchange-2013-help.md)

如需如何建立管理角色的詳細資訊，請參閱[建立角色](create-a-role-exchange-2013-help.md)。

回到頁首

## 管理角色階層

管理角色有區分上層與子項的階層。根據預設，階層頂端是 Exchange 2013 中所提供的內建管理角色。當您建立角色時，會建立上層角色的副本。新角色是所複製角色的下層。然後您可自訂新角色以符合所指派之系統管理員或使用者的需要。

可使用自訂角色建立角色。當您從現有的自訂角色建立角色時，現有自訂角色會保持為其上層角色的下層，但同時成為新角色的上層。每次複製角色時，新下層角色只能包含存在於直屬上層角色中的角色項目。

每一個管理角色都有無法變更的特定角色類型。角色類型會定義角色的基本使用環境。當建立下層角色時，會從上層角色複製角色類型。

**管理角色階層**

![RBAC 管理角色階層式圖表](images/Dd298116.6851c829-ca8f-40e7-a67c-cc9e85c33953(EXCHG.150).gif "RBAC 管理角色階層式圖表")

上圖說明數種管理角色的階層關係。「郵件收件者」和「服務台」角色是內建角色。衍生自這些角色的所有下層角色會繼承每個內建角色的角色類型。例如，從「郵件收件者」角色直接或間接衍生的所有下層角色都會繼承 `MailRecipients` 角色類型。

「Seattle 收件者系統管理員」自訂角色是「郵件收件者」內建角色的子項，但同時也是「Seattle 銷售收件者系統管理員」自訂角色與「Seattle 合法收件者系統管理員」自訂角色的上層。「Seattle 收件者系統管理員」自訂角色僅包含在「郵件收件者」角色中可用之指令程式的子集。「Seattle 收件者系統管理員」自訂角色的下層角色只能包含也存在於該角色中的指令程式。例如，如果指令程式存在於「郵件收件者」角色中，但不存在於「Seattle 收件者系統管理員」自訂角色中，就無法將指令程式新增至「Seattle 銷售收件者系統管理員」自訂角色。

所有自訂角色都會遵循與上述角色相同的模式。如需如何存取管理角色上所控制之指令程式的詳細資訊，請參閱本主題下一節的Management Role Entries。

回到頁首

## 管理角色項目

每個管理角色，不論是否為自訂 Exchange 角色或未限定範圍角色，都必須至少有一個管理角色項目。項目是由您要提供的單一指令程式和其參數、指令碼或特殊權限所組成。如果指令程式或指令碼並非管理角色上的項目，則不可透過該角色存取該指令程式或指令碼。同樣地，如果參數不存在於項目中，則不可透過該角色存取該指令程式或指令碼上的參數。

Exchange 2013 可讓您管理根據內建 Exchange 管理頂層角色以及未限定範圍角色的角色項目。根據內建 Exchange 頂層角色的角色只能包含 Exchange 2013指令程式的角色項目。若要新增可讓使用者使用的自訂指令碼或非 Exchange 指令程式，您必須將它們新增為未限定範圍頂層角色的未限定範圍角色項目。如需未限定角色項目的詳細資訊，請參閱本主題稍後說明的Unscoped Top-Level Role Entries。

所有角色項目，不論是否為 Exchange 指令程式或未限定範圍者，都要遵循與以下小節所述相同的原則。

如需管理角色項目的詳細資訊，請參閱[管理角色和角色項目](management-roles-and-role-entries-exchange-2013-help.md)。

## 上層和下層管理角色的關聯性

如前文所提，管理角色項目，包含指令程式和其參數，都必須存在於直屬上層角色中，才能新增項目到下層角色。例如，如果上層角色沒有 **New-Mailbox** 的項目，則無法指派該指令程式到下層角色。此外，如果上層角色有 **Set-Mailbox**，但已從項目中移除 *Database* 參數，則無法將 **Set-Mailbox**指令程式上的 *Database* 參數新增至下層角色上的項目。

因為如果項目不在上層角色中，您就無法新增管理角色項目到下層角色，且因為角色是根據特定的角色類型，所以當要建立自訂角色時，必須仔細選擇要複製的上層角色。

回到頁首

## 管理角色項目名稱

管理角色項目名稱是與它們相關之管理角色、指令程式或指令碼名稱的組合。角色名稱和指令程式或指令碼是以反斜線字元 (\\) 分隔。例如，「郵件收件者」角色上之 **Set-Mailbox**指令程式的角色項目名稱是 `Mail Recipients\Set-Mailbox`。如果角色項目名稱包含空格，請使用引號 (") 括住名稱。

可以在角色項目名稱中使用萬用字元 (\*) 以傳回所有與所輸入內容相符的角色項目。可在反斜線字元的任一側使用萬用字元。下表包含幾個在角色項目名稱中變化使用萬用字元的方式。

**含有萬用字元的管理角色項目名稱**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>範例</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>*\*</code></p></td>
<td><p>傳回所有角色的所有角色項目清單。</p></td>
</tr>
<tr class="even">
<td><p><code>*\Set-Mailbox</code></p></td>
<td><p>傳回包含 <strong>Set-Mailbox</strong>指令程式的所有角色項目清單。</p></td>
</tr>
<tr class="odd">
<td><p><code>Mail Recipients\*</code></p></td>
<td><p>傳回「郵件收件者」角色上所有角色項目的清單。</p></td>
</tr>
<tr class="even">
<td><p><code>Mail Recipients\*Mailbox</code></p></td>
<td><p>傳回「郵件收件者」角色上包含以 Mailbox 結尾之指令程式的所有角色項目清單。</p></td>
</tr>
<tr class="odd">
<td><p><code>My*\*Group*</code></p></td>
<td><p>傳回所有以 My 開頭之角色且指令程式名稱中包含字串 Group 的所有角色項目清單。</p></td>
</tr>
</tbody>
</table>


## 未限定範圍的頂層角色項目

未限定範圍的頂層角色項目要搭配未限定範圍的頂層管理角色使用，以根據自訂指令碼或非 Exchange 指令程式建立角色。每個未限定範圍的角色項目都與單一自訂指令碼或非 Exchange 指令程式相關聯。若要表示想在未限定範圍角色上建立未限定範圍角色項目，必須指定 **Add-ManagementRoleEntry**指令程式上的 *UnscopedTopLevel* 參數。

當您新增未限定範圍角色項目時，必須指定可以與指令碼或非 Exchange 指令程式搭配使用的所有參數。當您新增角色項目時，Exchange 會嘗試驗證您所提供的參數。僅有建立時新增至角色項目的參數適用於指派到未限定範圍角色的使用者。如果您新增參數到指令碼或非 Exchange 指令程式，或如果重新命名參數，則必須手動更新角色項目。Exchange 不會檢查是否已變更未限定範圍角色項目上的現有參數。如果變更指令碼中角色項目上的參數，且您嘗試使用該參數，則命令會失敗。

您新增至未限定範圍角色項目的指令碼必須位於系統管理員和使用者以 Exchange 2013 管理管理命令介面所連接之每部伺服器上的 Exchange 指令碼目錄。如果您嘗試新增的未限定範圍角色項目，是根據不存在於用來新增角色項目之伺服器上 Exchange 2013 指令碼目錄中的指令碼，則會發生錯誤。Exchange 2013 指令碼目錄的預設安裝位置是 C:\\Program Files\\Microsoft\\Exchange Server\\V15\\RemoteScripts。

您新增至未限定範圍角色項目的非 Exchange 指令程式，必須安裝於系統管理員和使用者以管理命令介面所連接且想使用指令程式的每部 Exchange 2013 伺服器上。如果您嘗試新增的未限定範圍角色項目，是根據並非安裝於用來新增角色項目之 Exchange 伺服器上的非 Exchange 2013 指令程式，則會發生錯誤。當您新增非 Exchange 指令程式時，必須指定包含非 Windows指令程式的 Exchange PowerShell 嵌入式管理單元名稱。

如需如何新增未限定範圍管理角色項目的詳細資訊，請參閱[將角色項目新增至角色](add-a-role-entry-to-a-role-exchange-2013-help.md)。

回到頁首

## 管理角色類型

管理角色類型是所有的管理角色的基礎。類型會定義指定角色類型之所有管理角色上定義的隱含範圍，並且可充當相關角色的邏輯群組。所有衍生自上層內建管理角色的管理角色有相同的角色類型。請參閱本主題稍早的管理角色階層圖，以了解此關係。管理角色類型也代表可新增至與角色類型相關之角色的指令程式及其參數的最大集合。

管理角色類型分成下列類別：

  - **系統管理員或專家**   與系統管理員或專家角色類型相關的角色，在 Exchange 組織中影響範圍較大。此角色類型的角色可從事諸如伺服器或收件者管理、組織組態、規範管理、稽核以及更多的這類工作。

  - **使用者為主**   與使用者為主角色類型相關的角色會對個別使用者造成一定範圍的密切影響。此角色類型的角色可從事諸如使用者設定檔組態、自我管理、使用者所擁有通訊群組的管理以及更多這類的工作。
    
    與使用者為主角色類型相關的角色名稱，以及使用者為主的角色類型名稱，都是以 My 開頭。

  - **專業**   與專業角色類型相關的角色可從事非系統管理或非使用者為主等角色類型的工作。此角色類型的角色可從事諸如應用程式模擬和以及使用非 Exchange 指令程式或指令碼這樣的工作。

下表列出 Exchange 2013 中所有的系統管理員管理角色類型，以及角色類型所允許的組態是否套用至整個 Exchange 組織或僅套用到個別伺服器。如需與這裡每種角色類型相關之管理角色的詳細資訊，包含每個角色的描述、誰可獲益於受指派的角色以及其他資訊，請參閱[內建管理角色](built-in-management-roles-exchange-2013-help.md)。

**系統管理員角色類型**


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>管理角色類型</th>
<th>內建管理角色</th>
<th>描述</th>
<th>組織或伺服器</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>ActiveDirectoryPermissions</code></p></td>
<td><p><a href="active-directory-permissions-role-exchange-2013-help.md">Active Directory 權限角色</a></p></td>
<td><p>此角色類型與讓系統管理員設定組織中 Active Directory 權限的角色相關。使用 Active Directory 權限或存取控制清單 (ACL) 的部分功能，包括傳輸的 [傳送] 和 [接收] 連接器，以及信箱的 [以下列傳送] 和 [傳送代理者] 權限。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>直接在 Active Directory 物件上設定的權限無法透過 RBAC 強制執行。</td>
</tr>
</tbody>
</table>

</td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>AddressLists</code></p></td>
<td><p><a href="address-lists-role-exchange-2013-help.md">地址清單角色</a></p></td>
<td><p>此角色類型與可讓系統管理員管理組織中通訊清單、全域通訊清單 (GAL) 及離線通訊清單的角色相關聯。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>ApplicationImpersonation</code></p></td>
<td><p><a href="applicationimpersonation-role-exchange-2013-help.md">ApplicationImpersonation 角色</a></p></td>
<td><p>此角色類型與可讓應用程式模擬組織中的使用者來代表使用者執行工作之角色相關聯。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>ArchiveApplication</code></p></td>
<td><p><a href="archiveapplication-role-exchange-2013-help.md">ArchiveApplication 角色</a></p></td>
<td><p>此角色類型與讓夥伴應用程式擷取組織中使用者信箱項目的角色相關聯。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>AuditLogs</code></p></td>
<td><p><a href="audit-logs-role-exchange-2013-help.md">稽核記錄 」 角色</a></p></td>
<td><p>此角色類型與可讓系統管理員管理組織中系統管理員稽核記錄設定的角色相關聯。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>CmdletExtensionAgents</code></p></td>
<td><p><a href="cmdlet-extension-agents-role-exchange-2013-help.md">Cmdlet 延伸代理程式角色</a></p></td>
<td><p>此角色類型與讓系統管理員管理組織中指令程式延伸代理程式的角色相關聯。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>DataLossPrevention</code></p></td>
<td><p><a href="data-loss-prevention-role-exchange-2013-help.md">資料外洩防護角色</a></p></td>
<td><p>此角色類型與組織中建立和管理防止資料遺失 (DLP) 原則及其原則內之規則的角色相關聯。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>DatabaseAvailabilityGroups</code></p></td>
<td><p><a href="database-availability-groups-role-exchange-2013-help.md">資料庫可用性群組角色</a></p></td>
<td><p>此角色類型與可讓系統管理員管理組織中資料庫可用性群組 (DAG) 的角色相關聯。直接或間接指派此角色的系統管理員為最高層級的系統管理員，負責組織中的高可用性設定。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>DatabaseCopies</code></p></td>
<td><p><a href="database-copies-role-exchange-2013-help.md">資料庫副本的角色</a></p></td>
<td><p>此角色類型與讓系統管理員管理個別伺服器上資料庫副本的角色相關聯。</p></td>
<td><p>伺服器</p></td>
</tr>
<tr class="even">
<td><p><code>Databases</code></p></td>
<td><p><a href="databases-role-exchange-2013-help.md">資料庫角色</a></p></td>
<td><p>此角色類型與讓系統管理員建立、管理、裝載及卸載個別伺服器上之信箱資料庫的角色相關聯。</p></td>
<td><p>伺服器</p></td>
</tr>
<tr class="odd">
<td><p><code>DisasterRecovery</code></p></td>
<td><p><a href="disaster-recovery-role-exchange-2013-help.md">嚴重損壞復原角色</a></p></td>
<td><p>此角色類型與讓系統管理員還原信箱和信箱資料庫、建立信箱資料庫和組織中執行資料庫可用性群組之資料中心轉換和回溯的角色相關聯。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>DistributionGroups</code></p></td>
<td><p><a href="distribution-groups-role-exchange-2013-help.md">通訊群組角色</a></p></td>
<td><p>此角色類型與讓系統管理員建立和管理組織中通訊群組和通訊群組成員的角色相關聯。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>EdgeSubscriptions</code></p></td>
<td><p><a href="edge-subscriptions-role-exchange-2013-help.md">Edge 訂閱角色</a></p></td>
<td><p>此角色類型與讓系統管理員管理Exchange 2010 Edge Transport server 和Exchange 2013組織中的信箱伺服器之間 edge 同步處理和訂閱設定的角色相關聯。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>EmailAddressPolicies</code></p></td>
<td><p><a href="e-mail-address-policies-role-exchange-2013-help.md">電子郵件地址原則角色</a></p></td>
<td><p>此角色類型與讓系統管理員管理組織中電子郵件地址原則的角色相關聯。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>ExchangeConnectors</code></p></td>
<td><p><a href="exchange-connectors-role-exchange-2013-help.md">Exchange 連接器角色</a></p></td>
<td><p>此角色類型與讓系統管理員建立、修改、檢視和移除傳遞代理程式連接器的角色相關聯。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>ExchangeServerCertificates</code></p></td>
<td><p><a href="exchange-server-certificates-role-exchange-2013-help.md">Exchange Server 憑證角色</a></p></td>
<td><p>此角色類型與讓系統管理員建立、匯入、匯出和管理個別伺服器上 Exchange 伺服器憑證的角色相關聯。</p></td>
<td><p>伺服器</p></td>
</tr>
<tr class="odd">
<td><p><code>ExchangeServers</code></p></td>
<td><p><a href="exchange-servers-role-exchange-2013-help.md">Exchange 伺服器角色</a></p></td>
<td><p>此角色類型與讓系統管理員管理個別伺服器上 Exchange 伺服器組態的角色相關聯。</p></td>
<td><p>伺服器</p></td>
</tr>
<tr class="even">
<td><p><code>ExchangeVirtualDirectories</code></p></td>
<td><p><a href="exchange-virtual-directories-role-exchange-2013-help.md">Exchange 虛擬目錄角色</a></p></td>
<td><p>此角色類型與讓系統管理員管理個別伺服器上 Outlook Web App、Microsoft ActiveSync、離線通訊錄 (OAB)、自動探索、Windows PowerShell 和 Exchange 系統管理中心虛擬目錄的角色相關聯。</p></td>
<td><p>伺服器</p></td>
</tr>
<tr class="odd">
<td><p><code>FederatedSharing</code></p></td>
<td><p><a href="federated-sharing-role-exchange-2013-help.md">同盟的共用的角色</a></p></td>
<td><p>此角色類型與讓系統管理員管理組織中跨樹系共用與跨組織共用的角色相關聯。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>InformationRightsManagement</code></p></td>
<td><p><a href="information-rights-management-role-exchange-2013-help.md">資訊版權管理角色</a></p></td>
<td><p>此角色類型與讓系統管理員管理組織中 Exchange 資訊版權管理 (IRM) 功能的角色相關聯。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>Journaling</code></p></td>
<td><p><a href="journaling-role-exchange-2013-help.md">日誌記錄角色</a></p></td>
<td><p>此角色類型與讓系統管理員管理組織中日誌設定的角色相關聯。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>LegalHold</code></p></td>
<td><p><a href="legal-hold-role-exchange-2013-help.md">法律保留角色</a></p></td>
<td><p>此角色類型與讓系統管理員設定信箱內的資料是否應保留，以供組織訴訟時使用的角色相關聯。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>MailboxImportExport</code></p></td>
<td><p><a href="mailbox-import-export-role-exchange-2013-help.md">信箱匯入匯出角色</a></p></td>
<td><p>此角色類型與可讓系統管理員匯入及匯出信箱內容，並清除信箱中不想要之內容的角色相關聯。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>MailboxSearch</code></p></td>
<td><p><a href="mailbox-search-role-exchange-2013-help.md">信箱搜尋角色</a></p></td>
<td><p>此角色類型與讓系統管理員在組織中搜尋一個或多個信箱之內容的角色相關聯。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>MailboxSearchApplication</code></p></td>
<td><p><a href="mailboxsearchapplication-role-exchange-2013-help.md">MailboxSearchApplication 角色</a></p></td>
<td><p>此角色類型與讓組織中夥伴應用程式設定和檢視信箱之合法持有狀態的角色相關聯。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>MailEnabledPublicFolders</code></p></td>
<td><p><a href="mail-enabled-public-folders-role-exchange-2013-help.md">擁有郵件功能的公用資料夾角色</a></p></td>
<td><p>此角色類型與讓系統管理員設定應啟用或停用組織中個別公用資料夾郵件功能的角色相關聯。</p>
<p>此角色類型僅能讓您管理公用資料夾的電子郵件內容。它無法讓您管理與電子郵件內容無關的公用資料夾內容。若要管理非電子郵件內容的公用資料夾內容，您必須被指派與 <code>PublicFolders</code> 角色類型相關聯的角色。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>MailRecipientCreation</code></p></td>
<td><p><a href="mail-recipient-creation-role-exchange-2013-help.md">郵件建立收件者角色</a></p>
<p></p></td>
<td><p>此角色類型與讓系統管理員在組織中建立信箱、郵件使用者、郵件連絡人、通訊群組與動態通訊群組的角色相關聯。與此角色類型相關聯的角色可以結合 <code>MailRecipients</code> 角色類型，以便建立和管理收件者。</p>
<p>此角色類型無法讓您啟用公用資料夾的郵件功能。若要啟用公用資料夾的郵件功能，您必須獲指派與 <code>MailEnabledPublicFolders</code> 角色類型相關聯的角色。</p>
<p>如果您的組織具有分割的權限模式，其中執行收件者建立的群組與執行收件者管理的群組不相同，請指派 <code>MailRecipientCreation</code> 角色給執行收件者建立的群組，並且指派 <code>MailRecipients</code> 角色給執行收件者管理的群組。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>MailRecipients</code></p></td>
<td><p><a href="mail-recipients-role-exchange-2013-help.md">郵件收件者角色</a></p></td>
<td><p>此角色類型與讓系統管理員管理組織中現有信箱、郵件使用者、郵件連絡人、通訊群組與動態通訊群組的角色相關聯。與此角色類型相關的角色不可建立這些收件者，但可以結合與 <code>MailRecipientCreation</code> 角色類型相關的角色來建立與管理收件者。</p>
<p>此角色類型不會讓您管理擁有郵件功能的公用資料夾或通訊群組。若要管理具備郵件功能的公用資料夾，您必須獲指派與 <code>MailEnabledPublicFolders</code> 角色類型相關聯的角色。若要管理通訊群組，您必須獲指派與 <code>DistributionGroups</code> 角色類型相關聯的角色。</p>
<p>如果您的組織具有分割的權限模式，其中執行收件者建立的群組與執行收件者管理的群組不相同，請指派 <code>MailRecipientCreation</code> 角色給執行收件者建立的群組，並且指派 <code>MailRecipients</code> 角色給執行收件者管理的群組。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>MailTips</code></p></td>
<td><p><a href="mail-tips-role-exchange-2013-help.md">郵件提示角色</a></p></td>
<td><p>此角色類型與可讓系統管理員管理組織中郵件提示的角色相關聯。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>MessageTracking</code></p></td>
<td><p><a href="message-tracking-role-exchange-2013-help.md">郵件追蹤角色</a></p></td>
<td><p>此角色類型與讓系統管理員追蹤組織中郵件的角色相關聯。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>Migration</code></p></td>
<td><p><a href="migration-role-exchange-2013-help.md">移轉角色</a></p></td>
<td><p>此角色類型與讓系統管理員將信箱和信箱內容移入或移出伺服器的角色相關聯。</p></td>
<td><p>伺服器</p></td>
</tr>
<tr class="even">
<td><p><code>Monitoring</code></p></td>
<td><p><a href="monitoring-role-exchange-2013-help.md">監視角色</a></p></td>
<td><p>此角色類型與讓系統管理員監控組織中 Microsoft Exchange 服務和元件可用性的角色相關聯。除了系統管理員以外，與此角色類型相關的角色還可搭配監控應用程式使用的服務帳戶，來收集 Exchange 伺服器狀態的相關資訊。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>MoveMailboxes</code></p></td>
<td><p><a href="move-mailboxes-role-exchange-2013-help.md">移動信箱角色</a></p></td>
<td><p>此角色類型與讓系統管理員在組織伺服器之間，以及在當地組織與其他組織伺服器之間移動信箱的角色相關聯。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>OfficeExtensionApplication</code></p></td>
<td><p><a href="officeextensionapplication-role-exchange-2013-help.md">OfficeExtensionApplication 角色</a></p></td>
<td><p>此角色類型與組織中讓 Microsoft Office 擴充應用程式存取使用者信箱的角色相關聯。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>OrgCustomApps</code></p></td>
<td><p><a href="org-custom-apps-role-exchange-2013-help.md">Org 自訂應用程式角色</a></p></td>
<td><p>此角色類型與組織中讓系統管理員檢視並修改組織中自訂應用程式的角色相關聯。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>OrgMarketplaceApps</code></p></td>
<td><p><a href="org-marketplace-apps-role-exchange-2013-help.md">Org 市集應用程式角色</a></p></td>
<td><p>此角色類型與組織中讓系統管理員檢視並修改組織中市集應用程式的角色相關聯。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>OrganizationClientAccess</code></p></td>
<td><p><a href="organization-client-access-role-exchange-2013-help.md">組織用戶端存取角色</a></p></td>
<td><p>此角色類型與系統管理員管理組織中「用戶端存取」伺服器設定的角色相關聯。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>OrganizationConfiguration</code></p></td>
<td><p><a href="organization-configuration-role-exchange-2013-help.md">組織設定角色</a></p></td>
<td><p>此角色類型與讓系統管理員管理整個組織設定的角色相關聯。此角色類型可控制的組織組態包括下列各項及更多：</p>
<ul>
<li><p>啟用或停用組織的郵件提示。</p></li>
<li><p>受管理資料夾首頁的 URL。</p></li>
<li><p>Microsoft Exchange 收件者 SMTP 位址和備用電子郵件地址。</p></li>
<li><p>資源信箱內容架構組態。</p></li>
<li><p>Exchange 系統管理中心和 Outlook Web App 的 [說明] URL。</p></li>
</ul>
<p>此角色類型不包括 <code>OrganizationClientAccess</code> 或 <code>OrganizationTransportSettings</code> 角色類型中包含的權限。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>OrganizationTransportSettings</code></p></td>
<td><p><a href="organization-transport-settings-role-exchange-2013-help.md">組織傳輸設定角色</a></p></td>
<td><p>此角色類型與讓系統管理員管理整個組織的傳輸設定 (例如系統訊息、Active Directory 站台設定以及其他整個組織的傳輸設定) 的角色相關聯。</p>
<p>此角色無法讓您建立或管理傳輸的接收連接器或傳送連接器、佇列、檢疫、代理程式、遠端和公認的網域，或是規則。若要建立或管理各項傳輸功能，您必須獲指派與以下角色類型相關聯的角色：</p>
<ul>
<li><p><strong>接收連接器</strong>   <code>ReceiveConnectors</code></p></li>
<li><p><strong>傳送連接器</strong>   <code>SendConnectors</code></p></li>
<li><p><strong>傳輸佇列</strong>   <code>TransportQueues</code></p></li>
<li><p><strong>傳輸檢疫</strong>   <code>TransportHygiene</code></p></li>
<li><p><strong>傳輸代理程式</strong>   <code>TransportAgents</code></p></li>
<li><p><strong>遠端和公認的網域</strong>   <code>RemoteAndAcceptedDomains</code></p></li>
<li><p><strong>傳輸規則</strong>   <code>TransportRules</code></p></li>
</ul></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>POP3AndIMAP4Protocols</code></p></td>
<td><p><a href="pop3-and-imap4-protocols-role-exchange-2013-help.md">POP3 與 IMAP4 通訊協定的角色</a></p></td>
<td><p>此角色類型與讓系統管理員管理個別伺服器上 POP3 和 IMAP4 組態 (例如驗證和連線設定) 的角色相關聯。</p></td>
<td><p>伺服器</p></td>
</tr>
<tr class="odd">
<td><p><code>PublicFolders</code></p></td>
<td><p><a href="public-folders-role-exchange-2013-help.md">公用資料夾角色</a></p></td>
<td><p>此角色類型與讓系統管理員管理組織中公用資料夾的角色相關聯。</p>
<p>此角色類型無法讓您管理是否啟用公用資料夾的郵件功能。若要啟用或停用公用資料夾的郵件功能，您必須獲指派與 <code>MailEnabledPublicFolders</code> 角色類型相關聯的角色。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>ReceiveConnectors</code></p></td>
<td><p><a href="receive-connectors-role-exchange-2013-help.md">接收連接器角色</a></p></td>
<td><p>此角色類型與可讓系統管理員管理個別伺服器上傳輸的 [接收] 連接器組態 (例如大小限制) 的角色相關聯。</p></td>
<td><p>伺服器</p></td>
</tr>
<tr class="odd">
<td><p><code>RecipientPolicies</code></p></td>
<td><p><a href="recipient-policies-role-exchange-2013-help.md">收件者原則角色</a></p></td>
<td><p>此角色類型與組織中讓系統管理員管理收件者原則 (例如佈建原則和行動裝置) 的角色相關聯。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>RemoteAndAcceptedDomains</code></p></td>
<td><p><a href="remote-and-accepted-domains-role-exchange-2013-help.md">遠端和公認的網域角色</a></p></td>
<td><p>此角色類型與讓系統管理員管理組織中遠端和公認的網域的角色相關聯。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>ResetPassword</code></p></td>
<td><p><a href="reset-password-role-exchange-2013-help.md">重設密碼角色</a></p></td>
<td><p>此角色類型與讓使用者重設其密碼，以及讓系統管理員重設組織內使用者密碼的角色相關聯。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>RetentionManagement</code></p></td>
<td><p><a href="retention-management-role-exchange-2013-help.md">保留管理角色</a></p></td>
<td><p>此角色類型與讓系統管理員管理組織中保留原則的角色相關聯。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>RoleManagement</code></p></td>
<td><p><a href="role-management-role-exchange-2013-help.md">角色管理角色</a></p></td>
<td><p>此角色類型與讓系統管理員管理組織中之管理角色群組、角色指派原則、管理角色、組織中的角色項目、指派以及範圍的角色相關聯。</p>
<p>獲指派此角色類型相關聯角色的使用者可覆寫 <strong>role group managed by</strong> 、設定任何角色群組，以及新增或移除任何角色群組的成員。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>SecurityGroupCreationAndMembership</code></p></td>
<td><p><a href="security-group-creation-and-membership-role-exchange-2013-help.md">安全群組建立與成員資格的角色</a></p></td>
<td><p>此角色類型與讓系統管理員建立與管理組織中萬用安全性群組及其成員資格的角色相關聯。</p>
<p>如果您的組織維持分割的權限模式，其中建立和管理 USG 的群組與管理 Exchange 伺服器的群組不相同，請指派與此角色類型相關聯的角色給該群組。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>SendConnectors</code></p></td>
<td><p><a href="send-connectors-role-exchange-2013-help.md">傳送連接器角色</a></p></td>
<td><p>此角色類型與讓系統管理員管理組織中傳輸 [傳送] 連接器的角色相關聯。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>SupportDiagnostics</code></p></td>
<td><p><a href="support-diagnostics-role-exchange-2013-help.md">支援診斷角色</a></p></td>
<td><p>此角色類型與讓系統管理員依據 Microsoft 支援服務的指示在組織中執行進階診斷的角色相關聯。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>與此角色類型相關聯的角色授與指令程式和指令碼權限應僅可依據 Microsoft 客戶服務及支援的指示來使用。</td>
</tr>
</tbody>
</table>

</td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>TeamMailboxes</code></p></td>
<td><p><a href="team-mailboxes-role-exchange-2013-help.md">小組信箱角色</a></p></td>
<td><p>此角色類型與組織中讓系統管理員定義一或多個站台信箱佈建原則和管理站台信箱的角色相關聯。指派與此角色類型相關聯之角色的系統管理員可以管理他們所沒有的站台信箱。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>TeamMailboxLifecycleApplication</code></p></td>
<td><p><a href="teammailboxlifecycleapplication-role-exchange-2013-help.md">TeamMailboxLifecycleApplication 角色</a></p></td>
<td><p>此角色類型與組織中讓夥伴應用程式更新網站信箱週期狀態的角色相關聯。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>TransportAgents</code></p></td>
<td><p><a href="transport-agents-role-exchange-2013-help.md">傳輸代理程式角色</a></p></td>
<td><p>此角色類型與讓系統管理員管理組織中傳輸代理程式的角色相關聯。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>TransportHygiene</code></p></td>
<td><p><a href="transport-hygiene-role-exchange-2013-help.md">傳輸檢疫角色</a></p></td>
<td><p>此角色類型與組織中讓系統管理員管理反垃圾和反惡意程式碼功能的角色相關聯。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>TransportQueues</code></p></td>
<td><p><a href="transport-queues-role-exchange-2013-help.md">傳輸佇列角色</a></p></td>
<td><p>此角色類型與讓系統管理員管理個別伺服器上傳輸佇列的角色相關聯。</p></td>
<td><p>伺服器</p></td>
</tr>
<tr class="even">
<td><p><code>TransportRules</code></p></td>
<td><p><a href="transport-rules-role-exchange-2013-help.md">傳輸規則角色</a></p></td>
<td><p>此角色類型與讓系統管理員管理組織中傳輸規則的角色相關聯。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>UMMailboxes</code></p></td>
<td><p><a href="um-mailboxes-role-exchange-2013-help.md">UM 信箱角色</a></p></td>
<td><p>此角色類型與讓系統管理員管理組織中信箱和其他收件者之整合通訊 (UM) 組態的角色相關聯。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>UMPrompts</code></p></td>
<td><p><a href="um-prompts-role-exchange-2013-help.md">UM 提示角色</a></p></td>
<td><p>此角色類型與讓系統管理員建立並管理組織中自訂 UM 語音提示的角色相關聯。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>UnifiedMessaging</code></p></td>
<td><p><a href="unified-messaging-role-exchange-2013-help.md">整合的通訊角色</a></p></td>
<td><p>此角色類型與讓系統管理員管理組織中整合通訊服務的角色相關聯。</p>
<p>此角色無法讓您管理 UM 專屬的信箱組態或 UM 提示。若要管理 UM 特有的信箱組態，請使用與 <code>UMMailboxes</code> 角色類型相關聯的角色。若要管理 UM 提示，請使用與 <code>UMPrompts</code> 角色類型相關聯的角色。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>UnScopedRoleManagement</code></p></td>
<td><p><a href="unscoped-role-management-role-exchange-2013-help.md">未限定範圍的角色管理角色</a></p></td>
<td><p>此角色類型與讓系統管理員建立並管理組織中未限定範圍之頂層管理角色的角色相關聯。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>UserOptions</code></p></td>
<td><p><a href="user-options-role-exchange-2013-help.md">使用者選項角色</a></p></td>
<td><p>此角色類型與讓系統管理員檢視組織中使用者之 Outlook Web App 選項的角色相關聯。與此角色類型相關聯的角色可用於協助使用者診斷與其組態相關的問題。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>UserApplication</code></p></td>
<td><p><a href="userapplication-role-exchange-2013-help.md">UserApplication 角色</a></p></td>
<td><p>此角色類型與讓組織中夥伴應用程式代表使用者身分的角色相關聯。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>ViewOnlyAuditLogs</code></p></td>
<td><p><a href="view-only-audit-logs-role-exchange-2013-help.md">僅檢視稽核記錄 」 角色</a></p></td>
<td><p>此角色類型與可讓系統管理員搜尋組織中系統管理員稽核記錄的角色相關聯。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>ViewOnlyConfiguration</code></p></td>
<td><p><a href="view-only-configuration-role-exchange-2013-help.md">僅檢視設定角色</a></p></td>
<td><p>此角色類型與讓系統管理員檢視組織中所有非收件者 Exchange 組態設定的角色相關聯。可檢視的組態範例包括伺服器組態、傳輸組態、資料庫組態，以及整個組織的組態。</p>
<p>與此角色類型相關聯的角色可以結合與 <code>ViewOnlyRecipients</code> 角色類型相關聯的角色，以建立能夠檢視組織內每一個物件的角色。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="odd">
<td><p><code>ViewOnlyRecipients</code></p></td>
<td><p><a href="view-only-recipients-role-exchange-2013-help.md">僅檢視收件者角色</a></p></td>
<td><p>此角色類型與讓系統管理員檢視收件者組態 (例如信箱，郵件使用者、郵件連絡人、通訊群組和動態通訊群組) 的角色相關聯。</p>
<p>與此角色類型相關聯的角色可以結合與 <code>ViewOnlyConfiguration</code> 角色類型相關聯的角色，以建立能夠檢視組織內每一個物件的角色。</p></td>
<td><p>組織</p></td>
</tr>
<tr class="even">
<td><p><code>WorkloadManagement</code></p></td>
<td><p><a href="workloadmanagement-role-exchange-2013-help.md">WorkloadManagement 角色</a></p></td>
<td><p>此角色類型與組織中讓系統管理員管理工作負載管理原則的角色相關聯。管理員可設定資源健康定義、工作量分類以及啟用或停用工作量管理。</p></td>
<td><p>組織</p></td>
</tr>
</tbody>
</table>


下表列出 Exchange 2013 中所有使用者為主的管理角色類型，以及其關聯的內建管理角色。

**使用者為主的角色類型**


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>管理角色類型</th>
<th>內建使用者為主角色</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>MyBaseOptions</code></p></td>
<td><p><a href="mybaseoptions-role-exchange-2013-help.md">MyBaseOptions 角色</a></p></td>
<td><p>此角色類型與讓個別使用者檢視和修改本身所擁有信箱之基本組態及相關設定的角色相關聯。</p></td>
</tr>
<tr class="even">
<td><p><code>MyContactInformation</code></p></td>
<td><p><a href="myaddressinformation-role-exchange-2013-help.md">MyAddressInformation 角色</a></p>
<p><a href="mycontactinformation-role-exchange-2013-help.md">MyContactInformation 角色</a></p>
<p><a href="mymobileinformation-role-exchange-2013-help.md">MyMobileInformation 角色</a></p>
<p><a href="mypersonalinformation-role-exchange-2013-help.md">MyPersonalInformation 角色</a></p></td>
<td><p>此角色類型與讓個別使用者修改其連絡人資訊的角色相關聯。這項資訊包括其地址和電話號碼。</p></td>
</tr>
<tr class="odd">
<td><p>MyCustomApps</p></td>
<td><p><a href="my-custom-apps-role-exchange-2013-help.md">我自訂應用程式的角色</a></p></td>
<td><p>此角色類型與讓個別使用者檢視和修改其自訂應用程式的角色相關聯。</p></td>
</tr>
<tr class="even">
<td><p>MyDiagnostics</p></td>
<td><p><a href="mydiagnostics-role-exchange-2013-help.md">MyDiagnostics 角色</a></p></td>
<td><p>此角色類型與可讓個別使用者在其信箱上執行基本診斷的角色相關聯，例如擷取行事曆診斷資訊。</p></td>
</tr>
<tr class="odd">
<td><p><code>MyDistributionGroupMembership</code></p></td>
<td><p><a href="mydistributiongroupmembership-role-exchange-2013-help.md">MyDistributionGroupMembership 角色</a></p></td>
<td><p>此角色類型與讓個別使用者檢視和修改本身在組織內通訊群組中的成員資格 (假設這些通訊群組允許操作群組成員資格) 的角色相關聯。</p></td>
</tr>
<tr class="even">
<td><p><code>MyDistributionGroups</code></p></td>
<td><p><a href="mydistributiongroups-role-exchange-2013-help.md">MyDistributionGroups 角色</a></p></td>
<td><p>此角色類型與讓個別使用者建立、修改及檢視通訊群組，以及修改、檢視、移除和新增成員至所擁有的通訊群組的角色相關聯。</p></td>
</tr>
<tr class="odd">
<td><p><code>MyProfileInformation</code></p></td>
<td><p><a href="mydisplayname-role-exchange-2013-help.md">MyDisplayName 角色</a></p>
<p><a href="myname-role-exchange-2013-help.md">為 MyName 角色</a></p>
<p><a href="myprofileinformation-role-exchange-2013-help.md">MyProfileInformation 角色</a></p></td>
<td><p>此角色類型與讓個別使用者修改其姓名的角色相關聯。</p></td>
</tr>
<tr class="even">
<td><p>MyMarketplaceApps</p></td>
<td><p><a href="my-marketplace-apps-role-exchange-2013-help.md">我市集應用程式的角色</a></p></td>
<td><p>此角色類型與讓個別使用者檢視和修改其市集應用程式的角色相關聯。</p></td>
</tr>
<tr class="odd">
<td><p><code>MyRetentionPolicies</code></p></td>
<td><p><a href="myretentionpolicies-role-exchange-2013-help.md">MyRetentionPolicies 角色</a></p></td>
<td><p>此角色類型與讓個別使用者檢視其保留標記，以及檢視與修改其保留標記設定和預設值的角色相關聯。</p></td>
</tr>
<tr class="even">
<td><p>MyTeamMailboxes</p></td>
<td><p><a href="myteammailboxes-role-exchange-2013-help.md">MyTeamMailboxes 角色</a></p></td>
<td><p>此角色類型與讓個別使用者建立站台信箱並將信箱連線 Microsoft SharePoint 站台的角色相關聯。</p></td>
</tr>
<tr class="odd">
<td><p><code>MyTextMessaging</code></p></td>
<td><p><a href="mytextmessaging-role-exchange-2013-help.md">MyTextMessaging 角色</a></p></td>
<td><p>此角色類型與讓個別使用者建立、檢視和修改其文字郵件設定的角色相關聯。</p></td>
</tr>
<tr class="even">
<td><p><code>MyVoiceMail</code></p></td>
<td><p><a href="myvoicemail-role-exchange-2013-help.md">MyVoiceMail 角色</a></p></td>
<td><p>此角色類型與讓個別使用者檢視和修改其語音郵件設定的角色相關聯。</p></td>
</tr>
</tbody>
</table>


回到頁首

## 相關資訊

[New-ManagementRole](https://technet.microsoft.com/zh-tw/library/dd298073\(v=exchg.150\))

[New-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd335193\(v=exchg.150\))

[Set-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd335173\(v=exchg.150\))

[New-ManagementScope](https://technet.microsoft.com/zh-tw/library/dd335137\(v=exchg.150\))

[Set-ManagementScope](https://technet.microsoft.com/zh-tw/library/dd297996\(v=exchg.150\))

[New-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd335193\(v=exchg.150\))

[Set-ManagementRoleAssignment](https://technet.microsoft.com/zh-tw/library/dd335173\(v=exchg.150\))

