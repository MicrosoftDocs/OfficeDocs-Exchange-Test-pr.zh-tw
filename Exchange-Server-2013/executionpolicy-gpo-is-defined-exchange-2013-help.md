---
title: '已定義 ExecutionPolicy GPO: Exchange 2013 Help'
TOCTitle: 已定義 ExecutionPolicy GPO
ms:assetid: 63de83e2-9a6b-4f57-85b9-df445bea18dd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.powershellexecutionpolicycheckset(v=EXCHG.150)
ms:contentKeyID: 61204228
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 已定義 ExecutionPolicy GPO

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2016-12-15_

Microsoft Exchange Server 2013 安裝程式偵測到 **ExecutionPolicy** 群組原則物件 (GPO) 定義下列其中一個或兩個原則，因此無法繼續：

  - **MachinePolicy**

  - **UserPolicy**

原則的定義方式並不重要。它們的定義與否才重要。

當您執行 Exchange 2013 安裝程式時，Exchange 會停止並停用 Windows Management Instrumentation (WMI) 服務。定義上述任一個原則時，需要啟用 WMI 服務，才能執行 Windows PowerShell 指令碼。如果已定義原則並停止 WMI 服務，則安裝程式會失敗，而且伺服器的狀態會不一致。

若要允許安裝程式繼續，您需要暫時移除 **ExecutionPolicy** GPO 中的任何 **MachinePolicy** 或 **UserPolicy** 定義。

如需如何移除**ExecutionPolicy** GPO 中的任何**MachinePolicy**或**UserPolicy**定義的資訊，請參閱[知識庫文章 KB981474](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=981474)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>此知識庫文章是針對 Exchange 2010 撰寫而成，但是它也適用於 Exchange 2013 累計更新和服務套件。</td>
</tr>
</tbody>
</table>


有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

找到您要的資訊了嗎？請撥冗[提供您的意見](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac)讓我們知道您需要什麼資訊。

