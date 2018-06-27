---
title: '將 eDiscovery 搜尋結果複製到探索信箱: Exchange Online Help'
TOCTitle: 將 eDiscovery 搜尋結果複製到探索信箱
ms:assetid: bff2ce89-9e6f-494a-bd6a-2f2011507845
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn624163(v=EXCHG.150)
ms:contentKeyID: 61183400
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 將 eDiscovery 搜尋結果複製到探索信箱

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-02-24_

建立就地 eDiscovery 搜尋之後，您可以使用 EAC 將結果複製到探索信箱。您也可以使用命令介面來啟動已建立使用**New-MailboxSearch**指令程式會將結果複製到探索信箱時您建立搜尋所指定的 eDiscovery 搜尋。

## 開始之前有哪些須知？

  - 預估完成時間： 5 分鐘或更久，這取決於信箱的項目數傳回搜尋結果中

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「就地 eDiscovery」項目。

  - EDiscovery 搜尋具有要建立使用 EAC 或命令介面中，您可以複製搜尋結果之前。如需詳細資訊，請參閱[建立就地 eDiscovery 搜尋](create-an-in-place-ediscovery-search-exchange-2013-help.md)。

  - Exchange 2013安裝程式會建立稱為 「**探索搜尋信箱**複製搜尋結果的探索信箱。\[探索搜尋信箱也會建立預設Exchange Online。您可以建立其他探索信箱。如需詳細資訊，請參閱[建立探索信箱](create-a-discovery-mailbox-exchange-2013-help.md)。

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

## 使用 EAC 來複製搜尋結果

1.  在 EAC 中，移至 \[**相符性管理**\>**就地 eDiscovery 和保留**。

2.  在清單檢視中，選取 \[eDiscovery 搜尋。

3.  按一下 \[搜尋\]![搜尋圖示](images/Dn624163.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "搜尋圖示")，然後從下拉式清單按一下 \[複製搜尋結果\]。

4.  在 \[複製搜尋結果\] 中，從下列選項選取：
    
      - **包含無法搜尋的項目**  選取此核取方塊以包含無法搜尋 （例如Exchange搜尋無法建立索引的檔案類型附件的郵件） 的信箱項目。如需詳細資訊，請參閱[Exchange eDiscovery 中項目\] 無法搜尋](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md)。
    
      - **啟用重複資料刪除**   選取此核取方塊，可排除重複的郵件。只會複製每封郵件的單一執行個體至探索信箱。
    
      - **啟用完整記錄**   選取此核取方塊，可在搜尋結果中包含完整記錄。
    
      - **複製完成時傳送電子郵件給我**   選取此核取方塊，可在搜尋完成時收到電子郵件通知。
    
      - **將結果複製到探索信箱**   按一下 \[瀏覽\]，可選取您要複製結果的目的地探索信箱。
        
        ![複製搜尋結果](images/Dn624163.875e25ed-8308-408c-92c4-8c76fc9d9bfc(EXCHG.150).gif "複製搜尋結果")  

5.  按一下 \[複製\] 以開始程序來將搜尋結果複製到指定的探索信箱。

6.  按一下 \[重新整理\]![重新整理圖示](images/Dn624163.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "重新整理圖示") 以更新詳細資料窗格中顯示的複製狀態的資訊。

7.  複製完成時，按一下 \[開啟\] 以開啟要檢視搜尋結果的探索信箱。

## 使用命令介面來複製搜尋結果

使用之後**New-MailboxSearch**指令程式來建立就地 eDiscovery 搜尋，您必須啟動，將郵件複製到探索信箱*TargetMailbox*參數所指定的搜尋。如需建立使用命令介面中的 eDiscovery 搜尋，請參閱：

  - [使用命令介面來建立就地 eDiscovery 搜尋](create-an-in-place-ediscovery-search-exchange-2013-help.md)

  - [New-MailboxSearch](https://technet.microsoft.com/zh-tw/library/dd298064\(v=exchg.150\))

例如，您會執行下列命令以啟動 eDiscovery 搜尋名為*Fabrikam 調查*，將搜尋結果複製到指定的探索信箱。

    Start-MailboxSearch "Fabrikam Investigation"

如果您要取得的搜尋結果的估計*EstimateOnly*參數，您必須之前可以複製搜尋結果中移除交換器。您也必須指定將搜尋結果複製到探索信箱。例如，之後使用下列命令建立僅預估搜尋：

    New-MailboxSearch "FY13 Q2 Financial Results" -StartDate "04/01/2013" -EndDate "06/30/2013" -SourceMailboxes "DG-Finance" -SearchQuery '"Financial" AND "Fabrikam"' -EstimateOnly -IncludeUnsearchableItems

若要將此搜尋結果複製到探索信箱，您會執行下列命令：

    Set-MailboxSearch "FY13 Q2 Financial Results" -EstimateOnly $false -TargetMailbox "Discovery Search Mailbox"

    Start-MailboxSearch "FY13 Q2 Financial Results"

## 複製搜尋結果的詳細資訊

  - 將搜尋結果複製到探索信箱後，您可以將搜尋結果匯出至 PST 檔案。如需詳細資訊，請參閱[將 eDiscovery 搜尋結果匯出至 PST 檔](export-ediscovery-search-results-to-a-pst-file-exchange-2013-help.md)。

  - 如需無法搜尋之項目的詳細資訊，請參閱[Exchange eDiscovery 中項目\] 無法搜尋](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md)。

  - 如果您正在複製特定日期範圍內的所有信箱內容 （由未指定任何關鍵字搜尋準則中），然後該日期範圍內所有無法搜尋的項目將會自動包含在搜尋結果。因此，未選取 \[**包含無法搜尋的項目**\] 核取方塊時複製搜尋結果。否則無法搜尋的所有項目重複複本會複製到探索信箱。

  - 除了將搜尋結果複製到探索信箱，您也可以預估或預覽搜尋結果所選取的搜尋。
    
      - **預估搜尋結果**  此選項會傳回的估計項目總大小和根據您指定的準則搜尋將傳回的項目數。在 EAC 中的 \[詳細資料\] 窗格中顯示預估值。
    
      - **預覽搜尋結果**  此選項可讓您預覽，而不必將它複製到探索信箱來檢視不是搜尋傳回的搜尋結果。這可讓您快速決定是否有相關的搜尋結果。預覽結果之後，您可以修改搜尋查詢來縮小搜尋結果並重新執行搜尋。因此您不能移動、 編輯、 刪除或轉寄 \[預覽\] 頁面上的實際的搜尋結果中的唯讀版本會在 \[預覽\] 頁面上的項目。
    
    如需詳細資訊，請參閱[預估或預覽搜尋結果](create-an-in-place-ediscovery-search-exchange-2013-help.md)。

