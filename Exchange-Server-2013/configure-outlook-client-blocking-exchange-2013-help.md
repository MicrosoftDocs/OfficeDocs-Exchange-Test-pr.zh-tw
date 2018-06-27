---
title: '設定 Outlook 用戶端封鎖: Exchange 2013 Help'
TOCTitle: 設定 Outlook 用戶端封鎖
ms:assetid: 3a579c83-8bc7-4adc-a25c-8eb6eed7220c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd335207(v=EXCHG.150)
ms:contentKeyID: 51409172
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定 Outlook 用戶端封鎖

 

_**適用版本：**Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

在 Exchange Server 2013 中，您可以使用保留原則或受管理的資料夾，以進行通訊記錄管理 (MRM)。 只有執行 Microsoft Outlook 2010 和更新版本的使用者才能存取保留原則的所有用戶端功能。 但不管使用者的 Outlook 用戶端版本為何，「受管理的資料夾助理員」一律會將保留原則套用在 Mailbox Server 上。 較舊版的 Outlook 用戶端並不會顯示這些功能的 MRM 功能。 例如，因為 Outlook 2007 不支援保留原則，使用者無法將個人標籤套用到項目或資料夾上。

您可以封鎖執行舊版 Outlook 的使用者，使其無法存取 Exchange 信箱。 您也可以根據信箱或用戶端存取伺服器來封鎖存取權。

如需有關 MRM 的其他管理工作相關資訊，請參閱[通訊記錄管理程序](messaging-records-management-procedures-exchange-2013-help.md)。

## 用戶端應用程式及版本的 MRM 功能可用性

下表列出可在各種用戶端應用程式及版本中使用的 MRM 功能。

### MRM 功能

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>用戶端應用程式</th>
<th>可用的 MRM 用戶端功能</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2013 及 Outlook 2010</p></td>
<td><p>全部</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2007</p></td>
<td><p>受管理的資料夾</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 2003 和較舊版本</p></td>
<td><p>不支援</p></td>
</tr>
<tr class="even">
<td><p>其他電子郵件用戶端軟體</p></td>
<td><p>無</p></td>
</tr>
</tbody>
</table>


下表顯示 Outlook 的版本號碼。

### Outlook 版本

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Outlook 版本</th>
<th>版本號碼</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2013</p></td>
<td><p>15</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2010</p></td>
<td><p>14</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 2007</p></td>
<td><p>12</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2003</p></td>
<td><p>11</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 2002</p></td>
<td><p>10</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2000</p></td>
<td><p>9</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 98</p></td>
<td><p>8.5</p></td>
</tr>
<tr class="even">
<td><p>Outlook 97</p></td>
<td><p>8</p></td>
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
<td>進行任何變更之前，請注意 Hotfix 及 Service Pack 版本可能會影響用戶端版本字串。 因為伺服器端 Exchange 元件也必須使用 MAPI 登入，所以限制用戶端存取權時請小心。 部分元件會將它們的用戶端版本報告為元件名稱 (例如 SMTP 或 OLE DB)，而其他元件則會報告 Exchange 組建號碼 (例如 6.0.4712.0)。 因此，請避免限制其版本號碼為 6.&lt;<em>x</em>.<em>x</em>.&gt; 開頭的用戶端。 例如，若要完全防止 MAPI 存取，請指定兩個範圍，讓伺服器元件可以登入，而不要指定 <strong>0.0.0-6.5535.65535.65535</strong>。 例如，指定下列項目： <strong>0.0.0-5.9.9; 7.0.0-</strong>.</td>
</tr>
</tbody>
</table>


執行這些程序之後，請注意如果封鎖使用者使其無法存取他們的信箱，則他們會接收到下列警告訊息。


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>您的 Exchange Server 系統管理員已封鎖您正在使用的 Outlook 版本。 請連絡系統管理員，以取得協助。</p></td>
</tr>
</tbody>
</table>


若要略過指出執行 Outlook 2010 之前之 Outlook 版本的電子郵件用戶端不支援 MRM 功能的警告，則可以在命令介面中使用 **New-Mailbox**、**Enable-Mailbox** 及 **Set-Mailbox** 指令程式的 *ManagedFolderMailboxPolicyAllowed* 參數。 使用 *ManagedFolderMailboxPolicy* 參數將受管理的資料夾信箱原則指派給信箱時，除非使用 *ManagedFolderMailboxPolicyAllowed* 參數，否則預設會出現警告。

## 開始之前有哪些須知？

  - 預估完成時間： 1 分鐘。

  - 您無法使用 Exchange 系統管理中心 (EAC) 來執行這些程序。您必須使用命令介面。

  - 本主題中的程序需要特定權限。請查看每個程序以取得權限資訊。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

## 您要執行的工作

## 根據每個信箱來封鎖 Outlook 版本

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「使用者信箱」項目。

這個例子封鎖了所有 11.8010.8036 之前的 Outlook 版本。

    Set-CASMailbox -Identity adam@contoso.com -MAPIBlockOutlookVersions "-11.8010.8036"

此範例會還原由 Outlook 的版本封鎖之信箱的存取權。

    Set-CASMailbox -Identity adam@contoso.com -MAPIBlockOutlookVersions $null

如需詳細的語法及參數資訊，請參閱 [Set-CASMailbox](https://technet.microsoft.com/zh-tw/library/bb125264\(v=exchg.150\))。

## 封鎖 Client Access Server 上的 Outlook 版本

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [用戶端和行動裝置權限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主題中的「RPC 用戶端存取設定」項目。

這個例子封鎖了 12.0.0 版本之前的 Outlook 用戶端，使其無法存取 Exchange 2010 或更新版本之 Client Access Server 上的信箱。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>範例為與 <em>BlockedClientVersions</em> 參數搭配使用的值。您可以剖析 <code>%ExchangeInstallPath%Logging\RPC Client Access</code> 中的 RPC Client Access 記錄檔，以判斷正確的用戶端軟體版本。</td>
</tr>
</tbody>
</table>


    Set-RpcClientAccess -Server CAS01 -BlockedClientVersions "0.0.0-5.65535.65535;7.0.0;8.02.4-11.65535.65535"

如需詳細的語法及參數定義，請參閱 [Set-RpcClientAccess](https://technet.microsoft.com/zh-tw/library/dd351072\(v=exchg.150\))。

