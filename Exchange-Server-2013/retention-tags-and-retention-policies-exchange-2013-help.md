---
title: '保留標記和保留原則: Exchange Online Help'
TOCTitle: 保留標記和保留原則
ms:assetid: 48c13be5-3f01-4849-a089-766210e54f89
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd297955(v=EXCHG.150)
ms:contentKeyID: 50473176
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 保留標記和保留原則

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

在 Microsoft Exchange Server 2013 和 Exchange Online 中，通訊記錄管理 (MRM) 可協助組織管理電子郵件生命週期並降低與電子郵件及其他通訊相關的法律風險。MRM 可讓您更容易地保留遵循公司原則、政府法令或法律規定所需的郵件，並移除不法或不具商業價值的內容。

觀賞如何將保留標記和保留原則套用至Exchange Online中信箱的快速概觀此[視訊](http://go.microsoft.com/fwlink/?linkid=825854) 。

逐步的程序來管理 MRM 在尋找吗？請參閱[通訊記錄管理程序](messaging-records-management-procedures-exchange-2013-help.md)。

**目錄**

通訊記錄管理策略

Retention tags

Retention policies

Managed Folder Assistant

Retention hold

## 通訊記錄管理策略

Exchange 2013 和 Exchange Online 中的 MRM 是使用「保留標記」和「保留原則」所完成。討論每一項保留功能的詳細資料之前，務必了解如何在整體 MRM 策略中使用這些功能。這項策略根據：

  - 指派*保留原則標記* (RPT) 給預設資料夾 (例如 \[收件匣\]與 \[刪除的郵件\])。

  - 將*預設原則標記* (DPT) 套用到信箱，以管理所有無標記項目的保留。

  - 允許使用者指派*個人標記*到自訂資料夾和個別項目。

  - 將 MRM 功能從使用者的收件匣管理和歸檔習慣區隔開來。使用者不需要根據保留需求在受管理的資料夾歸檔郵件。個別郵件的保留標記可以與套用到所在資料夾的標記不相同。

下圖說明執行這項策略的相關工作。

![使用信箱保留的保留原則](images/Dd297955.429b51d5-51b8-4816-b8a4-221e0915d0c0(EXCHG.150).gif "使用信箱保留的保留原則")

回到頁首

## 保留標記

如上圖所示，保留標記可用來套用保留設定到資料夾和個別項目，例如電子郵件訊息和語音信箱。這些設定可指定郵件保留在信箱中的時間長度，以及當郵件達到指定的保留時間時應採取的動作。當郵件達到保留時間時，會移到個人封存或刪除。

![保留標記中的設定](images/Dd297955.936edd6a-8bc4-4c03-94a3-c240ffe7dd6a(EXCHG.150).png "保留標記中的設定")

保留標記可讓使用者在其專屬信箱資料夾和個別項目保留標記。使用者無法再對中佈建根據郵件保留需求系統管理員的受管理資料夾的檔案項目。

## 保留標記的類型

保留標記被分為下列根據誰可以套用與信箱的可套用的其中三種類型。


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>保留標記的類型</th>
<th>Applied...</th>
<th>套用的...</th>
<th>可用的動作...]</th>
<th>詳細資料</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>預設原則標記 (DPT)</p></td>
<td><p>自動到整個信箱</p>
<p>DPT 適用於<em>無標記</em>項目、 沒有套用直接或透過從資料夾繼承其保留標記的信箱項目。</p></td>
<td><p>系統管理員</p></td>
<td><ul>
<li><p>移至封存</p></li>
<li><p>刪除並允許復原</p></li>
<li><p>永久刪除</p></li>
</ul></td>
<td><p>使用者無法變更套用至信箱的 dpt 套用。</p></td>
</tr>
<tr class="even">
<td><p>保留原則標記 （印）</p></td>
<td><p>自動至預設資料夾</p>
<p>預設資料夾是例如自動建立的所有信箱資料夾：<strong>收件匣</strong>、<strong>刪除項目</strong>，並<strong>傳送的項目</strong>。請參閱<a href="default-folders-that-support-retention-policy-tags-exchange-2013-help.md">支援保留原則標記的預設資料夾</a>中支援的預設資料夾的清單。</p></td>
<td><p>系統管理員</p></td>
<td><ul>
<li><p>刪除並允許復原</p></li>
<li><p>永久刪除</p></li>
</ul></td>
<td><p>使用者無法變更套用至預設資料夾印。</p></td>
</tr>
<tr class="odd">
<td><p>個人標記</p></td>
<td><p>手動以項目與資料夾</p>
<p>使用者可以自動化標記使用收件匣規則也將郵件移至具有特定的標記的資料夾或套用個人標記到的郵件。</p></td>
<td><p>使用者</p></td>
<td><ul>
<li><p>移至封存</p></li>
<li><p>刪除並允許復原</p></li>
<li><p>永久刪除</p></li>
</ul></td>
<td><p>個人標記允許使用者決定應為多久項目保留。例如信箱可以有七個年度中刪除的項目 DPT，但使用者可以藉由套用個人標記三天內刪除這些建立新聞稿及自動的通知等項目發生例外狀況。</p></td>
</tr>
</tbody>
</table>


## 更多有關個人標記

個人標記可用來Outlook 2010與Outlook Web App使用者為其保留原則的一部分。Outlook 2010與Outlook Web App、 個人標記**移至封存**巨集指令以顯示為**封存原則**\] 後**刪除並允許復原**或**永久刪除**動作個人標記會顯示為**保留原則**，如下圖所示。

![Outlook 2010 和 Outlook Web App 中的個人標記](images/Dd297955.2dbaee13-fdd0-4c30-b821-e662ce2587bb(EXCHG.150).gif "Outlook 2010 和 Outlook Web App 中的個人標記")

使用者可以套用個人標記為他們所建立的資料夾或個別項目的。已套用個人標記的郵件一律會根據 \[個人標記的設定來處理。使用者可套用個人標記一則訊息使它已移動或刪除提早或延遲超過 DPT 或 Rpt 中所指定的設定套用至該使用者信箱。您也可以建立個人標記與保留已停用。這可讓使用者標記的項目讓他們正在永不會移至封存或永遠不過期。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用者可以將原則套用至預設資料夾、使用者建立的資料夾或子資料夾，以及個別項目中。使用者可以將保留原則套用至使用者建立的資料夾或子資料夾，以及個別項目 (包括預設資料夾中的子資料夾與項目) 中，但不能套用至預設資料夾。</td>
</tr>
</tbody>
</table>


使用者也可以使用 Exchange 系統管理中心 (EAC) 選取未連結至其保留原則的其他個人標記。選取的標記就可在 Outlook 2010 與 Outlook Web App 中使用。為讓使用者可以從 EAC 選取其他標記，您必須將 [MyRetentionPolicies 角色](myretentionpolicies-role-exchange-2013-help.md) 新增至使用者的角色指派原則中。若要深入了解使用者的角色指派原則，請參閱[了解管理角色指派原則](understanding-management-role-assignment-policies-exchange-2013-help.md)。若您允許使用者選取其他個人標記，就必須讓他們能夠使用 Exchange 組織中的所有個人標記。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>個人標記是高階功能。具備包含這些標記之原則的信箱 (或因使用者將標記新增至他們的信箱) 需要 Exchange 企業用戶端存取使用權 (CAL)。</td>
</tr>
</tbody>
</table>


回到頁首

## 保留時間

當您啟用保留標記時，必須指定標記的保留時間。此時間指出郵件送達使用者信箱後的保留天數。

非週期性項目 (例如電子郵件訊息) 的保留天數計算方式，與具有結束日期之項目或週期性項目 (例如會議和工作) 的計算方式不同。若要了解如何針對不同類型項目計算保留天數，請參閱[保留期間的計算方式](how-retention-age-is-calculated-exchange-2013-help.md)。

您也可以建立保留標記與保留已停用或之後他們正在建立停用標記。未處理已套用已停用的標記的郵件，因為保留會不採取任何動作。因此，使用者可以使用已停用的個人標記為**永遠不會移動**標籤或**永不刪除**標記覆寫 DPT 或印否則會套用至郵件。

## 保留動作

當建立或設定其保留標記，您可以選取下列保留動作，其中項目達到其保留期間時要採取：


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>保留動作</th>
<th>採取的動作...</th>
<th>除非...]</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>將移至封存</strong> 1</p></td>
<td><ul>
<li><p>會將郵件移至使用者的封存信箱</p></li>
<li><p>只適用於 dpt 套用和個人標記</p></li>
</ul>
<p>如需有關封存的詳細資訊，請參閱：</p>
<ul>
<li><p><a href="in-place-archiving-in-exchange-2013-exchange-2013-help.md">就地封存 in Exchange 2013</a></p></li>
<li><p><a href="https://technet.microsoft.com/zh-tw/library/dn922147(v=exchg.150)">Exchange Online 中的封存信箱</a></p></li>
</ul></td>
<td><ul>
<li><p>如果使用者沒有封存信箱，會不採取任何動作。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>刪除並允許復原</strong></p></td>
<td><ul>
<li><p>當使用者會清空 [刪除的郵件] 資料夾像行為。</p></li>
<li><p>項目的會移至<a href="recoverable-items-folder-exchange-2013-help.md">可復原的項目資料夾</a>信箱中，且保留之前<em>刪除的郵件項目的保留</em>期間。</p></li>
<li><p>提供給第二個機會復原使用 [<strong>復原刪除的項目</strong>] 對話方塊中的項目] 方塊內選取Outlook或Outlook Web App使用者</p></li>
</ul></td>
<td><ul>
<li><p>如果您已將已刪除項目的保留期間設為零天，永久刪除項目的。如需詳細資訊，請參閱<a href="https://technet.microsoft.com/zh-tw/library/dn163584(v=exchg.150)">Exchange Online 信箱之保留時間變更多久永久刪除項目</a>。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>永久刪除</strong></p></td>
<td><ul>
<li><p>永久刪除郵件。</p></li>
<li><p>您無法復原訊息之後永久刪除。</p></li>
</ul></td>
<td><ul>
<li><p>如果信箱處於<a href="in-place-hold-and-litigation-hold-exchange-2013-help.md">就地保留與訴訟暫止</a>或訴訟暫止狀態、 項目會保留在根據保留參數的可復原的項目] 資料夾。<a href="in-place-ediscovery-exchange-2013-help.md">就地 eDiscovery</a>仍會在搜尋結果中傳回這些項目。</p>
<p></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>標示為超過保留限制</strong></p></td>
<td><ul>
<li><p>會將郵件標示為過期。在 Outlook 2010 或更新版本和Outlook Web App，到期的項目顯示通知註指出 '此項目已過期' 與 '此項目將會在 0 天內到期'。Outlook 2007 中標示為過期的項會顯示使用刪除線文字。</p></li>
</ul></td>
<td><p>不適用</p></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>1 Exchange混合部署，可以啟用內部部署主要信箱的雲端式封存信箱。如果您將封存原則指派給內部部署信箱，項目所移至雲端式封存。如果目移到封存信箱，一份不會保留在內部部署信箱。如果內部部署信箱處於保留狀態，封存原則仍會他們會保留期間保留所指定的雲端式封存信箱移動項目。</td>
</tr>
</tbody>
</table>


如需如何建立保留標記的詳細資訊，請參閱[建立保留原則](create-a-retention-policy-exchange-2013-help.md)。

回到頁首

## 保留原則

若要將一個以上的保留標記套用到信箱，您必須將標記新增到保留原則，然後將原則套用到信箱。信箱不能有一個以上的保留原則。保留標記可隨時連結至保留原則，或中斷與保留原則的連結，而且變更會自動在所有已套用原則的信箱上生效。

保留原則可以有下列保留標記：


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>保留標記類型</th>
<th>原則中標記</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>預設原則標記 (DPT)</p></td>
<td><ul>
<li><p>搭配 <strong>[移至封存]</strong> 動作的一個 DPT</p></li>
<li><p>一個 DPT，搭配 [刪除並允許復原] 或 [永久刪除] 動作</p></li>
<li><p>一個 DPT 與<strong>刪除並允許復原</strong>或<strong>永久刪除</strong>動作的語音信箱郵件</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>保留原則標記 (RPTs)</p></td>
<td><ul>
<li><p>一個 RPT，適用於每個支援的預設資料夾</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您無法將特殊預設資料夾 (例如 [刪除的郵件]) 的多個 RPT 連結至相同保留原則。</td>
</tr>
</tbody>
</table>

</li>
</ul></td>
</tr>
<tr class="odd">
<td><p>個人標記</p></td>
<td><ul>
<li><p>任意數目的個人標記</p></li>
</ul>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>許多原則中的個人標記可以將混淆使用者。建議您將不超過 10 個個人標記新增至保留原則。</td>
</tr>
</tbody>
</table>

</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>雖然保留原則並不一定要連結保留標記，但不建議使用這個案例。如果信箱的保留原則未連結任何保留標記，可能會造成信箱項目永遠不會過期。</td>
</tr>
</tbody>
</table>


保留原則可同時包含封存標記 (將項目移至個人封存信箱的標記) 和刪除標記 (刪除項目的標記)。信箱項目也可套用這兩種類型的標記。封存信箱沒有不同的保留原則。相同的保留原則會套用至主要和封存信箱。

當您計劃建立保留原則時，必須考慮它們是否將同時包含封存和刪除標記。如先前所述，保留原則可以有一個使用 **\[移至封存\]** 動作的 DPT，以及一個使用 **\[刪除並允許復原\]** 或 **\[永久刪除\]** 動作的 DPT。使用 **\[移至封存\]** 動作之 DPT 的保留時間，必須少於使用刪除動作之 DPT 的保留時間。例如，您可以使用搭配 **\[移至封存\]** 動作的 DPT，在兩年後將項目移至封存信箱，並使用搭配刪除動作的 DPT，在七年後將項目從信箱中移除。在主要與封存信箱中的項目將在七年後刪除。

如需與保留原則相關的管理工作清單，請參閱[通訊記錄管理程序](messaging-records-management-procedures-exchange-2013-help.md)。

## 預設保留原則

Exchange安裝程式會建立保留原則**預設 MRM 原則**。預設 MRM 原則會自動套用至新的信箱中Exchange Online。中Exchange Server、 原則會自動套用如果建立新的使用者的封存而且沒有指定保留原則

您可以修改包含在預設 MRM 原則中，例如變更保留期間或保留動作的標記、 停用標記或修改原則來新增或移除標記。更新的原則會套用至信箱下一次由受管理的資料夾助理員處理。

如需詳細資訊，包括清單中的保留標記連結到該原則，請參閱[在 Exchange Online 與 Exchange Server 的預設保留原則](default-retention-policy-in-exchange-online-and-exchange-server-exchange-2013-help.md)。

回到頁首

## 受管理的資料夾助理員

受管理的資料夾助理員 (在信箱伺服器上執行的信箱助理員) 會處理已套用保留原則的信箱。

受管理的資料夾助理員會檢查信箱中的項目，並決定這些項目是否應受限於保留原則，以進一步套用保留原則。然後它會以適當的保留標記在受限於保留原則的項目上加上戳記，並針對超過保留時間的項目執行指定的保留動作。

受管理的資料夾助理員是以節流為基礎的助理員。以節流為基礎的助理員會永遠執行，不需要設定排程。它們可耗用的系統資源會受到節流。您可以設定受管理的資料夾助理員，使其在特定期間內 (稱為*工作週期*) 處理信箱伺服器上的所有信箱。此外，助理員會以指定的間隔 (稱為*工作週期檢查點*) 重新整理要處理的信箱清單。在重新整理期間，助理員會將新建立或移動的信箱新增至佇列。它也會針對因為失敗而未處理成功的現有信箱，重新設定其優先順序，並將它們移至佇列的較高順序，以便在同一個工作週期中處理它們。

您也可以使用 [Start-ManagedFolderAssistant](https://technet.microsoft.com/zh-tw/library/aa998864\(v=exchg.150\)) Cmdlet 手動觸發助理員，以處理指定的信箱。若要深入了解，請參閱[設定受管理的資料夾助理員](configure-the-managed-folder-assistant-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>受管理的資料夾助理員不會對不需保留的郵件採取任何動作，這是透過停用保留標記來指定。您也可以停用保留標記，以暫停處理具有該標記的項目。</td>
</tr>
</tbody>
</table>


## 在資料夾之間移動項目

從一個資料夾移至另一個資料夾的信箱項目，會繼承目的資料夾所套用的任何標記。如果將項目移至未指派標記的資料夾，則會套用 DPT。如果項目已有明確指派的標記，則該標記的優先順序會永遠高於任何資料夾層級的標記或預設標記。

## 將保留標記套用至封存中的資料夾

當使用者將個人標記套用至封存中的資料夾時，如果主要信箱中存在同名的資料夾且有不同的標記，則封存中該資料夾的標記會變更為符合主要信箱中的標記。這是經過設計的功能，當封存中的資料夾與使用者主要信箱中的相同資料夾有不同的到期行為時，可避免其中的項目產生任何混淆。例如，使用者在主要信箱中有一個名為 Project Contoso 的資料夾具有*「刪除 - 3 年」*標記，且封存信箱中也有一個 Project Contoso 資料夾。假設使用者套用*「刪除 - 1 年」*個人標記，以在 1 年後刪除資料夾中的項目。當再次處理信箱時，資料夾就會恢復為「刪除 - 3 年」標記。

## 移除或刪除保留原則中的保留標記

當保留標記從套用至信箱的保留原則中移除時，使用者將無法再使用該標記，且無法將其套用至信箱中的項目。

受管理的資料夾助理員會根據這些設定，繼續處理已由該標記所戳記的現有項目，而在標記中指定的任何保留動作也會套用到這些郵件。

不過，如果您刪除標記，則會移除儲存在 Active Directory 中的標記定義。這會導致受管理的資料夾助理員處理信箱中的所有項目，並重新戳記已套用移除標記的項目。根據信箱和郵件的數量，這項處理可能會大量消耗所有信箱伺服器的資源，這些信箱伺服器內含使用保留原則的信箱，其中包括移除的標記。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當保留標記從保留原則中移除時，任何已套用標記的現有信箱項目仍會因標記的設定而到期。若要避免標記的設定套用到任何項目，您應將標記刪除。刪除標記時，也會將它從所在所有保留原則中移除。</td>
</tr>
</tbody>
</table>


## 停用保留標記

如果停用保留標記，受管理的資料夾助理員會忽略已套用該標記的項目。具有停用保留功能之保留標記的項目將永不移動或永不刪除 (視指定的保留動作而定)。因為這些項目仍被視為已標記的項目，因此 DPT 不會套用到這些項目。例如，如果要疑難排解保留標記的設定，您可以暫時停用保留標記，使受管理的資料夾助理員停止處理具有該標記的郵件。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>向使用者顯示的已停用保留標記的保留期間為 <strong>[永不]</strong>。如果使用者標記某個項目並相信永不會刪除它，稍後啟用該標記可能導致意外刪除使用者不想刪除的項目。使用 <strong>[移至封存]</strong> 動作的標記亦是如此。</td>
</tr>
</tbody>
</table>


回到頁首

## 保留功能

當使用者暫停工作且無法存取電子郵件時，可在繼續工作或可以存取電子郵件之前，先將保留設定套用至新郵件。根據保留原則，郵件可能會被刪除或移至使用者的個人封存中。您可以啟用信箱的保留功能，使保留原則在指定期間內暫時停止處理信箱。在啟用信箱的保留功能時，您也可以指定保留註解以通知信箱使用者 (或授權可存取信箱的其他使用者) 已啟用保留功能，包括排定保留功能的開始和結束時間。保留註解隨即顯示在支援的 Outlook 用戶端。您也可以依使用者慣用的語言，將保留註解當地語系化。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>啟用信箱的保留功能不會影響信箱儲存配額的處理方式。根據信箱使用量和適當的信箱配額，考慮針對休假中或有很長一段時間無法存取電子郵件的使用者，暫時增加信箱儲存配額。如需信箱儲存配額的詳細資訊，請參閱<a href="configure-storage-quotas-for-a-mailbox-exchange-2013-help.md">設定信箱的儲存配額</a>。</td>
</tr>
</tbody>
</table>


若使用者有很長一段時間不工作，可能會累積大量的電子郵件。根據電子郵件數量和缺勤時間長度而定，使用者可能會需要數週時間來排序他們的郵件。在上述情況下，請考量使用者將郵件停止保留功能之前，處理這些郵件所需要的額外時間。

如果您的組織從未執行 MRM，而且使用者不熟悉其功能，您也可以在 MRM 部署的初始*暖身與訓練*階段使用保留功能。您可以建立及部署保留原則，並教育使用者有關原則的知識，不會發生在使用者可標記項目前將項目移動或刪除的風險。在暖身與訓練期間結束前幾天，您應該提醒使用者暖身截止期限。在截止期限過後，您可將保留功能從使用者信箱移除，讓受管理的資料夾助理員可處理信箱項目並採取指定的保留動作。

如需如何為信箱設定保留功能的詳細資訊，請參閱[就地保留信箱保留 」 狀態](place-a-mailbox-on-retention-hold-exchange-2013-help.md)。

回到頁首

