---
title: '管理 Edge Transport server 上的地址修正: Exchange 2013 Help'
TOCTitle: 管理 Edge Transport server 上的地址修正
ms:assetid: 323a0b55-f921-425d-b1b0-18ad0fac315c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa997185(v=EXCHG.150)
ms:contentKeyID: 61060514
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理 Edge Transport server 上的地址修正

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-08_

您可以在 Edge Transport Server 上使用 Exchange 管理命令介面，以進行所有與地址修正和地址修正代理程式有關的管理工作。如需地址修正的相關資訊，請參閱[地址修正 Edge Transport server 上](address-rewriting-on-edge-transport-servers-exchange-2013-help.md)。

您可以建立要套用至單一收件者、套用至特定網域或子網域中的所有收件者，或對多個子網域中的所有收件者套用的地址修正項目。地址修正可以是僅限輸出，或是同時用於輸入和輸出 (雙向)。當您建立地址修正項目時，請留意下列事項：

  - 確認產生的電子郵件地址在您的組織中是唯一的。

  - 電子郵件地址值僅支援文字字串。

  - 只有內部地址 (您要變更的地址) 才支援萬用字元 (\*)。使用萬用字元的有效語法為 **\*.contoso.com**。不允許使用 **\*contoso.com** 或 **sales.\*.com** 值。

  - 使用萬用字元時，您必須將地址修正設定為「僅限輸出」(您必須將 *OutboundOnly* 參數設為 `$true` 值)。

  - 在設定僅限輸出的地址修正時 (將 *OutboundOnly* 參數設為 `$true` 值)，您必須為受影響的收件者設定 Proxy 位址。如此，郵件在傳送至修正後的地址時才能正確傳遞。

  - 依預設會對單一收件者或特定網域或子網域中的所有收件者進行雙向的地址修正 (*OutboundOnly* 參數的預設值為 `$false`)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：10 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「Edge Transport Server」一節。

  - 您只能使用命令介面來執行此程序。

  - 設定地址修正時請多加留意。您所做的任何變更都會在您執行命令後立即套用。請考慮執行使用 *WhatIf* 參數的命令。如需 *WhatIf* 參數的詳細資訊，請參閱 [WhatIf、Confirm 及 ValidateOnly 參數](whatif-confirm-and-validateonly-switches-exchange-2013-help.md)。

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

## 使用命令介面啟用或停用地址修正

若要完全啟用或停用地址修正，您可以啟用或停用地址修正代理程式。根據預設，Edge Transport Server 會啟用地址修正代理程式。

若要停用地址修正，請執行下列命令：

    Disable-TransportAgent "Address Rewriting Inbound Agent"
    Disable-TransportAgent "Address Rewriting Outbound Agent"

若要啟用地址修正，請執行下列命令：

    Enable-TransportAgent "Address Rewriting Inbound Agent"
    Enable-TransportAgent "Address Rewriting Outbound Agent"

## 如何知道這是否正常運作？

若要確認您是否已順利啟用或停用地址修正，請執行下列動作：

1.  執行下列命令：
    
        Get-TransportAgent

2.  確認地址修正輸入代理程式和地址修正輸出代理程式的 **\[已啟用\]** 內容值，是您所設定的值。

## 使用命令介面檢視地址修正項目

若要檢視所有地址修正項目的摘要清單，請執行下列命令：

    Get-AddressRewriteEntry

若要檢視地址修正項目的詳細資料，請使用下列語法。

    Get-AddressRewriteEntry <AddressRewriteEntryIdentity> | Format-List

下列範例會顯示名為「將 Contoso.com 修正為 Northwindtraders.com」的地址修正項目的詳細資料：

    Get-AddressRewriteEntry "Rewrite Contoso.com to Northwindtraders.com" | Format-List

## 使用命令介面建立地址修正項目

## 修正單一收件者的電子郵件地址

若要修正單一收件者的電子郵件地址，請使用下列語法：

    New-AddressRewriteEntry -Name "<Descriptive Name>" -InternalAddress <internal email address> -ExternalAddress <external email address> [-OutboundOnly <$true | $false>]

下列範例會為收件者 joe@contoso.com 修正所有進入及離開 Exchange 組織之郵件的電子郵件地址。輸出郵件經過修正後，看起來會像是來自 support@nortwindtraders.com。傳送至 support@northwindtraders.com 的輸入郵件會修正為 joe@contoso.com，以傳遞給收件者 (*OutboundOnly* 參數預設為 `$false`)。

    New-AddressRewriteEntry -Name "joe@contoso.com to support@northwindtraders.com" -InternalAddress joe@contoso.com -ExternalAddress support@northwindtraders.com

## 為單一網域或子網域中的收件者修正電子郵件地址

若要為單一網域或子網域中的收件者修正電子郵件地址，請使用下列語法：

    New-AddressRewriteEntry -Name "<Descriptive Name>" -InternalAddress <domain or subdomain> -ExternalAddress <domain> [-OutboundOnly <$true | $false>]

下列範例會為 contoso.com 網域中的收件者修正所有進入及離開 Exchange 組織之郵件的電子郵件地址。輸出郵件經過修正後，看起來會像是來自 fabrikam.com 網域。傳送至 fabrikam.com 電子郵件地址的輸入郵件會修正為 contoso.com，以傳遞給收件者 (*OutboundOnly* 參數預設為 `$false`)。

    New-AddressRewriteEntry -Name "Contoso to Fabrikam" -InternalAddress contoso.com -ExternalAddress fabrikam.com

下列範例會為 sales.contoso.com 子網域中的收件者從 Exchange 組織傳送出去的所有郵件修正電子郵件地址。輸出郵件經過修正後，看起來會像是來自 contoso.com 網域。傳送至 contoso.com 電子郵件地址的輸入郵件不會進行修正。

    New-AddressRewriteEntry -Name "sales.contoso.com to contoso.com" -InternalAddress sales.contoso.com -ExternalAddress contoso.com -OutboundOnly $true

## 為多個子網域中的收件者修正電子郵件地址

若要為一個網域和所有子網域中的收件者修正電子郵件地址，請使用下列語法。

    New-AddressRewriteEntry -Name "<Descriptive Name>" -InternalAddress *.<domain> -ExternalAddress <domain> -OutboundOnly $true [-ExceptionList <domain1,domain2...>]

下列範例會為 contoso.com 網域和所有子網域中的收件者從 Exchange 組織傳送出去的所有郵件修正電子郵件地址。輸出郵件經過修正後，看起來會像是來自 contoso.com 網域。傳送給 contoso.com 收件者的輸入郵件無法進行修正，因為 *InternalAddress* 參數中使用了萬用字元。

    New-AddressRewriteEntry -Name "Rewrite all contoso.com subdomains" -InternalAddress *.contoso.com -ExternalAddress contoso.com -OutboundOnly $true

下列範例與前述範例類似，差別在於，此時 legal.contoso.com 和 corp.contoso.com 子網域中的收件者所傳送的郵件一律不會進行修正：

    New-AddressRewriteEntry -Name "Rewrite all contoso.com subdomains except legal.contoso.com and corp.contoso.com" -InternalAddress *.contoso.com -ExternalAddress contoso.com -OutboundOnly $true -ExceptionList legal.contoso.com,corp.contoso.com

## 如何知道這是否正常運作？

若要確認您是否已順利建立地址修正項目，請執行下列動作：

1.  執行 `Get-AddressRewriteEntry <AddressRewriteEntryIdentity> | Format-List` 命令，並確認顯示的設定與您所設定的相同。

2.  從受到地址修正項目影響的信箱中，將測試郵件傳送至外部信箱。確認測試郵件看起來像是從修正後的電子郵件地址寄出。

3.  從外部信箱回覆測試郵件。確認原始信箱可接收回覆。

## 使用命令介面修改地址修正項目

您在修改現有地址修正項目時所能使用的組態選項，與您建立新的地址修正項目時的組態選項相同。

## 修改單一收件者的地址修正項目

若要對修正單一收件者之電子郵件地址的地址修正項目進行修改，請使用下列語法：

    Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -Name "<Descriptive Name>" -InternalAddress <internal email address> -ExternalAddress <external email address> -OutboundOnly <$true | $false>

下列範例會針對名為「joe@contoso.com 修正為 support@nortwindtraders.com」的單一收件者地址修正項目，進行下列內容的修改：

  - 將外部地址變更為 support@northwindtraders.net。

  - 將地址修正項目的名稱變更為「joe@contoso.com 修正為 support@northwindtraders.net」。

  - 將 *OutboundOnly* 的值變更為 `$true`。請注意，在進行此變更時，您必須將在 Joe 的信箱上將 support@northwindtraders.net 設定為 Proxy 位址。

<!-- end list -->

    Set-AddressRewriteEntry "joe@contoso.com to support@nortwindtraders.com" -Name "joe@contoso.com to support@northwindtraders.net" -ExternalAddress support@northwindtraders.net -OutboundOnly $true

## 為單一網域或子網域中的收件者修改地址修正項目

若要修改為單一網域或子網域中的收件者進行電子郵件地址修正的地址修正項目，請使用下列語法。

    Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -Name "<Descriptive Name>" -InternalAddress <domain or subdomain> -ExternalAddress <domain> -OutboundOnly <$true | $false>

下列範例會變更單一網域的地址修正項目「Northwind Traders 修正為 Contoso」的內部地址值。

    Set-AddressRewriteEntry "Northwindtraders to Contoso" -InternalAddress northwindtraders.net

## 為多個子網域中的收件者修改地址修正項目

若要修改為一個網域和所有子網域中的收件者進行電子郵件地址修正的地址修正項目，請使用下列語法。

    Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -Name "<Descriptive Name>" -InternalAddress *.<domain> -ExternalAddress <domain> -ExceptionList <list of domains>

若要取代多重子網域地址修正項目的現有例外狀況清單值，請使用下列語法：

    Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -ExceptionList <domain1,domain2,...>

下列範例會將多重子網域地址修正項目「Contoso 修正為 Northwind Traders」的現有例外狀況清單，取代為 marketing.contoso.com 值和 legal.contoso.com 值：

    Set-AddressRewriteEntry "Contoso to Northwind Traders" -ExceptionList sales.contoso.com,legal.contoso.com

若要在多重子網域地址修正項目中選擇性地新增或移除例外狀況清單值，而不修改任何現有的例外狀況清單值，請使用下列語法：

    Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -ExceptionList @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...}

下列範例會在多重子網域地址修正項目「Contoso 修正為 Northwind Traders」的例外狀況清單中新增 finanace.contoso.com 並移除 marketing.contoso.com：

    Set-AddressRewriteEntry "Contoso to Northwind Traders" -ExceptionList @{Add="finanace.contoso.com"; Remove="marketing.contoso.com"}

## 如何知道這是否正常運作？

若要確認您是否已順利修改地址修正項目，請執行下列動作：

1.  執行 `Get-AddressRewriteEntry <AddressRewriteEntryIdentity> | Format-List` 命令，並確認顯示的設定與您所設定的相同。

2.  從受到地址修正項目影響的信箱中，將測試郵件傳送至外部信箱。確認測試郵件看起來像是從修正後的電子郵件地址寄出。

3.  從外部信箱回覆測試郵件。確認原始信箱可接收回覆。

## 使用命令介面移除地址修正項目

若要移除單一地址修正項目，請使用下列語法：

    Remove-AddressRewriteEntry <AddressRewriteEntryIdentity>

下列範例會移除名為「Contoso.com 修正為 Northwindtraders.com」的地址修正項目：

    Remove-AddressRewriteEntry "Contoso.com to Northwindtraders.com"

若要移除多個地址修正項目，請使用下列語法：

    Get-AddressRewriteEntry [<search criteria>] | Remove-AddressRewriteEntry [-WhatIf]

下列範例會移除所有的地址修正項目：

    Get-AddressRewriteEntry | Remove-AddressRewriteEntry

下列範例會模擬如何移除在名稱中含有「修正為 contoso.com」等字詞的地址修正項目。*WhatIf* 參數可讓您直接預覽結果而不需認可任何變更。

    Get-AddressRewriteEntry "*to contoso.com" | Remove-AddressRewriteEntry -WhatIf

如果您接受結果，請再執行一次不含 *WhatIf* 參數的命令，以移除地址修正項目。

    Get-AddressRewriteEntry "*to contoso.com" | Remove-AddressRewriteEntry

## 如何知道這是否正常運作？

若要確認您是否已順利移除地址修正項目，請執行下列動作：

1.  執行 `Get-AddressRewriteEntry` 命令，並確認您所移除的地址修正項目並未列出。

2.  從受到地址修正項目影響的信箱中，將測試郵件傳送至外部信箱。確認已移除的地址修正項目對測試郵件已無影響。

3.  從外部信箱回覆測試郵件。確認原始信箱可接收回覆，且已移除的地址修正項目對郵件已無影響。

