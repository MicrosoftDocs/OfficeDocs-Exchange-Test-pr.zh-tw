---
title: '了解管理角色範圍篩選器: Exchange 2013 Help'
TOCTitle: 了解管理角色範圍篩選器
ms:assetid: 6acc2922-ee9c-41f1-8a0f-10a541e8c273
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd298043(v=EXCHG.150)
ms:contentKeyID: 50473434
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 了解管理角色範圍篩選器

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

管理角色範圍篩選器可以用來定義是高度可自訂的管理範圍。您可以使用範圍篩選器來建立範圍符合如何您分割您的收件者、 資料庫及伺服器，讓系統管理員能夠管理應該具有存取權的物件。範圍篩選器可以使用幾乎任何收件者、 資料庫或伺服器的物件屬性。

若要使用管理角色範圍篩選器，您必須熟悉管理角色範圍。如需管理角色範圍的詳細資訊，請參閱[了解管理角色範圍](understanding-management-role-scopes-exchange-2013-help.md)。

使用**New-ManagementScope**指令程式可建立在 Microsoft Exchange Server 2013這個篩選過的自訂範圍。規則的範圍及獨佔範圍分為兩種類型的篩選過的範圍、 收件者及組態 （其中包含的伺服器和資料庫的範圍）。下列清單顯示哪些參數**New-ManagementScope**指令程式用來建立每一種經過篩選的範圍上：

  - **收件者一般篩選範圍**   若要建立此類型的篩選範圍，可使用 *RecipientRestrictionFilter* 參數。

  - **收件者獨佔篩選範圍**   若要建立此類型的篩選範圍，可將 *RecipientRestrictionFilter* 參數和 *Exclusive* 參數一起使用。

  - **伺服器型組態一般篩選範圍**   若要建立此類型的篩選範圍，可使用 *ServerRestrictionFilter* 參數。

  - **伺服器型組態獨佔篩選範圍**   若要建立此類型的篩選範圍，可將 *ServerRestrictionFilter* 參數和 *Exclusive* 參數一起使用。

  - **資料庫型組態一般篩選範圍**   若要建立此類型的篩選範圍，可使用 *DatabaseRestrictionFilter* 參數。

  - **資料庫型組態獨佔篩選範圍**   若要建立此類型的篩選範圍，可將 *DatabaseRestrictionFilter* 參數和 *Exclusive* 參數一起使用。

當您建立這個篩選過的自訂範圍時，範圍就會嘗試比對具有可存取的管理角色隱含讀取範圍內的任何物件的篩選。如果找到物件，它會包含在篩選所傳回的結果並物件可供由自訂領域的管理角色。篩選不能傳回的管理角色的隱含讀取範圍外的結果。

如果您指定收件者篩選器使用*RecipientRestrictionFilter*參數，您可以使用*RecipientRoot*參數指定組織單位 (OU) 來限制篩選器。當您在*RecipientRoot*參數中指定的 OU 時、 收件者篩選器會嘗試比對的位於該 OU 僅，而不是內隱含整個讀取範圍收件者。

若要使用本主題中所含的可篩選內容建立管理範圍，請參閱[建立規則或獨佔範圍](create-a-regular-or-exclusive-scope-exchange-2013-help.md)。

## 篩選器語法

收件者和設定篩選器來建立篩選器查詢使用相同的語法。所有篩選查詢至少必須都具有、，下列元件：

  - **左括號**   左大括弧 ({) 表示篩選器查詢的開頭。

  - **若要檢查的屬性**  屬性是您想要測試對物件的值。例如，這可以是縣/市或部門在收件者物件、 Active Directory站台名稱或在 \[伺服器組態物件的伺服器名稱或資料庫組態物件上的資料庫名稱。

  - **比較運算子**  比較運算子會指示查詢評估對儲存在屬性的值指定值的方式。例如，比較運算子可以是**Eq**，這表示等於;**Ne**，這表示不等於;**Like**，這表示類似為等等。您可以使用Exchange管理命令介面中的運算子的完整清單，請參閱[比較運算子](https://technet.microsoft.com/zh-tw/library/bb125229\(v=exchg.150\))。

  - **若要比較的值**  您指定篩選條件查詢中的值會與儲存在所指定之屬性的值相比較。您指定的值必須以引號 （"）。如果您想要指定部分的字串，您可以萬用字元 （\*） 括住您提供的字串及使用支援萬用字元項目，例如**Like**比較運算子。部分的字串會包含任何字串會比對 filter 查詢。

  - **右括號**   右大括弧 (}) 表示篩選器查詢的結尾。

下列為選用元件，可用來建立更複雜的篩選器查詢：

  - **括弧**  如同數學、 括弧 （），在篩選查詢可讓您強制作業會發生的順序。最內層括號會先評估及篩選查詢向外運作來外層括號。

  - **邏輯運算子**  邏輯運算子結合在一起的一或多個比較作業且需要 filter 查詢來評估整個陳述式。例如，邏輯運算子包括**And**、 **Or**、 和**Not**。

當放在一起，則只要查詢看起來像是`{ City -Eq "Vancouver" }`。此篩選器會比對出**City**屬性的值等於字串"溫哥華"任何收件者。

另一個、 較複雜的查詢是`{ ((City -Eq "Vancouver") -And (Department -Eq "Sales")) -Or (Title -Like "*Manager*") }`。篩選查詢評估下列順序：

1.  來評估屬性**City**和**Department** 。每個設定為`True`或`False`，儲存在每個屬性值而定。

2.  然後會評估**City**及**Department**陳述式的結果。如果兩者都是`True`、 整個**And**陳述式會變成`True`。如果一或兩`False`，整個**And**陳述式會變成`False`。下列適用於：
    
      - 如果**And**陳述式會評估為`True`，因為**Or**運算子會指出查詢或其他的其中一邊必須是`True`整個篩選查詢會變成`True` 。物件會公開給角色指派。
    
      - 如果 **And** 陳述式是 `False`，篩選器查詢會繼續評估 **Title** 內容。

3.  然後評估**Title**屬性。它是設定為`True`或`False`、 **Title**屬性中儲存的值。下列適用於：
    
      - 如果**Title**屬性評估為`True`，因為**Or**運算子會指出查詢或其他的其中一邊必須是`True`整個篩選查詢會變成`True` 。物件會公開給角色指派。
    
      - 如果 **Title** 內容評估為 `False`，則整個篩選器查詢會評估為 `False`，而且物件不會對角色指派公開。

下表顯示具有這些值的範例，其指出當複雜查詢評估為 `True`，以及評估為 `False` 的情況。

### 複雜的查詢

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>City</th>
<th>Department</th>
<th>Title</th>
<th>結果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Vancouver (True)</p></td>
<td><p>Sales (True)</p></td>
<td><p>CEO (False)</p></td>
<td><p>因為<strong>City</strong>和<strong>Department</strong>評估為 True，則為 true。因為已滿足篩選查詢條件<strong>Title</strong>不會評估。</p></td>
</tr>
<tr class="even">
<td><p>Seattle (False)</p></td>
<td><p>Sales (True)</p></td>
<td><p>IT Manager (True)</p></td>
<td><p>因為<strong>Title</strong>評估為 True，則為 true。因為<strong>Title</strong>會評估為 True，滿足篩選查詢條件則會捨棄<strong>City</strong>和<strong>Department</strong>比較的結果。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>IT Manager 符合篩選器查詢條件，因為已使用 <strong>Like</strong> 比較運算子，其符合當篩選器查詢中使用萬用字元 (*) 時的部分字串。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="odd">
<td><p>Vancouver (True)</p></td>
<td><p>Marketing (False)</p></td>
<td><p>Writer (False)</p></td>
<td><p>因為 <strong>City</strong> 和 <strong>Department</strong> 都未評估為 True，而 <strong>Title</strong> 亦未評估為 True，所以為 False。</p></td>
</tr>
</tbody>
</table>


## 可篩選的收件者內容

當您建立收件者篩選，可以收件者物件上使用幾乎任何屬性。如需可篩選的收件者屬性的清單，請參閱[-RecipientFilter 參數的可篩選內容](https://technet.microsoft.com/zh-tw/library/bb738157\(v=exchg.150\))。本主題討論屬性可以與其他指令程式上的*RecipientFilter*參數搭配使用，雖然大部分的這些屬性也*RecipientRestrictionFilter*參數上使用**New-ManagementScope**指令程式。

## 可篩選的伺服器內容

當您使用 *ServerRestrictionFilter* 參數建立管理範圍時，可使用下列伺服器內容：

  - **CurrentServerRole**

  - **CustomerFeedbackEnabled**

  - **DataPath**

  - **DistinguishedName**

  - **ExchangeLegacyDN**

  - **ExchangeLegacyServerRole**

  - **ExchangeVersion**

  - **Fqdn**

  - **Guid**

  - **InternetWebProxy**

  - **Name**

  - **NetworkAddress**

  - **ObjectCategory**

  - **ObjectClass**

  - **ProductID**

  - **ServerRole**

  - **ServerSite**

  - **WhenChanged**

  - **WhenChangedUTC**

  - **WhenCreated**

  - **WhenCreatedUTC**

## 可篩選的資料庫內容

當您使用 *DatabaseRestrictionFilter* 參數建立管理範圍時，可使用下列資料庫內容：

  - **AdminDisplayName**

  - **AllowFileRestore**

  - **BackgroundDatabaseMaintenance**

  - **CircularLoggingEnabled**

  - **DatabaseCreated**

  - **DeletedItemRetention**

  - **Description**

  - **DistinguishedName**

  - **EdbFilePath**

  - **EventHistoryRetentionPeriod**

  - **ExchangeLegacyDN**

  - **ExchangeVersion**

  - **Guid**

  - **IssueWarningQuota**

  - **LogFilePrefix**

  - **LogFileSize**

  - **LogFolderPath**

  - **MasterServerOrAvailabilityGroup**

  - **MountAtStartup**

  - **Name**

  - **ObjectCategory**

  - **ObjectClass**

  - **RetainDeletedItemsUntilBackup**

  - **Server**

  - **WhenChanged**

  - **WhenChangedUTC**

  - **WhenCreated**

  - **WhenCreatedUTC**

