---
title: '管理佇列: Exchange 2013 Help'
TOCTitle: 管理佇列
ms:assetid: 37f11378-a884-4aff-ab55-689f40a46321
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa997263(v=EXCHG.150)
ms:contentKeyID: 51409181
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理佇列

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-01-31_

在 Microsoft Exchange Server 2013 中，您可以使用 Exchange 工具箱或 Exchange 管理命令介面中的佇列檢視器來管理佇列。如需在 Exchange 管理命令介面中使用佇列管理指令程式的詳細資訊，請參閱[使用 Exchange 管理命令介面管理佇列](use-the-exchange-management-shell-to-manage-queues-exchange-2013-help.md)。

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

## 檢視佇列

## 使用 Exchange 工具箱內的佇列檢視器來檢視佇列

1.  按一下 \[開始\] \> \[所有程式\] \> \[Microsoft Exchange 2013\] \> \[Exchange 工具箱\]。

2.  在 \[郵件流程工具\] 區段下，按兩下 \[佇列檢視器\]，在新視窗中開啟工具。

3.  在佇列檢視器中，按一下 \[佇列\] 索引標籤。畫面會顯示所連線之伺服器上所有佇列的清單。

4.  您可以使用執行窗格中的 **\[匯出清單\]** 連結來匯出佇列的清單。如需詳細資訊，請參閱 [從佇列檢視器中匯出清單](export-lists-from-queue-viewer-exchange-2013-help.md)。

## 使用命令介面檢視佇列

若要檢視佇列，請使用下列語法。

    Get-Queue [-Filter <Filter> -Server <ServerIdentity> -Include <Internal | External | Empty | DeliveryType> -Exclude <Internal | External | Empty | DeliveryType>]

此範例會顯示名為 Mailbox01 之 Exchange 2013 Mailbox Server 上所有非空白之佇列的基本資訊。

    Get-Queue -Server Mailbox01 -Exclude Empty

此範例會顯示執行命令之 Mailbox Server 上所有含有超過 100 封郵件之佇列的詳細資訊。

    Get-Queue -Filter {MessageCount -gt 100} | Format-List

## 使用命令介面來檢視多部 Exchange 伺服器上的佇列摘要資訊

**Get-QueueDigest** 指令程式可提供特定範圍中所有伺服器上的佇列狀態高階、彙總檢視，例如 DAG、Active Directory 站台、伺服器清單，或是整個 Active Directory 樹系。請注意，結果中不會包含周邊網路中已訂閱的 Edge Transport Server 上的佇列。此外，**Get-QueueDigest** 也可在 Edge Transport Server 上使用，但結果只會顯示 Edge Transport Server 上的佇列。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>依預設，<strong>Get-QueueDigest</strong> 指令程式會顯示包含十封郵件以上的傳遞佇列，而且會是一到二分鐘之前的結果。如需如何變更這些預設值的指示，請參閱<a href="configure-get-queuedigest-exchange-2013-help.md">設定 Get-QueueDigest</a>。</td>
</tr>
</tbody>
</table>


若要檢視多部 Exchange 伺服器上的佇列摘要資訊，請執行以下命令：

    Get-QueueDigest <-Server <ServerIdentity1,ServerIdentity2,..> | -Dag <DagIdentity1,DagIdentity2...> | -Site <ADSiteIdentity1,ADSiteIdentity2...> | -Forest> [-Filter <Filter>]

此範例會針對名為 FirstSite 之 Active Directory 站台內的所有 Exchange 2013 Mailbox Server，顯示郵件計數大於 100 之佇列的摘要資訊。

    Get-QueueDigest -Site FirstSite -Filter {MessageCount -gt 100}

此範例會針對名為 DAG01 之資料庫可用性群組 (DAG) 中的所有 Exchange 2013 Mailbox Server，顯示佇列狀態值為 **Retry** 之佇列的摘要資訊。

    Get-QueueDigest -Dag DAG01 -Filter {Status -eq "Retry"}

## 繼續佇列

繼續佇列，表示可重新啟動狀態為 \[已擱置\] 之佇列上的外寄活動。佇列的狀態必須是 \[已擱置\]，這個動作才會生效。當您繼續佇列時，佇列中的郵件狀態並不會改變。具有 \[已擱置\] 狀態的郵件仍然會維持擱置狀態，不會離開佇列。

## 使用 Exchange 工具箱內的佇列檢視器來繼續佇列

1.  按一下 \[開始\] \> \[所有程式\] \> \[Microsoft Exchange 2013\] \> \[Exchange 工具箱\]。

2.  在 \[郵件流程工具\] 區段下，按兩下 \[佇列檢視器\]，在新視窗中開啟工具。

3.  在佇列檢視器中，按一下 \[佇列\] 索引標籤。畫面會顯示所連線之伺服器上所有佇列的清單。

4.  按一下 **\[建立篩選器\]**，並輸入篩選器運算式，如下所示：
    
    1.  從佇列內容下拉式清單中選取 **\[狀態\]**。
    
    2.  從比較運算子下拉式清單中選取 **\[等於\]**。
    
    3.  從值下拉式清單中選取 **\[已擱置\]**。

5.  按一下 **\[套用篩選器\]**。即會顯示伺服器上目前擱置中的所有佇列。

6.  從清單中選取一或多個佇列、按一下滑鼠右鍵，然後選取 **\[繼續\]**。

## 使用命令介面繼續佇列

若要繼續佇列，請使用下列語法。

    Resume-Queue <-Identity QueueIdentity | -Filter {QueueFilter} [-Server ServerIdentity]>

此範例會繼續本機伺服器上具有 \[擱置中\] 狀態的所有佇列。

    Resume-Queue -Filter {Status -eq "Suspended"}

此範例會繼續名為 Mailbox01 之伺服器上名為 contoso.com 的擱置中傳遞佇列。

    Resume-Queue -Identity Mailbox01\contoso.com

## 如何知道這是否正常運作？

若要確認您是否已成功繼續佇列，請執行下列動作：

1.  使用佇列檢視器或 **Get-Queue** 指令程式來尋找您嘗試繼續的佇列。

2.  確認佇列的 **Status** 內容值不是 `Suspended`。

## 重試佇列

當傳輸伺服器無法連接至下一個躍點時，傳遞佇列就會處於 \[重試\] 狀態。當您使用佇列檢視器或命令介面來重試傳遞佇列時，便會立即強制進行連線嘗試，並且覆寫所排定的下一次重試時間。如果連線未成功，就會重設重試間隔計時器。傳遞佇列必須處於 \[重試\] 狀態，此動作才能生效。

## 使用 Exchange 工具箱內的佇列檢視器來重試佇列

1.  按一下 \[開始\] \> \[所有程式\] \> \[Microsoft Exchange 2013\] \> \[Exchange 工具箱\]。

2.  在 \[郵件流程工具\] 區段下，按兩下 \[佇列檢視器\]，在新視窗中開啟工具。

3.  在佇列檢視器中，按一下 \[佇列\] 索引標籤。畫面會顯示所連線之伺服器上所有佇列的清單。

4.  按一下 **\[建立篩選器\]**，並輸入篩選器運算式，如下所示：
    
    1.  從佇列內容下拉式清單中選取 **\[狀態\]**。
    
    2.  從比較運算子下拉式清單中選取 **\[等於\]**。
    
    3.  從值下拉式清單中選取 **\[重試\]**。

5.  按一下 **\[套用篩選器\]**。會顯示目前處於 **\[重試\]** 狀態的所有佇列。

6.  從清單中選取一個或多個佇列。按一下滑鼠右鍵，再選取 **\[重試佇列\]**。如果連線嘗試成功，佇列狀態會變更為 **\[使用中\]**。如果無法建立連線，佇列會繼續維持 **\[重試\]** 狀態，並更新下一個重試時間。

## 使用命令介面來重試佇列

若要重試佇列，請使用下列語法。

    Retry-Queue <-Identity QueueIdentity | -Filter QueueFilter [-Server ServerIdentity]>

此範例會重試本機伺服器上所有處於 \[重試\] 狀態的佇列。

    Retry-Queue -Filter {status -eq "retry"}

此範例會重試名為 Mailbox01 之伺服器上名為 contoso.com 且處於 `Retry` 狀態的佇列。

    Retry-Queue -Identity Mailbox01\contoso.com

## 如何知道這是否正常運作？

若要確認您是否已成功重試佇列，請執行下列動作：

1.  使用佇列檢視器或 **Get-Queue** 指令程式來尋找您嘗試重試的佇列。

2.  確認佇列的 **LastRetryTime** 內容與您嘗試重試佇列的時間相符。

## 重新提交佇列中的郵件

重新提交佇列與重試佇列相似，只不過系統會將郵件送回提交佇列以便分類程式重新處理。您可以重新提交具有下列狀態的郵件：

  - 具有「重試」狀態的傳遞佇列。佇列中的郵件不得處於「擱置」狀態。

  - 「無法存取」佇列中不是處於「暫停」狀態的郵件。

  - 毒藥郵件佇列中的郵件。

## 使用命令介面重新提交郵件

若要重新提交郵件，請使用下列語法。

    Retry-Queue <-Identity QueueIdentity | -Filter {Status -eq "Retry"} -Server ServerIdentity> -Resubmit $true

此範例會重新提交名為 Mailbox01 之伺服器上任何處於「重試」狀態之傳遞佇列中的所有郵件。

    Retry-Queue -Filter {Status -eq "Retry"} -Server Mailbox01 -Resubmit $true

此範例會重新提交伺服器 Mailbox01 上無法存取之佇列中的所有郵件。

    Retry-Queue -Identity Mailbox01\Unreachable -Resubmit $true

## 重新提交毒藥郵件佇列中的郵件

您可以藉由繼續郵件來重新提交毒藥郵件佇列中的郵件。您可以使用佇列檢視器或命令介面來重新提交毒藥郵件佇列中的郵件。請注意，只有在毒藥郵件佇列中有郵件時，您才能在佇列檢視器中看到毒藥郵件佇列。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>毒藥郵件佇列包含在伺服器失敗之後，被判斷為對 Exchange 系統有害的郵件。郵件的內容或格式可能的確是有害。或者，郵件可能是因設計不良的代理程式在處理可能有害的郵件時，造成 Exchange 伺服器無法運作的犧牲品。如果您不確定毒藥郵件佇列中的郵件是否安全，則應將郵件匯出到檔案以進行檢驗。如需詳細資訊，請參閱 <a href="export-messages-from-queues-exchange-2013-help.md">從佇列匯出訊息</a>。</td>
</tr>
</tbody>
</table>


## 使用 Exchange 工具箱內的佇列檢視器來重新提交毒藥郵件佇列中的郵件

1.  按一下 \[開始\] \> \[所有程式\] \> \[Microsoft Exchange 2013\] \> \[Exchange 工具箱\]。

2.  在 \[郵件流程工具\] 區段下，按兩下 \[佇列檢視器\]，在新視窗中開啟工具。

3.  在佇列檢視器中，按一下 \[佇列\] 索引標籤。畫面會顯示所連線之伺服器上所有佇列的清單。

4.  按一下毒藥郵件佇列。在執行窗格中，選取 **\[檢視郵件\]**。

5.  從清單中選取一或多封郵件、按一下滑鼠右鍵，然後選取 **\[繼續\]**。

## 使用命令介面重新提交毒藥郵件佇列中的郵件

若要重新提交毒藥郵件佇列中的郵件，請執行以下步驟。

1.  執行以下命令來找出郵件的識別碼。
    
        Get-Message -Queue Poison | Format-Table Identity

2.  將在上個步驟找出來的郵件識別碼用於以下命令中。
    
        Resume-Message <PoisonMessageIdentity>
    
    此範例會繼續傳遞毒藥郵件佇列中郵件識別碼值為 222 的郵件。
    
        Resume-Message 222

## 如何知道這是否正常運作？

若要確認您是否已成功重新提交毒藥郵件佇列中的郵件，請執行下列動作：

1.  使用佇列檢視器或 **Get-Queue** 指令程式來檢視您嘗試重新提交郵件的毒藥郵件佇列。

2.  確認郵件不再位於毒藥郵件佇列中。請注意，空白的毒藥郵件佇列不會出現在佇列檢視器或 **Get-Queue**指令程式中。因此，如果您重新提交的郵件是毒藥郵件佇列中唯一的郵件且該毒藥郵件佇列已不再出現，表示您已成功重新提交郵件。

## 擱置佇列

擱置佇列會使郵件無法離開佇列，但並不會變更郵件在佇列中的狀態。透過 SMTP-send 傳遞的訊息會完成作業。您可以擱置佇列來停止郵件流程，然後擱置佇列中的其中一封或多封郵件。當佇列繼續進行時，已暫停的郵件將不會離開佇列。

您可以暫停狀態為 Active 或 Retry 的佇列。也可以暫停 Unreachable 佇列和 Submission 佇列。

如果暫停 Unreachable 佇列，則在佇列重新繼續運作之前，傳輸伺服器收到組態更新時都不會將項目重新提交到分類程式。如果暫停 Submission 佇列，則在佇列重新繼續運作之前，分類程式不會收取郵件。

## 使用 Exchange 工具箱內的佇列檢視器來擱置佇列

1.  按一下 \[開始\] \> \[所有程式\] \> \[Microsoft Exchange 2013\] \> \[Exchange 工具箱\]。

2.  在 \[郵件流程工具\] 區段下，按兩下 \[佇列檢視器\]，在新視窗中開啟工具。

3.  在佇列檢視器中，按一下 \[佇列\] 索引標籤。畫面會顯示所連線之伺服器上所有佇列的清單。您可以建立篩選器，只顯示符合特定準則的佇列。

4.  選取一個或多個佇列，並在其上按一下滑鼠右鍵，然後選取 **\[暫停\]**。

## 使用命令介面來擱置佇列

若要擱置佇列，請使用下列語法。

    Suspend-Queue <-Identity QueueIdentity | -Filter {QueueFilter} [-Server ServerIdentity]>

本範例會擱置本機伺服器上郵件計數等於或大於 1,000，而且狀態為「重試」的所有佇列。

    Suspend-Queue -Filter {MessageCount -ge 1000 -and Status -eq "Retry"}

此範例會擱置名為 Mailbox01 之伺服器上名為 contoso.com 的佇列。

    Suspend-Queue -Identity Mailbox01\contoso.com

## 如何知道這是否正常運作？

若要確認您是否已成功擱置佇列，請執行下列動作：

1.  使用佇列檢視器或 **Get-Queue** 指令程式來尋找您嘗試擱置的佇列。

2.  確認佇列的 **Status** 內容值是 `Suspended`。

