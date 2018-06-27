---
title: '建立使用者信箱: Exchange 2013 Help'
TOCTitle: 建立使用者信箱
ms:assetid: 51a8b4c6-a53e-41c5-8bb1-ea4c0eaa0174
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ991919(v=EXCHG.150)
ms:contentKeyID: 52062542
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 建立使用者信箱

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2013-04-12_

信箱位於 Exchange 組織中的資訊工作者所使用的最常見收件者類型。每個信箱相關聯的 Active Directory 使用者帳戶。使用者可以使用信箱傳送及接收的郵件，並儲存郵件、 約會 （英文）、 工作、 記事及文件。使用 EAC 或命令介面來建立使用者信箱。

您也可以建立使用者信箱的現有使用者的 Active Directory 使用者帳戶但沒有對應的信箱。這就是所謂*信箱啟用*現有使用者。

## 開始之前有哪些須知？

  - 估計每個使用者信箱工作的完成時間：2 至 5 分鐘。

  - 當您建立新的使用者信箱時，您無法使用單引號 （'） 或引號 （"） 在 \[別名\] 或 \[使用者登入名稱因為這些字元不受支援。如果您建立新的信箱使用不受支援的字元，可能不會收到錯誤，雖然這些字元會導致問題稍後。例如，已指派存取權限給使用不受支援的字元建立信箱的使用者可能會遇到的問題或未預期的行為。

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

## 建立使用者信箱

## 使用 EAC 建立使用者信箱

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[信箱\]。

2.  按一下 \[新增\] \> \[使用者信箱\]。

3.  在 \[**新的使用者信箱**\] 頁面上 \[**別名**\] 方塊中輸入使用者的別名，這會指定使用者的電子郵件別名。使用者的別名為左側的電子郵件地址的部分在 (@) 符號。其必須是唯一的樹系中。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果方塊為空白，會使用 [使用者登入名稱] 的使用者名稱部分之數值作為電子郵件別名。</td>
    </tr>
    </tbody>
    </table>


4.  
    
    選取下列其中一個選項：
    
      - \[現有使用者\]   選取可啟用現有使用者的郵件，並建立信箱。
        
        按一下 \[**瀏覽\]**以開啟 \[**選取使用者 – 整個樹系**\] 對話方塊。此對話方塊會顯示未啟用郵件功能或沒有 Exchange 信箱的樹系中 Active Directory 使用者帳戶清單。選取您想要啟用郵件功能的使用者帳戶，然後按一下 \[**確定\]**。如果您選取這個選項，您不需要因為這項資訊已經存在於 Active Directory 提供使用者帳戶資訊。
    
      - **新的使用者**  選取 \[Active Directory 中建立新的使用者帳戶並建立該使用者的信箱。如果您選取這個選項，您必須提供必要的使用者帳戶資訊。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Active Directory帳戶相關聯使用者信箱必須位於相同的樹系Exchange伺服器。若要建立的信箱位於受信任的樹系中的使用者帳戶，您必須建立連結的信箱。請參閱<a href="manage-linked-mailboxes-exchange-2013-help.md">管理連結的信箱</a>。</td>
    </tr>
    </tbody>
    </table>


5.  
    
    如果您在步驟 4 中選取**新的使用者**，填妥下列方塊在**新的使用者信箱**\] 頁面上。否則請跳至步驟 7。
    
      - **名字** 使用此方塊輸入使用者的名字。
    
      - **縮寫** 使用此方塊輸入使用者的縮寫。
    
      - **姓氏** 使用此方塊輸入使用者的姓氏。
    
      - **\* 顯示名稱**  使用此方塊可輸入使用者的顯示名稱。這是在 EAC 中與共用的通訊錄中的信箱清單中所列的名稱。根據預設，此方塊會填入您在 \[**名字**、**縮寫**和**姓氏**\] 方塊中輸入的名稱。如果您未使用這些方塊，您必須仍輸入名稱在此方塊因為有必要。名稱不可超過 64 個字元。
    
      - **\* 名稱**  使用此方塊可輸入使用者的名稱。這是在Active Directory中所列的名稱。此方塊也會填入您在 \[**名字**、**縮寫**和**姓氏**\] 方塊中輸入的名稱。如果您未使用這些方塊，您仍必須在因為此方塊所輸入的名稱。此名稱也不可超過 64 個字元。
    
      - \[組織單位\]   您可選取預設值以外但在收件者範圍中的組織單位 (OU)。如果將收件者範圍設定為樹系，則預設值會設定為正在執行 EAC 的電腦包含在內的 Active Directory 網域中出現的 \[使用者\] 容器。若收件者範圍設為特定網域，則依預設會選取該網域的使用者容器。若收件者範圍設為特定 OU，則依預設會選取該 OU。
        
        若要選取不同的 OU，請按一下 \[瀏覽\]。此對話方塊會顯示樹系中在指定範圍內的所有 OU。選取所需的 OU，然後按一下 \[確定\]。
    
      - **\* 使用者登入名稱**  使用此方塊可輸入使用者將會使用登入至信箱與登入網域的名稱。使用者登入名稱所組成的左側的使用者名稱在 (@) 符號和右邊的後置詞。通常，尾碼為件所在的使用者帳戶的網域名稱。請注意您無法使用單引號 （'） 或引號 （"） 在使用者登入名稱因為這些字元不受支援。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>如果使用者名稱的值不同於 [別名] 方塊中使用的值，則使用者的電子郵件地址和使用者登入名稱將不同。</td>
        </tr>
        </tbody>
        </table>
    
      - **\* 新密碼**   使用此方塊以輸入使用者必須使用以登入信箱的密碼。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>請確定您提供的密碼符合您正在其中建立使用者帳戶之網域的密碼長度、複雜性和歷程需求。</td>
        </tr>
        </tbody>
        </table>
    
      - \[\* 確認密碼\]   使用這個方塊確認您在 \[密碼\] 方塊中輸入的密碼。
    
      - **下次登入需要密碼變更**   如果您想要使用者在首次登入信箱時重設密碼，請選取此方塊。
        
        如果您選取此核取方塊，在第一部登入、 新的使用者將會提示與要變更密碼\] 對話方塊。不允許使用者執行任何工作直到成功變更密碼。

6.  
    
    按一下 \[**更多選項**來設定下列方塊。否則，請跳至步驟 7 儲存新的使用者信箱。
    
      - \[指定信箱資料庫\]   使用這個選項指定信箱資料庫，而不讓 Exchange 為您選取資料庫。按一下 \[瀏覽\] 以開啟 \[選取信箱資料庫\] 對話方塊。這個對話方塊會列出您 Exchange 組織中所有的信箱資料庫。依預設，信箱資料庫是以名稱排序。您也可以按一下對應欄位的標題，依照伺服器名稱或版本來排序資料庫。選取您要使用的信箱資料庫，然後按一下 \[確定\]。
    
      - **此使用者建立本機封存存放區**  選取此核取方塊來建立封存信箱的信箱。如果您建立封存信箱，信箱項目將會移動自動從主要信箱的封存，根據預設保留原則設定\] 或 \[那些您定義。
        
        按一下 \[瀏覽\] 選取位於本機樹系中的資料庫，用來儲存封存信箱。
        
        若要深入了解，請參閱[就地封存 in Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md)。
    
      - **通訊錄原則**  使用此選項可指定通訊錄原則 (ABP) 信箱。Abp 包含全域通訊清單 (GAL)、 離線通訊錄 (OAB)、 \[聊天室\] 清單中，以及一組通訊清單。時指派給使用者的信箱、 ABP 提供這些存取 Outlook 和 Outlook Web App 中的自訂 GAL。若要深入了解，請參閱[通訊錄原則](address-book-policies-exchange-2013-help.md)。
        
        在下拉式清單中，選取要與這個信箱產生關聯的原則。

7.  
    
    完成作業後，按一下 \[儲存\] 建立信箱。

## 使用命令介面建立使用者信箱

此範例會建立一個名為 Pilar Pinilla 的新使用者帳戶及信箱，其詳細資料如下：

  - 別名是 pilarp

  - 名字是 Pilar，姓氏是 Pinilla

  - 該名稱與顯示的名稱是 Pilar Pinilla

  - 使用者登入名稱是 pilarp@contoso.com

  - 密碼是 Pa$$word1

  - 會在預設的 OU 中建立信箱。若要指定不同的 OU，您可以使用*OrganizationalUnit*參數。

<!-- end list -->

    New-Mailbox -Alias pilarp -Name "Pilar Pinilla" -FirstName Pilar -LastName Pinilla -DisplayName "Pilar Pinilla" -UserPrincipalName pilarp@contoso.com -Password (ConvertTo-SecureString -String 'Pa$$word1' -AsPlainText -Force)

如需語法及參數資訊，請參閱 [New-Mailbox](https://technet.microsoft.com/zh-tw/library/aa997663\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要驗證是否成功建立使用者信箱，請執行以下其中一個操作：

  - 在 EAC 中，瀏覽至 \[**收件者**\>**信箱**。新的使用者信箱會顯示在 \[信箱\] 清單中。**信箱類型**\] 底下類型是**使用者**。

  - 在命令介面中，執行以下命令以顯示新使用者信箱的資訊。
    
        Get-Mailbox <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress

## 建立現有使用者的信箱

您也可以建立使用者信箱的現有使用者的 Active Directory 使用者帳戶但沒有對應的信箱。這就是所謂*信箱啟用*現有使用者。您 enable-mailbox 之後的現有使用者，使用者可以傳送及接收電子郵件訊息。

## 使用 EAC 為現有的使用者建立信箱

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[信箱\]。

2.  按一下 \[新增\] \> \[使用者信箱\]。

3.  在 \[**新的使用者信箱**\] 頁面上 \[**別名**\] 方塊中輸入使用者的別名，這會指定使用者的電子郵件別名。使用者的別名為左側的電子郵件地址的部分在 (@) 符號。其必須是唯一的樹系中。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果方塊為空白，會使用 [使用者登入名稱] 的使用者名稱部分之數值作為電子郵件別名。</td>
    </tr>
    </tbody>
    </table>


4.  按一下 \[現有的使用者\]。

5.  按一下 \[**瀏覽\]**以開啟 \[**選取使用者 – 整個樹系**\] 對話方塊。此對話方塊會顯示未啟用郵件功能或沒有 Exchange 信箱的樹系中 Active Directory 使用者帳戶清單。選取您想要啟用郵件功能的使用者帳戶，然後按一下 \[**確定\]**。
    
    當您為現有使用者建立信箱後，您不必提供帳戶資訊，因為此資訊已存在於 Active Directory 中。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Active Directory帳戶相關聯使用者信箱必須位於相同的樹系Exchange伺服器。若要建立的信箱位於受信任的樹系中的使用者帳戶，您必須建立連結的信箱。請參閱<a href="manage-linked-mailboxes-exchange-2013-help.md">管理連結的信箱</a>。</td>
    </tr>
    </tbody>
    </table>


6.  按一下 \[**更多選項**來設定下列方塊。否則，請跳至步驟 7 儲存新的使用者信箱。
    
      - \[指定信箱資料庫\]   使用這個選項指定信箱資料庫，而不讓 Exchange 為您選取資料庫。按一下 \[瀏覽\] 以開啟 \[選取信箱資料庫\] 對話方塊。這個對話方塊會列出您 Exchange 組織中所有的信箱資料庫。依預設，信箱資料庫是以名稱排序。您也可以按一下對應欄位的標題，依照伺服器名稱或版本來排序資料庫。選取您要使用的信箱資料庫，然後按一下 \[確定\]。
    
      - **此使用者建立本機封存存放區**  選取此核取方塊來建立封存信箱的信箱。如果您建立封存信箱，信箱項目將會移動自動從主要信箱的封存，根據預設保留原則設定\] 或 \[那些您定義。
        
        按一下 \[瀏覽\] 選取位於本機樹系中的資料庫，用來儲存封存信箱。
        
        若要深入了解，請參閱[就地封存 in Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md)。
    
      - **通訊錄原則**  使用此選項可指定通訊錄原則 (ABP) 信箱。Abp 包含全域通訊清單 (GAL)、 離線通訊錄 (OAB)、 \[聊天室\] 清單中，以及一組通訊清單。時指派給使用者的信箱、 ABP 提供這些存取 Outlook 和 Outlook Web App 中的自訂 GAL。若要深入了解，請參閱[通訊錄原則](address-book-policies-exchange-2013-help.md)。
        
        在下拉式清單中，選取要與這個信箱產生關聯的原則。

7.  完成作業後，按一下 \[儲存\] 建立信箱。

## 使用命令介面為現有的使用者創立信箱

此範例會為名為 UsersMailboxDatabase 的 Exchange 資料庫上的現有使用者 estherv@contoso.com 建立一個信箱。

    Enable-Mailbox estherv@contoso.com -Database UsersMailboxDatabase

您也可以使用**Enable-Mailbox**指令程式來啟用多個使用者的郵件功能。您可以將傳送**Get-User**指令程式在**Enable-Mailbox** cmdlet 的結果。當您執行**Get-User**指令程式時，您必須傳回都已啟用郵件功能的使用者。若要這樣做，您需要使用*RecipientTypeDetails*參數指定使用者的值。您也可以限制所要求符合您指定的準則的使用者使用*Filter*參數傳回的結果。接著，您將傳送到**Enable-Mailbox** cmdlet 的結果。

例如，以下命令會啟用原本未啟用信箱且 **UserPrincipalName** 屬性中有值之使用者的信箱，確保您不會不小心將系統帳戶轉換為信箱。

    Get-User -RecipientTypeDetails User -Filter { UserPrincipalName -ne $Null } | Enable-Mailbox

如需語法及參數的相關資訊，請參閱 [Enable-Mailbox](https://technet.microsoft.com/zh-tw/library/aa998251\(v=exchg.150\)) 和 [Get-User](https://technet.microsoft.com/zh-tw/library/aa996896\(v=exchg.150\)).

如需管線的詳細資訊，請參閱[管線](https://technet.microsoft.com/zh-tw/library/aa998260\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要驗證是否成功建立現有使用者的信箱，請執行以下其中一個操作：

  - 在 EAC 中，瀏覽至 \[**收件者**\>**信箱**。新信箱功能的使用者會顯示在 \[信箱\] 清單中。**信箱類型**\] 底下類型是**使用者**。

  - 在命令介面中，執行以下命令以顯示新啟用信箱之使用者的資訊。
    
        Get-Mailbox <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress
    
    請注意，*RecipientTypeDetails* 的屬性值是 `UserMailbox`。

