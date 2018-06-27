---
title: '管理寄件者篩選: Exchange 2013 Help'
TOCTitle: 管理寄件者篩選
ms:assetid: a7f4b3e1-2970-45ad-911e-a9f46d880d3d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124087(v=EXCHG.150)
ms:contentKeyID: 50473893
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理寄件者篩選

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-08_

寄件者篩選是由寄件者篩選器代理程式所提供。寄件者篩選器代理程式依賴來決定何種巨集指令，才會內送的電子郵件上的任何**MAIL FROM:** SMTP 標頭。

當 Exchange 伺服器上啟用寄件者篩選功能時，寄件者篩選功能會篩選經由該電腦上的所有接收連接器傳入的所有郵件。

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

## 使用命令介面來啟用或停用寄件者篩選

若要停用寄件者篩選，請執行下列命令：

    Set-SenderFilterConfig -Enabled $false

若要啟用寄件者篩選，請執行下列命令：

    Set-SenderFilterConfig -Enabled $true

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您停用寄件者篩選時，仍會啟用基礎的寄件者篩選器代理程式。若要停用寄件者篩選器代理程式，請執行命令： <code>Disable-TransportAgent &quot;Sender Filter Agent&quot;</code>。</td>
</tr>
</tbody>
</table>


## 如何才能了解這是否正常運作？

若要確認已成功啟用或停用寄件者篩選，請執行下列操作：

1.  執行下列命令：
    
        Get-SenderFilterConfig | Format-List Enabled

2.  請確認顯示的值是您所設定的值。

## 使用命令介面設定封鎖的寄件者和網域

若要取代現有的值，請執行下列命令：

    Set-SenderFilterConfig -BlockedSenders <sender1,sender2...> -BlockedDomains <domain1,domain2...> -BlockedDomainsAndSubdomains <domain1,domain2...>

此範例會設定寄件者篩選器代理程式封鎖來自 kim@contoso.com 和 john@contoso.com 的郵件、來自 fabrikam.com 網域的郵件，以及來自 northwindtraders.com 和所有其子網域的郵件。

    Set-SenderFilterConfig -BlockedSenders kim@contoso.com,john@contoso.com -BlockedDomains fabrikam.com -BlockedDomainsAndSubdomains northwindtraders.com

若要新增或移除項目而不修改任何現有的值，請執行下列命令：

    Set-SenderFilterConfig -BlockedSenders @{Add="<sender1>","<sender2>"...; Remove="<sender1>","<sender2>"...} -BlockedDomains @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...} -BlockedDomainsAndSubdomains @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...}

此範例會以下列資訊設定寄件者篩選器代理程式：

  - 將 chris@contoso.com 和 michelle@contoso.com 新增至現有的封鎖寄件者清單。

  - 從現有的封鎖寄件者網域清單移除 tailspintoys.com。

  - 將 blueyonderairlines.com 新增至現有的封鎖寄件者網域和子網域清單。

<!-- end list -->

    Set-SenderFilterConfig -BlockedSenders @{Add="chris@contoso.com","michelle@contoso.com"} -BlockedDomains @{Remove="tailspintoys.com"} -BlockedDomainsAndSubdomains @{Add="blueyonderairlines.com"}

## 如何才能了解這是否正常運作？

若要確認是否已成功設定封鎖的寄件者，請執行下列操作：

1.  執行下列命令：
    
        Get-SenderFilterConfig | Format-List BlockedSenders,BlockedDomains,BlockedDomainsAndSubdomains

2.  請確認顯示的值是您所設定的值。

## 使用命令介面啟用或停用封鎖空白寄件者的郵件

若要啟用或停用封鎖空白寄件者的郵件，請執行下列命令：

    Set-SenderFilterConfig -BlankSenderBlockingenabled <$true | $false>

此範例會設定封鎖未指定寄件者從郵件中的郵件寄件者篩選器代理程式： SMTP 命令：

    Set-SenderFilterConfig -BlankSenderBlockingEnabled $true

## 如何才能了解這是否正常運作？

若要確認已成功啟用或停用封鎖空白寄件者的郵件，請執行下列操作：

1.  執行下列命令：
    
        Get-SenderFilterConfig | Format-List BlankSenderBlockingEnabled

2.  請確認顯示的值是您所設定的值。

