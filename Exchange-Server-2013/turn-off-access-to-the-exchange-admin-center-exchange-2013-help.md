---
title: '關閉 Exchange 系統管理中心存取: Exchange 2013 Help'
TOCTitle: 關閉 Exchange 系統管理中心存取
ms:assetid: 49f4fa77-1722-4703-81c9-8724ae0334fb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ218639(v=EXCHG.150)
ms:contentKeyID: 50473179
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 關閉 Exchange 系統管理中心存取

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2013-05-20_

基於安全性考量，某些組織可能會想要限制存取 Exchange 系統管理中心 (EAC) 來自網際網路的使用者。此程序將示範如何關閉 eac 的存取。此程序不會防止使用者存取 Outlook Web App 中的選項。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>此程序會停用完全步驟所套用之 CAS 伺服器上的 EAC 中系統管理員存取權。如果您啟用 EAC 管理員供內部使用者，您應該安裝個別的 CAS 伺服器並將其設定為僅處理內部要求使用下列命令：<br />
<code>Set-ECPVirtualDirectory -Identity &quot;InternalCAS\ecp (default web site)&quot; -AdminEnabled $True</code></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>此程序僅會套用至 Exchange Server 2013 的內部部署。</td>
</tr>
</tbody>
</table>


## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [Exchange 及命令介面基礎結構權限](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)主題中的「Exchange 系統管理中心連線」項目。

  - 您無法使用 EAC 來執行此程序。您必須使用命令介面。

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


## 使用命令介面來關閉網際網路至 EAC 的存取

此範例會關閉伺服器 CAS01 上的 EAC 存取。

    Set-ECPVirtualDirectory -Identity "CAS01\ecp (default web site)" -AdminEnabled $false

如需詳細的語法及參數資訊，請參閱 [Set-EcpVirtualDirectory](https://technet.microsoft.com/zh-tw/library/dd297991\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要確認您是否已成功關閉 EAC 的存取，請執行下列步驟：

1.  使用網際網路瀏覽器，輸入您的組織內部或外部 URL 存取 Outlook Web App 但取代**/ecp/owa**識別碼。例如，如果您存取 Outlook Web App 的外部 URL 為 https://primary.tailspintoys.com/owa，使用 https://primary.tailspintoys.com/ecp。

2.  若存取已關閉，您將會收到 **\[404 – website not found\]** 錯誤。

