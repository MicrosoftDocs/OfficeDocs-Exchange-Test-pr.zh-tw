---
title: '設定郵件流程規則的最佳作法: Exchange Online Help'
TOCTitle: 設定郵件流程規則的最佳作法
ms:assetid: abd863c3-c0ce-42f3-9470-a573adc3cbba
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn960147(v=EXCHG.150)
ms:contentKeyID: 65211635
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定郵件流程規則的最佳作法

 

_**適用版本：**Exchange Online, Exchange Online Protection, Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

遵循這些Exchange傳輸規則的最佳作法建議以避免一般設定錯誤。每個建議的連結範例與逐步說明主題。

## 測試您的規則

若要確定人的電子郵件不會發生未預期的事情及以確定您真正會議商務、 法律或規範意願的您的規則，請務必徹底測試。有許多種和規則可以彼此互動，因此請務必測試您預期同時會符合規則和以防您不經意做過一般的規則不會符合規則的訊息。若要深入了解測試規則的所有選項，請參閱[測試郵件流程規則](test-a-mail-flow-rule-exchange-2013-help.md)。

## 您的規則的範圍

請確定您的規則只適用於您想要的訊息。 例如：

  - **規則限制 \[進入\] 或 \[進階不在組織的郵件**
    
    根據預設，新的規則套用至郵件傳送或接收到您組織中的人員。因此如果您想要套用只有一個方法的規則，請務必所指定的規則條件。如需範例，請參閱[常見的附件封鎖案例](common-attachment-blocking-scenarios-for-mail-flow-rules-exchange-2013-help.md)。

  - **限制的寄件者或受話者的網域為基礎的規則**
    
    根據預設，新的規則會套用至從傳送或接收任何網域的郵件。有時您想要套用至所有網域但不包括一個，或只是一個網域的規則。如需範例，請參閱[在 Office 365 中建立全組織的安全寄件者或封鎖的寄件者清單](https://technet.microsoft.com/zh-tw/library/dn198251\(v=exchg.150\))。

所有條件和例外狀況可用的傳輸規則的完整清單，請參閱：

  - [Exchange Online 中的郵件流程規則條件和例外狀況 (predicates)](https://technet.microsoft.com/zh-tw/library/jj919235\(v=exchg.150\))

  - [傳輸規則條件 （述詞）](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

  - [郵件流程規則條件和例外狀況 （述詞） 在 \[Exchange Online Protection](https://technet.microsoft.com/zh-tw/library/jj919234\(v=exchg.150\))

## 知道您需要兩個規則

有時延長執行您想要的這兩個規則。傳輸規則處理順序，讓多個規則可以套用至相同的訊息。例如，如果其中一個動作是要封鎖郵件，而且您也可以另一個您想要套用，例如將郵件複製到寄件者的管理員或變更的通知郵件主旨的動作就需要這兩個規則。第一個規則無法將郵件複製到寄件者的管理員及變更主旨及第二個規則可能封鎖郵件。

如果您是使用類似的這兩個規則，請務必條件皆相同。若要查看範例，請查看[常見的郵件核准案例](common-message-approval-scenarios-exchange-2013-help.md)、 [常見的附件封鎖案例](common-attachment-blocking-scenarios-for-mail-flow-rules-exchange-2013-help.md)，與[整個組織的免責聲明、簽章、頁尾或標頭](organization-wide-disclaimers-signatures-footers-or-headers-exchange-online-help.md)範例 3 中的範例 3。

## 不要重複上每個電子郵件交談中的動作

電子郵件交談中的鏈結可包含許多個別的郵件，並重複上每則訊息中之記錄的動作可能會取得惱人。例如，如果您有例如新增免責聲明的動作時，可能會想要僅適用於執行緒中第一封郵件。若是如此，新增例外狀況的已包含的免責聲明文字的郵件。 如需範例，請參閱[整個組織的免責聲明、簽章、頁尾或標頭](organization-wide-disclaimers-signatures-footers-or-headers-exchange-online-help.md)。

## 了解停止規則處理時間

有時它合理停止規則處理後可於符合規則。例如，如果您有一項規則封鎖附件的郵件，另一個符合模式的郵件中插入免責聲明，您可能應該停止規則處理後郵件會遭到封鎖。有不需要進一步的動作。

若要停止規則處理之後會觸發規則，在 \[規則\] 中，選取 \[**停止處理其他規則**\] 核取方塊。

## 如果您有許多關鍵字\] 或 \[以符合模式時，會從檔案載入它們

例如，您可能會想要防止如果它們包含無法接受或不正確的文字清單傳送電子郵件。您可以建立包含這些單字和片語的文字檔案，然後使用 \[設定傳輸規則來封鎖使用這些郵件的 \[ Windows PowerShell 。

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


如需範例顯示使用規則運算式和使用，請參閱[使用清單中的文字、 片語或模式為基礎的路由電子郵件的郵件流程規則](use-mail-flow-rules-to-route-email-based-on-a-list-of-words-phrases-or-patterns-exchange-2013-help.md)Exchange模組Windows PowerShell命令的文字檔案。

若要了解如何指定使用規則運算式模式，請參閱[規則運算式參考](https://go.microsoft.com/fwlink/p/?linkid=532394)。

