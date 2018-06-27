---
title: '信箱移轉的 CSV 檔案: Exchange Online Help'
TOCTitle: CSV files for mailbox migration
ms:assetid: e67b3455-3946-4335-b80c-97823c76ac54
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn170437(v=EXCHG.150)
ms:contentKeyID: 54652575
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 信箱移轉的 CSV 檔案

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2017-11-16_

您可以使用 CSV 檔案以大量移轉大量的使用者信箱。您可以指定 CSV 檔案時您使用 Exchange 系統管理中心 (EAC) 或**New-MigrationBatch**指令程式在Exchange 管理命令介面建立遷移批次。使用 CSV 來指定多個使用者的遷移批次中遷移支援下列遷移情況：

  - **在內部部署 Exchange 組織中移動**
    
      - **本機移動：**本機移動是其中的信箱從一個信箱資料庫間移動。本機移動發生在單一樹系內。
    
      - **跨樹系企業移動：**在跨樹系企業移動，信箱會移至不同的樹系。跨樹系移動所啟動從目標樹系，也就是您想要信箱移至樹系，或從來源樹系，這是目前主控信箱之樹系。

  - **Exchange Online** 中的上架和下架
    
      - **Onboarding 遠端移動遷移：**在Exchange混合式部署中，您可以將信箱從內部部署Exchange組織移至Exchange Online。這也稱為是因為*onboarding*遠端移動遷移您要Exchange Online內建的信箱。
    
      - **下架遠端移動遷移：**您也可以執行「下架」遠端移動遷移，也就是將 Exchange Online 信箱遷移至您的內部部署 Exchange 組織。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>上架和下架遠端移動遷移都是從您的 Exchange Online 組織內啟動。</td>
        </tr>
        </tbody>
        </table>
    
      - **分段 Exchange 遷移：**您也可以從內部部署Exchange組織的信箱的子集將移轉至Exchange Online。這是另一種類型的 onboarding 移轉。您可以僅Exchange 2003和Exchange 2007使用遷移遷移信箱分段的Exchange 。Exchange 2010和Exchange 2013移轉信箱不支援使用分段的遷移。在執行分段式的移轉，您必須Exchange Online組織中使用目錄同步處理或其他方法來佈建的郵件使用者。
    
      - **IMAP 遷移：**此 onboarding 遷移類型會將信箱資料從 IMAP 伺服器 （包括Exchange） 移轉至Exchange Online。進行 IMAP 遷移時，您必須佈建Exchange Online中的信箱移轉信箱資料之前。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>轉換Exchange移轉不支援使用 CSV 檔案因為所有內部部署使用者信箱都會移轉至Exchange Online單一批次中。</td>
</tr>
</tbody>
</table>


## 進行大量移動或遷移時所支援在 CSV 檔中使用的屬性

第一列或欄位名稱\] 列的 CSV 檔案用於移轉的使用者清單遵循列上指定的屬性或欄位名稱。每個屬性名稱是以逗號分隔。標頭列\] 下方的每一個資料列代表個別使用者而提供遷移所需的資訊。每個個別的使用者\] 列中的屬性必須位於相同的順序為標題列中的屬性名稱。每個屬性值是以逗號分隔。特定的記錄的屬性值為 null，如果沒有輸入該屬性的任何項目。不過，請確定您包含逗點分隔的 null 值從下一個屬性。

使用 EAC 或Exchange 管理命令介面建立遷移批次時使用的相同參數時 CSV 檔案中的屬性值會覆寫對應參數的值。如需詳細資訊和範例，請參閱\] 區段中的 CSV 檔案中的屬性值會覆寫遷移批次的值。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您可以使用任何文字編輯器來建立 CSV 檔案，但使用諸如 Microsoft Excel 的應用程式可讓您輕鬆將資料匯入及設定以及組織 CSV 檔案。請務必將 CSV 檔案儲存為.csv 或.txt 檔案。</td>
</tr>
</tbody>
</table>


下列各節說明每種遷移類型的 CSV 檔案的標題列的支援的屬性。每一節包含列出每個支援的屬性表是否有必要，若要使用的屬性和描述值的範例。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>下列各節中，<em>來源環境</em>表示使用者信箱或資料庫的目前位置。<em>目標環境</em>表示將信箱移轉至的位置或信箱要移至資料庫。</td>
</tr>
</tbody>
</table>


## 本機移動

下表說明用於本機移動 CSV 檔案的支援的屬性。如需詳細資訊，請參閱[管理內部移動](manage-on-premises-moves-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>屬性</th>
<th>必要或選用</th>
<th>接受的值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EmailAddress</p></td>
<td><p>必要</p></td>
<td><p>使用者的 SMTP 位址</p></td>
<td><p>指定將會移動的使用者。</p></td>
</tr>
<tr class="even">
<td><p>TargetDatabase</p></td>
<td><p>選用</p></td>
<td><p>資料庫名稱</p></td>
<td><p>指定要移至使用者的主要信箱的信箱資料庫。您可以在不同的資料列的 CSV 檔案，可讓您將在相同的遷移批次中的信箱移至不同的資料庫指定不同的資料庫。</p></td>
</tr>
<tr class="odd">
<td><p>TargetArchiveDatabase</p></td>
<td><p>選用</p></td>
<td><p>資料庫名稱</p></td>
<td><p>指定使用者的封存信箱 （如果存在的話） 會移至的信箱資料庫。您可以在不同的資料列的 CSV 檔案，可讓您將在相同的遷移批次中的封存信箱移至不同的資料庫指定不同的資料庫。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您未指定的封存資料庫、 封存信箱移至相同的資料庫做為主要信箱。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p>BadItemLimit</p></td>
<td><p>選用</p></td>
<td><p><code>Unlimited</code>，或 <code>0</code> (預設值) 到最大值 <code>2147483647</code> 之間的非負值整數</p></td>
<td><p>指定略過如果遷移服務發生損毀的項目在信箱中的錯誤項目數目。如果您在 CSV 檔案中包含此屬性，它會覆寫預設值或指定如果在建立遷移批次使用 EAC 或Exchange 管理命令介面時包含<em>BadItemLimit</em>參數的值。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>建議您使用預設值 0，而且只有在特定使用者的移動或遷移失敗時，才對此使用者提高不良項目限制。</td>
</tr>
</tbody>
</table>

<p></p></td>
</tr>
<tr class="odd">
<td><p>MailboxType</p></td>
<td><p>選用</p></td>
<td><p>請使用下列其中一個值：</p>
<ul>
<li><p><code>PrimaryOnly</code></p></li>
<li><p><code>ArchiveOnly</code></p></li>
<li><p><code>PrimaryAndArchive</code> (預設值)</p></li>
</ul></td>
<td><p>會指定是否要移動使用者的主要信箱、 封存信箱或兩者。</p></td>
</tr>
</tbody>
</table>


## 混合式部署中的上架遠端移動遷移

在混合式部署中，您可以將信箱從內部部署Exchange組織移至Exchange Online。當 onboarding 信箱遷移批次Exchange Online組織中建立及起始Exchange Online管理員。如需詳細資訊，請參閱[在混合式部署中內部部署與 Exchange Online 組織之間移動信箱](https://technet.microsoft.com/zh-tw/library/jj906432\(v=exchg.150\))。

下表描述進行上架遠端移動遷移時，可支援在 CSV 檔案中使用的屬性。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>屬性</th>
<th>必要或選用</th>
<th>接受的值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EmailAddress</p></td>
<td><p>必要</p></td>
<td><p>使用者的 SMTP 位址</p></td>
<td><p>指定 Exchange Online 組織中擁有郵件功能之使用者的電子郵件地址，該使用者對應至將會遷移的內部部署使用者信箱。</p></td>
</tr>
<tr class="even">
<td><p>BadItemLimit</p></td>
<td><p>選用</p></td>
<td><p><code>Unlimited</code>，或 <code>0</code> (預設值) 到最大值 <code>2147483647</code> 之間的非負值整數</p></td>
<td><p>指定略過如果遷移服務發生損毀的項目在信箱中的錯誤項目數目。如果您在 CSV 檔案中包含此屬性，它會覆寫預設值或指定如果在建立遷移批次使用 EAC 或Exchange 管理命令介面時包含<em>BadItemLimit</em>參數的值。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>建議您使用預設值 0，而且只有在特定使用者的移動或遷移失敗時，才對此使用者提高不良項目限制。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="odd">
<td><p>LargeItemLimit</p></td>
<td><p>選用</p></td>
<td><p><code>Unlimited</code>，或 <code>0</code> (預設值) 到最大值之間的非負值整數。</p></td>
<td><p>指定使用者的信箱，會略過大項目數。當大項目數超過這個值時，信箱移轉失敗。</p>
<p>預設值為 0，其表示若信箱包含任何大項目，移轉便會失敗。</p>
<p>將信箱上架至 Exchange Online 時，會遷移最高 35 MB 的項目。</p></td>
</tr>
<tr class="even">
<td><p>MailboxType</p></td>
<td><p>選用</p></td>
<td><p>請使用下列其中一個值：</p>
<ul>
<li><p><code>PrimaryOnly</code></p></li>
<li><p><code>ArchiveOnly</code></p></li>
<li><p><code>PrimaryAndArchive</code> (預設值)</p></li>
</ul></td>
<td><p>會指定是否要移動使用者的主要信箱、 封存信箱或兩者。</p></td>
</tr>
</tbody>
</table>


## 混合式部署中的跨樹系企業移動和下架遠端移動遷移

如先前所述、 跨樹系移動所啟動從目標樹系或從來源樹系。Offboarding 遠端移動遷移所啟動Exchange Online組織。如需詳細資訊，請參閱：

  - [準備跨樹系移動要求的信箱](prepare-mailboxes-for-cross-forest-move-requests-exchange-2013-help.md)

  - [在混合式部署中內部部署與 Exchange Online 組織之間移動信箱](https://technet.microsoft.com/zh-tw/library/jj906432\(v=exchg.150\))

下表描述在 Exchange 混合式部署中進行跨樹系企業移動和下架遠端移動遷移時，可支援在 CSV 檔中使用的屬性。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>屬性</th>
<th>必要或選用</th>
<th>接受的值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EmailAddress</p></td>
<td><p>必要</p></td>
<td><p>使用者的 SMTP 位址</p></td>
<td><p>若是跨樹系企業移動，這指定來源樹系中的信箱或擁有郵件功能的使用者。</p>
<p>若是下架遠端移動遷移，則是指定 Exchange Online 信箱。</p></td>
</tr>
<tr class="even">
<td><p>TargetDatabase</p></td>
<td><p>所需的 offboarding 遠端移動遷移及起始從來源樹系的跨樹系企業移動。或者，這個屬性可以指定當建立遷移批次中的 EAC 或使用Exchange 管理命令介面。</p>
<p>對於從目標樹系啟動的跨樹系企業移動而言，這是選用屬性。</p></td>
<td><p>資料庫名稱</p></td>
<td><p>使用者的主要信箱要移至目標樹系中指定的信箱資料庫。您可以在不同的資料列的 CSV 檔案，可讓您將在相同的遷移批次中的信箱移至不同的資料庫指定不同的資料庫。</p></td>
</tr>
<tr class="odd">
<td><p>TargetArchiveDatabase</p></td>
<td><p>選用</p></td>
<td><p>資料庫名稱</p></td>
<td><p>使用者的封存信箱會移至目標樹系中指定的信箱資料庫。您可以在不同的資料列的 CSV 檔案，可讓您將在相同的遷移批次中的封存信箱移至不同的資料庫指定不同的資料庫。</p></td>
</tr>
<tr class="even">
<td><p>BadItemLimit</p></td>
<td><p>選用</p></td>
<td><p><code>Unlimited</code>，或 <code>0</code> (預設值) 到最大值 <code>2147483647</code> 之間的非負值整數</p></td>
<td><p>指定略過如果遷移服務發生損毀的項目在信箱中的錯誤項目數目。如果您在 CSV 檔案中包含此屬性，它會覆寫預設值或指定如果在建立遷移批次使用 EAC 或Exchange 管理命令介面時包含<em>BadItemLimit</em>參數的值。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>建議您使用預設值 0，而且只有在特定使用者的移動或遷移失敗時，才對此使用者提高不良項目限制。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="odd">
<td><p>LargeItemLimit</p></td>
<td><p>選用</p></td>
<td><p><code>Unlimited</code>，或 <code>0</code> (預設值) 到最大值之間的非負值整數。</p></td>
<td><p>指定使用者的信箱，會略過大項目數。當大項目數超過這個值時，信箱移轉失敗。</p>
<p>預設值為 0，其表示若信箱包含任何大項目，移轉便會失敗。</p>
<p>將信箱上架至 Exchange Online 時，會遷移最高 35 MB 的項目。</p></td>
</tr>
<tr class="even">
<td><p>MailboxType</p></td>
<td><p>選用</p></td>
<td><p>請使用下列其中一個值：</p>
<ul>
<li><p><code>PrimaryOnly</code></p></li>
<li><p><code>ArchiveOnly</code></p></li>
<li><p><code>PrimaryAndArchive</code> (預設值)</p></li>
</ul></td>
<td><p>會指定是否要移動使用者的主要信箱、 封存信箱或兩者。</p></td>
</tr>
</tbody>
</table>


## 分段 Exchange 遷移

您必須使用 CSV 檔案時要使用分段的 Exchange 遷移來移轉 Exchange 2003 和 Exchange 2007 內部部署信箱移轉至Exchange Online識別的遷移批次所需的使用者群組。沒有限制您可以移轉至雲端使用分段的 Exchange 遷移的信箱數目。不過，遷移批次的 CSV 檔案可以包含 1000 個資料列的最大值。若要將超過 1000 個信箱的遷移，您必須建立額外的 CSV 檔案，然後使用每個來建立新的遷移批次。如需分段 Exchange 遷移的詳細資訊，請參閱[使用分段遷移將信箱遷移至 Exchange Online](https://technet.microsoft.com/zh-tw/library/jj874018\(v=exchg.150\))。

下表描述進行分段 Exchange 遷移時，可支援在 CSV 檔中使用的屬性。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>屬性</th>
<th>必要或選用</th>
<th>接受的值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EmailAddress</p></td>
<td><p>必要</p></td>
<td><p>使用者的 SMTP 位址</p></td>
<td><p>指定啟用郵件功能的使用者 （或如果您正在重試中遷移信箱） 的電子郵件地址中Exchange Online對應至將移轉的內部部署使用者信箱。目錄同步作業由於Exchange Online或另一個佈建程序中建立擁有郵件功能的使用者。啟用郵件功能的使用者電子郵件地址必須符合對應的內部部署信箱的<em>WindowsEmailAddress</em>屬性。</p></td>
</tr>
<tr class="even">
<td><p>Password</p></td>
<td><p>選用</p></td>
<td><p>密碼至少要有 8 個字元，並且符合您 Office 365 組織套用的任何密碼限制。</p></td>
<td><p>使用者帳戶上會在遷移期間將 Exchange Online 中擁有郵件功能的相對應使用者轉換成信箱時，設定此密碼。</p></td>
</tr>
<tr class="odd">
<td><p>ForceChangePassword</p></td>
<td><p>選用</p></td>
<td><p><code>True</code>或<code>False</code></p></td>
<td><p>指定使用者第一次登入 Exchange Online 信箱時，是否必須變更密碼。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您已在內部部署組織中部署 Active Directory Federation Services 2.0 (AD FS 2.0) 來實作單一登入解決方案，您必須使用<code>False</code>此屬性的值。</td>
</tr>
</tbody>
</table>

</td>
</tr>
</tbody>
</table>


## IMAP 移轉

IMAP 遷移批次的 CSV 檔案可以有最大值為 50000 個列。但是很好移轉數個較小的批次中的使用者。如需 IMAP 移轉的詳細資訊，請參閱下列主題：

  - [將電子郵件從 IMAP 伺服器遷移至 Exchange Online 信箱](https://technet.microsoft.com/zh-tw/library/jj874015\(v=exchg.150\))

  - [IMAP 遷移批次的 CSV 檔案](https://technet.microsoft.com/zh-tw/library/jj200730\(v=exchg.150\))

下表描述進行 IMAP 遷移時，可支援在 CSV 檔中使用的屬性。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>屬性</th>
<th>必要或選用</th>
<th>接受的值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EmailAddress</p></td>
<td><p>必要</p></td>
<td><p>使用者的 SMTP 位址。</p></td>
<td><p>指定用於使用者 Exchange Online 信箱的使用者識別碼。</p></td>
</tr>
<tr class="even">
<td><p>UserName</p></td>
<td><p>必要</p></td>
<td><p>可在 IMAP 郵件系統上識別使用者的字串，需為 IMAP 伺服器支援的格式。</p></td>
<td><p>指定在 IMAP 郵件系統 （來源環境） 中的使用者帳戶的登入名稱。除了使用者名稱，您可以使用已指派存取信箱之 IMAP 伺服器上的必要權限帳戶的認證。如需詳細資訊，請參閱<a href="https://technet.microsoft.com/zh-tw/library/jj200730(v=exchg.150)">IMAP 遷移批次的 CSV 檔案</a>。</p></td>
</tr>
<tr class="odd">
<td><p>Password</p></td>
<td><p>必要</p></td>
<td><p>密碼字串。</p></td>
<td><p>指定 UserName 屬性所指定之使用者帳戶的密碼。</p></td>
</tr>
</tbody>
</table>


## CSV 檔中的屬性值會覆寫遷移批次的值

使用 EAC 或Exchange 管理命令介面建立遷移批次時使用的相同參數時 CSV 檔案中的屬性值會覆寫對應參數的值。如果您想要套用至使用者的遷移批次值，您會留該儲存格 CSV 檔案中。這可讓您混合使用且符合特定屬性值為一個遷移批次中選取的使用者。

例如，我們說您建立的批次Exchange 管理命令介面跨樹系企業移動來移動使用者的主要和封存信箱移轉至目標樹系與下列Exchange 管理命令介面命令。

    New-MigrationBatch -Name CrossForestBatch1 -SourceEndpoint ForestEndpoint1 -TargetDeliveryDomain forest2.contoso.com -TargetDatabases @(EXCH-MBX-02,EXCH-MBX-03) -TargetArchiveDatabases @(EXCH-MBX-A02,EXCH-MBX-A03) -CSVData ([System.IO.File]::ReadAllBytes("C:\Users\Administrator\Desktop\CrossForestBatch1.csv")) -AutoStart

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>預設值是要移動主要和封存信箱，因為您沒有明確地指定Exchange 管理命令介面命令中。</td>
</tr>
</tbody>
</table>


此遷移批次所用的 CrossForestBatch1.csv 檔有一部分看起來像這樣：

    EmailAddress,TargetDatabase,TargetArchiveDatabase
    user1@contoso.com,EXCH-MBX-01,EXCH-MBX-A01
    user2@contoso.com,,
    user3@contoso.com,EXCH-MBX-01,
    ...

因為 CSV 檔案中的值覆寫的遷移批次，主要的值，並為 user1 的封存信箱移至 NM-EXCH-UM-1ST MBX 01 和 NM-EXCH-UM-2ND MBX A01，分別在目標樹系中。主要和 user2 的封存信箱移至 NM-EXCH-UM-1ST-MBX-02 或 NM-EXCH-UM-1ST-MBX-03。User3 的主要信箱移至 NM-EXCH-UM-1ST MBX 01 和封存信箱移至 NM-EXCH-UM-1ST-MBX-A02 或 NM-EXCH-UM-1ST-MBX-A03。

在另一個範例中，假設您將封存信箱移至Exchange Online採用下列命令在混合部署中建立的 onboarding 遠端移動遷移批次。

    New-MigrationBatch -Name OnBoarding1 -SourceEndpoint RemoteEndpoint1 -TargetDeliveryDomain cloud.contoso.com -CSVData ([System.IO.File]::ReadAllBytes("C:\Users\Administrator\Desktop\OnBoarding1.csv")) -MailboxType ArchiveOnly -AutoStart

但您也想要移動所選使用者的主要信箱，所以此遷移批次所用的 OnBoarding1.csv 檔有一部分看起來像這樣：

    EmailAddress,MailboxType
    user1@contoso.com,
    user2@contoso.com,
    user3@cloud.contoso.com,PrimaryAndArchive
    user4@cloud.contoso.com,PrimaryAndArchive
    ...

因為 CSV 檔案中的信箱類型的值會覆寫在命令中建立的批次*MailboxType*參數的值、 只封存信箱 user1 和 user2 已移轉至Exchange Online。但主要和 user3 和 user4 封存信箱移動至Exchange Online。

