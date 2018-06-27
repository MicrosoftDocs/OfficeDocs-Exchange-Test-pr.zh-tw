---
title: '管理網站信箱佈建原則: Exchange 2013 Help'
TOCTitle: 管理網站信箱佈建原則
ms:assetid: 2f160d1a-a031-461f-8d29-c9cd49ca1645
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ710340(v=EXCHG.150)
ms:contentKeyID: 50472780
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理網站信箱佈建原則

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2013-02-21_

網站信箱佈建原則僅適用於傳送至網站信箱與來自網站信箱的電子郵件，以及在 Exchange 伺服器上的網站信箱大小。

若要深入了解網站信箱，請參閱[網站信箱](site-mailboxes-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [共用和協同作業的權限](sharing-and-collaboration-permissions-exchange-2013-help.md)主題中的「站台信箱」項目。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

  - 雖然您可以建立多個站台信箱佈建原則，請佈建原則的預設值將會套用至所有站台信箱。您無法將多個原則套用在組織內。

  - 您無法使用 Exchange 系統管理中心 (EAC) 執行此程序。您必須使用命令介面。

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

## 建立網站信箱佈建原則

此範例建立具有下列設定的預設佈建原則 SM\_ProvisioningPolicy：

  - 網站的信箱的警告配額是 9 GB。

  - 當信箱大小達 10GB 時，站台信箱會禁止接收郵件。

  - 可傳送至站台信箱的電子郵件大小上限為 50 MB。

<!-- end list -->

    New-SiteMailboxProvisioningPolicy -Name SM_ProvisioningPolicy -IsDefault -IssueWarningQuota 9GB -ProhibitSendReceiveQuota 10GB -MaxReceiveSize 50MB

## 檢視網站信箱佈建原則的設定

此範例會傳回組織中所有關於站台信箱佈建原則的詳細資訊。

    Get-SiteMailboxProvisioningPolicy | Format-List

此範例會傳回組織中所有原則，但僅會顯示 `IsDefault` 資訊，以識別何者為預設原則。

    Get-SiteMailboxProvisioningPolicy | Format-List IsDefault

## 對現有的網站信箱佈建原則進行變更

此範例會變更站台信箱佈建原則名為允許的站台信箱到 25 MB 可以接收的電子郵件大小上限的預設值。（當您安裝 Exchange 時，具有**預設**名稱即會建立佈建原則）。

    Set-SiteMailboxProvisioningPolicy -Identity Default -MaxReceiveSize 25MB

本範例會變更警告配額至 9.5 GB，限制傳送與接收配額至 10 GB。

    Set-SiteMailboxProvisioningPolicy -Identity Default -IssueWarningQuota 9GB -ProhibitSendReceiveQuota 10GB

## 設定站台信箱名稱前置詞

建立新的站台信箱之後，根據預設其電子郵件地址必須前置詞。電子郵件地址前置詞可讓您輕鬆地搜尋及查詢站台信箱並可能會協助他們也能辨識的使用者。如果您選擇，您可以停用首碼，或在 Office 365 租用戶或在內部部署中的指定樹系變更前置詞。預設的前置詞行為，如果您的網站信箱建立 Office 365 中的預設前置字元是**SMO-**。或者，如果您在內部部署中建立站台信箱、 前置字元為**SM-**。預設行為不同這些內部部署之間使混合客戶不會發生衝突如果站台信箱在兩個位置中所建立且再同步處理跨部署。

此範例會將 *DefaultAliasPrefixEnabled* 參數設為 $false，以停用前置詞命名。

    Set-SiteMailboxProvisioningPolicy -Identity Default -DefaultAliasPrefixEnabled $false -AliasPrefix $null

此範例會變更預設佈建原則，並將 *AliasPrefix* 設為 FOREST01。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>對於有多個樹系的部署，建議在每個樹系中使用不同的前置詞，以避免如果在兩個以上的樹系中建立了同名的站台信箱，當物件在樹系之間同步處理時發生衝突。</td>
</tr>
</tbody>
</table>


    Set-SiteMailboxProvisioningPolicy -Identity Default -AliasPrefix FOREST01 -DefaultAliasPrefixEnabled $false

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>但如果是必須 Exchange 內部部署的混合式部署與 Office 365 中，所有的雲端架構的站台信箱會建立具有前置詞<strong>SMO-</strong>。前置詞是不同 Office 365 與 Exchange 內部部署，因此將不會遇到混合客戶衝突如果站台信箱在兩個位置中所建立且再同步處理跨部署。AliasPrefix 參數會優先於 DefaultAliasPrefixEnabled 參數 ；因此，如果<em>AliasPrefix</em>參數設為有效，非 null 字串每個新的站台信箱必須加上別名前面的字串。</td>
</tr>
</tbody>
</table>


## 刪除網站信箱佈建原則

此範例刪除在 Exchange 安裝期間建立的網站信箱佈建原則。

    Remove-SiteMailboxProvisioningPolicy -Identity Default

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您必須先建立並指定預設原則，才能移除命名為 [預設] 的原則。</td>
</tr>
</tbody>
</table>


## 相關資訊

如需詳細的語法及參數資訊，請參閱下列主題：

[New-SiteMailboxProvisioningPolicy](https://technet.microsoft.com/zh-tw/library/jj218647\(v=exchg.150\))

[Get-SiteMailboxProvisioningPolicy](https://technet.microsoft.com/zh-tw/library/jj218617\(v=exchg.150\))

[Set-SiteMailboxProvisioningPolicy](https://technet.microsoft.com/zh-tw/library/jj218624\(v=exchg.150\))

[Remove-SiteMailboxProvisioningPolicy](https://technet.microsoft.com/zh-tw/library/jj218672\(v=exchg.150\))

