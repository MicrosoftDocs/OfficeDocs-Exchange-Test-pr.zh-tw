---
title: '建立就地 eDiscovery 搜尋的自訂管理範圍: Exchange Online Help'
TOCTitle: 建立就地 eDiscovery 搜尋的自訂管理範圍
ms:assetid: 1543aefe-3709-402c-b9cd-c11fe898aad1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn741464(v=EXCHG.150)
ms:contentKeyID: 62219743
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 建立就地 eDiscovery 搜尋的自訂管理範圍

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2015-01-21_

您可以使用自訂管理範圍讓特定人員或群組使用「就地 eDiscovery」，在您的 Exchange 2013 或 Exchange Online 組織中搜尋信箱子集。例如，您可以讓探索管理員只在特定位置或部門中搜尋使用者的信箱。您可以建立自訂管理範圍來這樣做。此自訂管理範圍使用收件者篩選器來控制可搜尋的信箱。收件者篩選器範圍使用篩選器，根據收件者類型或其他收件者屬性，鎖定以特定的收件者為目標。

在「就地 eDiscovery」中，使用者信箱上只有通訊群組成員資格這個屬性 (實際屬性名稱為 *MemberOfGroup*) 可用來建立自訂範圍的收件者篩選器。如果您使用其他屬性 (例如 *CustomAttributeN*、*Department* 或 *PostalCode*)，則獲指派自訂範圍的角色群組成員執行搜尋時會失敗。

若要深入了解管理範圍，請參閱：

  - [了解管理角色範圍](understanding-management-role-scopes-exchange-2013-help.md)

  - [了解管理角色範圍篩選器](understanding-management-role-scope-filters-exchange-2013-help.md)

## 開始之前有哪些須知？

  - 預估完成時間：15 分鐘

  - 如前所述，您只能使用群組成員資格作為收件者篩選器，以建立主要用於 eDiscovery 的自訂收件者篩選器範圍。不能使用其他任何收件者屬性來建立 eDiscovery 搜尋的自訂範圍。請注意，也不能使用動態通訊群組中的成員資格。

  - 執行步驟 1 到 3，讓探索管理員為使用自訂管理範圍的 eDiscovery 搜尋匯出搜尋結果。

  - 如果探索管理員不需要預覽搜尋結果，您可以略過步驟 4。

  - 如果探索管理員不需要複製搜尋結果，您可以略過步驟 5。

## 步驟 1：將使用者組織成為 eDiscovery 的通訊群組

若要搜尋組織中的信箱子集，或將來源信箱縮小到探索管理員可搜尋的範圍，您需要將信箱子集分組成一或多個通訊群組。當您在步驟 2 中建立自訂管理範圍時，您將會使用這些通訊群組作為收件者篩選器來建立自訂管理範圍。這樣可讓探索管理員只搜尋身為特定群組之成員的使用者信箱。

您可以基於 eDiscovery 用途而使用現有的通訊群組，也可以建立新的通訊群組。如需有關如何建立可用來設定 eDiscovery 搜尋範圍的通訊群組的秘訣，請參閱本主題最後的＜其他資訊＞。

## 步驟 2：建立自訂管理範圍

現在，您將建立由通訊群組的成員資格所定義的自訂管理範圍 (使用 *MemberOfGroup* 收件者篩選器)。當此範圍套用至 eDiscovery 使用的角色群組時，角色群組的成員可以搜尋屬於用來建立自訂管理範圍之通訊群組成員的使用者信箱。

此程序使用 Exchange 管理命令介面命令來建立一個名為 Ottawa Users eDiscovery Scope 的自訂範圍。它指定名為 Ottawa Users 的通訊群組，作為自訂範圍的收件者篩選器。

1.  執行此命令來取得 Ottawa Users 群組的屬性並儲存為變數，下一個命令中將使用此變數。
    
        $DG = Get-DistributionGroup -Identity "Ottawa Users"

2.  執行此命令根據 Ottawa Users 通訊群組的成員資格來建立自訂管理範圍。
    
        New-ManagementScope "Ottawa Users eDiscovery Scope" -RecipientRestrictionFilter "MemberOfGroup -eq '$($DG.DistinguishedName)'"
    
    通訊群組的辨別名稱 (包含在變數 **$DG** 中) 用來建立新管理範圍的收件者篩選器。

## 步驟 3：建立管理角色群組

在此步驟中，您建立新的管理角色群組，並指派您在步驟 2 中建立的自訂範圍。加入 Legal Hold 和 Mailbox Search 角色，讓角色群組成員能夠執行「就地 eDiscovery」搜尋，並將信箱置於「就地保留」或「訴訟暫止」狀態。您也可以將成員加入至這個角色群組，讓他們能夠搜尋步驟 2 中用來建立自訂範圍之通訊群組成員的信箱。

在下列範例中，將加入 Ottawa Users eDiscovery Managers 安全性群組作為此角色群組的成員。您可以使用命令介面或 EAC 來執行此步驟。

## 使用命令介面來建立管理角色群組

執行此命令來建立新的角色群組，該群組使用步驟 2 中建立的自訂範圍。此命令也會加入 Legal Hold 和 Mailbox Search 角色，並加入 Ottawa Users eDiscovery Managers 安全性群組作為新角色群組的成員。

    New-RoleGroup "Ottawa Discovery Management" -Roles "Mailbox Search","Legal Hold" -CustomRecipientWriteScope "Ottawa Users eDiscovery Scope" -Members "Ottawa Users eDiscovery Managers"

## 使用 EAC 來建立管理角色群組

1.  在 EAC 中，移至 **\[權限\]** \> **\[管理員角色\]**，然後按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")\]。

2.  在 **\[新增角色群組\]** 中，提供下列資訊：
    
      - **名稱**   提供新角色群組的描述性名稱。在此範例中，您使用 **Ottawa Discovery Management**。
    
      - **寫入範圍**   選取您在步驟 2 中建立的自訂管理範圍。此範圍會套用至新的角色群組。
    
      - **角色**   按一下 \[**加入**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")\]，然後將 **Legal Hold** 和 **Mailbox Search** 角色加入至新的角色群組。
    
      - **成員**   按一下 \[**加入**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")\]，然後選取要加入成為新角色群組之成員的使用者、安全性群組或角色群組。在此範例中，**Ottawa Users eDiscovery Managers** 安全性群組的成員只能搜尋身為 **Ottawa Users** 通訊群組成員的使用者信箱。

3.  按一下 **\[儲存\]** 以建立角色群組。
    
    以下是完成時的 **\[新增角色群組\]** 視窗的畫面。
    
    ![為自訂範圍建立新的角色群組](images/Dn741464.a6e3419f-d5d9-404f-890d-ad35f499756f(EXCHG.150).gif "為自訂範圍建立新的角色群組")  

## (選用) 步驟 4：加入探索管理員作為用來建立自訂管理範圍的通訊群組成員

只有在想讓探索管理員預覽 eDiscovery 搜尋結果時，才需要執行此步驟。

執行此命令來加入 Ottawa Users eDiscovery Managers 安全性群組作為 Ottawa Users 通訊群組的成員。

    Add-DistributionGroupMember -Identity "Ottawa Users" -Member "Ottawa Users eDiscovery Managers"

您也可以使用 EAC 將成員加入至通訊群組。如需詳細資訊，請參閱 [建立並管理通訊群組](create-and-manage-distribution-groups-exchange-2013-help.md)。

## (選用) 步驟 5：加入探索信箱作為用來建立自訂管理範圍的通訊群組成員

只有在想讓探索管理員複製 eDiscovery 搜尋結果時，才需要執行此步驟。

執行此命令來加入名為 Ottawa Discovery Mailbox 的探索信箱作為 Ottawa Users 通訊群組的成員。

    Add-DistributionGroupMember -Identity "Ottawa Users" -Member "Ottawa Discovery Mailbox"

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要開啟探索信箱和檢視搜尋結果，探索管理員必須獲指派探索信箱的「完整存取」權限。如需詳細資訊，請參閱 <a href="create-a-discovery-mailbox-exchange-2013-help.md">建立探索信箱</a>。</td>
</tr>
</tbody>
</table>


## 如何知道這是否正常運作？

以下提供一些方法來確認您是否已成功實作 eDiscovery 的自訂管理範圍。在驗證時，請確定執行 eDiscovery 搜尋的使用者是使用自訂管理範圍的角色群組成員。

  - 建立 eDiscovery 搜尋，然後選取用來建立自訂管理範圍的通訊群組，作為要搜尋的信箱來源。應該可成功搜尋所有信箱。

  - 建立 eDiscovery 搜尋，然後搜尋不屬於用來建立自訂管理範圍之通訊群組成員的任何使用者的信箱。搜尋應該會失敗，因為探索管理員只能搜尋屬於用來建立自訂管理範圍之通訊群組成員的使用者信箱。在此情況下，將傳回「無法搜尋信箱 \<*信箱名稱*\>，因為目前的使用者沒有權限存取信箱」之類的錯誤。

  - 建立 eDiscovery 搜尋，然後搜尋屬於用來建立自訂管理範圍之通訊群組成員的使用者信箱。在相同的搜尋中，加入不是成員的使用者信箱。應該會順利完成部分搜尋。應該能順利搜尋用來建立自訂管理範圍之通訊群組成員的信箱。搜尋不是群組成員的使用者信箱應該會失敗。

## 其他資訊

  - 因為通訊群組在此案例中是用來設定 eDiscovery 搜尋的範圍，而不是用於郵件傳遞，在建立和設定 eDiscovery 的通訊群組時，請考量下列事項：
    
      - 以封閉式成員資格建立通訊群組，以限制只有群組擁有者才能在群組中加入或移除成員。如果您在命令介面中建立群組，請使用語法 `MemberJoinRestriction closed` 和 `MemberDepartRestriction closed`。
    
      - 啟用群組仲裁，使任何傳送至群組的郵件先傳送給群組仲裁者，由仲裁者視情況來核准或拒絕郵件。如果您在命令介面中建立群組，請使用語法 `ModerationEnabled $true`。如果您使用 EAC，您可以在建立群組之後啟用仲裁。
    
      - 從組織的共用通訊錄中隱藏通訊群組。在建立群組之後，使用 EAC 或 **Set-DistributionGroup** 指令程式。如果您使用命令介面，請使用語法 `HiddenFromAddressListsEnabled $true`。
    
    在下列範例中，第一個命令會建立具有封閉式成員資格並啟用仲裁的通訊群組。第二個命令會從共用通訊錄中隱藏群組。
    
        New-DistributionGroup -Name "Vancouver Users eDiscovery Scope" -Alias VancouverUserseDiscovery -MemberJoinRestriction closed -MemberDepartRestriction closed -ModerationEnabled $true
    
        Set-DistributionGroup "Vancouver Users eDiscovery Scope" -HiddenFromAddressListsEnabled $true
    
    如需有關建立和管理通訊群組的詳細資訊，請參閱＜[建立並管理通訊群組](create-and-manage-distribution-groups-exchange-2013-help.md)＞。

  - 雖然您只能使用通訊群組成員資格作為 eDiscovery 所使用的自訂管理範圍的收件者篩選器，但您可以使用其他收件者屬性將使用者加入至該通訊群組。以下一些範例說明使用 **Get-Mailbox** 和 **Get-Recipient** 指令程式，以根據一般使用者或信箱屬性來傳回一組特定的使用者。
    
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'Department -eq "HR"'
    
        Get-Mailbox -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'CustomAttribute15 -eq "VancouverSubsidiary"'
    
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'PostalCode -eq "98052"'
    
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'StateOrProvince -eq "WA"'
    
        Get-Mailbox -RecipientTypeDetails UserMailbox -ResultSize unlimited -OrganizationalUnit "namsr01a002.sdf.exchangelabs.com/Microsoft Exchange Hosted Organizations/contoso.onmicrosoft.com"

  - 然後，您可以利用先前項目符號中的範例來建立變數，此變數可用於 **Add-DistributionGroupMember** 指令程式中將一組使用者加入至通訊群組。在下列範例中，第一個命令會建立一個變數，此變數包含使用者帳戶中 *Department* 屬性值為 **Vancouver** 的所有使用者信箱。第二個命令會將這些使用者加入 Vancouver Users 通訊群組。
    
        $members = Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'Department -eq "Vancouver"'
    
        $members | ForEach {Add-DistributionGroupMember "Ottawa Users" -Member $_.Name}

  - 您可以使用 **Add-RoleGroupMember** 指令程式將成員加入至用來設定 eDiscovery 搜尋範圍的現有角色群組。例如，下列命令會將使用者 admin@ottawa.contoso.com 加入至 Ottawa Discovery Management 角色群組。
    
        Add-RoleGroupMember "Vancouver Discovery Management" -Member paralegal@vancouver.contoso.com
    
    您也可以使用 EAC 將成員新增至角色群組。如需詳細資訊，請參閱 ＜ [管理角色群組成員](manage-role-group-members-exchange-2013-help.md)的 「 新增成員至角色群組 」 一節。

  - 在Exchange Online、 ediscovery （英文） 所使用的自訂管理範圍無法來搜尋不在作用中的信箱。這是因為非使用中的信箱不能將通訊群組的成員。例如，假設使用者是用來建立自訂管理範圍的 eDiscovery 的通訊群組的成員。然後該使用者離開組織和他們的信箱就不在作用中 （放置訴訟暫止狀態或就地保留信箱並再將其刪除對應的 Office 365 使用者帳戶）。結果是使用者已從任何通訊群組，包括用來建立自訂管理範圍 ediscovery （英文） 所使用的群組成員身分。 如果探索管理員 （身為 「 已指派自訂管理範圍的角色群組的成員） 嘗試搜尋不在作用中的信箱搜尋會失敗。若要搜尋不在作用中的信箱，探索管理員必須是 「 探索管理角色群組或擁有權限來搜尋整個組織任何角色群組的成員。
    
    如需非使用中信箱的詳細資訊，請參閱[Exchange Online 中的非使用中信箱](https://technet.microsoft.com/zh-tw/library/dn798632\(v=exchg.150\))。

