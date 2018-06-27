---
title: '案例： 部署通訊錄原則: Exchange 2013 Help'
TOCTitle: 案例： 部署通訊錄原則
ms:assetid: 6ac3c87d-161f-447b-afb2-149ae7e3f1dc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ657455(v=EXCHG.150)
ms:contentKeyID: 50473405
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 案例： 部署通訊錄原則

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

## 部署案例

下列三種案例說明可能的部署解決方案的三種不同的組織類型。雖然有許多其他案例，以下涵蓋最常用的錯誤。地址清單及這些案例中的全域通訊清單 (Gal) 所建立根據篩選，例如邏輯分組物件的自訂屬性。

## 案例 1： 兩個個別公司-一部 Exchange 組織

此案例中是適用於政府機構案件、 部門或共用基礎結構，但沒有報表鏈結且沒有一般員工的部門。此外，部門沒有任何特殊安全性或隱私權顧忌。在此案例中，兩個通訊錄原則 (Abp) 建立出員工只能看到相同組織中的成員時檢視 GAL\] 或 \[查看其他通訊群組的成員資格。此外，沒有任何使用者將會跨整個組織的通訊群組的成員。

![具有兩個個別公司的通訊錄原則](images/JJ657455.b4fc82da-a659-4ade-ba33-d55d90dcf204(EXCHG.150).gif "具有兩個個別公司的通訊錄原則")

使用下列通訊清單、 全域通訊清單、 會議室清單及 Oab，建立使用分組物件搭配例如自訂屬性篩選收件者篩選器所建立的 Contoso 和 Humungous 保險 Abp。兩家公司都沒有任何兩者之間的互動不同，因為有共用不任何地址清單。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>Contoso</p></td>
<td><p>Humungous Insurance</p></td>
</tr>
<tr class="even">
<td><p>通訊清單</p></td>
<td><p>AL_CON_Groups</p>
<p>AL_CON_Users</p>
<p>AL_CON_Contacts</p></td>
<td><p>AL_HI_Groups</p>
<p>AL_HI_Users</p>
<p>AL_HI_Contacts</p></td>
</tr>
<tr class="odd">
<td><p>全域通訊清單</p></td>
<td><p>GAL_CON</p></td>
<td><p>GAL_HI</p></td>
</tr>
<tr class="even">
<td><p>會議室通訊清單</p></td>
<td><p>AL_CON_Rooms</p></td>
<td><p>AL_HI_Rooms</p></td>
</tr>
<tr class="odd">
<td><p>離線通訊錄 (OAB)</p></td>
<td><p>OAB_CON</p></td>
<td><p>OAB_HI</p></td>
</tr>
</tbody>
</table>


## 案例 2： 兩家公司共用 CEO

在此案例中，Fabrikam 及 Tailspin Toys 共用相同的 Exchange 組織與相同 CEO。執行長是兩個公司之間僅限常見的人員。此案例需要三個 Abp 具有下列特性：

  - Tailspin Toys 公司的使用者在瀏覽全域通訊清單時僅能看到 Tailspin Toys 公司的使用者。

  - Fabrikam 公司的使用者在瀏覽全域通訊清單時僅能看到 Fabrikam 公司的使用者。

  - 每間公司各自擁有一個 SeniorLeaders 通訊群組，當中包含了該公司的資深領導人和共同的 CEO。

  - 查看 CEO 的群組成員資格的使用者只會看到屬於使用者的公司的群組。就不會看到群組不在自己的公司。

  - 所建立的三個 Abp： **Fab**、**條紋**，以及**執行長**。

![兩家公司一位執行長](images/Hh529948.c87a5654-d456-4688-acb2-0be15ba1cda6(EXCHG.150).gif "兩家公司一位執行長")


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>Fabrikam</p></td>
<td><p>Tailspin Toys</p></td>
<td><p>CEO</p></td>
</tr>
<tr class="even">
<td><p>通訊清單</p></td>
<td><p>AL_FAB_Users_DGs</p>
<p>AL_FAB_Contacts</p></td>
<td><p>AL_TAIL_Users_DGs</p>
<p>AL_TAIL_Contacts</p></td>
<td><p>AL_FAB_Users_DGs</p>
<p>AL_FAB_Contacts</p>
<p>AL_TAIL_Users_DGs</p>
<p>AL_TAIL_Contacts</p></td>
</tr>
<tr class="odd">
<td><p>全域通訊清單</p></td>
<td><p>GAL_FAB</p></td>
<td><p>GAL_TAIL</p></td>
<td><p>預設 GAL</p></td>
</tr>
<tr class="even">
<td><p>會議室通訊清單</p></td>
<td><p>AL_FAB_Rooms</p></td>
<td><p>AL_TAIL_Rooms</p></td>
<td><p>預設所有會議室</p></td>
</tr>
<tr class="odd">
<td><p>離線通訊錄 (OAB)</p></td>
<td><p>OAB_FAB</p></td>
<td><p>OAB_TAIL</p></td>
<td><p>預設 OAB</p></td>
</tr>
</tbody>
</table>


當執行長新增至每個組織的通訊群組並再執行長變成可以看到每個公司內的每個公司 ABP 範圍都屬於。執行長可以建立通訊群組跨越這兩家公司並將會出現在每個公司的 GAL 但通訊群組的成員僅能檢視他們自己的組織內之群組的成員。

## 案例 3： 教育

此案例中是適用於學校或大學其中類別的會議室的部門是必要確保學生的隱私。教育案例具有下列特性：

  - 每間教室的學生只能看到同班同學、老師和校長。

  - 老師只看得到自己教室內的學生。

  - 老師可以看到所有其他老師和校長。

  - 通訊群組是為每間教室的學生家長和教職員而建立的。

![通訊錄原則教育案例](images/JJ657455.435f3b1a-9752-4c61-ab8a-80115c643d12(EXCHG.150).gif "通訊錄原則教育案例")


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>Students_ClassA</p></td>
<td><p>Teachers_ClassA</p></td>
<td><p>校長</p></td>
</tr>
<tr class="even">
<td><p>通訊清單</p></td>
<td><p>AL_ClassAAL_Principal</p></td>
<td><p>AL_ClassAAL_AllTeachersAL_AllGroupsAL_Principal</p></td>
<td><p>AL_ClassA</p>
<p>AL_ClassB</p>
<p>AL_AllTeachers</p>
<p>AL_AllStudents</p>
<p>AL_AllGroups</p></td>
</tr>
<tr class="odd">
<td><p>全域通訊清單</p></td>
<td><p>GAL_StudentsClassA</p></td>
<td><p>GAL_TeachersClassA</p></td>
<td><p>GAL_Everyone</p></td>
</tr>
<tr class="even">
<td><p>會議室通訊清單</p></td>
<td><p>AL_BlankRoom</p></td>
<td><p>AL_BlankRoom</p></td>
<td><p>預設所有會議室</p></td>
</tr>
<tr class="odd">
<td><p>離線通訊錄 (OAB)</p></td>
<td><p>OAB_StudentsClassA</p></td>
<td><p>OAB_TeachersClassA</p></td>
<td><p>預設 OAB</p></td>
</tr>
</tbody>
</table>


## 考量與最佳作法

在組織中使用 ABP 時，請考量下列事項：

  - 為使 ABP 能正確運作，您套用 ABP 的使用者信箱必須位於 Exchange 2010 SP3 或 Exchange 2013 伺服器上。

  - 不要在通用類別目錄伺服器上執行 Exchange 2010 用戶端存取伺服器角色。正在使用名稱服務提供者介面 (NSPI)，而不是 Microsoft Exchange 通訊錄服務的 Active Directory 中會產生能力。您可以在通用類別目錄伺服器上執行 Exchange 2013 伺服器角色且正常運作，但不建議在網域控制站上安裝 Exchange 的 Abp。

  - 您無法使用階層式通訊錄 (HABs) 和 Abp 同時。深入了解，請參閱 ＜ [階層式通訊錄](hierarchical-address-books-exchange-2013-help.md)。

  - 任何已指定 ABP 的使用者應存在於自己的 GAL 中。

  - 如果允許用戶端應用程式以存取 Active Directory 直接透過 LDAP，會將會略過 Abp 內建的邏輯。Outlook for Mac 2011 與 Entourage 2008 使用直接 LDAP 查詢來存取 Active Directory，因為這些用戶端應用程式不會正確運作 Abp 如果在網域控制站或通用類別目錄伺服器未指定或自動探索服務所提供給他們。Outlook for Mac 2011 可以使用 EWS 或本機 OAB 來存取目錄資訊。不過，如果 Outlook for Mac 2011 可以直接存取 LDAP 服務，它會嘗試這麼做。

  - GAL 中使用 ABP 必須至少包含所有地址的清單，包括的會議室通訊清單，定義且指定 ABP.不要建立包含較少的物件比在同一個 ABP.的地址清單中的任何 GAL

  - 建議您建立不跨虛擬組織界限的通訊群組。建立通訊群組包含下列問題中的多個虛擬組織結果的成員：
    
      - 若群組成員寄送郵件給通訊群組時要求傳遞或讀信回條，他們將可以在其他虛擬組織中，看得到群組成員的電子郵件地址。
    
      - 至通訊群組傳送加密的郵件與部分群組的成員不具有有效的數位 Id，如果寄件會收到警告訊息包含總數沒有有效 Id 成員以及其電子郵件的地址清單。 不過，如果沒有有效的數位 Id 那些成員的一些較寄件者的不同組織中，警告訊息將會包含正確的計數但不會納入其他組織成員的電子郵件地址。因此，總數將不會符合成員地址清單。
        
        例如，假設通訊群組包含五個成員總從兩個組織機構 A 和 b 機構。三個群組成員已從機構的且其中這些成員為無效的數位識別碼。其他兩個成員是來自機構 B 和兩個他們有無效的數位 Id。如果成員從機構的傳送加密的郵件至通訊群組的成員會收到警告訊息，說明有三個收件者沒有有效的數位 Id 總共。不過，只從機構的收件者電子郵件地址將會列在警告訊息。
    
      - ABP 的不適用於**Get-Group**指令程式。因此，任何使用者或能夠執行**Get-Group**的程序會看到他們可以存取任何群組中的所有成員。
        
        我們建議您修改群組管理的設定 OWA 選項讓使用者無法使用 Outlook Web App 來管理群組。若要防止使用者使用 OWA 選項來管理群組，請使用者排除 MyDistributionGroupMembership RBAC 角色。如需詳細資訊，請參閱[MyDistributionGroupMembership 角色](mydistributiongroupmembership-role-exchange-2013-help.md)。
    
      - 如果您允許使用者使用 Outlook 或 Outlook Web App 來管理群組，群組擁有者必須具有完整的群組成員清單可見性。

  - 所有 Abp 必須都包含會議室通訊清單。不過，如果您的組織不使用會議室通訊清單，您可以建立的預設空會議室通訊清單。

  - 部署 Abp 不會防止從另一個虛擬組織中的使用者傳送電子郵件的一部虛擬組織中的使用者。若要防止使用者傳送電子郵件與跨組織，建議您建立傳輸規則。例如，若要建立的傳輸規則會防止 Contoso 使用者接收的郵件來自 Fabrikam 的使用者，但仍可讓 Fabrikam 的資深領導小組將郵件傳送至 Contoso 的使用者，執行下列命令介面命令：
    
        New-TransportRule -Name "StopFabrikamtoContosoMail" -FromMemberOf "AllFabrikamEmployees" -SentToMemberOf "AllContosoEmployees" -DeleteMessage -ExceptIfFrom seniorleadership@fabrikam.com

  - 如果您想要強制執行的功能類似 Lync 用戶端 ABP，您可以在特定使用者物件上設定`msRTCSIP-GroupingID`屬性。如需詳細資訊，請參閱[取代成 Msrtcsip-groupingid](https://go.microsoft.com/fwlink/p/?linkid=232306)主題。

## 一般部署步驟

## 由通訊清單分割中遷移至 ABP

如果貴組織中進行設定 Exchange 2007 地址清單區隔解決方案白皮書[設定虛擬組織與 Exchange 2007 中的地址清單區隔](https://go.microsoft.com/fwlink/p/?linkid=109601)中使用的指示，您應該先移轉至 Exchange Server 2010 使用[移轉至 Exchange Server 2010 通訊錄原則從 Exchange Server 2007 地址清單區隔](https://go.microsoft.com/fwlink/p/?linkid=235967)中所述的步驟。此程序將您的組織需要一些停機時間與因此您必須據此計劃。

## 新通訊錄原則部署

如果您的組織正在部署 Exchange 2013 通訊錄原則，且未進行過 Exchang 2007 通訊清單分割作業，則可以利用這些步驟在組織中部署通訊錄原則。

本章節中的步驟會引導您逐步完成案例 2：共用 CEO 的兩個公司。在此案例中，兩個公司 （Fabrikam 和 Tailspin Toys） 不同但 CEO 及資深領導小組共用。

## 步驟 1： 安裝及設定 Address Book Policy Routing 代理程式

如果您使用 Abp，而且不想不同的虛擬組織中的使用者能夠檢視彼此的潛在私人資訊，您可以開啟的 Address Book Policy Routing 代理程式。Address Book Policy Routing 代理程式是信箱伺服器執行收解決的方式，可控制在組織中傳輸代理程式。當通訊錄原則路由代理程式安裝及設定時，已指派不同的 Gal 使用者顯示為外部收件者，因為他們無法檢視外部收件者的連絡人卡片。

如需詳細指示，請參閱[安裝及設定 Address Book Policy Routing 代理程式](install-and-configure-the-address-book-policy-routing-agent-exchange-2013-help.md)。

## 步驟 2： 劃分為您的虛擬組織

您將需要開發劃分為貴組織的方式。我們建議使用 CustomAttribute1-15 屬性上信箱、 連絡人及群組，而不是預先定義的條件屬性如公司、 部門或 StateOrProvince 分隔的虛擬組織基於下列原因：

  - 並非所有收件者類型的物件有預先定義 Active Directory 中設定格式化的條件屬性。例如，通訊群組和動態通訊群組不支援公司、 部門或 state 屬性。

  - 並非所有預先定義的條件屬性都會公開 cmdlet 中的某些收件者。例如， *Company*、 *department*，以及*StateOrProvince*參數沒有提供的郵件使用者、 連絡人、 通訊群組及擁有郵件功能的公用資料夾的顯示在指令程式。

  - 多個 cmdlet 所需隔離收件者時使用的預先定義的設定格式化的條件屬性。例如，您需要執行 Set-user *Company*、 *Department*、 *StateOrProvince*標記的 UserMailbox 之後執行**New-Mailbox**或**Set-Mailbox**指令程式。

  - 所有收件者類型的 Set-\* 指令程式中會顯示所有的 *CustomAttributeX* 參數，我們因此能透過單一 Set- 指令程式完成該類型的所有分割作業。

  - CustomAttributeX 屬性會為組織自訂作業而明確予以保留，並完全由組織系統管理員所控制。

另請考慮實作時加以分離貴組織的最佳作法是使用中的通訊群組和動態通訊群組名稱的公司識別碼。Exchange 具有會根據許多屬性建立包括建立者的通訊群組的公司、 StateorProvince、 Title、 及 CustomAttribute15 以 CustomAttribute1 為通訊群組的使用者通訊群組的名稱自動新增尾碼或首碼群組命名原則功能。群組命名原則，請務必特別是如果您要讓使用者能夠建立自己的通訊群組。如需詳細資訊，請參閱[建立通訊群組命名原則](create-a-distribution-group-naming-policy-exchange-2013-help.md)。

群組命名原則並不適用於動態通訊群組，因此必須以手動方式分割並手動套用命名原則。

## 步驟 3： 建立通訊清單、 Gal 及 Oab

當您建立通訊清單及全域通訊清單不使用"IncludedRecipient"和"ConditionalX"參數，例如 ConditionalCompany 和 ConditionalCustomAttribute5。您應該改為使用收件者篩選器。您必須使用命令介面來建立收件者篩選器。如需收件者篩選器的詳細資訊，請參閱[Edge Transport Server 上的收件者篩選](recipient-filtering-on-edge-transport-servers-exchange-2013-help.md)

中建立 ABP，您將建立多個地址清單根據您想讓使用者在 Outlook 或 Outlook Web App 中檢視地址清單的方式。此組織有四個通訊清單：

  - AL\_FAB\_Users\_DGs

  - AL\_FAB\_Contacts

  - AL\_TAIL\_Users\_DGs

  - AL\_TAIL\_Contacts

此範例會建立 AL\_TAIL\_Users\_DGs 的地址清單。通訊清單包含所有的使用者和 CustomAttribute15 其中等於條紋的通訊群組。

    New-AddressList -Name "AL_TAIL_Users_DGs" -RecipientFilter {((RecipientType -eq 'UserMailbox') -or (RecipientType -eq "MailUniversalDistributionGroup") -or (RecipientType -eq "DynamicDistributionGroup")) -and (CustomAttribute15 -eq "TAIL")}

如需更多有關使用收件者篩選器建立通訊清單的資訊，請參閱[使用收件者篩選器來建立通訊清單](create-an-address-list-by-using-recipient-filters-exchange-2013-help.md)。

可建立將 ABP，您必須提供會議室通訊清單。如果您的組織如會議室或設備信箱沒有資源信箱，我們建議您建立的空白會議室通訊清單。下列範例會在因為在組織中有無會議室信箱建立空白會議室通訊清單。

    New-AddressList -Name AL_BlankRoom -RecipientFilter {(Alias -ne $null) -and ((RecipientDisplayType -eq 'ConferenceRoomMailbox') -or (RecipientDisplayType -eq 'SyncedConferenceRoomMailbox'))}

不過，在此案例中，Fabrikam 與 Contoso 有會議室信箱。本範例會建立會議室清單為 Fabrikam 使用其中 CustomAttribute15 等於 FAB 收件者篩選器。

    New-AddressList -Name AL_FAB_Room -RecipientFilter {(Alias -ne $null) -and (CustomAttribute15 -eq "FAB")-and (RecipientDisplayType -eq 'ConferenceRoomMailbox') -or (RecipientDisplayType -eq 'SyncedConferenceRoomMailbox')}

將 ABP 中所使用的全域通訊清單必須是更多的地址清單。不會有較少物件比存在於中任一或所有 ABP.通訊清單建立 GAL本範例會建立包含所有存在之收件者地址清單和會議室通訊清單中的 Tailspin Toys 的全域通訊清單。

    New-GlobalAddressList -Name "GAL_TAIL" -RecipientFilter {(CustomAttribute15 -eq "TAIL")}

如需詳細資訊，請參閱 [建立全域通訊清單](create-a-global-address-list-exchange-2013-help.md)。

當您建立時意外遺失時提供*AddressLists*參數的 New-或 Set-offlineaddressbook 以確保任何項目應包含適當的 GAL 的 OAB。基本上，您可以自訂的使用者會看到或藉由指定的 AddressLists 清單中 AddressLists 的 New/Set-offlineaddressbook 減少 OAB 下載大小的項目。不過，如果您想讓使用者看到完整的 GAL OAB 中的項目，請確定 AddressLists 納入 GAL。

此範例會為 Fabrikam 建立名為 OAB\_FAB 的離線通訊錄 (OAB)。

    New-OfflineAddressBook -Name "OAB_FAB" -AddressLists "GAL_FAB"

如需詳細資訊，請參閱 [建立離線通訊錄](create-an-offline-address-book-exchange-2013-help.md)。

## 步驟 4： 建立 Abp

您已建立的所有必要物件之後，您可以建立 ABP.此範例會建立名為 ABP\_TAIL ABP。

    New-AddressBookPolicy -Name "ABP_TAIL" -AddressLists "AL_TAIL_Users_DGs"," AL_TAIL_Contacts" -OfflineAddressBook "\OAB_TAIL" -GlobalAddressList "\GAL_TAIL" -RoomList "\AL_TAIL_Rooms"

如需詳細資訊，請參閱 [建立通訊錄原則](create-an-address-book-policy-exchange-2013-help.md)。

## 步驟 5： 將 Abp 指派給信箱

將 ABP 指派給使用者是程序中的最後一個步驟。當使用者的應用程式連線至用戶端存取伺服器上的 Microsoft Exchange 通訊錄服務 Abp 就會生效。如果使用者已連線至 Outlook 或 Outlook Web App ABP 套用至其帳戶時，他們必須關閉並重新啟動用戶端應用程式，才可以看到其新的通訊清單和 GAL。

此範例會指派 ABP\_FAB 給 CustomAttribute15 等於 "FAB" 的所有信箱。

    Get-Mailbox -resultsize unlimited | where {$_.CustomAttribute15 -eq "TAIL"} | Set-Mailbox -AddressBookPolicy "ABP_TAIL"

如需詳細資訊，請參閱 [通訊錄原則指派給郵件使用者](assign-an-address-book-policy-to-mail-users-exchange-2013-help.md)。

