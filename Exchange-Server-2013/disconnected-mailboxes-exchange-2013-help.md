---
title: '中斷連線的信箱: Exchange 2013 Help'
TOCTitle: 中斷連線的信箱
ms:assetid: 508ebe2b-387d-4867-bdb0-028ef351ce56
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb232039(v=EXCHG.150)
ms:contentKeyID: 50553983
ms.date: 01/01/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 中斷連線的信箱

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

每個 Microsoft Exchange 信箱是由儲存在 Exchange 信箱資料庫的 Active Directory 使用者帳戶和信箱資料所組成。信箱的所有設定資料會儲存在 Active Directory 使用者物件的 Exchange 屬性中。信箱資料庫包含的郵件資料位於與使用者帳戶關聯的信箱中。下圖顯示信箱的元件。

**信箱元件**

![組成信箱的組件](images/Bb201680.5fcb5e6d-656e-42ae-871f-0eef8aea456b(EXCHG.150).gif "組成信箱的組件")

*「中斷連線的信箱」*是信箱資料庫中與 Active Directory 使用者帳戶無關聯的信箱物件。已中斷連線的信箱有兩種類型：

  - **已停用的信箱**   當信箱在 Exchange 系統管理中心 (EAC) 遭到停用或刪除，或是在 Exchange 管理命令介面中使用 **Disable-Mailbox** 或 **Remove-Mailbox** Cmdlet 時，Exchange 會將刪除的信箱保留在信箱資料庫中，並將信箱切換成停用狀態。這就是停用或刪除的信箱稱為「已停用的信箱」的原因。區別在於，當您停用信箱時，Exchange 屬性會從對應的 Active Directory 使用者帳戶移除，但會保留使用者帳戶。當您刪除信箱時，會同時刪除 Exchange 屬性和 Active Directory 使用者帳戶。
    
    已停用和已刪除的信箱會保留在信箱資料庫中，直到已刪除的信箱保留期間到期，預設為 30 天。保留期間到期之後，信箱就會永久刪除 (也稱為「清除」)。如果使用 **Remove-Mailbox** Cmdlet 刪除信箱，系統也會保留該信箱直到保留期間到期。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果使用 <strong>Remove-Mailbox</strong> Cmdlet 以及 <em>Permanent</em> 或 <em>StoreMailboxIdentity</em> 參數刪除信箱，則會立即從信箱資料庫刪除該信箱。</td>
    </tr>
    </tbody>
    </table>
    
    若要識別組織中已停用的信箱，請在命令介面中執行下列命令。
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisconnectReason -eq "Disabled" } | ft DisplayName,Database,DisconnectDate

  - **虛刪除信箱**   將信箱移動至其他的信箱資料庫時，Exchange 不會在移動完成之後將信箱從來源信箱資料庫中完全刪除。而是會將來源信箱資料庫中的信箱切換到「虛刪除」狀態。如同停用的信箱，虛刪除的信箱會保留在來源資料庫中，直到刪除的信箱保留期間到期或直到使用 **Remove-StoreMailbox** Cmdlet 清除信箱。
    
    請執行下列命令，識別組織中的虛刪除信箱。
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisconnectReason -eq "SoftDeleted" } | ft DisplayName,Database,DisconnectDate

**目錄**

使用已停用的信箱

使用已停用的封存信箱

使用虛刪除信箱

使用中斷連線信箱的摘要說明

中斷連線信箱的文件

## 使用已停用的信箱

在從信箱資料庫清除已停用的信箱前，您可以對該信箱執行數項操作：

  - 將它重新連線到相同的使用者帳戶。

  - 將它連線到未啟用郵件功能的使用者帳戶，亦即使用者帳戶沒有信箱。

  - 將它還原到具有現有信箱的使用者帳戶。例如，如果已刪除信箱的使用者有新信箱，您可以將該使用者已停用的信箱還原到其新信箱。

  - 從 Exchange 信箱資料庫永久刪除它。

## 連線或還原已停用的信箱

在下列案例中，您可能想在已停用的信箱保留期間到期或永久刪除之前，連線或還原該信箱：

  - 您已停用信箱，但現在卻想要將信箱重新連線至相同的 Active Directory 使用者帳戶。

  - 您已使用 EAC 或 [Remove-Mailbox](https://technet.microsoft.com/zh-tw/library/aa995948\(v=exchg.150\)) Cmdlet 刪除信箱，但現在卻想要將信箱重新連線至不同的 Active Directory 使用者帳戶。

  - 您已刪除信箱，但現在卻想要將信箱還原到現有的信箱。例如，如果已刪除信箱的使用者有新信箱，您可以將該使用者已停用的信箱還原到其新信箱。

  - 您想要將使用者信箱轉換成連結的信箱，而後者則與 Exchange 組織存在的樹系外部之使用者帳戶相關聯。例如，在資源樹系中，您便會想將信箱與外部帳戶產生關聯。在此案例中，Exchange 樹系中的使用者物件具有信箱，但已停用使用者物件的登入。您必須使 Exchange 樹系中的信箱與外部帳戶樹系中的使用者帳戶產生關聯。

您有兩種方法可以重新連線或還原已停用的信箱。第一種方法是使用 EAC 或 **Connect-Mailbox** Cmdlet，將已停用的信箱連線到使用者帳戶。如需重新連線已停用信箱的程序，請參閱＜[連線已停用的信箱](connect-a-disabled-mailbox-exchange-2013-help.md)＞。

第二種方法是使用 **New-MailboxRestoreRequest** Cmdlet，將已停用的信箱內容與現有信箱合併。此 Cmdlet 會使用信箱複寫服務 (MRS) 來還原信箱。如需還原已停用信箱的程序，請參閱＜[連線或還原已刪除的信箱](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)＞。

## 永久刪除已停用的信箱

如上所述，Exchange 會根據您對該信箱資料庫所設定的已刪除信箱保留期間設定，保留信箱資料庫中已停用的信箱。過了指定的保留期間後，會從 Exchange 信箱資料庫中清除已停用的信箱。您也可以使用 **Remove-StoreMailbox** Cmdlet，從信箱資料庫永久刪除已停用的信箱及其所有郵件內容。在已停用的信箱經系統自動清除或由系統管理員永久刪除後，資料便會永久遺失，且無法復原信箱。

如需詳細資訊，請參閱＜[永久刪除信箱](permanently-delete-a-mailbox-exchange-2013-help.md)＞。

使用已停用的信箱

## 使用已停用的封存信箱

封存信箱在停用時會中斷連線。中斷連線的封存信箱類似於已停用的主要信箱，可以透過搭配使用 **Connect-Mailbox** Cmdlet 與 *Archive* 參數來進行連線。

主要信箱和封存信箱共用相同的舊辨別名稱 (DN)，因此必須將封存信箱連線到之前所連線的相同使用者信箱。您無法將封存信箱連線到不同的使用者信箱。

您可以對中斷連線的封存信箱執行兩項操作：

  - **將它連線到現有的主要信箱**   如同中斷連線的主要信箱，中斷連線的封存信箱會保留在信箱資料庫中，直到已刪除的信箱保留期間到期，預設為 30 天。在這段期間，您可以將封存信箱重新連線到停用之前所連線的同一個使用者帳戶，以復原該信箱。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>若您停用使用者信箱的封存信箱，然後為相同使用者啟用封存信箱，該使用者信箱將取得新的封存信箱。當您使用 <strong>Connect-Mailbox</strong> Cmdlet將主要信箱連線到使用者，您必須使用 <strong>Enable-Mailbox</strong> Cmdlet 將停用的封存信箱連線到現有的信箱。</td>
    </tr>
    </tbody>
    </table>
    
    如需詳細資訊，請參閱＜[管理 Exchange 2013 中的就地封存](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md)＞。

  - **從 Exchange 信箱資料庫永久刪除它**    Exchange 會根據您對該信箱資料庫所設定的已刪除信箱保留期間設定，保留中斷連線的封存信箱。預設的保留期間是 30 天。過了指定的信箱保留期間後，會從 Exchange 信箱資料庫中清除中斷連線的封存信箱。
    
    如同已停用的主要信箱，您可以隨時使用 **Remove-StoreMailbox** Cmdlet 永久刪除已停用的封存信箱。如需詳細資訊，請參閱＜[永久刪除信箱](permanently-delete-a-mailbox-exchange-2013-help.md)＞。

使用已停用的信箱

## 使用虛刪除信箱

當信箱從 Exchange 信箱資料庫移至任何其他信箱資料庫時，會建立虛刪除的信箱。Exchange 並不會在移動之後完全刪除來源資料庫中的信箱，以避免移動時發生錯誤而造成目的資料庫中的信箱失效。您可以隨時還原來源信箱並再試一次。Exchange 會在信箱保留期間保留虛刪除信箱。

您可以對虛刪除信箱執行兩項操作：

  - 將它還原到現有信箱。

  - 從 Exchange 信箱資料庫永久刪除它。

還原和永久刪除虛刪除信箱的程序，與已停用信箱的程序類似。如需相關資訊，請參閱下列主題：

  - [還原虛刪除信箱](restore-a-soft-deleted-mailbox-exchange-2013-help.md)

  - [永久刪除信箱](permanently-delete-a-mailbox-exchange-2013-help.md)

使用已停用的信箱

## 使用中斷連線信箱的摘要說明

下表摘要說明中斷連線信箱的相關資訊，包括如何中斷連線信箱、對應的 Active Directory 使用者帳戶在信箱中斷連線時會發生什麼變化，以及連線或還原中斷連線信箱所需的選項和工具。


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>信箱的停用方式</th>
<th><em>DisconnectReason</em> 屬性的值</th>
<th>是否保留 Active Directory 使用者帳戶？</th>
<th>連線或還原選項</th>
<th>工具</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>EAC：<strong>收件者</strong> &gt; <strong>信箱</strong> &gt; <strong>停用</strong></p></li>
<li><p>命令介面：<strong>Disable-Mailbox</strong> Cmdlet</p></li>
</ul></td>
<td><p>已停用</p></td>
<td><p>是</p></td>
<td><p>連線到相同的使用者帳戶</p></td>
<td><ul>
<li><p>EAC：<strong>收件者</strong> &gt; <strong>信箱</strong> &gt; <strong>連線信箱</strong></p></li>
<li><p>命令介面：<strong>Connect-Mailbox</strong> Cmdlet</p></li>
</ul></td>
</tr>
<tr class="even">
<td><ul>
<li><p>EAC：<strong>收件者</strong> &gt; <strong>信箱</strong> &gt; <strong>刪除</strong></p></li>
<li><p>命令介面：<strong>Remove-Mailbox</strong> Cmdlet</p></li>
</ul></td>
<td><p>已停用</p></td>
<td><p>否</p></td>
<td><ul>
<li><p>連線到不同的使用者帳戶</p></li>
<li><p>還原到不同的信箱</p></li>
</ul></td>
<td><ul>
<li><p>EAC：<strong>收件者</strong> &gt; <strong>信箱</strong> &gt; <strong>連線信箱</strong></p></li>
<li><p>命令介面：<strong>Connect-Mailbox</strong> Cmdlet</p></li>
<li><p><strong>Enable-Mailbox</strong></p></li>
<li><p>命令介面：<strong>New-MailboxRestore</strong> Cmdlet</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>移動到不同的信箱資料庫</p></td>
<td><p>SoftDeleted</p></td>
<td><p>是</p></td>
<td><ul>
<li><p>連線到不同的使用者帳戶</p></li>
<li><p>還原到不同的信箱</p></li>
</ul></td>
<td><ul>
<li><p>EAC：<strong>收件者</strong> &gt; <strong>信箱</strong> &gt; <strong>連線信箱</strong></p></li>
<li><p>命令介面：<strong>Connect-Mailbox</strong> Cmdlet</p></li>
<li><p><strong>Enable-Mailbox</strong></p></li>
<li><p>命令介面：<strong>New-MailboxRestore</strong> Cmdlet</p></li>
</ul></td>
</tr>
</tbody>
</table>


使用已停用的信箱

## 中斷連線信箱的文件

下表包含的主題連結可協助您管理中斷連線的信箱。這包括管理中斷連線的使用者信箱、連結的信箱、資源信箱以及共用信箱。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>主題</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="disable-or-delete-a-mailbox-exchange-2013-help.md">停用或刪除信箱</a></p></td>
<td><p>瞭解如何停用或刪除信箱。</p></td>
</tr>
<tr class="even">
<td><p><a href="connect-a-disabled-mailbox-exchange-2013-help.md">連線已停用的信箱</a></p></td>
<td><p>瞭解如何將已停用的信箱連線到現有的使用者帳戶。</p></td>
</tr>
<tr class="odd">
<td><p><a href="connect-or-restore-a-deleted-mailbox-exchange-2013-help.md">連線或還原已刪除的信箱</a></p></td>
<td><p>瞭解如何將已刪除的信箱連線到使用者帳戶，或將已刪除的信箱內容還原到現有信箱。</p></td>
</tr>
<tr class="even">
<td><p><a href="restore-a-soft-deleted-mailbox-exchange-2013-help.md">還原虛刪除信箱</a></p></td>
<td><p>瞭解如何將虛刪除的信箱連線到使用者帳戶，或將虛刪除的信箱還原到現有信箱。</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-mailbox-restore-requests-exchange-2013-help.md">管理信箱還原要求</a></p></td>
<td><p>瞭解如何使用命令介面管理信箱還原要求。</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p><a href="permanently-delete-a-mailbox-exchange-2013-help.md">永久刪除信箱</a></p></td>
<td><p>瞭解如何永久刪除信箱。</p></td>
</tr>
</tbody>
</table>


使用已停用的信箱

