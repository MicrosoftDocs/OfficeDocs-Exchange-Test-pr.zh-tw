---
title: '管理日誌: Exchange Online Help'
TOCTitle: 管理日誌
ms:assetid: d517f27e-f80a-4a06-988c-cbbf981c701d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ651670(v=EXCHG.150)
ms:contentKeyID: 50474283
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理日誌

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

日誌記錄可協助您錄製內送和外寄電子郵件通訊以回應法律聲明、 法規及組織規範需求的組織。本主題顯示如何執行與管理Exchange 2013和Exchange Online日誌記錄相關的基本工作。

標準日誌記錄設定於信箱資料庫。它會使日誌代理程式記錄進出特定信箱資料庫中信箱的所有郵件。您也可以使用高階日誌記錄讓日誌代理程式利用日誌規則執行更細微的日誌記錄。有別於記錄信箱資料庫上所有的信箱，您可以藉由記錄個別收件者或通訊群組成員，設定符合組織需求的日誌規則。您必須具備 Exchange 企業用戶端存取使用權 (CAL)，才能使用高階日誌記錄。

若要深入了解日誌記錄，請參閱[日誌](journaling-exchange-2013-help.md)。

**內容**

建立日誌規則

檢視或修改日誌規則

啟用或停用日誌規則

移除日誌規則

啟用或停用每個信箱資料庫日誌

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘。

  - [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md) 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 主題中的「日誌」項目。

  - 建立日誌記錄信箱之後，或現有信箱可做為日誌記錄信箱。您無法指定Exchange Online信箱作為日誌記錄信箱。您可以傳送日誌報告至內部部署封存系統或協力廠商封存服務。如果您正在執行的混合式部署與您的內部伺服器與Exchange Online之間分割的信箱，您可以指定為日誌記錄信箱的內部部署信箱Exchange Online和內部部署信箱。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您在Exchange Online傳送日誌報告至日誌記錄信箱不存在或無效的目的地設定的日誌規則、 日誌報告仍會保留 Microsoft 資料中心伺服器上傳輸佇列中。 如果發生這種情況將會嘗試 Microsoft 資料中心人員連絡您的組織並要求您修正此問題，讓日誌報告可以成功傳遞至日誌記錄信箱。如果您尚未解決問題的被連絡兩天後，Microsoft 將停用之問題的日誌規則。</td>
    </tr>
    </tbody>
    </table>


  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。如果您無法使用<strong>JournalingReportDNRTo</strong>信箱，查看<a href="https://go.microsoft.com/fwlink/p/?linkid=331674">傳輸和信箱在 Exchange Online 中的規則未如預期般運作</a>。</td>
</tr>
</tbody>
</table>


## 建立日誌規則

## 使用 EAC 建立日誌規則

1.  在 EAC 中，前往 \[**相符性管理**\>**日誌規則**，然後按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

2.  在 \[日誌規則\] 中，提供日誌規則的名稱，然後填妥下列欄位：
    
      - \[如果郵件傳送至或來自\]   指定規則所鎖定的收件者。您可以選取特定收件者，也可以將規則套用於所有郵件。
    
      - \[日記下列郵件\]   指定日誌規則的範圍。您可以只記錄內部郵件、只記錄外部郵件，或記錄任何來源或目的地的所有郵件。
    
      - \[傳送日誌報告至\]   輸入將接收所有日誌報告的日誌信箱地址。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>您也可以輸入顯示名稱或郵件使用者或郵件連絡人的別名為日誌信箱。在此例中日誌報告將傳送給郵件使用者或郵件連絡人的外部電子郵件地址。但是如先前所述的郵件使用者或郵件連絡人的外部電子郵件地址不能Exchange Online信箱的地址。</td>
        </tr>
        </tbody>
        </table>


3.  按一下 \[儲存\] 建立新的日誌規則。

## 使用命令介面來建立日誌規則

此範例會建立一個日誌規則「探索日誌收件者」，用於記錄所有由收件者 user1@contoso.com 傳送及接收的郵件。

    New-JournalRule -Name "Discovery Journal Recipients" -Recipient user1@contoso.com -JournalEmailAddress "Journal Mailbox" -Scope Global -Enabled $True

## 如何知道這是否正常運作？

若要確認您是否成功建立日誌規則，請執行下列其中一項：

  - 從 EAC 中，確認您建立的新日誌規則列在 \[日誌規則\] 索引標籤中。

  - 從命令介面中，執行下列命令，確定新日誌規則存在 (下列範例會驗證以上命令介面中建立的規則)：
    
        Get-JournalRule "Discovery Journal Recipients"

返回頁首

## 檢視或修改日誌規則

## 使用 EAC 檢視或修改日誌規則

1.  在 EAC 中，移至 \[**相符性管理**\>**日誌規則**。

2.  在清單檢視中，您將看見組織中所有的日誌規則。

3.  連按兩下要檢視或修改的規則。

4.  在 \[日誌規則\] 中，修改所需的設定。如需此對話方塊設定的詳細資訊，請參閱本主題中稍早的程序Use the EAC to create a journal rule。

## 使用命令介面檢視或修改日誌規則

本範例顯示 Exchange 組織中所有日誌規則的摘要清單：

    Get-JournalRule

本範例會擷取 Brokerage Journal Rule 日誌規則，並以管線輸出至 **Format-List** 命令，以清單格式顯示規則內容：

    Get-JournalRule "Brokerage Journal Rule" | Format-List

若您要修改具體規則的內容，必須使用 [Set-JournalRule](https://technet.microsoft.com/zh-tw/library/bb125010\(v=exchg.150\)) 指令程式。此範例將日誌 `JR-Sales` 的名稱變更為 `TraderVault`。以下是會一併變更的規則設定：

  - 收件者

  - JournalEmailAddress

  - 範圍

<!-- end list -->

    Set-JournalRule JR-Sales -Name TraderVault -Recipient traders@woodgrovebank.com -JournalEmailAddress tradervault@woodgrovebank.com -Scope Internal

## 如何知道這是否正常運作？

若要確認您是否成功修改日誌規則，請執行下列其中一項：

  - 從 EAC 中，瀏覽至 \[規範管理\], \> \[日誌規則\]。連按兩下您修改的規則，並驗證已儲存您的變更。

  - 從命令介面執行下列命令，確認您已經成功修改日誌規則。此命令將列出連同規則名稱一併修改的內容 (以下範例將確認以上命令程式範例中修改的規則)：
    
        Get-TransportRule "TraderVault" | Format-List Name,Recipient,JournalEmailAddress,Scope

返回頁首

## 啟用或停用日誌規則

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您提用日誌規則時，日誌代理程式將停止記錄規則所鎖定的郵件。停用日誌規則時，一般由規則記錄的任何郵件將不予記錄。確定您並未因為停用日誌規則而破壞您組織的規定或規範需求。</td>
</tr>
</tbody>
</table>


## 使用 EAC 啟用或停用日誌規則

1.  在 EAC 中，移至 \[**相符性管理**\>**日誌規則**。

2.  在清單檢視的規則名稱旁邊的 \[開啟\] 欄中，勾選核取方塊啟用規則，或取消勾選核取方塊停用規則。

## 使用命令介面啟用或停用日誌規則

此範例啟用規則 Contoso。

    Enable-JournalRule "Contoso Journal Rule"

此範例會停用 Contoso 規則。

    Disable-JournalRule "Contoso Journal Rule"

## 如何知道這是否正常運作？

若要確認您是否成功啟用或停用日誌規則，請執行下列其中一項：

  - 從 EAC 中，檢視日誌規則的清單，並檢查 \[開啟\] 欄的核取方塊狀態。

  - 從命令介面中，執行下列指令，反為您組織所有日誌規則及其狀態的清單：
    
        Get-JournalRule | Format-Table Name,Enabled

返回頁首

## 移除日誌規則

## 使用 EAC 移除日誌規則

1.  在 EAC 中，移至 \[**相符性管理**\>**日誌規則**。

2.  在清單檢視中，選取要移除的規則，然後按一下 \[刪除\]![刪除圖示](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "刪除圖示")。

## 使用命令介面移除日誌規則

此範例移除 Brokerage Journal Rule 規則。

    Remove-JournalRule "Brokerage Journal Rule"

## 如何知道這是否正常運作？

若要確認您是否成功移除日誌規則，請執行下列其中一項：

  - 從 EAC 中，確認您移除的規則不再列在 \[日誌規則\] 索引標籤中。

  - 從命令介面執行下列命令，確認您移除的規則不再列出：
    
        Get-JournalRule

返回頁首

## 啟用或停用每個信箱的資料庫日誌

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>停用信箱資料庫的郵件日誌可能導致您的組織不符合任何適用郵件保留原則的規範。停用信箱資料庫的郵件日誌時，對於信箱資料庫上的信箱所傳送或接收的郵件，將不再傳送日誌回條。</td>
</tr>
</tbody>
</table>


## 使用 EAC 啟用或停用每個信箱資料庫日誌

1.  在 EAC 中，移至 \[伺服器\] \> \[資料庫\]。

2.  在清單檢視中，連按兩下要啟用日誌的信箱資料庫。

3.  按一下 \[維護\]，然後按一下 \[日誌收件者\] 方塊旁邊的 \[瀏覽\]，選取日誌信箱。指定日誌收件者將啟用資料庫的日誌。
    
    若要停用日誌，請按一下 \[移除 X\] 移除日記收件者。

## 使用命令介面啟用或停用每個信箱的資料庫日誌

此範例啟用信箱資料庫「銷售資料庫」的日誌，並設定「銷售資料庫」日誌信箱作為日誌收件者。

    Set-MailboxDatabase "Sales Database" -JournalRecipient "Sales Database Journal Mailbox"

此範例停用「銷售資料庫」信箱資料庫的每個信箱資料庫日誌。

    Set-MailboxDatabase "Sales Database" -JournalRecipient $Null

此範例停用 Exchange 組織中所有信箱資料庫的每個信箱資料庫日誌。[Get-MailboxDatabase](https://technet.microsoft.com/zh-tw/library/bb124924\(v=exchg.150\)) Cmdlet 用來擷取 Exchange 組織中所有的信箱資料庫，而且命令介面的結果傳送至 [Set-MailboxDatabase](https://technet.microsoft.com/zh-tw/library/bb123971\(v=exchg.150\)) Cmdlet。

    Get-MailboxDatabase | Set-MailboxDatabase -JournalRecipient $Null

## 如何知道這是否正常運作？

若要確認您是否成功啟用或停用每個信箱資料庫日誌，請執行下列其中一項：

1.  在 EAC 中，移至 \[伺服器\] \> \[資料庫\]。

2.  連按兩下要確認的資料庫，然後選取 \[維護\] 索引標籤。

3.  如果正確的日誌收件者列在 \[日誌收件者\] 方塊中，表示您已經成功啟用信箱資料庫的日誌。如果未列出任何日誌收記者，表示已針對資料庫停用日誌。

<!-- end list -->

  - 從命令介面執行下列命令，傳回您組織中所有信箱資料庫的清單，包括與這些資料庫相關聯的日誌收件者。對於列出日誌收件者的資料庫，將啟用日誌，否則將予以停用。
    
        Get-MailboxDatabase | Format-Table Name,JournalRecipient

返回頁首

## 相關資訊

[日誌](journaling-exchange-2013-help.md)

[停用或啟用語音信箱和未接的來電通知的日誌記錄](disable-or-enable-journaling-of-voice-mail-and-missed-call-notifications-exchange-2013-help.md)

[New-JournalRule](https://technet.microsoft.com/zh-tw/library/bb125242\(v=exchg.150\))

[Get-JournalRule](https://technet.microsoft.com/zh-tw/library/aa998866\(v=exchg.150\))

[Set-JournalRule](https://technet.microsoft.com/zh-tw/library/bb125010\(v=exchg.150\))

[Enable-JournalRule](https://technet.microsoft.com/zh-tw/library/bb123902\(v=exchg.150\))

[Disable-JournalRule](https://technet.microsoft.com/zh-tw/library/aa995925\(v=exchg.150\))

[Remove-JournalRule](https://technet.microsoft.com/zh-tw/library/bb123489\(v=exchg.150\))

[Set-MailboxDatabase](https://technet.microsoft.com/zh-tw/library/bb123971\(v=exchg.150\))

