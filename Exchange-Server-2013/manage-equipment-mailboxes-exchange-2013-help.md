---
title: '管理設備信箱: Exchange Online Help'
TOCTitle: 管理設備信箱
ms:assetid: e5f58b3a-83e1-4742-8846-85103a44ee18
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ215770(v=EXCHG.150)
ms:contentKeyID: 50472411
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理設備信箱

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2014-10-09_

*設備信箱*是指派給沒有具體位置之資源的資源信箱，如可攜式電腦、投影機、麥克風或公務車。在系統管理員建立設備信箱之後，使用者可以透過在會議邀請中包含對應設備信箱，輕鬆預約設備。您可以使用 EAC 和命令介面，建立設備信箱或變更設備信箱內容。如需詳細資訊，請參閱[收件者](recipients-exchange-2013-help.md)。

如需其他類型的資源信箱、會議室信箱等的詳細資訊，請參閱[建立及管理會議室信箱](create-and-manage-room-mailboxes-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：2 至 5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「收件者佈建權限」一節。

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

## 建立設備信箱

## 使用 EAC 建立設備信箱

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[資源\]。

2.  若要建立設備信箱，請按一下 \[新增\] \> \[設備信箱\]。若要建立會議室信箱，請按一下 \[新增\] \> \[會議室信箱\]。

3.  使用頁面上的選項來指定新資源信箱的設定。
    
      - \[\* 設備名稱\]   使用這個方塊輸入設備信箱的名稱。此為列於 EAC 中與組織通訊錄中，資源郵件清單的名稱。 此名稱為必要項目，且不得超過 64 個字元。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>雖然有其他欄位 (例如 [容量]) 可描述會議室的詳細資料，但是請考量使用一致的命名慣例摘要列出設備名稱中最重要的詳細資料。為什麼？這樣使用者從會議邀請的通訊錄中選取設備時，才能輕鬆看到詳細資料。</td>
        </tr>
        </tbody>
        </table>
    
      - \[\* 電子郵件地址\]   設備信箱會有一個電子郵件地址，這樣它就可以接收預約要求。電子郵件地址中 @ 符號的左側包含別名，必須在樹系中是唯一的，而右側則是網域名稱。電子郵件地址為必要項目。

4.  完成作業後，按一下 \[儲存\] 即可建立設備信箱。

一旦您已經建立設備信箱，您可以編輯您的設備信箱來更新預約選項、 寄件提醒和委派的資訊。查看 \[變更設備信箱內容\] 區段下變更會議室信箱內容

## 使用命令介面建立設備信箱

這個範例會建立具有下列設定的設備信箱：

  - 設備信箱位於信箱資料庫 1 上。

  - 設備的名稱為 MotorVehicle2，而此名稱在 GAL 中會顯示為 Motor Vehicle 2。

  - 電子郵件地址是 MotorVehicle2@contoso.com。

  - 信箱位於設備組織單位中。

  - *Equipment* 參數可指定將這個信箱建立為設備信箱。

<!-- end list -->

    New-Mailbox -Database "Mailbox Database 1" -Name MotorVehicle2 -OrganizationalUnit Equipment -DisplayName "Motor Vehicle 2" -Equipment

如需詳細的語法及參數資訊，請參閱 [New-Mailbox](https://technet.microsoft.com/zh-tw/library/aa997663\(v=exchg.150\))。

## 如何知道這是否正常運作？

若要驗證是否成功建立使用者信箱，請執行以下其中一個操作：

  - 在 EAC 中，瀏覽至 \[收件者\] \> \[資源\]。信箱清單中將顯示新的使用者信箱。在 \[信箱類型\] 下，類型為 \[設備\]。

  - 在命令介面中，執行下列命令，顯示新設備信箱的相關資訊。
    
        Get-Mailbox <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress

## 變更設備信箱內容

建立設備信箱之後，您可以使用 EAC 或命令介面來變更和設定其他內容。

## 使用 EAC 變更設備信箱內容

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[資源\]。

2.  在資源信箱清單中，按一下您要變更內容的設備信箱，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在設備信箱內容頁上，按一下下列其中一個要檢視或變更內容的區段。
    
      - General
    
      - Delegates
    
      - Booking Options
    
      - Contact Information
    
      - Email Address
    
      - MailTip

## 一般

使用 \[一般\] 區段以檢視或變更資源相關的基本資訊。

  - \[\* 設備名稱\]   此名稱顯示在 EAC 與組織通訊錄中的資源信箱清單中。若要變更，不得超過 64 字元。

  - \[\* 電子郵件地址\]   此唯讀方塊顯示設備信箱的電子郵件地址。您可於Email Address區段變更。

  - \[容量\]   使用此方塊可以輸入使用這個資源的人員數上限，例如，如果設備信箱對應小汽車，則您可以輸入 **4**。

按一下 \[更多選項\]，檢視或變更這些額外的內容：

  - \[組織單位\]   此唯讀方塊可顯示包含設備信箱帳戶的組織單位 (OU)。您必須使用 Active Directory 使用者與電腦以將帳號移到不同的 OU。

  - \[信箱資料庫\]   此唯讀方塊顯示主控設備信箱的信箱資料庫名稱。使用 EAC 中的 \[遷移\] 頁面，將信箱移到不同的資料庫。

  - \[\* 別名\] 使用此方塊可變更設備信箱的別名。

  - \[從地址清單隱藏\]   選取此核取方塊，可防止設備信箱出現在 Exchange 組織中定義的通訊錄和其他地址清單中。選取此核取方塊後，使用者仍可以使用此電子郵件地址傳送預約郵件給設備信箱。

  - \[部門\]   使用此方塊可指定與資源相關的部門名稱。您可使用此內容來建立動態通訊群組與通訊清單的收件者條件。

  - \[公司\]   使用此方塊可指定與資源相關的公司。與 \[部門\] 內容相同，您可使用此內容來建立動態通訊群組與通訊清單的收件者條件。

  - \[通訊錄原則\]   使用此選項可指定資源的通訊錄原則 (ABP)。ABP 包含全域通訊清單 (GAL)、離線通訊錄 (OAB)、會議室清單和一組通訊清單。若要深入了解，請參閱[通訊錄原則](address-book-policies-exchange-2013-help.md)。
    
    在下拉式清單中，選取要與這個信箱產生關聯的原則。

  - \[自訂屬性\]   這個區段顯示為設備信箱定義的自訂屬性。若要指定自訂屬性值，請按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。您最多可為收件者指定 15 個自訂屬性。

## 委派

使用此區段可檢視或變更設備信箱處理預約要求的方式，以及定義接受或拒絕預約要求的人員 (如果不是自動進行)。

  - \[預約要求\]   選擇下列其中一個選項來處理預約要求。
    
      - \[自動接受或拒絕預約要求\]   有效的會議邀請會自動預約資源。如果現有的預約發生排程衝突，或是預約要求違反資源的排程限制 (例如，預約時數太長)，則會議邀請會自動遭到拒絕。
    
      - \[選取接受或拒絕預約要求的代理人\]   資源代理人會負責接受或拒絕傳送給設備信箱的會議邀請。如果您指派了多位資源代理人，只有其中一位必須處理特定會議邀請。

  - \[代理人\]   若您選擇需將預約要求傳送給代理人的選項，會列出特定的代理人。按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示") 或 \[移除\]![\[移除\] 圖示](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[移除] 圖示") 以從此清單新增或移除代理人。

## 預約選項

使用 \[預約選項\] 區段可檢視或變更下列設定：排定資源時定義的預約原則、預約時間長度以及可預約的距離。

  - \[允許週期性會議\]   此設定可允許或阻止資源的週期性會議。此設定預設為啟用，所以系統會允許週期性會議。

  - \[僅允許於工作時間排定\]   此設置可接受或拒絕為資源定義的工作時間之外的會議要求。預設會停用此設定，因此允許工作時間以外的會議要求。預設的工作時間為星期一到星期五上午 8:00 至下午 5:00。　您可以在 \[行事曆\] 頁面的 \[外觀\] 區段中設定設備信箱的工作時間。

  - \[結束日期若超過此限則一律拒絕\]   此設定可透過指定預約重疊時間上限設定，控制超過日期的週期性會議之行為。
    
      - 若啟用此設定，如果預約時間始於或早於 \[預約重疊時間上限\] 方塊中指定的特定日期值，且該值超過此特定日期，則會自動拒絕週期性預約要求。這是預設設定。
    
      - 若停用此設定，如果預約要求始於或早於 \[預約前置時間上限\] 方塊中指定的日期值，且它們超過此指定日期，則會自動接受週期性預約要求。不過，預約數量會減少，如此在指定的日期之後將不會有預約。

  - \[預約前置時間上限 (天)\]   此設定指定可以提前預約資源的時間上限 (天)。此參數的有效輸入是 0 到 1080 的整數。預設值是 180 天。

  - \[持續時間上限 (小時)\]   此設定指定預約要求中可以預約資源的持續時間上限。預設值為 24 小時。
    
    對於週期性會議而言，會議最長期限會套用至每個週期性預約要求執行個體的長度。

此頁面上也有一個方塊，可用於書寫郵件，並傳送到傳送會議要求以預定資源的使用者。

## 連絡人資訊

使用 \[連絡人資訊\] 區段可檢視或變更資源的連絡人資訊。此頁的資訊顯示於通訊錄中。

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


## 電子郵件地址

使用 \[電子郵件地址\] 區段可用來檢視或變更與設備信箱相關聯的電子郵件地址。這包括此信箱的主要 SMTP 位址以及任一關聯的 Proxy 位址。在通訊清單中，主要 SMTP 位址 (亦稱為「回覆地址」) 會以粗體文字顯示，並在 \[類型\] 欄位中包含大寫的 **SMTP** 值。

  - \[新增\]  按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")，可為此信箱新增新的電子郵件地址。選取下列其中一種位址類型：
    
      - \[SMTP\]   這是預設的位址類型。按一下此按鈕，然後在 \[\* 電子郵件地址\] 方塊中輸入新的 SMTP 位址。
    
      - \[EUM\]   EUM (Exchange 整合通訊) 位址是由 Microsoft Exchange 整合通訊服務用於尋找 Exchange 組織中啟用 UM 功能的使用者。EUM 位址包含啟用 UM 功能的使用者本身的分機號碼和 UM 撥號對應表。點選此按鈕並在 \[通訊錄/分機\]方塊中輸入分機號碼。然後按一下 \[瀏覽\] 並選擇信箱的撥號對應表。
    
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
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>當您新增新的電子郵件時，會出現主要 SMTP 位址的選項。</td>
    </tr>
    </tbody>
    </table>


  - \[依照套用至此收件者的電子郵件地址原則自動更新電子郵件地址\]   選取此核取方塊，可讓收件者的電子郵件地址自動依照組織內電子郵件地址原則的變更而更新。

## MailTip

使用 \[郵件提示\] 區段可新增「郵件提示」，以便在傳送預約要求給設備信箱前，警示使用者潛在的問題。「郵件提示」是在此收件者加入至新電子郵件的 \[收件者\]、\[副本\] 或 \[密件副本\] 行時，顯示在資訊列中的文字。

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


## 使用命令介面變更設備信箱內容

使用下列 Cmdlet 集可以檢視和變更設備信箱內容：**Get-Mailbox** 與 **Set-Mailbox** Cmdlet 可檢視和變更設備信箱的一般內容和電子郵件地址。使用 **Get-CalendarProcessing** 與 **Set-CalendarProcessing** Cmdlet 來檢視與變更代理人及預約選項。

  - **Get-User** 與 **Set-User**   使用這兩個 Cmdlet 可檢視和設定一般內容，例如，部門和公司名稱。

  - **Get-Mailbox** 與 **Set-Mailbox**   使用這些 Cmdlet 來檢視並設定信箱內容，例如電子郵件地址與信箱資料庫。

  - **Get-CalendarProcessing** 和 **Set-CalendarProcessing**   使用這些 Cmdlet 來檢視與設定預約選項及代理人。

如需這些指令程式的資訊，請參閱下列主題：

  - [Get-User](https://technet.microsoft.com/zh-tw/library/aa996896\(v=exchg.150\))

  - [Set-User](https://technet.microsoft.com/zh-tw/library/aa998221\(v=exchg.150\))

  - [Get-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123685\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\))

  - [Get-CalendarProcessing](https://technet.microsoft.com/zh-tw/library/dd298137\(v=exchg.150\))

  - [Set-CalendarProcessing](https://technet.microsoft.com/zh-tw/library/dd335046\(v=exchg.150\))

下列範例使用命令介面來變更設備信箱內容。

此範例變更 MotorPool 1 設備信箱的顯示名稱和主要 SMTP 位址 (稱為預設回覆地址)。以前的回覆地址將用做 Proxy 位址。

    Set-Mailbox "MotorPool 1" -DisplayName "Motor Pool 1 - Compact" -EmailAddresses SMTP:MP1.compact@contoso.com,smtp:MP.1@contoso.com

此範例將設備信箱設定為僅在工作時間允許排定預約要求。

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'EquipmentMailbox')} | Set-CalendarProcessing -ScheduleOnlyDuringWorkHours $true

此範例使用 **Get-User** Cmdlet 尋找 Audio Visual 部門中的所有設備信箱，然後使用 **Set-CalendarProcessing** Cmdlet 傳送預約要求至名為 Ann Beebe 的代理人，以便接受或拒絕。

    Get-User -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'EquipmentMailbox') -and (Department -eq 'Audio Visual')} | Set-CalendarProcessing -AllBookInPolicy $false -AllRequestInPolicy $true -ResourceDelegates "Ann Beebe"

## 如何知道這是否正常運作？

若要驗證已成功變更設備信箱的內容，請進行下列步驟：

  - 在 EAC 中，選擇信箱然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示") 以檢視您已變更的內容或功能。根據您變更的屬性，可能會顯示在選取信箱的 \[詳細資料\] 窗格中。

  - 在命令介面中，使用 **Get-Mailbox** Cmdlet 來驗證變更。使用介面的其中一個優勢是，可檢視多個會議室信箱的不同內容。在上述僅允許在工作時間排定預約要求的範例中，執行下列命令來驗證新值。
    
        Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'EquipmentMailbox')} | Get-CalendarProcessing | fl Identity,ScheduleOnlyDuringWorkHours

