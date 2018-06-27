---
title: '管理郵件使用者: Exchange Online Help'
TOCTitle: 管理郵件使用者
ms:assetid: bb8b8804-f730-4ad7-9173-896a4965b90f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124381(v=EXCHG.150)
ms:contentKeyID: 50472419
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.NewMailUserWizardForm.NewMailUserIntroductionWizardPage
ms.translationtype: MT
---

# 管理郵件使用者

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

郵件使用者類似於郵件連絡人。 這兩者都擁有外部電子郵件地址，也都包含 Exchange 或 Exchange Online 組織外的人員相關資訊，而這些資訊都可顯示在共用通訊錄和其他通訊清單中。 不過，和郵件連絡人不同的是，郵件使用者在您的 Exchange 或 Office 365 組織中具有登入認證，並且可以存取資源。 如需詳細資訊，請參閱 [收件者](recipients-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 2 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md) 主題中的「收件者佈建權限」一節。

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

## 建立郵件使用者

## 使用 EAC 建立郵件使用者

1.  在 EAC 中，瀏覽至 **\[收件者\]** \> **\[連絡人\]** \> **\[新增\]** \> **\[郵件使用者\]**。

2.  在 \[新增郵件使用者\] 頁面的 \[\* 別名\] 方塊中，輸入郵件使用者的別名。 別名不得超過 64 個字元，且必須在樹系中是唯一的。 這是必填的方塊。

3.  執行下列其中一項操作，指定郵件使用者的電子郵件地址類型：
    
      - 若要指定郵件使用者外部電子郵件地址的 SMTP 電子郵件地址，請按一下 \[SMTP\]。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Exchange 會驗證 SMTP 位址以確定格式正確。 如果您輸入的資料與 SMTP 格式不相符，在您按一下 [儲存] 建立郵件使用者時便會顯示錯誤訊息。</td>
        </tr>
        </tbody>
        </table>
    
      - 若要指定自訂地址類型，請按一下選項按鈕，然後輸入自訂地址類型。 例如，您可以指定 X.500、GroupWise 或 Lotus Notes 地址。

4.  在 \[\* 外部電子郵件地址\] 方塊中，輸入郵件使用者的外部電子郵件地址。 傳送給此郵件使用者的電子郵件會轉送到這個電子郵件地址。 這是必填的方塊。

5.  
    
    選取下列其中一個選項：
    
      - **現有的使用者**   選取以啟用現有使用者的郵件功能。
        
        按一下 \[瀏覽\] 以開啟 \[選取使用者 – 整個樹系\] 對話方塊。 這個對話方塊會列出組織中不具郵件功能或不具信箱的使用者帳戶。 選取您要啟用郵件的使用者帳戶，然後按一下 \[確定\]。 如果選取此選項，則不需要提供使用者帳戶資訊，因為 Active Directory 已經存在這些資訊。
    
      - **新增使用者**   選取即可建立 Active Directory 中的新使用者帳戶，以及擁有郵件功能的使用者。 如果選取此選項，必須提供所需的使用者帳戶資訊。

6.  
    
    如果您在步驟 5 中選取 \[新增使用者\]，請在 \[新增郵件使用者\] 頁面上完成下列方塊。 否則請跳到步驟 7。
    
      - **名字**   使用此方塊輸入郵件使用者的名字。
    
      - **縮寫**   使用此方塊輸入郵件使用者的縮寫。
    
      - **姓氏**   使用此方塊輸入郵件使用者的姓氏。
    
      - \[\* 名稱\]   使用這個方塊輸入使用者的顯示名稱。 這是 EAC 的連絡人清單和您組織的通訊錄中列出的名稱。 依預設，此方塊中會填入您在 \[名字\]、\[縮寫\] 和 \[姓氏\] 方塊中輸入的名稱。 如果您未使用這些方塊，仍必須在這個方塊中輸入名稱，因為這是必填的方塊。 名稱不可超過 64 個字元。
    
      - \[\* 名稱\]   使用此方塊輸入郵件使用者的名稱。 這是列在目錄服務中的名稱。 這個方塊中也會填入您在 \[名字\]、\[縮寫\]和 \[姓氏\] 方塊中輸入的名稱。 如果您未使用這些方塊，仍必須輸入名稱，因為這是必填的方塊。 這個名稱也不可超過 64 個字元。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>只有在 Exchange Server 2013 中才有 <strong>[名稱]</strong> 方塊。 在 Exchange Online 中沒有。</td>
        </tr>
        </tbody>
        </table>
    
      - \[組織單位\]   您可選取預設值以外但在收件者範圍中的組織單位 (OU)。 如果將收件者範圍設定為樹系，則預設值會設定為執行 EAC 的電腦所在之網域中的使用者容器。 若收件者範圍設為特定網域，則依預設會選取該網域的使用者容器。 若收件者範圍設為特定 OU，則依預設會選取該 OU。
        
        若要選取不同的 OU，請按一下 \[瀏覽\]。 此對話方塊會顯示樹系中在指定範圍內的所有 OU。 選取想要的 OU，然後按一下 \[確定\]。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>只有在 Exchange Server 2013 中才有 <strong>[組織單位]</strong> 方塊。 在 Exchange Online 中沒有。</td>
        </tr>
        </tbody>
        </table>
    
      - \[\* 使用者登入名稱\]   使用此方塊輸入郵件使用者用來登入網域的名稱。 使用者登入名稱包含 (@) 符號左側的使用者名稱以及右側的尾碼。 一般來說，尾碼是使用者帳戶所在的網域名稱。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>在 Exchange Online 中，此方塊會標名為 <strong>[使用者識別碼]</strong>。</td>
        </tr>
        </tbody>
        </table>
    
      - \[\* 新密碼\]   使用此方塊輸入郵件使用者必須用來登入網域的密碼。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>請確定您提供的密碼符合您要在其中建立使用者帳戶之網域的密碼長度、複雜性和歷程記錄需求。</td>
        </tr>
        </tbody>
        </table>
    
      - \[\* 確認密碼\]   使用這個方塊確認您在 \[密碼\] 方塊中輸入的密碼。
    
      - \[下次登入時必須變更密碼\]   如果您希望郵件使用者在初次登入網域時重設密碼，請選取這個核取方塊。
        
        如果您選取此核取方塊，新的郵件使用者第一次登入時，就會出現一個提示變更密碼的對話方塊。 順利變更密碼後，郵件使用者才能執行任何工作。

7.  
    
    完成作業後，按一下 \[儲存\] 建立郵件使用者。

## 使用命令介面建立郵件使用者

此範例會在 Exchange Server 2013 中為 Jeffrey Zeng 建立具有郵件功能的使用者帳戶，詳細資料如下：

  - 名稱和顯示名稱為 Jeffrey Zeng。

  - 別名為 jeffreyz。

  - 外部電子郵件地址為 jzeng@tailspintoys.com。

  - 名字為 Jeffrey，姓氏為 Zeng。

  - 登入名稱為 jeffreyz@contoso.com。

  - 密碼為 Pa$$word1。

  - 郵件使用者將在預設的 OU 中建立。 若要指定其他的 OU，請使用 *OrganizationalUnit* 參數。

<!-- end list -->

    New-MailUser -Name "Jeffrey Zeng" -Alias jeffreyz -ExternalEmailAddress jzeng@tailspintoys.com -FirstName Jeffrey -LastName Zeng -UserPrincipalName jeffreyz@contoso.com -Password (ConvertTo-SecureString -String 'Pa$$word1' -AsPlainText -Force)

此範例會在 Exchange Online 中為 Rene Valdes 建立具有郵件功能的使用者帳戶。

    New-MailUser -Name "Rene Valdes" -Alias renev -ExternalEmailAddress renevaldes@fineartschool.edu -FirstName Rene -LastName Valdes -MicrosoftOnlineServicesID renev@contoso.com -Password (ConvertTo-SecureString -String 'P@ssw0rd' -AsPlainText -Force)

## 如何才能了解這是否正常運作？

若要確認是否已成功建立郵件使用者，請執行下列其中一項操作：

  - 在 EAC 中，瀏覽至 \[收件者\] \> \[連絡人\]。 新的郵件使用者會顯示在連絡人清單中。 在 \[連絡人類型\] 下，類型為**郵件使用者**。

  - 在命令介面中，執行下列命令以顯示新郵件使用者的相關資訊。
    
        Get-MailUser <Name> | FL Name,RecipientTypeDetails,ExternalEmailAddress

## 變更郵件使用者內容

在您建立郵件使用者之後，可以使用 EAC 或命令介面進行變更並設定其他內容。

可同時間變更多個使用者信箱的內容。 如需詳細資訊，請參閱 Bulk edit mail users。

完成這項工作的預估時間隨著要檢視或變更的內容數目而不同。

## 使用 EAC 變更使用者信箱內容

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[連絡人\]。

2.  在連絡人清單中，按一下要變更其內容的郵件使用者，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在郵件使用者內容頁面上，按一下下列其中一個區段以檢視或變更內容。
    
      - General
    
      - Contact Information
    
      - Organization
    
      - Email Addresses
    
      - Mail Flow Settings
    
      - Member Of
    
      - MailTip

## 一般

使用 \[一般\] 區段可檢視或變更郵件使用者的基本資訊。

  - \[名字\]、\[縮寫\]、\[姓氏\]

  - \[\* 名稱\]   這是列於 Active Directory 中的名稱。 如果您變更這個名稱，這個名稱不可超過 64 個字元。

  - \* \[顯示名稱\]   這個名稱會出現在組織通訊錄、電子郵件及信箱清單的 \[收件者:\] 和 \[寄件者:\] 行上，以及 EAC 的連絡人清單中。 這個顯示名稱前後不可包含空格。

  - **\* 使用者登入名稱**   這是使用者用來登入網域的名稱。 在 Exchange Online 中，這是使用者用來登入 Office 365 的使用者識別碼。

  - **在通訊清單中隱藏**   選取此核取方塊，可防止郵件使用者出現在通訊錄以及您的 Exchange 組織中定義的其他通訊清單中。 選取此核取方塊後， 使用者仍可以使用電子郵件地址傳送郵件給收件者。

  - **下次登入時必須變更密碼**   如果您希望使用者在下次登入網域時重設密碼，請選取這個核取方塊。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>在 Exchange Online 中沒有此方塊。</td>
    </tr>
    </tbody>
    </table>


按一下 \[更多選項\]，檢視或變更這些額外的內容：

  - **組織單位**   這個唯讀方塊可顯示包含信箱使用者帳戶的組織單位 (OU)。 您必須使用 Active Directory 使用者與電腦以將帳號移到不同的 OU。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>在 Exchange Online 中沒有此方塊。</td>
    </tr>
    </tbody>
    </table>


  - **自訂屬性**   此區段會顯示為郵件使用者定義的自訂屬性。 若要指定自訂屬性值，請按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。 您最多可為收件者指定 15 個自訂屬性。

## 連絡人資訊

使用\[連絡人資訊\]：這個區段可用來檢視或變更使用者的連絡人資訊。 此頁的資訊顯示於通訊錄中。 按一下\[更多選項\]以顯示其他方塊。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您可以使用 [州/省]方塊來建立動態通訊群組、電子郵件地址原則或通訊清單的收件者條件。</td>
</tr>
</tbody>
</table>


## 組織

使用 \[組織\]區段可以記錄組織中之使用者角色的詳細資訊。 這個資訊將出現在通訊錄中。 另外，您可以從 Outlook 之類的電子郵件用戶端存取的建立虛擬組織圖表。

  - **職稱**   使用這個方塊可檢視或變更收件者的職稱。

  - \[部門\]   使用這個方塊可檢視或變更使用者工作的部門。 您可以使用此方塊建立動態通訊群組、電子郵件地址原則或通訊清單的收件者條件。

  - \[公司\]   使用這個方塊可檢視或變更使用者工作的公司。 您可以使用此方塊建立動態通訊群組、電子郵件地址原則或通訊清單的收件者條件。

  - **主管**   若要新增主管，按一下 **\[瀏覽\]**。 在 \[選取管理員\] 中選取人員，然後按一下 \[確定\]。

  - \[直屬員工\]   您無法修改這個方塊。 *「直屬員工」*是向指定的主管報告的使用者。 如果您已經為使用者指定主管，此使用者在主管信箱的詳細資料中會顯示為直屬員工。 例如，Kari 負責管理 Chris 和 Kate，因此會在 Chris 和 Kate 的 \[主管\] 方塊中指定 Kari，而 Chris 和 Kate 會出現在 Kari 帳戶內容的 \[直屬員工\] 方塊中。

## 電子郵件地址

\[電子郵件地址\] 區段可用來檢視或變更與郵件使用者相關聯的電子郵件地址。 這包括郵件使用者的主要 SMTP 位址、其外部電子郵件地址，以及任何關聯的 Proxy 位址。 主要 SMTP 位址 (也稱為*預設回覆地址*) 以粗體顯示在通訊清單中，並且在 \[類型\] 欄中顯示大寫的 **SMTP** 值。 根據預設，在建立郵件使用者之後，主要 SMTP 位址和外部電子郵件地址會相同。

  - \[新增\]  按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")，可為此信箱新增新的電子郵件地址。 選取下列其中一種位址類型：
    
      - \[SMTP\]   這是預設的位址類型。 按一下此按鈕，然後在 \[\* 電子郵件地址\] 方塊中輸入新的 SMTP 位址。
    
      - \[自訂位址類型\]   按一下此按鈕，並在 \[\* 電子郵件地址\] 方塊中，輸入其中一種支援的非 SMTP 電子郵件地址類型。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>除了 X.400 位址以外，Exchange 不會驗證自訂位址的格式是否正確。 您必須確保指定的自訂位址符合該位址類型的格式需求。</td>
        </tr>
        </tbody>
        </table>


  - **設定外部電子郵件地址**   使用此方塊變更郵件使用者的外部地址。 傳送給此郵件使用者的電子郵件會轉送到這個電子郵件地址。

  - \[依照套用至此收件者的電子郵件地址原則自動更新電子郵件地址\]   選取此核取方塊，可讓收件者的電子郵件地址自動依照組織內電子郵件地址原則的變更而更新。 預設會選取此方塊。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>在 Exchange Online 中沒有此核取方塊。</td>
    </tr>
    </tbody>
    </table>


## 郵件流程設定

使用 \[郵件流程設定\] 區段可檢視或變更下列設定：

  - **郵件大小限制**   這些設定會控制郵件使用者可以傳送和接收的郵件大小。 請按一下 \[檢視詳細資料\] 來檢視和變更傳送和接收郵件的大小上限。
    
      - \[已傳送郵件\]   若要指定此使用者傳送的最大郵件容量，請選擇 \[郵件大小上限 (KB)\] 核取方塊並在方塊中輸入值。 郵件大小必須介於 0 和 2,097,151 KB 之間。 如果使用者傳送的郵件大於指定的大小，該郵件便會傳回給使用者，並說明為錯誤郵件。
    
      - \[已接收郵件\]   若要指定此使用者接收的最大郵件容量，請選擇 \[郵件大小上限 (KB)\] 核取方塊並在方塊中輸入值。郵件大小必須介於 0 和 2,097,151 KB 之間。 如果使用者收到的郵件大於指定的大小，該郵件便會退回給寄件者，並提供說明錯誤訊息。

  - **郵件傳遞限制**   這些設定會控制可以傳送電子郵件訊息給這位郵件使用者的寄件者。 請按一下 \[檢視詳細資料\] 來檢視和變更這些限制。
    
      - \[接受郵件的來源\]   使用此區段來指定誰可以傳送郵件給此位使用者。
        
          - \[所有寄件者\]   選擇此選項以指定使用者可接收來自所有寄件者的郵件。 其中同時包括 Exchange 組織和外部寄件者中的寄件者。 此為預設選取的選項。 只有在您清除 \[需要驗證所有寄件者\] 核取方塊時，這個選項才會包括外部使用者。 如果您選取此核取方塊，則來自外部使用者的郵件將遭拒。
        
          - \[僅下列清單中的寄件者\]   選擇此選項以指定使用者只可接受來自 Exchange 組織中指定之一組寄件者的郵件。按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")以顯示 \[選擇收件人\] 頁面，此頁面將顯示所有在您的 Exchange 組織中的收件人。 選取想要的收件者，然後按一下 \[確定\]。 您也可以在搜尋方塊中輸入收件者的名稱，然後按一下 \[搜尋\]![搜尋圖示](images/Dn624163.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "搜尋圖示")，就可以搜尋特定的收件者。
        
          - \[需要驗證所有寄件者\]   選取這個選項，可防止匿名使用者傳送郵件給使用者。
    
      - \[拒絕郵件的來源\]   使用此區段來指定傳送郵件給此位使用者的封鎖對象。
        
          - \[沒有寄件者\]   選擇此選項以指定信箱不會拒絕來自 Exchange 組織中任何寄件者的郵件。 此為預設選取的選項。
        
          - \[下列清單中的寄件者\]   選擇此選項以指定信箱將拒絕來自 Exchange 組織中指定之一組寄件者的郵件。按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")以顯示 \[選擇收件人\] 頁面，此頁面將顯示所有在您的 Exchange 組織中的收件人。選取想要的收件者，然後按一下 \[確定\]。 您也可以在搜尋方塊中輸入收件者的名稱，然後按一下 \[搜尋\]![搜尋圖示](images/Dn624163.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "搜尋圖示")，就可以搜尋特定的收件者。

## 成員隸屬

使用 \[成員隸屬\] 區段可檢視此使用者所屬之通訊群組或安全性群組的清單。 您不能更改此頁上的成員資訊。 請注意，使用者可能會符合組織中，一個或多個動態通訊群組的準則。 不過，動態通訊群組不會顯示在這個頁面上，因為每次使用此群組時就會計算其成員資格。

## 郵件提示

使用 \[郵件提示\] 區段加入「郵件提示」，以便在將郵件傳送給此收件者前，警示使用者潛在的問題。 「郵件提示」是在此收件者加入至新電子郵件的 \[收件者\]、\[副本\] 或 \[密件副本\] 行時，顯示在資訊列中的文字。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>「寄件提醒」可以包含 HTML 標記，但是不允許指令碼。 自訂郵件提示的長度不能超過 175 個顯示的字元。 HTML 標記則不包括在此限制內。</td>
</tr>
</tbody>
</table>


## 使用命令介面變更郵件使用者內容

郵件使用者的內容會同時儲存在 Active Directory 和 Exchange 中。 一般而言，使用 **Get-User** 和 **Set-User** 指令程式可檢視和變更組織及連絡人資訊的內容。 使用 **Get-MailUser** 和 **Set-MailUser** 指令程式可檢視或變更郵件相關內容，例如電子郵件地址、郵件提示、自訂屬性，以及郵件使用者是否在通訊清單中隱藏。

使用 **Get-MailUser** 和 **Set-MailUser** 指令程式可檢視和變更郵件使用者的內容。 如需相關資訊，請參閱下列主題：

  - [Get-User](https://technet.microsoft.com/zh-tw/library/aa996896\(v=exchg.150\))

  - [Set-User](https://technet.microsoft.com/zh-tw/library/aa998221\(v=exchg.150\))

  - [Get-MailUser](https://technet.microsoft.com/zh-tw/library/aa997254\(v=exchg.150\))

  - [Set-MailUser](https://technet.microsoft.com/zh-tw/library/aa995971\(v=exchg.150\))

以下是一些使用命令介面變更郵件使用者內容的範例。

此範例會設定 Pilar Pinilla 的外部電子郵件地址。

    Set-MailUser "Pilar Pinilla" -ExternalEmailAddress pilarp@tailspintoys.com

此範例會在組織的通訊錄中隱藏所有郵件使用者。

    Get-MailUser | Set-MailUser -HiddenFromAddressListsEnabled $true

此範例會將所有郵件使用者的 \[公司\] 內容設定為 \[Contoso\]。

    Get-User -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'mailuser')} | Set-User -Company Contoso

此範例會將 \[公司\] 內容中值為 \[Contoso\] 的所有郵件使用者的 \[CustomAttribute1\] 內容設定為 \[ContosoEmployee\] 這個值。

    Get-User -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'mailuser') -and (Company -eq 'Contoso')}| Set-MailUser -CustomAttribute1 ContosoEmployee

## 如何才能了解這是否正常運作？

若要確認是否已成功變更郵件使用者的內容，請執行下列動作：

  - 在 EAC 中，選取郵件使用者，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示") 以檢視您變更的內容。

  - 在命令介面中，使用 **Get-User** 和 **Get-MailUser** 指令程式來驗證變更。 使用命令介面的其中一項優點是，您可以檢視多個郵件連絡人的內容。
    
        Get-MailUser | Fl Name,CustomAttribute1 
    
    在上述所有郵件連絡人的 \[公司\] 內容設為 \[Contoso\] 的範例中，執行下列命令以驗證變更：
    
        Get-User -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'mailuser')} | FL Name,Company
    
    在上述所有郵件使用者的 \[CustomAttribute1\] 內容設為 \[ContosoEmployee\] 的範例中，執行下列命令以驗證變更。
    
        Get-MailUser | Fl Name,CustomAttribute1 

## 大量編輯郵件使用者

您也可以使用 EAC 變更為多位郵件使用者選取的內容。 當您從 EAC 的連絡人清單中選取兩位或多位郵件使用者時，可以大量編輯的內容就會顯示在 \[詳細資料\] 窗格中。 變更其中一項內容時，變更將套用於所有選取的收件者。

當您大量編輯郵件使用者時，可以變更下列內容範圍：

  - **連絡人資訊**   變更街道、郵遞區號和城市名稱等共用內容。

  - **組織**   變更部門名稱、公司名稱以及選取的郵件連絡人或郵件使用者直屬經理等共用內容。

## 使用 EAC 大量編輯郵件使用者

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[連絡人\]。

2.  在連絡人清單中，選取兩位或多位郵件使用者。 您無法大量編輯郵件連絡人和郵件使用者的組合。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您可以按住 Shift 鍵，並依序按一下您要編輯的第一位和最後一位郵件使用者，以選取多位相鄰的郵件使用者。 您也可以按住 Ctrl 鍵，並按一下您要編輯的每一位郵件使用者，以選取多位郵件使用者。</td>
    </tr>
    </tbody>
    </table>


3.  在 \[詳細資料\] 窗格的 \[大量編輯\] 下，按一下 \[連絡人資訊\] 或 \[組織\] 下的 \[更新\]。

4.  在內容頁上進行變更，然後儲存您的變更。

## 如何才能了解這是否正常運作？

若要確認是否已成功大量編輯郵件使用者，請執行下列其中一項操作：

  - 在 EAC 中，選取已大量編輯的每一位郵件使用者，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示") 以檢視您變更的內容。

  - 在命令介面中，使用 **Get-User** 指令程式來驗證變更。 例如，假設您使用 EAC 中的大量編輯功能，變更名為 A. Datum Corporation 的廠商公司中所有郵件使用者的管理者和辦公室。 若要確認這些變更，可以在命令介面中執行下列命令：
    
        Get-User -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'mailuser') -and (Company -eq 'Adatum')} | fl Name,Office,Manager

## 用於目錄同步作業管理 Exchange Online 中的郵件使用者

本節提供使用目錄同步處理 Exchange Online 中管理電子郵件使用者相關資訊。目錄同步處理的混合式客戶與內部部署和雲端託管信箱，且完全託管的 Exchange Online 客戶其 Active Directory 為內部部署。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您使用目錄同步作業來管理收件者，您仍可在 Office 365 系統管理中心 中新增和管理使用者，但這些使用者不會和您的內部部署 Active Directory 同步處理。這是因為目錄同步作業只會從內部部署 Active Directory 同步收件者至雲端。</td>
</tr>
</tbody>
</table>


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
<td>建議搭配下列功能一起使用目錄同步處理：
<ul>
<li><p><strong>Outlook 安全寄件和封鎖寄件者清單</strong> 時同步服務，這些清單會高於垃圾郵件篩選服務中。這可讓使用者管理自己的安全寄件和每個使用者或每個網域為基礎的封鎖寄件清單。</p></li>
<li><p><strong>目錄架構邊緣封鎖 (DBEB)</strong> 如需 DBEB 的詳細資訊，請參閱<a href="https://technet.microsoft.com/zh-tw/library/dn600322(v=exchg.150)">使用目錄架構邊緣封鎖以拒絕傳送至無效收件者的郵件</a>。</p></li>
<li><p><strong>使用者垃圾郵件隔離</strong> 才可存取使用者垃圾郵件隔離區，使用者必須具備有效的 Office 365 使用者識別碼和密碼。具有內部部署信箱的客戶必須是有效的電子郵件使用者。</p></li>
<li><p><strong>傳輸規則</strong> 當您使用目錄同步作業時，現有的 Active Directory 使用者和群組會自動上傳至雲端，及您可建立傳輸規則的目標特定使用者和/或群組而不需要以手動方式將其新增透過 EAC 或遠端 Windows PowerShell。請注意，<a href="https://go.microsoft.com/fwlink/?linkid=507569">動態通訊群組</a>無法透過目錄同步作業進行同步處理。</p></li>
</ul></td>
</tr>
</tbody>
</table>


**開始之前**

取得必要的權限並做好目錄同步處理的[準備目錄同步處理](https://go.microsoft.com/fwlink/p/?linkid=308908)所述。

同步處理使用者目錄

1.  啟動目錄同步作業[啟用目錄同步處理](https://go.microsoft.com/fwlink/p/?linkid=308909)中所述。

2.  設定目錄同步處理電腦，如[設定您的目錄同步處理電腦](http://go.microsoft.com/fwlink/p/?linkid=308911)所說明。

3.  同步處理您的目錄，如[使用設定精靈同步處理您的目錄](http://go.microsoft.com/fwlink/?linkid=308912)所說明。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>完成 Azure Active Directory 同步處理工具設定精靈 之後，您的 Active Directory 樹系中會建立 <strong>MSOL_AD_SYNC</strong> 帳戶。此帳戶將用來讀取和同步處理您的內部部署 Active Directory 資訊。為了讓目錄同步作業能夠正確運作，請確定有開啟您的本機目錄同步作業伺服器上的 TCP 443。</td>
    </tr>
    </tbody>
    </table>


4.  啟動已同步處理的使用者，如[啟用同步處理的使用者](http://go.microsoft.com/fwlink/p/?linkid=308913)所說明。

5.  管理目錄同步處理，如[管理目錄同步作業](http://go.microsoft.com/fwlink/p/?linkid=308915)所說明。

6.  請確認的 Exchange Online 已正確同步處理。在 EAC 中，移至 \[**收件者**\>**連絡人**並檢視使用者清單從內部部署環境正確同步處理。

