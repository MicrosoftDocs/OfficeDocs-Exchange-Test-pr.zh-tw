---
title: '管理 Exchange 2013 中的就地封存: Exchange 2013 Help'
TOCTitle: 管理 Exchange 2013 中的就地封存
ms:assetid: 49ef4a3e-d209-4fb2-80a3-6132b0f69bd0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ651146(v=EXCHG.150)
ms:contentKeyID: 50473067
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理 Exchange 2013 中的就地封存

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-02-01_

就地封存可協助您帶來需要個人存放區 (.pst) 檔案，並讓您以符合組織的郵件保留和 eDiscovery 需求取回貴組織的郵件資料的控制權。與封存功能，使用者可以使用MicrosoftOutlook和Outlook Web App是可以存取封存信箱中儲存的郵件。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「原有範圍封存」項目。

  - 它不支援讓使用者的主要信箱位於較舊的Exchange版本比使用者的封存。只有在使用者的主要信箱仍位於 Exchange 2010，您必須以 Exchange 2013 移動的同時將封存移至 Exchange 2013。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 您要執行的工作

## 建立信箱並啟用內部部署封存

## 使用 EAC

1.  瀏覽至 \[收件者\] \> \[信箱\]。

2.  按一下 \[新增\] \> \[使用者信箱\]。

3.  在 **\[新增使用者信箱\]** 頁面的 **\[別名\]** 方塊中，輸入使用者的別名。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果方塊為空白，系統會將您輸入 <strong>[使用者登入名稱]</strong> 方塊中的值當作別名。</td>
    </tr>
    </tbody>
    </table>


4.  
    
    選取下列其中一個選項：
    
      - **現有的使用者**   按一下此按鈕，然後再按一下 **\[瀏覽\]** 可開啟 **\[選取使用者 – 整個樹系\]** 對話方塊。這個對話方塊會在樹系中顯示 Active Directory 使用者帳戶清單，而這些使用者帳戶沒有郵件功能或不具有 Exchange 信箱。選取您要啟用郵件的使用者帳戶，然後按一下 \[確定\]。如果選取此選項，不需要提供使用者帳戶資訊，因為 Active Directory 已經存在這些資訊。
    
      - **新增使用者**   按一下此按鈕可在 Active Directory 中建立新的使用者帳戶，並且為這位使用者建立信箱。如果選取此選項，必須提供所需的使用者帳戶資訊。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>與使用者信箱關聯的 Active Directory 帳戶必須與 Exchange 伺服器位於同一樹系。若要為信任樹系中的使用者帳戶建立信箱，必須建立連結的信箱。如需詳細資訊，請參閱<a href="manage-linked-mailboxes-exchange-2013-help.md">管理連結的信箱</a>。</td>
    </tr>
    </tbody>
    </table>


5.  
    
    按一下 **\[更多選項\]** 以配置下列設定。
    
      - **信箱資料庫**   按一下 **\[瀏覽\]** 可選取儲存信箱的信箱資料庫。如果您未選取資料庫，Exchange 會自動指派一個資料庫。
    
      - **封存**   選取此核取方塊可為信箱建立封存信箱。如果您建立封存信箱，則信箱項目將依據預設保留原則設定或您的定義，自動從主要信箱移動到封存。
        
        按一下 \[瀏覽\] 選取位於本機樹系中的資料庫，用來儲存封存信箱。
        
        若要深入了解，請參閱[就地封存 in Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md)。
    
      - **通訊錄原則**   使用這個清單可選取信箱的通訊錄原則 (ABP)。ABP 包含全域通訊清單 (GAL)、離線通訊錄 (OAB)、會議室清單和一組通訊清單。在指派 ABP 給信箱使用者時，他們就可以存取在 Outlook 和 Outlook Web App 中自訂的 GAL。若要深入了解，請參閱[通訊錄原則](address-book-policies-exchange-2013-help.md)。

6.  
    
    完成作業後，按一下 \[儲存\] 建立信箱。

## 使用命令介面

此範例會在 Active Directory 中建立使用者 Chris Ashton，並在信箱資料庫 DB01 上建立信箱及啟用封存。必須在下次登入時重設密碼。為了設定密碼的初始值，此範例會建立變數 ($password)、提示您輸入密碼，並將該密碼指派給變數作為 SecureString 物件。

    $password = Read-Host "Enter password" -AsSecureString
    New-Mailbox -UserPrincipalName chris@contoso.com -Alias chris -Archive -Database "DB01" -Name ChrisAshton -OrganizationalUnit Users -Password $password -FirstName Chris -LastName Ashton -DisplayName "Chris Ashton" 

如需詳細的語法及參數資訊，請參閱 [New-Mailbox](https://technet.microsoft.com/zh-tw/library/aa997663\(v=exchg.150\))。

## 如何知道這是否正常運作？

若要驗證是否成功以內部部署封存建立使用者信箱，請執行以下其中一個操作：

  - 在 EAC 中，瀏覽至 **\[收件者\]** \> **\[信箱\]**，然後在清單中選取新使用者信箱。在詳細資料窗格的 **\[就地封存\]** 下，確認此項目的設定為 **\[已啟用\]**。按一下 \[檢視詳細資料\] 檢視封存內容，包括封存狀態，以及建立封存的信箱資料庫。

  - 在命令介面中，執行下列命令來顯示關於新使用者信箱與封存的資訊。
    
        Get-Mailbox <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress,*Archive*

  - 在命令介面中，使用 **Test-ArchiveConnectivity** 指令程式測試封存的連線。如需如何測試封存連線的範例，請參閱 [Test-ArchiveConnectivity](https://technet.microsoft.com/zh-tw/library/hh529914\(v=exchg.150\)) 中的＜範例＞一節。

## 啟用現有信箱的內部部署封存

可為擁有信箱卻未啟用封存的現有使用者建立封存。稱之為現有信箱的 *「啟用封存」*。

## 使用 EAC

1.  瀏覽至 \[收件者\] \> \[信箱\]。

2.  選取信箱。

3.  在詳細資料窗格的 **\[就地封存\]** 下，按一下 **\[啟用\]**。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您也可以選取多個信箱 (使用 Shift 或 Ctrl 鍵) 來大量啟用封存。選取多個信箱後，請在詳細資料窗格中按一下 <strong>[其他選項]</strong>。接著按一下 <strong>[封存]</strong> 下方的 <strong>[啟用]</strong>。</td>
    </tr>
    </tbody>
    </table>


4.  在 **\[建立就地儲存\]** 頁面上，按一下 **\[確定\]** 以讓 Exchange 自動選取封存的信箱資料庫，或按一下 **\[瀏覽\]** 來指定封存的信箱資料庫。

## 使用命令介面

此範例會啟用 Tony Smith 之信箱的封存。

    Enable-Mailbox "Tony Smith" -Archive

此範例會擷取資料庫 DB01 中的信箱，該資料庫未啟用內部部署或雲端架構封存，也沒有以 DiscoverySearchMailbox 為開頭的名稱。其將結果以管線輸出至 **Enable-Mailbox** 指令程式來啟用所有在信箱資料庫 DB01 上的封存。

    Get-Mailbox -Database DB01 -Filter {ArchiveGuid -Eq $null -AND ArchiveDomain -eq $null -AND Name -NotLike "DiscoverySearchMailbox*"} | Enable-Mailbox -Archive

如需詳細的語法及參數資訊，請參閱 [Enable-Mailbox](https://technet.microsoft.com/zh-tw/library/aa998251\(v=exchg.150\)) 與 [Get-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123685\(v=exchg.150\))。

## 如何知道這是否正常運作？

若要驗證是否成功為現有使用者信箱啟用內部部署封存，請執行以下其中一個操作：

  - 在 EAC 中，瀏覽至 **\[收件者\]** \> **\[信箱\]**，然後在清單中選取信箱。在詳細資料窗格的 **\[就地封存\]** 下，確認此項目的設定為 **\[已啟用\]**。按一下 \[檢視詳細資料\] 檢視封存內容，包括封存狀態，以及建立封存的信箱資料庫。

  - 在命令介面中，執行下列命令來顯示關於新增封存的資訊。
    
        Get-Mailbox <Name> | FL Name,*Archive*

  - 在命令介面中，使用 **Test-ArchiveConnectivity** 指令程式測試封存的連線。如需如何測試封存連線的範例，請參閱[Test-ArchiveConnectivity](https://technet.microsoft.com/zh-tw/library/hh529914\(v=exchg.150\))中的範例。

## 停用內部部署封存

為了進行疑難排解，或是如果您正把信箱移至不支援個人封存的 Exchange 版本，您可能會想要停用使用者的個人 (內部部署) 或原有範圍封存。如果您停用內部部署封存，封存中的所有資訊將保留在信箱資料庫中，直到信箱保留時間已屆，該封存便會永久刪除(依預設，Exchange 將保留已中斷連線的信箱，包括封存信箱，持續三十天)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>停用封存會將封存從信箱移除，並且在信箱資料庫中將其標示為刪除。</td>
</tr>
</tbody>
</table>


如果您想要將內部部署封存重新連線到該信箱，可以使用 [Connect-Mailbox](https://technet.microsoft.com/zh-tw/library/aa997878\(v=exchg.150\)) 指令程式搭配 *Archive* 參數。

## 使用 EAC

1.  瀏覽至 \[收件者\] \> \[信箱\]。

2.  選取信箱。

3.  在詳細資料窗格的 **\[就地封存\]** 下，按一下 **\[停用\]**。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您也可以選取多個信箱 (使用 Shift 或 Ctrl 鍵) 來大量停用封存。選取多個信箱後，請在詳細資料窗格中按一下 <strong>[其他選項]</strong>。接著按一下 <strong>[封存]</strong> 下方的 <strong>[停用]</strong>。</td>
    </tr>
    </tbody>
    </table>


## 使用命令介面

此範例會停用 Chris Ashton 信箱的封存。它不會停用信箱。

    Disable-Mailbox -Identity "Chris Ashton" -Archive

如需詳細的語法及參數資訊，請參閱 [Disable-Mailbox](https://technet.microsoft.com/zh-tw/library/aa997210\(v=exchg.150\))。

## 如何知道這是否正常運作？

若要確認您是否已成功停用封存，執行下列操作：

  - 在 EAC 中選取信箱。接著，在詳細資料窗格的 **\[就地封存\]** 下查看其封存狀態。

  - 在命令介面中，執行以下命令來查看信箱使用者的封存屬性。
    
        Get-Mailbox -Identity "Chris Ashton" | Format-List *Archive*
    
    若封存已停用，下列值將回復為封存相關屬性。
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>屬性</th>
    <th>值</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>ArchiveDatabase (用於內部部署封存)</p></td>
    <td><p>&lt;空白&gt;</p></td>
    </tr>
    <tr class="even">
    <td><p>ArchiveState</p></td>
    <td><p><code>None</code></p></td>
    </tr>
    <tr class="odd">
    <td><p>DisabledArchiveDatabase (用於內部部署封存)</p></td>
    <td><p>&lt;信箱資料庫的名稱&gt;</p></td>
    </tr>
    <tr class="even">
    <td><p>DisabledArchiveGuid</p></td>
    <td><p>&lt;停用封存的 GUID&gt;</p></td>
    </tr>
    </tbody>
    </table>


## 連接內部部署封存

當您停用封存信箱時，將會中斷連接。中斷連線的封存信箱會在指定的時間內保留在信箱資料庫中。Exchange 預設會保留中斷連線的封存 30 天。在這段時間內，可以藉由讓封存與現有信箱產生關聯的方式來復原個人封存。您可以修改已刪除信箱的保留期間，來增減保留已刪除信箱或封存的時間。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若您停用使用者封存然後啟用相同使用者的封存，使用者將獲得新的封存。新的封存將不會包含在使用者連線中斷的封存中的資料。若您想要重新連接使用者與他或她的連線中斷封存，必須執行此步驟。</td>
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
<td>您不可使用 EAC 來將連線中斷的封存連接至信箱使用者。</td>
</tr>
</tbody>
</table>


## 使用命令介面

1.  如果不知道封存的名稱，您可以透過執行下列命令，在命令介面中檢視。此範例會擷取 DB01 信箱資料庫，以管線輸出至 **Get-MailboxStatistics** 指令程式來擷取資料庫上所有信箱的信箱統計資料，然後使用 **Where-Object** 指令程式來篩選結果並擷取連線中斷封存的清單。命令顯示關於每個封存的額外資訊，如 GUID 與項目計數。
    
        Get-MailboxDatabase "DB01" | Get-MailboxStatistics | Where {($_.DisconnectDate -ne $null) -and ($_.IsArchiveMailbox -eq $true)} | Format-List

2.  將封存連線至主要信箱。這個範例將 Chris Ashton 的封存連線至 Chris Ashton 的主要信箱，並使用 GUID 作為封存的識別。
    
        Enable-Mailbox -ArchiveGuid "8734c04e-981e-4ccf-a547-1c1ac7ebf3e2" -ArchiveDatabase "DB01" -Identity "Chris Ashton"

如需詳細的語法及參數資訊，請參閱下列主題：

  - [Get-MailboxDatabase](https://technet.microsoft.com/zh-tw/library/bb124924\(v=exchg.150\))

  - [Get-MailboxStatistics](https://technet.microsoft.com/zh-tw/library/bb124612\(v=exchg.150\))

  - [Enable-Mailbox](https://technet.microsoft.com/zh-tw/library/aa998251\(v=exchg.150\))

## 如何知道這是否正常運作？

若要確認您是否已成功將連線中斷的封存連接至信箱使用者，執行下列命令介面命令來擷取信箱使用者的封存屬性並驗證回復至 *ArchiveGuid* 與 *ArchiveDatabase* 屬性的值：

    Get-Mailbox -Identity "Chris Ashton" | Format-List *Archive*

