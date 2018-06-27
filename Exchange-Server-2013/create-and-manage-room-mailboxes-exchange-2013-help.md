---
title: '建立及管理會議室信箱: Exchange Online Help'
TOCTitle: 建立及管理會議室信箱
ms:assetid: f70752ad-fce0-4e14-8428-fc5ac63f6c54
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ215781(v=EXCHG.150)
ms:contentKeyID: 50472410
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 建立及管理會議室信箱

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2017-02-02_

預估完成時間：5 分鐘。

「會議室信箱」是指派給像是會議室、視聽室或訓練室等實體地點的資源信箱。在系統管理員建立會議室信箱之後，使用者就可以在會議邀請中加入會議室信箱，輕鬆預約會議室。如需詳細資訊，請參閱＜[收件者](recipients-exchange-2013-help.md)＞。

如需另一種資源信箱類型的相關資訊，請參閱＜[管理設備信箱](manage-equipment-mailboxes-exchange-2013-help.md)＞。

## 您要執行的工作

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱[收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「收件者佈建權限」一節。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您在混合案例中執行 Exchange 2013，請確定您有在適當的地方建立會議室信箱。針對內部部署組織建立會議室信箱，而且 Exchange Online 端的會議室信箱應建立在雲端。</td>
</tr>
</tbody>
</table>



## 建立會議室信箱

## 使用 Exchange 系統管理中心來建立會議室信箱

1.  在 Exchange 系統管理中心內，瀏覽至 \[收件者\] \> \[資源\]。

2.  若要建立會議室信箱，請按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示") \> \[會議室信箱\]。

3.  使用頁面上的選項來指定新資源信箱的設定。
    
      - \[\* 會議室名稱\]   使用此方塊可輸入會議室名稱的名稱。此為列於 Exchange 系統管理中心內與組織通訊錄中，資源郵件清單的名稱。此名稱為必要項目，且不得超過 64 個字元。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>雖然有其他欄位可描述會議室的詳細資料，例如位置和容納的人員數量，但是請考慮使用一致的命名慣例摘要列出會議室名稱中最重要的詳細資料。為什麼？這樣使用者從會議邀請的通訊錄中選取會議室時，才能輕鬆看到詳細資料。</td>
        </tr>
        </tbody>
        </table>
    
      - \[\* 電子郵件地址\]   會議室信箱有電子郵件地址，才能接受預約要求。電子郵件地址中 @ 符號的左側包含別名，必須在樹系中是唯一的，而右側則是網域名稱。電子郵件地址為必要項目。
    
      - **位置**、**電話**、**容量**：您可以使用這些欄位輸入有關會議室的詳細資料。但是，如同之前所說明，您可以在會議室名稱中包含這項資訊的部分或全部，好讓使用者可以看到。

4.  完成作業後，按一下 \[儲存\] 建立會議室信箱。

建立會議室信箱之後，您可以編輯會議室信箱，以更新關於預約選項、寄件提醒和信箱委派的資訊。請參閱下面的＜使用 Exchange 系統管理中心＞一節，以變更會議室信箱內容

## 使用 Exchange PowerShell 來建立會議室信箱

這個範例會使用下列設定來建立會議室信箱：

  - 會議室信箱位於信箱資料庫 1 上。

  - 信箱的名稱為 ConfRoom1。此名稱將用於建立會議室的電子郵件地址。

  - Exchange 系統管理中心和通訊錄中的顯示名稱會是「會議室信箱 1」。

  - *Room* 參數可指定將這個信箱建立為會議室信箱。

<!-- end list -->

    New-Mailbox -Database "Mailbox Database 1" -Name ConfRoom1 - -DisplayName "Conference Room 1" -Room

如需詳細的語法及參數資訊，請參閱＜[New-Mailbox](https://technet.microsoft.com/zh-tw/library/aa997663\(v=exchg.150\))＞。

## 如何知道這是否正常運作？

您可以透過幾種不同的方式來確定是否已正確建立會議室信箱：

  - 在 Exchange 系統管理中心中，瀏覽至 \[收件者\] \> \[資源\]。信箱清單中將顯示新的會議室信箱。在 \[信箱類型\] 下，該類型是 \[會議室\]。

  - 在 Exchange PowerShell 中，執行下列命令以顯示新會議室信箱的相關資訊。
    
        Get-Mailbox <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress

## 建立會議室清單

如果您計劃要有一百個以上的會議室，或已經建立一百個以上的會議室，請使用會議室清單來組織您的會議室。如果貴公司的幾棟建築物中有會議室可供開會預訂，最好能建立每棟建築物的會議室清單。會議室清單是特別標示的通訊群組，其使用方式與其他通訊群組相同。不過，您只可以使用 Exchange 管理命令介面建立會議室清單。

## 使用 Exchange PowerShell 來建立會議室清單

此範例會建立建築物 32 的會議室清單。

    New-DistributionGroup -Name "Building 32 Conference Rooms" -OrganizationalUnit "contoso.com/rooms" -RoomList

## 使用 Exchange PowerShell 以在會議室清單中新增會議室

此範例會將 confroom3223 加入建築物 32 的會議室清單中。

    Add-DistributionGroupMember -Identity "Building 32 Conference Rooms" -Member confroom3223@contoso.com

## 使用 Exchange PowerShell 將通訊群組轉換成會議室清單

您以前可能已建立過包含會議室的通訊群組。您不需要予以重建；我們可以將它們快速轉換成會議室清單。

此範例會將通訊群組 (建築物 34 的會議室) 轉換成會議室清單。

    Set-DistributionGroup -Identity "Building 34 Conference Rooms" -RoomList

## 變更會議室信箱內容

建立會議室信箱之後，您可以使用 Exchange 系統管理中心或是 Exchange PowerShell 來進行變更及設定其他內容。

## 使用 Exchange 系統管理中心來變更會議室信箱內容

1.  在 Exchange 系統管理中心內，瀏覽至 \[收件者\] \> \[資源\]。

2.  在資源信箱清單中，按一下您要變更其內容的會議室信箱，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在會議室信箱內容頁面上，按一下下列其中一個要檢視或變更內容的區段。
    
      - 一般
    
      - 委派
    
      - 預約選項
    
      - 連絡人資訊
    
      - 電子郵件地址
    
      - MailTip

## 一般

使用 \[一般\] 區段以檢視或變更資源相關的基本資訊。

  - \[\* 會議室名稱\]   這個名稱會顯示在 Exchange 系統管理中心與組織通訊錄的資源信箱清單中。若要變更，不得超過 64 字元。

  - \[\* 電子郵件地址\]   這個唯讀方塊會顯示會議室信箱的電子郵件地址。您可於電子郵件地址區段變更。

  - \[容量\]   使用此方塊可輸入會議室能容納的最多人數。

按一下 \[更多選項\]，檢視或變更這些額外的內容：

  - \[組織單位\]   這個唯讀方塊可顯示包含會議室信箱之帳戶的組織單位 (OU)。您必須使用 Active Directory 使用者與電腦以將帳號移到不同的 OU。

  - \[信箱資料庫\]   這個唯讀方塊可顯示主控會議室信箱的信箱資料庫之名稱。使用 Exchange 系統管理中心內的 \[遷移\] 頁面，將信箱移到不同的資料庫。

  - \[\* 別名\]   使用此方塊可變更會議室信箱的別名。

  - \[在通訊清單中隱藏\]   選取此核取方塊，可防止會議室信箱出現在 Exchange 組織中定義的通訊錄及其他其他通訊清單上。選取此核取方塊後，使用者仍可以使用電子郵件地址，傳送預約郵件給會議室信箱。

  - \[部門\]   使用此方塊可指定會議室關聯的部門名稱。您可使用此內容來建立動態通訊群組與通訊清單的收件者條件。

  - \[公司\]   使用此方塊可指定會議室關聯的公司 (若適用)。與 \[部門\] 內容相同，您可使用此內容來建立動態通訊群組與通訊清單的收件者條件。

  - \[通訊錄原則\]   使用此選項指定信箱的通訊錄原則 (ABP)。ABP 包含全域通訊清單 (GAL)、離線通訊錄 (OAB)、會議室清單和一組通訊清單。若要深入了解，請參閱＜[通訊錄原則](address-book-policies-exchange-2013-help.md)＞。
    
    在下拉式清單中，選取要與這個信箱產生關聯的原則。

  - \[自訂屬性\]   這個區段會顯示會議室信箱所定義的自訂屬性。若要指定自訂屬性值，請按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。您最多可為收件者指定 15 個自訂屬性。

## 委派

這個區段可用來檢視或變更會議室信箱如何處理預約要求，以及定義在未自動處理的情形下，哪些人可以接受或拒絕預約要求。

  - \[預約要求\]   選擇下列其中一個選項來處理預約要求。
    
      - \[自動接受或拒絕預約要求\]   有效的會議邀請會自動預約會議室。如果現有的預約發生排程衝突，或是預約要求違反資源的排程限制 (例如，預約時數太長)，則會議邀請會自動遭到拒絕。
    
      - \[選取可以接受或拒絕預約要求的代理人\]   資源代理人會負責接受或拒絕傳送給會議室信箱的會議邀請。如果您指派了多位資源代理人，只有其中一位必須處理特定會議邀請。

  - \[代理人\]   若您選擇需將預約要求傳送給代理人的選項，會列出特定的代理人。按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示") 或 \[移除\]![\[移除\] 圖示](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[移除] 圖示") 以從此清單新增或移除代理人。

## 預約選項

使用 \[預約選項\] 區段可以檢視或變更用於定義可排程會議室的時間、可預約長度以及可保留多久等預約原則的設定。

  - \[允許週期性會議\]   此區段可允許或禁止在會議室安排週期性會議。此設定預設為啟用，所以系統會允許週期性會議。

  - \[僅允許於工作時間排定\]   此區段可接受或拒絕不在該會議室定義之工作時間內的會議邀請。預設會停用此設定，因此允許工作時間以外的會議要求。預設的工作時間為星期一到星期五上午 8:00 至下午 5:00。　您可以在 \[行事曆\] 頁面的 \[外觀\] 區段中設定會議室的工作時間。

  - \[結束日期若超過此限則一律拒絕\]   此設定可透過指定預約重疊時間上限設定，控制超過日期的週期性會議之行為。
    
      - 若啟用此設定，如果預約時間始於或早於 \[預約重疊時間上限\] 方塊中指定的特定日期值，且該值超過此特定日期，則會自動拒絕週期性預約要求。這是預設設定。
    
      - 若停用此設定，如果預約要求始於或早於 \[預約前置時間上限\] 方塊中指定的日期，且該值超過此指定的日期，則會自動接受週期性預約要求。不過，預約數量會減少，如此在指定的日期之後將不會有預約。

  - \[預約前置時間上限 (天)\]   此設定可指定可提前預約會議室的最大天數。此參數的有效輸入是 0 到 1080 的整數。預設值是 180 天。

  - \[持續時間上限 (小時)\]   此設定可指定預約要求中可保留會議室的持續時間上限。預設值為 24 小時。
    
    對於週期性會議而言，會議最長期限會套用至 Exchange 系統管理中心週期性預約要求執行個體的長度。

此頁面上還有一個方塊，可供您寫下訊息，此訊息將會傳送給送出保留會議室之預約要求的使用者。

## 連絡人資訊

使用 \[連絡人資訊\] 區段可以檢視或變更會議室的連絡人資訊。此頁的資訊顯示於通訊錄中。

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

使用 \[電子郵件地址\] 區段可以檢視或變更與會議室信箱關聯的電子郵件地址。這包括此信箱的主要 SMTP 位址以及任一關聯的 Proxy 位址。在通訊清單中，主要 SMTP 位址 (亦稱為「回覆地址」) 會以粗體文字顯示，並在 \[類型\] 欄位中包含大寫的 **SMTP** 值。

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

使用 \[郵件提示\] 區段可加入「郵件提示」，以便在使用者送出預約要求給會議室信箱前，警示使用者潛在的問題。「郵件提示」是在此收件者加入至新電子郵件的 \[收件者\]、\[副本\] 或 \[密件副本\] 行時，顯示在資訊列中的文字。

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


## 使用 Exchange PowerShell 來變更會議室信箱內容

使用下列 Cmdlet 集，可以檢視和變更會議室信箱內容：**Get-Mailbox** 與 **Set-Mailbox** Cmdlet 可檢視與變更會議室信箱的一般內容及電子郵件地址。使用 **Get-CalendarProcessing** 與 **Set-CalendarProcessing** 指令程式來檢視與變更代理人及預約選項。

  - **Get-User** 與 **Set-User**   使用這些 Cmdlet 來檢視與設定位置、部門和公司名稱等一般內容。

  - **Get-Mailbox** 與 **Set-Mailbox**   使用這些指令程式來檢視並設定信箱內容，例如電子郵件地址與信箱資料庫。

  - **Get-CalendarProcessing** 和 **Set-CalendarProcessing**   使用這些 Cmdlet 來檢視與設定預約選項及代理人。

如需這些指令程式的資訊，請參閱下列主題：

  - [Get-User](https://technet.microsoft.com/zh-tw/library/aa996896\(v=exchg.150\))

  - [Set-User](https://technet.microsoft.com/zh-tw/library/aa998221\(v=exchg.150\))

  - [Get-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123685\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\))

  - [Get-CalendarProcessing](https://technet.microsoft.com/zh-tw/library/dd298137\(v=exchg.150\))

  - [Set-CalendarProcessing](https://technet.microsoft.com/zh-tw/library/dd335046\(v=exchg.150\))

以下是一些使用 Exchange PowerShell 來變更會議室信箱內容的範例。

此範例會變更顯示名稱、主要 SMTP 位址 (稱為預設回覆地址) 和會議室容量。另外，上述回覆地址也會保留為 Proxy 位址。

    Set-Mailbox "Conf Room 123" -DisplayName "Conf Room 31/123 (12)" -EmailAddresses SMTP:Rm33.123@contoso.com,smtp:rm123@contoso.com -ResourceCapacity 12

此範例會設定會議室信箱，只允許在工作時間內排程預約要求，並設定持續時間上限為 9 小時。

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'RoomMailbox')} | Set-CalendarProcessing -ScheduleOnlyDuringWorkHours $true -MaximumDurationInMinutes 540

此範例使用 **Get-User** Cmdlet 來尋找對應至私人會議室的所有會議室信箱，接著使用 **Set-CalendarProcessing** Cmdlet 傳送預約要求給名為 Robin Wood 的代理人，請他接受或拒絕。

    Get-User -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'RoomMailbox') -and (DisplayName -like 'Private*')} | Set-CalendarProcessing -AllBookInPolicy $false -AllRequestInPolicy $true -ResourceDelegates "Robin Wood"

## 如何知道這是否正常運作？

若要確認您是否已成功變更會議室信箱的內容，請執行下列動作：

  - 在 Exchange 系統管理中心中，選擇信箱然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示") 以檢視您已變更的內容或功能。根據您變更的屬性，可能會顯示在選取信箱的 \[詳細資料\] 窗格中。

  - 在 Exchange PowerShell 中，使用 **Get-Mailbox** 指令程式來驗證變更。使用 Exchange PowerShell 的其中一個優勢是，可檢視多個會議室信箱的不同內容。在上述只允許於工作時間內排程預約要求，並設定持續時間上限為 9 小時的範例中，執行下列命令，驗證新值。
    
        Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'RoomMailbox')} | Get-CalendarProcessing | fl Identity,ScheduleOnlyDuringWorkHours,MaximumDurationInMinutes

如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

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

