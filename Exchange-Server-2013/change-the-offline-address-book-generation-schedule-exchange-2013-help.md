---
title: '變更離線通訊錄產生排程: Exchange Online Help'
TOCTitle: 變更離線通訊錄產生排程
ms:assetid: d2b4d527-311e-442d-9f1f-54fac8371b80
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124719(v=EXCHG.150)
ms:contentKeyID: 50474324
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.Mailbox.OfflineAddressBookGeneralPage
ms.translationtype: HT
---

# 變更離線通訊錄產生排程

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-12-05_

離線通訊錄 (OAB) 是已下載的通訊錄副本，讓 Outlook 使用者可以在與伺服器中斷連線時存取其所包含的資訊。您可以使用 Set-MailboxServer Cmdlet 上的 *OABGeneratorWorkCycle* 與 *OABGeneratorWorkCycleCheckpoint* 參數設定產生 OAB 的頻率。

如需與 OAB 相關的其他管理工作，請參閱[離線通訊錄程序](offline-address-book-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱[電子信箱地址與通訊錄權限](email-address-and-address-book-permissions-exchange-2013-help.md)主題中的「離線通訊錄」項目。

  - 您無法使用 Exchange 系統管理中心 (EAC) 執行此程序。您必須使用命令介面。

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


## 使用命令介面設定 OAB 內容

在此範例中，信箱通訊錄 MBXServer01 上每天每隔六小時產生一次離線通訊錄。

    Set-MailboxServer -Identity MBXServer01 -OABGeneratorWorkCycle 01.00:00:00 -OABGeneratorWorkCycleCheckpoint 06:00:00 

如需詳細的語法及參數資訊，請參閱 [Set-OfflineAddressBook](https://technet.microsoft.com/zh-tw/library/aa996330\(v=exchg.150\))。

