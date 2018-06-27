---
title: '將所有的信箱就地保留: Exchange Online Help'
TOCTitle: 將所有的信箱就地保留
ms:assetid: 4c141604-3210-44cc-b98e-f3e0f15613b8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn767952(v=EXCHG.150)
ms:contentKeyID: 62486282
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 將所有的信箱就地保留

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2017-01-18_

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>我們已延後 2017 年 7 月 1 日的期限以在 Exchange Online 中建立新的就地保留 (在 Office 365 和 Exchange Online 獨立計劃中)。但今年稍晚或明年初，您將無法在 Exchange Online 中建立新的就地保留。使用就地保留的替代方法是，您可以使用 <a href="https://go.microsoft.com/fwlink/?linkid=780738">eDiscovery 案例</a>或 Office 365 安全性和規範中心的<a href="https://go.microsoft.com/fwlink/?linkid=827811">保留原則</a>。在我們解除委任新就地保留後，您仍然可以修改現有的就地保留，而在 Exchange Server 2013 和 Exchange混合部署中建立新的就地保留仍會受到支援。而且，您依然能夠讓信箱處於「訴訟暫止」。</td>
</tr>
</tbody>
</table>


您的組織可能需要以保留指定期限內的所有信箱資料。您可以使用訴訟暫止狀態或就地保留功能來滿足此需求。將信箱置於訴訟暫止或就地保留功能之後，可修改或永久刪除的信箱項目會保留在 \[可復原的項目\] 資料夾。如需詳細資訊，請參閱[就地保留與訴訟暫止](in-place-hold-and-litigation-hold-exchange-2013-help.md)。

將組織中的所有信箱設為訴訟暫止或就地保留狀態之前，請考慮下列事項：

  - 當您將信箱就地保留時，使用者的封存信箱 （如果已啟用） 中的內容也被處於保留狀態。

  - 將所有信箱置於保留組織可能大幅影響信箱大小。Exchange Server 2013部署中規劃足夠的儲存以符合您的組織保留需求。在Exchange Online、 使用者的[信箱儲存限制](https://go.microsoft.com/fwlink/?linkid=403645)會取決於使用者訂閱授權。

  - 長持續期間保留信箱資料將會產生使用者的主要信箱和封存信箱中的可復原的項目\] 資料夾的成長。\[可復原的項目\] 資料夾有自己的儲存量限制，因此在資料夾中的項目不計算至接近信箱儲存限制。 在Exchange Server 2013和Exchange Online，\[可復原的項目\] 資料夾的預設儲存量限制為 30 GB。
    
      - 中Exchange Online，\[可復原的項目\] 資料夾的配額自動增加為 100 GB 時將信箱置於保留。
    
      - 在Exchange Server 2013，我們建議您定期監視以確定它不會到達此限制此資料夾的大小。如需詳細資訊，請參閱[可復原的項目資料夾](recoverable-items-folder-exchange-2013-help.md)。

## 選擇訴訟暫止或就地保留

以下是一些因素決定應該用於您組織中的所有信箱的保留功能保留時需要考量。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>您想要...</th>
<th>使用訴訟暫止</th>
<th>使用就地保留</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>使用 EAC</p></td>
<td><p>是</p>
<p>如需設定訴訟暫止狀態，EAC 最適合在幾個信箱的快速 one-off 動作。我們建議您組織中的所有使用者的設定 [訴訟暫止狀態使用命令介面。</p></td>
<td><p>是</p>
<p>不過，您無法在 EAC 中選取超過 500 個來源信箱。</p></td>
</tr>
<tr class="even">
<td><p>使用命令介面</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>暫停處理 10,000 個以上的信箱</p></td>
<td><p>是</p>
<p>訴訟資料暫留為信箱屬性。您可以將保留組織內的所有信箱使用<strong>Set-Mailbox</strong>指令程式。</p></td>
<td><p>[否]。使用多個就地保留</p>
<p>您可以使用通訊群組可在單一就地保留指定最大值為 10000 個信箱。若要將其他信箱就地保留，您必須建立其他就地保留。這會產生額外的管理負荷。使用訴訟暫止狀態將大量信箱上保留是比較簡單。</p></td>
</tr>
<tr class="even">
<td><p>將許多不同的信箱分配在不同期間暫停處理。</p></td>
<td><p>是</p>
<p>訴訟暫止是信箱屬性。您可以將每個信箱 (或幾組信箱) 暫停處理一段不同的保留時間。</p>
<p>請參閱範例使用篩選器中的收件者屬性讓您可以利用對信箱的子集的 「 訴訟暫止狀態的詳細資訊一節。</p></td>
<td><p>是</p>
<p>如果要個別保留數千個信箱，則建議使用訴訟暫止。如果要針對涉及多個使用者的特定事件建立保留，請對使用者群組使用單一就地保留。</p>
<p>不建議您建立每個信箱的個別為就地保留這會建立可讓管理更困難比訴訟保留許多就地保留的查詢。大量就地保留物件也可能會導致在 EAC 中重新整理、 建立或修改保留物件時的效能低落。</p></td>
</tr>
<tr class="odd">
<td><p>自動保留新的信箱</p></td>
<td><p>否</p>
<p>您必須將新信箱置於訴訟暫止狀態會在建立之後。您可以排定命令或指令碼以經常所需的身分來達到相同的效果。</p></td>
<td><p>否</p>
<p>您必須加入新的信箱就地保留，即使您建立就地保留時指定通訊群組。您也可以排程的命令或指令碼以經常所需的身分來達到相同的效果。我們建議指令碼] 核取如果現有的就地保留已達到 10000 信箱限制，並結束視需要建立 [新的就地保留功能。</p></td>
</tr>
<tr class="even">
<td><p>置於保留的所有公用資料夾</p></td>
<td><p>否</p>
<p>在Exchange Online、 不支援將公用資料夾信箱上的放置訴訟暫止狀態。 您必須使用就地保留功能。</p></td>
<td><p>是</p></td>
</tr>
</tbody>
</table>


## 將所有信箱設為訴訟暫止

您可以快速和輕鬆地將所有信箱保留無限期或在指定的期間使用命令介面。此命令會將所有信箱都置於保留 2555 天 （大約 7 年）。

    Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -eq "UserMailbox"} | Set-Mailbox -LitigationHoldEnabled $true -LitigationHoldDuration 2555

此範例使用[Get-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123685\(v=exchg.150\))指令程式和收件者篩選器來擷取組織中的所有使用者信箱，然後將 \[ [Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\))指令程式來啟用訴訟暫止狀態及保留持續時間指定信箱的清單。如需詳細資訊，請參閱[將信箱設為訴訟暫止](place-a-mailbox-on-litigation-hold-exchange-2013-help.md)。

## 將所有信箱設為就地保留

您可以使用 EAC 來選取最多 500 個信箱並保留它們。如需詳細資訊，請參閱[建立或移除就地保留](create-or-remove-an-in-place-hold-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要將 500 個以上的使用者設為就地保留，使用命令介面。請參閱<a href="https://technet.microsoft.com/zh-tw/library/dd298064(v=exchg.150)">New-MailboxSearch</a>。</td>
</tr>
</tbody>
</table>


## 其他資訊

  - 當您將所有信箱保留在組織中時，只存在於您執行命令的時間的信箱已處於保留狀態。如果您建立新的信箱之後，再次執行命令置於 \[保留。如果您經常建立新的信箱，您可以做為排程工作所需經常執行命令。

  - 防止刪除前指定期間內並儲存郵件的原始版本它會修改之前會保留上放置信箱保留資料。它會自動不會在指定的期間之後刪除訊息。合併訴訟暫止狀態或就地保留與保留原則，指定期間之後自動刪除的郵件，以符合組織的電子郵件保留需求。請參閱[保留標記和保留原則](retention-tags-and-retention-policies-exchange-2013-help.md)如需詳細資訊。

  - 本主題中用來將所有信箱的訴訟暫止狀態的 PowerShell 命令使用會傳回所有使用者信箱的收件者篩選器。您可以使用其他收件者的屬性來傳回您可以再透過管線傳到**Set-Mailbox**指令程式置於訴訟保留這些信箱的特定信箱的清單。
    
    以下是一些範例使用**Get-Mailbox**與**Get-Recipient** cmdlet 可傳回根據常見的使用者或信箱內容的信箱的子集。下列範例會假設相關信箱內容 （例如*CustomAttributeN*或*Department*） 已填入。
    
        Get-Mailbox -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'CustomAttribute15 -eq "OneYearLitigationHold"'
    
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'Department -eq "HR"'
    
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'PostalCode -eq "98052"'
    
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'StateOrProvince -eq "WA"'
    
        Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -ne "DiscoveryMailbox"}
    
    您可以使用篩選器中的其他使用者信箱屬性以包含或排除信箱。如需詳細資訊，請參閱[可篩選的內容-Filter 參數](https://technet.microsoft.com/zh-tw/library/bb738155\(v=exchg.150\))。

