---
title: '權限: Exchange 2013 Help'
TOCTitle: 權限
ms:assetid: d8dd605e-0af1-4e18-9ce6-e51d04e161ba
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd351175(v=EXCHG.150)
ms:contentKeyID: 50474360
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 權限

 

_**適用版本：**Exchange Server, Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

Microsoft Exchange Server 2013包含大型，預先定義的權限，您可以輕鬆地授與權限給系統管理員和使用者立即使用角色型存取控制 (RBAC) 權限模型為基礎。您可以Exchange 2013中使用的權限功能，讓您可以取得新的組織設定且快速地執行。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有幾項 RBAC 功能和概念屬於進階功能，因此不在本主題討論之列。如果本主題所討論的功能不符合您的需求，而且您想進一步自訂權限模型，請參閱<a href="understanding-role-based-access-control-exchange-2013-help.md">了解角色型存取控制</a>。</td>
</tr>
</tbody>
</table>


要尋找之所有的權限主題清單嗎？請參閱Permissions documentation。

**目錄**

Role-based permissions

Role groups and role assignment policies

Work with role groups

Work with role assignment policies

## 以角色為基礎的權限

Exchange 2013，在您授與系統管理員和使用者的權限根據管理角色。角色定義的系統管理員或使用者可以執行的工作。例如，呼叫`Mail Recipients`管理角色定義某人可在一組的信箱、 連絡人和通訊群組執行的工作。角色指派給系統管理員或使用者，當該名人員會授與角色所提供的權限。

角色可分成系統管理角色和使用者角色兩種類型：

  - **系統管理角色**   您可以使用負責管理 Exchange 組織某個部分 (例如收件者、伺服器或資料庫) 的角色群組，將這些角色包含的權限指派給系統管理員或專家使用者。

  - **使用者角色**  這些角色指派利用角色指派原則，讓使用者管理其所擁有自己信箱和通訊群組的層面。使用者角色的前置詞`My`開頭。

角色授與權限可讓指令程式可用來指派角色的使用者可以執行系統管理員和使用者的工作。Exchange 系統管理中心 (EAC) 和Exchange管理命令介面使用 cmdlet 來管理Exchange，因為授與存取權指令程式讓系統管理員或使用者執行工作的每個Exchange管理的權限介面。

Exchange 2013包含可用來授與權限大約 86 的角色。如需隨附Exchange 2013角色的清單，請參閱[內建管理角色](built-in-management-roles-exchange-2013-help.md)。

回到頁首

## 角色群組和指派原則

角色可授與在 Exchange 2013 中執行工作的權限，但是您還需要一種可將角色指派給系統管理員和使用者的簡易方式。Exchange 2013 提供下列項目來協助您執行這項作業：

  - **角色群組**   角色群組可讓您授與權限給系統管理員和專家使用者。

  - **角色指派原則**   角色指派原則可讓您授與使用者在其專屬信箱或所擁有之通訊群組上變更設定的權限。

如需角色群組和角色指派原則的詳細資訊，請參閱下列各節。

## 角色群組

管理Exchange 2013每個系統管理員必須具有至少一或多個角色。因為它們可能會執行跨多個區域Exchange中的工作功能系統管理員可能會有一個以上的角色。例如，一位管理員可能會管理收件者和Exchange伺服器。在此例中，系統管理員可能會指派`Mail Recipients`和`Exchange Servers`角色。

若要讓您輕鬆將多個角色指派給系統管理員， Exchange 2013包含角色群組。角色群組是特殊萬用安全性群組 (Usg) 使用Exchange 2013內含Active Directory使用者、 Usg 及其他角色群組。當角色指派給角色群組時、 角色授與的權限會授與的角色群組所有成員。這可讓您一次將許多角色指派給許多角色群組成員。角色群組通常包含更廣泛的管理方面，例如收件者管理。它們只適用於系統管理角色、 使用者角色無法用。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>很可能角色直接指派給使用者或 USG 而不需使用角色群組。但角色指派該方法是進階的程序並不本主題所述。我們建議您使用角色群組管理的權限。</td>
</tr>
</tbody>
</table>


下圖顯示使用者、角色群組和角色之間的關係。

**角色、角色群組和角色群組成員**

![角色、角色群組和成員關係](images/Dd351175.3fb0b47d-333a-4953-ae38-d710d327bde0(EXCHG.150).gif "角色、角色群組和成員關係")

Exchange 2013包含數個內建角色群組，每一個提供管理Exchange 2013中的特定區域的權限。部分的角色群組可能會重疊與其他人。下表列出每個角色具有群組用途的描述。 如果您想要查看指派給每個角色群組的角色，按一下 \[」 角色群組 」\] 欄中的角色群組的名稱，然後開啟 \[」 管理角色指派到此角色群組 」 一節。

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
<td><p>屬於 組織管理 角色群組之成員的系統管理員擁有整個 Exchange 2013 組織的管理存取權，並幾乎可對任何 Exchange 2013 物件執行任何工作，只有少部分例外，例如 <code>Discovery Management</code> 角色。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>由於 組織管理 角色群組是功能強大的角色，因此只有執行可能影響整個 Exchange 組織之組織層級管理工作的使用者或 USG 才能成為這個角色群組的成員。</td>
</tr>
</tbody>
</table>

</td>
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
<td><p>屬於 UM Management 角色群組成員的系統管理員可以管理 Exchange 組織中的功能，例如整合通訊 (UM) 服務組態、信箱上的 UM 內容、UM 提示及 UM 自動語音應答組態。</p></td>
</tr>
<tr class="odd">
<td><p><a href="help-desk-exchange-2013-help.md">服務台</a></p></td>
<td><p>Help Desk 角色群組中，根據預設，可讓成員能檢視並修改組織中任何使用者的 Microsoft OfficeOutlook Web App選項。這些選項可能包括修改使用者的顯示名稱、 地址和電話號碼。它們不包含不Outlook Web App選項，例如或修改之信箱的大小設定為信箱位於信箱資料庫中可用的選項。</p></td>
</tr>
<tr class="even">
<td><p><a href="hygiene-management-exchange-2013-help.md">檢疫管理</a></p></td>
<td><p>身為檢疫管理角色群組成員的系統管理員可以設定Exchange 2013防毒及反垃圾郵件功能。Exchange 2013與整合協力廠商程式可以將服務帳戶新增至這些 cmdlet 來擷取並設定Exchange設定所需的程式存取權授與此角色群組。</p></td>
</tr>
<tr class="odd">
<td><p><a href="records-management-exchange-2013-help.md">記錄管理</a></p></td>
<td><p>屬於 記錄管理 角色群組成員的使用者可以設定符合性功能，例如保留原則標記、訊息分類和傳輸規則。</p></td>
</tr>
<tr class="even">
<td><p><a href="discovery-management-exchange-2013-help.md">探索管理</a></p></td>
<td><p>系統管理員或是屬於 探索管理 角色群組成員的使用者可在 Exchange 組織中執行信箱搜尋，以尋找符合特定準則的資料，並可以對信箱設定合法持有。</p></td>
</tr>
<tr class="odd">
<td><p><a href="public-folder-management-exchange-2013-help.md">公用資料夾管理</a></p></td>
<td><p>屬於「公用資料夾管理」角色群組成員的系統管理員可以在執行 Exchange 2013 的伺服器上管理公用資料夾。</p></td>
</tr>
<tr class="even">
<td><p><a href="server-management-exchange-2013-help.md">伺服器管理</a></p></td>
<td><p>屬於 Server Management 角色群組之成員的系統管理員可以設定伺服器特定的傳輸組態、整合通訊、用戶端存取以及信箱功能，例如資料庫複本、憑證、傳輸佇列及傳送連接器、虛擬目錄以及用戶端存取通訊協定。</p></td>
</tr>
<tr class="odd">
<td><p><a href="delegated-setup-exchange-2013-help.md">委派安裝</a></p></td>
<td><p>身為「委派安裝」角色群組成員的系統管理員，可部署先前已由 Exchange 2013 角色群組的成員提供的 組織管理 伺服器。</p></td>
</tr>
<tr class="even">
<td><p><a href="compliance-management-exchange-2013-help.md">規範管理</a></p></td>
<td><p>屬於規範管理角色群組成員的使用者可按照組織的原則，設定並管理 Exchange 規範設定。</p></td>
</tr>
</tbody>
</table>


如果您在小型組織中具有只有幾個系統管理員解決問題，您可能需要將這些管理員新增至只組織管理角色群組和您可能會永遠不需要使用其他角色群組。如果您在大型組織中工作時，您可能必須執行管理Exchange，例如收件者或伺服器管理的特定工作的管理員。在這些情況下，您可能會將一個收件者管理角色群組中，系統管理員與其他系統管理員新增至伺服器管理角色群組。系統管理員可以然後管理Exchange 2013其特定區域但不會有管理它們不是負責的部分權限。

如果Exchange 2013中的內建角色群組不符合您的系統管理員的工作函數，您可建立角色群組並新增至他們的角色。如需詳細資訊，請參閱本主題稍後的Work with 角色群組。

回到頁首

## 角色指派原則

Exchange 2013提供角色指派原則，因此您可以控制其所擁有的哪些使用者可以的設定在自己的信箱及通訊群組上。這些設定包括其顯示名稱、 連絡人資訊、 語音信箱設定及通訊群組成員資格。

Exchange 2013組織可以有多個提供不同的權限層級的不同類型的使用者在您組織中的角色指派原則。可允許某些使用者變更其地址或其他人無法根據其信箱相關聯的角色指派原則時建立通訊群組。角色指派原則新增到信箱，直接及每個信箱只可關聯一個角色指派原則一次。

在組織的角色指派原則中，有一個會被標示為預設的原則。如果在建立新信箱時沒有明確指派特定的角色指派原則，這些新信箱就會與預設的角色指派原則產生關聯。預設的角色指派原則應該包含多數信箱所應套用的權限。

權限是透過使用者角色來新增到角色指派原則。使用者角色以 `My` 開頭，而且它們授與給使用者的權限，只能讓他們管理自己的信箱或他們所擁有的通訊群組；使用者角色不能用來管理其他任何信箱。此外，您只能將使用者角色指派到角色指派原則。

將使用者角色指派到角色指派原則後，與該角色指派原則相關聯的所有信箱都會取得該角色所授與的權限。因此，您不需要設定個別的信箱，就可以對多組使用者新增或移除權限。下圖顯示：

  - 使用者角色會指派至角色指派原則。角色指派原則可以共用相同的使用者角色。

  - 角色指派原則會與信箱產生關聯。每個信箱只能與一個角色指派原則相關聯。

  - 在信箱與角色指派原則產生關聯後，使用者角色會套用到該信箱。信箱使用者會獲得角色所授與的權限。

**角色、角色指派原則和信箱**

![角色、角色指派原則關係、信箱關係](images/Dd351175.82e07b3d-da59-465b-b349-e0bfde369ace(EXCHG.150).gif "角色、角色指派原則關係、信箱關係")

預設角色指派原則角色指派原則功能隨附於Exchange 2013。顧名思義，它會為預設角色指派原則。如果您想要變更此角色指派原則所提供的權限或您想要建立角色指派原則，請參閱Work with 角色指派原則本主題稍後的。

## 使用角色群組

若要管理您的Exchange 2013使用角色群組的權限，我們建議您使用 Exchange 系統管理中心。當您使用 EAC 來管理角色群組時，您可以新增和移除角色和成員、 建立角色群組並複製角色群組與按幾下滑鼠。EAC 中提供簡單的對話方塊，如圖所示下，若要執行這些工作的 \[**新增角色群組**\] 對話方塊。

**EAC 中新增的 \[角色群組\] 對話方塊**

![EAC 中的 \[新增角色群組\] 對話方塊](images/Dd351175.e0577090-73e6-4671-ae98-78a8064fde87(EXCHG.150).jpg "EAC 中的 [新增角色群組] 對話方塊")

Exchange 2013包含數個不同權限集中到特定的系統管理方面的角色群組。如果這些現有的角色群組提供系統管理員管理Exchange 2013組織所需的權限，您只需要將系統管理員新增為適當的角色群組的成員。將管理員新增至角色群組之後，他們可以管理該角色群組與相關的功能。新增或移除角色群組的成員，開啟角色群組在 EAC 中，然後新增或移除成員資格清單中的成員。如需內建角色群組的清單，請參閱[內建角色群組](built-in-role-groups-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果系統管理員是多個角色群組的成員，Exchange 2013 會將系統管理員所屬角色群組提供的所有權限，授與給系統管理員。</td>
</tr>
</tbody>
</table>


如果沒有任何一個Exchange 2013所含的角色群組具有您所需要的權限，您可以使用 EAC 來建立角色群組並新增您需要的權限的角色。新角色群組，您將會：

1.  選擇角色群組的名稱。

2.  選取要新增到角色群組的角色。

3.  在角色群組中新增成員。

4.  儲存角色群組。

建立角色群組之後，您可以比照其他任何角色群組來管理它。

如果現有的角色群組具有一些，但並非所有需要的權限，您可以將它複製，然後進行變更建立角色群組。您可以複製現有的角色群組並進行變更，而不影響原始的角色群組。複製的角色群組的一部分，您可以新增的新名稱和描述、 新增和移除角色與新的角色群組，並新增成員。當您建立或複製角色群組時，您會使用如上圖所示的相同對話方塊。

您也可以修改現有的角色群組。您可以新增和移除現有的角色群組、 角色和新增和移除成員它同時，使用類似圖中 EAC\] 對話方塊。藉由新增和移除角色若要從角色群組、 您開啟和關閉系統管理功能該角色群組的成員。如需您可以新增至角色群組的角色的清單，請參閱[內建管理角色](built-in-management-roles-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>雖然您可以變更指派至內建角色群組的角色，我們還是建議您複製內建角色群組、修改角色群組複本，然後再新增成員到角色群組複本。</td>
</tr>
</tbody>
</table>


回到頁首

## 使用角色指派原則

若要管理的權限授與使用者來管理自己的信箱中Exchange 2013，我們建議您使用 EAC。當您使用 EAC 來管理使用者權限時，您可以新增角色、 角色中移除和建立角色指派原則按幾下滑鼠。EAC 中提供簡單的對話方塊，如圖所示下，若要執行這些工作的**角色指派原則**\] 對話方塊。

**EAC 中的 \[角色指派原則\] 對話方塊**

![EAC 中的 \[角色指派原則\] 對話方塊](images/Dd351175.ecdf3cd4-d50e-4014-95f8-1bd5dafacaff(EXCHG.150).jpg "EAC 中的 [角色指派原則] 對話方塊")

Exchange 2013包含名為預設角色指派原則角色指派原則。此角色指派原則可讓的使用者信箱相關聯其執行下列動作：

  - 加入或離開可讓成員自行管理成員資格的通訊群組。

  - 在自己的信箱上檢視並修改基本的信箱設定，例如收件匣規則、拼字檢查行為和 Microsoft ActiveSync 裝置。

  - 修改連絡資訊，例如公司地址和電話號碼、行動電話號碼，以及呼叫器號碼。

  - 建立、修改或檢視簡訊設定。

  - 檢視或修改語音信箱設定。

  - 檢視和修改市場應用程式。

  - 建立團隊信箱，並且將這些信箱連接到 Microsoft SharePoint 清單。

如果要從「預設角色指派原則」或其他任何角色指派原則新增或移除權限，您可以使用 EAC。使用的對話方塊與上圖所示的對話方塊類似。當您在 EAC 中開啟角色指派原則時，請選取要指派至該原則的角色旁的核取方塊，或清除想要移除的角色旁的核取方塊。您對角色指派原則所做的變更將會套用到與它相關聯的每一個信箱。

如果要指派不同的使用者權限給組織中各種類型的使用者，您可以建立角色指派原則。建立角色指派原則時，您會看到與上圖類似的對話方塊。您可以為角色指派原則指定新名稱，然後再選取要指派至角色指派原則的角色。建立角色指派原則後，您可以使用 EAC 讓它與信箱產生關聯。

如果想要變更預設的角色指派原則，您必須使用命令介面。在您變更預設的角色指派原則之後，如果沒有為建立的任何信箱明確指定角色指派原則，這些信箱都會與新的預設角色指派原則產生關聯。當您選取新的預設角色指派原則時，與現有信箱關聯的角色指派原則將維持不變。

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果選取含有子角色之角色的核取方塊，也會選取子角色的核取方塊。如果取消選取含有子角色之角色的核取方塊，也會取消選取子角色的核取方塊。<br />
如需如何建立角色指派原則或變更現有角色指派原則的詳細步驟，請參閱下列主題：
<ul>
<li><p><a href="manage-role-assignment-policies-exchange-2013-help.md">管理角色指派原則</a></p></li>
<li><p><a href="change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md">變更在信箱上的指派原則</a></p></li>
</ul></td>
</tr>
</tbody>
</table>


回到頁首

## 權限文件

下表包含主題的連結，這些主題有助於您瞭解和管理 Exchange 2013 中的權限。


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
<td><p><a href="understanding-role-based-access-control-exchange-2013-help.md">了解角色型存取控制</a></p></td>
<td><p>瞭解組成 RBAC 的各個元件，以及如何在角色群組及管理角色不足時建立進階權限模型。</p></td>
</tr>
<tr class="even">
<td><p><a href="understanding-multiple-forest-permissions-exchange-2013-help.md">了解多重樹系權限</a></p></td>
<td><p>瞭解在含有帳戶及資源樹系的組織中實作 RBAC 權限。</p></td>
</tr>
<tr class="odd">
<td><p><a href="understanding-split-permissions-exchange-2013-help.md">了解分割權限</a></p></td>
<td><p>瞭解使用 RBAC 及 Active Directory 分割權限來分割 Exchange 及安全性主體管理。</p></td>
</tr>
<tr class="even">
<td><p><a href="understanding-permissions-coexistence-with-exchange-2007-and-exchange-2010-exchange-2013-help.md">了解 Exchange 2007 與 Exchange 2010 的權限共存</a></p></td>
<td><p>設定權限以便能在現有的 Exchange 2007 和 Exchange 2010 組織中管理 Exchange 2013。</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-role-groups-exchange-2013-help.md">管理角色群組</a></p></td>
<td><p>使用角色群組設定 Exchange 系統管理員和專家使用者的權限。</p></td>
</tr>
<tr class="even">
<td><p><a href="manage-role-group-members-exchange-2013-help.md">管理角色群組成員</a></p></td>
<td><p>將成員新增到與角色群組。新增和移除成員若要從角色群組，由您設定誰能夠管理 Exchange 功能。</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-linked-role-groups-exchange-2013-help.md">管理連結的角色群組</a></p></td>
<td><p>在多重樹系 Exchange 部署中，設定 Exchange 系統管理員和專業使用者的權限。</p></td>
</tr>
<tr class="even">
<td><p><a href="manage-role-assignment-policies-exchange-2013-help.md">管理角色指派原則</a></p></td>
<td><p>設定使用者在自己的信箱上使用角色指派原則時，可存取哪些功能。</p></td>
</tr>
<tr class="odd">
<td><p><a href="change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md">變更在信箱上的指派原則</a></p></td>
<td><p>設定哪些角色指派原則套用於一個或多個信箱。</p></td>
</tr>
<tr class="even">
<td><p><a href="create-linked-role-groups-that-mirror-built-in-role-groups-exchange-2013-help.md">建立鏡像內建角色群組的連結的角色群組</a></p></td>
<td><p>重新建立內建角色群組成為多重樹系 Exchange 部署中連結的角色群組。</p></td>
</tr>
<tr class="odd">
<td><p><a href="view-effective-permissions-exchange-2013-help.md">檢視有效的權限</a></p></td>
<td><p>檢視哪些人擁有管理 Exchange 功能的權限。</p></td>
</tr>
<tr class="even">
<td><p><a href="feature-permissions-exchange-2013-help.md">功能權限</a></p></td>
<td><p>瞭解管理 Exchange 功能和服務所需的權限。</p></td>
</tr>
<tr class="odd">
<td><p><a href="advanced-permissions-exchange-2013-help.md">進階權限</a></p></td>
<td><p>使用進階 RBAC 功能建立高度自訂的權限模型，以滿足任何組織的需要。</p></td>
</tr>
</tbody>
</table>

