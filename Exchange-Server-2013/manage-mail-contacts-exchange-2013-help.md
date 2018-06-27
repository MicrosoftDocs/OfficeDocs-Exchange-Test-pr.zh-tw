---
title: '管理郵件連絡人: Exchange Online Help'
TOCTitle: 管理郵件連絡人
ms:assetid: 74c72aed-e9ff-4927-8eb7-c08a86e79ae0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa998858(v=EXCHG.150)
ms:contentKeyID: 50472317
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.NewMailContactWizardForm.NewMailContactIntroductionWizardPage
ms.translationtype: MT
---

# 管理郵件連絡人

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2017-10-04_

郵件連絡人是擁有郵件功能的目錄服務物件包含的人員或組織存在 Exchange 或Exchange Online組織外部的相關資訊。每個郵件連絡人都有外部的電子郵件地址。如需郵件連絡人的詳細資訊，請參閱[收件者](recipients-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：2 分鐘。

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

## 建立郵件連絡人

## 使用 EAC 來建立郵件連絡人

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[連絡人\]。

2.  按一下 **\[新增\]** ![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示") \> **\[郵件連絡人\]**。

3.  在 \[新增郵件連絡人\] 頁面上完成下列方塊：
    
      - **名字**   使用此方塊可以輸入連絡人的名字。
    
      - **縮寫**   使用此方塊可以輸入連絡人名字的縮寫。
    
      - **姓氏**   使用此方塊可以輸入連絡人的姓氏。
    
      - **\* 顯示名稱**  使用此方塊可輸入連絡人的顯示名稱。這是在 EAC 中與您組織的通訊錄中的 \[連絡人\] 清單中所列的名稱。根據預設，此方塊會填入您在 \[**名字**、**縮寫**和**姓氏**\] 方塊中輸入的名稱。如果您未使用這些方塊，您必須仍輸入名稱在此方塊因為有必要。名稱不可超過 64 個字元。
    
      - **\* 名稱**  使用此方塊可輸入連絡人的名稱。這是目錄服務中所列的名稱。顯示名稱，例如此方塊會填入預設您在 \[**名字**、**縮寫**和**姓氏**\] 方塊中輸入的名稱。如果您未使用這些方塊，您必須仍輸入名稱在此方塊因為有必要。名稱不可超過 64 個字元。
    
      - **\* 別名**使用此方塊可輸入別名 (64 個字元或更少) 的連絡人。需要此方塊。
    
      - **\* 外部的電子郵件地址**  使用此方塊可輸入連絡人的外部電子郵件帳戶。需要此方塊。傳送給此連絡人的電子郵件轉寄給此電子郵件地址。
    
      - **組織單位**  您可以選取組織單位 (OU) 以外的預設值，這是收件者的範圍。如果收件者範圍會設為樹系中，預設值是設定為 \[使用者\] 容器中包含 EAC 執行所在之電腦的網域。如果收件者範圍會設為特定的網域，預設會選取該網域中的 \[使用者\] 容器。如果收件者範圍會設為特定的 OU，預設會選取該 OU。
        
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


4.  完成作業後，請按一下 **\[儲存\]**。

## 使用命令介面來建立郵件連絡人

此範例會在 Exchange Server 2013 中建立 Debra Garcia 的郵件連絡人。

    New-MailContact -Name "Debra Garcia" -ExternalEmailAddress dgarcia@tailspintoys.com -OrganizationalUnit Users

此範例會在 Exchange Online 中建立 Alan Shen 的郵件連絡人。

    New-MailContact -Name "Alan Shen" -ExternalEmailAddress alans@fourthcoffee.com

此範例會使 Exchange Server 2013 中名稱爲 Karen Toh 的現有連絡人具備郵件功能。

    Enable-MailContact -Identity "Karen Toh" -ExternalEmailAddress ktoh@tailspintoys.com

## 如何才能了解這是否正常運作？

若要驗證是否成功建立信箱連絡人，請執行以下其中一個操作：

  - 在 EAC 中，瀏覽至 \[**收件者**\>**連絡人**。新的郵件連絡人會顯示在連絡人清單中。\[**連絡人類型**\] 下方類型是**郵件連絡人**。

  - 在命令介面中，執行以下命令以顯示新郵件連絡人的資訊。
    
        Get-MailContact <Name> | FL Name,RecipientTypeDetails,ExternalEmailAddress

## 變更郵件連絡人內容

## 使用 EAC 變更郵件連絡人內容

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[連絡人\]。

2.  在郵件連絡人與郵件使用者的清單中，按一下您希望變更內容的郵件連絡人，接著按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在信箱連絡人內容頁上，按一下下列其中一個要檢視或變更內容的區段。
    
      - General
    
      - Contact Information
    
      - Organization
    
      - Email Options (Exchange Online 中無法使用)
    
      - MailTip

## 一般

使用 \[一般\] 區段以檢視或變更郵件連絡人相關的基本資訊。

  - \[名字\]、\[縮寫\]、\[姓氏\]

  - \[\* 名稱\]   這是列於 Active Directory 中的名稱。 如果您變更這個名稱，這個名稱不可超過 64 個字元。

  - **\* 顯示名稱**  此名稱會出現在貴組織的通訊錄，在\] 和 \[從電子郵件，並在信箱清單中的行。這個名稱不能包含空白空格之前或之後的顯示名稱。

  - **\* 別名**  這是郵件連絡人的別名。如果您變更它，它必須是唯一在組織中且必須是 64 個字元或更少。

  - **\* 外部的電子郵件地址**  這是郵件連絡人的主要 SMTP 位址和其外部電子郵件帳戶。傳送給此連絡人的電子郵件轉寄給此電子郵件地址。

  - 按一下 \[**更多選項\]**以顯示包含郵件連絡人帳戶的 OU。您必須使用 Active Directory 使用者和電腦移至不同的 OU 的連絡人。

## 連絡人資訊

使用**連絡人資訊**\] 區段來檢視或變更收件者的連絡資訊，例如郵寄地址和電話號碼。此資訊會顯示在通訊錄中。

## 組織

郵件連絡人的角色的詳細的資訊記錄在組織中使用 \[**組織**\] 區段中。此資訊會顯示在通訊錄中。此外，您可以建立可從例如 Outlook 的電子郵件用戶端存取虛擬組織圖。

  - \[職稱\]   使用這個方塊可檢視或變更連絡人的職稱。

  - **部門**  使用此方塊來檢視或變更連絡人的運作的部門。您可以使用此方塊來建立動態通訊群組的收件者條件及通訊清單。

  - **公司**  使用此方塊來檢視或變更其連絡人的運作方式的公司。您也可以使用此方塊來建立動態通訊群組的收件者條件。

  - **主管**   若要新增主管，按一下 **\[瀏覽\]**。 在 \[選取管理員\] 中選取人員，然後按一下 \[確定\]。

  - **直屬員工**  您無法修改此方塊。*直屬*為收件者向特定管理員報告。如果您已指定收件者的管理員，該收件者會顯示為直屬主管的信箱的詳細資料。例如，羅管理 Ann 和 Spencer，因此羅組織內容中的 \[**管理員**\] 方塊中指定 Ann 和 Spencer，且 Ann 和 Spencer 出現羅的信箱之屬性的**直屬員工**方塊中屬於郵件連絡人。

## 電子郵件選項

使用**電子郵件選項**\] 區段中新增或移除的郵件連絡人的 proxy 位址或編輯現有的 proxy 位址。郵件連絡人的主要 SMTP 位址也會顯示在這個部分，但是您無法將其變更。若要變更其，您必須變更連絡人的 \[**一般**\] 區段中的外部電子郵件地址。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>[<strong>電子郵件選項</strong>] 區段中Exchange Server 2013只有。不提供Exchange Online。</td>
</tr>
</tbody>
</table>


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


## 使用命令介面來變更郵件連絡人內容

郵件連絡人的屬性儲存在Active Directory與 Exchange 中。一般會使用**Get-Contact**和**Set-Contact** cmdlet 來檢視和變更組織和連絡人資訊內容。使用**Get-MailContact**和**Set-MailContact**指令程式來檢視或變更郵件相關屬性，例如電子郵件地址、 郵件提示、 自訂屬性及是否隱藏通訊清單的連絡人。

如需相關資訊，請參閱下列主題：

  - [Get-Contact](https://technet.microsoft.com/zh-tw/library/aa998258\(v=exchg.150\))

  - [Set-Contact](https://technet.microsoft.com/zh-tw/library/bb124535\(v=exchg.150\))

  - [Get-MailContact](https://technet.microsoft.com/zh-tw/library/bb124717\(v=exchg.150\))

  - [Set-MailContact](https://technet.microsoft.com/zh-tw/library/aa995950\(v=exchg.150\))

以下是使用命令介面變更郵件連絡人內容的範例。

此範例為郵件連絡人 Kai Axford 設定了 \[職稱\]、\[部門\]、\[公司\] 與 \[主管\] 內容。

    Set-Contact "Kai Axford" _-Title Consultant -Department "Public Relations" -Company Fabrikam -Manager "Karen Toh"

此範例將所有郵件連絡人的 CustomAttribute1 內容設定為值 PartTime，並且將它們從組織的通訊錄中隱藏。

    Get-MailContact | Set-MailContact -CustomAttribute1 PartTime -HiddenFromAddressListsEnabled $true

此範例將公共關係部門中的所有郵件連絡人的 CustomAttribute15 內容設定為值 TemporaryEmployee。

    Get-Contact -Filter "Department -eq 'Public Relations'" | Set-MailContact -CustomAttribute15 TemporaryEmployee

## 如何才能了解這是否正常運作？

若要確認您已成功變更郵件連絡人的內容，請執行下列動作：

  - 在 EAC 中，選取郵件連絡人，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示") 以檢視您變更的內容。

  - 在命令介面中使用**Get-Contact**和**Get-MailContact**指令程式來確認所做的變更。使用命令介面的一個優點是您可以檢視多個郵件連絡人的多個屬性。在上述其中所有郵件連絡人鎖 CustomAttribute1 屬性設定為 PartTime 與已從通訊錄中隱藏的範例中，執行下列命令來確認所做的變更。
    
        Get-MailContact | Fl Name,CustomAttribute1,HiddenFromAddressListsEnabled
    
    在上述範例中，所有公共關係部門之郵件連絡人的 CustomAttribute15 內容均已進行設定，請執行以下命令以驗證變更。
    
        Get-Contact -Filter "Department -eq 'Public Relations'" | Get-MailContact | FL Name,CustomAttribute15

## 大量編輯郵件連絡人

您可以使用 EAC 來變更選取多個郵件連絡人的內容。當您在 EAC 中的 \[連絡人\] 清單中選取兩個或多個郵件連絡人時，顯示可以大量編輯屬性的詳細資料窗格中。當您變更這些屬性的其中一個時，變更會套用至所有選取的收件者。

當您大量編輯郵件連絡人時，您可以變更以下內容區域：

  - **連絡人資訊**   變更街道、郵遞區號和城市名稱等共用內容。

  - **組織**   變更部門名稱、公司名稱以及選取的郵件連絡人或郵件使用者直屬經理等共用內容。

## 使用 EAC 來大量編輯郵件連絡人

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[連絡人\]。

2.  在連絡人清單中，選取兩個或多個郵件連絡人。您不想大量編輯郵件連絡人和郵件使用者的組合。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您可以選取多個相鄰的郵件連絡人按住 Shift 鍵及與 [第一個郵件連絡人，然後按一下 [您想要編輯的最後一個郵件連絡人。您也可以按住 Ctrl 鍵並按一下您想要編輯的每個選取多個郵件連絡人。</td>
    </tr>
    </tbody>
    </table>


3.  在 \[詳細資料\] 窗格的 \[大量編輯\] 下，按一下 \[連絡人資訊\] 或 \[組織\] 下的 \[更新\]。

4.  在內容頁上進行變更，然後儲存您的變更。

## 如何才能了解這是否正常運作？

若要驗證是否成功大量編輯信箱連絡人，請執行以下其中一個操作：

  - 在 EAC 中，選擇每一個您已大量編輯的信箱連絡人，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示") 以檢視您已變更的內容。

  - 在命令介面中使用**Get-Contact**指令程式來確認所做的變更。例如，之後在 EAC 中用於變更名為 a 材料 Corporation 廠商公司主管和所有郵件連絡人的 office 大量編輯功能。若要確認這些變更，您無法在命令介面中執行下列命令。
    
        Get-Contact -ResultSize unlimited -Filter {(Company -eq 'Adatum')} | fl Name,Office,Manager


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

