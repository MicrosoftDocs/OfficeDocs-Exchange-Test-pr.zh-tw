---
title: '啟用或停用信箱稽核記錄功能信箱: Exchange 2013 Help'
TOCTitle: 啟用或停用信箱稽核記錄功能信箱
ms:assetid: c4bbfd52-6196-49c7-8c31-777fbbee11f2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ff461937(v=EXCHG.150)
ms:contentKeyID: 50474203
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟用或停用信箱稽核記錄功能信箱

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-09-30_

與信箱稽核記錄，您可以追蹤登入至信箱，以及為使用者時採取哪些動作登入。當您啟用信箱稽核記錄的信箱由管理員執行某些動作及代理人會記錄預設。None 信箱擁有者所執行的動作會記錄。若要了解更多有關信箱稽核記錄，請參閱[信箱稽核記錄](mailbox-audit-logging-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>稽核的信箱擁有者動作可以產生的信箱稽核記錄項目數目與因此預設會停用。建議您僅啟用特定的擁有者動作以符合商務或安全性需求所需的稽核。</td>
</tr>
</tbody>
</table>


如需與信箱稽核記錄相關的其他工作，請參閱[信箱稽核記錄程序](mailbox-audit-logging-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「信箱稽核記錄」項目。

  - 您無法使用 Exchange 系統管理中心 (EAC) 來啟用或停用信箱稽核記錄。您必須使用命令介面。

  - 獲指派使用者信箱「完整存取」權限的系統管理員會被視為委派使用者。

  - 信箱會被視為只能在下列情況中系統管理員存取：
    
      - 使用 In-Place eDiscovery 來搜尋信箱。
    
      - 使用 **New-MailboxExportRequest** 指令程式來匯出信箱。
    
      - Microsoft Exchange Server MAPI 編輯器用來存取信箱。

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

## 使用命令介面來啟用或停用信箱稽核記錄

您可以使用命令介面啟用或停用信箱稽核記錄功能信箱。這會啟用或停用的所有作業的管理員、 委派及信箱擁有者指定的記錄。

這個範例會啟用 Ben Smith 信箱的信箱稽核記錄。

    Set-Mailbox -Identity "Ben Smith" -AuditEnabled $true

這個範例會停用 Ben Smith 信箱的信箱稽核記錄。

    Set-Mailbox -Identity "Ben Smith" -AuditEnabled $false

如需詳細的語法及參數資訊，請參閱 [Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\))。

## 使用命令介面，針對系統管理員、代理人或擁有者存取方面設定信箱稽核記錄設定

啟用信箱的信箱稽核記錄時，系統僅會記錄信箱稽核記錄設定中所指定之系統管理員、代理人和擁有者的行為。

這個範例指定會為 Ben Smith 信箱記錄委派使用者執行的 `SendAs` 或 `SendOnBehalf` 動作。

    Set-Mailbox -Identity "Ben Smith" -AuditDelegate SendAs,SendOnBehalf -AuditEnabled $true

這個範例指定會為 Ben Smith 的信箱記錄系統管理員執行的 `MessageBind` 和 `FolderBind` 動作。

    Set-Mailbox -Identity "Ben Smith" -AuditAdmin MessageBind,FolderBind -AuditEnabled $true

這個範例指定將會為 Ben Smith 信箱記錄信箱擁有者執行的 `HardDelete` 動作。

    Set-Mailbox -Identity "Ben Smith" -AuditOwner HardDelete -AuditEnabled $true

如需詳細的語法及參數資訊，請參閱 [Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要驗證您是否已成功啟用信箱的信箱稽核記錄，並針對系統管理員、代理人或擁有者存取方面指定好正確的記錄設定，可使用 [Get-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123685\(v=exchg.150\)) Cmdlet 以擷取該信箱的信箱稽核記錄設定。

此範例會擷取 Ben Smith 的信箱設定，並將指定的稽核設定 (包括稽核記錄保留天數) 傳送至 **Format-List** Cmdlet。

    Get-Mailbox "Ben Smith" | Format-List *audit*

