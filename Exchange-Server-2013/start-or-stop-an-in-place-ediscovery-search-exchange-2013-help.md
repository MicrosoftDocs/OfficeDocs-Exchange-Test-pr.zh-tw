---
title: '啟動或停止就地 eDiscovery 搜尋: Exchange Online Help'
TOCTitle: 啟動或停止就地 eDiscovery 搜尋
ms:assetid: 0d546763-4bf5-4523-91f4-d181b7ee4ac2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd335090(v=EXCHG.150)
ms:contentKeyID: 50472545
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟動或停止就地 eDiscovery 搜尋

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-07-14_

可於任何時間停止或重新啟動就地 eDiscovery 搜尋。 例如，若您要修改搜尋內容 (例如搜尋的關鍵字或信箱)，則必須先停止搜尋。 然後，您可以在進行必要的變更後重新啟動搜尋。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若您重新啟動就地 eDiscovery 搜尋，複製到搜尋中指定的探索信箱之結果將被移除。</td>
</tr>
</tbody>
</table>


## 開始之前有哪些須知？

  - 預估完成時間： 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「就地 eDiscovery」項目。

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

## 使用 EAC 來開始或停止就地 eDiscovery 搜尋

1.  瀏覽至 \[規範管理\] \> \[就地 eDiscovery 和保留\]。

2.  若要停止處理中的搜尋，請選擇搜尋然後按一下 \[停止搜尋\]。

3.  若要開始已停止的搜尋，請選擇搜尋然後按一下 \[繼續搜尋\]。

## 使用命令見面來開始或停止就地 eDiscovery 搜尋

如需如何開始就地 eDiscovery 搜尋的範例，請參閱 [Start-MailboxSearch](https://technet.microsoft.com/zh-tw/library/dd351245\(v=exchg.150\)) 中的「範例 1」。

如需如何停止就地 eDiscovery 搜尋的範例，請參閱 [Stop-MailboxSearch](https://technet.microsoft.com/zh-tw/library/dd351075\(v=exchg.150\)) 中的「範例 1」。

