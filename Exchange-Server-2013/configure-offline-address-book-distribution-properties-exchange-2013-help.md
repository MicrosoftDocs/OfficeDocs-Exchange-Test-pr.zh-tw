---
title: '設定離線通訊錄通訊群組屬性: Exchange Online Help'
TOCTitle: 設定離線通訊錄通訊群組屬性
ms:assetid: 8df985e9-75ba-47ea-9cc3-aa98a5d8acf4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb123710(v=EXCHG.150)
ms:contentKeyID: 50473703
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.ClientAccess.OabDistributionGeneralPage
ms.translationtype: MT
---

# 設定離線通訊錄通訊群組屬性

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2012-10-14_

您可以在 Exchange 中為每個離線通訊錄 OAB 發佈點設定二個 URL：一個是內部 URL，只能從您公司的內部網路存取；一個是外部 URL，可從網際網路存取。

如需與 OAB 相關的其他管理工作，請參閱[離線通訊錄程序](offline-address-book-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [電子信箱地址與通訊錄權限](email-address-and-address-book-permissions-exchange-2013-help.md)主題中的「離線通訊錄」項目。

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


## 使用命令介面設定 OAB 發佈內容

此範例在 OAB 虛擬目錄 OAB (預設網站) 上設定 OAB 發佈的輪詢間隔為 6 小時。

    Set-OABVirtualDirectory "OAB (Default Web Site)" -PollInterval 360

此範例為預設 OAB 虛擬目錄 OAB (預設網站) 設定外部發佈點為 https://contoso.com/OAB。

    Set-OABVirtualDirectory "OAB (Default Web Site)" -ExternalUrl https://contoso.com/OAB

如需詳細的語法及參數資訊，請參閱 [Set-OabVirtualDirectory](https://technet.microsoft.com/zh-tw/library/bb124707\(v=exchg.150\))。

## 詳細資訊

[離線通訊錄](offline-address-books-exchange-2013-help.md)

