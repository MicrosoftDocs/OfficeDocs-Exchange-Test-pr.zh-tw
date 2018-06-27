---
title: '保護含有文件指紋的表單資料: Exchange Online Help'
TOCTitle: 保護含有文件指紋的表單資料
ms:assetid: 110c839b-7693-42f6-aa5d-58ce64f4c357
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn635175(v=EXCHG.150)
ms:contentKeyID: 61204223
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 保護含有文件指紋的表單資料

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2014-09-11_

如果您的組織使用表單收集敏感資訊，使用者可能會嘗試透過電子郵件將這些表單傳送給外部連絡人，而產生安全性風險。Exchange 中的資料外洩防護 (DLP) 可使用[文件指紋](overview-of-document-fingerprinting-in-exchange.md)來偵測此類資訊，協助您保護資訊的安全。若要使用文件指紋，請直接上載空白表單，例如智慧財產文件、政府表單，或是您的組織中使用的其他標準表單。接著，請將產生的文件指紋新增至 DLP 原則或傳輸規則。方法如下。

> [!VIDEO https://www.microsoft.com/zh-tw/videoplayer/embed/0f803e16-397a-4b83-8a85-06cd4264aaca]

## 使用 EAC 建立文件指紋

![反白顯示 EAC 中文件指紋的路徑](images/Dn635175.e8562ea7-40ba-4feb-adde-2e81f029fcda(EXCHG.150).png "反白顯示 EAC 中文件指紋的路徑")

1.  在 Exchange 系統管理中心 (EAC) 裡，移至 \[相符性管理\] \> \[資料外洩防護\]。

2.  按一下 \[管理文件指紋\]。

3.  在文件指紋頁面上按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")，以建立新的文件指紋。

4.  在 \[名稱\] 和 \[描述\] 中提供文件指紋。(您所選擇的名稱會出現在敏感資訊類型清單中。)

5.  若要上載表單，請按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

6.  選擇 \[表單\]，並按一下 \[**開啟\]**。（請確定您上傳的檔案包含文字、 不是密碼保護且在其中一個傳輸規則中所支援的檔案類型。如需支援的檔案類型的清單，請參閱[使用檢查 Office 365 中的郵件附件的郵件流程規則](https://technet.microsoft.com/zh-tw/library/jj919236\(v=exchg.150\))。否則，您將收到的錯誤當您嘗試建立指紋。）重複針對您想要新增此文件指紋的文件清單任何其他檔案。您也可以新增或移除檔案此文件指紋稍後如果您想。

7.  按一下 **\[儲存\]**。

文件指紋屬於現在機密資訊類型，並且您可以將它新增至 DLP 原則或將其新增至**訊息中包含敏感資訊...**條件透過傳輸規則。

![反白顯示「如果出現下列情況，則套用這個規則」條件](images/Dn635175.9355a513-a790-48eb-a61b-575ba2ecdfa6(EXCHG.150).png "反白顯示「如果出現下列情況，則套用這個規則」條件")

如需將規則新增至 DLP 原則的相關資訊，請參閱[管理 DLP 原則](manage-dlp-policies-exchange-2013-help.md)的「變更 DLP 原則」一節；如需修改傳輸規則的相關資訊，請參閱[與傳輸規則整合敏感資訊規則](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md)。若要建立新原則，請參閱[從範本建立 DLP 原則](how-to-new-dlp-data-loss-prevention-policy-template.md)。

## 根據文件指紋使用命令介面建立分類規則套件

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>雖然您可以建立及修改命令介面中的分類規則套件，您可能會發現建立文件指紋是在 EAC 中更簡單。我們建議您試試看發生前嘗試這個命令介面中的程序。</td>
</tr>
</tbody>
</table>


DLP 會使用分類規則套件偵測郵件中的敏感內容。若要根據文件指紋建立分類規則套件，請使用 **New-Fingerprint** 和 **New-DataClassification** 指令程式。由於 **New-Fingerprint** 的結果不會儲存在資料分類規則外部，因此您一律會在相同的 PowerShell 工作階段中執行 **New-Fingerprint** 和 **New-DataClassification** 或 **Set-DataClassification**。下列範例會根據 C:\\My Documents\\Contoso Employee Template.docx 檔案建立新的文件指紋。您可以將新的指紋儲存為變數，讓您可以將它與相同 PowerShell 工作階段中的 **New-DataClassification** 指令程式搭配使用。

    $Employee_Template = Get-Content "C:\My Documents\Contoso Employee Template.docx" -Encoding byte
    $Employee_Fingerprint = New-Fingerprint -FileData $Employee_Template -Description "Contoso Employee Template"

現在，我們要新建名為 "Contoso Employee Confidential" 的資料分類規則，並使其使用 C:\\My Documents\\Contoso Customer Information Form.docx 檔案的文件指紋。

    $Employee_Template = Get-Content "C:\My Documents\Contoso Customer Information Form.docx" -Encoding byte
    $Customer_Fingerprint = New-Fingerprint -FileData $Customer_Form -Description "Contoso Customer Information Form"
    New-DataClassification -Name "Contoso Customer Confidential" -Fingerprints $Customer_Fingerprint -Description "Message contains Contoso customer information." 

您現在可以使用 **Get-DataClassification** 指令程式尋找所有的 DLP 資料分類規則套件；在此範例中，"Contoso Customer Confidential" 會成為資料分類規則套件清單的一部分。

最後，請將 "Contoso Customer Confidential" 資料分類規則套件新增至 DLP 原則。

    New-TransportRule -Name "Notify :External Recipient Contoso confidential" -NotifySender NotifyOnly -Mode Enforce -SentToScope NotInOrganization -MessageContainsDataClassification @{Name=" Contoso Customer Confidential"}

DLP 代理程式現已可偵測符合 Contoso Customer Form.docx 文件指紋的文件。

如需語法及參數的相關資訊，請參閱 [New-Fingerprint](https://technet.microsoft.com/zh-tw/library/dn584142\(v=exchg.150\))、[New-DataClassification](https://technet.microsoft.com/zh-tw/library/dn584139\(v=exchg.150\))、[Set-DataClassification](https://technet.microsoft.com/zh-tw/library/dn584141\(v=exchg.150\)) 和 [Get-DataClassification](https://technet.microsoft.com/zh-tw/library/jj215720\(v=exchg.150\))。

## 相關資訊

[文件指紋](overview-of-document-fingerprinting-in-exchange.md)

[管理 DLP 原則](manage-dlp-policies-exchange-2013-help.md)

[與傳輸規則整合敏感資訊規則](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md)

