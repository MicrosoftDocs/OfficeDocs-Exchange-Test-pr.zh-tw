---
title: '移除就地 eDiscovery 搜尋: Exchange Online Help'
TOCTitle: 移除就地 eDiscovery 搜尋
ms:assetid: 78461a78-1255-4a26-9d36-c6b8eb82a4f9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd298078(v=EXCHG.150)
ms:contentKeyID: 50473557
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 移除就地 eDiscovery 搜尋

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-07-14_

在 Microsoft Exchange Server 2013，您可以使用就地 eDiscovery 來搜尋信箱內容。您可以移除任何時候就地 eDiscovery 搜尋。當您移除的就地 eDiscovery 搜尋時，搜尋結果移除探索信箱。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>刪除就地 eDiscovery 搜尋將會移除任何搜尋結果複製到探索信箱。</td>
</tr>
</tbody>
</table>


## 開始之前有哪些須知？

  - 預估完成時間： 2-5 分鐘。

  - 若要移除已啟用的就地保留就地 eDiscovery 搜尋，您必須先移除就地保留搜尋。如需詳細資訊，請參閱[建立或移除就地保留](create-or-remove-an-in-place-hold-exchange-2013-help.md)。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「就地 eDiscovery」項目。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

## 您要執行的工作

## 使用 EAC 來移除就地 eDiscovery 搜尋

1.  瀏覽至 \[規範管理\] \> \[就地 eDiscovery 和保留\]。

2.  在清單檢視中，選取您要移除的就地 eDiscovery 搜尋和 \[**刪除**![刪除圖示](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "刪除圖示")。

## 使用命令介面來移除就地 eDiscovery 搜尋

如何移除就地 eDiscovery 搜尋的範例，請參閱[Remove-MailboxSearch](https://technet.microsoft.com/zh-tw/library/dd298130\(v=exchg.150\))「 範例 」 一節。

## 如何知道這是否正常運作？

若要確認您已成功移除就地 eDiscovery 搜尋，請執行下列其中一項：

  - 使用 EAC 來確認搜尋都不再出現在清單檢視中的 \[**就地 eDiscovery 和保留**\] 索引標籤。

  - 使用**Get-MailboxSearch**指令程式來擷取在就地 eDiscovery 搜尋。如何擷取就地 eDiscovery 搜尋的範例，請參閱[Get-MailboxSearch](https://technet.microsoft.com/zh-tw/library/dd351021\(v=exchg.150\))「 範例 」 一節。

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

