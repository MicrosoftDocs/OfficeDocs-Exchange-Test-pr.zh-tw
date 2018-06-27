---
title: '管理擁有郵件功能的安全性群組: Exchange Online Help'
TOCTitle: 管理擁有郵件功能的安全性群組
ms:assetid: 80b3b537-4786-4d02-9202-44e373811a25
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb123521(v=EXCHG.150)
ms:contentKeyID: 50472348
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理擁有郵件功能的安全性群組

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2017-10-04_

擁有郵件功能的安全性群組可用來發佈，以及郵件來授與存取權限給Active Directory中的資源。如需詳細資訊，請參閱[收件者](recipients-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：2 至 5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「通訊群組」項目。

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

## 建立啟用郵件功能的安全性群組

## 使用 EAC 建立安全性群組

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[群組\]。

2.  按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示") \> \[安全性群組\]。

3.  在 \[新增安全性群組\] 頁面上，完成下列欄位：
    
      - **\* 顯示名稱**  使用此方塊可輸入顯示名稱。此名稱會出現在共用的通訊錄，在 \[收件者： 電子郵件傳送到此群組中，並在 EAC 中的 \[群組\] 清單時的直線。顯示名稱為必要與讓人員辨識功能應易記。它也必須是唯一的樹系中。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>如果已套用群組命名原則，您必須依照您的組織強制執行的命名限制。如需詳細資訊，請參閱<a href="create-a-distribution-group-naming-policy-exchange-2013-help.md">建立通訊群組命名原則</a>。如果您想要覆寫您的組織群組命名原則，請參閱<a href="override-the-distribution-group-naming-policy-exchange-2013-help.md">通訊群組命名原則會覆寫</a>。</td>
        </tr>
        </tbody>
        </table>
    
      - **\* 別名**  使用此方塊可輸入 \[安全性\] 群組的別名。別名不可超過 64 個字元和必須是唯一的樹系中。當使用者輸入上 \[收件者的別名： 行的電子郵件訊息，則解析為群組的顯示名稱。
    
      - \[描述\]   這個方塊可用來描述群組，讓人員了解安全性群組的用途。
    
      - \[組織單位\]   您可選取預設值以外但在收件者範圍中的組織單位 (OU)。如果將收件者範圍設定為樹系，則預設值會設定為正在執行 EAC 的電腦包含在內的 Active Directory 網域中出現的 \[使用者\] 容器。若收件者範圍設為特定網域，則依預設會選取該網域的使用者容器。若收件者範圍設為特定 OU，則依預設會選取該 OU。
        
        若要選取不同的 OU，請按一下 \[瀏覽\]。此對話方塊會顯示樹系中在指定範圍內的所有 OU。選取所需的 OU，然後按一下 \[確定\]。
    
      - **\* 擁有者**  根據預設，會建立一組人員是擁有者。所有群組都必須至少一個擁有者。您可以依序按一下 \[**新增\]**新增擁有者。
    
      - \[成員\]：使用此區段來新增成員並可指定使用者在加入或離開群組時是否需要經過核准。
        
        群組擁有者不必是群組的成員。使用 \[新增群組擁有者為成員\]可以將擁有者新增為成員，或移除其成員資格。
        
        若要將成員新增至群組中，按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。完成新增成員已，請按一下**\[確定\]**回到 \[**新的安全性群組**\] 頁面上。
        
        如果您要群組擁有者收到使用者的加入群組請求，請選取 \[需要擁有者核准\] 核取方塊。如果您選擇了此選項，則只有群組擁有者可以移除成員。

4.  完成作業後，按一下 \[儲存\] 建立安全性群組。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>根據預設，所有新郵件功能的安全性群組需要驗證所有寄件者。這可防止外部寄件者傳送郵件給擁有郵件功能的安全性群組。若要設定為接受來自所有寄件者的郵件擁有郵件功能的安全群組，您必須修改該群組的郵件傳遞限制設定。</td>
</tr>
</tbody>
</table>


## 使用命令介面建立安全性群組

此範例會建立名為 File Server Managers 且別名為 fsadmin 的安全性群組。該安全性建立於預設 OU 中，且任何人受群組擁有者核准都能加入此群組。

    New-DistributionGroup -Name "File Server Managers" -Alias fsadmin -Type security

如需更多有關使用命令介面來建立已啟用郵件功能的安全性群組資訊，請參閱[New-DistributionGroup](https://technet.microsoft.com/zh-tw/library/aa998856\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要驗證是否成功建立已啟用郵件功能的安全性群組，請執行以下其中一個操作：

  - 在 EAC 中，瀏覽至 \[**收件者**\>**群組**。新擁有郵件功能的安全性群組會顯示在 \[群組\] 清單中。\[**群組類型**\] 下方的類型為**安全性群組**。

  - 在命令介面中，執行以下命令以顯示已啟用郵件功能的新安全性群組資訊。
    
        Get-DistributionGroup <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress

## 變更已啟用郵件功能的安全性群組內容

## 使用 EAC 變更已啟用郵件功能的安全性群組內容

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[群組\]。

2.  在群組清單中，按一下您希望檢視或變更的安全性群組，接著按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在群組屬性頁面上，按一下下列區段其中之一以檢視或變更屬性。
    
      - General
    
      - Ownership
    
      - Membership
    
      - Membership approval
    
      - Delivery management
    
      - Message approval
    
      - Email options
    
      - MailTip
    
      - Group delegation

## 一般

這個區段可用來檢視或變更群組的基本資訊。

  - **\* 顯示名稱**：這個名稱會出現在通訊錄的 \[收件者:\] 中：行以及 \[群組\] 清單中 (當電子郵件傳送至此群組時)。顯示名稱為必要項目，應以好記易懂為原則，以便他人分辨群組的用途。這個名稱在您的網域中也必須是唯一的。

  - \[\* 別名\]  此為電子郵件地址中顯示於 @ 符號左側的部分。變更別名時，群組的主要 SMTP 位址也會變更，並會包含新的別名。此外，使用之前別名的電子郵件地址仍會保留為群組的主要 Proxy 位址。

  - \[描述\]  這個方塊可用來描述群組，讓人員了解群組的用途。此描述會顯示在通訊錄和 EAC 的 \[詳細資料\] 窗格中。

  - **隱藏此群組的通訊清單**  如果您不想使用者看到此群組在通訊錄中的，選取此核取方塊。在 \[收件者輸入群組的別名或電子郵件地址如果選取這個核取方塊已寄件者:\] 或 \[副本： 字行，以將郵件傳送至群組。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您可以考慮隱藏安全性群組，因為它們通常是用來指派權限給群組成員，而非傳送電子郵件。</td>
    </tr>
    </tbody>
    </table>


  - **組織單位**  此唯讀方塊顯示包含安全性群組組織單位 (OU)。您必須使用 Active Directory 使用者和電腦移至不同的 OU 的群組。

## 擁有權

這個區段可用來指派群組擁有者。群組擁有者可以將成員新增至群組，並核准或拒絕要求加入群組。根據預設，會建立一組人員是擁有者。所有群組都必須至少一個擁有者。

您可以按一下 \[新增\]**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")，新增擁有者。您可以選取擁有者後再按一下 \[移除\]![\[移除\] 圖示](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[移除] 圖示")，移除該擁有者。**

## 成員資格

這個區段可用來新增或移除成員。群組擁有者不必是群組的成員。在 \[成員\] 下方按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示") 以新增成員。可在成員清單中選擇使用者然後按一下 \[移除\]![\[移除\] 圖示](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[移除] 圖示") 以移除成員。

## 成員資格核准

使用此區段來指定擁有者核准是否需要使用者在加入群組。如果您選取**擁有者核准 」 是必要**的核取方塊，群組擁有者或擁有者會收到要求核准才能加入群組的電子郵件。如先前所述，只有擁有者可以移除群組的成員。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>此選項會無法使用擁有郵件功能的安全性群組因安全性相關的限制。</td>
</tr>
</tbody>
</table>


## 傳遞管理

您可使用此區段來管理哪些使用者可以傳送電子郵件給這個群組。

  - **只限我組織內的寄件者**：選取這個選項可以只允許您組織中的寄件者傳送郵件給群組。這表示如果組織外部人員傳送電子郵件給這個群組，郵件會遭到拒絕。這是預設設定。

  - **我的組織內部和外部的寄件者**：選取這個選項可讓任何人傳送郵件給群組。
    
    若要進一步限制可傳送郵件給群組的人員，可以只允許特定寄件者傳送郵件到這個群組。按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")，然後選取一或多個收件者。 如果新增寄件者至這個清單，只有他們可傳送郵件給群組。不在清單上的任何人所傳送的郵件會遭到拒絕。
    
    若要移除清單中的人員或群組，請從清單中選取他們，然後按一下 \[移除\]![\[移除\] 圖示](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[移除] 圖示")。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果群組已設定為只允許您組織中的寄件者傳送郵件給群組，即使郵件連絡人列於此清單中，他們所傳送的電子郵件也會遭到拒絕。</td>
    </tr>
    </tbody>
    </table>


## 訊息核准

使用此區段可設定用以仲裁群組的選項。仲裁者可在郵件送達群組成員前核准或拒絕傳送給群組的郵件。

  - **此群組傳送的郵件必須由仲裁者核准**  預設不選取此核取方塊。如果您選取此核取方塊，內送郵件將檢閱由群組仲裁者在傳遞之前。群組仲裁者可以核准或拒絕的內送郵件。

  - **群組仲裁者**  若要新增群組仲裁者，請按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。若要移除仲裁，請選取 \[仲裁者，然後按一下 \[**移除**![\[移除\] 圖示](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[移除] 圖示")。如果您已選取 「 傳送到此群組的訊息可以由仲裁者核准 」，您不選取仲裁者將傳送郵件給群組擁有者群組進行核准。

  - **不需要郵件核准的寄件者**  若要新增的人員或群組，可以略過這個群組仲裁，按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。若要移除的人員或群組，請選取的項目，然後按一下 \[**移除**![\[移除\] 圖示](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[移除] 圖示")。

  - **選取仲裁通知**   使用此區段可設定使用者接收郵件核准相關通知的方式。
    
      - **通知所有寄件者時其郵件未核准**  這是預設設定。當其郵件未核准組織內外的寄件者將會收到通知。
    
      - \[僅在組織中寄件者的郵件未獲核准時加以通知\]   如果選取這個選項，則只有組織內的人員或群組有傳送給群組的郵件未通過仲裁者核准時，才會予以通知。
    
      - \[訊息未獲核准時不要通知任何人\]   若選取此選項，郵件的寄件者在其郵件未通過群組仲裁者的核准時，將不會收到通知。

## 電子郵件選項

這個區段可用來檢視或變更與群組相關聯的電子郵件地址。這包括群組的主要 SMTP 位址和任何相關聯的 Proxy 位址。在通訊清單中，主要 SMTP 位址 (亦稱為「回覆地址」) 會以粗體文字顯示，並在 \[類型\] 欄位中包含大寫的 **SMTP** 值。

  - \[新增\] 按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")，可為此信箱新增新的電子郵件地址。選取下列其中一種位址類型：
    
      - \[SMTP\]  這是預設的位址類型。按一下此按鈕，然後在 \[\* 電子郵件地址\] 方塊中輸入新的 SMTP 位址。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>若要讓新的通訊群組的主要 SMTP 位址，請選取 [<strong>將此設為回覆地址</strong>] 核取方塊。只有當未選取 [<strong>自動更新根據電子郵件地址原則套用到此收件者的電子郵件地址</strong>] 核取方塊時，會顯示此核取方塊。</td>
        </tr>
        </tbody>
        </table>
    
      - \[自訂位址類型\]   按一下此按鈕，並在 \[\* 電子郵件地址\] 方塊中，輸入其中一種支援的非 SMTP 電子郵件地址類型。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>除了 X.400 位址以外，Exchange 不會驗證自訂位址的格式是否正確。您必須確保指定的自訂位址符合該位址類型的格式需求。</td>
        </tr>
        </tbody>
        </table>


  - \[編輯\]  若要變更與群組相關的電子郵件地址，先於清單中選擇然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>若要讓現有的通訊群組的主要 SMTP 位址，請選取 [<strong>將此設為回覆地址</strong>] 核取方塊。如上所述，未選取 [<strong>自動更新根據電子郵件地址原則套用到此收件者的電子郵件地址</strong>] 核取方塊時才會顯示此核取方塊。</td>
    </tr>
    </tbody>
    </table>


  - \[移除\]  若要刪除與群組相關的電子郵件地址，先於清單中選擇然後按一下 \[移除\]![\[移除\] 圖示](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[移除] 圖示")。

  - **根據電子郵件地址原則套用到此收件者的電子郵件地址會自動更新**選取此核取方塊已自動更新的收件者的電子郵件地址根據電子郵件地址原則您組織中的所做的變更。根據預設，會選取此方塊。

## MailTip

這個區段可用來新增郵件提示的潛在問題的使用者發出警示之前傳送的郵件時加入此群組。郵件提示是此群組 」 新增至 \[收件者\]、 \[副本\] 或 \[密件副本\] 行中的新的電子郵件時顯示在資訊列中的文字。例如，您可以加入大型群組警告他們的訊息就會傳送給人員大量的潛在寄件者 」 郵件提示。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>「寄件提醒」可以包含 HTML 標記，但是不允許指令碼。自訂郵件提示的長度不能超過 175 個顯示的字元。HTML 標記則不包括在此限制內。</td>
</tr>
</tbody>
</table>


## 群組代理人

本區段可用來指派權限給使用者 (稱為「代理人」)，以允許使用者以群組身份傳送郵件，或代表群組來傳送郵件。您可以指派下列權限：

  - \[以群組身份傳送\]  此權限允許代理人以群組身份傳送郵件。指派此權限之後，代理人即可將群組新增至 \[寄件者\] 行，以表明郵件是由群組所傳送。

  - \[代表群組傳送\]  此權限也可讓代理人代表群組傳送郵件。在此權限指派後，代理人可選擇是否於 \[寄件者\] 行中新增群組。此時郵件看起來會像是由群組所傳送的，其中會顯示該郵件是由代理人代表群組所傳送。

若要將權限指派給代理人，按一下以顯示您可以將指派權限的 Exchange 組織中顯示的所有收件者清單**選取 \[收件者**\] 頁面上的適當權限之下的 \[**新增**\]。選取您想要的收件者、 將其新增至清單，然後按一下 \[**確定\]**。您也可以在 \[搜尋\] 方塊中輸入收件者的名稱，然後按一下 \[**搜尋**![搜尋圖示](images/Dn624163.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "搜尋圖示")來搜尋特定收件者。

## 使用命令介面變更安全性群組內容

使用 **Get-DistributionGroup** 與 **Set-DistributionGroup** 指令程式來檢視與變更安全性群組的內容。使用命令介面的優點是能夠變更在 EAC 中不可用的內容，以及變更多個安全性群組內容。如需更多有關哪些參數對應哪些通訊群組內容的資訊，請參閱以下主題：

  - [Get-DistributionGroup](https://technet.microsoft.com/zh-tw/library/bb124755\(v=exchg.150\))

  - [Set-DistributionGroup](https://technet.microsoft.com/zh-tw/library/bb124955\(v=exchg.150\))

以下是使用命令介面變更安全性群組內容的範例。

本範例會顯示組織中所有安全性群組的清單。

    Get-DistributionGroup -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'MailUniversalSecurityGroup')}

此範例將 Seattle Administrators 安全性群組的主要 SMTP 位址 (也稱為回覆地址) 從 admins@contoso.com 變更為 seattle.admins@contoso.com。前一個回覆地址將會作為 Proxy 位址保留。

    Set-DistributionGroup "Seattle Employees" -EmailAddresses SMTP:sea.admins@contoso.com,smtp:admins@contoso.com

此範例從通訊錄中隱藏了組織中的所有安全性群組。

    Get-DistributionGroup -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'MailUniversalSecurityGroup')} | Set-DistributionGroup -HiddenFromAddressListsEnabled $true

## 如何才能了解這是否正常運作？

若要確認您已成功變更安全性群組的內容，請執行下列操作：

  - 在 EAC 中，選取群組，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示") 以檢視所變更的內容和功能。依據您所變更的內容而定，其有可能會顯示在您所選群組的 \[詳細資料\] 窗格中。

  - 在命令介面中使用**Get-DistributionGroup**指令程式來確認所做的變更。使用命令介面的一個優點是您可以檢視針對多個群組的多個屬性。在上述其中所有安全性群組已從通訊錄中都隱藏範例中，執行下列命令來確認新的值。
    
        Get-DistributionGroup -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'MailUniversalSecurityGroup')} |
         fl Name,HiddenFromAddressListsEnabled


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><img src="images/Bb123521.eac8a413-9498-4220-8544-1e37d1aaea13(EXCHG.150).png" title="LinkedIn Learning 的短圖示" alt="LinkedIn Learning 的短圖示" /> <strong>初次使用 Office 365？</strong><br />
探索 LinkedIn Learning 提供的 <a href="https://support.office.com/zh-tw/article/office-365-admin-and-it-pro-courses-68cc9b95-0bdc-491e-a81f-ee70b3ec63c5">Office 365 admins and IT pros</a> 免費影片課程。</p></td>
</tr>
</tbody>
</table>

