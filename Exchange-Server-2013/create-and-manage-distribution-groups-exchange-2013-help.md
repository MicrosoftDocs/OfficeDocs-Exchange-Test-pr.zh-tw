---
title: '建立並管理通訊群組: Exchange Online Help'
TOCTitle: 建立並管理通訊群組
ms:assetid: c4c43493-55e1-46d2-bd4b-d6f6cecd747f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124513(v=EXCHG.150)
ms:contentKeyID: 50474206
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.CreateDistributionGroupWizardForm.CreateDistributionGroupIntroductionWizardPage
ms.translationtype: HT
---

# 建立並管理通訊群組

 

_**適用版本：**Exchange Online, Exchange Server 2016, Office 365_

_**上次修改主題的時間：**2016-12-09_

使用 Exchange 系統管理中心 (EAC) 或 Exchange 管理命令介面，在 Exchange 組織中建立新通訊群組，或啟用 Active Directory 現有群組的郵件功能。

下列兩種群組可用於發佈郵件：

  - 「擁有郵件功能的萬用通訊群組」(也稱為「通訊群組」) 僅可用於發佈郵件。

  - 「擁有郵件功能的萬用安全性群組」(也稱為「安全性群組」) 可用來發佈郵件以及授與 Active Directory 中資源的存取權限。如需詳細資訊，請參閱[管理擁有郵件功能的安全性群組](manage-mail-enabled-security-groups-exchange-2013-help.md)。

請務必注意 Active Directory 與 Exchange 之間的術語差異。在 Active Directory 中，通訊群組是指任何沒有安全性內容的群組 (無論是否擁有郵件功能)。反之，在 Exchange 中，所有擁有郵件功能的群組都是指通訊群組 (不論是否具有安全性內容)。

## 開始之前有哪些須知？

  - 預估完成時間：2 至 5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱[收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「通訊群組」項目。

  - 若您的組織已設定了群組命名原則，其只能套用至使用者所建立的群組。當您或其他系統管理員使用 EAC 建立通訊群組時，系統會忽略群組命名原則，而不會將它套用至群組名稱。不過，如果您使用命令介面建立或重新命名通訊群組，則只有使用 *IgnoreNamingPolicy* 參數覆寫群組命名原則，才會套用該原則。如需詳細資訊，請參閱：
    
      - [建立通訊群組命名原則](create-a-distribution-group-naming-policy-exchange-2013-help.md)
    
      - [通訊群組命名原則會覆寫](override-the-distribution-group-naming-policy-exchange-2013-help.md)

## 您要執行的工作

## 建立通訊群組

## 使用 EAC 建立通訊群組

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[群組\]。

2.  按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示") \> \[通訊群組\]。

3.  
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><img src="images/Bb124513.3ea82c95-9dda-450f-823b-cd0772249d81(EXCHG.150).png" title="新增功能 試用 Office 365 群組" alt="新增功能 試用 Office 365 群組" /><br />
    如果您有商務用 Office 365 方案或 Exchange Online 方案，現在就可以建立 Office 365 群組來取代通訊群組。Office 365 群組擁有通訊群組的功能以及其他功能。您可以利用 Office 365 群組傳送電子郵件至群組、共用一般行事曆，以及擁有可儲存並支援群組檔案和資料夾的程式庫。按一下 [新增]<img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="加入圖示" alt="加入圖示" /> &gt; [Office 365 群組] 開始使用，並參閱 <a href="https://go.microsoft.com/fwlink/p/?linkid=800653">Office 365 群組 - 管理員說明</a>。<br />
    如果您有想要遷移到 Office 365 群組的現有通訊群組，請參閱<a href="https://go.microsoft.com/fwlink/p/?linkid=824756">將通訊群組清單移轉到 Office 365 群組 - 管理員說明</a>。<br />
    如果您仍然想要建立通訊群組，請按一下或點選 [新增通訊群組] 精靈。</td>
    </tr>
    </tbody>
    </table>


4.  
    
    在 \[新增通訊群組\] 頁面上填妥以下方塊：
    
      - \[\* 顯示名稱\]   使用此方塊輸入顯示名稱。當電子郵件傳送至此群組時，這個名稱會出現在組織通訊錄的 \[收件者:\]行和 EAC 的 \[群組\] 清單中。顯示名稱為必要項目，應以好記易懂為原則，以便他人分辨群組的用途。它在樹系中必須是唯一的。
    
      - \[\* 別名\]使用此方塊輸入群組的別名。別名不得超過 64 個字元，且必須在樹系中是唯一的。當使用者在電子郵件 \[收件者:\] 行中輸入別名時，系統會將別名解析為群組的顯示名稱。
    
      - **組織單位**   (只有在內部部署的 Exchange 2013 中看得到這個選項) 您可選取預設值以外 (在收件者範圍中) 的組織單位 (OU)。如果將收件者範圍設定為樹系，則預設值會設定為 Active Directory 網域 (包含正在執行 EAC 的電腦) 中出現的使用者容器。若收件者範圍設為特定網域，則依預設會選取該網域的使用者容器。若收件者範圍設為特定 OU，則依預設會選取該 OU。
        
        若要選取不同的 OU，請按一下 \[瀏覽\]。此對話方塊會顯示樹系中在指定範圍內的所有 OU。選取想要的 OU，然後按一下 \[確定\]。
    
      - **\* 擁有者**：群組的建立者預設為擁有者。每個群組至少必須有一個擁有者。您可以按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示") 新增擁有者。
    
      - \[成員\]  使用此區段可新增成員並指定使用者在加入或離開群組時是否需要經過核准。
        
        群組擁有者不必是群組的成員。使用 \[新增群組擁有者為成員\]可以將擁有者新增為成員，或移除其成員資格。
        
        若要將成員新增至群組，請按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。完成新增成員之後，請按一下 \[確定\] 回到 \[新增通訊群組\] 頁面。
        
        在 \[選擇在加入群組時是否需要擁有者核准\] 下方，指定使用者在加入群組時是否需要經過核准。請選取下列其中一個設定：
        
          - **開啟：任何人皆可直接加入此群組，不需經過群組擁有者核准**  這是預設設定。
        
          - **關閉：成員只能由群組擁有者加入。所有加入要求都會自動拒絕**
        
          - 擁有者核准：**群組擁有者會手動核准或拒絕所有要求\]**  如果您選取這個選項，群組擁有者會收到請求核准加入群組的電子郵件。
        
        在 \[選擇群組是否可自由離開\] 下方，指定使用者在離開群組時是否需要經過核准。請選取下列其中一個設定：
        
          - **開啟：任何人都可以離開此群組，而不需要群組擁有者的核准  **這是預設設定。
        
          - **關閉：成員只能由群組擁有者移除。所有退出要求都會自動被拒絕。**

5.  完成作業後，請按一下\[儲存\] 以建立通訊群組。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>依預設，新的通訊群組會要求所有寄件者經過驗證。如此便可防止外部寄件者傳送郵件給通訊群組。若要設定通訊群組接受來自所有寄件者的郵件，則必須修改該通訊群組的郵件傳遞限制設定。</td>
</tr>
</tbody>
</table>


## 使用命令介面建立通訊群組

此範例會建立別名為 **itadmin** 且名稱為 **IT Administrators** 的通訊群組。通訊群組是在預設 OU 中建立的，因此任何人都可以加入此群組，而不需群組擁有者的核准。

    New-DistributionGroup -Name "IT Administrators" -Alias itadmin -MemberJoinRestriction open

如需使用命令介面建立通訊群組的相關資訊，請參閱 [New-DistributionGroup](https://technet.microsoft.com/zh-tw/library/aa998856\(v=exchg.150\))。

## 如何知道這是否正常運作？

若要驗證是否成功建立通訊群組，請執行以下其中一個操作：

  - 在 EAC 中，瀏覽至 \[收件者\] \> \[群組\]。新的通訊群組會顯示在群組清單中。在 \[群組類型\] 下方的類型應為 \[通訊群組\]。

  - 在命令介面中，執行下列命令以顯示新通訊群組的資訊。
    
        Get-DistributionGroup <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>可以只建立萬用通訊群組或啟用萬用通訊群組的郵件功能。若要將網域本機或全域群組轉換至萬用群組，您可以使用命令介面中的 <a href="https://technet.microsoft.com/zh-tw/library/bb123770(v=exchg.150)">Set-Group</a> Cmdlet。您可能會有從舊版 Exchange 遷移之擁有郵件功能的群組，但這些群組不是萬用群組。您可以使用 EAC 或命令介面來管理這些群組</td>
</tr>
</tbody>
</table>


## 變更通訊群組內容

## 使用 EAC 變更通訊群組內容

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[群組\]。

2.  在群組清單中，按一下您要檢視或變更的通訊群組，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在群組屬性頁面上，按一下下列區段其中之一以檢視或變更屬性。
    
      - 一般
    
      - 擁有權
    
      - 成員資格
    
      - 成員資格核准
    
      - 傳遞管理
    
      - 訊息核准
    
      - 電子郵件選項
    
      - MailTip
    
      - 群組代理人

## 一般

這個區段可用來檢視或變更群組的基本資訊。

  - **\* 顯示名稱**：這個名稱會出現在通訊錄的 \[收件者:\] 中：行以及 \[群組\] 清單中 (當電子郵件傳送至此群組時)。顯示名稱為必要項目，應以好記易懂為原則，以便他人分辨群組的用途。這個名稱在您的網域中也必須是唯一的。
    
    如果您已經實作群組命名原則，顯示名稱就必須符合此原則所定義的命名格式。

  - \[\* 別名\]  此為電子郵件地址中顯示於 @ 符號左側的部分。變更別名時，群組的主要 SMTP 位址也會變更，並會包含新的別名。此外，使用之前別名的電子郵件地址仍會保留為群組的主要 Proxy 位址。

  - \[描述\]  這個方塊可用來描述群組，讓人員了解群組的用途。此描述會顯示在通訊錄和 EAC 的 \[詳細資料\] 窗格中。

  - \[從通訊清單中隱藏這個群組\]  如果您不想要讓使用者在通訊錄中看見這個群組，請選取此核取方塊。若要傳送電子郵件至此群組，寄件者必須在 \[收件者:\]或 \[副本:\]行中輸入群組的別名或電子郵件地址。
    
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


  - \[組織單位\]  這個唯讀方塊會顯示包含通訊群組的組織單位 (OU)。您必須使用 Active Directory 使用者和電腦，才能將群組移動至不同的 OU。

## 擁有權

這個區段可用來指派群組擁有者。群組擁有者可以新增成員至群組、核准或拒絕加入或離開群組的要求，以及核准或拒絕寄給群組的郵件。群組的建立者預設為擁有者。每個群組至少必須有一個擁有者。

您可以按一下 \[新增\]**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")，新增擁有者。您可以選取擁有者後再按一下 \[移除\]![\[移除\] 圖示](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[移除] 圖示")，移除該擁有者。**

## 成員資格

這個區段可用來新增或移除成員。群組擁有者不必是群組的成員。在 \[成員\] 下方按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示") 以新增成員。可在成員清單中選擇使用者然後按一下 \[移除\]![\[移除\] 圖示](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[移除] 圖示") 以移除成員。

## 成員資格核准

使用此區段可指定使用者在加入或離開群組時是否需要經過核准。

  - \[選擇是否需要擁有者核准才能加入群組\]  請選取下列其中一個設定：
    
      - **開啟:任何人都可以加入此群組，不需由群組擁有者核准**
    
      - **關閉：成員只能由群組擁有者加入。所有加入要求都會自動拒絕**
    
      - **擁有者核准: 所有要求都經由群組擁有者核准或拒絕\]**  如果您選取這個選項，群組擁有者會收到請求核准加入群組的電子郵件。

  - **選擇群組是否可自由離開**：請選取下列其中一個設定：
    
      - **開啟:任何人都可以離開此群組，不需由群組擁有者核准**
    
      - **關閉：成員只能由群組擁有者移除。所有退出要求都會自動被拒絕。**

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
    <td>如果您已將群組設定為只允許您組織中的寄件者傳送郵件給群組，則即使將郵件連絡人新增至此清單中，他們所傳送的電子郵件也會遭到拒絕。</td>
    </tr>
    </tbody>
    </table>


## 訊息核准

使用此區段可設定用以仲裁群組的選項。仲裁者可在郵件送達群組成員前核准或拒絕傳送給群組的郵件。

  - \[傳送至此群組的訊息必須經過仲裁者的核准\]  這個核取方塊預設為未選取狀態。如果選取這個核取方塊，群組仲裁者會在內送郵件傳遞前加以審視。群組仲裁者可核准或拒絕內送郵件。

  - \[群組仲裁者\]  若要新增群組仲裁者，請按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。若要移除仲裁者，請選取該仲裁者，然後按一下 \[移除\]![\[移除\] 圖示](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[移除] 圖示")。如果已選取 \[傳送至此群組的訊息必須經過仲裁者的核准\]，但未選取仲裁者，傳送給該群組的郵件將會交由群組擁有者來核准。

  - \[寄件者不需要訊息核准\] 若要新增可略過此群組之仲裁的人員或群組，請按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。若要移除人員或群組，請選取項目，然後按一下 \[移除\]![\[移除\] 圖示](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[移除] 圖示")。

  - **選取仲裁通知**   使用此區段可設定使用者接收郵件核准相關通知的方式。
    
      - \[在所有寄件者的郵件未獲核准時加以通知\]  這是預設設定。當組織內外所有寄件者的郵件未獲核准時予以通知。
    
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
        <td>若要讓新的位址成為群組的主要 SMTP 位址，請選取 [將此位址設為回覆地址] 核取方塊。</td>
        </tr>
        </tbody>
        </table>
    
      - \[自訂位址類型\]  按一下此按鈕，並在 \[\* 電子郵件地址\] 方塊中，輸入其中一種支援的非 SMTP 電子郵件地址類型。
        
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
    <td>若要讓現有的位址成為群組的主要 SMTP 位址，請選取 [將此位址設為回覆地址] 核取方塊。</td>
    </tr>
    </tbody>
    </table>


  - \[移除\]  若要刪除與群組相關的電子郵件地址，先於清單中選擇然後按一下 \[移除\]![\[移除\] 圖示](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[移除] 圖示")。

  - \[依照套用至此收件者的電子郵件地址原則自動更新電子郵件地址\]  選取此核取方塊，可讓收件者的電子郵件地址自動依照組織內電子郵件地址原則的變更而更新。預設會選取此方塊。

## MailTip

本區段可用來新增「寄件提醒」，以便在使用者傳送郵件給此群組時，通知使用者潛在的問題。「寄件提醒」是在此群組新增至新電子郵件的 \[收件者\]、\[副本\] 或 \[密件副本\] 行時，顯示在資訊列中的文字。例如，您可以將郵件提示新增至大型群組，以便警告可能的寄件者，表示其郵件將傳送至大量人員。

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

若要指派權限給代理人，請按一下適當權限下方的 \[新增\]，即會顯示 \[選取收件者\] 頁面，其會顯示一份 Exchange 組織中可指派權限的所有收件者清單。選取想要的收件者，然後按一下 \[確定\]。您也可以在搜尋方塊中輸入收件者的名稱，然後按一下 \[搜尋\]，以搜尋特定的收件者。

## 使用命令介面變更通訊群組內容

使用 **Get-DistributionGroup** 和 **Set-DistributionGroup** Cmdlet 以檢視或變更通訊群組的內容。使用命令介面的優點是可以變更 EAC 中無法使用的內容，並可變更多個群組的內容。若要了解哪些參數與通訊群組內容相對應的相關資訊，請參閱下列主題：

  - [Get-DistributionGroup](https://technet.microsoft.com/zh-tw/library/bb124755\(v=exchg.150\))

  - [Set-DistributionGroup](https://technet.microsoft.com/zh-tw/library/bb124955\(v=exchg.150\))

下列為使用命令介面變更通訊群組內容的部分範例。

此範例會將 Seattle Employees 通訊群組的主要 SMTP 位址 (亦稱為回覆地址) 從 employees@contoso.com 變更為 sea.employees@contoso.com。此外，之前的回覆地址仍會保留為 Proxy 位址。

    Set-DistributionGroup "Seattle Employees" -EmailAddresses SMTP:sea.employees@contoso.com,smtp:employees@contoso.com

此範例會將可傳送至組織中所有通訊群組的郵件大小上限限制為 10 MB。

    Get-DistributionGroup -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'MailUniversalDistributionGroup')} | Set-DistributionGroup -MaxReceiveSize 10MB

此範例會對 Customer Support 通訊群組啟用仲裁，並將仲裁者設定為 Amy。此外，這個有仲裁者在管控的通訊群組將會在仲裁者未核准由組織內的寄件者所傳送的郵件時，通知該寄件者。

    Set-DistributionGroup -Identity "Customer Support" -ModeratedBy "Amy" -ModerationEnabled $true -SendModerationNotifications 'Internal'

此範例會將使用者建立的 Dog Lovers 通訊群組變更為當使用者要加入群組時，必須先經過群組管理員的核准。此外還使用 *BypassSecurityGroupManagerCheck* 參數，讓群組管理員不會收到通訊群組設定變更的通知。

    Set-DistributionGroup -Identity "Dog Lovers" -MemberJoinRestriction 'ApprovalRequired' -BypassSecurityGroupManagerCheck

## 如何知道這是否正常運作？

若要驗證是否成功變更通訊群組的內容，請執行以下其中一個操作：

  - 在 EAC 中，選取群組，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示") 以檢視所變更的內容和功能。依據您所變更的內容而定，其有可能會顯示在您所選群組的 \[詳細資料\] 窗格中。

  - 在命令介面中，使用 **Get-DistributionGroup** 指令程式來驗證變更。使用命令介面的其中一個優點就是您可以檢視多個群組的多項內容。在上方範例中變更收件者限制的位置執行下列命令，以驗證新值。
    
        Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'UserMailbox')} | fl Name,RecipientLimits
    
    針對上述變更郵件限制的範例中，請執行此命令。
    
        Get-Mailbox -OrganizationalUnit "Marketing" | fl Name,IssueWarningQuota,ProhibitSendQuota,ProhibitSendReceiveQuota,UseDatabaseQuotaDefaults

