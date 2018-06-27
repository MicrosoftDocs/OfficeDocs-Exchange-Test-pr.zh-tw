---
title: '檢查清單： 執行 Exchange 2013 全新安裝: Exchange 2013 Help'
TOCTitle: 檢查清單： 執行 Exchange 2013 全新安裝
ms:assetid: f70d9dd3-7370-472e-b05e-1ea1671272b2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ff805042(v=EXCHG.150)
ms:contentKeyID: 50474619
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 檢查清單： 執行 Exchange 2013 全新安裝

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

使用此檢查清單可部署 Microsoft Exchange Server 2013。開始使用此檢查清單之前，請確定您熟悉以下討論的概念：

  - [規劃及部署](planning-and-deployment-for-exchange-2013-installation-instructions.md)

  - [部署安全性檢查清單](deployment-security-checklist-exchange-2013-help.md)

這是一般性的檢查清單，針對一般案例提供指引。

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


## Exchange 2013 全新安裝的檢查清單


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
<td><p>1. 閱讀版本資訊。</p></td>
<td><p><a href="release-notes-for-exchange-2013-exchange-2013-help.md">Exchange 2013 版本資訊</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>2. 確認系統需求。</p></td>
<td><p><a href="exchange-2013-system-requirements-exchange-2013-help.md">Exchange 2013 系統需求</a></p></td>
</tr>
<tr class="even">
<td> </td>
<td><p>3. 確認已完成必要步驟。</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 必要條件</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>4. 設定脫離的命名空間。</p>
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
<td><p><a href="disjoint-namespace-scenarios-exchange-2013-help.md">斷續的命名空間案例</a></p></td>
</tr>
<tr class="even">
<td> </td>
<td><p>5. 安裝 Mailbox server role。</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">使用安裝精靈安裝 Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>6. 安裝 Client Access server role。</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">使用安裝精靈安裝 Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>7. 安裝 Edge Transport server role。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>此步驟是選用的。只有在想要安裝 Edge Transport Server 時才需要此步驟。如需詳細資訊，請參閱<a href="edge-transport-servers-exchange-2013-help.md">Edge Transport Server</a>。</td>
</tr>
</tbody>
</table>

</td>
<td><p><a href="install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md">使用設定精靈安裝 Exchange 2013 Edge Transport role</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>8. 建立 EdgeSync 訂閱。</p>
<p>此步驟是選用的。只有在已安裝 Edge Transport Server，而且想要在 Edge Transport Server 與 Hub Transport Server 之間設定 EdgeSync 訂閱時才需要此步驟。如需詳細資訊，請參閱<a href="edge-subscriptions-exchange-2013-help.md">Edge 訂閱</a>。</p></td>
<td><p><a href="configure-internet-mail-flow-through-a-subscribed-edge-transport-server-exchange-2013-help.md">透過訂閱的 Edge Transport Server 設定網際網路郵件流程</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>9. 設定傳輸。</p></td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 1: Create a Send connector</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>10. 新增公認的網域。</p></td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 2: Add additional accepted domains</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>11. 設定電子郵件地址原則。</p></td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 3: Configure the default email address policy</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>12. 設定虛擬目錄的設定值，包括離線通訊錄、Exchange Web 服務、Exchange 系統管理中心 (EAC)、Outlook Web App 和 Exchange ActiveSync 虛擬目錄。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您要使用 Exchange Web 服務、Outlook 無所不在或離線通訊錄，就需要執行此步驟。如果您需要變更 EAC、Outlook Web App 或 Exchange ActiveSync 的任何預設設定，則可能也需要此步驟。</td>
</tr>
</tbody>
</table>

</td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 4: Configure external URLs</a></p>
<p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 5: Configure internal URLs</a></p></td>
</tr>
<tr class="even">
<td> </td>
<td><p>13. 在用戶端存取伺服器上新增數位憑證。</p></td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 6: Configure an SSL certificate</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>14. 設定整合通訊。</p>
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
<td><p><a href="deploying-voice-mail-and-um-exchange-2013-help.md">部署語音信箱和 UM</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>15. 設定額外的「整合通訊」與 Lync Server 設定。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>此步驟是選用的。只有在您於組織中設定「整合通訊」並希望與 Lync Server 整合時才需要。</td>
</tr>
</tbody>
</table>

</td>
<td><p><a href="deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md">部署 Exchange 2013 UM 和 Lync Server 概觀 （英文）</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>16. 安裝後期工作。</p></td>
<td><p><a href="exchange-2013-post-installation-tasks-exchange-2013-help.md">Exchange 2013 後續安裝工作</a></p></td>
</tr>
</tbody>
</table>

