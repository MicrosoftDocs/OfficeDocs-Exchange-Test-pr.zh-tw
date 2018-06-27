---
title: '檢查清單： 部署保留原則: Exchange 2013 Help'
TOCTitle: 檢查清單： 部署保留原則
ms:assetid: 59e299fd-b6a8-48f5-88ae-dc20dbe32e90
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee364743(v=EXCHG.150)
ms:contentKeyID: 50473258
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 檢查清單： 部署保留原則

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

使用此檢查清單來部署MicrosoftExchange Server 2013組織中的保留原則。您開始使用此檢查清單之前，請確定您已熟悉下列主題中的概念：

  - [通訊記錄管理](messaging-records-management-exchange-2013-help.md)

  - [保留標記和保留原則](retention-tags-and-retention-policies-exchange-2013-help.md)

## 部署保留原則的檢查清單


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>完成了嗎？</th>
<th>工作</th>
<th>資源</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p> </p></td>
<td><p>評估不同使用者集合的通訊記錄管理 (MRM) 需求。</p></td>
<td><p><a href="messaging-records-management-exchange-2013-help.md">通訊記錄管理</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>判斷正在使用的 Microsoft Outlook 用戶端版本。</p></td>
<td><p>剖析位於<code>%ExchangeInstallPath%Logging\RPC Client Access</code>RPC 用戶端存取記錄檔。</p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>建立保留標記。</p></td>
<td><p><a href="create-a-retention-policy-exchange-2013-help.md">建立保留原則</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>建立保留原則。</p></td>
<td><p><a href="create-a-retention-policy-exchange-2013-help.md">建立保留原則</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>將保留標記新增至保留原則。</p></td>
<td><p><a href="add-retention-tags-to-or-remove-retention-tags-from-a-retention-policy-exchange-2013-help.md">若要保留標記中新增或移除保留標記的保留原則</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>為信箱啟用保留功能。</p></td>
<td><p><a href="place-a-mailbox-on-retention-hold-exchange-2013-help.md">就地保留信箱保留 」 狀態</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>將保留原則套用至用於測試的單一信箱。</p></td>
<td><p><a href="apply-a-retention-policy-to-mailboxes-exchange-2013-help.md">將保留原則套用至信箱</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>選用： 實作封鎖封鎖舊版Outlook用戶端的用戶端。</p></td>
<td><p><a href="configure-outlook-client-blocking-exchange-2013-help.md">設定 Outlook 用戶端通訊記錄管理的封鎖</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>開始進行使用者的通訊與訓練活動。包含在期限工作時將會處理保留原則，並移動或刪除項目。</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>將保留原則套用至其他信箱。</p></td>
<td><p><a href="apply-a-retention-policy-to-mailboxes-exchange-2013-help.md">將保留原則套用至信箱</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>提前幾天提醒使用者注意截止期限。</p></td>
<td><p>不適用</p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>在截止期限從信箱移除保留功能。</p></td>
<td><p><a href="place-a-mailbox-on-retention-hold-exchange-2013-help.md">就地保留信箱保留 」 狀態</a></p></td>
</tr>
</tbody>
</table>

