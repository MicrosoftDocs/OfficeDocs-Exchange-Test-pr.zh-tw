---
title: '設定 UM 以搭配 Lync Server: Exchange 2013 Help'
TOCTitle: 設定 UM 以搭配 Lync Server
ms:assetid: 29bdddbf-75d5-4c92-988e-c8506ecc7a1c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ966276(v=EXCHG.150)
ms:contentKeyID: 52062529
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定 UM 以搭配 Lync Server

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-06-11_

當您要整合 Microsoft Lync Server 與 Exchange 整合通訊 (UM) 時，您必須在命令介面中執行 ExchUcUtil.ps1 指令碼。ExchUcUtil.ps1 指令碼可執行下列作業：

  - 建立每個 Lync Server 集區的 UM IP 閘道。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>ExchUcUtil.ps1 指令碼可建立一或多個 UM IP 閘道。您必須在除了指令碼所建立的一個閘道以外的所有 UM IP 閘道上，停用撥出電話。這包括在已於執行指令碼之前就建立的 UM IP 閘道上，停用撥出電話。若要在 UM IP 閘道上停用撥出電話，請參閱<a href="disable-outgoing-calls-on-um-ip-gateways-exchange-2013-help.md">停用 UM IP 閘道器上的撥出電話</a>。</td>
    </tr>
    </tbody>
    </table>


  - 為每個 UM IP 閘道建立一個 UM 群組搜尋。每個群組搜尋的引導識別碼可指定與 UM IP 閘道相關聯的 Lync Server 前端集區或 Standard Edition 伺服器所使用的 UM SIP URI 撥號對應表。

  - 授與權限給 Lync Server 來讀取 Active Directory UM 容器物件，例如 UM 撥號對應表、自動語音應答、UM IP 閘道及 UM 群組搜尋。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>每個 UM 樹系必須設定為信任部署了 Lync Server 2013 的樹系，而部署了 Lync Server 2013 的樹系必須設定為信任每個 UM 樹系。如果在多個樹系中安裝了 Exchange UM，則必須為每個 UM 樹系執行 Exchange Server 整合步驟，否則必須指定 Lync Server 網域。例如，<em>ExchUcUtil.ps1 –Forest:&lt;lync-domain-controller-fqdn&gt;</em>。</td>
</tr>
</tbody>
</table>


如需與整合 Lync Server 和整合通訊相關的其他管理工作，請參閱[部署 Exchange 2013 UM 和 Lync Server 概觀 （英文）](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：2 分鐘。

  - [Exchange 2013 指令程式](https://technet.microsoft.com/zh-tw/library/bb124413\(v=exchg.150\)) 主題中的 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱「權限 Cmdlet」項目。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 使用命令介面來執行 ExchUcUtil.ps1 指令碼

請在組織中與 Microsoft Lync Server 位於相同拓撲的任何 Exchange 伺服器上，執行 ExchUcUtil.ps1 指令碼。您可以在 Mailbox Server 中使用命令介面來執行指令碼，或者您可以在 Client Access Server 上使用遠端 Windows PowerShell 來執行指令碼。如果您在組織中的 Client Access Server 上執行指令碼，則 Client Access Server 會將遠端 Windows PowerShell 工作階段，Proxy 處理至組織中的 Mailbox Server。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ExchUcUtil.ps1 指令碼可建立一或多個 UM IP 閘道。您必須在除了指令碼所建立的一個閘道以外的所有 UM IP 閘道上，停用撥出電話。這包括在已於執行指令碼之前就建立的 UM IP 閘道上，停用撥出電話。若要在 UM IP 閘道上停用撥出電話，請參閱<a href="disable-outgoing-calls-on-um-ip-gateways-exchange-2013-help.md">停用 UM IP 閘道器上的撥出電話</a>。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您必須具備「Exchange 組織管理」角色的權限或屬於 Exchange Organization Administrators 安全性群組的成員，才能執行此指令碼。</td>
</tr>
</tbody>
</table>


1.  開啟 \[Exchange 管理命令介面\]。

2.  在 `C:\Windows\System32` 提示中，輸入 **cd \&quot;\<磁碟機代號\>\\Program Files\\Microsoft\\Exchange Server\\V15\\Scripts\>.ExchUcUtil.ps1\&quot;**，然後按 Enter。

## 如何知道這是否正常運作？

若要確認是否已成功完成 ExchUcUtul.ps1 指令碼，請執行下列作業：

  - 使用 **Get-UMIPGateway** Cmdlet 或 EAC 來檢視所建立的新 UM IP 閘道。

  - 使用 **Get-UMHuntGroup** Cmdlet 或 EAC 來檢視所建立的新 UM 群組搜尋。

