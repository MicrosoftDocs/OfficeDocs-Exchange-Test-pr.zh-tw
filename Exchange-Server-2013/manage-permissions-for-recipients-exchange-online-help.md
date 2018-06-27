---
title: '管理收件者的權限: Exchange Online Help'
TOCTitle: 管理收件者的權限
ms:assetid: 749cdfe3-496b-453f-96eb-20a0bf28fd52
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ919240(v=EXCHG.150)
ms:contentKeyID: 51406991
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理收件者的權限

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2018-04-20_

您可以使用 EAC 或命令介面將權限指派給使用者或群組 (名稱為*代理人*)，讓他們能從其他信箱開啟或傳送郵件。可以將權限指派給使用者信箱、連結的信箱、資源信箱以及共用信箱。您也可以將權限指派給通訊群組、動態通訊群組和擁有郵件功能的安全性群組，讓代理人能代表群組傳送郵件。您也可以將下列權限指派給代理人，以代表信箱或群組存取信箱或傳送郵件：

  - **\[完整存取\]**   此權限允許代理人開啟使用者的信箱和存取信箱內容。但是，指派 \[完整存取\] 權限，並不允許代理人從信箱傳送郵件。您必須將 \[以下列傳送\] 或 \[代理傳送者\] 權限指派給代理人，以便傳送郵件。
    
    設定群組的權限時，無法使用 \[完整存取\] 權限。

  - **\[以下列傳送\]**   此權限允許代理人使用該信箱傳送郵件。在此權限指派給代理人後，任何代理人自此信箱傳送的郵件都將顯示為由信箱擁有者傳送。但是，此權限不允許代理人登入至使用者的信箱。只允許使用者開啟信箱。如果此權限已指派給群組，則代理人所傳送的郵件會顯示為由群組傳送。

  - **\[代理傳送者\]**   此權限同時允許代理人使用此信箱傳送郵件。將此權限指派給代理人後，代理人所傳送郵件中的 **\[寄件者\]** 地址指出郵件是由代理人代表信箱擁有者傳送。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您指派完整存取]、 傳送者] 或 [傳送代理者] 權限以存取地址清單隱藏的信箱] 代理人將無法開啟信箱或傳送的郵件。</td>
</tr>
</tbody>
</table>


## 開始之前有哪些須知？

  - 每項程序的預估完成時間：2 分鐘。

  - 本主題中的程序需要特定權限。請查看每個程序以取得權限資訊。

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

## 指派權限給信箱

如先前所述，您可以將代理人權限指派給使用者信箱、連結的信箱、資源信箱以及共用信箱。您也可以使用命令介面，將用以存取探索信箱的權限指派給代理人。

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中「收件者佈建權限」一節的「權限和委派」項目。

## 使用 EAC 指派權限

下列程序說明如何將權限指派給使用者信箱。您可以遵循類似程序，瀏覽至 EAC 中的 **\[資源\]** 或 **\[共用\]** 頁面並選取要被指派權限的信箱，以將權限指派給資源或共用信箱。

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[信箱\]。

2.  在信箱清單中，按一下您想指派權限的信箱，然後按 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在信箱內容頁面上，按一下 **\[信箱委派\]**。

4.  若要指派權限給代理人，請按一下適當權限下方的 **\[新增\]**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")，即會顯示一個頁面，其中列出 Exchange 組織中可指派權限的所有收件者。選取想要的收件者，然後按一下 \[確定\]。您也可以在搜尋方塊中輸入收件者的名稱，然後按一下 \[搜尋\]![搜尋圖示](images/Dn624163.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "搜尋圖示")，就可以搜尋特定的收件者。
    
    若要移除收件者的權限，請在適當的權限之下，選取收件者，然後按一下 **\[移除\]**![\[移除\] 圖示](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[移除] 圖示")。

5.  按一下 **\[儲存\]** 以儲存變更。

## 使用 EAC 大量指派權限

使用下列步驟以大量指派權限。

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[信箱\]。

2.  選取想要指派的權限的信箱。

3.  按一下或點選 \[**更多選項\]**在右窗格的 \[**信箱委派\]**下選擇，**新增\]**。

4.  在 \[**大量新增委派**\] 頁面上按一下或點選**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")底下顯示列出您可以將指派權限的 Exchange 組織中的所有收件者\] 頁面上的適當權限。選取您想要的收件者、 將其新增至清單，然後按一下 \[**確定\]**。
    
    若要移除收件者\] 適當的權限\] 下的權限選取 \[收件者和 \[**移除**![\[移除\] 圖示](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[移除] 圖示")。

## 使用 EAC 來將利用其他使用者的信箱傳送電子郵件的權限指派給使用者

下列程序將示範如何將利用其他使用者的信箱傳送電子郵件的權限指派給使用者。

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[信箱\]。

2.  在信箱清單中，按一下您要對其指派 \[以下列傳送\] 權限的信箱，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在信箱內容頁面上，按一下 **\[信箱委派\]**。

4.  若要指派權限給代理人，請在 \[以下列傳送 \] 或 \[代理傳送者\] 下方，按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")，即會顯示一個頁面，列出 Exchange 組織中可作為權限指派目標的所有收件者。選取想要的收件者，然後按一下 \[確定\]。您也可以在搜尋方塊中輸入收件者的名稱，然後按一下 \[搜尋\]![搜尋圖示](images/Dn624163.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "搜尋圖示")，就可以搜尋特定的收件者。
    
    \[以下列傳送 \] 權限可讓代理人利用此信箱傳送電子郵件。
    
    \[代理傳送者\] 權限可讓代理人代表此信箱傳送電子郵件。由代理人所傳送之任何郵件的 \[寄件人\] 行會指出郵件是由代理人代表信箱擁有者所傳送。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果使用者也要能夠開啟並檢視該信箱的內容，您還必須對使用者指派 [完整存取] 權限。</td>
    </tr>
    </tbody>
    </table>


5.  按一下 **\[儲存\]** 以儲存變更。

## 使用 EAC 來將利用群組傳送電子郵件的權限指派給使用者

下列程序將示範如何將利用群組傳送電子郵件的權限指派給使用者。

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[群組\]。

2.  在群組清單中，按一下您要對其指派 \[以下列傳送 \] 權限的群組，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在群組內容頁面上，按一下 **\[群組委派\]**。

4.  若要指派權限給代理人，請在 \[以下列傳送 \] 或 \[代理傳送者\] 下方，按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")，即會顯示一個頁面，列出 Exchange 組織中可作為權限指派目標的所有收件者。選取想要的收件者，然後按一下 \[確定\]。您也可以在搜尋方塊中輸入收件者的名稱，然後按一下 \[搜尋\]![搜尋圖示](images/Dn624163.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "搜尋圖示")，就可以搜尋特定的收件者。
    
    \[以下列傳送\] 權限可讓代理人利用此群組傳送電子郵件。
    
    \[代理傳送者\] 權限可讓代理人代表此群組傳送電子郵件。由代理人所傳送之任何郵件的 \[寄件人\] 行會指出郵件是由代理人代表群組所傳送。

5.  按一下 **\[儲存\]** 以儲存變更。

## 使用 EAC 來指派完整存取權限

下列程序將示範如何對使用者信箱指派完整存取權限。

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[信箱\]。

2.  在信箱清單中，按一下您要對其指派完整存取權限的信箱，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在信箱內容頁面上，按一下 **\[信箱委派\]**。

4.  若要指派權限給代理人，請在 \[完整存取\] 下方，按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")，即會顯示一個頁面，列出 Exchange 組織中可作為權限指派目標的所有收件者。選取想要的收件者，然後按一下 \[確定\]。您也可以在搜尋方塊中輸入收件者的名稱，然後按一下 \[搜尋\]![搜尋圖示](images/Dn624163.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "搜尋圖示")，就可以搜尋特定的收件者。
    
    \[完整存取\] 權限可讓代理人開啟使用者的信箱，並存取信箱的內容。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>指派 [完整存取] 權限並不允許代理人利用此信箱傳送郵件。您必須將 [以下列傳送] 或 [代理傳送者] 權限指派給代理人，以便傳送郵件。</td>
    </tr>
    </tbody>
    </table>


5.  按一下 **\[儲存\]** 以儲存變更。

## 使用命令介面指派權限

下列各節說明如何使用命令介面來管理信箱的 \[完整存取\]、\[以下列傳送\] 或 \[代理傳送者\] 權限。

## 管理完整存取權限

下列範例說明如何使用 **Add-MailboxPermission** 和 **Remove-MailboxPermission** 指令程式來管理完整存取權限。

此範例將 Terry Adams 的信箱完整存取權限指派給代理人 Raymond Sam。

    Add-MailboxPermission -Identity "Terry Adams" -User raymonds -AccessRights FullAccess -InheritanceType all

此範例將組織的預設探索搜尋信箱的完整存取權限指派給 Esther Valle。

    Add-MailboxPermission -Identity "DiscoverySearchMailbox{D919BA05-46A6-415f-80AD-7E09334BB852}" -User estherv -AccessRights FullAccess -InheritanceType all

此範例將 \[服務台票證\] 共用信箱的完整存取權限指派給服務台通訊群組的成員。

    Add-MailboxPermission "HelpdeskTickets" -User helpdesk -AccessRights FullAccess -InheritanceType all

此範例移除 Jim Hance 對於 Ayla Kol 信箱的完整存取權限。

    Remove-MailboxPermission -Identity ayla -User "Jim Hance" -AccessRights FullAccess -Inheritance

如需詳細的語法及參數資訊，請參閱下列主題：

  - [Add-MailboxPermission](https://technet.microsoft.com/zh-tw/library/bb124097\(v=exchg.150\))

  - [Remove-MailboxPermission](https://technet.microsoft.com/zh-tw/library/bb125153\(v=exchg.150\))

## 管理「以下列傳送」權限

下列範例說明如何在 Exchange Server 2013 和 Exchange Online 中管理 \[以下列傳送\] 權限。在 Exchange 2013 中，您必須使用 **Add-ADPermission** 和 **Remove-ADPermission** 指令程式；在 Exchange Online 中，您必須使用 **Add-RecipientPermission** 和 **Remove-RecipientPermission** 指令程式。在這兩個情況中，您可使用 *Identity* 參數來指定應新增或移除 \[以下列傳送\] 權限的信箱名稱，以及使用 *User* 或 *Trustee* 參數來指定將指派或取消指派 \[以下列傳送\] 權限的代理人 (例如使用者或群組)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用 <strong>Get-Recipient</strong> 指令程式以擷取信箱和代理人的 <em>Name</em> 內容。使用這些值來指派 [以下列傳送] 權限。</td>
</tr>
</tbody>
</table>


## Exchange Server 2013

此範例將 \[以下列傳送\] 權限指派給 Helpdesk Support Team 共用信箱上的 Helpdesk 群組。

    Add-ADPermission -Identity helpdesksupport -User helpdeskgroup -ExtendedRights "Send As"

此範例移除使用者 Pilar Pinilla 對於 James Alvord 信箱的 \[以下列傳送\] 權限。

    Remove-ADPermission -Identity "James Alvord" -User pilarp -ExtendedRights "Send As"

如需詳細的語法及參數資訊，請參閱：

  - [Add-ADPermission](https://technet.microsoft.com/zh-tw/library/bb124403\(v=exchg.150\))

  - [Remove-ADPermission](https://technet.microsoft.com/zh-tw/library/aa996048\(v=exchg.150\))

## Exchange Online

此範例將 \[以下列傳送\] 權限指派給 Contoso Printer Support 共用信箱上的 Printer Support 群組。

    Add-RecipientPermission -Identity "Contoso Printer Support" -Trustee "Printer Support" -AccessRights SendAs

此範例移除使用者 Karen Toh 對於 Yan Li 信箱的 \[以下列傳送\] 權限。

    Remove-RecipientPermission -Identity "Yan Li" -Trustee "Karen Toh" -ExtendedRights SendAs

如需詳細的語法及參數資訊，請參閱：

  - [Add-RecipientPermission](https://technet.microsoft.com/zh-tw/library/ff935839\(v=exchg.150\))

  - [Remove-RecipientPermission](https://technet.microsoft.com/zh-tw/library/ff945794\(v=exchg.150\))

## 管理「代理傳送者」權限

下列範例說明如何使用 **Set-Mailbox** 指令程式來管理 \[代理傳送者\] 權限。

此範例將 Sean Chai 信箱的 \[代理傳送者\] 權限指派給代理人 Holly Holt。

    Set-Mailbox -Identity seanc@contoso.com -GrantSendOnBehalfTo hollyh

此範例移除 Contoso Executives 共用信箱上已指派給 Temporary Executive Assistants 群組的 \[代理傳送者\] 權限。

    Set-Mailbox "Contoso Executives" -GrantSendOnBehalfTo @{remove="tempassistants@contoso.com"}

如需詳細的語法及參數資訊，請參閱 [Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\))。

## 如何知道這是否正常運作？

若要驗證您是否已成功將權限指派給信箱或共用信箱，請執行下列其中一項操作：

  - 在 EAC 中：
    
    1.  瀏覽至 **\[收件者\]** \> **\[新增\]** 或 **\[共用\]**，按一下信箱，然後按 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。
    
    2.  在信箱內容頁面上，按一下 **\[信箱委派\]**。
    
    3.  如果您已指派權限給收件者，請驗證使用者或群組是否列在適當的權限之下。如果您已移除權限，請確認收件者未列在適當的權限之下。

或

  - 在命令介面中，根據您管理的權限而定，執行下列其中一個命令。
    
      - **完整存取權**
        
            Get-MailboxPermission -Identity <mailbox>
        
        若要驗證特定代理人是否被指派信箱的 \[完整存取\] 權限，請執行下列命令。
        
            Get-MailboxPermission -Identity <mailbox> -User <delegate>
    
      - **以下列傳送**
        
        在 Exchange Server 2013 中，執行下列命令。
        
            Get-ADPermission -Identity <name of mailbox> -User <delegate>
        
        在 Exchange Online 中，執行下列命令。
        
            Get-RecipientPermission -Identity <mailbox> -Trustee <delegate>
    
      - **代理傳送者**
        
            Get-Mailbox -Identity <mailbox> | FL GrantSendOnBehalfTo

## 指派權限給群組

如先前所述，您可以將 \[以下列傳送\] 和 \[代理傳送者\] 權限指派給通訊群組、動態通訊群組和擁有郵件功能的安全性群組，讓代理人能代表或代理群組傳送郵件。

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中「收件者佈建權限」一節的「通訊群組」和「動態通訊群組」項目。

## 使用 EAC 指派權限

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[群組\]。

2.  在群組清單中，按一下您想指派權限的群組，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在群組內容頁面上，按一下 **\[群組委派\]**。

4.  若要指派權限給代理人，請按一下適當權限下方的 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")，即會顯示一個頁面，其中會顯示一份 Exchange 組織中可指派權限的所有收件者清單。選取想要的收件者，然後按一下 \[確定\]。您也可以在搜尋方塊中輸入收件者的名稱，然後按一下 \[搜尋\]![搜尋圖示](images/Dn624163.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "搜尋圖示")，就可以搜尋特定的收件者。
    
    若要移除收件者的權限，請在適當的權限之下，選取收件者，然後按一下 **\[移除\]**![\[移除\] 圖示](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[移除] 圖示")。

5.  按一下 **\[儲存\]** 以儲存變更。

## 使用命令介面指派權限

下列各節說明如何使用命令介面來管理群組的 \[以下列傳送\] 和 \[代理傳送者\] 權限。

## 管理「以下列傳送」權限

下列範例說明如何在 Exchange Server 2013 和 Exchange Online 中管理群組的 \[以下列傳送\] 權限。在 Exchange 2013 中，您必須使用 **Add-ADPermission** and **Remove-ADPermission** 指令程式。在 Exchange Online 中，您必須使用 **Add-RecipientPermission** 和 **Remove-RecipientPermission** 指令程式。在這兩個情況中，您可使用 *Identity* 參數來指定應新增或移除 \[以下列傳送\] 權限的群組名稱，以及使用 *User* 或 *Trustee* 參數來指定將指派或取消指派 \[以下列傳送\] 權限的代理人 (例如使用者或群組)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用 <strong>Get-Recipient</strong> 指令程式擷取群組和代理人的 <em>Name</em> 內容。使用這些值來指派 [以下列傳送] 權限。</td>
</tr>
</tbody>
</table>


## Exchange Server 2013

此範例將 \[以下列傳送\] 權限指派給 Contoso Sales Info 群組的 Sales Admins 群組。這樣可讓銷售管理群組的成員代表 Contoso Sales Information 群組傳送郵件。

    Add-ADPermission -Identity "Contoso Sales Info" -User "Sales Admins" -ExtendedRights "Send As"

此範例移除使用者 Alan Shen 對於 Corporate IT Admins 群組的 \[以下列傳送\] 權限。

    Remove-ADPermission -Identity "Corporate IT Admins" -User contoso\alans -ExtendedRights "Send As"

如需詳細的語法及參數資訊，請參閱：

  - [Add-ADPermission](https://technet.microsoft.com/zh-tw/library/bb124403\(v=exchg.150\))

  - [Remove-ADPermission](https://technet.microsoft.com/zh-tw/library/aa996048\(v=exchg.150\))

## Exchange Online

此範例將 \[以下列傳送\] 權限指派給 Emergency Broadcast Messages 動態通訊群組的 Contoso Admins 群組。

    Add-RecipientPermission -Identity emergencybroadcast@contoso.com -Trustee "Contoso Admins" -AccessRights SendAs

此範例移除使用者 Walter Harp 對於 Printer Resources 安全性群組的 \[以下列傳送\] 權限。

    Remove-RecipientPermission -Identity "Printer Resources" -Trustee walterh@contoso.com ExtendedRights SendAs

如需詳細的語法及參數資訊，請參閱：

  - [Add-RecipientPermission](https://technet.microsoft.com/zh-tw/library/ff935839\(v=exchg.150\))

  - [Remove-RecipientPermission](https://technet.microsoft.com/zh-tw/library/ff945794\(v=exchg.150\))

## 管理「代理傳送者」權限

下列範例說明如何使用 **Set-DistributionGroup** 和 **Set-DynamicDistributionGroup** 指令程式來管理群組的 \[代理傳送者\] 權限。

此範例將 \[印表機支援\] 通訊群組的 \[代理傳送者\] 權限指派給代理人 Sara Davis。

    Set-DistributionGroup -Identity printersupport@contoso.com -GrantSendOnBehalfTo sarad

此範例將 \[所有員工\] 通訊群組的 \[代理傳送者\] 權限指派給代理人 Administrator。

    Set-DynamicDistributionGroup -Identity "All Employees" -GrantSendOnBehalfTo administrator

此範例移除 \[所有員工\] 動態通訊群組上已指派給 \[系統管理員的 \[代理傳送者\] 權限。

    Set-DynamicDistributionGroup "All Employees" -GrantSendOnBehalfTo @{remove="administrator"}

如需詳細的語法及參數資訊，請參閱：

  - [Set-DistributionGroup](https://technet.microsoft.com/zh-tw/library/bb124955\(v=exchg.150\))

  - [Set-DynamicDistributionGroup](https://technet.microsoft.com/zh-tw/library/bb123796\(v=exchg.150\))

## 如何知道這是否正常運作？

若要驗證是否成功指派權限給群組，請執行以下其中一個操作：

  - 在 EAC 中：
    
    1.  瀏覽至 **\[收件者\]** \> **\[群組\]**，按一下群組，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。
    
    2.  在群組內容頁面上，按一下 **\[群組委派\]**。
    
    3.  如果您已指派權限給收件者，請驗證使用者或群組是否列在適當的權限之下。如果您已移除權限，請確認收件者未列在適當的權限之下。

或

  - 在命令介面中，根據您管理的權限而定，執行下列其中一個命令。
    
      - **以下列傳送**
        
        在 Exchange Server 2013 中，執行下列命令。
        
            Get-ADPermission -Identity <name of group> -User <delegate>
        
        在 Exchange Online 中，執行下列命令。
        
            Get-RecipientPermission -Identity <group> -Trustee <delegate>
    
      - **代理傳送者**
        
            Get-DistributionGroup -Identity <group> | FL GrantSendOnBehalfTo
        
        或
        
            Get-DynamicDistributionGroup -Identity <group> | FL GrantSendOnBehalfTo

