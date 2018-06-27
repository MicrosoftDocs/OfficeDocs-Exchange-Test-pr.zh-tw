---
title: '就地保留信箱保留 」 狀態: Exchange Online Help'
TOCTitle: 就地保留信箱保留 」 狀態
ms:assetid: 2baac4a7-3402-4142-bfb3-1649a950e677
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd335168(v=EXCHG.150)
ms:contentKeyID: 50472758
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 就地保留信箱保留 」 狀態

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2012-10-14_

將信箱設定保留暫停處理保留原則或該信箱的受管理的資料夾信箱原則。保留旨在協助使用者暫時正在休假或離開等情況。

期間保留功能，使用者可以登入其信箱並變更或刪除項目。當您執行信箱搜尋時，搜尋結果未傳回過去的已刪除的項目保留期間的已刪除項目。若要確定變更過或刪除使用者所擁有的項目會保留在合法持有案例，您必須將信箱置於法務保存措施。如需詳細資訊，請參閱[建立或移除就地保留](create-or-remove-an-in-place-hold-exchange-2013-help.md)。

您也可以包含保留註解的信箱置於保留。支援版本的 Microsoft Outlook中顯示註解。

如需與通訊記錄管理 (MRM) 相關的其他管理工作，請參閱[通訊記錄管理程序](messaging-records-management-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「通訊記錄管理」項目。

  - 您無法使用 Exchange 系統管理中心 (EAC) 若要將信箱置於保留。您必須使用命令介面。

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

## 使用命令介面為信箱啟用保留功能

本範例會在 Michael Allen 的信箱上啟用保留功能。

    Set-Mailbox "Michael Allen" -RetentionHoldEnabled $true

如需詳細的語法及參數資訊，請參閱 [Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\))。

## 使用命令介面移除信箱的保留功能

本範例會從 Michael Allen 的信箱移除保留功能。

    Set-Mailbox "Michael Allen" -RetentionHoldEnabled $false

如需詳細的語法及參數資訊，請參閱 [Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要確認您已成功將信箱置於保留，請使用 [Get-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123685\(v=exchg.150\)) 指令程式來擷取信箱的 *RetentionHoldEnabled* 屬性。

此命令為 Michael Allen 的信箱擷取 *RetentionHoldEnabled* 屬性。

    Get-Mailbox "Michael Allen" | Select RetentionHoldEnabled

此指令擷取所有在 Exchange 組織中的信箱、篩選置於保留的信箱、並以每個信箱得保留原則列出。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>因為<em>RetentionHoldEnabled</em>不是在Exchange 2013可篩選屬性，您無法使用<em>Filter</em>參數與篩選信箱的保留保留在伺服器端<strong>Get-Mailbox</strong>指令程式。此命令會擷取所有信箱和用戶端執行命令介面工作階段的篩選的清單。在大型環境中使用千分位的信箱，此命令可能需要長的時間才能完成。</td>
</tr>
</tbody>
</table>


    Get-Mailbox -ResultSize unlimited | Where-Object {$_.RetentionHoldEnabled -eq $true} | Format-Table Name,RetentionPolicy,RetentionHoldEnabled -Auto

