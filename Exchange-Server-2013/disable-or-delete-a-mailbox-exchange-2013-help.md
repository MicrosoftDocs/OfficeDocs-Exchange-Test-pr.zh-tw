---
title: '停用或刪除信箱: Exchange 2013 Help'
TOCTitle: 停用或刪除信箱
ms:assetid: 31ad25d6-2942-4fd9-aecb-cdf9654163d2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ863434(v=EXCHG.150)
ms:contentKeyID: 50553958
ms.date: 01/04/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 停用或刪除信箱

 

_**適用版本：**Exchange Server 2013 SP1_

_**上次修改主題的時間：**2015-03-09_

您可以使用 EAC 或命令介面來停用或刪除 Exchange 2013 中的信箱。停用或刪除信箱時，Exchange 會將信箱保留在信箱資料庫中，並將信箱切換成停用狀態。已停用和已刪除的信箱會保留在信箱資料庫中，直到已刪除的信箱保留期間到期，預設為 30 天。保留期間到期之後，信箱就會永久刪除或「清除」。

如果您需要刪除 Exchange Online 中的信箱，請參閱＜[刪除或還原 Exchange Online 中的使用者信箱](https://technet.microsoft.com/zh-tw/library/dn186233\(v=exchg.150\))＞。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>已停用或已刪除的信箱稱為「中斷連線信箱」。</td>
</tr>
</tbody>
</table>


刪除和停用信箱的主要差異在於，當您停用信箱時，Exchange 屬性會從對應的 Active Directory 使用者帳戶移除，但使用者帳戶仍保留下來。當您刪除信箱時，會同時刪除 Exchange 屬性和 Active Directory 使用者帳戶。此差異也會決定重新連線或還原已停用和已刪除信箱時的選項。

下表顯示可以停用和刪除的 Exchange 信箱類型。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>信箱類型</th>
<th>停用？</th>
<th>刪除？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>封存信箱</p></td>
<td><p>是</p></td>
<td><p>否*</p></td>
</tr>
<tr class="even">
<td><p>連結的信箱</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>資源信箱 (會議室或設備)</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>共用信箱</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>使用者信箱</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
</tbody>
</table>


\* 如果啟用封存信箱，當刪除主要信箱時，會一併刪除。如需停用封存信箱的詳細資訊，請參閱＜[管理 Exchange 2013 中的就地封存](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md)＞。

如果系統管理員刪除的使用者帳戶有信箱，則 Exchange 資訊儲存庫最終會偵測到信箱已不再連接到使用者帳戶，並將該信箱標示為待刪除，即使信箱已保留。若您想保留信箱，必須執行下列作業：

1.  不要刪除使用者帳戶，而是停用使用者帳戶。

2.  變更信箱的屬性，以限制其對信箱的使用和存取。例如，將收發配額設為 1，封鎖可以傳送訊息至信箱的人，並限制可以存取信箱的對象。

3.  保留信箱直到所有資料皆刪除，或直到不再需要保留。

如需與中斷連線信箱相關的其他管理工作，請參閱下列主題：

  - [中斷連線的信箱](disconnected-mailboxes-exchange-2013-help.md)

  - [連線已停用的信箱](connect-a-disabled-mailbox-exchange-2013-help.md)

  - [連線或還原已刪除的信箱](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)

  - [永久刪除信箱](permanently-delete-a-mailbox-exchange-2013-help.md)

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：2 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱[收件者權限](recipients-permissions-exchange-2013-help.md) 主題中的「收件者佈建權限」一節。

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

## 停用信箱

如前所述，當您停用信箱時，Exchange 屬性會從對應的 Active Directory 使用者帳戶移除，但使用者帳戶仍保留下來。

## 使用 EAC 停用信箱

下列程序顯示如何停用使用者信箱。在瀏覽到 EAC 中的適當頁面之後，請使用相同的程序停用其他信箱類型。

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[信箱\]。

2.  在使用者信箱清單中，按一下要停用的信箱。

3.  按一下 \[更多\]![更多選項圖示](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "更多選項圖示")，然後按一下 \[停用\]。

4.  此時，會出現一個警告，詢問 \[您確定要停用信箱嗎?\]。按一下 \[是\] 以停用信箱。

信箱隨即從信箱清單移除。

## 使用命令介面停用信箱

請使用下列命令停用使用者信箱、連結的信箱、資源信箱以及共用信箱。

    Disable-Mailbox <identity>

執行此命令時，會顯示訊息詢問您是否確認要停用信箱。

下面是停用信箱的一些命令範例。

    Disable-Mailbox danj

    Disable-Mailbox "Conf Room 31/1234 (12)"

    Disable-Mailbox sharedmbx@contoso.com

## 如何知道這是否正常運作？

若要確認您是否成功停用信箱，請執行下列其中一項：

  - 在 EAC 中，按一下 \[收件者\]，瀏覽到您已停用之信箱類型的適當頁面，然後確認信箱是否不再列出。

  - 在 \[Active Directory 使用者及電腦\] 中，以滑鼠右鍵按一下停用信箱的使用者帳戶，然後按一下 \[內容\]。在 \[一般\] 索引標籤上，注意 \[電子郵件\] 欄位是否空白。這可確認信箱已停用，但使用者帳戶仍存在。

  - 在命令介面中，執行下列命令。
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisconnectReason,DisconnectDate
    
    *DisconnectReason* 屬性中的 `Disabled` 值表示信箱已停用。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>當您刪除信箱時，<em>DisconnectReason</em> 屬性中的值也會是 <code>Disabled</code>。不過，對應的 Active Directory 使用者帳戶會刪除。</td>
    </tr>
    </tbody>
    </table>


  - 在命令介面中，執行下列命令。
    
        Get-User <identity>
    
    請注意，*RecipientType* 內容的值為 `User`，而不是 `UserMailbox` (具有已啟用信箱之使用者的值)。這也可確認信箱已停用，但使用者帳戶保留下來。

## 刪除信箱

如前所述，當您刪除信箱時，會同時刪除 Exchange 屬性和 Active Directory 使用者帳戶。信箱 (以及啟用的封存信箱) 在信箱保留期間到期之後，便會從信箱資料庫永久刪除。

## 使用 EAC 刪除信箱

下列程序顯示如何刪除使用者信箱。在瀏覽到 EAC 中的適當頁面之後，請使用相同的程序刪除其他信箱類型。

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[信箱\]。

2.  在使用者信箱清單中，按一下您想刪除的信箱，然後按一下 \[刪除\]![刪除圖示](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "刪除圖示")。

3.  此時會出現警告，詢問您是否確定要刪除信箱。請按一下 \[是\]以刪除信箱。

信箱隨即從信箱清單移除。

## 使用命令介面刪除信箱

請使用下列命令刪除使用者信箱、連結的信箱、資源信箱以及共用信箱。

    Remove-Mailbox <identity>

執行此命令時，會顯示訊息詢問您是否確認要移除信箱以及對應的 Active Directory 使用者帳戶。

下面是刪除信箱的一些命令範例。

    Remove-Mailbox pilarp@contoso.com

    Remove-Mailbox "Fleet Van (16)"

    Remove-Mailbox corpprint

## 如何知道這是否正常運作？

若要驗證是否成功刪除信箱，請執行下列其中一組驗證程序：

1.  在 EAC 中，按一下 \[收件者\]，然後瀏覽到您已刪除之信箱類型的適當頁面，確認信箱是否不再列出。

2.  在 \[Active Directory 使用者及電腦\] 中，確認對應的使用者帳戶不再列出。

或

1.  執行下列命令來確認已刪除信箱。
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisconnectReason,DisconnectDate
    
    *DisconnectReason* 屬性中的 `Disabled` 值表示信箱已刪除。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>當您停用信箱時，<em>DisconnectReason</em> 屬性中的值也會是 <code>Disabled</code>。不過，對應的 Active Directory 使用者帳戶會保留。</td>
    </tr>
    </tbody>
    </table>


2.  執行下列命令來確認已刪除 Active Directory 使用者帳戶。
    
        Get-User <identity>
    
    此命令將傳回錯誤，表示找不到使用者，確認已刪除帳戶。

