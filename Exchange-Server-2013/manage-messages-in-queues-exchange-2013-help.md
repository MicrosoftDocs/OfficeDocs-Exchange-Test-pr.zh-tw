---
title: '管理佇列中的郵件: Exchange 2013 Help'
TOCTitle: 管理佇列中的郵件
ms:assetid: 83358884-6036-4e91-87a8-35200541874d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb123535(v=EXCHG.150)
ms:contentKeyID: 51409223
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理佇列中的郵件

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-05-07_

在 Microsoft Exchange Server 2013 中，您可以使用 Exchange 工具箱中的佇列檢視器或 Exchange 管理命令介面來管理佇列中的郵件。如需在 Exchange 管理命令介面中使用郵件管理指令程式的相關資訊，請參閱[使用 Exchange 管理命令介面管理佇列](use-the-exchange-management-shell-to-manage-queues-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：15 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「佇列」項目。

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

## 移除佇列中的郵件

要傳送給多位收件者的郵件可能會存放在多個佇列中。若要在單一作業中移除來自多個佇列中的訊息，您必須使用篩選器。您可以選擇是否要在移除佇列中的郵件時傳送未傳遞回報 (NDR)。您無法移除提交佇列中的郵件。

## 使用 Exchange 工具箱中的佇列檢視器來移除郵件

1.  按一下 \[開始\] \> \[所有程式\] \> \[Microsoft Exchange 2013\] \> \[Exchange 工具箱\]。

2.  在 \[郵件流程工具\] 區段下，按兩下 \[佇列檢視器\]，在新視窗中開啟工具。

3.  在佇列檢視器中，按一下 \[郵件\] 索引標籤。畫面會顯示所連線之伺服器上所有郵件的清單。若要調整單一佇列的動作，請按一下 **\[佇列\]** 索引標籤，連按兩下佇列名稱，再按一下出現的 *\[服器佇列\]* 索引標籤。

4.  選取清單中的一或多則郵件，按一下滑鼠右鍵，然後選取 **\[移除郵件 (含未傳遞回報 (NDR))\]** 或 **\[移除郵件 (不含未傳遞回報 (NDR))\]**。此時會出現一個對話方塊，確認選取的動作並顯示 \[您要繼續嗎?\]按一下 **\[是\]**。

5.  若要移除特定佇列中的所有郵件，請按一下 \[佇列\] 索引標籤。選取一個佇列，按一下滑鼠右鍵，然後選取 **\[移除郵件 (含未傳遞回報 (NDR))\]** 或 **\[移除郵件 (不含未傳遞回報 (NDR))\]**。此時會出現一個對話方塊，確認選取的動作並顯示 **\[您要繼續嗎?\]**按一下 **\[是\]**。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>若您使用的是篩選過的清單，則所顯示的頁面可能不會包括篩選器中的所有項目。在這種情況下會出現下列提示：<strong>此動作將影響這個頁面上的所有項目。若要擴充此動作的範圍以納入此篩選中所有的項目，請先核取下列方塊，然後按一下 [確定]。</strong></td>
    </tr>
    </tbody>
    </table>


## 使用命令介面來移除郵件

若要從佇列移除郵件，請使用下列語法。

    Remove-Message <-Identity MessageIdentity | -Filter {MessageFilter}> -WithNDR <$true | $false>

此範例會移除佇列中主旨為「Win Big」的郵件，但不傳送 NDR。

    Remove-Message -Filter {Subject -eq "Win Big"} -WithNDR $false

此範例會從 Mailbox01 伺服器上無法存取的佇列中移除郵件 ID 為 3 的郵件，並傳送 NDR。

    Remove-Message -Identity Mailbox01\Unreachable\3 -WithNDR $true

## 如何知道這是否正常運作？

若要確認您是否已成功移除佇列中的郵件，請執行下列其中一項操作：

  - 在佇列檢視器中，選取佇列或建立篩選器，確認郵件已不再存在。

  - 使用 **Get-Message** 指令程式搭配 *Queue* 或 *Filter* 參數，確認郵件已不再存在。如需詳細資訊，請參閱 [Get-Message](https://technet.microsoft.com/zh-tw/library/bb124738\(v=exchg.150\))。

## 移除佇列中的郵件

您可繼續目前狀態為 \[已擱置\] 的郵件。繼續郵件，表示進行傳遞郵件。如果您繼續位於有害郵件佇列中的郵件，則會將郵件傳送到分類程式進行處理。正要傳送給多位收件者的訊息可能會在多個佇列中。若要在單一作業中繼續進行位於多個佇列中的郵件，您必須使用篩選。

## 使用 Exchange 工具箱中的佇列檢視器來繼續傳送郵件

1.  按一下 \[開始\] \> \[所有程式\] \> \[Microsoft Exchange 2013\] \> \[Exchange 工具箱\]。

2.  在 \[郵件流程工具\] 區段下，按兩下 \[佇列檢視器\]，在新視窗中開啟工具。

3.  在佇列檢視器中，按一下 \[郵件\] 索引標籤。畫面會顯示所連線之伺服器上所有郵件的清單。若要將動作調整為著重在單一佇列，請按一下 \[佇列\] 索引標籤，連按兩下佇列名稱，再按一下出現的 *\[伺服器\\佇列\]* 索引標籤。

4.  按一下 \[建立篩選器\]，並輸入篩選器運算式，如下所示：
    
    1.  從郵件內容下拉式清單中選取 \[狀態\]。
    
    2.  從比較運算子下拉式清單中選取 \[等於\]。
    
    3.  從值下拉式清單中選取 \[已擱置\]。

5.  按一下 \[套用篩選器\]。隨即顯示狀態為 \[已擱置\] 的所有郵件。

6.  從清單中選取一或多封郵件、按一下滑鼠右鍵，然後選取 \[繼續\]。

## 使用命令介面來繼續傳送郵件

若要繼續傳送郵件，請使用下列語法：

    Resume-Message <-Identity MessageIdentity | -Filter {MessageFilter}>

此範例會繼續 Contoso.com 網域中從任何寄件者傳送的所有郵件。

    Resume-Message -Filter {FromAddress -eq "*contoso.com"}

此範例會繼續伺服器 Hub01 上無法存取之佇列中訊息識別碼為 3 的郵件。

    Resume-Message -Identity Hub01\Unreachable\3

若要重新提交有害郵件佇列中的郵件，請執行下列其中一個步驟：

## 如何知道這是否正常運作？

若要確認您是否已成功繼續傳送佇列中的郵件，請執行下列其中一項操作：

  - 在佇列檢視器中，選取佇列或建立篩選器，確認郵件不再擱置。

  - 使用 **Get-Message** 指令程式搭配 *Queue* 或 *Filter* 參數，確認郵件不再擱置。如需詳細資訊，請參閱 [Get-Message](https://technet.microsoft.com/zh-tw/library/bb124738\(v=exchg.150\))。

請注意，如果在伺服器上的任何佇列中找不到此郵件，這可能表示此郵件已成功傳遞至下一個躍點。

## 擱置佇列中的郵件

擱置郵件時可以防止傳遞郵件。出現在佇列中但正在傳遞的郵件將無法擱置。傳遞將會繼續，而且郵件的狀態會是 **PendingSuspend**。如果傳遞失敗，郵件將會重新進入佇列，然後郵件會被擱置。您無法擱置提交佇列或有害郵件佇列中的郵件。

正要傳送給多位收件者的訊息可能會在多個佇列中。若要在單一作業中擱置位於多個佇列中的郵件，您必須使用篩選器。

## 使用 Exchange 工具箱中的佇列檢視器來擱置郵件

1.  按一下 \[開始\] \> \[所有程式\] \> \[Microsoft Exchange 2013\] \> \[Exchange 工具箱\]。

2.  在 \[郵件流程工具\] 區段下，按兩下 \[佇列檢視器\]，在新視窗中開啟工具。

3.  在佇列檢視器中，按一下 \[郵件\] 索引標籤。畫面會顯示所連線之伺服器上所有郵件的清單。若要限制為單一佇列的檢視，請按一下 \[佇列\] 索引標籤，按兩下佇列名稱，再按一下出現的 \[*伺服器\\佇列*\] 索引標籤。

4.  選取一或多封郵件，並在其上按一下滑鼠右鍵，然後選取 \[擱置\]。

## 使用命令介面擱置郵件

若要擱置郵件，請使用下列語法：

    Suspend-Message <-Identity MessageIdentity | -Filter {MessageFilter}>

此範例會擱置佇列中來自 contoso.com 網域之任何寄件者的所有郵件。

    Suspend-Message -Filter {FromAddress -eq "*contoso.com"}

此範例會擱置 Mailbox01 伺服器上無法存取之佇列中郵件識別碼為 3 的郵件：

    Suspend-Message -Identity Mailbox01\Unreachable\3

## 如何知道這是否正常運作？

若要確認您是否已成功擱置佇列中的郵件，請執行下列其中一項操作：

  - 在佇列檢視器中，選取佇列或建立篩選器，確認郵件已擱置。

  - 使用 **Get-Message** 指令程式搭配 *Queue* 或 *Filter* 參數，確認郵件已擱置。如需詳細資訊，請參閱 [Get-Message](https://technet.microsoft.com/zh-tw/library/bb124738\(v=exchg.150\))。

