---
title: '容錯移轉叢集的命令介面視窗功能不會安裝: Exchange 2013 Help'
TOCTitle: 容錯移轉叢集的命令介面視窗功能不會安裝
ms:assetid: 0d839514-5ab7-497d-8945-41392b4c3980
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.setupreadiness.rsatclusteringcmdinterfaceinstalled(v=EXCHG.150)
ms:contentKeyID: 51409153
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 容錯移轉叢集的命令介面視窗功能不會安裝

 

_**適用版本：**Exchange Server_

_**上次修改主題的時間：**2014-12-03_

因為本機電腦遺漏必要的 Windows 功能，所以 Microsoft Exchange Server 2013 安裝程式無法繼續。您必須先安裝此 Windows 功能，Exchange 2013 安裝程式才能繼續。

Exchange 2013安裝程式需要**容錯移轉叢集命令介面**Windows 功能安裝在電腦上才能繼續進行安裝。

依下列方式在這部電腦上安裝 Windows 功能。若此功能需要重新開啟才可完成安裝，需離開 Exchange 2013 安裝程式、重新開機然後再次啟動安裝程式。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>可能需要先安裝其他 Windows 功能或更新，Exchange 2013 安裝程式才能繼續。如需必要 Windows 功能和更新的完整清單，請查看 <a href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 必要條件</a>。</td>
</tr>
</tbody>
</table>


1.  本機電腦上開啟 Windows PowerShell。

2.  執行下列命令以安裝必要的 Windows 功能。
    
        Install-WindowsFeature RSAT-Clustering-CmdInterface

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

找到您要的資訊了嗎？請撥冗[提供您的意見](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac)讓我們知道您需要什麼資訊。

