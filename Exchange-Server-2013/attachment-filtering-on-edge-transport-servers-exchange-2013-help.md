---
title: 'Edge Transport server 上的附件篩選: Exchange 2013 Help'
TOCTitle: Edge Transport server 上的附件篩選
ms:assetid: be39a181-c82e-41f5-8846-085bf1f84164
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124399(v=EXCHG.150)
ms:contentKeyID: 60828737
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Edge Transport server 上的附件篩選

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-02-10_

在 Microsoft Exchange Server 2013 中，您可以在 Edge Transport Server 上使用附件篩選，控制使用者在電子郵件中接收到的附件。附件篩選是由附件篩選代理程式 (只在 Edge Transport Server 上提供) 所執行。

## 附件篩選類型

您可以使用下列的附件篩選類型來控制透過邊際傳輸伺服器進出您組織的附件：

  - **以檔案名稱或副檔名為基礎的篩選**   您可以指定想要篩選的實際檔案名稱或副檔名。檔案名稱篩選範例為 `BadFileName.exe`。副檔名篩選範例為 `*.exe`。

  - **以檔案 MIME 內容類型為基礎的篩選**   您可以指定想要篩選的 MIME 內容類型值。MIME 內容類型值會指出附件的類型 (例如，JPEG 影像、可執行檔或 Microsoft Excel 檔案)。內容類型是以 `type/subtype` 表示。例如，JPEG 影像檔案是以 `image/jpeg` 表示。
    
    若要檢視附件篩選可偵測到之所有副檔名及內容類型的完整清單，請在 Edge Transport Server 上執行下列命令：
    
        Get-AttachmentFilterEntry | Format-List

在您定義要尋找的檔案之後，可以設定要對含有這些附件的郵件採取的動作。您不可以針對不同類型的附件指定不同的動作。您必須針對所有符合任何附件篩選的郵件，設定下列其中一個動作：

  - **拒絕 (封鎖) 郵件**   郵件會遭到封鎖。寄件者會收到未傳遞回報 (NDR)，解釋郵件包含無法接受的附件，因此未予以傳遞。您可以自訂 NDR 中的文字。預設文字為：`Message rejected due to unacceptable attachments`.

  - **刪除附件但允許郵件通過**   郵件中的附件會遭到移除。不過，郵件本身和其他任何不符合篩選的附件則允許通過。如果移除附件，就會以說明移除附件原因的文字檔取代該附件。這是預設動作。

  - **無訊息地刪除郵件**   郵件會遭到刪除。寄件者和收件者都不會收到通知。

如需相關資訊，請參閱[管理 Edge Transport server 上的附件篩選](manage-attachment-filtering-on-edge-transport-servers-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您無法擷取已封鎖的郵件或已刪除的附件。當您設定附件篩選時，請仔細檢查所有可能相符的檔案名稱，並且確認合法的附件不受篩選所影響。<br />
同時，請不要從已數位簽署、加密或保障權限的電子郵件中移除附件。如果您從這些郵件中移除附件，將導致數位簽署的郵件無效，並且使加密與保障權利的郵件變成無法閱讀。</td>
</tr>
</tbody>
</table>

