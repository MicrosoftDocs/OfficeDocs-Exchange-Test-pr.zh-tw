---
title: '管理動態通訊群組: Exchange Online Help'
TOCTitle: 管理動態通訊群組
ms:assetid: 8ef85d0a-41df-4b5c-b8e7-ca8d09c048ca
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb123722(v=EXCHG.150)
ms:contentKeyID: 50472361
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.CreateDynamicGroupWizardForm.CreateDynamicGroupInformationWizardPage
ms.translationtype: MT
---

# 管理動態通訊群組

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

動態通訊群組是擁有郵件功能的 Active Directory 群組物件，建立的用途在於加快 Microsoft Exchange 組織內大量傳送電子郵件與其他訊息的速度。

與一般通訊不同動態通訊群組是包含已定義的一組成員，成員資格清單的群組會計算每一則訊息傳送至\] 群組中，根據篩選器的時間與您定義的條件。當動態通訊群組傳送電子郵件訊息時，它會傳送給所有收件者在組織中符合該群組所定義的條件。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>動態通訊群組會包含任何收件者中Active Directory符合其篩選的屬性值。若要比對 filter 會修改收件者的屬性、 無法不經意會成為群組成員並啟動接收寄至群組的郵件收件者。周詳、 一致帳戶佈建程序會減少這個問題發生的機率。</td>
</tr>
</tbody>
</table>


## 開始之前有哪些須知？

  - 預估完成時間：2 至 5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「動態通訊群組」項目。

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

## 建立動態通訊群組

## 使用 EAC 建立動態通訊群組

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[群組\] \> \[新增\] \> \[動態通訊群組\]。

2.  
    
    在 \[新增動態通訊群組\] 頁面上，填妥以下方塊：
    
      - **\* 顯示名稱**  使用此方塊可輸入顯示名稱。此名稱會出現在共用的通訊錄，在 \[收件者： 電子郵件傳送到此群組中，並在 EAC 中的 \[群組\] 清單時的直線。顯示名稱為必要與讓人員辨識功能應易記。它也必須是唯一的樹系中。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>群組命名原則不應套用於動態通訊群組。</td>
        </tr>
        </tbody>
        </table>
    
      - **\* 別名**  使用此方塊可輸入群組名稱的別名。別名不可超過 64 個字元和必須是唯一的樹系中。當使用者輸入中 \[收件者的別名： 行的電子郵件訊息，則解析為群組的顯示名稱。
    
      - **描述**  使用此方塊可讓使用者知道群組目的說明群組。此描述會出現在共用的通訊錄中。
    
      - **組織單位**  您可以選取組織單位 (OU) 以外的預設值 （也就是收件者範圍）。如果收件者範圍會設為樹系中，預設值是設定為 \[使用者\] 容器Active Directory網域包含在其執行 EAC 中的電腦中。如果收件者範圍會設為特定的網域，預設會選取該網域中的 \[使用者\] 容器。如果收件者範圍會設為特定的 OU，預設會選取該 OU。
        
        若要選取不同的 OU，請按一下 \[瀏覽\]。此對話方塊會顯示樹系中在指定範圍內的所有 OU。選取想要的 OU，然後按一下 \[確定\]。
    
      - **擁有者** 動態通訊群組的擁有者是選擇性的。您可以依序按一下 \[**瀏覽**然後從清單中選取的使用者新增擁有者。

3.  
    
    使用 \[**成員**\] 區段中指定的收件者群組的類型和設定會決定成員資格的規則。選取其中一個下列方塊：
    
      - \[所有收件者類型\]   選擇此選項以傳送與此群組定義之條件相符的郵件給所有收件者類型。
    
      - \[只有下列收件者類型\]   符合此群組所定義之條件的郵件將被傳送給以下一或多個收件者類型：
        
          - **使用 Exchange 信箱的使用者**  如果您想要包含有 Exchange 信箱的使用者，選取此核取方塊。具有Exchange信箱的使用者是那些有一個使用者的網域帳戶和Exchange組織中的信箱。
        
          - **使用外部的電子郵件地址的使用者**  如果您想要包含有外部電子郵件地址的使用者，選取此核取方塊。具有外部電子郵件帳戶的使用者Active Directory、 中有使用者的網域帳戶但使用組織外部的電子郵件帳戶。這可讓全域通訊清單 (GAL) 中包含並且新增至通訊群組清單。
        
          - **資源信箱**  如果您想要包含Exchange資源信箱，選取這個核取方塊。資源信箱可讓您管理信箱，例如會議室或公司車輛透過公司資源。
        
          - **外部電子郵件地址的連絡人**  如果您想要包含有外部電子郵件地址的連絡人，選取此核取方塊。有外部電子郵件地址的連絡人的網域使用者帳戶中沒有Active Directory，但 GAL 中可用的外部電子郵件地址。
        
          - **擁有郵件功能的群組**  如果您想要加上安全性群組或已啟用郵件功能的通訊群組，選取此核取方塊。擁有郵件功能的群組的相似之通訊群組。傳送至擁有郵件功能的群組帳戶的電子郵件將傳送到數個收件者。

4.  
    
    按一下 \[新增規則\] 以定義此群組中的成員資格條件。

5.  從下拉式清單中選取下列收件者的屬性之一，並提供一個值。如果選取屬性的值符合您所定義的值，收件者會收到此群組傳送的訊息。
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>屬性</th>
    <th>傳送郵件給收件者，如果…...</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>收件者容器</strong></p></td>
    <td><p>收件者物件駐留在指定的網域或 OU 中。</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>縣/市</strong></p></td>
    <td><p>收件者的 [縣/市] 屬性與指定值相符。</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>公司</strong></p></td>
    <td><p>指定的值與收件者的 [公司] 屬性相符。</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>部門</strong></p></td>
    <td><p>指定的值與收件者的 [部門] 屬性相符。</p></td>
    </tr>
    <tr class="odd">
    <td><p>[自訂 attributeN] (其中 N 是從 1 到 15 的數字)</p></td>
    <td><p>指定的值與收件者的 CustomAttributeN 屬性相符。</p></td>
    </tr>
    </tbody>
    </table>
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您輸入所選屬性的值必須完全符合這些會出現在 [收件者的屬性。例如，如果您輸入<strong>華盛頓州或省</strong>，但收件者屬性的值是<strong>WA</strong>，則不符合條件。此外，您指定的文字型值不區分大小寫。例如，如果您指定<strong>Contoso公司</strong>屬性，將傳送訊息到收件者如果這個值是<strong>contoso</strong>。</td>
    </tr>
    </tbody>
    </table>


6.  在 \[**指定單字或片語**\] 視窗中，輸入 \[文字\] 方塊中的值。按一下 \[**新增**\] 及 \[**確定\]**。

7.  若要新增另一個定義成員資格的規則，在您之前建立的規則下方按一下 \[新增規則\]。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>若您要新增多個規則可以定義成員資格，收件者必須符合以接收郵件傳送至群組的每個規則的條件。換句話說，每個規則已連接到布林運算子<strong>與</strong>。</td>
    </tr>
    </tbody>
    </table>


8.  當您完成後，按一下 \[儲存\] 以建立動態通訊群組。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您想要指定規則屬性可在 EAC 中以外，您必須使用命令介面來建立動態通訊群組。請記住的篩選及條件動態通訊群組具有自訂的收件者篩選器可以管理設定只能使用命令介面。例如如何使用自訂查詢建立動態通訊群組中，請參閱上使用命令介面來建立動態通訊群組的下一節。</td>
</tr>
</tbody>
</table>


## 使用命令介面建立動態通訊群組

此範例建立僅包含信箱使用者的動態通訊群「組信箱使用者 DDG」。

    New-DynamicDistributionGroup -IncludedRecipients MailboxUsers -Name "Mailbox Users DDG" -OrganizationalUnit Users

本範例會建立動態通訊群組與自訂的收件者篩選器。動態通訊群組包含名為 Server1 的伺服器上的所有信箱使用者。

    New-DynamicDistributionGroup -Name "Mailbox Users on Server1" -OrganizationalUnit Users -RecipientFilter {((RecipientTypeDetails -eq 'UserMailbox' -and ServerName -eq 'Server1'))}

本範例會建立動態通訊群組與自訂的收件者篩選器。動態通訊群組包含在**CustomAttribute10**屬性值為"FullTimeEmployee"的所有信箱使用者。

    New-DynamicDistributionGroup -Name "Full Time Employees" -RecipientFilter {(RecipientTypeDetails -eq 'UserMailbox') -and (CustomAttribute10 -eq 'FullTimeEmployee')}

如需詳細的語法及參數資訊，請參閱 [New-DynamicDistributionGroup](https://technet.microsoft.com/zh-tw/library/bb125127\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要驗證是否成功建立動態通訊群組，請執行以下其中一個操作：

  - 在 EAC 中，瀏覽至 \[**收件者**\>**群組**。新的動態通訊群組會顯示在 \[群組\] 清單中。\[**群組類型**\] 下方類型是**動態通訊群組**。

  - 在命令介面中，執行以下命令以顯示新增之動態通訊群組的資訊。
    
        Get-DynamicDistributionGroup | FL Name,RecipientTypeDetails,RecipientFilter,PrimarySmtpAddress

## 變更動態通訊群組屬性

## 使用 EMC 變更動態通訊群組屬性

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[群組\]。

2.  在群組清單中，按一下您想檢視或變更的動態通訊群組，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在群組屬性頁面上，按一下下列區段其中之一以檢視或變更屬性。
    
      - General
    
      - Ownership
    
      - Membership
    
      - Delivery management
    
      - Message approval
    
      - Email options
    
      - MailTip
    
      - Group delegation

## \[一般\]

這個區段可用來檢視或變更群組的基本資訊。

  - **\* 顯示名稱**：這個名稱會出現在通訊錄的 \[收件者:\] 中：行以及 \[群組\] 清單中 (當電子郵件傳送至此群組時)。顯示名稱為必要項目，應以好記易懂為原則，以便他人分辨群組的用途。這個名稱在您的網域中也必須是唯一的。

  - **\* 別名**  這是出現在左邊的電子郵件地址的部分在 (@) 符號。如果您變更別名，群組的主要 SMTP 位址也會變更，並包含新的別名。此外，作為 proxy 地址群組就會保留與先前別名的電子郵件地址。

  - \[描述\]  這個方塊可用來描述群組，讓人員了解群組的用途。此描述會顯示在通訊錄和 EAC 的 \[詳細資料\] 窗格中。

  - \[從通訊清單中隱藏這個群組\]  如果您不想要讓使用者在通訊錄中看見這個群組，請選取此核取方塊。若要傳送電子郵件至此群組，寄件者必須在 \[收件者:\]或 \[副本:\]行中輸入群組的別名或電子郵件地址。

  - **組織單位**  此唯讀方塊顯示含有動態通訊群組的組織單位 (OU)。您必須使用 Active Directory 使用者和電腦移至不同的 OU 的群組。

## \[擁有權\]

這個區段可用來指派群組擁有者。動態通訊群組可以有一個擁有者。群組擁有者會出現在 \[Active Directory 使用者及電腦物件的**受管理的**索引標籤上。

您可以依序按一下 \[**瀏覽\]**從清單中選取擁有者新增擁有者。若要移除擁有者，請按一下 \[**清除\]**和 \[**儲存**。![\[移除\] 圖示](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[移除] 圖示")。

## \[成員資格\]

這個區段可用來變更用來決定群組的成員資格的準則。您可以刪除或變更現有的成員資格規則並加入新的規則。如要告訴您如何執行這項作業的程序，請參閱 ＜ 設定當您使用 EAC 來建立新的動態通訊群組的成員資格的程序中的步驟 3 。

## \[傳遞管理\]

您可使用此區段來管理哪些使用者可以傳送電子郵件給這個群組。

  - **僅寄件者內我的組織**  選取這個選項可讓您的組織將郵件傳送至群組中僅寄件者。這表示如果您的組織外的某個人加入此群組傳送電子郵件訊息，則被拒絕。這是預設設定。

  - \[我的組織內部和外部的寄件者\]   選取這個選項可讓任何人傳送郵件給群組。
    
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
    <td>如果您已設定群組只允許您組織中的寄件者傳送郵件給群組，即使外部連絡人列於此清單中，他們所傳送的電子郵件也會遭到拒絕。</td>
    </tr>
    </tbody>
    </table>


## \[訊息核准\]

使用此區段可設定用以仲裁群組的選項。仲裁者可在郵件送達群組成員前核准或拒絕傳送給群組的郵件。

  - \[傳送至此群組的訊息必須經過仲裁者的核准\]  這個核取方塊預設為未選取狀態。如果選取這個核取方塊，群組仲裁者會在內送郵件傳遞前加以審視。群組仲裁者可核准或拒絕內送郵件。

  - \[群組仲裁者\]  若要新增群組仲裁者，請按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。若要移除仲裁者，請選取該仲裁者，然後按一下 \[移除\]![\[移除\] 圖示](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[移除] 圖示")。如果已選取 \[傳送至此群組的訊息必須經過仲裁者的核准\]，但未選取仲裁者，傳送給該群組的郵件將會交由群組擁有者來核准。

  - \[寄件者不需要訊息核准\] 若要新增可略過此群組之仲裁的人員或群組，請按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。若要移除人員或群組，請選取項目，然後按一下 \[移除\]![\[移除\] 圖示](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[移除] 圖示")。

  - \[選取仲裁通知\]   使用此區段可設定使用者接收郵件核准相關通知的方式。
    
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


  - \[編輯\]   若要變更與群組相關的電子郵件地址，先從清單中選擇然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。
    
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


  - \[移除\]   若要刪除與群組相關的電子郵件地址，先從清單中選擇然後按一下 \[移除\]![\[移除\] 圖示](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[移除] 圖示")。

  - \[依照套用至此收件者的電子郵件地址原則自動更新電子郵件地址\]  選取此核取方塊，可讓收件者的電子郵件地址自動依照組織內電子郵件地址原則的變更而更新。預設會選取此方塊。

## \[郵件提示\]

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


## \[群組代理人\]

本區段可用來指派權限給使用者 (稱為「代理人」)，以允許使用者以群組身份傳送郵件，或代表群組來傳送郵件。您可以指派下列權限：

  - \[以群組身份傳送\]  此權限允許代理人以群組身份傳送郵件。指派此權限之後，代理人即可將群組新增至 \[寄件者\] 行，以表明郵件是由群組所傳送。

  - **傳送代理者**  此權限也可讓代理人代表群組傳送郵件。指派此權限後，代理人具有**從**線條上新增群組的選項。會顯示群組所傳送郵件，並會說它已由代理人代替群組傳送。

若要指派權限給代理人，請按一下適當權限下方的 \[新增\]，即會顯示 \[選取收件者\] 頁面，其會顯示一份 Exchange 組織中可指派權限的所有收件者清單。選取想要的收件者，然後按一下 \[確定\]。您也可以在搜尋方塊中輸入收件者的名稱，然後按一下 \[搜尋\]，以搜尋特定的收件者。

## 使用命令介面變更動態通訊群組屬性

使用**Get-DynamicDistributionGroup**和**Set-DynamicDistributionGroup** cmdlet 來檢視和變更動態通訊群組的屬性。使用命令介面的優點是能夠變更屬性的 eac 並變更多個群組的屬性。如需哪些參數會對應至通訊群組內容，請參閱下列主題：

  - [Get-DynamicDistributionGroup](https://technet.microsoft.com/zh-tw/library/bb124762\(v=exchg.150\))

  - [Set-DynamicDistributionGroup](https://technet.microsoft.com/zh-tw/library/bb123796\(v=exchg.150\))

這裡提供一些使用命令介面變更動態通訊群組屬性的範例。

此範例會變更以下組織中所有動態通訊群組的參數：

  - \[隱藏通訊錄中所有動態通訊群組\]

  - 設定傳送至群組的郵件大小上限為 5MB

  - \[啟用仲裁\]

  - 指派系統管理員作為群組仲裁者

<!-- end list -->

    Get-DynamicDistributionGroup -ResultSize unlimited | Set-DynamicDistributionGroup -HiddenFromAddressListsEnabled $true -MaxReceiveSize 5MB -ModerationEnabled $true -ModeratedBy administrator

此範例會新增 Proxy SMTP 電子郵件信箱地址 Seattle.Employees@contoso.com 給 \[全部員工\] 群組。

    Set-DynamicDistributionGroup -Identity "All Employees" -EmailAddresses SMTP:All.Employees@contoso.com, smtp:Seattle.Employees@contoso.com

## 如何才能了解這是否正常運作？

若要驗證是否成功變更動態通訊群組的屬性，請執行以下其中一個操作：

  - 在 EAC 中，選取群組，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示") 以檢視所變更的內容和功能。依據您所變更的內容而定，其有可能會顯示在您所選群組的 \[詳細資料\] 窗格中。

  - 在命令介面中使用**Get-DynamicDistributionGroup**指令程式來確認所做的變更。使用命令介面的一個優點是您可以檢視針對多個群組的多個屬性。在第一個範例中，您會執行下列命令來確認新的值。
    
        Get-DynamicDistributionGroup -ResultSize unlimited | fl Name,HiddenFromAddressListsEnabled,MaxReceiveSize,ModerationEnabled,ModeratedBy
    
    針對上述變更郵件限制的範例中，請執行此命令。
    
        Get-Mailbox -OrganizationalUnit "Marketing" | fl Name,IssueWarningQuota,ProhibitSendQuota,ProhibitSendReceiveQuota,UseDatabaseQuotaDefaults

