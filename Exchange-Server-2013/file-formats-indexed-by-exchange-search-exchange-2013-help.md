---
title: '依 Exchange 搜尋編製索引的檔案格式: Exchange 2013 Help'
TOCTitle: 依 Exchange 搜尋編製索引的檔案格式
ms:assetid: e5110ac1-28e1-4554-acc3-85d08c997bc5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee633485(v=EXCHG.150)
ms:contentKeyID: 52062594
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 依 Exchange 搜尋編製索引的檔案格式

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2015-07-21_

在 MicrosoftExchange Server 2013 和 Exchange Online 中，「Exchange 搜尋」包含篩選器來為常見被加成郵件附件的檔案格式類型製作索引。您也可以安裝篩選器，以製作其他檔案類型的索引。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在 Exchange 2013 中，不需要安裝和註冊 Microsoft Office Filter Pack 。<br />
根據預設，可依Exchange Server 2013內部編製索引的大小上限檔案為 32 MB。若要增加此大小限制，您必須在組織中所有的 CAS 和多重角色伺服器上新增下列登錄機碼：<br />
<code>@&quot;SOFTWARE\Microsoft\ExchangeServer\V15\Search\SystemParameters&quot;  DWORD: &quot;MaxAttachmentSize&quot;</code></td>
</tr>
</tbody>
</table>


在管理或使用「Exchange 搜尋」和相依的功能 (如[就地 eDiscovery](in-place-ediscovery-exchange-2013-help.md)) 時請注意，無法搜尋的項目、已停用索引的檔案格式，以及其內容無法供製作索引的檔案格式，這彼此之間是有差異的：

  - **無法搜尋的項目** 當 Exchange 搜尋無法針對任何人員製作特定檔案類型的索引時 (例如若是未安裝篩選器)，則搜尋該檔案類型將會失敗。包含此類附件的郵件會標記為「已部分編制索引」。若要擷取無法搜尋的項目，可使用 [Get-FailedContentIndexDocuments](https://technet.microsoft.com/zh-tw/library/dd351154\(v=exchg.150\)) 指令程式。將就地 eDiscovery 搜尋結果複製到探索信箱時，或是將搜尋結果匯出到 PST 檔案時，您可以包含無法搜尋的項目。如需詳細資訊，請參閱 [Exchange eDiscovery 中項目\] 無法搜尋](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md)。

  - **其內容無法供製作索引的檔案格式**   某些檔案類型 (如 Windows Media 視訊檔 (WMV)) 不包含可供製作索引的內容，因此無法建立索引。郵件如果包含此類檔案類型，也會在就地 eDiscovery 搜尋中當成無法搜尋的項目傳回。

  - **停用的檔案格式** 在內部部署組織中，系統管理員可以對指定的檔案格式停用索引的製作。郵件如果包含屬於停用格式的附件，就會當成無法搜尋的項目傳回。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>儘管郵件附件可能無法搜尋，或是屬於無法建立索引的檔案格式，但郵件主旨、郵件內文和其他中繼資料則可以建立索引，以在搜尋中傳回郵件。</td>
</tr>
</tbody>
</table>


如需內部部署組織中與「Exchange 搜尋」相關的其他管理工作，請參閱[Exchange 搜尋程序](exchange-search-procedures-exchange-2013-help.md)。

## 預設篩選器

下表列出 Exchange 2013 Mailbox Server 和 Exchange Online 中安裝的預設搜尋篩選器。您可以使用 [Get-SearchDocumentFormat](https://technet.microsoft.com/zh-tw/library/jj873755\(v=exchg.150\)) 指令程式來擷取預設篩選器清單。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>篩選器</th>
<th>副檔名</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>電子郵件</p></td>
<td><p>.eml</p></td>
</tr>
<tr class="even">
<td><p>圖形交換格式</p></td>
<td><p>.gif</p></td>
</tr>
<tr class="odd">
<td><p>JPEG</p></td>
<td><p>.jpeg</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Excel</p></td>
<td><p>.xls, .xlt, .xlsx, .xlsm, .xlb, .xlc, .xlsb</p></td>
</tr>
<tr class="odd">
<td><p>Excel 檔案</p></td>
<td><p>odbcexcel</p></td>
</tr>
<tr class="even">
<td><p>Microsoft InfoPath</p></td>
<td><p>.infopathml</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Office Binder</p></td>
<td><p>.obt、obd</p></td>
</tr>
<tr class="even">
<td><p>Microsoft PowerPoint</p></td>
<td><p>.pptx, .pptm, .ppt, .ppsx, .ppsm, .pps, .ppam, .potm, .pot, .potx</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Publisher</p></td>
<td><p>.pub</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Word</p></td>
<td><p>.doc, .docm, .dotx, .dotm, .dot, .docx</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft XML 文件規格</p></td>
<td><p>.xps</p></td>
</tr>
<tr class="even">
<td><p>OneNote</p></td>
<td><p>.one</p></td>
</tr>
<tr class="odd">
<td><p>OpenDocument 簡報</p></td>
<td><p>.odp</p></td>
</tr>
<tr class="even">
<td><p>OpenDocument 試算表</p></td>
<td><p>.ods</p></td>
</tr>
<tr class="odd">
<td><p>OpenDocument 文字</p></td>
<td><p>.odt</p></td>
</tr>
<tr class="even">
<td><p>Outlook 項目</p></td>
<td><p>.msg</p></td>
</tr>
<tr class="odd">
<td><p>可攜式文件格式</p></td>
<td><p>.pdf</p></td>
</tr>
<tr class="even">
<td><p>RTF 文字</p></td>
<td><p>.rtf</p></td>
</tr>
<tr class="odd">
<td><p>文字</p></td>
<td><p>.txt</p></td>
</tr>
<tr class="even">
<td><p>vCalendar</p></td>
<td><p>.vcs</p></td>
</tr>
<tr class="odd">
<td><p>vCard</p></td>
<td><p>.vcf</p></td>
</tr>
<tr class="even">
<td><p>Visio</p></td>
<td><p>.vdw, .vsd, .vss, .vst, .vsx, .vtx, .vssx, .vssm, .vsdm, .vstx, .vstm, .vdx</p></td>
</tr>
<tr class="odd">
<td><p>網頁封存</p></td>
<td><p>.mhtml</p></td>
</tr>
<tr class="even">
<td><p>網頁</p></td>
<td><p>.html</p></td>
</tr>
<tr class="odd">
<td><p>XML 文件</p></td>
<td><p>.xml</p></td>
</tr>
<tr class="even">
<td><p>ZIP 封存</p></td>
<td><p>.zip</p></td>
</tr>
</tbody>
</table>


## 已停用的檔案格式

下表列出在 Exchange 2013 Mailbox Server 上和 Exchange Online 中預設停用索引的搜尋篩選器。在 Exchange 2013 中，系統管理員可以使用 [Set-SearchDocumentFormat](https://technet.microsoft.com/zh-tw/library/jj873756\(v=exchg.150\)) Cmdlet 停用或重新啟用支援的檔案格式，以便製作索引。此 Cmdlet 無法用於 Exchange Online。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>篩選器</th>
<th>副檔名</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AVI</p></td>
<td><p>.avi</p></td>
</tr>
<tr class="even">
<td><p>點陣圖</p></td>
<td><p>.bmp</p></td>
</tr>
<tr class="odd">
<td><p>MP3</p></td>
<td><p>.mp3</p></td>
</tr>
<tr class="even">
<td><p>MPEG</p></td>
<td><p>.mpeg</p></td>
</tr>
<tr class="odd">
<td><p>PNG</p></td>
<td><p>.png</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Windows Wave Audio</p></td>
<td><p>.wav</p></td>
</tr>
</tbody>
</table>

