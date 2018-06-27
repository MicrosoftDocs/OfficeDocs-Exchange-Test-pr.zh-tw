---
title: '連線已停用的信箱: Exchange 2013 Help'
TOCTitle: 連線已停用的信箱
ms:assetid: a8abd399-75fd-4ee2-b2e4-634b55e4f79f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ863439(v=EXCHG.150)
ms:contentKeyID: 50554072
ms.date: 01/04/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 連線已停用的信箱

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-11-13_

您可以使用 EAC 或命令介面將被停用的信箱連接至 Active Directory 使用者帳戶。當您停用信箱時，Exchange 會在信箱資料庫中保留該信箱，並將該信箱切換成停用狀態。也會從相對應的 Active Directory 使用者帳戶中移除 Exchange 屬性，但保留使用者帳戶。信箱會保留直到超過刪除信箱的保留期間 (預設為 30 天)，然後才從信箱資料庫永久刪除 (或「清除」)。

在已停用的信箱從 Exchange 信箱資料庫永久刪除之前，您可以使用 EAC 或命令介面將其重新連接至原來的 Active Directory 使用者帳戶。

若要深入了解中斷連線信箱與執行其他相關管理工作的詳細資訊，請參閱以下主題：

  - [中斷連線的信箱](disconnected-mailboxes-exchange-2013-help.md)

  - [停用或刪除信箱](disable-or-delete-a-mailbox-exchange-2013-help.md)

  - [連線或還原已刪除的信箱](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)

  - [永久刪除信箱](permanently-delete-a-mailbox-exchange-2013-help.md)

## 開始之前有哪些須知？

  - 預估完成時間：2 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱[收件者權限](recipients-permissions-exchange-2013-help.md) 主題中的「收件者佈建權限」一節。

  - 在命令介面中執行 **Get-User** Cmdlet 來確認您想連接之停用信箱的 Active Directory 使用者帳戶已存在，而且尚未與其他信箱建立關聯。若要將停用信箱連接至使用者帳戶，該帳戶必須已存在，而且 *RecipientType* 屬性的值必須設為 `User`，此值表示該帳戶尚未啟用信箱功能。
    
    若是內部部署 Exchange 的組織，您也可以在 \[Active Directory 使用者及電腦\] 中確認此資訊。

  - 請執行下列命令，確認您想連接使用者帳戶的已停用信箱是否仍存在於信箱資料庫中，而且不是虛刪除的信箱。
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisplayName,Database,DisconnectReason
    
    若要連接已停用的信箱，該信箱必須存在於信箱資料庫中，而且 *DisconnectReason* 屬性的值必須設為 `Disabled`。如果信箱已從資料庫中清除，此命令將不會傳回任何結果。

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

## 使用 EAC 連接已停用的信箱

下列程序顯示如何連接已停用的使用者信箱。您也可以將已停用的連結信箱和已停用的共用信箱重新連接至相應的使用者帳戶。

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[信箱\]。

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


3.  按一下您要重新連接的已停用信箱，然後按一下 \[連線\]。

4.  在詢問您是否確定要重新連接信箱的視窗中，按一下 \[是\]。
    
    Exchange 隨即將已停用的信箱重新連接至相應的使用者帳戶。

## 使用命令介面連接已停用的信箱

在命令介面中使用 **Connect-Mailbox** Cmdlet 將使用者帳戶連接至已停用的信箱。您必須指定要連接的信箱類型。下列範例顯示用來重新連接使用者、連結和共用等信箱的語法。

這個範例會連接使用者信箱。*Identity* 參數指定 Exchange 資料庫中的中斷連線信箱。*User* 參數指定要重新連接信箱的 Active Directory 使用者帳戶。

    Connect-Mailbox -Identity "Jeffrey Zeng" -Database MBXDB01 -User "Jeffrey Zeng"

這個範例會連接到連結的信箱。*Identity* 參數指定 Exchange 資料庫中的中斷連線信箱。*LinkedMasterAccount* 參數指定您要重新連接信箱到樹系中哪一個 Active Directory 使用者帳戶。*Alias* 參數指定欲重新連接之信箱的別名，也就是電子郵件地址中 at (@) 符號左側的部分。

    Connect-Mailbox -Identity "Kai Axford" -Database MBXDB02 -LinkedDomainController FabrikamDC01 -LinkedMasterAccount kai.axford@fabrikam.com -Alias kaia

這個範例會連接共用的信箱。

    Connect-Mailbox -Identity "Corporate Shared Mailbox" -Database "Mailbox Database 03" -User "Corporate Shared Mailbox" -Alias corpshared -Shared

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您執行 <strong>Connect-Mailbox</strong> Cmdlet 時未包含 <em>Alias</em> 參數，則會使用 <em>User</em> 或 <em>LinkedMasterAccount</em> 參數指定的值來建立重新連接信箱之電子郵件地址的別名。</td>
</tr>
</tbody>
</table>


如需詳細的語法及參數資訊，請參閱 [Connect-Mailbox](https://technet.microsoft.com/zh-tw/library/aa997878\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要驗證是否成功將已停用的信箱連接至使用者帳戶，請執行下列其中一項操作：

  - 在 EAC 中，按一下 \[收件者\]，導覽至您要重新連接之信箱類型的適當頁面，按一下 \[重新整理\]![重新整理圖示](images/Dn624163.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "重新整理圖示")，然後確認信箱已列在其中。

  - 在 \[Active Directory 使用者及電腦\] 中，於要停用其信箱的使用者帳戶上按一下滑鼠右鍵，然後按一下 \[內容\]。在 \[一般\] 索引標籤中，注意 \[電子郵件\] 方塊是否已填入重新連接之信箱的電子郵件地址。

  - 在命令介面中，執行下列命令。
    
        Get-User <identity>
    
    *RecipientType* 屬性的 **UserMailbox** 值指出使用者帳戶和信箱已連接。您也可以執行 **Get-Mailbox** Cmdlet 來確認信箱是否存在。

