---
title: '從 Exchange 中移除 Outlook Web App 信箱原則: Exchange Online Help'
TOCTitle: 從 Exchange 中移除 Outlook Web App 信箱原則
ms:assetid: edab7bac-b62c-4b82-8f21-dcac77cf0e8f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd351239(v=EXCHG.150)
ms:contentKeyID: 50474542
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 從 Exchange 中移除 Outlook Web App 信箱原則

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2013-03-15_

您可以使用 EAC 或命令介面，從 Microsoft 組織中移除 Outlook Web AppExchange 信箱原則。

如需其他與 Outlook Web App 信箱原則相關的管理工作，請參閱 [Outlook Web App 信箱原則](outlook-web-app-mailbox-policies-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 完成每項程序預估時間： 3 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [用戶端和行動裝置權限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主題中的「Outlook Web App 信箱原則」項目。

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

## 使用 EAC 移除 Outlook Web App 信箱原則

1.  在系統管理中心中，按一下 \[權限\] \> \[Outlook Web App 原則\]。

2.  在結果窗格中，按一下以選取您要移除的信箱原則。

3.  按一下 \[刪除\] 按鈕。

4.  在確認視窗中，按一下 **\[是\]** 以移除信箱原則，或按一下 **\[否\]** 取消。

## 使用命令介面移除 Outlook Web App 信箱原則

此範例會移除名為  `Policy1` 的 Outlook Web App 信箱原則。

    Remove-OwaMailboxPolicy -Name Policy1 

如需語法及參數的相關資訊，請參閱 [Remove-OwaMailboxPolicy](https://technet.microsoft.com/zh-tw/library/dd298103\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要確認您是否已成功移除 Outlook Web App 信箱原則：

  - 在 EAC 中，按一下 \[**權限**\> **Outlook Web App 原則**。您移除原則應不再出現在清單中。

