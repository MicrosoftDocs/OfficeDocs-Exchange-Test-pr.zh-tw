---
title: '移除通訊清單: Exchange 2013 Help'
TOCTitle: 移除通訊清單
ms:assetid: 39a313f3-41d4-4c8f-af67-df2316f3687f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa997294(v=EXCHG.150)
ms:contentKeyID: 50472983
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 移除通訊清單

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-14_

本主題說明如何移除通訊清單。您無法移除預設全域通訊清單 (GAL)。

如需與通訊清單相關的其他管理工作，請參閱[地址清單程序](address-list-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [電子信箱地址與通訊錄權限](email-address-and-address-book-permissions-exchange-2013-help.md)主題中的「通訊清單」項目。

  - 您無法移除包含子通訊清單的父通訊清單。不過，您可以移除子與父通訊清單鍵盤上按下 CTRL 鍵並再選取 \[父項及子項地址清單。如果您嘗試移除父通訊清單，而不移除子位址清單，則會收到錯誤。

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

## 使用 EAC 來移除通訊清單

1.  瀏覽至 \[組織\] \> \[通訊清單\]。

2.  在清單檢視中，選擇想要移除的通訊清單，然後按一下 \[刪除\]![刪除圖示](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "刪除圖示")。

3.  請在警告中按一下 \[是\] 移除通訊清單。

## 使用命令介面來移除通訊清單

此範例會移除通訊清單 Sales Department，其中不包含子通訊清單。

    Remove-AddressList -Identity "Sales Department"

輸入 **Y** 以確認您要移除此通訊清單，然後按 ENTER。

如需詳細的語法及參數資訊，請參閱 [Remove-AddressList](https://technet.microsoft.com/zh-tw/library/bb124342\(v=exchg.150\))。

## 使用命令介面移除包含子通訊清單的通訊清單

此範例會移除父系通訊清單 Departments 與其所有子通訊清單。

    Remove-AddressList -Identity Departments -Recursive

輸入 **Y** 以確認您要移除父通訊清單以及其子通訊清單，然後按 ENTER。

如需詳細的語法及參數資訊，請參閱 [Remove-AddressList](https://technet.microsoft.com/zh-tw/library/bb124342\(v=exchg.150\))。

