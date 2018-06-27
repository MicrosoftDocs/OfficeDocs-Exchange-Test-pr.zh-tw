---
title: '降低探索 Exchange 中信箱的大小: Exchange Online Help'
TOCTitle: 降低探索 Exchange 中信箱的大小
ms:assetid: fa762d14-f942-4728-8813-887d11441a68
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn750895(v=EXCHG.150)
ms:contentKeyID: 62371314
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 降低探索 Exchange 中信箱的大小

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2015-04-07_

有超過 50 GB 限制的探索信箱嗎？若要修正此問題，您可以建立新的探索信箱，然後將搜尋結果從較大的探索信箱複製到新的探索信箱。

## 我為何想要這樣做？

在Exchange Server 2013和Exchange Online，用來儲存在就地 eDiscovery 搜尋結果的探索信箱的大小上限為 50 GB。在目前的大小限制之前, 您將能夠增加為超過 50 GB，可提升擁有探索信箱更加大於 50 GB 的存放區配額。有超過 50 GB 的探索信箱的三個問題：

  - 不受支援。

  - 無法移轉至 Office 365。

  - 如果是Exchange Server 2010中的探索信箱，他們無法升級到Exchange Server 2013。

## 程序概覽

以下簡略說明將超過 50 GB 限制的探索信箱縮小所需執行的動作：

1.  Create其他探索信箱來分散搜尋結果。

2.  將搜尋結果從現有的探索信箱Copy到一或多個新的探索信箱。

3.  從原始探索信箱Delete eDiscovery 搜尋來降低大小。

這裡提出的策略是根據日期範圍，將原始探索信箱的搜尋結果分組成個別的 eDiscovery 搜尋。有一個方法可快速將許多搜尋結果複製到新的探索信箱。下圖說明此方法。

![降低探索信箱的大小](images/Dn750895.4400df18-c7ed-4c62-b304-f9060ffbdba5(EXCHG.150).gif "降低探索信箱的大小")

## 開始之前有哪些須知？

  - 完成此工作的預估時間：時間隨著要複製到不同探索信箱的搜尋結果數量和大小而有所不同。

  - 執行下列命令以判斷您的組織中的探索信箱大小。
    
        Get-Mailbox -RecipientTypeDetails DiscoveryMailbox | Get-MailboxStatistics | FL DisplayName,TotalItemSize

  - 在超過 50 GB 限制的探索信箱中，決定是否需要保留部分或全部的搜尋結果。請依照本主題的步驟，將搜尋結果複製到不同的探索信箱，以保留搜尋結果。如果您不需要保留特定 eDiscovery 搜尋的結果，您可以依步驟 3 的說明來刪除搜尋。刪除搜尋會從探索信箱中刪除搜尋結果。

  - 在超過 50 GB 限制的探索信箱中，如果您不需要其中任何搜尋結果，您可以刪除此信箱。如果這是佈建 Exchange 組織時所建立的預設探索信箱，您可以重新建立它。如需詳細資訊，請參閱 [刪除並重新建立 Exchange 中預設的探索信箱](delete-and-re-create-the-default-discovery-mailbox-in-exchange-exchange-2013-help.md)。

  - 對於目前的法律案件，您可能想要將選取的 eDiscovery 搜尋的結果匯出至 .pst 檔案。這樣做可讓特定搜尋的結果保持不變。除了匯出包含搜尋結果的 .pst 檔案，也會匯出搜尋結果記錄檔 (.csv 檔案格式)，其中，搜尋結果中傳回的每個郵件都有一個項目。此檔案中的每個項目可識別郵件所在的來源信箱。如需詳細資訊，請參閱 [將 eDiscovery 搜尋結果匯出至 PST 檔](export-ediscovery-search-results-to-a-pst-file-exchange-2013-help.md)。
    
    將搜尋結果匯出至 .pst 檔案之後，如果想要將搜尋結果匯入到新的探索信箱，則需要使用 Outlook。

## 步驟 1：建立探索信箱

第一步是建立其他探索信箱，讓您能夠從超過大小限制的探索信箱中複製搜尋結果。根據探索信箱的 50 GB 大小限制，決定需要另外再建立多少個探索信箱。接著，您需要指派必要的權限給使用者或群組來開啟這些新的探索信箱。

1.  執行下列命令以建立新的搜索信箱。
    
        New-Mailbox -Name <discovery mailbox name> -Discovery

2.  執行下列命令，將開啟探索信箱和檢視搜尋結果的權限指派給使用者或群組。
    
        Add-MailboxPermission <discovery mailbox name> -User <name of user or group> -AccessRights FullAccess -InheritanceType all

## 步驟 2：將搜尋結果複製到探索信箱

下一步是使用 **New-MailboxSearch** 指令程式，從現有探索信箱中將搜尋結果複製到上一步所建立的新探索信箱。此程序使用 *StartDate* 和 *EndDate* 參數，將搜尋結果的範圍設為不超過 50 GB 的批次。這可能需要一些測試 (藉由評估搜尋結果)，才能適當地決定搜尋結果的大小。

1.  執行下列命令以建立新的 eDiscovery 搜索。
    
        New-MailboxSearch -Name "Search results from 2010" -SourceMailboxes "Discovery Search Mailbox" -StartDate "01/01/2010" -EndDate "12/31/2010" -TargetMailbox "Discovery Mailbox Backup 01" -EstimateOnly -StatusMailRecipients admin@contoso.com
    
    此範例使用下列參數：
    
      - *Name*   此參數指定新的 eDiscovery 搜尋名稱。因為是依傳送和接收日期來設定範圍，所以搜尋的名稱最好包含日期範圍。
    
      - *SourceMailboxes*   此參數指定預設探索信箱。您也可以指定另一個超過大小限制之探索信箱的名稱。
    
      - *StartDate* 和 *EndDate*   這些參數指定預設探索信箱中的搜尋結果日期範圍，以併入搜尋結果中。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>請使用簡短日期格式 (mm/dd/yyyy) 來指定日期，即使本機電腦的 [地區選項] 設定是設為不同的格式也一樣，例如 dd/mm/yyyy。例如，使用 <strong>03/01/2014</strong> 來指定 2014 年 3 月 1 日。</td>
        </tr>
        </tbody>
        </table>
    
      - *TargetMailbox*   此參數指定應該將搜尋結果複製到名為 "Discovery Mailbox Backup 01" 的探索信箱。
    
      - *EstimateOnly*   此參數指定開始搜尋時只預估將傳回的項目數。如果未包含此參數，則開始搜尋時會將郵件複製到目標信箱。使用此參數可讓您在必要時調整日期範圍，以增加或減少搜尋結果數目。
    
      - *StatusMailRecipients*   此參數指定應該將狀態訊息傳送給指定的收件者。

2.  建立搜尋之後，使用命令介面或 Exchange 管理中心 (EAC) 來啟動搜尋。
    
      - **使用命令介面：**執行下列命令來啟動上一步所建立的搜尋。因為建立搜尋時已包含 *EstimateOnly* 參數，所以不會將搜尋結果複製到目標探索信箱。
        
            Start-MailboxSearch "Search results from 2010"
    
      - **使用 EAC：**移至 **\[規範管理\]** \> **\[就地 eDiscovery & 保留\]**。選取上一步所建立的搜尋，按一下 \[**搜尋**![搜尋圖示](images/Dn624163.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "搜尋圖示")\]，然後按 **\[估計搜尋結果\]**。

3.  如有必要，調整日期範圍來增加或減少傳回的搜尋結果數量。如果您變更日期範圍，請再次執行搜尋來取得新的結果估計值。請考慮變更搜尋的名稱來反映新的日期範圍。

4.  測試搜尋完成時，請使用命令介面或 EAC，將搜尋結果複製到目標探索信箱。
    
      - **使用命令介面：**執行下列命令來複製搜尋結果。您必須先移除 *EstimateOnly* 參數，才能複製搜尋結果。
        
            Set-MailboxSearch "Search results from 2010" -EstimateOnly $false
        
            Start-MailboxSearch "Search results from 2010"
    
      - **使用 EAC：**移至 **\[規範管理\]** \> **\[就地 eDiscovery & 保留\]**。選取搜尋，按一下 \[**搜尋**![搜尋圖示](images/Dn624163.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "搜尋圖示")\]，然後按 **\[複製搜尋結果\]**。
    
    如需詳細資訊，請參閱 [將 eDiscovery 搜尋結果複製到探索信箱](copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md)。

5.  重複步驟 1 到 4，為其他日期範圍建立新的搜尋。在新搜尋的名稱中包含日期範圍，以表示結果的範圍。為了確保探索信箱都不超過 50 GB 限制，請使用不同的探索信箱作為目標信箱。

## 步驟 3：刪除 eDiscovery 搜尋

將搜尋結果從原始探索信箱複製到另一個探索信箱之後，您就可以刪除原始的 eDiscovery 搜尋。刪除 eDiscovery 搜尋會從儲存搜尋結果的探索信箱中刪除搜尋結果。

在刪除搜尋之前，您可以針對組織中的所有搜尋，執行下列命令來識別已複製到探索信箱的搜尋結果大小。

    Get-MailboxSearch | FL Name,TargetMailbox,ResultSizeCopied

您可以使用命令介面或 EAC 來刪除 eDiscovery 搜尋。

  - **使用命令介面：**執行下列命令。
    
        Remove-MailboxSearch -Identity <name of search>

  - **使用 EAC：**移至 **\[規範管理\]** \> **\[就地 eDiscovery & 保留\]**。選取您要刪除的搜尋，然後按一下 \[**刪除**![刪除圖示](images/JJ651670.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "刪除圖示")\]。

## 如何知道這是否正常運作？

在經由刪除 eDiscovery 搜尋而從儲存結果的探索信箱中移除結果之後，請執行下列命令來顯示所選取的探索信箱的大小。

    Get-Mailbox <name of discovery mailbox> | Get-MailboxStatistics | FL TotalItemSize

