---
title: '了解 Exchange 2007 與 Exchange 2010 的權限共存: Exchange 2013 Help'
TOCTitle: 了解 Exchange 2007 與 Exchange 2010 的權限共存
ms:assetid: 28ab1433-23ee-4914-8f21-9a32578792e5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd335157(v=EXCHG.150)
ms:contentKeyID: 54914975
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 了解 Exchange 2007 與 Exchange 2010 的權限共存

 

_**適用版本：**Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013_

_**上次修改主題的時間：**2015-04-07_

當您安裝 Microsoft Exchange Server 2013到現有的 Microsoft Exchange Server 2010或 Microsoft Exchange Server 2007組織時，您需要了解權限的新組織中的運作方式。閱讀下節的適用於您的組織。

  - Installing Exchange 2013 into an existing Exchange 2010 organization

  - Installing Exchange 2013 into an existing Exchange 2007 organization

## 將 Exchange 2013 安裝至現有的 Exchange 2010 組織

Exchange 2013使用Exchange 2010中所使用的相同角色型存取控制 (RBAC) 權限模型。當您安裝Exchange 2013到現有的Exchange 2010組織時，相同的管理角色群組、 管理角色及管理範圍適用於Exchange 2013和Exchange 2010伺服器和收件者。角色群組或使用者指派給角色的成員可以管理任何Exchange 2013或Exchange 2013伺服器或角色群組或角色的範圍中包含的收件者。如果您未在組織中使用範圍與您想要管理 Exchange 2010 和 Exchange 2013 伺服器與收件者您現有的角色群組的成員，您不需要執行任何動作。系統管理員可以管理 Exchange 2013 伺服器與新增至組織的收件者。如果您需要的權限的運作方式在 Exchange 2010 與 Exchange 2013 上的提醒，請參閱[權限](permissions-exchange-2013-help.md)。

在新的組織可能會想要隔開的 Exchange 2010 和 Exchange 2013 伺服器與收件者管理。系統管理員負責管理 Exchange 2010 伺服器與收件者可能不會允許管理 Exchange 2013 伺服器與收件者\] 群組，反之亦然。在此例中，您可用於管理範圍定義應允許每個系統管理員群組管理的伺服器和收件者。建立您所需要的範圍之後，您可以再複製現有的角色群組新增管理員應該是每個、 成員及再將範圍新增至這些角色群組。當您完成時，每個角色群組的成員將只能夠管理伺服器與符合其各自的範圍的收件者。

如需角色群組、範圍、複製角色群組以及新增範圍至角色群組的相關資訊，請參閱下列主題：

  - [管理角色群組](manage-role-groups-exchange-2013-help.md)

  - [建立規則或獨佔範圍](create-a-regular-or-exclusive-scope-exchange-2013-help.md)

  - [了解管理角色群組](understanding-management-role-groups-exchange-2013-help.md)

  - [了解管理角色範圍](understanding-management-role-scopes-exchange-2013-help.md)

## 將 Exchange 2013 安裝至現有的 Exchange 2007 組織

Exchange 2013包含取代Active Directory存取控制項目 (ACE) 的角色型存取控制 (RBAC) 權限-用於 Microsoft Exchange Server 2007根據的授權模型。RBAC 是 Exchange 2013 的用於大部分管理的驗證機制。此機制包含下列的管理領域：

  - Exchange 管理命令介面

  - Exchange 系統管理中心 (EAC)

  - Exchange Web 服務

如需如何規劃 Exchange 2013 與 Exchange 2007 之間之共存的相關資訊，請參閱[從 Exchange 2007 升級至 Exchange 2013](upgrade-from-exchange-2007-to-exchange-2013-exchange-2013-help.md)。

要尋找相關的權限的管理工作嗎？取出[權限](permissions-exchange-2013-help.md)。

## Exchange 2013 權限

Exchange 2013 RBAC 權限模型包含其中一個數個管理角色指派的管理角色群組。管理角色包含的權限可讓系統管理員Exchange組織中執行的工作。系統管理員新增為角色群組的成員，且會授與角色提供的所有權限。下表提供角色群組、 角色指派給角色群組和使用者可能會擔任的角色群組成員的類型描述的一些的範例。

### Exchange 2013 中之角色群組與角色的範例

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>管理角色群組</th>
<th>管理角色</th>
<th>這個角色群組的成員</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>組織管理</p></td>
<td><p>下列角色是指派給這個角色群組的一些角色：</p>
<ul>
<li><p>通訊清單</p></li>
<li><p>Exchange Server</p></li>
<li><p>日誌</p></li>
<li><p>郵件收件者</p></li>
<li><p>公用資料夾</p></li>
</ul></td>
<td><p>管理整個Exchange 2013組織的使用者應此角色群組的成員。某些例外，此角色群組的成員可以管理Exchange 2013組織幾乎任何的層面。</p>
<p>根據預設，用於為 Active Directory 準備 Exchange 2013 的使用者帳戶是這個角色群組的成員。</p>
<p>如需這個角色群組的詳細資訊，以及指派至這個角色群組之角色的完整清單，請參閱<a href="organization-management-exchange-2013-help.md">組織管理</a>。</p></td>
</tr>
<tr class="even">
<td><p>僅限檢視組織管理</p></td>
<td><p>下列角色是指派給這個角色群組的角色：</p>
<ul>
<li><p>監視</p></li>
<li><p>僅限檢視組態</p></li>
<li><p>僅限檢視收件者</p></li>
</ul></td>
<td><p>使用者檢視整個Exchange 2013組織的組態應此角色群組的成員。這些使用者必須能夠檢視伺服器組態和收件者的資訊，並執行的功能變更的組織] 或 [收件者的設定而監控功能。</p>
<p>如需這個角色群組的詳細資訊，請參閱<a href="view-only-organization-management-exchange-2013-help.md">僅限檢視組織管理</a>。</p></td>
</tr>
<tr class="odd">
<td><p>收件者管理</p></td>
<td><p>下列角色是指派給這個角色群組的角色：</p>
<ul>
<li><p>通訊群組</p></li>
<li><p>啟用郵件的公用資料夾</p></li>
<li><p>建立郵件收件者</p></li>
<li><p>郵件收件者</p></li>
<li><p>郵件追蹤</p></li>
<li><p>遷移</p></li>
<li><p>移動信箱</p></li>
<li><p>收件者原則</p></li>
</ul></td>
<td><p>管理收件者例如信箱、 連絡人和通訊群組Exchange 2013組織中的使用者應此角色群組的成員。這些使用者可以建立收件者、 修改或刪除現有的收件者] 或移出信箱。</p>
<p>如需這個角色群組的詳細資訊，以及指派至這個角色群組之角色的完整清單，請參閱<a href="recipient-management-exchange-2013-help.md">收件者管理</a>。</p></td>
</tr>
<tr class="even">
<td><p>伺服器管理</p></td>
<td><p>下列角色是指派給這個角色群組的一些角色：</p>
<ul>
<li><p>資料庫</p></li>
<li><p>Exchange 連接器</p></li>
<li><p>Exchange Server</p></li>
<li><p>接收連接器</p></li>
<li><p>傳輸佇列</p></li>
</ul></td>
<td><p>管理等接收連接器、 憑證、 資料庫及虛擬目錄的Exchange伺服器組態的使用者應此角色群組的成員。這些使用者可以修改Exchange伺服器設定、 建立資料庫，並重新啟動及操作傳輸佇列。</p>
<p>如需這個角色群組的詳細資訊，以及指派至這個角色群組之角色的完整清單，請參閱<a href="server-management-exchange-2013-help.md">伺服器管理</a>。</p></td>
</tr>
<tr class="odd">
<td><p>探索管理</p></td>
<td><p>下列角色是指派給這個角色群組的角色：</p>
<ul>
<li><p>合法持有</p></li>
<li><p>信箱搜尋</p></li>
</ul></td>
<td><p>執行信箱搜尋以支援法律訴訟或設定合法持有的使用者必須是這個角色群組的成員。</p>
<p>這是可能會包含非Exchange系統管理員，例如法務部門中的人員在角色群組的範例。法務人員可以從Exchange管理員執行介入其工作。</p>
<p>如需這個角色群組的詳細資訊，以及指派至這個角色群組之角色的完整清單，請參閱<a href="discovery-management-exchange-2013-help.md">探索管理</a>。</p></td>
</tr>
</tbody>
</table>


下表顯示該Exchange 2013提供您授與系統管理員的權限控制細微層級。您可以選擇在Exchange 201312 角色群組。如需角色群組和其所提供的權限的完整清單，請參閱[內建角色群組](built-in-role-groups-exchange-2013-help.md)。

因為Exchange 2013提供許多角色群組和進一步自訂項目可能藉由建立具有不同的角色組合的角色群組，因為操作的存取控制清單 (Acl) 的Active Directory物件上不再需要且沒有作用。Acl 不再可用來將權限套用至個別的系統管理員或Exchange 2013中的群組。由 RBAC 管理所有工作\]，例如系統管理員建立信箱或使用者存取信箱。RBAC 授權任務，並再Exchange執行即代表使用者如果允許的工作。ExchangeExchange受信任子系統萬用安全性群組 (USG) 中執行工作。某些例外， Active Directory中的物件上的所有 Acl 該Exchange 2010都具有Exchange受信任子系統 USG 會授與存取權。這是從如何處理Exchange 2007中的權限的基本變更。

授與 Active Directory 中之使用者的權限，與使用者使用 Exchange 2013 管理工具時 RBAC 授與使用者的權限不同。

如需有關 RBAC 的詳細資訊，請參閱[了解角色型存取控制](understanding-role-based-access-control-exchange-2013-help.md)。

## Exchange 2007 權限

Exchange 2007系統管理模式如何運用以定義安全性界限Active Directory樹系。沒有隔離特定樹系內的安全性權限。樹系擁有者和企業系統管理員一律可以入侵任何網域中的所有資源的存取權。在Exchange 2007，您可能要企業系統管理員權限授與僅暫時為基礎的最上層網域系統管理員權限。

Exchange 2007 提供下列預先定義的系統管理員角色：

  - **Exchange 組織系統管理員角色**  此角色授與權限來控制Exchange 2007組織的所有層面。此外，具有此角色的系統管理員可以授與權限其他Exchange管理員。此角色會授與帳戶您用以安裝Exchange 2007。

  - **Exchange 僅檢視系統管理員角色**  此角色授與檢視Exchange設定的權限。不過，具有此角色的系統管理員無法修改Exchange 2007組織中的物件。

  - **Exchange 收件者系統管理員角色**  此角色授與權限管理電子郵件收件者。具有此角色的系統管理員可以修改Exchange-相關的使用者、 群組、 連絡人和通訊群組的項目。

  - **Exchange Server 系統管理員角色**  此角色授與權限管理特定伺服器。不過，此角色不會授與權限執行全域影響Exchange 2007組織的動作。

  - **Exchange 公用資料夾系統管理員角色**  此角色已新增在 Exchange 2007 Service Pack 1**.**此角色授與管理Exchange 2007組織中的公用資料夾的權限。

此權限模型使用 Usg 但不包括Exchange伺服器系統管理員角色的所有角色。當您執行Exchange 2007**Setup /PrepareAD**命令時，安裝程式的根網域中建立 Usg 和 Usg 提供整個樹系的範圍。Usg 指派給來管理整個Active DirectoryExchange物件的 Acl。

在Exchange 2007，您可以分隔管理員其指派各種角色。指派權限直接其中一個給使用者或 USG 的使用者為其成員。該使用者的Active Directory帳戶的內容中執行使用者執行任何動作。下表列出Exchange 2007系統管理員角色以及其Exchange-相關的權限。

### Exchange 2007 系統管理員角色

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>系統管理員角色</th>
<th>成員</th>
<th>成員隸屬</th>
<th>Exchange 權限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 組織系統管理員</p></td>
<td><p>系統管理員帳戶或用來安裝第一部 Exchange 2007 伺服器的帳戶</p></td>
<td><p>Exchange 收件者系統管理員</p>
<p><em>&lt;伺服器名稱&gt;</em> 的系統管理員本機群組</p></td>
<td><p>對 Active Directory 中 Microsoft Exchange 容器的完整控制</p></td>
</tr>
<tr class="even">
<td><p>Exchange 僅檢視系統管理員</p></td>
<td><p>Exchange 收件者系統管理員</p>
<p>Exchange Server 系統管理員 (<em>&lt;伺服器名稱</em>&gt;)</p></td>
<td><p>Exchange 收件者系統管理員</p>
<p>Exchange Server 系統管理員</p></td>
<td><p>對 Active Directory 中 Microsoft Exchange 容器的讀取權限</p>
<p>對具有 Exchange 收件者之所有 Windows 網域的讀取權限</p></td>
</tr>
<tr class="odd">
<td><p>Exchange 收件者系統管理員</p></td>
<td><p>Exchange 組織系統管理員</p></td>
<td><p>Exchange View-Only Administrators</p></td>
<td><p>對 Active Directory 使用者物件上之 Exchange 內容的完整控制</p></td>
</tr>
<tr class="even">
<td><p>Exchange Server 系統管理員</p></td>
<td><p>Exchange 組織系統管理員</p></td>
<td><p>Exchange View-Only Administrators</p>
<p><em>&lt;伺服器名稱</em>&gt; 的系統管理員本機群組</p></td>
<td><p>對 Exchange <em>&lt;伺服器名稱</em>&gt; 的完整控制</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>每個 Exchange 2007 電腦帳戶</p></td>
<td><p>Exchange View-Only Administrators</p></td>
<td><p>特殊</p></td>
</tr>
<tr class="even">
<td><p>Exchange 公用資料夾系統管理員</p></td>
<td><p>Exchange 組織系統管理員</p></td>
<td><p>Exchange View-Only Administrators</p></td>
<td><p>對管理所有公用資料夾 (獲授與建立頂層公用資料夾延伸權限) 的完整控制</p></td>
</tr>
</tbody>
</table>


如果您需要進行更細微權限工作分派，您可以修改個別Exchange 2007物件，例如通訊清單或資料庫的 Acl。您必須新增這些使用者是直接以 ACL 成員的使用者或安全性群組群組。然後，在特定使用者的內容執行動作。

如需如何在 Exchange 2007 中管理權限的相關資訊，請參閱[在 Exchange Server 2007 中設定權限](http://go.microsoft.com/fwlink/p/?linkid=90671)。

## Exchange 2013 與 Exchange 2007 共存權限

由於權限模型Exchange 2013和Exchange 2007而有所不同Exchange 2013權限分派是分開Exchange 2007權限指派。即使這兩個版本已安裝在相同樹系中也是 Exchange 的如此。沒有其他設定Exchange 2013管理員沒有必要的權限管理Exchange 2007-型伺服器和Exchange 2007管理員沒有必要的權限管理Exchange 2013-型伺服器。您應該考量下列問題：

  - 您要授與 Exchange 2013 系統管理員管理 Exchange 2007 伺服器的存取權嗎？

  - 您要授與 Exchange 2007 系統管理員管理 Exchange 2013 伺服器的存取權嗎？

  - 您要自訂 Exchange 2013 權限，使其符合對 Exchange 2007 ACL 所做的任何自訂嗎？

## 將 Exchange 2013 權限授與 Exchange 2007 系統管理員

如果您想Exchange 2007系統管理員能夠管理Exchange 2013伺服器， Exchange 2007系統管理員必須新增一或多個Exchange 2013角色群組的成員。您可以將使用者或 Usg 新增至角色群組。授與給角色群組的權限則會套用至使用者或 Usg 的成員身分加入。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您使用網域本機或全域 Active Directory 安全性群組，若是想要將其新增為 Exchange 2013 角色群組的成員，必須將其變更為 USG。Exchange 2013 只支援 USG。</td>
</tr>
</tbody>
</table>


下表說明 Exchange 2007 系統管理員角色與 Exchange 2013 角色群組之間的對應。

### Exchange 2007 系統管理員角色與 Exchange 2010 角色群組

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange 2007 系統管理員角色</th>
<th>Exchange 2013 角色群組</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 組織系統管理員</p></td>
<td><p>組織管理</p></td>
</tr>
<tr class="even">
<td><p>Exchange 收件者系統管理員</p></td>
<td><p>收件者管理</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server 系統管理員</p></td>
<td><p>伺服器管理</p></td>
</tr>
<tr class="even">
<td><p>Exchange 僅檢視系統管理員</p></td>
<td><p>僅限檢視組織管理</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>Exchange 2013 中沒有同等的角色群組</p>
<p>(如需如何建立自訂角色群組的詳細資訊，請參閱<a href="manage-role-groups-exchange-2013-help.md">管理角色群組</a>)。</p></td>
</tr>
<tr class="even">
<td><p>Exchange 公用資料夾系統管理員</p></td>
<td><p>公用資料夾管理</p></td>
</tr>
</tbody>
</table>


如果您的所有Exchange 2007管理員其中Exchange 2007系統管理角色的成員，您可以新增至其相等Exchange 2013角色群組的每個系統管理群組的成員。例如，如果您想要授與所有Exchange 2007組織系統管理員的完整存取Exchange 2013物件，請將Exchange組織管理員 USG 新增至組織管理角色群組。

如需如何將使用者和 USG 新增至角色群組的詳細資訊，請參閱[管理角色群組成員](manage-role-group-members-exchange-2013-help.md)。

如果您修改 Exchange 2007 物件的 ACL，以授與 Exchange 2007 系統管理員更細微的權限，並想要指派 Exchange 2013 伺服器的相似權限給這些系統管理員，請遵循下列步驟：

1.  檢閱對 Exchange 2007 物件所做的 ACL 自訂，並找出已被授與每個物件之權限的系統管理員。

2.  分類的每個Exchange 2007物件。例如，判斷物件是資料庫、 伺服器或收件者物件。

3.  將物件對應至相對應的Exchange 2013角色群組。如需內建角色群組的清單，請參閱[內建角色群組](built-in-role-groups-exchange-2013-help.md)。

4.  將 Usg 或為每一種物件的使用者新增至對應的Exchange 2013角色群組。如需如何將使用者和 Usg 新增至角色群組的詳細資訊，請參閱[管理角色群組成員](manage-role-group-members-exchange-2013-help.md)。

完成這些步驟之後， Exchange 2007系統管理員會對應至適當的Exchange 2013物件的特定角色群組的成員。Exchange 2007系統管理員可以使用Exchange 2013管理工具來管理Exchange 2013伺服器和收件者。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>一般而言，Exchange 2007 伺服器和收件者必須使用 Exchange 2007 管理工具來管理，而 Exchange 2013 伺服器和收件者必須使用 Exchange 2013 管理工具來管理。</td>
</tr>
</tbody>
</table>


如果內建角色群組不提供的特定您想要授與某些系統管理員的權限集，您可以建立自訂角色群組。當您建立自訂角色群組時，您可以選取哪些角色新增至其中。您可以定義您想要管理角色群組的成員的特定功能。例如，如果您要系統管理員管理僅通訊群組，您可以建立自訂角色群組、，然後選取 \[僅的通訊群組的角色。執行這項作業之後，該自訂角色群組的成員可以管理僅通訊群組。如需如何建立自訂角色群組的詳細資訊，請參閱[管理角色群組](manage-role-groups-exchange-2013-help.md)。

如果您將選擇性權限指派給某些 Exchange 2007 物件 (例如只允許系統管理員管理特定資料庫)，而您想要套用相同的組態至 Exchange 2013 伺服器，請參閱本主題稍後的「使用 Exchange 2007 中的管理範圍重新建立 Exchange 2013 ACL 自訂」。

## 將 Exchange 2007 權限授與 Exchange 2013 系統管理員

如果您想Exchange 2013系統管理員能夠管理Exchange 2007伺服器時，將Exchange 2013管理員新增至 Usg 或會對應至特定Exchange 2007系統管理員角色的 \[安全性\] 群組。或者，如果您已自訂 ACL 設定，請將管理員新增至適當的 Acl。角色群組是 Usg，因此角色群組可直接加入Exchange 2007系統管理員角色 Usg。

完成之後， Exchange 2013系統管理員將適當的Exchange 2007系統管理員角色或角色的成員。Exchange 2013系統管理員可以使用Exchange 2007管理工具來管理Exchange 2007伺服器和收件者。

## 使用 Exchange 2013 中的管理範圍重新建立 Exchange 2007 ACL 自訂

在Exchange 2007，當您想要限制可以管理特定信箱儲存區、 管理特定使用者或控制項，建立的信箱儲存區信箱時您必須修改您想要限制物件上呼叫的 Acl。Exchange 2013提供相同功能，但不必修改任何 Acl。其執行方法是使用管理範圍，亦即的 RBAC 元件。

管理範圍提供內建的範圍及自訂範圍定義系統管理員可以管理的物件。藉由套用管理範圍，您可以定義可以管理哪些收件者且哪一個信箱資料庫信箱可以建立，應管理哪些收件者或伺服器，以系統管理員一小群與沒有任何人。

您可以建立下列類型的管理範圍：

  - **預先定義相對**  預先定義的相對範圍會包含在Exchange 2013。您可以控制使用者所收到的下列與使用者的修改。例如預先定義的相對範圍可以控制使用者是否會看見只有其本身相關資訊或整個組織的相關資訊。

  - **收件者**  收件者範圍會控制哪些收件者系統管理員可以建立、 修改或刪除。這些選項可以根據組織單位 (OU)、 收件者篩選器，或兩者。收件者篩選器指定收件者必須符合要包含在範圍中的準則。例如，您可能會建立包含所有使用者在特定部門或特定位置中的收件者篩選器範圍。您甚至可以合併 Ou 和收件者篩選器來比對只是誰特定 OU 內且誰向特定管理員報告的使用者。

  - **伺服器**  伺服器範圍控制系統管理員可以管理哪些伺服器。您可以指定伺服器清單或伺服器篩選。伺服器清單您可以定義可以管理的伺服器的靜態清單。當收件者篩選，因為您可以指定具有要比對的準則以相同的方式運作伺服器篩選器。例如，您可能會建立符合特定Active Directory站台內的所有伺服器的伺服器範圍。

  - **資料庫**  資料庫範圍控制系統管理員可以管理哪些資料庫。他們也可以控制可在建立信箱資料庫或資料庫信箱可以移至。類似伺服器範圍他們可以定義為清單或篩選。例如，您可以建立清單或可讓管理員在建立信箱或將信箱移至特定子公司所管理的特定信箱資料庫的篩選器。

  - **獨佔**  收件者、 伺服器及資料庫範圍也可以建立為獨佔範圍。獨佔範圍工時以相同的方式以拒絕存取 Acl 中的 Ace。如果不要符合獨佔範圍時，只有系統管理員指派獨佔範圍可以管理該物件。即使不是互斥的另一個範圍符合相同的物件都會成立。當您可能會想僅一些、 高度受信任的個人能夠管理 executive 信箱，這是特別有用。即使另一個規則的收件者範圍更廣泛且在範圍中包含 executive 信箱、 指派更廣泛、 一般收件者範圍的系統管理員將無法管理該 executive 信箱除非他們也分派獨佔範圍。

管理範圍用於管理角色、 管理角色指派和控制人員可以管理哪些物件的管理角色群組與何種方式他們可以管理這些物件。如需詳細資訊，請參閱下列主題：

  - [了解管理角色範圍](understanding-management-role-scopes-exchange-2013-help.md)

  - [了解獨佔範圍](understanding-exclusive-scopes-exchange-2013-help.md)

  - [了解管理角色指派](understanding-management-role-assignments-exchange-2013-help.md)

  - [了解管理角色群組](understanding-management-role-groups-exchange-2013-help.md)

  - [了解管理角色](understanding-management-roles-exchange-2013-help.md)

若要建立Exchange 2013使用您可能會使用自訂的 Acl 已定義的管理範圍的相同的權限模型，您必須清查您已自訂的 Acl，然後建立 \[符合他們的管理範圍。您可以在收件者、 伺服器和資料庫物件使用可用的可篩選屬性來建立包含您想要控制存取每個管理範圍的物件的管理範圍。如需您可以使用與管理範圍篩選器的屬性的詳細資訊，請參閱[了解管理角色範圍篩選器](understanding-management-role-scope-filters-exchange-2013-help.md)。

如需如何建立管理範圍的詳細資訊，請參閱[建立規則或獨佔範圍](create-a-regular-or-exclusive-scope-exchange-2013-help.md)。

