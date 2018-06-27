---
title: '停用或啟用 Exchange 搜尋: Exchange 2013 Help'
TOCTitle: 停用或啟用 Exchange 搜尋
ms:assetid: 195b25be-53fb-4215-90a5-04340d640bcc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa996416(v=EXCHG.150)
ms:contentKeyID: 52062519
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 停用或啟用 Exchange 搜尋

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-05-07_

依預設，所有新的信箱資料庫都會啟用 Exchange 搜尋，不需要額外的設定。不過，如果想要讓 Exchange 搜尋停止建立信箱內容的索引，您可以停用個別信箱資料庫或整個信箱伺服器的這項功能。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>停用 Exchange 搜尋會影響全文搜尋的功能和效能，這些搜尋是使用者在線上模式或在 Windows 行動裝置上使用 Outlook 執行的。<br />
<a href="in-place-ediscovery-exchange-2013-help.md">就地 eDiscovery</a> 也依賴 Exchange 搜尋。如果您針對信箱資料庫或 Mailbox Server 停用 Exchange 搜尋，則就地 eDiscovery 搜尋就不會從資料庫或伺服器傳回任何郵件。</td>
</tr>
</tbody>
</table>


如需其他與 Exchange 搜尋相關的管理工作，請參閱 [Exchange 搜尋程序](exchange-search-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：1 分鐘

  - 本主題中的程序需要特定權限。請查看每個程序以取得權限資訊。

  - 您可以針對伺服器或信箱資料庫啟用或停用 Exchange 搜尋，但針對個別信箱使用者則不能這麼做。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

## 您要執行的工作

## 針對信箱資料庫停用或啟用 Exchange 搜尋

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「Exchange 搜尋」項目。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您無法使用 EAC，來針對信箱資料庫停用或啟用 Exchange 搜尋。</td>
</tr>
</tbody>
</table>


此命令會針對名稱為 EXCH01 的信箱資料庫停用 Exchange 搜尋。

    Set-MailboxDatabase "Mailbox Database (EXCH01)" -IndexEnabled $false

此命令會針對名稱為 EXCH01 的信箱資料庫啟用 Exchange 搜尋。

    Set-MailboxDatabase "Mailbox Database (EXCH01)" -IndexEnabled $true

如需詳細語法及參數的資訊，請參閱[Set-MailboxDatabase](https://technet.microsoft.com/zh-tw/library/bb123971\(v=exchg.150\))。

## 針對信箱伺服器停用或啟用 Exchange 搜尋

若要針對信箱伺服器停用 Exchange 搜尋，您必須停用並停止 Microsoft Exchange 搜尋服務。同樣地，若要針對信箱伺服器啟用 Exchange 搜尋，您必須啟用並啟動 Microsoft Exchange 搜尋服務。您可以使用服務主控台或命令介面執行此程序。

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「管理 Mailbox Server 上的 Exchange 搜尋服務」項目。

**使用服務主控台**

1.  移至 **\[開始\]** \> **\[系統管理工具\]** \> **\[服務\]**。

2.  在 **\[服務\]** 詳細資料窗格中，以滑鼠右鍵按一下 **\[Microsoft Exchange 搜尋\]** 服務，然後選取 **\[內容\]**。

3.  在 **\[一般\]** 索引標籤的 **\[啟動類型\]** 清單中，選取 **\[已停用\]** 以停用服務，或選取 **\[自動\]** 以自動啟動服務。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>啟動類型會在下次嘗試啟動此服務時 (伺服器重新啟動後自動啟動服務或手動啟動服務時) 影響服務。在下一個步驟中，會手動停止或啟動服務。</td>
    </tr>
    </tbody>
    </table>


4.  按一下 **\[停止\]** 以停止服務；或按一下 **\[啟動\]** 以啟動服務。

5.  按一下 **\[確定\]**，儲存變更。

**使用命令介面**

執行下列命令來停止並停用 Microsoft Exchange 搜尋服務。

    Stop-Service MSExchangeFastSearch

    Set-Service MSExchangeFastSearch -StartupType Disabled

執行下列命令將 Exchange 搜尋服務設定為自動啟動，然後啟動此服務。

    Set-Service MSExchangeFastSearch -StartupType Automatic

    Start-Service MSExchangeFastSearch

