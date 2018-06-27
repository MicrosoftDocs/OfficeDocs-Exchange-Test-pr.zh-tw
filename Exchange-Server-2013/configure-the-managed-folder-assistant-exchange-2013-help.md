---
title: '設定受管理的資料夾助理員: Exchange 2013 Help'
TOCTitle: 設定受管理的資料夾助理員
ms:assetid: 9fcfb9b6-bd24-4218-a163-bc599cd5476a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb123958(v=EXCHG.150)
ms:contentKeyID: 50473854
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定受管理的資料夾助理員

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-10-01_

*受管理的資料夾助理員*是MicrosoftExchange信箱助理員套用保留原則中設定的郵件保留設定。

如需與通訊記錄管理 (MRM) 相關的其他管理工作，請參閱[通訊記錄管理程序](messaging-records-management-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 完成時間： 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「通訊記錄管理」項目。

  - 您無法使用 Exchange 系統管理中心 (EAC) 來設定受管理的資料夾助理員。您必須使用命令介面

  - 在Exchange 2013、 受管理的資料夾助理員會是節流為基礎的小幫手。節流型助理會永遠執行，所以不需要排程。它們可耗用的系統資源已受到節流。您可以設定受管理的資料夾助理員處理特定期間內的所有信箱的信箱伺服器上 (又稱為*工作週期)*。預設工作週期設定的一天。

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

## 使用命令介面來設定受管理的資料夾助理員

此範例會在受管理的資料夾助理員處理在一天內的所有信箱。

    Set-MailboxServer MyMailboxServer -ManagedFolderWorkCycle 1

如需詳細的語法及參數資訊，請參閱 [Set-MailboxServer](https://technet.microsoft.com/zh-tw/library/aa998651\(v=exchg.150\))。

## 如何知道這是否正常運作？

若要確認您已成功設定受管理的資料夾助理員，使用[Get-MailboxServer](https://technet.microsoft.com/zh-tw/library/bb123539\(v=exchg.150\))指令程式來檢查*ManagedFolderWorkCycle*參數。

此命令會擷取組織中的所有 Mailbox server 及輸出的每一部伺服器以表格格式的受管理的資料夾助理員的工作週期屬性。*Auto*參數用來自動調整欄寬。

    Get-MailboxServer | Format-Table Name,ManagedFolderWorkCycle* -Auto

## 使用命令介面來啟動 \[受管理的資料夾助理員

此範例會觸發受管理的資料夾助理員立即處理 Morris Cornejo 信箱。

    Start-ManagedFolderAssistant -Identity morris.cornejo@contoso.com

如需詳細的語法及參數資訊，請參閱[Start-ManagedFolderAssistant](https://technet.microsoft.com/zh-tw/library/aa998864\(v=exchg.150\))。

