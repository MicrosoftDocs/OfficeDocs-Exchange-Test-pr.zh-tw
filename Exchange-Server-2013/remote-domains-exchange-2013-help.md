---
title: '遠端網域: Exchange 2013 Help'
TOCTitle: 遠端網域
ms:assetid: 10fb7d62-4d78-40a3-82db-d62bcd27ba42
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa996309(v=EXCHG.150)
ms:contentKeyID: 50472588
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 遠端網域

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-07_

您可以建立遠端網域項目定義郵件傳輸時必須使用 Microsoft Exchange Server 2013組織和Exchange組織外部的網域之間的設定。當您建立的遠端網域項目時，會控制傳送至該網域的郵件的類型。您也可以套用郵件格式原則與可接受的字元組從您組織中使用者傳送至遠端網域的郵件。遠端網域的設定包括Exchange組織的通用組態設定。

遠端網域設定會在 Mailbox server 上的傳輸服務中的分類期間套用至郵件。收件者解析時發生的收件者的網域會進行比對設定的遠端網域。如果遠端網域設定封鎖特定的郵件類型阻止傳送給收件者的網域中，會刪除郵件。如果您指定特定的郵件格式為遠端網域，則會修改的郵件標頭和內容。這些設定套用至Exchange組織所處理的所有郵件。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您針對每個使用者設定郵件設定，則每個使用者設定會覆寫組織組態。</td>
</tr>
</tbody>
</table>


根據預設，有單一的遠端網域項目。網域位址空間設定為星號 （\*）。這表示所有遠端網域。如果您沒有建立其他遠端網域項目，就會傳送給所有遠端網域中的所有收件者的所有郵件都已套用至他們的相同設定。

當您設定遠端網域時，您可以防止特定類型的郵件傳送給該網域。這些訊息類型包括不在辦公室的訊息、 自動回覆郵件、 未傳遞回報 (Ndr) 及會議轉寄通知。如果您有多個樹系環境，您可能會想要允許這些類型的網域的郵件傳送。不過，如果您已識別網域中的垃圾郵件來源、 要封鎖傳送這些類型的遠端網域的郵件。

**目錄**

Message format

Automatic replies settings

Controlling NDR information

## 郵件格式

您可以指定郵件格式和用於傳送至遠端網域的電子郵件訊息的字元集。這些設定有助於確保您網域中的寄件者所傳送至遠端網域的電子郵件是相容於接收的電子郵件系統。例如，如果您知道遠端網域的郵件系統是Exchange，您可以指定一律使用Exchange rtf 格式 (RTF)。如需詳細資訊，請參閱[內容轉換](content-conversion-exchange-2013-help.md)。

## 自動回覆設定

在Exchange 2013，使用者可以指定不同的自動回覆的內部和外部收件者。此外，您的組織中可用的自動回覆類型也取決於使用 Microsoft Outlook版本。

Exchange 2013 有兩種自動回覆：

  - **外部**  支援Exchange 2013和Exchange 2010。只能由Outlook 2010或Office Outlook 2007、 設定或使用 Microsoft OfficeOutlook Web App。

  - **內部**  支援Exchange 2013和Exchange 2010。只能由Outlook 2010或Outlook 2007、 設定或使用Outlook Web App。

下表說明各種伺服器與用戶端組合，以及在每個組合中可使用的自動回覆類型。

**用戶端和伺服器的自動回覆的支援**


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>用戶端版本</th>
<th>Exchange 版本</th>
<th>支援的自動回覆</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2010或Outlook 2007</p></td>
<td><p>Exchange 2013 Exchange 2010 Exchange 2007</p></td>
<td><p>內部、外部</p></td>
</tr>
<tr class="even">
<td><p>Outlook Web App</p></td>
<td><p>Exchange 2013 Exchange 2010 Exchange 2007</p></td>
<td><p>內部、外部</p></td>
</tr>
</tbody>
</table>


## 控制 NDR 資訊

如本主題的開頭所述，您可以防止 Ndr 傳送給遠端網域。藉由封鎖阻止傳送至遠端網域的 Ndr，您可以防止離開貴組織的 NDR 郵件中包含的資訊進而限制惡意使用者可以取得的知識有關您的組織。但是，這也會防止合法的寄件者收到 Ndr，則產生混淆與遺失的產能。

Exchange 2013提供細微的控制透過目的地遠端網域的 NDR 的內容。使用Exchange 2013，您可以讓 Ndr 至遠端網域，同時去除所有的診斷資訊。如此一來，您可以仍防止資訊洩漏至組織時，同時提供給外部寄件者的 NDR 通知Exchange部署的相關。

這項功能被控制**Set-RemoteDomain**指令程式上*NDRDiagnosticInfoEnabled*參數。因為此設定可設定每個遠端網域，您可以根據您的需求的不同設定。例如，您可以選擇移除預設遠端網域的 NDR 診斷資訊但允許遠端網域代表您協力廠商的完整 NDR 診斷資訊。

如需此新設定的相關資訊，請參閱 [Set-RemoteDomain](https://technet.microsoft.com/zh-tw/library/aa997857\(v=exchg.150\))。

