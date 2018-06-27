---
title: '部署安全性檢查清單: Exchange 2013 Help'
TOCTitle: 部署安全性檢查清單
ms:assetid: 0cbfad59-f503-48a0-8184-6ca999d89e61
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa996026(v=EXCHG.150)
ms:contentKeyID: 50472553
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 部署安全性檢查清單

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

Microsoft Exchange Server 2013功能的設計被用來協助提升您的郵件環境的安全性。一般而言， Exchange 2013，如下列條件成立：

  - Exchange 2013 使用的帳戶擁有執行指定的工作集所需的最低權限。

  - 依預設，只會啟動必要的服務。

  - 會最小化 Exchange 物件的存取控制清單 (ACL) 權限。

  - 系統管理權限是依據對物件進行指定之修改所需的變更範圍而設定。

  - 根據預設，會加密所有內部的預設郵件路徑。

本主題將列出我們建議您採取才能安裝Microsoft Exchange強化郵件環境的步驟。我們建議您參閱此檢查清單每當您安裝新的Exchange伺服器角色。

安裝 Exchange 2013 之前，請執行下列程序。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>程序</th>
<th>完成了嗎？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>執行<a href="https://go.microsoft.com/fwlink/p/?linkid=54836">Microsoft Update</a>。</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>執行MicrosoftWindows惡意軟體移除工具。惡意軟體移除工具所含Microsoft更新。此工具的詳細資訊可以找到<a href="http://go.microsoft.com/fwlink/p/?linkid=73452">惡意軟體移除工具</a>。</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>執行<a href="https://go.microsoft.com/fwlink/p/?linkid=16526">Microsoft Baseline Security Analyzer</a>。</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>

