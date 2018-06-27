---
title: '管理寄件者識別碼: Exchange 2013 Help'
TOCTitle: 管理寄件者識別碼
ms:assetid: 2e7b646a-8a66-4be7-a7c1-0bd43bb79a5b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa997136(v=EXCHG.150)
ms:contentKeyID: 50472910
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理寄件者識別碼

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-08_

寄件者識別碼功能是由寄件者識別碼代理程式所提供。寄件者識別碼來確認對寄件者網域一頭擁有者的寄件者的 IP 位址的驗證電子郵件訊息的原點而言。寄件者識別碼篩選在來自網際網路但未經過驗證的內送郵件上執行。為外部郵件處理這些訊息。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘

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

## 使用命令介面來啟用或停用寄件者識別碼

若要停用寄件者識別碼，請執行下列命令：

    Set-SenderIDConfig -Enabled $false

若要啟用寄件者識別碼，請執行下列命令：

    Set-SenderIDConfig -Enabled $true

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您停用寄件者識別碼時，仍然會啟用基礎的寄件者識別碼代理程式。若要停用寄件者識別碼代理程式，請執行命令： <code>Disable-TransportAgent &quot;Sender ID Agent&quot;</code>。</td>
</tr>
</tbody>
</table>


## 如何才能了解這是否正常運作？

若要驗證您已成功啟用或停用寄件者識別碼，請執行下列操作：

1.  執行下列命令：
    
        Get-SenderIDConfig | Format-List Enabled

2.  請確認顯示的值是您所設定的值。

## 使用命令介面針對冒名郵件設定寄件者識別碼動作

若要為冒名郵件設定寄件者識別碼動作，請執行下列命令：

    Set-SenderIDConfig -SpoofedDomainAction <StampStatus | Reject | Delete>

此範例將寄件者識別碼代理程式設定為拒絕任何傳送伺服器的 IP 位址在傳送網域的 DNS 寄件人原則架構記錄中未列為授權 SMTP 傳送伺服器的郵件。

    Set-SenderIDConfig -SpoofedDomainAction Reject

## 如何才能了解這是否正常運作？

若要驗證您是否已成功設定冒名郵件的寄件者識別碼動作，請執行下列命令：

1.  執行下列命令：
    
        Get-SenderIDConfig | Format-List SpoofedDomainAction

2.  請確認顯示的值是您所設定的值。

## 使用命令介面針對暫時性錯誤設定寄件者識別碼動作

若要為暫時性錯誤設定寄件者識別碼動作，請執行下列命令：

    Set-SenderIDConfig -TempErrorAction <StampStatus | Reject | Delete>

此範例會設定要暫時的 DNS 伺服器錯誤導致無法判斷寄件者識別碼狀態時的郵件加上戳記的寄件者識別碼代理程式。郵件會由其他反垃圾郵件代理程式處理和決定郵件的 SCL 值時所內容篩選器代理程式會使用標記。

    Set-SenderIDConfig -TempErrorAction StampStatus

請注意，`StampStatus` 為 *TempErrorAction* 參數的預設值。

## 如何才能了解這是否正常運作？

若要驗證您是否已成功設定暫時性錯誤的寄件者識別碼動作，請執行下列命令：

1.  執行下列命令：
    
        Get-SenderIDConfig | Format-List TempErrorAction

2.  請確認顯示的值是您所設定的值。

## 使用命令介面設定收件者及寄件者網域例外狀況

若要取代現有的值，請執行下列命令：

    Set-SenderIDConfig -BypassedRecipients <recipient1,recipient2...> -BypassedSenderDomains <domain1,domain2...>

此範例設定寄件者識別碼代理程式來略過傳送至 kim@contoso.com 及 john@contoso.com 的郵件寄件者識別碼檢查，並忽略來自 fabrikam.com 網域的郵件寄件者識別碼檢查。

    Set-SenderIDConfig -BypassedRecipients kim@contoso.com,john@contoso.com -BypassedSenderDomains fabrikam.com

若要新增或移除項目而不修改任何現有的值，請執行下列命令：

    Set-SenderIDConfig -BypassedRecipients @{Add="<recipient1>","<recipient2>"...; Remove="<recipient1>","<recipient2>"...} -BypassedSenderDomains @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...}

此範例透過以下資訊設定寄件者識別碼代理程式：

  - 新增 chris@contoso.com 與 michelle@contoso.com 至現有的忽略寄件者識別碼檢查清單。

  - 自現有的忽略寄件者識別碼檢查網域清單移除 tailspintoys.com。

<!-- end list -->

    Set-SenderIDConfig -BypassedRecipients @{Add="chris@contoso.com","michelle@contoso.com"} -BypassedSenderDomains @{Remove="tailspintoys.com"}

## 如何才能了解這是否正常運作？

若要驗證您是否已成功設定收件者與寄件者網域例外，請執行下列命令：

1.  執行下列命令：
    
        Get-SenderIDConfig | Format-List BypassedRecipients,BypassedSenderDomains

2.  請確認顯示的值是您所設定的值。

