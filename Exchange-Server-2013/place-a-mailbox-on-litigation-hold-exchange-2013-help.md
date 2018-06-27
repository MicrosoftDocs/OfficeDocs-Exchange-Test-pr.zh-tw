---
title: '將信箱設為訴訟暫止: Exchange Online Help'
TOCTitle: 將信箱設為訴訟暫止
ms:assetid: adee4621-3626-4aec-aa53-00b35ff0d0b0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn743673(v=EXCHG.150)
ms:contentKeyID: 62269039
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 將信箱設為訴訟暫止

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2016-10-18_

將信箱設為訴訟暫止狀態以保留所有信箱內容，包括已刪除的項目和已修改項目的原始版本。當您將使用者的信箱設為訴訟暫止，使用者封存信箱 (若已啟用) 中的內容也會處於暫止狀態。已刪除和修改過的項目會保留一段指定的期間，或直到信箱退出「訴訟暫止」狀態為止。[就地 eDiscovery](in-place-ediscovery-exchange-2013-help.md) 搜尋時會傳回這類信箱項目。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>訴訟暫止會保留使用者信箱內 [可復原的項目] 資料夾中的項目。根據刪除或修改的項目數量和大小，信箱 [可復原的項目] 資料夾的大小可能會快速增加。[可復原的項目] 資料夾預設以高配額設定。在 Exchange Online 中，當您將信箱設為訴訟暫止，就會自動增加此配額。在 Exchange Server 2013 中，我們建議您每週監控處於訴訟暫止的信箱，以確保它們不會達到 [可復原的項目] 的配額限制。</td>
</tr>
</tbody>
</table>


## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘

  - 訴訟暫止設定可能需要最多 60 分鐘才會生效。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 在 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「就地保留」項目。

  - 若要將 Exchange Online 信箱設為訴訟暫止，必須指派 Exchange Online (方案 2) 授權給信箱。如果信箱已獲派 Exchange Online (方案 1) 的授權，您必須指派另一個 Exchange Online 封存授權，才能將信箱設為保留。

  - 如同先前所解說，當您將使用者的信箱設為訴訟暫止，使用者封存信箱中的內容也會處於暫止狀態。如果您在 Exchange 混合式部署中對內部部署主要信箱進行訴訟暫止，雲端型封存信箱 (如果已啟用) 也會保留。

  - 在 Exchange Online 中，當您對信箱進行訴訟暫止，\[可復原的項目\] 資料夾的配額會自動增加到 100 GB。此資料夾的預設大小為 30 GB。

  - 訴訟暫止狀態會保留刪除的項目，也會保留已修改項目的原始版本，直到移除暫止狀態為止。您可以選擇指定保留期間，這會使信箱項目保留一段指定的時間週期。若您指定暫止持續時間，則將自接收訊息或建立信箱項目的日期開始計算。若要保留符合指定準則的項目，請使用就地保留來建立*查詢式*保留。如需詳細資訊，請參閱[建立或移除就地保留](create-or-remove-an-in-place-hold-exchange-2013-help.md)。

  - 若要使用命令介面將 Exchange Online 信箱設為保留狀態，您必須使用 Exchange Online PowerShell。 如需詳細資訊，請參閱＜[使用遠端 PowerShell 連線到 Exchange Online](https://technet.microsoft.com/zh-tw/library/jj984289\(v=exchg.150\))＞。

  - 不支援將公用資料夾信箱設為訴訟暫止。您必須使用就地保留來保留公用資料夾。

## 使用 EAC 將信箱設為訴訟暫止

1.  移至 \[收件者\] \> \[信箱\]。

2.  在使用者信箱清單中，按一下您要啟用訴訟暫止的信箱，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在信箱的屬性頁上，按一下 \[信箱功能\]。

4.  在 \[訴訟暫止：停用\] 下，按一下 \[啟用\] 可讓信箱處於訴訟暫止狀態。

5.  在 \[訴訟暫止\] 頁面上，輸入下列選擇性資訊：
    
      - **訴訟暫止持續時間 (天)**   使用此方塊指定當信箱處於訴訟暫止狀態時，信箱項目保留多久的時間。持續時間自接收或建立信箱項目的日期開始計算。如果您將此方塊保留空白，則會無限期保留項目，或將項目保留到移除保留為止。請使用天數為單位來指定持續時間。
    
      - **附註**   使用此方塊告知使用者他們的信箱處於訴訟暫止。如果使用者使用 Outlook 2010 或更新版本，附註將會出現在使用者的信箱中。
    
      - **URL**   使用此方塊將使用者導向至網站，使其進一步瞭解訴訟暫止。如果使用者使用 Outlook 2010 或更新版本，此 URL 會出現在使用者的信箱中。

6.  在 \[訴訟暫止\] 頁面上，按一下 \[儲存\]，然後在信箱屬性頁面上按一下 \[儲存\]。

回到頁首

## 使用命令介面將信箱設為無限期訴訟暫止

本範例會將信箱 bsuneja@contoso.com 設為訴訟暫止。系統會無限期保留信箱中的項目，或將項目保留到移除保留為止。

    Set-Mailbox bsuneja@contoso.com -LitigationHoldEnabled $true

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您將信箱設為無限期訴訟暫止狀態 (藉由不指定時間週期)，<em>LitigationHoldDuration</em> 屬性信箱的值會設為 <code>Unlimited</code>。</td>
</tr>
</tbody>
</table>


## 使用命令介面將信箱設為訴訟暫止，並在指定的期間保留項目

本範例會將信箱 bsuneja@contoso.com 設為訴訟暫止，並保留項目 2555 天 (約 7 年)。

    Set-Mailbox bsuneja@contoso.com -LitigationHoldEnabled $true -LitigationHoldDuration 2555

## 使用命令介面將所有信箱針對指定的期間設為訴訟暫止

您的組織可能需要將所有信箱資料保留一段特定時間。將組織中的所有信箱設為訴訟暫止狀態之前，請考慮下列事項：

本範例會將組織中的所有使用者信箱設為一年 (365 天) 的訴訟暫止。

    Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -eq "UserMailbox"} | Set-Mailbox -LitigationHoldEnabled $true -LitigationHoldDuration 365

範例使用 [Get-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123685\(v=exchg.150\)) Cmdlet 來擷取組織中的所有信箱，指定收件者篩選器來包含所有使用者信箱，然後將信箱清單傳給 [Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\)) Cmdlet 以啟用訴訟暫止及保留期間。

若要將所有使用者信箱設為無限期保留，執行上一個命令，但不要包含 *LitigationHoldDuration* 參數。

請參閱詳細資訊一節，以查看使用篩選器中的其他收件者屬性來包含或排除一或多個信箱的範例。

## 使用命令介面從訴訟暫止中移除信箱

本範例會從訴訟暫止移除信箱 bsuneja@contoso.com。

    Set-Mailbox bsuneja@contoso.com -LitigationHoldEnabled $false

回到頁首

## 如何知道這是否正常運作？

若要確認是否已成功將信箱設為訴訟暫止，請進行下列其中一項：

  - 在 EAC 中：
    
    1.  移至 \[收件者\] \> \[信箱\]。
    
    2.  在使用者信箱清單中，按一下您想確認訴訟暫止設定的信箱，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。
    
    3.  在信箱的屬性頁上，按一下 \[信箱功能\]。
    
    4.  在 \[訴訟暫止\] 下，請確認已啟用。
    
    5.  按一下 \[檢視詳細資料\] 來確認信箱設定為訴訟暫止的時間和設定的對象。您也可以確認或變更 \[訴訟暫止持續時間 (天)\]、\[附註\] 和 \[URL\] 等選擇性方塊中的值。

  - 在命令介面中，執行下列任一命令：
    
        Get-Mailbox <name of mailbox> | FL LitigationHold*
    
    或
    
        Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -eq "UserMailbox"} | FL Name,LitigationHold*
    
    若信箱設為無限期訴訟暫止狀態，*LitigationHoldDuration* 屬性信箱的值會設為 `Unlimited`。

## 詳細資訊

  - 如果貴組織要求所有信箱資料必須保留一段特定時間，在您將組織中的所有信箱設為訴訟暫止之前，請考慮下列事項。
    
      - 當您使用上一個命令來保留組織的所有信箱 (或符合指定收件者篩選器的部分信箱)，只有在您執行命令時存在的信箱會被保留。如果您後來建立新的信箱，您必須再次執行此命令來保留新信箱。如果您經常建立新的信箱，您可以將命令當做排程工作，依需要而經常執行。
    
      - 將所有信箱設為訴訟暫止可能對信箱大小造成重大影響。在 Exchange Server 2013 組織中，請規劃足夠的儲存空間，以符合組織的保留需求。
    
      - \[可復原的項目\] 資料夾本身有其儲存限制，所以資料夾中的項目不計入信箱儲存限制中。如同先前所解說，長時間保留信箱資料會導致使用者信箱和封存中 \[可復原的項目\] 資料夾的大小增加。若要容納 Exchange Online 中增加的大小，當您對信箱進行訴訟暫止，\[可復原的項目\] 資料夾的配額會自動從 30 GB 增加到 100 GB。
        
        在 Exchange Server 2013 中，\[可復原的項目\] 資料夾預設的儲存空間限制也是 30 GB。建議您定期監視此資料夾大小，以確保未達到限制。如需詳細資訊，請參閱＜[可復原的項目資料夾](recoverable-items-folder-exchange-2013-help.md)＞。

  - 要保留所有信箱的前一個命令，是使用會傳回所有使用者信箱的收件者篩選器。您可以使用其他收件者屬性以傳回一份特定信箱的清單，您便可以將這些信箱傳輸至 **Set-Mailbox** Cmdlet 以設為訴訟暫止。
    
    以下一些範例說明使用 **Get-Mailbox** 和 **Get-Recipient** Cmdlet，以根據一般使用者或信箱屬性來傳回信箱子集。這些範例假設相關的信箱屬性 (例如 *CustomAttributeN* 或 *Department*) 皆已填入。
    
        Get-Mailbox -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'CustomAttribute15 -eq "OneYearLitigationHold"'
    
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'Department -eq "HR"'
    
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'PostalCode -eq "98052"'
    
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'StateOrProvince -eq "WA"'
    
        Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -ne "DiscoveryMailbox"}
    
    您可以在篩選器中使用其他使用者信箱屬性來包含或排除信箱。如需詳細資訊，請參閱[可篩選的內容-Filter 參數](https://technet.microsoft.com/zh-tw/library/bb738155\(v=exchg.150\))。

回到頁首

