---
title: '更新離線通訊錄: Exchange Online Help'
TOCTitle: 更新離線通訊錄
ms:assetid: 448a207e-41b4-4cef-9fe9-a68b81e2ec4e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa997684(v=EXCHG.150)
ms:contentKeyID: 50473147
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 更新離線通訊錄

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2013-11-15_

在建立 OAB 或修改 OAB 設定之後，所做的變更要等到 OAB 產生 (OABGen) 處理程序完成後才可供使用者使用。

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


## 使用命令介面更新 OAB

此範例會更新名為 My OAB 的 OAB。

    Update-OfflineAddressBook -Identity "My OAB"

如需詳細的語法及參數資訊，請參閱 [Update-OfflineAddressBook](https://technet.microsoft.com/zh-tw/library/aa995979\(v=exchg.150\))。

