---
title: '連線或還原已刪除的信箱: Exchange 2013 Help'
TOCTitle: 連線或還原已刪除的信箱
ms:assetid: a5e6ac44-5901-4eab-9017-c6fae80a0f83
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ863438(v=EXCHG.150)
ms:contentKeyID: 50554043
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 連線或還原已刪除的信箱

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-05-04_

您可以使用 EAC 或命令介面來連線至 Active Directory 使用者帳戶的刪除的信箱。當您刪除信箱時，Exchange 會保留在信箱資料庫中的信箱並切換至已停用狀態的信箱。也會刪除相關聯的 Active Directory 使用者帳戶。信箱會從信箱資料庫保留之前刪除的信箱保留期間到期，其中會根據預設，然後它的 30 天永久刪除 （或*清除*）。

Exchange 信箱資料庫會永久刪除已刪除的信箱，直到您可以使用 EAC 或命令介面來連線至 Active Directory 使用者帳戶。您也可以使用命令介面來還原已刪除的信箱的內容至現有的信箱。

若要深入了解中斷連線信箱與執行其他相關管理工作的詳細資訊，請參閱以下主題：

  - [中斷連線的信箱](disconnected-mailboxes-exchange-2013-help.md)

  - [停用或刪除信箱](disable-or-delete-a-mailbox-exchange-2013-help.md)

  - [連線已停用的信箱](connect-a-disabled-mailbox-exchange-2013-help.md)

  - [永久刪除信箱](permanently-delete-a-mailbox-exchange-2013-help.md)

## 開始之前有哪些須知？

  - 預估完成時間：2 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「收件者佈建權限」一節。

  - 若要連線至已刪除的信箱的 Active Directory 中建立新的使用者帳戶。或使用**Get-User**指令程式在命令介面中確認您想要連線至存在於已刪除的信箱且不是與另一個信箱相關聯的 Active Directory 使用者帳戶。若要連線至使用者帳戶的已刪除的信箱，帳戶必須存在且*RecipientType*屬性的值設為`User`，指出該帳戶不是尚未擁有信箱功能。
    
    若是內部部署 Exchange 的組織，您也可以在 \[Active Directory 使用者及電腦\] 中確認此資訊。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>當您連接被刪除的連結信箱、資源信箱或共用信箱時，您必須停用欲連接信箱的 Active Directory 使用者帳戶。</td>
    </tr>
    </tbody>
    </table>


  - 若要確認您想連接使用者帳戶的被刪除信箱是否仍存在於信箱資料庫中，而且不是虛刪除的信箱，請執行下列命令。
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisplayName,Database,DisconnectReason
    
    已刪除的信箱已存在於信箱資料庫中且*DisconnectReason*屬性的值設為`Disabled`。如果已經被從資料庫清除信箱，此命令將不會傳回任何結果。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

  - 有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。.

## 您要執行的工作

## 連接被刪除的信箱

當您連線已刪除的信箱時，建立關聯信箱與不是擁有郵件功能的使用者帳戶，這表示它不會有現有的信箱。若要刪除的信箱連接至具有信箱的使用者帳戶，您必須還原已刪除的信箱。如需詳細資訊，請參閱本主題稍後的還原已刪除的信箱。

## 使用 EAC 連接被刪除的信箱

下列程序示範如何將已刪除的使用者信箱連接至使用者帳戶。您也可以使用此程序來連線連結的信箱、 資源信箱和已刪除的共用的信箱的使用者帳戶。

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[信箱\]。

2.  按一下 \[更多\]![更多選項圖示](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "更多選項圖示")，然後按一下 \[連接信箱\]。
    
    隨即顯示您 Exchange 組織中選定 Exchange 伺服器上已中斷連線的信箱清單。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>此中斷連線信箱清單中包括停用的信箱、刪除的信箱，以及虛刪除的信箱。</td>
    </tr>
    </tbody>
    </table>


3.  按一下您要連接使用者的被刪除信箱，然後按一下 \[連線\]。

4.  在詢問您是否確定要連接信箱的視窗中，按一下 \[是\]。
    
    隨即顯示未擁有郵件功能的使用者帳戶清單。

5.  按一下您要連接被刪除信箱的使用者，然後按一下 \[確定\]。
    
    Exchange 會將被刪除的信箱連接至您選取的使用者帳戶。

## 使用命令介面連接被刪除的信箱

使用命令介面中的**Connect-Mailbox**指令程式來連線至未啟用郵件功能的使用者帳戶的刪除的信箱。您必須指定您要連接的信箱的類型。下列範例顯示重新連線使用者、 連結、 會議室、 設備及共用的信箱的語法。在所有的範例中，選擇性*Alias*參數用來指定電子郵件別名，這是在左邊的電子郵件地址的部分在 (@) 符號。如果您未包含*Alias*參數， *User*或*LinkedMasterAccount*參數中指定的值用來建立 reconnected 信箱的電子郵件地址的別名。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如前所述，當您連接連結信箱、資源信箱或共用信箱時，您必須停用欲連結信箱的 Active Directory 使用者帳戶。</td>
</tr>
</tbody>
</table>


此範例會連線使用者信箱。*Identity*參數會指定已刪除的信箱保留在名為 MBXDB01 信箱資料庫中的顯示名稱。*User*參數會指定要連線至信箱的 Active Directory 使用者帳戶。

    Connect-Mailbox -Identity "Paul Cannon" -Database MBXDB01 -User "Robin Wood" -Alias robinw

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您也可以使用 <code>LegacyDN</code> 或 <code>MailboxGuid</code> 內容的值來識別被刪除的信箱。</td>
</tr>
</tbody>
</table>


此範例會連線連結的信箱。*Identity*參數會指定已刪除的信箱上名為 MBXDB02 的信箱資料庫。*LinkedMasterAccount*參數會指定您想要連線的信箱帳戶樹系中 Active Directory 使用者帳戶。*LinkedDomainController*參數會指定帳戶樹系中的網域控制站。

    Connect-Mailbox -Identity "Temp User" -Database MBXDB02 -LinkedDomainController FabrikamDC01 -LinkedMasterAccount danpark@fabrikam.com -Alias dpark

這個範例會連線會議室信箱。

    Connect-Mailbox -Identity "rm2121" -Database "MBXResourceDB" -User "Conference Room 2121" -Alias ConfRm2121 -Room

這個範例會連線設備信箱。

    Connect-Mailbox -Identity "MotorPool01" -Database "MBXResourceDB" -User "Van01 (12 passengers)" -Alias van01 -Equipment

這個範例會連接共用的信箱。

    Connect-Mailbox -Identity "Printer Support" -Database MBXDB01 -User "Corp Printer Support" -Alias corpprint -Shared

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您也可以使用 <code>LegacyDN</code> 或 <code>MailboxGuid</code> 的值來識別被刪除的信箱。</td>
</tr>
</tbody>
</table>


如需詳細的語法及參數資訊，請參閱 [Connect-Mailbox](https://technet.microsoft.com/zh-tw/library/aa997878\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要驗證是否成功將被刪除的信箱連接至使用者帳戶，請執行下列其中一項操作：

  - 在 EAC 中，按一下 \[收件者\]，瀏覽至您要連接之信箱類型的適當頁面，按一下 \[重新整理\]![重新整理圖示](images/Dn624163.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "重新整理圖示")，然後確認信箱已列在其中。

  - Active Directory 使用者及電腦\] 中以滑鼠右鍵按一下 \[連接到信箱的使用者帳戶和 \[**屬性**。在 \[**一般**\] 索引標籤，請注意 \[**電子郵件**\] 方塊中填入連線的信箱的電子郵件地址。

  - 在命令介面中，執行下列命令。
    
        Get-User <identity>
    
    *RecipientType*屬性的**UserMailbox**值會指出已連線的使用者帳戶和信箱。您也可以執行**Get-Mailbox \<identity\>**命令，以確認已連線的信箱。

## 還原被刪除的信箱

您可以使用命令介面來還原已刪除的信箱至現有的信箱使用**New-MailboxRestoreRequest**指令程式。當您還原已刪除的信箱時、 其內容都會複製到現有的信箱，稱為 「*目標信箱*。還原刪除的信箱後，它具有仍保留在信箱資料庫之前會永久刪除由系統管理員或已刪除的信箱保留期間到期之後清除。

信箱還原要求成功完成後，它會保留 30 天內，根據預設之前就會被刪除。您可以移除它更早使用**Remove-StoreMailbox**指令程式。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您無法使用 EAC 來還原被刪除的信箱。</td>
</tr>
</tbody>
</table>


## 使用命令介面還原被刪除的信箱

若要建立信箱還原要求，您必須使用顯示名稱、 舊版的辨別的名稱 (DN) 或信箱已刪除信箱的 GUID。使用**Get-MailboxStatistics**指令程式來顯示您想要還原已刪除信箱`DisplayName`、 `MailboxGuid`，以及`LegacyDN`屬性的值。例如，執行下列命令以傳回所有此資訊已停用和刪除您組織中的信箱。

    Get-MailboxDatabase | Get-MailboxStatistics | Where {$_.DisconnectReason -eq "Disabled"} | fl DisplayName,MailboxGuid,LegacyDN,Database

此範例會還原刪除的信箱，由其*SourceStoreMailbox*參數所識別並位於要目標信箱蔡 Garcia MBXDB01 信箱資料庫。*AllowLegacyDNMismatch*參數會在來源信箱可以還原至不同的信箱，都不會有相同的傳統 DN 值的其中一個因此。

    New-MailboxRestoreRequest -SourceStoreMailbox e4890ee7-79a2-4f94-9569-91e61eac372b -SourceDatabase MBXDB01 -TargetMailbox "Debra Garcia" -AllowLegacyDNMismatch

此範例會為 Pilar Pinilla 刪除的封存信箱還原至其目前的封存信箱。因為主要信箱和其對應的封存信箱有相同的傳統 DN *AllowLegacyDNMismatch*參數不必要的。

    New-MailboxRestoreRequest -SourceStoreMailbox "Personal Archive - Pilar Pinilla" -SourceDatabase "MDB01" -TargetMailbox pilarp@contoso.com -TargetIsArchive

如需詳細的語法及參數資訊，請參閱 [New-MailboxRestoreRequest](https://technet.microsoft.com/zh-tw/library/ff829875\(v=exchg.150\))。

## 使用命令介面來還原已刪除公用資料夾信箱

如果您硬刪除公用資料夾信箱，您現在要還原的信箱已刪除項目保留限制 （請參閱[設定已刪除的項目保留及可復原的項目配額](configure-deleted-item-retention-and-recoverable-items-quotas-exchange-2013-help.md)） 您可以使用`Connect-Mailbox`指令程式，後面接著`Update-StoreMailboxState`指令程式。如需詳細的語法及參數資訊，請參閱[Connect-Mailbox](https://technet.microsoft.com/zh-tw/library/aa997878\(v=exchg.150\))和[Update-StoreMailboxState](https://technet.microsoft.com/zh-tw/library/jj860462\(v=exchg.150\))。

您必須刪除公用資料夾信箱，以及 GUID 或名稱包含公用資料夾信箱的信箱資料庫的 GUID。如果您不需要此資訊，您可以執行下列步驟：

1.  取得完整網域名稱 (FQDN) 的 Active Directory 樹系與網域控制站執行下列 cmdlet：
    
        Get-OrganizationConfig | fl OriginatingServer

2.  步驟 1 所傳回的資訊、 搜尋 Deleted Objects 容器 Active Directory 中的公用資料夾信箱 GUID 以及 GUID 或刪除公用資料夾信箱已包含在信箱資料庫的名稱。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您可以搜尋使用自訂指令碼的已刪除物件或藉由使用 Ldp 公用程式，其可以開啟 Powershell 提示字元中輸入<strong>ldp.exe</strong> 。</td>
    </tr>
    </tbody>
    </table>


當您知道刪除公用資料夾信箱 GUID 和名稱或 GUID 之信箱資料庫的包含公用資料夾信箱，執行下列命令，以還原公用資料夾信箱。

1.  執行下列命令 （可能系統提示您提供適當的認證） 來建立新的 Active Directory 物件：
    
        New-MailUser <mailUserName> -ExternalEmailAddress <emailAddress> 
        
        Get-MailUser <mailUserName> | Disable-MailUser
    
    其中`<mailUserName>`、 `<emailAddress>`，以及`<mailUserName>`是值您選擇。您必須在下一個步驟中使用相同的`<mailUserName>`值。

2.  刪除公用資料夾信箱連接至您剛才建立透過執行下列命令 Active Directory 物件：
    
        Connect-Mailbox -Identity <public folder mailbox GUID> -Database <database name or GUID> -User <mailUserName>
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><code>Identity</code>參數指定要連線至 Active Directory 使用者物件的 Exchange 資料庫將信箱物件。上述範例會指定公用資料夾信箱的 GUID，但您也可以使用顯示名稱或 LegacyExchangeDN 值。</td>
    </tr>
    </tbody>
    </table>


3.  對公用資料夾信箱，根據下面範例執行`Update-StoreMailboxState` ：
    
        Update-StoreMailboxState -Identity <public folder mailbox GUID> -Database <database name or GUID>
    
    如步驟 2 所示的`Identity`參數會接受 GUID、 顯示名稱或公用資料夾信箱的 LegacyExchangeDN 值。

## 如何知道這是否正常運作？

若要確認您是否已成功還原已刪除公用資料夾信箱，請執行**Get-PublicFolder -GetChildren -\<public folder mailbox GUID\>**指令程式。如果還原是否成功，此指令程式可運作。

如需詳細資訊，請參閱：

  - [Connect-Mailbox](https://technet.microsoft.com/zh-tw/library/aa997878\(v=exchg.150\))

  - [Update-StoreMailboxState](https://technet.microsoft.com/zh-tw/library/jj860462\(v=exchg.150\))

