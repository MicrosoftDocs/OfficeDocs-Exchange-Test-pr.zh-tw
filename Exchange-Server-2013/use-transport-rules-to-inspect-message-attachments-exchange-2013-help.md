---
title: '使用傳輸規則檢查郵件附件: Exchange 2013 Help'
TOCTitle: 使用傳輸規則檢查郵件附件
ms:assetid: c0de687e-e33c-4e8a-b253-771494678795
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ674307(v=EXCHG.150)
ms:contentKeyID: 50474182
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用傳輸規則檢查郵件附件

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-27_

您可以設定傳輸規則，以檢查組織中的電子郵件附件。Exchange 提供的傳輸規則能夠檢查電子郵件附件，以便符合通訊安全性和規範需求。當您檢查附件時，您可以根據附件的內容或特性，對已檢查的郵件採取動作。以下是可使用傳輸規則來執行的一些附件相關工作：

  - 搜尋壓縮附件 (例如 .zip 和 .rar 檔) 中的檔案，如果有任何文字符合您指定的模式，則在郵件結尾加上免責聲明。

  - 檢查附件內的內容，如果有您指定的任何關鍵字，則將郵件轉寄給仲裁者核准之後再傳遞。

  - 檢查郵件是否有無法檢查的附件，然後阻止傳送整個郵件。

  - 檢查附件是否超過特定大小，如果您選擇防止傳遞郵件，則將問題告知寄件者。

  - 建立通知，當使用者傳送的郵件符合傳輸規則時，就向使用者發出警示。

  - 封鎖所有包含附件的郵件。如需範例，請參閱[常見的附件封鎖案例](common-attachment-blocking-scenarios-for-mail-flow-rules-exchange-2013-help.md)。

Exchange 管理員可以移至 **\[Exchange 系統管理中心\]** \> **\[郵件流程\]** \> **\[規則\]** 來建立傳輸規則。您必須已獲指派權限，才能執行此程序。開始建立新規則之後，您可以在 **\[套用此規則...\]** 下按一下 **\[更多選項\]** \> **\[任何附件\]**，以查看附件相關條件的完整清單。下圖顯示附件相關選項。

![選取附件相關規則的對話方塊](images/JJ674307.2ae4a179-bfd2-4a0e-abe1-53ed4e9e3368(EXCHG.150).jpg "選取附件相關規則的對話方塊")

如需傳輸規則的詳細資訊 (包括您可以選擇的所有條件和動作)，請參閱[郵件流程或傳輸規則](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)。＜[設定 EOP 的最佳作法](https://technet.microsoft.com/zh-tw/library/jj723164\(v=exchg.150\))＞中提供的傳輸規則最佳作法對 Exchange Online Protection (EOP) 和混合式客戶有益。如果您已準備好開始建立規則，請參閱＜[管理郵件流程規則](manage-mail-flow-rules-exchange-2013-help.md)＞。

## 檢查附件內的內容

您可以利用下表的傳輸規則條件來檢查郵件的附件內容。這些條件只檢查附件的前 150 KB。若要在檢查郵件時開始使用這些條件，您必須將這些條件新增至傳輸規則。若要了解建立或變更規則，請參閱＜[管理郵件流程規則](manage-mail-flow-rules-exchange-2013-help.md)＞。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>EAC 中的條件名稱</th>
<th>命令介面中的條件名稱</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>任何附件內容包含任何這些字詞</strong></p></td>
<td><p><code>AttachmentContainsWords</code></p></td>
<td><p>此條件可找出支援的檔案類型附件包含指定之字串或字元群組的郵件。</p></td>
</tr>
<tr class="even">
<td><p><strong>任何附件內容符合這些文字模式</strong></p></td>
<td><p><code>AttachmentMatchesPatterns</code></p></td>
<td><p>此條件可找出支援的檔案類型附件包含文字樣式符合指定規則運算式的郵件。</p></td>
</tr>
</tbody>
</table>


此處所列條件的 Exchange 管理命令介面 名稱是需要 `TransportRule` 指令程式的參數。

  -  
    若要深入了解此指令程式，請參閱＜[New-TransportRule](https://technet.microsoft.com/zh-tw/library/bb125138\(v=exchg.150\))＞。

  -  
    若要深入了解這些條件的屬性類型，請參閱＜[Conditions and exceptions for mail flow rules on Mailbox servers](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)＞。

傳輸規則只能檢查受支援檔案類型的內容。如果傳輸規則代理程式碰到不在支援的檔案類型清單中的附件，則會觸發 `AttachmentIsUnsupported` 條件。下節會列出支援的檔案類型。未列出的任何檔案都會觸發 `AttachmentIsUnsupported` 條件。

## 壓縮的封存檔

如果郵件包含壓縮的封存檔 (例如 zip 或 cab 檔)，傳輸規則代理程式將檢查包含在該附件中的檔案。此類郵件會以類似包含多個附件之郵件的方式處理。系統不會檢查壓縮封存檔的屬性。例如，就算容器檔案類型支援註解，也不會檢查該欄位。

## 傳輸規則內容檢查支援的檔案類型

下表列出傳輸規則支援的檔案類型。系統自動偵測檔案類型時會檢查檔案屬性，而非實際的副檔名，因此，可防止惡意的駭客將副檔名重新命名，而規避傳輸規則篩選。本主題稍後會列出可於傳輸規則範圍內檢查可執行程式碼的檔案類型清單。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>類別</th>
<th>副檔名</th>
<th>附註</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Office 2013、Office 2010 與 Office 2007</p></td>
<td><p>.docm, .docx, .pptm, .pptx, .pub, .one, .xlsb, .xlsm, .xlsx</p></td>
<td><p>依預設，Microsoft OneNote 和 Microsoft Publisher 檔案不受支援。您可以使用 IFilter 整合來支援這些檔案類型。如需詳細資訊，請參閱 <a href="register-filter-pack-ifilters-with-exchange-2013-exchange-2013-help.md">對 Exchange 2013 註冊 Filter Pack IFilter</a>。</p>
<p>也會檢查包含在這些檔案類型內之任何內嵌式組件的內容。然而，不會檢查任何未內嵌的物件，例如連結的文件。</p></td>
</tr>
<tr class="even">
<td><p>Office 2003</p></td>
<td><p>.doc, .ppt, .xls</p></td>
<td><p>無</p></td>
</tr>
<tr class="odd">
<td><p>其他 Office 檔案</p></td>
<td><p>.rtf, .vdw, .vsd, .vss, .vst</p></td>
<td><p>無</p></td>
</tr>
<tr class="even">
<td><p>Adobe PDF</p></td>
<td><p>.pdf</p></td>
<td><p>無</p></td>
</tr>
<tr class="odd">
<td><p>HTML</p></td>
<td><p>.html</p></td>
<td><p>無</p></td>
</tr>
<tr class="even">
<td><p>XML</p></td>
<td><p>.xml, .odp, .ods, .odt</p></td>
<td><p>無</p></td>
</tr>
<tr class="odd">
<td><p>文字</p></td>
<td><p>.txt, .asm, .bat, .c, .cmd, .cpp, .cxx, .def, .dic, .h, .hpp, .hxx, .ibq, .idl, .inc, .inf, .ini、inx, .js, .log, .m3u, .pl, .rc, .reg, .txt, .vbs, .wtx</p></td>
<td><p>無</p></td>
</tr>
<tr class="even">
<td><p>OpenDocument</p></td>
<td><p>.odp, .ods, .odt</p></td>
<td><p>不會處理 .odf 檔案的任何部分。例如，如果 .odf 檔案包含內嵌式文件，則不會檢查該內嵌式文件的內容。</p></td>
</tr>
<tr class="odd">
<td><p>AutoCAD 繪圖</p></td>
<td><p>.dxf</p></td>
<td><p>不支援 AutoCAD 2013 檔案。</p></td>
</tr>
<tr class="even">
<td><p>影像</p></td>
<td><p>.jpg, .tiff</p></td>
<td><p>只會檢查與這些影像檔案相關聯的中繼資料文字。沒有光學字元辨識功能。</p></td>
</tr>
</tbody>
</table>


## 檢查附件的檔案屬性

下列傳輸規則條件可檢查郵件所附加檔案的屬性。若要在檢查郵件時開始使用這些條件，您必須將這些條件新增至傳輸規則。此處列出可於傳輸規則範圍內檢查可執行程式碼的受支援檔案類型清單。如需建立或變更規則的詳細資訊，請參閱[管理郵件流程規則](manage-mail-flow-rules-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>EAC 中的條件名稱</th>
<th>命令介面中的條件名稱</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>任何附件檔案名稱符合這些文字模式</strong></p></td>
<td><p><code>AttachmentNameMatchesPatterns</code></p></td>
<td><p>此條件會比對受支援檔案類型附件的名稱包含指定字元的郵件。</p></td>
</tr>
<tr class="even">
<td><p><strong>任何附件副檔名包括這些字詞</strong></p></td>
<td><p><code>AttachmentExtensionMatchesWords</code></p></td>
<td><p>此條件會比對受支援檔案類型附件符合指定副檔名的郵件。</p></td>
</tr>
<tr class="odd">
<td><p><strong>任何附件都大於或等於</strong></p></td>
<td><p><code>AttachmentSizeOver</code></p></td>
<td><p>此條件會比對受支援檔案類型附件超過指定大小的郵件。</p></td>
</tr>
<tr class="even">
<td><p><strong>任何附件未完成掃描</strong></p></td>
<td><p><code>AttachmentProcessingLimitExceeded</code></p></td>
<td><p>此條件可找出未由傳輸規則代理程式檢查附件的郵件。</p></td>
</tr>
<tr class="odd">
<td><p><strong>任何附件都有可執行的內容</strong></p></td>
<td><p><code>AttachmentHasExecutableContent</code></p></td>
<td><p>此條件可找出包含可執行檔案附件的郵件。支援的檔案類型會列在此處。</p></td>
</tr>
<tr class="even">
<td><p><strong>所有附件均受密碼保護</strong></p></td>
<td><p><code>AttachmentIsPasswordProtected</code></p></td>
<td><p>此條件會比對受支援檔案類型附件由密碼保護的郵件。</p></td>
</tr>
</tbody>
</table>


此處所列條件的 Exchange 管理命令介面 名稱是需要 `TransportRule` 指令程式的參數。

  -  
    若要深入了解此指令程式，請參閱＜[New-TransportRule](https://technet.microsoft.com/zh-tw/library/bb125138\(v=exchg.150\))＞。

  -  
    若要深入了解這些條件的屬性類型，請參閱＜[Conditions and exceptions for mail flow rules on Mailbox servers](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)＞。

## 傳輸規則檢查支援的可執行檔類型

傳輸代理程式會檢查檔案屬性而不是只檢查副檔名，藉此使用真正的類型偵測。這有助於避免惡意的駭客將副檔名重新命名，而規避您的規則。下表列出這些條件支援的可執行檔類型。如果有檔案未列在其中，便會觸發 `AttachmentIsUnsupported` 條件。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>檔案類型</th>
<th>原生副檔名</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>以 WinRAR 封存程式建立的自我解壓縮封存檔案。</p></td>
<td><p>.rar</p></td>
</tr>
<tr class="even">
<td><p>具有動態連結程式庫副檔名的 32 位元 Windows 可執行檔。</p></td>
<td><p>.dll</p></td>
</tr>
<tr class="odd">
<td><p>自我解壓縮的可執行程式檔。</p></td>
<td><p>.exe</p></td>
</tr>
<tr class="even">
<td><p>Java 封存檔案。</p></td>
<td><p>.jar</p></td>
</tr>
<tr class="odd">
<td><p>解除安裝可執行檔。</p></td>
<td><p>.exe</p></td>
</tr>
<tr class="even">
<td><p>程式捷徑檔案。</p></td>
<td><p>.exe</p></td>
</tr>
<tr class="odd">
<td><p>已編譯的原始碼檔案或 3-D 物件檔案或序列檔案。</p></td>
<td><p>.obj</p></td>
</tr>
<tr class="even">
<td><p>32 位元 Windows 執行檔。</p></td>
<td><p>.exe</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Visio XML 繪圖檔案。</p></td>
<td><p>.vxd</p></td>
</tr>
<tr class="even">
<td><p>OS/2 作業系統檔案。</p></td>
<td><p>.os2</p></td>
</tr>
<tr class="odd">
<td><p>16 位元 Windows 執行檔。</p></td>
<td><p>.w16</p></td>
</tr>
<tr class="even">
<td><p>磁碟作業系統檔案。</p></td>
<td><p>.dos</p></td>
</tr>
<tr class="odd">
<td><p>歐洲電腦防毒研究協會標準防毒測試檔案。</p></td>
<td><p>.com</p></td>
</tr>
<tr class="even">
<td><p>Windows 程式資訊檔案。</p></td>
<td><p>.pif</p></td>
</tr>
<tr class="odd">
<td><p>Windows 可執行程式檔。</p></td>
<td><p>.exe</p></td>
</tr>
</tbody>
</table>


## 擴充支援的檔案類型數目

本主題中所列的支援檔案類型可以隨時使用 IFilter 整合進行修改。如需詳細資訊，請參閱 [對 Exchange 2013 註冊 Filter Pack IFilter](register-filter-pack-ifilters-with-exchange-2013-exchange-2013-help.md)。

您使用此程序新增的檔案類型會變成支援的檔案類型，而且不再觸發 `AttachmentIsUnsupported` 條件。

## 資料外洩防護原則和附件傳輸規則

為了協助您管理電子郵件中重要的商務資訊，除了資料外洩防護 (DLP) 原則，您還可以加入任何附件相關條件。例如，只有當護照號碼放在以密碼保護的附件中，您才允許傳送含有護照號碼的郵件。若要這麼做，請執行下列動作：

  - 建立 DLP 原則來檢查郵件中的護照相關機密資訊。若要深入了解，請參閱＜[DLP 程序](dlp-procedures-exchange-2013-help.md)＞。

  - 在 **\[例外狀況...\]** 傳輸規則區域中，新增 **\[任何附件均受密碼保護\]** 例外狀況。

  - 定義要對護照號碼不在受保護檔案中的郵件採取的動作。

DLP 原則和附件相關條件可將業務需求定義為傳輸規則條件、例外狀況和動作，協助您強制執行這些需求。在 DLP 原則中加入機密資訊檢查時，只會對郵件的任何附件掃描該資訊。但是，除非加入本主題列出的條件，否則不含大小或檔案類型等附件相關條件。所有 Exchange 都未提供 DLP。若要深入了解，請參閱＜[資料遺失防護](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)＞。

## 相關資訊

[資料遺失防護](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[郵件流程或傳輸規則](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[傳輸規則條件 （述詞）](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

[使用檢查 Office 365 中的郵件附件的郵件流程規則](https://technet.microsoft.com/zh-tw/library/jj919236\(v=exchg.150\)) 於 Exchange Online

