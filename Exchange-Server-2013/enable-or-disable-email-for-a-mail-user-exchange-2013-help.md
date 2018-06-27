---
title: '啟用或停用郵件使用者的電子郵件: Exchange 2013 Help'
TOCTitle: 啟用或停用郵件使用者的電子郵件
ms:assetid: 1e2571d4-ff84-4fda-bb1d-825e96e1bd26
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa996598(v=EXCHG.150)
ms:contentKeyID: 50553948
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟用或停用郵件使用者的電子郵件

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2012-11-14_

您可以為 Exchange 組織中停用現有郵件使用者的電子郵件。當您停用郵件使用者的電子郵件時，它已從 Exchange 與您組織的通訊錄。如果郵件使用者的通訊群組的成員，使用者不會再收到寄送至群組的郵件。另外，Exchange 屬性已從 Active Directory 中的使用者物件，但使用者物件和非 Exchange 屬性 （如連絡人及組織資訊） 都會保留在 Active Directory 中。

停用郵件使用者的電子郵件之後，您可以啟用郵件功能之使用者再次使用**Enable-MailUser**指令程式在命令介面中。您也可以使用此指令程式來啟用任何 Active Directory 使用者的郵件功能。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>郵件使用者 （也稱為<em>擁有郵件功能的使用者</em>） 的方式不同於組織中沒有信箱的使用者。主要差異是郵件使用者代表 Exchange 組織外部的使用者具有的外部電子郵件地址。沒有在組織中的信箱。如需有您組織中的信箱的使用者和郵件使用者之間的差異的詳細資訊，請參閱<a href="recipients-exchange-2013-help.md">收件者</a>。</td>
</tr>
</tbody>
</table>


關於與郵件使用者相關的其他管理工作，請參閱[管理郵件使用者](manage-mail-users-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：2 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「郵件使用者」項目。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 您要執行的工作

## 停用郵件使用者的電子郵件

如先前所述，當您停用郵件使用者的電子郵件、 Exchange 屬性已從對應的 Active Directory 郵件使用者物件，但是會保留使用者。郵件使用者會移除清單中的郵件使用者在 EAC 中，但您可以檢視和使用 Active Directory 使用者及電腦或命令介面中使用**Get-MailUser**和**Set-Set-MailUser**指令程式來管理對應的 Active Directory 連絡人物件。

## 使用 EAC 停用郵件使用者的電子郵件

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[連絡人\]。

2.  在連絡人清單中，按一下要停用其電子郵件的郵件使用者。

3.  按一下 \[更多\]![更多選項圖示](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "更多選項圖示")，然後按一下 \[停用\]。

4.  確定您要停用所選的郵件使用者會顯示詢問一則警告訊息。按一下 \[**是\]**以停用它。

郵件使用者會從連絡人清單中移除。

## 使用命令介面停用郵件使用者的電子郵件

此範例會停用郵件使用者 Yan Li 的電子郵件。

    Disable-MailUser -Identity "Yan Li"

如需詳細的語法及參數資訊，請參閱 [Disable-MailUser](https://technet.microsoft.com/zh-tw/library/aa998578\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要確認是否已成功停用郵件使用者的電子郵件，請執行下列其中一項操作：

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[連絡人\]，並確認該郵件使用者不再列出。

2.  Active Directory 使用者及電腦\] 中以滑鼠右鍵按一下 \[使用者\] 中，並再按一下 \[**內容**。在 \[**一般**\] 索引標籤上注意到**電子郵件**\] 方塊是空白。這會驗證郵件使用者無法擁有郵件功能。

3.  在命令介面中，執行下列命令。
    
        Get-MailUser
    
    您停用其電子郵件的郵件使用者不會回到結果中，因為此 Cmdlet 只會傳回啟用郵件功能的使用者。

4.  在命令介面中，執行下列命令。
    
        Get-User
    
    您停用其電子郵件的郵件使用者會回到結果中，因為此 Cmdlet 會傳回所有 Active Directory 使用者物件。

## 使用命令介面啟用使用者的郵件功能

您可以使用**Enable-MailUser**指令程式來啟用現有的 Active Directory 使用者的郵件功能。您可以擁有郵件功能的單一使用者或擁有郵件功能多位使用者使用 CSV 檔案。

## 使用命令介面啟用單一使用者的郵件功能

本範例會啟用郵件功能的使用者 Sanjay Shah。您必須提供外部電子郵件地址。

    Enable-MailUser -Identity "Sanjay Shah" -ExternalEmailAddress renev@tailspintoys.com

## 使用命令介面和 CSV 檔啟用多個使用者的郵件功能

當您所郵件-啟用大量的使用者，您先匯出使用者未啟用郵件功能為 CSV （逗點分隔值） 檔案，並使用 \[記事本\] 之類的文字編輯器或例如 Microsoft Excel 試算表應用程式再新增至 CSV 檔案的外部電子郵件地址清單。然後您可以使用更新的 CSV 檔案中的命令介面命令來 CSV 檔案中所列的使用者啟用郵件功能。

1.  執行下列命令，將未啟用郵件功能且在您組織中沒有信箱的現有使用者清單匯出到管理員桌面上名為 UsersToMailEnable.csv 的檔案。
    
        Get-User | Where { $_.RecipientType -eq "User" } | Out-File "C:\Users\Administrator\Desktop\UsersToMailEnable.csv"
    
    產生的檔案類似下列檔案。
    
        Name            RecipientType
        ----            -------------
        Guest           User
        krbtgt          User
        RMS_SERVICE     User
        David Pelton    User
        Kim Akers       User
        Janet Schorr    User
        Jeffrey Zang    User
        Spencer Low     User
        Toni Poe        User
        ...

2.  對 CSV 檔進行下列變更：
    
      - 刪除任何您不想從 CSV 檔案的擁有郵件功能的使用者。例如，您會刪除前一個範例中的前三個項目因為它們是預設的系統帳戶。
    
      - 刪除 **RecipientType** 欄和所有 `User` 執行個體。
    
      - 新增名為**EmailAddress**欄標題，並再檔案中新增的每位使用者的電子郵件地址。必須以逗號分隔的名稱和每個使用者的外部電子郵件地址。
    
    更新的 CSV 檔應該類似下列檔案。
    
        Name,EmailAddress
        David Pelton,davidp@contoso.com
        Kim Akers,kakers@tailspintoys.com
        Janet Schorr,janet.schorr@adatum.com
        Jeffrey Zang,jzang@tailspintoys.com
        Spencer Low,spencerl@fouthcoffee.com
        Toni Poe,tonip@contoso.com
        ...

3.  執行下列命令，以使用 CSV 檔中的資料啟用檔案中所列使用者的郵件功能。
    
        Import-CSV "C:\Users\Administrator\Desktop\UsersToMailEnable.csv" | ForEach-Object {Enable-MailUser -Identity $_.Name -ExternalEmailAddress $_.EmailAddress}
    
    命令結果會顯示啟用郵件功能之新使用者的相關資訊。

## 如何才能了解這是否正常運作？

若要確認是否已成功啟用 Active Directory 使用者的郵件功能，請執行下列其中一項操作：

  - 在 EAC 中，瀏覽至 \[**收件者**\>**連絡人**。新的郵件使用者會顯示在連絡人清單中。\[**連絡人類型**\] 下方類型是**郵件使用者**。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您可能需要按一下 [重新整理]<img src="images/Dn624163.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif" title="重新整理圖示" alt="重新整理圖示" /> 以顯示新郵件使用者。</td>
    </tr>
    </tbody>
    </table>


  - 在命令介面中，執行下列命令以顯示新郵件使用者的相關資訊。
    
        Get-MailUser | Format-Table Name,RecipientTypeDetails,ExternalEmailAddress

