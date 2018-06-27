---
title: '將 IRM 設定 Exchange 搜尋與就地 ediscovery （英文）: Exchange 2013 Help'
TOCTitle: 將 IRM 設定 Exchange 搜尋與就地 ediscovery （英文）
ms:assetid: d96790e9-93ad-4a56-b90f-2dbfa2f2073c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg588319(v=EXCHG.150)
ms:contentKeyID: 50474362
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 將 IRM 設定 Exchange 搜尋與就地 ediscovery （英文）

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-11-16_

在 Microsoft Exchange Server 2013，您可以設定資訊版權管理 (IRM) 方便Exchange搜尋可編製索引受 IRM 保護的郵件。

當探索管理角色群組的成員執行[就地 eDiscovery](in-place-ediscovery-exchange-2013-help.md)搜尋時，受 IRM 保護的郵件搜尋結果中傳回且複製到探索信箱搜尋中指定。此外，探索管理角色群組的成員可以使用Outlook Web App來存取已複製到探索信箱因為探索搜尋的受 IRM 保護之訊息。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>探索管理角色群組的成員無法存取受 IRM 保護之訊息的探索信箱匯出至另一個信箱或.pst 檔案。只能透過使用Outlook Web App可以存取受 IRM 保護郵件中的探索信箱。</td>
</tr>
</tbody>
</table>


若欲瞭解更多與 IRM 相關的管理工作，請參閱 [資訊版權管理程序](information-rights-management-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「版權保護」項目。

  - 必須在Exchange 2013組織中設定 IRM。若要深入了解，請參閱[啟用或停用內部郵件的 IRM](enable-or-disable-irm-for-internal-messages-exchange-2013-help.md)。

  - 同盟信箱必須新增至Active Directory Rights Management Services (AD RMS) 超級使用者群組。若要深入了解，請參閱[至 AD RMS 超級使用者群組新增同盟信箱](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md)。

  - 您無法使用 Exchange 系統管理中心 (EAC) 來設定 IRM Exchange搜尋及 In-place eDiscovery。您必須使用命令介面。

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

## 使用命令介面來設定 IRM 的 Exchange 搜尋

此範例會設定 IRM 以允許Exchange搜尋編製索引受 IRM 保護的郵件。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>根據預設， <em>SearchEnabled</em>參數設為<code>$true</code>。若要停用受 IRM 保護之訊息的編製索引，請將它設為<code>$false</code>。停用編製索引的受 IRM 保護之訊息防止這些使用者搜尋信箱或時探索管理員使用就地 eDiscovery 搜尋結果中所傳回。</td>
</tr>
</tbody>
</table>


    Set-IRMConfiguration -SearchEnabled $true

如需詳細的語法及參數資訊，請參閱 [Set-IRMConfiguration](https://technet.microsoft.com/zh-tw/library/dd979792\(v=exchg.150\))。

## 使用命令介面來設定 IRM 就地 ediscovery （英文）

此範例會啟用探索信箱內的受 IRM 保護郵件存取 「 探索管理角色群組的成員。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>根據預設， <em>EDiscoverySuperUserEnabled</em>參數設為<code>$true</code>。若要停用受 IRM 保護之訊息的存取探索管理角色群組的成員，請將它設為<code>$false</code>。</td>
</tr>
</tbody>
</table>


    Set-IRMConfiguration -EDiscoverySuperUserEnabled $true

如需詳細的語法及參數資訊，請參閱 [Set-IRMConfiguration](https://technet.microsoft.com/zh-tw/library/dd979792\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要確認您已成功設定 IRM 的 Exchange 搜尋 」 和 「 就地 eDiscovery，使用**Get-IRMConfigurtaion**指令程式來擷取的 IRM 組態資訊。如需如何將擷取的 IRM 組態的範例，請參閱**Get-IRMConfiguration**中的[範例](https://technet.microsoft.com/zh-tw/e1821219-fe18-4642-a9c2-58eb0aadd61a\(exchg.150\)#examples)。

