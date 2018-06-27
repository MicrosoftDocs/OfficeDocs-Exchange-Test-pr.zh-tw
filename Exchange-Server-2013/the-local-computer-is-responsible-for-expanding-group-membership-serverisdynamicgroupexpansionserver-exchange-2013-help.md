---
title: '本機電腦負責展開群組 membership_ServerIsDynamicGroupExpansionServer: Exchange 2013 Help'
TOCTitle: 本機電腦負責展開群組 membership_ServerIsDynamicGroupExpansionServer
ms:assetid: f6fdd8e1-fda1-45be-b8a2-0d356dbe7d83
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.serverisdynamicgroupexpansionserver(v=EXCHG.150)
ms:contentKeyID: 50474613
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 本機電腦負責展開群組 membership\_ServerIsDynamicGroupExpansionServer

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2012-06-05_

此主題中的內容尚未針對 Microsoft Exchange Server 2013 進行更新。在更新之前，可能還是適用於 Exchange 2013。如果您仍然需要幫助，請查看下方的社群資源。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft® Exchange Server 2007 安裝程式無法繼續因為嘗試解除安裝集線傳輸角色，負責展開群組成員資格失敗。

Exchange 2007 安裝需要的通訊群組清單延伸移除目前的 Bridgehead 伺服器之前要解除安裝集線傳輸角色。

擴充通訊群組清單的啟用識別碼的個別收件者屬於通訊群組清單，可以識別或其他通訊群組的識別列出擴充。展開通訊群組清單可以傳回任何必要的傳遞狀態通知 (DSN) 的路徑。Dsn 通知的 Microsoft Exchange 系統管理員或電子郵件寄件者的特定電子郵件訊息的狀態。此外，通訊群組清單延伸識別是否不在辦公室訊息或自動產生的回覆應該傳送給原始郵件的寄件者。

若要解決此問題，請移至另一部伺服器的通訊群組擴充和重新執行 Microsoft Exchange 安裝程式。

若要變更通訊群組或動態通訊群組擴充伺服器

1.  開啟 Exchange 管理主控台。

2.  在主控台樹狀目錄中展開 \[**收件者組態**\]。

3.  在主控台樹狀目錄中，按一下 \[**通訊群組**。

4.  建立檢視所有通訊群組和動態通訊群組擴充伺服器以使用目前的 Bridgehead 伺服器篩選。
    
    1.  在 \[動作\] 窗格中，按一下 \[**建立篩選器\]**。
    
    2.  在 \[屬性\] 下拉式清單中，按一下 \[**擴充伺服器**。
    
    3.  在 \[運算子\] 下拉式清單中，按一下 \[**等於**\]。
    
    4.  在 \[值\] 方塊中，按一下 \[**瀏覽**\] 按鈕以選取 Bridgehead 伺服器的目前做為擴充伺服器。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>下一個步驟是選擇性的。</td>
</tr>
</tbody>
</table>


1.  按一下 \[**新增運算式**，以指定其他的篩選準則。會顯示符合所有的篩選條件的郵件。

2.  按一下 \[**套用篩選**\]。會顯示符合篩選準則的結果。

<!-- end list -->

1.  在 \[結果\] 窗格中，按一下您想要變更的擴充伺服器的通訊群組，然後按一下 \[動作\] 窗格中的**內容**。

2.  在**屬性**，按一下 \[**進階**\] 索引標籤。

3.  在 \[擴充伺服器\] 下拉式清單中，從清單中選取特定伺服器或選取**組織中的任何伺服器**。

4.  針對所有通訊群組或使用 Bridgehead 伺服器做為其擴充伺服器的動態通訊群組重複步驟 5 到 7。

