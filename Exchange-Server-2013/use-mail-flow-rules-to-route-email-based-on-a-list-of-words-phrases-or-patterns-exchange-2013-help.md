---
title: '使用清單中的文字、 片語或模式為基礎的路由電子郵件的郵件流程規則: Exchange Online Help'
TOCTitle: 使用清單中的文字、 片語或模式為基礎的路由電子郵件的郵件流程規則
ms:assetid: 4c5bee1b-58b5-4152-baef-86fa103050ae
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn951131(v=EXCHG.150)
ms:contentKeyID: 65210905
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用清單中的文字、 片語或模式為基礎的路由電子郵件的郵件流程規則

 

_**適用版本：**Exchange Online, Exchange Online Protection, Exchange Server 2013_

_**上次修改主題的時間：**2017-10-30_

若要協助您遵守貴組織的電子郵件的使用者，您可以使用Exchange傳輸規則來決定如何路由傳送電子郵件，其中包含特定字詞或模式。簡短的單字或片語清單，您可以使用Exchange 系統管理中心。較長的清單中，您可能要使用ExchangeWindows PowerShell模組以文字檔案中讀取清單。

  - 範例 1： 使用無法接受文字簡短清單

  - 範例 2： 使用過長的無法接受單字清單

如果您的組織使用的資料遺失防護 (DLP)，請參閱[資料遺失防護](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)用來識別和路由傳送電子郵件包含敏感資訊的其他選項。

## 範例 1： 使用無法接受文字簡短清單

如果您的單字或片語清單很簡短，您可以建立使用Exchange 系統管理中心的規則。例如，如果您想要確定無人傳送電子郵件使用不良字眼或拼字錯誤的公司名稱、 內部縮寫或產品名稱無法建立規則\] 以封鎖郵件並告知寄件者。請注意單字、 片語及模式不區分大小寫。

本範例會封鎖常見錯字的郵件。

![顯示根據文字模式封鎖訊息的規則](images/Dn951131.a8489cbb-be59-4890-ae30-1431703eeb88(EXCHG.150).png "顯示根據文字模式封鎖訊息的規則")

## 範例 2： 使用過長的無法接受單字清單

如果清單中的文字、 片語或模式為 long，您可以將其置於中含有每個字、 片語或圖樣的文字檔案在其專屬行。 使用Windows PowerShellExchange模組清單中的關鍵字讀入變數、 建立傳輸規則，並將使用關鍵字變數指派給傳輸規則條件。例如，下列指令碼會從呼叫 misspelled\_companyname.txt 檔案採用拼字錯誤的清單。

    $keywords=Import-Content  .\misspelled_companyname.txt
    New-TransportRule -Name "Block messages with unacceptable words" -SubjectOrBodyContainsWords $keywords -SentToScope "NotInOrganization" -RejectMessageReasonText "Do not use internal acronyms, product names, or misspellings in external communications."

## 使用的文字檔案中的片語和模式

文字檔案可以包含規則運算式的模式。這些運算式不需區分大小寫。常見的規則運算式包括：


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>運算式</strong></p></td>
<td><p><strong>符合</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>.</strong></p></td>
<td><p>任何單一字元</p></td>
</tr>
<tr class="odd">
<td><p><strong>*</strong></p></td>
<td><p>任何其他字元</p></td>
</tr>
<tr class="even">
<td><p><strong>\d</strong></p></td>
<td><p>任何十進位數字</p></td>
</tr>
<tr class="odd">
<td><p>[<em>character_group</em>]</p></td>
<td><p><em>character_group</em> 內的任何單一字元。</p></td>
</tr>
</tbody>
</table>


例如，此文字檔案包含Microsoft的常見拼字錯誤。

    [mn]sft
    [mn]icrosft
    [mn]icro soft
    [mn].crosoft

若要了解如何指定使用規則運算式模式，請參閱[規則運算式參考](https://go.microsoft.com/fwlink/p/?linkid=532394)。

