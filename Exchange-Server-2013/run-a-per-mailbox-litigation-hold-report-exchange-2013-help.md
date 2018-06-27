---
title: '執行個別信箱訴訟資料暫留報告: Exchange Online Help'
TOCTitle: 執行個別信箱訴訟資料暫留報告
ms:assetid: 98c46226-2f48-42c6-a741-34bb5944f519
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ150542(v=EXCHG.150)
ms:contentKeyID: 50472334
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 執行個別信箱訴訟資料暫留報告

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2012-10-13_

如果您的組織與法律有關，您必須採取步驟來保留相關的資料，例如可能可當作的電子郵件訊息。在類似的情況下，您可以使用訴訟資料暫留保留所有電子郵件傳送和接收由特定人員或保留所有電子郵件傳送和接收在您的組織在特定時間期間。如需關於信箱時會發生什麼情況處於訴訟暫止狀態以及如何啟用和停用它，請參閱[管理使用者信箱](manage-user-mailboxes-exchange-2013-help.md)中的 「 信箱功能 」 章節。

您可以使用訴訟暫止報告來追蹤在給定的期間內，對某個信箱所做的以下變更類型：

  - 訴訟暫止已啟用。

  - 訴訟暫止已停用。

對於每一種變更類型而言，報告都會包含進行變更的使用者以及變更的時間和日期。

## 開始之前有哪些須知？

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [Exchange 及命令介面基礎結構權限](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)主題中的「僅檢視系統管理員稽核記錄」項目。

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


## 使用 EAC 執行訴訟暫止報告

1.  在 EAC 中，瀏覽至 \[規範管理\] \> \[稽核\]。

2.  按一下 \[執行每個信箱的訴訟資料暫留報告\]。
    
    Microsoft Exchange 會針對在過去兩週以來對信箱所做的訴訟暫止變更執行報告。

3.  若要檢視特定信箱、 變更在搜尋結果\] 窗格中，選取的信箱。在詳細資料窗格中檢視搜尋結果。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>要縮小搜尋結果吗？選取的開始日期、 結束日期] 或兩者，然後選取特定信箱搜尋。按一下 [<strong>搜尋</strong>重新執行 [報告]。</td>
</tr>
</tbody>
</table>


## 如何才能了解這是否正常運作？

若要確認您是否已成功執行訴訟暫止狀態報表有訴訟保留搜尋結果\] 窗格中顯示變更的日期範圍內的信箱。如果不有任何結果，然後訴訟資料暫留未變更發生的日期範圍內或最新變更尚未尚未採取效果。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當信箱放置了訴訟暫止時，可能需要 60 分鐘才會使訴訟暫止生效。</td>
</tr>
</tbody>
</table>

