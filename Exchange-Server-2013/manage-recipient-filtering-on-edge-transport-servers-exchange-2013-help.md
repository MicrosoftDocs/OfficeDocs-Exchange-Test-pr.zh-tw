---
title: '管理 Edge Transport server 上的收件者篩選: Exchange 2013 Help'
TOCTitle: 管理 Edge Transport server 上的收件者篩選
ms:assetid: f2d0041f-2872-4669-95ec-443233f4956d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb125187(v=EXCHG.150)
ms:contentKeyID: 50474576
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理 Edge Transport server 上的收件者篩選

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-08_

收件者篩選功能是由 \[收件者篩選器\] 代理程式提供。在 Exchange 伺服器上啟用收件者篩選時，會篩選來自網際網路但未經驗證的內送郵件。會使用與處理外部訊息相同的方式來處理這些訊息。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>雖然您可以在 Mailbox Server 上使用收件者篩選代理程式，但是不應該進行設定。Mailbox Server 上的收件者篩選在含有其他有效收件者的郵件中偵測到一個無效或已封鎖收件者時，即會拒絕郵件。如果您在 Mailbox Server 上安裝反垃圾郵件代理程式，則預設會啟用收件者篩選代理程式。不過，不會將它設定為封鎖任何收件者。如需詳細資訊，請參閱<a href="enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md">啟用信箱伺服器上的反垃圾郵件功能</a>。</td>
</tr>
</tbody>
</table>


## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [反垃圾郵件和反惡意程式的權限](anti-spam-and-anti-malware-permissions-exchange-2013-help.md)主題中的「反垃圾郵件功能」項目。

  - 您只能使用命令介面來執行此程序。

  - 預設在 Mailbox Server 的 Transport 服務中未啟用反垃圾郵件功能。通常只有在您的 Exchange 組織接受內送郵件之前未進行任何事前的反垃圾郵件篩選的情況下，您才會在 Mailbox Server 上啟用反垃圾郵件功能。如需詳細資訊，請參閱[啟用信箱伺服器上的反垃圾郵件功能](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md)。

  - **Set-AcceptedDomain**指令程式的 *AddressBookEnabled* 參數可以啟用或停用公認的網域中，對於收件者的收件者篩選功能。依預設，會為授權網域啟用收件者篩選，為內部轉送網域和外部轉送網域停用收件者篩選。若要檢視組織中公認的網域之 *AddressBookEnabled* 參數的狀態，請執行下列命令：
    
        Get-AcceptedDomain | Format-List Name,AddressBookEnabled

  - 如果使用本主題中的程序停用收件者篩選，則會停用收件者篩選功能，但基礎的 \[收件者篩選器\] 代理程式仍維持啟用。

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

## 使用命令介面來啟用或停用收件者篩選

若要停用收件者篩選，請執行下列命令：

    Set-RecipientFilterConfig -Enabled $false

若要啟用收件者篩選，請執行下列命令：

    Set-RecipientFilterConfig -Enabled $true

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>停用收件者篩選後，基礎的 [收件者篩選器] 代理程式仍維持啟用。若要停用 [收件者篩選器] 代理程式，請執行命令：<code>Disable-TransportAgent &quot;Recipient Filter Agent&quot;</code>.</td>
</tr>
</tbody>
</table>


## 如何知道這是否正常運作？

若要確認您是否已成功啟用或停用收件者篩選，請執行下列動作：

1.  執行下列命令：
    
        Get-RecipientFilterConfig | Format-List Enabled

2.  請確認顯示的值是您所設定的值。

## 使用命令介面啟用或停用收件者封鎖清單

執行下列命令：

    Set-RecipientFilterConfig -BlockListEnabled <$true | $false>

本範例會啟用收件者封鎖清單：

    Set-RecipientFilterConfig -BlockListEnabled $true

## 如何知道這是否正常運作？

若要確認您是否已成功啟用或停用收件者封鎖清單，請執行下列動作：

1.  執行下列命令：
    
        Get-RecipientFilterConfig | Format-List BlockListEnabled

2.  請確認顯示的值是您所設定的值。

## 使用命令介面設定收件者封鎖清單

若要取代現有的值，請執行下列命令：

    Set-RecipientFilterConfig -BlockedRecipients <recipient1,recipient2...>

本範例會使用 valuesmark@contoso.com 和 kim@contoso.com 來設定收件者封鎖清單：

    Set-RecipientFilterConfig -BlockedRecipients mark@contoso.com,kim@contoso.com

若要新增或移除項目而不修改任何現有的值，請執行下列命令：

    Set-RecipientFilterConfig -BlockedRecipients @{Add="<recipient1>","<recipient2>"...; Remove="<recipient1>","<recipient2>"...}

本範例將 chris@contoso.com 加入收件者清單，並從收件者封鎖清單的收件者清單中，移除 michelle@contoso.com：

    Set-RecipientFilterConfig -BlockedRecipients @{Add="chris@contoso.com"; Remove="michelle@contoso.com"}

## 如何知道這是否正常運作？

若要確認您是否已成功設定收件者封鎖清單，請執行下列動作：

1.  執行下列命令：
    
        Get-RecipientFilterConfig | Format-List BlockedRecipients

2.  請確認顯示的值是您所設定的值。

## 使用命令介面啟用或停用收件者查閱

執行下列命令：

    Set-RecipientFilterConfig -RecipientValidationEnabled <$true | $false>

若要封鎖送至組織中不存在之收件者的郵件，請執行下列命令：

    Set-RecipientFilterConfig -RecipientValidationEnabled $true

## 如何知道這是否正常運作？

若要確認您是否已成功啟用或停用收件者查閱，請執行下列動作：

1.  執行下列命令：
    
        Get-RecipientFilterConfig | Format-List RecipientValidationEnabled

2.  請確認顯示的值是您所設定的值。

