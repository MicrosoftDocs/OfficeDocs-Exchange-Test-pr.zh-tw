---
title: '管理內容篩選: Exchange 2013 Help'
TOCTitle: 管理內容篩選
ms:assetid: 05bd9d39-81dc-4514-8b75-7be386d5bcad
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa995953(v=EXCHG.150)
ms:contentKeyID: 50472490
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理內容篩選

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-08_

內容篩選由內容篩選器代理程式提供。內容篩選代理程式會篩選 Exchange 伺服器上來自所有接收連接器的所有郵件。這樣只會篩選出來自未經驗證的來源的郵件。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：10 分鐘

  - [反垃圾郵件和反惡意程式的權限](anti-spam-and-anti-malware-permissions-exchange-2013-help.md)主題中的您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱「反垃圾郵件功能」項目。

  - 您只能使用命令介面來執行此程序。

  - 預設在 Mailbox Server 的 Transport 服務中未啟用反垃圾郵件功能。通常只有在您的 Exchange 組織接受內送郵件之前未進行任何事前的反垃圾郵件篩選的情況下，您才會在 Mailbox Server 上啟用反垃圾郵件功能。如需詳細資訊，請參閱[啟用信箱伺服器上的反垃圾郵件功能](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md)。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 您要執行的工作

## 使用命令介面啟用或停用內容篩選

若要停用內容篩選，請執行下列命令：

    Set-ContentFilterConfig -Enabled $false

若要啟用內容篩選，請執行下列命令：

    Set-ContentFilterConfig -Enabled $true

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您停用內容篩選時，基礎內容篩選代理程式仍啟用。若要停用內容篩選器代理程式，請執行命令：<code>Disable-TransportAgent &quot;Content Filter Agent&quot;</code>。</td>
</tr>
</tbody>
</table>


## 如何知道這是否正常運作？

若要驗證您已成功啟用或停用內容篩選，請執行下列操作：

1.  執行下列命令：
    
        Get-ContentFilterConfig | Format-List Enabled

2.  確認顯示的 *Enabled* 內容值。

## 使用命令介面啟用或停用外部郵件的內容篩選

預設會對外部郵件啟用內容篩選功能。

若要停用外部郵件的內容篩選，請執行下列命令：

    Set-ContentFilterConfig -ExternalMailEnabled $false

若要啟用外部郵件的內容篩選，請執行下列命令：

    Set-ContentFilterConfig -ExternalMailEnabled $true

## 如何知道這是否正常運作？

若要驗證您已成功啟用或停用外部郵件的內容篩選，請執行下列操作：

1.  執行下列命令：
    
        Get-ContentFilterConfig | Format-List ExternalMailEnabled

2.  確認顯示的 *ExternalMailEnabled* 內容值。

## 使用命令介面啟用或停用內部郵件的內容篩選

最佳作法是不要篩選來自受信任之協力廠商或來自組織內部的郵件。執行反垃圾郵件篩選器時，篩選器永遠都有可能將非垃圾郵件偵測為垃圾郵件。若要降低篩選器錯誤處理合法電子郵件的可能性，您應讓反垃圾郵件代理程式僅針對來自潛在不受信任與未知來源的郵件執行。

若要啟用內部郵件的內容篩選，請執行下列命令：

    Set-ContentFilterConfig -InternalMailEnabled $true

若要停用內部郵件的內容篩選，請執行下列命令：

    Set-ContentFilterConfig -InternalMailEnabled $false

## 如何知道這是否正常運作？

若要驗證您已成功啟用或停用內部郵件的內容篩選，請執行下列操作：

1.  執行下列命令：
    
        Get-ContentFilterConfig | Format-List InternalMailEnabled

2.  確認顯示的 *InternalMailEnabled* 內容值。

## 使用命令介面設定收件者與寄件者例外狀況

若要取代現有的值，請執行下列命令：

    Set-ContentFilterConfig -BypassedRecipients <recipient1,recipient2...> -BypassedSenders <sender1,sender2...> -BypassedSenderDomains <domain1,domain2...>

本範例設定於內容篩選中的下列例外：

  - 收件者 laura@contoso.com 與 julia@contoso.com 未由內容篩選檢查。

  - 寄件者 steve@fabrikam.com 與 cindy@fabrikam.com 未由內容篩選檢查。

  - 所有在網域 nwtraders.com 與所有子網域中的寄件者未由內容篩選檢查。

<!-- end list -->

    Set-ContentFilterConfig -BypassedRecipients laura@contoso.com,julia@contoso.com -BypassedSenders steve@fabrikam.com,cindy@fabrikam.com -BypassedSenderDomains *.nwtraders.com

若要新增或移除項目而不修改任何現有的值，請執行下列命令：

    Set-ContentFilterConfig -BypassedRecipients @{Add="<recipient1>","<recipient2>"...; Remove="<recipient1>","<recipient2>"...} -BypassedSenders @{Add="<sender1>","<sender2>"...; Remove="<sender1>","<sender2>"...} -BypassedSenderDomains @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...}

本範例設定於內容篩選中的下列例外：

  - 新增 tiffany@contoso.com 與 chris@contoso.com 至未由內容篩選檢查的現有收件者清單。

  - 新增 joe@fabrikam.com 與 michelle@fabrikam 至未由內容篩選檢查的現有寄件者清單。

  - 新增 blueyonderairlines.com 至未由內容篩選檢查的現有寄件者清單。

  - 將網域 woodgrovebank.com 與所有子網域自未由內容篩選檢查的現有寄件者清單中移除。

<!-- end list -->

    Set-ContentFilterConfig -BypassedRecipients @{Add="tiffany@contoso.com","chris@contoso.com"} -BypassedSenders @{Add="joe@fabrikam.com","michelle@fabrikam.com"} -BypassedSenderDomains @{Add="blueyonderairlines.com"; Remove="*.woodgrovebank.com"}

## 如何知道這是否正常運作？

若要驗證您是否已成功設定收件者與寄件者例外，請執行下列命令：

1.  執行下列命令：
    
        Get-ContentFilterConfig | Format-List Bypassed*

2.  請確認顯示的值符合您所指定的設定。

## 使用命令介面來設定允許與封鎖的片語

若要新增允許與封鎖的字與詞，請執行下列命令：

    Add-ContentFilterPhrase -Influence GoodWord -Phrase <Phrase> -Influence BadWord -Phrase <Phrase>

此範例允許所有包含詞語「客戶意見」的郵件。

    Add-ContentFilterPhrase -Influence GoodWord -Phrase "customer feedback"

此範例封鎖所有包含詞語「股票訣竅」的郵件。

    Add-ContentFilterPhrase -Influence BadWord -Phrase "stock tip"

若要移除允許或封鎖的詞語，請執行下列命令：

    Remove-ContentFilterPhrase -Phrase <Phrase>

本範例移除詞語「股票訣竅」：

    Remove-ContentFilterPhrase -Phrase "stock tip"

## 如何知道這是否正常運作？

若要驗證您是否已成功設定允許與封鎖的詞語，請執行下列命令：

1.  執行下列命令：
    
        Get-ContentFilterPhrase | Format-List Influence,Phrase

2.  請確認顯示的值符合您所指定的設定。

## 使用命令介面設定 SCL 閾值

若要設定垃圾郵件信賴等級 (SCL) 閾值與動作，請執行下列命令：

    Set-ContentFilterConfig -SCLDeleteEnabled <$true | $false> -SCLDeleteThreshold <Value> -SCLRejectEnabled <$true | $false> -SCLRejectThreshold <Value> -SCLQuarantineEnabled <$true | $false> -SCLQuarantineThreshold <Value>

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>[刪除] 動作的優先順序高於 [拒絕] 動作，而 [拒絕] 動作的優先順序高於 [隔離] 動作。因此，[刪除] 動作的 SCL 閾值應大於 [拒絕] 動作的 SCL 閾值，而此閾值應大於 [隔離] 動作的 SCL 閾值。只有 [拒絕] 動作根據預設啟動，且擁有 SCL 閾值。</td>
</tr>
</tbody>
</table>


本範例設定下列的 SCL 閾值：

  - \[刪除\] 動作已啟用，且對應的 SCL 閾值設為 9。

  - \[拒絕\] 動作已啟用，且對應的 SCL 閾值設為 8。

  - \[隔離\] 動作已啟用，且對應的 SCL 閾值設為 7。

<!-- end list -->

    Set-ContentFilterConfig -SCLDeleteEnabled $true -SCLDeleteThreshold 9 -SCLRejectEnabled $true -SCLRejectThreshold 8 -SCLQuarantineEnabled $true -SCLQuarantineThreshold 7

## 如何知道這是否正常運作？

若要驗證您是否已成功設定 SCL 閾值，執行下列操作：

1.  執行下列命令：
    
        Get-ContentFilterConfig | Format-List SCL*

2.  請確認顯示的值符合您所指定的設定。

## 使用命令介面設定拒絕回應

\[拒絕\] 動作啟用時，您可自訂傳送給郵件寄件者的拒絕回應。拒絕回應不可超過 240 個字元。

若要設定自訂拒絕回應，請執行以下命令：

    Set-ContentFilterConfig -RejectionResponse "<Custom Text>"

本範例會將內容篩選器代理程式設為傳送自訂的拒絕回應。

    Set-ContentFilterConfig -RejectionResponse "Your message was rejected because it appears to be SPAM."

## 如何知道這是否正常運作？

若要驗證您是否已成功設定拒絕回應，執行下列操作：

1.  執行下列命令：
    
        Get-ContentFilterConfig | Format-List *Reject*

2.  請確認顯示的值符合您所指定的設定。

## 使用命令介面啟用或停用 Outlook 電子郵件郵戳

*Outlook 電子郵件郵戳*驗證是 Microsoft Outlook 用在外寄郵件上的計算證明，可協助收件者郵件系統分辨合法郵件和垃圾郵件。郵戳功能在 Outlook 2007 或更新版本中皆可使用。郵戳可協助降低誤判情況。Outlook 電子郵件郵戳根據預設將啟用。

若要停用 Outlook 電子郵件郵戳，請執行下列命令：

    Set-ContentFilterConfig -OutlookEmailPostmarkValidationEnabled $false

若要啟用 Outlook 電子郵件郵戳，請執行下列命令：

    Set-ContentFilterConfig -OutlookEmailPostmarkValidationEnabled $true

## 如何知道這是否正常運作？

若要驗證您是否已成功設定 Outlook 電子郵件郵戳，請執行下列步驟：

1.  執行下列命令：
    
        Get-ContentFilterConfig | Format-List OutlookEmailPostmarkValidationEnabled

2.  請確認顯示的值符合您所指定的設定。

