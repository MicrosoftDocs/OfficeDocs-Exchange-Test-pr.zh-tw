---
title: '公用資料夾的限制: Exchange 2013 Help'
TOCTitle: 公用資料夾的限制
ms:assetid: 709b075e-9584-484b-bcaa-e781c26497b4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn594582(v=EXCHG.150)
ms:contentKeyID: 61170924
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 公用資料夾的限制

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

在 Exchange Server 2013 中，我們已將公用資料夾從傳統資料庫架構移至信箱架構。這項轉換可讓公用資料夾利用資料庫可用性群組 (DAG) 的彈性以及多年來的其他信箱加強功能來獲得好處。不過，有新的限制及效能問題應該納入考量。本文件提供組態選項的一些高階指導，而組態選項可能會影響公用資料夾效能和連線能力。

## 限制

下表列出在內部部署 Exchange Server 2013 中的公用資料夾的限制。除非限制特別另有說明，所建議，此表格中所列的值所支援的限制的公用資料夾。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>尋找 Office 365 的 Exchange Online 限制吗？請參閱<a href="https://go.microsoft.com/fwlink/?linkid=391188">Exchange Online 限制</a>。</td>
</tr>
</tbody>
</table>



<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>項目</th>
<th>限制</th>
<th>記事</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>公用資料夾信箱總數</p></td>
<td><p>100</p></td>
<td><p>雖然您可以建立 100 個以上的公用資料夾信箱，但並不予以支援。<a href="create-a-public-folder-mailbox-exchange-2013-help.md">建立公用資料夾信箱</a></p></td>
</tr>
<tr class="even">
<td><p>階層中的公用資料夾總數</p></td>
<td><p>1,000,000</p></td>
<td><p>雖然您可以建立超過 1000000 個公用資料夾，並不支援。100000 或更多公用資料夾的任何部署，建議您閱讀<a href="considerations-when-deploying-public-folders-exchange-2013-help.md">部署公用資料夾時的考量</a>。</p></td>
</tr>
<tr class="odd">
<td><p>上層資料夾下的子資料夾</p></td>
<td><p>10,000</p></td>
<td><p>雖然您可以建立超過 1000 個上層資料夾下的子資料夾，我們不建議您這麼做。</p>
<p><a href="https://technet.microsoft.com/zh-tw/library/bb123981(v=exchg.150)">Set-Mailbox</a> 指令程式上的 <em>FolderHierarchyChildrenCountReceiveQuota</em> 參數。</p></td>
</tr>
<tr class="even">
<td><p>資料夾深度</p></td>
<td><p>300</p></td>
<td><p>資料夾深度是指公用資料夾樹狀目錄的一個分支中可存在的巢狀資料夾層數。<a href="https://technet.microsoft.com/zh-tw/library/bb123981(v=exchg.150)">Set-Mailbox</a> Cmdlet 上的 <em>FolderHierarchyDepthRecieveQuota</em> 參數。</p></td>
</tr>
<tr class="odd">
<td><p>每個公用資料夾的郵件數上限</p></td>
<td><p>1 百萬</p></td>
<td><p><a href="https://technet.microsoft.com/zh-tw/library/bb123981(v=exchg.150)">Set-Mailbox</a> Cmdlet 上的 <em>MailboxMessagesPerFolderCountRecieveQuota</em> 參數。</p></td>
</tr>
<tr class="even">
<td><p>個別公用資料夾大小上限</p></td>
<td><p>10 GB</p></td>
<td><p>此限制不含單一資料夾下的子資料夾。</p>
<p><a href="configure-storage-quotas-for-a-mailbox-exchange-2013-help.md">設定信箱的儲存配額</a></p></td>
</tr>
<tr class="odd">
<td><p>公用資料夾信箱大小</p></td>
<td><p>100 GB</p></td>
<td><p><a href="configure-storage-quotas-for-a-mailbox-exchange-2013-help.md">設定信箱的儲存配額</a></p></td>
</tr>
<tr class="even">
<td><p>每個公用資料夾信箱的使用者登入數目</p></td>
<td><p>2,000 個並行使用者登入</p></td>
<td><p>建議您設定階層，讓每個公用資料夾信箱都不超過 2,000 位使用者。例如，如果您有 20,000 名使用者，則應該有 10 個公用資料夾信箱。</p></td>
</tr>
<tr class="odd">
<td><p>移動項目保留</p></td>
<td><p>建議 14 天</p></td>
<td><p>在 <strong>Set-OrganizationConfig</strong> Cmdlet 上使用 <em>DefaultPublicFolderMovedItemRetention</em> 參數。</p></td>
</tr>
<tr class="even">
<td><p>保留天數</p></td>
<td><p>建議您將此項目設為用於一般信箱的相同預設值。</p></td>
<td><p>在下列層級可以進行這些設定：</p>
<ul>
<li><p><strong>組織層級：</strong> <strong>Set-OrganizationConfig</strong> Cmdlet 上的 <em>DefaultPublicFolderAgeLimit</em> 參數。</p></li>
<li><p><strong>信箱層級：</strong> <strong>Set-Mailbox</strong> Cmdlet 上的 <em>AgeLimit</em> 參數。</p></li>
<li><p><strong>資料夾層級：</strong> <strong>Set-PublicFolder</strong> Cmdlet 上的 <em>AgeLimit</em> 參數。</p></li>
</ul>
<p></p></td>
</tr>
<tr class="odd">
<td><p>刪除項目保留</p></td>
<td><p>建議您將此項目設為用於一般信箱的相同預設值。</p></td>
<td><p>在下列層級可以進行這些設定：</p>
<ul>
<li><p><strong>組織層級：Set-OrganizationConfig Cmdlet 上的</strong> <em>DefaultPublicFolderMovedItemRetention</em> 參數。</p></li>
<li><p><strong>信箱層級：</strong> <strong>Set-Mailbox</strong> Cmdlet 上的 <em>RetainDeletedItemsFor</em>。</p></li>
<li><p><strong>資料夾層級：</strong> <strong>Set-PublicFolder</strong> Cmdlet 上的 <em>RetainDeleteItemsFor</em> 參數。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>可移轉至 Exchange 2013 公用資料夾數目上限</p></td>
<td><p>500,000</p></td>
<td><p>這是您可以從舊版的 Exchange 中的單一移轉移至 Exchange 2013 公用資料夾數目上限。如需將公用資料夾的詳細資訊，請參閱<a href="use-batch-migration-to-migrate-public-folders-to-exchange-2013-from-previous-versions-exchange-2013-help.md">使用批次移轉公用資料夾從舊版移轉至 Exchange 2013</a></p></td>
</tr>
</tbody>
</table>

