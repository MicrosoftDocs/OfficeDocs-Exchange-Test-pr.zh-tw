---
title: '檢查清單：從 Exchange 2010 升級: Exchange 2013 Help'
TOCTitle: 檢查清單：從 Exchange 2010 升級
ms:assetid: 06c1045a-5fcf-4e24-a901-1a979302fb8d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee332309(v=EXCHG.150)
ms:contentKeyID: 51409151
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 檢查清單：從 Exchange 2010 升級

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-07_

從 Microsoft Exchange 2010升級至Exchange 2013使用此檢查清單。您開始使用此檢查清單之前，請確定您已熟悉中討論的概念：

  - [規劃及部署](planning-and-deployment-for-exchange-2013-installation-instructions.md)

  - [Exchange 2013 的新功能](what-s-new-in-exchange-2013-exchange-2013-help.md)

這是一般性的檢查清單，針對一般升級案例提供指引。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Exchange Server 部署助理提供您如何部署 Exchange Server 的自訂逐步指導。部署助理可協助您部署 Exchange Server 2013 的全新安裝、將舊版產品升級至 Exchange 2013，或是設定 Exchange 2013 與 Exchange Online 的混合式部署。若要深入了解，請參閱<a href="exchange-server-deployment-assistant-exchange-2013-help.md">Exchange Server 部署助理</a>。</td>
</tr>
</tbody>
</table>


## 從 Exchange 2010 升級至 Exchange 2013 的檢查清單


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>完成了嗎？</p></td>
<td><p>工作</p></td>
<td><p>主題</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>1. 閱讀版本資訊。</p></td>
<td><p><a href="release-notes-for-exchange-2013-exchange-2013-help.md">Exchange 2013 版本資訊</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>2. 確認系統需求</p></td>
<td><p><a href="exchange-2013-system-requirements-exchange-2013-help.md">Exchange 2013 系統需求</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>3. 確認已完成必要步驟</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 必要條件</a></p>
<p><a href="deployment-security-checklist-exchange-2013-help.md">部署安全性檢查清單</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>4. 設定脫離的命名空間</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>此步驟是選用的。只有在組織執行脫離的命名空間才需要。</td>
</tr>
</tbody>
</table>

</td>
<td><p><a href="configure-the-dns-suffix-search-list-for-a-disjoint-namespace-exchange-2013-help.md">設定脫離的命名空間的 DNS 尾碼搜尋清單</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>5. 為所有 Exchange 2010 信箱資料庫選取一個離線通訊錄。</p></td>
<td><p><a href="manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md">Set mailbox database properties</a> 於<a href="manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md">管理 Exchange 2013 中的信箱資料庫</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>6. 安裝 Exchange 2013</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">使用安裝精靈安裝 Exchange 2013</a></p>
<p><a href="install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md">使用設定精靈安裝 Exchange 2013 Edge Transport role</a></p>
<p><a href="verify-an-exchange-2013-installation-exchange-2013-help.md">確認 Exchange 2013 安裝</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>7. 建立 Exchange 2013 信箱</p></td>
<td><p><a href="create-user-mailboxes-exchange-2013-help.md">建立使用者信箱</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>8. 設定 Exchange 相關虛擬目錄</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您要使用 Exchange Web 服務、Outlook 無所不在或離線通訊錄，就需要執行此步驟。如果您需要變更 Exchange 控制台、Microsoft Office Outlook Web App 或 Exchange ActiveSync 的任何預設設定，也可能需要此步驟。<br />
</td>
</tr>
</tbody>
</table>

</td>
<td><p><a href="exchange-2013-client-access-server-configuration-exchange-2013-help.md">Exchange 2013 用戶端存取伺服器組態</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>9. 在 Client Access server 上新增數位憑證</p></td>
<td><p><a href="digital-certificates-and-ssl-exchange-2013-help.md">數位憑證和 SSL</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>10. 移動仲裁信箱</p></td>
<td><p><a href="move-the-exchange-2010-system-mailbox-to-exchange-2013-exchange-2013-help.md">將 Exchange 2010 系統信箱移至 Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>11. 設定整合通訊</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>此步驟是選用的。只有在您想在組織中使用整合通訊時才需要。</td>
</tr>
</tbody>
</table>

</td>
<td><p><a href="upgrade-exchange-2010-um-to-exchange-2013-um-exchange-2013-help.md">將 Exchange 2010 UM 升級至 Exchange 2013 UM</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>12. 設定 Edge Transport Server</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>此步驟是選用的。只有在組織正在使用 Edge Transport Server 時才需要。</td>
</tr>
</tbody>
</table>

</td>
<td><p><a href="configure-internet-mail-flow-through-a-subscribed-edge-transport-server-exchange-2013-help.md">透過訂閱的 Edge Transport Server 設定網際網路郵件流程</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>13. 啟用和設定 Outlook 無所不在</p></td>
<td><p><a href="outlook-anywhere-exchange-2013-help.md">Outlook 無所不在</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>14. 設定服務連線點</p></td>
<td><p><a href="exchange-2013-client-access-server-configuration-exchange-2013-help.md">Exchange 2013 用戶端存取伺服器組態</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>15. 設定 DNS 記錄</p></td>
<td><p><a href="https://technet.microsoft.com/zh-tw/library/dn307232(v=exchg.150)">針對 Exchange 2010 多部伺服器安裝設定 DNS 記錄</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>16.將信箱移從Exchange 2010至Exchange 2013</p></td>
<td><p><a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">在 Exchange 2013 移動信箱</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>17. 將公用資料夾資料從 Exchange 2013 移至 Exchange 2013</p></td>
<td><p><a href="public-folders-exchange-2013-help.md">公用資料夾</a></p>
<p><a href="https://technet.microsoft.com/zh-tw/library/jj150486(v=exchg.150)">使用序列遷移公用資料夾從舊版移轉至 Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>18. 安裝後期工作</p></td>
<td><p><a href="exchange-2013-post-installation-tasks-exchange-2013-help.md">Exchange 2013 後續安裝工作</a></p></td>
</tr>
</tbody>
</table>

