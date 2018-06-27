---
title: '了解分割權限: Exchange 2013 Help'
TOCTitle: 了解分割權限
ms:assetid: 2b709e15-63a2-4841-94bc-b289b71166d0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd638106(v=EXCHG.150)
ms:contentKeyID: 50472885
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 了解分割權限

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-07_

個別管理 Microsoft Exchange Server 2013物件及Active Directory物件的組織會使用項目已呼叫*分割權限*模型。分割權限可以讓組織對組織內的特定群組指派特定權限和相關的工作。此區分工作協助維護標準與工作流程，並協助控制變更組織中。

最高的分割權限層級是Exchange管理和Active Directory管理的區隔。許多組織有兩個群組： 管理組織的Exchange基礎結構，包括伺服器與收件者的管理員與管理Active Directory基礎結構的管理員。這是許多組織的重要分離因為Active Directory基礎結構通常跨越多位置、 網域、 服務、 應用程式以及即使Active Directory樹系。Active Directory系統管理員必須確定Active Directory所做的變更不造成負面影響任何其他服務。因此，通常只有一小群管理員允許來管理該基礎結構。

同時， Exchange，包括伺服器與收件者\] 的基礎結構可以也會很複雜且需要專業的知識。此外， Exchange儲存之組織的業務的極機密資訊。Exchange管理員可能可以存取此資訊。限制Exchange管理員數目、 組織限制誰可以對Exchange組態中的變更及可存取敏感資訊的人員。

分割權限通常會進行建立Active Directory，例如使用者和安全性群組，以及這些物件的後續組態中的安全性主體之間的差別。這有助於減少未經授權存取的網路控制誰可以建立授與存取權給它的物件。大部分通常只Active Directory系統管理員可以建立同時其他管理員，例如Exchange系統管理員的安全性主體，可以管理現有的Active Directory物件的特定屬性。

若要支援的不同需求來分隔Exchange及Active Directory的管理， Exchange 2013可讓您選擇是否要共用的權限模型或分割權限模式。Exchange 2013提供兩種類型的分割權限模型： RBAC 和Active Directory。Exchange 2013預設值為共用權限模型。

**目錄**

說明角色型存取控制及 Active Directory

共用權限

分割權限

RBAC 分割權限

Active Directory 分割權限

## 說明角色型存取控制及 Active Directory


若要了解分割權限，您需要了解角色型存取控制 (RBAC) 權限模型中的全部Exchange 2013與Active Directory的運作方式。RBAC 模型控制項誰可以執行的動作，以及哪些物件上都執行這些動作。如本主題中所討論的 RBAC 的各項元件的相關詳細資訊，請參閱[了解角色型存取控制](understanding-role-based-access-control-exchange-2013-help.md)。

在Exchange 2013、 Exchange物件所執行的所有工作必須都透過Exchange管理命令介面或Exchange系統管理中心 (EAC) 介面。這兩種管理工具使用 RBAC 以授權所執行的所有工作。

RBAC 是存在於執行Exchange 2013每台伺服器的元件。RBAC 會檢查是否要執行這項操作授權使用者執行的動作：

  - 如果使用者不已授權可執行的動作，RBAC 不允許進行的動作。

  - 如果使用者有權執行動作，RBAC 會檢查使用者是否有權執行對所要求的特定物件的動作：
    
      - 如果使用者已獲得授權，RBAC 允許要繼續執行的動作。
    
      - 如果未授權使用者，RBAC 不允許進行的動作。

如果 RBAC 允許繼續進行的動作，是Exchange受信任子系統的內容而不是使用者的內容中執行的動作。Exchange受信任子系統是高權萬用安全性群組 (USG) 可讀取/寫入存取每個Exchange- Exchange組織中的相關的物件。它也是系統管理員本機安全性群組與Exchange Windows 權限 USG，可讓Exchange來建立及管理Active Directory物件的成員。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>未變更任何手動對Exchange受信任子系統安全性群組的成員資格。此外，不將它新增或移除物件的存取控制清單 (Acl)。變更Exchange受信任子系統 USG 自行，您就會造成造成無法挽回的損害Exchange組織。</td>
</tr>
</tbody>
</table>


請務必了解並不重要Active Directory權限的使用者具有時使用Exchange管理工具。若授權使用者，透過 RBAC，若要執行巨集指令中Exchange管理工具\] 中上的使用者可以執行不論其Active Directory權限的巨集指令。相反地，如果使用者是企業系統管理員在Active Directory中但不已授權可執行的動作，例如Exchange中管理工具\] 建立信箱，巨集指令會將不會成功因為使用者沒有根據 RBAC 的必要權限。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>雖然的 RBAC 權限模型不會套用至Active Directory使用者和電腦管理工具， Active Directory使用者及電腦無法管理Exchange組態。所以雖然使用者可能會有修改Active Directory物件，例如使用者的顯示名稱的某些屬性存取使用者必須使用Exchange管理工具] 中，與因此必須授權 RBAC，來管理Exchange屬性。</td>
</tr>
</tbody>
</table>


回到頁首

## 共用權限

共用權限模型的功能Exchange 2013預設模型。您不需要變更的任何項目如果這是您想要使用的權限模型。此模型不會分隔Exchange和Active Directory物件從Exchange管理工具中的管理。它可讓系統管理員使用Exchange管理工具在Active Directory中建立安全性主體。

下表顯示啟用的安全性主體Exchange和它們指定給預設管理角色群組中建立的角色。

### 安全性主體管理角色

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>管理角色</th>
<th>角色群組</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="mail-recipient-creation-role-exchange-2013-help.md">郵件建立收件者角色</a></p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p></td>
</tr>
<tr class="even">
<td><p><a href="security-group-creation-and-membership-role-exchange-2013-help.md">安全群組建立與成員資格的角色</a></p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p></td>
</tr>
</tbody>
</table>


角色群組、 使用者或 Usg 指派 「 建立郵件收件者 」 角色可以建立例如Active Directory使用者的安全性主體。依預設， 組織管理和收件者管理角色群組是指派給此角色。因此這些角色群組的成員可以建立安全性主體。

角色群組、 使用者或 Usg 指派安全性群組建立與成員資格角色可以建立安全性群組或管理其成員資格。根據預設，只有組織管理角色群組指定給此角色。因此只有組織管理角色群組的成員可以建立及管理安全性群組的成員資格。

您可以建立郵件收件者角色與安全性群組建立與成員資格角色至其他角色群組、 使用者或 Usg 如果您想指派其他使用者可以建立安全性主體。

若要啟用現有的安全性主體Exchange 2013中管理、 郵件收件者角色指派給組織管理和收件者管理角色群組預設。角色群組、 使用者或 Usg 指派 「 郵件收件者 」 角色可以管理現有的安全性主體。如果您想要能夠管理現有的安全性主體其他角色群組、 使用者或 Usg，您必須指派 「 郵件收件者 」 角色給他們。

如需如何將角色新增至角色群組、 使用者或 Usg 的詳細資訊，請參閱下列主題：

  - [管理角色群組](manage-role-groups-exchange-2013-help.md)

  - [將角色新增至使用者或 USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

如果您切換到分割權限模式並想要變更回共用權限模型，請參閱[如需共用權限設定 Exchange 2013](configure-exchange-2013-for-shared-permissions-exchange-2013-help.md)。

回到頁首

## 分割權限

如果貴組織所分隔Exchange管理和Active Directory管理，您需要設定Exchange支援分割權限模式。當設定正確，只想要建立的安全性主體，例如Active Directory管理員、 管理員將能夠達成和只有Exchange系統管理員可以修改現有的安全性主體的Exchange屬性。此分割權限也都屬於大致上沿著Active Directory中的網域和組態分割區的線條。分割區也稱為命名內容。網域磁碟分割可儲存使用者、 群組及其他物件的特定網域。組態磁碟分割可儲存使用Active Directory，例如Exchange服務的整個樹系的組態資訊。雖然物件可能包含Exchange網域分割區中儲存的資料通常由Active Directory管理員所管理- Exchange管理員可以管理的特定屬性。將資料儲存在此分割區中每個個別服務的系統管理員管理儲存在組態分割資料。Exchange，這是一般Exchange系統管理員。

Exchange 2013支援兩種下列類型的分割權限：

  - **RBAC 分割權限**  Active Directory網域分割區中建立安全性主體的權限是由 RBAC 控制。僅限Exchange伺服器、 服務及適當的角色群組之成員的使用者可以建立安全性主體。

  - **Active Directory 分割權限**  從任何Exchange使用者、 服務或伺服器完全移除Active Directory網域分割區中建立安全性主體的權限。建立安全性主體的 RBAC 不提供的任何選項。使用Active Directory管理工具必須執行Active Directory中的安全性主體的建立。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>雖然Active Directory分割權限可啟用或停用電腦已安裝的Exchange 2013Active Directory分割權限組態會套用至Exchange 2013和Exchange 2010伺服器上執行安裝程式。它，但沒有任何影響 Microsoft Exchange Server 2007伺服器上。</td>
    </tr>
    </tbody>
    </table>


如果您的組織選擇使用分割權限模式，而不是共用的權限，我們建議您使用的 RBAC 分割權限模型。RBAC 分割權限模型會提供大幅更大的彈性同時提供幾乎相同管理分離為Active Directory分割權限、 例外狀況的Exchange伺服器和服務可以 RBAC 分割權限模式中建立安全性主體。

您正在詢問您是否要啟用Active Directory在安裝期間分割權限。如果您選擇啟用Active Directory分割權限，您只能變更至共用的權限或 RBAC 分割來重新執行安裝程式的權限並停用Active Directory分割權限。此選項會套用至組織中的所有Exchange 2010和Exchange 2013伺服器。

下列各節說明 RBAC 和Active Directory分割權限的詳細資訊。

回到頁首

## RBAC 分割權限

RBAC 的安全性模型修改分隔誰可以管理Exchange組織中的資料Active Directory組態磁碟分割的使用者可以從Active Directory網域分割區中建立安全性主體的預設管理角色指派。安全性主體，例如與信箱和通訊群組的使用者可以建立由系統管理員建立郵件收件者和安全性群組建立與成員資格角色的成員。這些權限保持分開建立Exchange外部安全性主體管理工具所需的權限。未指派的建立郵件收件者或安全性群組建立與成員資格角色Exchange系統管理員仍可修改Exchange-相關安全性主體的屬性。Active Directory系統管理員也可以使用Exchange管理工具來建立Active Directory安全性主體的選項。

Exchange伺服器和Exchange受信任子系統也有Active Directory中建立安全性主體代表使用者和整合 RBAC 的協力廠商程式的權限。

RBAC 分割權限，則您的組織很好的選擇下屬實：

  - 您的組織不需要建立安全性主體是執行使用Active Directory管理工具，以及只對其指派特定Active Directory權限的使用者。

  - 貴組織可讓服務，例如Exchange伺服器，以建立安全性主體。

  - 您想要簡化允許從其建立內Exchange管理工具中建立信箱、 擁有郵件功能的使用者、 通訊群組和角色群組所需的程序。

  - 您想要管理通訊群組和Exchange管理工具中的角色群組的成員資格。

  - 您必須與協力廠商程式需要Exchange伺服器要能夠在其代理上建立安全性主體。

如果貴組織需要Exchange與Active Directory管理完整區分對於使用Exchange管理工具可以不執行任何Active Directory管理或Exchange服務，請參閱本主題稍後的 \[ Active Directory 分割權限\] 區段。

從共用的權限切換到 RBAC 分割權限是您用來移除建立安全性主體授與它們預設角色群組所需的權限手動程序。下表顯示啟用的安全性主體Exchange和它們指定給預設管理角色群組中建立的角色。

### 安全性主體管理角色

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>管理角色</th>
<th>角色群組</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="mail-recipient-creation-role-exchange-2013-help.md">郵件建立收件者角色</a></p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件者管理</a></p></td>
</tr>
<tr class="even">
<td><p><a href="security-group-creation-and-membership-role-exchange-2013-help.md">安全群組建立與成員資格的角色</a></p></td>
<td><p><a href="organization-management-exchange-2013-help.md">組織管理</a></p></td>
</tr>
</tbody>
</table>


根據預設， 組織管理和收件者管理角色群組的成員可以建立安全性主體。您必須將建立從內建角色群組的安全性主體至您建立新角色群組的功能。

若要設定 RBAC 分割權限，您必須執行下列動作：

1.  如果已啟用停用Active Directory分割權限。

2.  建立角色群組，其會包含將能夠建立安全性主體Active Directory系統管理員。

3.  建立 「 建立郵件收件者 」 角色與新角色群組之間的一般和委派角色指派。

4.  建立安全性群組建立與成員資格角色與新角色群組之間的一般和委派角色指派。

5.  移除一般和委派 「 建立郵件收件者 」 角色和組織管理和收件者管理角色群組之間的管理角色指派。

6.  移除一般和委派的安全性群組建立與成員資格的角色與組織管理角色群組之間的角色指派。

執行此動作後只有您建立新角色群組的成員能建立的安全性主體，例如信箱。新的群組只可以建立的物件。將無法在新的物件上設定Exchange屬性。Active Directory系統管理員，為新群組的成員，會需要建立物件，然後Exchange管理員必須在物件上設定Exchange屬性。Exchange系統管理員將無法使用下列 cmdlet：

  - **New-Mailbox**

  - **New-MailContact**

  - **New-MailUser**

  - **New-RemoteMailbox**

  - **Remove-Mailbox**

  - **Remove-MailContact**

  - **Remove-MailUser**

  - **Remove-RemoteMailbox**

Exchange系統管理員將，但是能夠建立及管理Exchange-特定物件，例如傳輸規則、 通訊群組、 等等並管理Exchange-相關的任何物件的屬性。

此外，EAC 和Outlook Web App，例如新的信箱精靈\] 中的相關的功能也不再可或如果您嘗試使用這些會產生錯誤。

如果您想要也能夠管理的新物件的Exchange屬性新的角色群組、 郵件收件者角色也必須指派給新角色群組。

如需設定分割權限模式的詳細資訊，請參閱[設定 Exchange 2013 分割權限](configure-exchange-2013-for-split-permissions-exchange-2013-help.md)。

回到頁首

## Active Directory 分割權限

Active Directory分割權限，以建立Active Directory網域磁碟分割，例如信箱及通訊群組中的安全性主體必須執行使用Active Directory管理工具。授與權限Exchange受信任的子系統及Exchange伺服器來限制Exchange系統管理員和伺服器可以執行的動作來進行數項變更。功能的下列變更發生當您啟用Active Directory分割權限：

  - 建立信箱、 擁有郵件功能的使用者、 通訊群組及其他安全性主體已從Exchange管理工具。

  - 無法從Exchange管理工具完成新增和移除通訊群組成員。

  - 會移除所有建立的權限授與給Exchange受信任的子系統及Exchange伺服器安全性主體。

  - Exchange伺服器和Exchange管理工具只能修改現有的安全性主體中Active DirectoryExchange屬性。

例如，建立信箱與Active Directory啟用分割權限，使用者必須先建立使用Active Directory工具所具有的必要的Active Directory權限的使用者。然後，使用者可以擁有信箱功能使用Exchange管理工具。僅限Exchange-相關Exchange使用Exchange管理工具的系統管理員可以修改信箱的屬性。

Active Directory分割權限，則您的組織很好的選擇下屬實：

  - 貴組織需要安全性主體是建立使用僅限Active Directory管理工具或僅由會授與Active Directory特定的權限的使用者。

  - 您想要完全分開管理Exchange組織的使用者可以從建立安全性主體的功能。

  - 您想要執行所有通訊群組管理，包括建立通訊群組並新增和移除使用Active Directory管理工具的這些群組的成員。

  - 您不想Exchange伺服器或使用Exchange其代理，建立安全性主體的協力廠商程式\]。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>切換到Active Directory分割權限是當您安裝Exchange 2013使用安裝程式精靈] 或從命令列執行<code>setup.exe</code>時發生使用<em>ActiveDirectorySplitPermissions</em>參數來進行選擇。您也可以啟用或停用Active Directory後重新執行<code>setup.exe</code>從命令列安裝Exchange 2013分割權限。若要啟用Active Directory分割權限，請將<em>ActiveDirectorySplitPermissions</em>參數設<code>true</code>。若要停用它，請將它設為<code>false</code>。您必須一律指定<em>PrepareAD</em>參數搭配<em>ActiveDirectorySplitPermissions</em>參數。<br />
如果您在同一個樹系內有多個網域，您必須也其中一個指定<em>PrepareAllDomains</em>切換時套用Active Directory分割權限或搭配<em>PrepareDomain</em>參數在每個網域中執行安裝程式。如果您選擇使用<em>PrepareDomain</em>交換器每個網域中執行安裝程式而不是使用<em>PrepareAllDomains</em>參數，您必須先準備包含Exchange伺服器、 啟用郵件功能的物件或無法存取Exchange伺服器的通用類別目錄伺服器的每個網域。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您無法啟用Active Directory如果您已在網域控制站上安裝Exchange 2010或Exchange 2013分割權限。<br />
啟用或停用Active Directory分割權限後，我們建議您在組織來強制其挑選與更新的權限的新Active Directory存取權杖中重新啟動Exchange 2010和Exchange 2013伺服器。</td>
</tr>
</tbody>
</table>


Exchange 2013透過ExchangeWindows權限安全性\] 群組中移除的權限和成員資格達到達成Active Directory分割權限。此安全性\] 群組中共用的權限與 RBAC 分割權限\] 權限授許多非Exchange物件和整個Active Directory中的屬性。移除的權限及此安全性群組的成員資格、 Exchange管理員及服務會禁止建立或修改這些非ExchangeActive Directory物件。

如需變更時，發生ExchangeWindows權限安全性群組及其他Exchange元件啟用或停用Active Directory分割權限的清單，請參閱下表。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>啟用Active Directory分割權限時移除角色指派給角色群組可讓Exchange系統管理員建立安全性主體。這是要移除的存取權時他們正在執行，因為沒有建立關聯的Active Directory物件的權限否則會產生錯誤的 cmdlet。</td>
</tr>
</tbody>
</table>


### Active Directory 分割權限變更

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Action</th>
<th>Exchange 所做的變更</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>啟用Active Directory分割第一個Exchange 2013 server 安裝期間的權限</p></td>
<td><p>會發生下列情況時啟用Active Directory分割透過安裝精靈或透過執行<code>setup.exe</code><code>/PrepareAD</code>和<code>/ActiveDirectorySplitPermissions:true</code>參數的權限：</p>
<ul>
<li><p>建立稱為 「 <strong>Microsoft Exchange 受保護群組</strong>組織單位 (OU)。</p></li>
<li><p><strong>Exchange Windows 權限</strong>的 [安全性] 群組會建立<strong>Microsoft Exchange 受保護群組</strong>OU。</p></li>
<li><p><strong>Exchange 受信任子系統</strong>的 [安全性] 群組無法新增至<strong>Exchange Windows 權限</strong>的 [安全性] 群組中。</p></li>
<li><p>建立非委派管理角色指派管理角色具有下列管理角色類型會略過：</p>
<ul>
<li><p><code>MailRecipientCreation</code></p></li>
<li><p><code>SecurityGroupCreationandMembership</code></p></li>
</ul></li>
<li><p>存取控制項目 (Ace) 會指派給<strong>Exchange Windows 權限</strong>的 [安全性] 群組未新增至Active Directory網域物件。</p></li>
</ul>
<p>如果您執行安裝程式與<em>PrepareAllDomains</em>或<em>PrepareDomain</em>參數時，會發生下列情況中每個已備妥的子網域：</p>
<ul>
<li><p>指派給<strong>Exchange Windows 權限</strong>的 [安全性] 群組的所有 Ace 都移除的網域物件。</p></li>
<li><p>除了任何指派給<strong>Exchange Windows 權限</strong>的 [安全性] 群組的 Ace 每個網域中設定的 Ace。</p></li>
</ul>
<p></p></td>
</tr>
<tr class="even">
<td><p>從共用的權限或分割Active Directory分割權限的權限的 RBAC 切換</p></td>
<td><p>會發生下列情況時您<code>/PrepareAD</code>和<code>/ActiveDirectorySplitPermissions:true</code>參數執行<code>setup.exe</code>命令：</p>
<ul>
<li><p>建立稱為 「 <strong>Microsoft Exchange 受保護群組</strong>OU。</p></li>
<li><p><strong>Exchange Windows 權限</strong>的 [安全性] 群組會移至 [<strong>受保護的 Microsoft Exchange</strong> OU。</p></li>
<li><p><strong>Exchange 受信任子系統</strong>安全性群組已從<strong>Exchange Windows 權限</strong>的安全性] 群組中移除。</p></li>
<li><p>會移除任何非委派角色指派管理角色具有下列角色類型：</p>
<ul>
<li><p><code>MailRecipientCreation</code></p></li>
<li><p><code>SecurityGroupCreationandMembership</code></p></li>
</ul></li>
<li><p>指派給<strong>Exchange Windows 權限</strong>的 [安全性] 群組的所有 Ace 都移除的網域物件。</p></li>
</ul>
<p>如果您執行安裝程式與<em>PrepareAllDomains</em>或<em>PrepareDomain</em>參數，會發生下列情況中每個已備妥的子網域：</p>
<ul>
<li><p>指派給<strong>Exchange Windows 權限</strong>的 [安全性] 群組的所有 Ace 都移除的網域物件。</p></li>
<li><p>除了任何指派給<strong>Exchange Windows 權限</strong>的 [安全性] 群組的 Ace 每個網域中設定的 Ace。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>切換從Active Directory分割共用權限或 RBAC 分割權限的權限</p></td>
<td><p>會發生下列情況時您<code>/PrepareAD</code>和<code>/ActiveDirectorySplitPermissions:false</code>參數執行<code>setup.exe</code>命令：</p>
<ul>
<li><p><strong>Exchange Windows 權限</strong>的 [安全性] 群組會移至<strong>Microsoft Exchange 安全性群組</strong>OU。</p></li>
<li><p>已移除<strong>Microsoft Exchange 受保護的</strong>OU。</p></li>
<li><p><strong>Exchange 受信任子系統</strong>的 [安全性] 群組新增至<strong>Exchange Windows 權限</strong>的 [安全性] 群組。</p></li>
<li><p>Ace 會新增至<strong>Exchange Windows 權限</strong>的 [安全性] 群組的網域物件。</p></li>
</ul>
<p>如果您執行安裝程式與<em>PrepareAllDomains</em>或<em>PrepareDomain</em>參數，會發生下列情況中每個已備妥的子網域：</p>
<ul>
<li><p>Ace 會新增至<strong>Exchange Windows 權限</strong>的 [安全性] 群組的網域物件。</p></li>
<li><p>Ace 都設定在每個網域包括指派給<strong>Exchange Windows 權限</strong>的 [安全性] 群組的 Ace。</p></li>
</ul>
<p>建立郵件收件者安全性群組建立和成員資格角色的角色指派未自動建立時從Active Directory切換 split 共用權限。如果委派角色指派自訂前Active Directory分割要啟用的權限，這些自訂項目會保留不變。若要建立這些角色與組織管理角色群組之間的角色指派，請參閱<a href="configure-exchange-2013-for-shared-permissions-exchange-2013-help.md">如需共用權限設定 Exchange 2013</a>。</p></td>
</tr>
</tbody>
</table>


啟用Active Directory分割權限後，已不再提供下列 cmdlet：

  - **New-Mailbox**

  - **New-MailContact**

  - **New-MailUser**

  - **New-RemoteMailbox**

  - **Remove-Mailbox**

  - **Remove-MailContact**

  - **Remove-MailUser**

  - **Remove-RemoteMailbox**

啟用Active Directory之後分割權限、 現已可存取下列 cmdlet，但您無法使用他們建立通訊群組或修改通訊群組成員資格：

  - **Add-DistributionGroupMember**

  - **New-DistributionGroup**

  - **Remove-DistributionGroup**

  - **Remove-DistributionGroupMember**

  - **Update-DistributionGroupMember**

某些指令程式，但仍然可以使用可能會提供僅限於的功能Active Directory分割權限搭配使用時。這是因為它們可能會讓您設定收件者位於網域Active Directory分割區和Exchange組態Active Directory分割區中的組態物件的物件。他們也可能會讓您設定Exchange-相關的網域分割中儲存的物件的屬性。嘗試使用 cmdlet 來建立物件，或修改非Exchange-相關網域分割中的物件的屬性將會產生錯誤。例如，如果您嘗試將權限新增到信箱**Add-ADPermission**指令程式會傳回錯誤。不過，如果您在接收連接器上設定權限會成功**Add-ADPermission**指令程式。這是因為信箱儲存在網域磁碟分割時接收連接器會儲存在組態磁碟分割。

此外， Exchange系統管理中心中相關聯的功能和Outlook Web App，例如 \[新的信箱精靈\] 將也不再提供或如果您嘗試使用這些會產生錯誤。

Exchange系統管理員將，但是能夠建立及管理Exchange-特定物件，例如傳輸規則，依此類推。

如需關於設定Active Directory分割權限模式，請參閱[設定 Exchange 2013 分割權限](configure-exchange-2013-for-split-permissions-exchange-2013-help.md)。

回到頁首

