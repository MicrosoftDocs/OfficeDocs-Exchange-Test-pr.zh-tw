---
title: '啟用或停用階層式通訊錄: Exchange Online Help'
TOCTitle: 啟用或停用階層式通訊錄
ms:assetid: b4c3a175-ce5e-4bfb-a4a0-92d25f3644b3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ff607473(v=EXCHG.150)
ms:contentKeyID: 50474057
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟用或停用階層式通訊錄

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

您可以設定階層式通訊錄 (HAB)，這是 Microsoft Outlook 2010 或更新版本中使用者可用的功能。透過 HAB，使用者可以使用以階層或管理結構為基礎的組織階層，尋找其 Exchange 組織中的收件者。若要深入瞭解 HAB，請參閱[階層式通訊錄](hierarchical-address-books-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：1 小時。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「通訊群組」項目。

  - 您無法使用 Exchange 系統管理中心 (EAC) 執行此程序。您必須使用命令介面。

  - 在開始之前，請閱讀主題[階層式通訊錄](hierarchical-address-books-exchange-2013-help.md)。您應該瞭解 HAB 是否適用於您的 Exchange 組織。

  - 瞭解目前如何在 Exchange 組織中設定組織單位 (OU)、群組、使用者和連絡人。

  - 瞭解下表中的指令程式和相關聯的參數，設定 HAB 時需要這些項目。
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>指令程式</th>
    <th>參數</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><a href="https://technet.microsoft.com/zh-tw/library/aa997443(v=exchg.150)">Set-OrganizationConfig</a></p></td>
    <td><p><em>HierarchicalAddressBookRoot</em></p></td>
    </tr>
    <tr class="even">
    <td><p><a href="https://technet.microsoft.com/zh-tw/library/bb123770(v=exchg.150)">Set-Group</a></p></td>
    <td><p><em>IsHierarchicalGroup</em></p>
    <p><em>SeniorityIndex</em></p>
    <p><em>PhoneticDisplayName</em></p></td>
    </tr>
    <tr class="odd">
    <td><p><a href="https://technet.microsoft.com/zh-tw/library/aa998221(v=exchg.150)">Set-User</a></p></td>
    <td><p><em>SeniorityIndex</em></p>
    <p><em>PhoneticDisplayName</em></p></td>
    </tr>
    <tr class="even">
    <td><p><a href="https://technet.microsoft.com/zh-tw/library/bb124535(v=exchg.150)">Set-Contact</a></p></td>
    <td><p><em>SeniorityIndex</em></p>
    <p><em>PhoneticDisplayName</em></p></td>
    </tr>
    </tbody>
    </table>


  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 您要執行的工作

## 使用命令介面啟用 HAB

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>雖然您無法使用 EAC 啟用 HAB，但在啟用之後，您可以使用 EAC 管理組織階層內的群組成員資格。</td>
</tr>
</tbody>
</table>


對於這個範例，將會對 HAB 建立 OU 呼叫的 HAB。組織的網域名稱為 Contoso-dom，而 Contoso,Ltd 是階層中最上層組織的名稱 (「根組織」)。名稱為 Corporate Office、Product Support Organization 和 Sales & Marketing Organization 的次級群組會在 Contoso,Ltd 下作為子組織而建立。此外，群組 Human Resources、Accounting Group 和 Administration Group 則會在 Corporate Office 下作為子組織而建立。

如需建立通訊群組的詳細資訊，請參閱[建立並管理通訊群組](create-and-manage-distribution-groups-exchange-2013-help.md)。

1.  在 Contoso 組織中建立 OU 命名的 HAB。您可以使用 Active Directory Users and Computers，或在命令提示字元中輸入下列內容。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>或者，您可以使用 Exchange 樹系中現有的 OU。</td>
    </tr>
    </tbody>
    </table>
    
        dsadd ou "OU=HAB,DC=Contoso-dom,DC=Contoso,DC=com"
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如需詳細資訊，請參閱 ＜<a href="https://go.microsoft.com/fwlink/p/?linkid=198986">建立新的組織單位</a>。</td>
    </tr>
    </tbody>
    </table>


2.  對 HAB 建立根通訊群組 Contoso,Ltd。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>針對本主題的目的，會提供命令介面範例。不過，您也可以使用 EAC 建立通訊群組。如需詳細資訊，請參閱<a href="create-and-manage-distribution-groups-exchange-2013-help.md">建立並管理通訊群組</a>。</td>
    </tr>
    </tbody>
    </table>
    
        New-DistributionGroup -Name "Contoso,Ltd" -DisplayName "Contoso,Ltd" -Alias "ContosoRoot" -OrganizationalUnit "Contoso-dom.Contoso.com/HAB" -SamAccountName "ContosoRoot" -Type "Distribution"

3.  將 Contoso,Ltd 指定為 HAB 的根組織。
    
        Set-OrganizationConfig -HierarchicalAddressBookRoot "Contoso,Ltd"

4.  對 HAB 中的其他層級建立通訊群組。對於這個範例，您會建立下列群組：Corporate Office、Product Support Organization、Sales & Marketing Organization、Human Resources、Accounting Group 和 Administration Group。這個範例會建立通訊群組 Corporate Office。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>針對本主題的目的，會提供命令介面範例。不過，您也可以使用 EAC 建立通訊群組。如需詳細資訊，請參閱<a href="create-and-manage-distribution-groups-exchange-2013-help.md">建立並管理通訊群組</a>。</td>
    </tr>
    </tbody>
    </table>
    
        New-DistributionGroup -Name "Corporate Office" -DisplayName "Corporate Office" -Alias "CorporateOffice" -OrganizationalUnit "Contoso-dom.Contoso.com/HAB" -SamAccountName "CorporateOffice" -Type "Distribution"

5.  將各個群組指定為 HAB 的成員。對於這個範例，您會將下列群組指定為階層式群組：Contoso,Ltd、Corporate Office、Product Support Organization、Sales & Marketing Organization、Human Resources、Accounting Group 和 Administration Group。這個範例會將通訊群組 Contoso,Ltd 指定為 HAB 的成員。
    
        Set-Group -Identity "Contoso,Ltd" -IsHierarchicalGroup $true

6.  將每個次級群組新增為根組織的成員。對於這個範例，通訊群組 Corporate Office、Product Support Organization 和 Sales & Marketing Organization 會新增為 HAB 中根組織 Contoso,Ltd 的成員。這個範例會將 Corporate Office 通訊群組新增為 Contoso,Ltd 根通訊群組的成員。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>這個範例會使用通訊群組的別名。</td>
    </tr>
    </tbody>
    </table>
    
        Add-DistributionGroupMember -Identity "ContosoRoot" -Member "CorporateOffice"

7.  將從屬於通訊群組 Corporate Office 的每一個群組新增為群組的成員。對於這個範例，通訊群組 Human Resources、Accounting Group 和 Administration Group 會新增為通訊群組 Corporate Office 的成員。這個範例會將 Human Resources 通訊群組新增為 Corporate Office 通訊群組的成員。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>這個範例會使用通訊群組的別名，並假設 Human Resources 通訊群組的別名為 HumanResources。</td>
    </tr>
    </tbody>
    </table>
    
        Add-DistributionGroupMember -Identity "CorporateOffice" -Member "HumanResources"

8.  將使用者加入 HAB 中的群組。對於這個範例，David Hamilton (SMTP 位址為 DHamilton@contoso.com) 是 OU Contoso-dom.Contoso.com/Users 中現有的使用者，並且會新增到群組 Corporate Office。重複這個步驟，以將其他使用者新增至 HAB 中的群組。
    
        Add-DistributionGroupMember -Identity "CorporateOffice" -Member "DHamilton"

9.  針對 HAB 中的群組設定 *SeniorityIndex* 參數。對於這個範例，Corporate Office 群組包含三個子群組：Human Resources、Accounting Group 和 Administration Group。不以遞增英文字母順序 (這是預設值) 列出群組，偏好的排序會是 Human Resources (*SeniorityIndex* = 100)、Accounting Group (*SeniorityIndex* = 50)，然後是 Administration Group (*SeniorityIndex* = 25)。這個範例會將 Human Resources 群組的 *SeniorityIndex* 參數設為 100。
    
        Set-Group -Identity "Human Resources" -SeniorityIndex 100
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><em>SeniorityIndex</em> 參數是數值，能以遞減數字順序排序 HAB 中的群組或使用者。如果 <em>SeniorityIndex</em> 參數未設定，或對於兩個或多個使用者來說是相等，則 HAB 排序順序會使用 <em>PhoneticDisplayName</em> 參數值以遞增英文字母順序來列出使用者。如果 <em>PhoneticDisplayName</em> 值未設定，則 HAB 排序順序預設為 <em>DisplayName</em> 參數值，並以遞增英文字母順序列出使用者。</td>
    </tr>
    </tbody>
    </table>


10. 針對 HAB 群組中的使用者設定 *SeniorityIndex* 參數。對於這個範例，Corporate Office 群組包含三個使用者：Amy Alberts、David Hamilton 和 Rajesh M. Patel。不以遞增的英文字母順序 (這是預設值) 列出使用者，偏好的排序會是 David Hamilton (*SeniorityIndex* = 100)、Rajesh M. Patel (*SeniorityIndex* = 50)，然後是 Amy Alberts (*SeniorityIndex* = 25)。這個範例會將使用者 David Hamilton 的 *SeniorityIndex* 參數設為 100。
    
        Set-User -Identity "DHamilton@contoso.com" -SeniorityIndex 100

完成上述步驟之後，HAB 便會顯示在 Outlook 中。若要檢視 HAB，請開啟 Outlook，然後按一下 \[通訊錄\]。HAB 會顯示在 \[組織\] 索引標籤上，類似下圖。

**Contoso,Ltd 的範例 HAB**

![階層式通訊錄對話方塊](images/Ff629379.d8cc782f-61cd-44c4-9c74-432ebea0c3db(EXCHG.150).gif "階層式通訊錄對話方塊")

建立 HAB 之後，您可以使用 EAC 來管理組織階層內的群組成員資格。不過，您必須使用命令介面，對任何新群組或使用者修改 *SeniorityIndex* 參數。

如需詳細的語法及參數資訊，請參閱下列各項：

  - [New-DistributionGroup](https://technet.microsoft.com/zh-tw/library/aa998856\(v=exchg.150\))

  - [Set-OrganizationConfig](https://technet.microsoft.com/zh-tw/library/aa997443\(v=exchg.150\))

  - [Set-Group](https://technet.microsoft.com/zh-tw/library/bb123770\(v=exchg.150\))

  - [Add-DistributionGroupMember](https://technet.microsoft.com/zh-tw/library/bb124340\(v=exchg.150\))

  - [Set-User](https://technet.microsoft.com/zh-tw/library/aa998221\(v=exchg.150\))

## 使用命令介面來停用階層式通訊錄

這個範例會停用用於 HAB 的根組織。

    Set-OrganizationConfig -HierarchicalAddressBookRoot $null

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>這個命令不會刪除 HAB 結構中使用的根組織或子群組，或對群組或使用者重設 <em>SeniorityIndex</em> 值。它只能防止 HAB 在 Outlook 中顯示。若要再次以相同的組態設定啟用 HAB，您只需要再次啟用根組織。</td>
</tr>
</tbody>
</table>


如需詳細的語法及參數資訊，請參閱 [Set-OrganizationConfig](https://technet.microsoft.com/zh-tw/library/aa997443\(v=exchg.150\))。

