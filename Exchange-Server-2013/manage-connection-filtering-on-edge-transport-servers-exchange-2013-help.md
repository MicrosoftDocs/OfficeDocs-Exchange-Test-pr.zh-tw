---
title: '管理 Edge Transport Server 上的連線篩選: Exchange 2013 Help'
TOCTitle: 管理 Edge Transport Server 上的連線篩選
ms:assetid: baebc865-ec3e-48ca-ac48-7aac8b34c003
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124376(v=EXCHG.150)
ms:contentKeyID: 60828736
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理 Edge Transport Server 上的連線篩選

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-08_

連線篩選是連線篩選代理程式所提供的反垃圾郵件功能，而連線篩選代理程式只有 Microsoft Exchange 2013 的 Edge Transport Server 上才有。連線篩選使下列功能可以使用：

  - IP 封鎖清單

  - IP 封鎖清單提供者

  - IP 允許清單

  - IP 允許清單提供者

可以個別地啟用或停用其中每一個功能。

## 開始之前有哪些須知？

  - 預估完成時間：15 分鐘。

  - [反垃圾郵件和反惡意程式的權限](anti-spam-and-anti-malware-permissions-exchange-2013-help.md)主題中的您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱「反垃圾郵件功能」項目。

  - 您只能使用命令介面來執行此程序。

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

## 使用命令介面啟用或停用連線篩選

若要完全啟用或停用連線篩選，您可以啟用或停用連線篩選代理程式。這項變更會在您重新啟動 Microsoft Exchange Transport 服務之後生效。在 Edge Transport Server 上重新啟動 Microsoft Exchange Transport 服務時，會暫時中斷該伺服器上的郵件流程。

若要停用連線篩選，請執行下列命令：

    Disable-TransportAgent "Connection Filtering Agent"

若要啟用連線篩選，請執行下列命令：

    Enable-TransportAgent "Connection Filtering Agent"

若要讓變更生效，請執行下列命令來重新啟動 Microsoft Exchange Transport 服務：

    Restart-Service MSExchangeTransport

## 如何知道這是否正常運作？

若要確認您已順利啟用或停用連線篩選，請執行下列命令，並確認顯示的值就是您設定的值。

    Get-TransportAgent "Connection Filtering Agent" | Format-List Enabled

## IP 封鎖清單程序

這些程序適用於您手動設定的 IP 封鎖清單。它們不適用於 IP 封鎖清單提供者。

使用 **IPBlockListConfig** 指令程式可以檢視和設定連線篩選使用 IP 封鎖清單的方式。使用 **IPBlockListEntry** 指令程式可以檢視和設定 IP 封鎖清單中的 IP 位址。

## 使用命令介面檢視 IP 封鎖清單的組態

若要檢視 IP 封鎖清單的組態，請執行下列命令：

    Get-IPBlockListConfig | Format-List *Enabled,*Response

## 使用命令介面啟用或停用 IP 封鎖清單

若要停用 IP 封鎖清單，請執行下列命令：

    Set-IPBlockListConfig -Enabled $false

若要啟用 IP 封鎖清單，請執行下列命令：

    Set-IPBlockListConfig -Enabled $true

## 如何知道這是否正常運作？

若要確認您已順利啟用或停用 IP 封鎖清單，請執行下列命令，並確認顯示的值就是您設定的值。

    Get-IPBlockListConfig | Format-List Enabled

## 使用命令介面設定 IP 封鎖清單

若要設定 IP 封鎖清單，請使用下列語法：

    Set-IPBlockListConfig [-ExternalMailEnabled <$true | $false>] [-InternalMailEnabled <$true | $false> -MachineEntryRejectionResponse "<Custom response text>"] [-StaticEntryRejectionResponse "<Custom response text>"]

此範例會使用下述的設定來設定 IP 封鎖清單：

  - IP 封鎖清單會篩選來自內部和外部郵件伺服器的傳入連線。預設只會篩選來自外部郵件伺服器的連線 (*ExternalMailEnabled* 設定為 `$true`，而 *InternalMailEnabled* 設定為 `$false`)。來自外部合作夥伴的未驗證連線和已驗證連線皆視為外部連線。

  - 連線如果是依通訊協定分析代理程式的寄件者信譽功能自動新增至 IP 封鎖清單的 IP 位址篩選而得，則其自訂回應文字會設定為「寄件者信譽已拒絕來自 IP 位址 {0} 的連線」值。

  - 連線如果是依手動新增至 IP 封鎖清單的 IP 位址篩選而得，則其自訂回應文字會設定為「連線篩選已拒絕來自 IP 位址 {0} 的連線」值。

<!-- end list -->

    Set-IPBlockListConfig -InternalMailEnabled $true -MachineEntryRejectionResponse "Connection from IP address {0} was rejected by sender reputation." -StaticEntryRejectionResponse "Connection from IP address {0} was rejected by connection filtering."

## 如何知道這是否正常運作？

若要確認您已順利設定 IP 封鎖清單，請執行下列命令，並確認顯示的值就是您設定的值。

    Get-IPBlockListConfig | Format-List *MailEnabled,*Response

## 使用命令介面檢視 IP 封鎖清單項目

若要檢視所有 IP 封鎖清單項目，請執行下列命令：

    Get-IPBlockListEntry

請注意，每個 IP 封鎖清單項目都是以整數值識別。當您新增項目至 IP 封鎖清單和 IP 允許清單時，系統會依遞增順序來指派身分識別整數。

若要檢視特定 IP 封鎖清單項目，請使用下列語法：

    Get-IPBlockListEntry <-Identity IdentityInteger | -IPAddress IPAddress>

例如，若要檢視含有 IP 位址 192.168.1.13 的 IP 封鎖清單項目，請執行下列命令：

    Get-IPBlockListEntry -IPAddress 192.168.1.13

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您使用 <em>IPAddress</em> 參數時，產生的 IP 封鎖清單項目可以是一個個別 IP 位址、某個 IP 位址範圍或一個無類別網域間路由選擇 (CIDR) IP。若要使用 <em>Identity</em> 參數，您可以指定指派給 IP 封鎖清單項目的整數值。</td>
</tr>
</tbody>
</table>


## 使用命令介面新增 IP 封鎖清單項目

若要新增 IP 封鎖清單項目，請使用下列語法：

    Add-IPBlockListEntry <-IPAddress IPAddress | -IPRange IP range or CIDR IP> [-ExpirationTime <DateTime>] [-comment "<Descriptive Comment>"]

下列範例會為 192.168.1.10 到 192.168.1.15 這個 IP 位址範圍新增一個 IP 封鎖清單項目，並設定此 IP 封鎖清單項目在 2014 年 7 月 4 日 15:00 到期。

    Add-IPBlockListEntry -IPRange 192.168.1.10-192.168.1.15 -ExpirationTime "7/4/2014 15:00"

## 如何知道這是否正常運作？

若要確認您已順利新增 IP 封鎖清單項目，請執行下列命令，並確認新的 IP 封鎖清單項目已顯示。

    Get-IPBlockListEntry

## 使用命令介面移除 IP 封鎖清單項目

若要移除 IP 封鎖清單項目，請使用下列語法：

    Remove-IPBlockListEntry <IdentityInteger>

下列範例會移除 *Identity* 值為 3 的 IP 封鎖清單項目。

    Remove-IPBlockListEntry 3

下列範例會移除含有 IP 位址 192.168.1.12 的 IP 封鎖清單項目，而不使用 *Identity* 整數值。請注意，IP 封鎖清單項目可以是個別 IP 位址或 IP 位址範圍。

    Get-IPBlockListEntry -IPAddress 192.168.1.12 | Remove-IPBlockListEntry

## 如何知道這是否正常運作？

若要確認您已順利移除 IP 封鎖清單項目，請執行下列命令，並確認移除的 IP 封鎖清單項目已消失。

    Get-IPBlockListEntry

## IP 封鎖清單提供者程序

這些程序適用於 IP 封鎖清單提供者。它們不適用於 IP 封鎖清單。

使用 **IPBlockListProvidersConfig** 指令程式可以檢視和設定連線篩選使用所有 IP 封鎖清單提供者的方式。使用 **IPBlockListProvider** 指令程式可以檢視、設定和測試 IP 封鎖清單提供者。

## 使用命令介面檢視所有 IP 封鎖清單提供者的組態

若要檢視連線篩選使用所有 IP 封鎖清單提供者的方式，請執行下列命令：

    Get-IPBlockListProvidersConfig | Format-List *Enabled,Bypassed*

## 使用命令介面啟用或停用所有 IP 封鎖清單提供者

若要停用所有 IP 封鎖清單提供者，請執行下列命令：

    Set-IPBlockListProvidersConfig -Enabled $false

若要啟用所有 IP 封鎖清單提供者，請執行下列命令：

    Set-IPBlockListProvidersConfig -Enabled $true

## 如何知道這是否正常運作？

若要確認您已啟用或停用所有 IP 封鎖清單提供者，請執行下列命令，並確認顯示的值就是您設定的值。

    Get-IPBlockListProvidersConfig | Format-List Enabled

## 使用命令介面設定所有 IP 封鎖清單提供者

若要設定連線篩選使用所有 IP 封鎖清單提供者的方式，請使用下列語法：

    Set-IPBlockListProvidersConfig [-BypassedRecipients <recipient1,recipient2...>] [-ExternalMailEnabled <$true | $false>] [-InternalMailEnabled <$true | $false>]

下列範例使用下列設定來設定所有 IP 封鎖清單提供者：

  - IP 封鎖清單提供者會篩選來自內部和外部郵件伺服器的傳入連線。預設只會篩選來自外部郵件伺服器的連線 (*ExternalMailEnabled* 設定為 `$true`，而 *InternalMailEnabled* 設定為 `$false`)。來自外部合作夥伴的未驗證連線和已驗證連線皆視為外部連線。

  - 傳送至內部收件者 chris@fabrikam.com 和 michelle@fabrikam.com 的郵件會排除於 IP 封鎖清單提供者進行的篩選範圍外。請注意，如果您想要新增收件者至清單，而不影響現有收件者，請使用語法：`@{Add="<recipient1>","<recipient2>"...}`。

<!-- end list -->

    Set-IPBlockListProvidersConfig -BypassedRecipients chris@fabrikam.com,michelle@fabrikam.com -InternalMailEnabled $true

如需詳細資訊，請參閱 [Set-IPBlockListProvidersConfig](https://technet.microsoft.com/zh-tw/library/aa998543\(v=exchg.150\))。

## 如何知道這是否正常運作？

若要確認您已順利設定所有 IP 封鎖清單提供者，請執行下列命令，並確認顯示的值就是您設定的值。

    Get-IPBlockListProvidersConfig | Format-List *MailEnabled,Bypassed*

## 使用命令介面檢視 IP 封鎖清單提供者

若要檢視所有 IP 封鎖清單提供者的摘要清單，請執行下列命令：

    Get-IPBlockListProvider

若要檢視特定提供者的詳細資料，請使用下列語法：

    Get-IPBlockListProvider <IPBlockListProviderIdentity>

下列範例顯示名稱為「Contoso IP Block List Provider」之提供者的詳細資料。

    Get-IPBlockListProvider "Contoso IP Block List Provider" | Format-List Name,Enabled,Priority,LookupDomain,*Match,*Response

## 使用命令介面新增 IP 封鎖清單提供者

若要新增 IP 封鎖清單提供者，請使用下列語法：

    Add-IPBlockListProvider -Name "<Descriptive Name>" -LookupDomain <FQDN> [-Priority <Integer>] [-Enabled <$true | $false>] [-AnyMatch <$true | $false>] [-BitmaskMatch <IPAddress>] [-IPAddressesMatch <IPAddressStatusCode1,IPAddressStatusCode2...>] [-RejectionResponse "<Custom Text>"]

此範例會使用下列選項來建立名稱為 "Contoso IP Block List Provider" 的 IP 封鎖清單提供者：

  - **要用來使用此提供者的 FQDN**   rbl.contoso.com

  - **要從此提供者使用的位元遮罩代碼**   127.0.0.1

<!-- end list -->

    Add-IPBlockListProvider -Name "Contoso IP Block List Provider" -LookupDomain rbl.contoso.com -BitmaskMatch 127.0.0.1

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您新增 IP 封鎖清單提供者時，預設會啟用它 (<em>Enabled</em> 的值是 <code>$true</code>)，而且優先順序值會遞增 (第一個項目的 <em>Priority</em> 值為 1)。</td>
</tr>
</tbody>
</table>


如需詳細資訊，請參閱 [Add-IPBlockListProvider](https://technet.microsoft.com/zh-tw/library/bb124358\(v=exchg.150\))。

## 如何知道這是否正常運作？

若要確認您已順利新增 IP 封鎖清單提供者，請執行下列命令，並確認新的 IP 封鎖清單提供者已顯示。

    Get-IPBlockListProvider

## 使用命令介面啟用或停用 IP 封鎖清單提供者

若要啟用或停用特定 IP 封鎖清單提供者，請使用下列語法：

    Set-IPBlockListProvider <IPBlockListProviderIdentity> -Enabled <$true | $false>

下列範例會停用名稱為 Contoso IP Block List Provider 的提供者。

    Set-IPBlockListProvider "Contoso IP Block List Provider" -Enabled $false

下列範例會啟用名稱為 Contoso IP Block List Provider 的提供者。

    Set-IPBlockListProvider "Contoso IP Block List Provider" -Enabled $true

## 如何知道這是否正常運作？

若要確認您已順利啟用或停用 IP 封鎖清單提供者，請執行下列命令，並確認顯示的值就是您設定的值。

    Get-IPBlockListProvider <IPBlockListProviderIdentity> | Format-List Enabled

## 使用命令介面設定 IP 封鎖清單提供者

**Set-IPBlockListProvider** 指令程式上可用的組態選項，與 **New-IPBlockListProvider** 指令程式上可用的組態選項相同。

若要設定現有 IP 封鎖清單提供者，請使用下列語法：

    Set-IPBlockListProvider <IPBlockListProviderIdentity> -Name "<Descriptive Name>" -LookupDomain <FQDN> [-Priority <Integer>] [-AnyMatch <$true | $false>] [-BitmaskMatch <IPAddress>] [-IPAddressesMatch <IPAddressStatusCode1,IPAddressStatusCode2...>] [-RejectionResponse "<Custom Text>"]

例如，若要將 IP 位址狀態碼 127.0.0.1 新增至名稱為 Contoso IP Block List Provider 之提供者的現有狀態碼清單，請執行下列命令：

    Set-IPBlockListProvider "Contoso IP Block List Provider" -IPAddressesMatch @{Add="127.0.0.1"}

如需詳細資訊，請參閱 [Set-IPBlockListProvider](https://technet.microsoft.com/zh-tw/library/bb124979\(v=exchg.150\))。

## 如何知道這是否正常運作？

若要確認您已順利設定 IP 封鎖清單提供者，請執行下列命令，並確認顯示的值就是您設定的值。

    Get-IPBlockListProvider <IPBlockListProviderIdentity> | Format-List

## 使用命令介面測試 IP 封鎖清單提供者

若要測試 IP 封鎖清單提供者，請使用下列語法。

    Test-IPBlockListProvider <IPBlockListProviderIdentity> -IPAddress <IPAddressToTest>

下列範例會查閱 IP 位址 192.168.1.1 來測試名稱為 Contoso IP Block List Provider 的提供者。

    Test-IPBlockListProvider "Contoso IP Block List Provider" -IPAddress 192.168.1.1

## 使用命令介面移除 IP 封鎖清單提供者

若要移除 IP 封鎖清單提供者，請使用下列語法：

    Remove-IPBlockListProvider <IPBlockListProviderIdentity>

下列範例會移除名稱為 Contoso IP Block List Provider 的 IP 封鎖清單提供者。

    Remove-IPBlockListProvider "Contoso IP Block list Provider"

## 如何知道這是否正常運作？

若要確認您已順利移除 IP 封鎖清單提供者，請執行下列命令，並確認移除的 IP 封鎖清單提供者已消失。

    Get-IPBlockListProvider

## IP 允許清單程序

這些程序適用於您手動設定的 IP 允許清單。它們不適用於 IP 允許清單提供者。

使用 **IPAllowListConfig** 指令程式可以檢視和設定連線篩選使用 IP 允許清單的方式。使用 **IPAllowListEntry** 指令程式可以檢視和設定 IP 允許清單中的 IP 位址。

## 使用命令介面檢視 IP 允許清單的組態

若要檢視 IP 允許清單的組態，請執行下列命令。

    Get-IPAllowListConfig | Format-List *Enabled

## 使用命令介面啟用或停用 IP 允許清單

若要停用 IP 允許清單，請執行下列命令：

    Set-IPAllowListConfig -Enabled $false

若要啟用 IP 允許清單，請執行下列命令：

    Set-IPAllowListConfig -Enabled $true

## 如何知道這是否正常運作？

若要確認您已順利啟用或停用 IP 允許清單，請執行下列命令，並確認顯示的值就是您設定的值。

    Get-IPAllowListConfig | Format-List Enabled

## 使用命令介面設定 IP 允許清單

若要設定 IP 允許清單，請使用下列語法：

    Set-IPAllowListConfig [-ExternalMailEnabled <$true | $false>] [-InternalMailEnabled <$true | $false>

此範例會設定 IP 允許清單來篩選來自內部和外部郵件伺服器的傳入連線。預設只會篩選來自外部郵件伺服器的連線 (*ExternalMailEnabled* 設定為 `$true`，而 *InternalMailEnabled* 設定為 `$false`)。來自外部合作夥伴的未驗證連線和已驗證連線皆視為外部連線。

    Set-IPAllowListConfig -InternalMailEnabled $true

## 如何知道這是否正常運作？

若要確認您已順利設定 IP 允許清單，請執行下列命令，並確認顯示的值就是您設定的值。

    Get-IPAllowListConfig | Format-List *MailEnabled

## 使用命令介面檢視 IP 允許清單項目

若要檢視所有 IP 允許清單項目，請執行下列命令：

    Get-IPAllowListEntry

請注意，每個 IP 允許清單項目都是以整數值來識別。當您新增項目至 IP 封鎖清單和 IP 允許清單時，系統會依遞增順序來指派身分識別整數。

若要檢視特定 IP 允許清單項目，請使用下列語法：

    Get-IPAllowListEntry <-Identity IdentityInteger | -IPAddress IPAddress>

例如，若要檢視含有 IP 位址 192.168.1.13 的 IP 允許清單項目，請執行下列命令：

    Get-IPAllowListEntry -IPAddress 192.168.1.13

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您使用 <em>IPAddress</em> 參數時，產生的 IP 允許清單項目可以是一個個別 IP 位址、某個 IP 位址範圍或一個無類別網域間路由選擇 (CIDR) IP。若要使用 <em>Identity</em> 參數，您可以指定指派給 IP 允許清單項目的整數值。</td>
</tr>
</tbody>
</table>


## 使用命令介面新增 IP 允許清單項目

若要新增 IP 允許清單項目，請使用下列語法：

    Add-IPAllowListEntry <-IPAddress IPAddress | -IPRange IP range or CIDR IP> [-ExpirationTime <DateTime>] [-Comment "<Descriptive Comment>"]

下列範例會為 192.168.1.10 到 192.168.1.15 這個 IP 位址範圍新增一個 IP 允許清單項目，並設定此 IP 允許清單項目在 2014 年 7 月 4 日 15:00 到期。

    Add-IPAllowListEntry -IPRange 192.168.1.10-192.168.1.15 -ExpirationTime "7/4/2014 15:00"

## 如何知道這是否正常運作？

若要確認您已順利新增 IP 允許清單項目，請執行下列命令，並確認新的 IP 允許清單項目已顯示。

    Get-IPAllowListEntry

## 使用命令介面移除 IP 允許清單項目

若要移除 IP 允許清單項目，請使用下列語法：

    Remove-IPAllowListEntry <IdentityInteger>

下列範例會移除 *Identity* 值為 3 的 IP 允許清單項目。

    Remove-IPAllowListEntry 3

此範例會移除含有 IP 位址 192.168.1.12 的 IP 允許清單項目，而不使用 *Identity* 整數值。請注意，IP 允許清單項目可以是個別 IP 位址或 IP 位址範圍。

    Get-IPAllowListEntry -IPAddress 192.168.1.12 | Remove-IPAllowListEntry

## 如何知道這是否正常運作？

若要確認您已順利移除 IP 允許清單項目，請執行下列命令，並確認移除的 IP 允許清單項目已消失。

    Get-IPAllowListEntry

## IP 允許清單提供者程序

這些程序適用於 IP 允許清單提供者。它們不適用於 IP 允許清單。

使用 **IPAllowListProvidersConfig** 指令程式可以檢視和設定連線篩選使用所有 IP 允許清單提供者的方式。使用 **IPAllowListProvider** 指令程式可以檢視、設定和測試 IP 允許清單提供者。

## 使用命令介面檢視所有 IP 允許清單提供者的組態

若要檢視連線篩選使用所有 IP 允許清單提供者的方式，請執行下列命令：

    Get-IPAllowListProvidersConfig | Format-List *Enabled

## 使用命令介面啟用或停用所有 IP 允許清單提供者

若要停用所有 IP 允許清單提供者，請執行下列命令：

    Set-IPAllowListProvidersConfig -Enabled $false

若要啟用所有 IP 允許清單提供者，請執行下列命令：

    Set-IPAllowListProvidersConfig -Enabled $true

## 如何知道這是否正常運作？

若要確認您已啟用或停用所有 IP 允許清單提供者，請執行下列命令，並確認顯示的值就是您設定的值。

    Get-IPAllowListProvidersConfig | Format-List Enabled

## 使用命令介面設定所有 IP 允許清單提供者

若要設定連線篩選使用所有 IP 允許清單提供者的方式，請使用下列語法：

    Set-IPAllowListProvidersConfig [-ExternalMailEnabled <$true | $false>] [-InternalMailEnabled <$true | $false>]

此範例會設定所有 IP 允許清單提供者來篩選來自內部和外部郵件伺服器的傳入連線。預設只會篩選來自外部郵件伺服器的連線 (*ExternalMailEnabled* 設定為 `$true`，而 *InternalMailEnabled* 設定為 `$false`)。來自外部合作夥伴的未驗證連線和已驗證連線皆視為外部連線。

    Set-IPAllowListProvidersConfig -InternalMailEnabled $true

如需詳細資訊，請參閱 [Set-IPBlockListProvidersConfig](https://technet.microsoft.com/zh-tw/library/aa998543\(v=exchg.150\))。

## 如何知道這是否正常運作？

若要確認您已順利設定所有 IP 允許清單提供者，請執行下列命令，並確認顯示的值就是您設定的值。

    Get-IPAllowListProvidersConfig | Format-List *MailEnabled

## 使用命令介面檢視 IP 允許清單提供者

若要檢視所有 IP 允許清單提供者的摘要清單，請執行下列命令。

    Get-IPAllowListProvider

若要檢視特定提供者的詳細資料，請使用下列語法。

    Get-IPAllowListProvider <IPAllowListProviderIdentity>

此範例顯示名稱為 Contoso IP Allow List Provider 之提供者的詳細資料。

    Get-IPAllowListProvider "Contoso IP Allow List Provider" | Format-List Name,Enabled,Priority,LookupDomain,*Match

## 使用命令介面新增 IP 允許清單提供者

若要新增 IP 允許清單提供者，請使用下列語法：

    Add-IPAllowListProvider -Name "<Descriptive Name>" -LookupDomain <FQDN> [-Priority <Integer>] [-Enabled <$true | $false>] [-AnyMatch <$true | $false>] [-BitmaskMatch <IPAddress>] [-IPAddressesMatch <IPAddressStatusCode1,IPAddressStatusCode2...>]

此範例會使用下列選項來建立名稱為 "Contoso IP Allow List Provider" 的 IP 允許清單提供者：

  - **要用來使用此提供者的 FQDN**   allow.contoso.com

  - **要從此提供者使用的位元遮罩代碼**   127.0.0.1

<!-- end list -->

    Add-IPAllowListProvider -Name "Contoso IP Allow List Provider" -LookupDomain allow.contoso.com -BitmaskMatch 127.0.0.1

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您新增 IP 允許清單提供者時，預設會啟用它 (<em>Enabled</em> 的值是 <code>$true</code>)，而且優先順序值會遞增 (第一個項目的 <em>Priority</em> 值為 1)。</td>
</tr>
</tbody>
</table>


如需詳細資訊，請參閱 [Add-IPBlockListProvider](https://technet.microsoft.com/zh-tw/library/bb124358\(v=exchg.150\))。

## 如何知道這是否正常運作？

若要確認您已順利新增 IP 允許清單提供者，請執行下列命令，並確認新的 IP 允許清單提供者已顯示。

    Get-IPAllowListProvider

## 使用命令介面啟用或停用 IP 允許清單提供者

若要啟用或停用特定 IP 允許清單提供者，請使用下列語法。

    Set-IPAllowListProvider <IPAllowListProviderIdentity> -Enabled <$true | $false>

此範例會停用名稱為 Contoso IP Allow List Provider 的提供者。

    Set-IPAllowListProvider "Contoso IP Allow List Provider" -Enabled $false

此範例會啟用名稱為 Contoso IP Allow List Provider 的提供者。

    Set-IPAllowListProvider "Contoso IP Allow List Provider" -Enabled $true

## 如何知道這是否正常運作？

若要確認您已順利啟用或停用 IP 允許清單提供者，請執行下列命令，並確認顯示的值就是您設定的值。

    Get-IPAllowListProvider <IPAllowListProviderIdentity> | Format-List Enabled

## 使用命令介面設定 IP 允許清單提供者

**Set-IPAllowListProvider** 指令程式上可用的組態選項，與 **New-IPAllowListProvider** 指令程式上可用的組態選項相同。

若要設定現有 IP 允許清單提供者，請使用下列語法：

    Set-IPAllowListProvider <IPAllowListProviderIdentity> -Name "<Descriptive Name>" -LookupDomain <FQDN> [-Priority <Integer>] [-AnyMatch <$true | $false>] [-BitmaskMatch <IPAddress>] [-IPAddressesMatch <IPAddressStatusCode1,IPAddressStatusCode2...>]

例如，若要將 IP 位址狀態碼 127.0.0.1 新增至名稱為 Contoso IP Allow List Provider 之提供者的現有狀態碼清單，請執行下列命令：

    Set-IPAllowListProvider "Contoso IP Allow List Provider" -IPAddressesMatch @{Add="127.0.0.1"}

如需詳細資訊，請參閱 [Set-IPBlockListProvider](https://technet.microsoft.com/zh-tw/library/bb124979\(v=exchg.150\))。

## 如何知道這是否正常運作？

若要確認您已順利設定 IP 允許清單提供者，請執行下列命令，並確認顯示的值就是您設定的值。

    Get-IPAllowListProvider <IPAllowListProviderIdentity> | Format-List

## 使用命令介面測試 IP 允許清單提供者

若要測試 IP 允許清單提供者，請使用下列語法：

    Test-IPAllowListProvider <IPAllowListProviderIdentity> -IPAddress <IPAddressToTest>

下列範例會查閱 IP 位址 192.168.1.1 來測試名稱為 Contoso IP Allow List Provider 的提供者。

    Test-IPAllowListProvider "Contoso IP Allow List Provider" -IPAddress 192.168.1.1

## 使用命令介面移除 IP 允許清單提供者

若要移除 IP 允許清單提供者，請使用下列語法：

    Remove-IPAllowListProvider <IPAllowListProviderIdentity>

此範例會移除名稱為 Contoso IP Allow List Provider 的 IP 允許清單提供者。

    Remove-IPAllowListProvider "Contoso IP Allow List Provider"

## 如何知道這是否正常運作？

若要確認您已順利移除 IP 允許清單提供者，請執行下列命令，並確認移除的 IP 允許清單提供者已消失。

    Get-IPAllowListProvider

