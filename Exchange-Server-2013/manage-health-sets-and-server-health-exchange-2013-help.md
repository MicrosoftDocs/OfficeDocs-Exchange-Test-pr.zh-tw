---
title: '管理健全設定與伺服器健康情況: Exchange 2013 Help'
TOCTitle: 管理健全設定與伺服器健康情況
ms:assetid: a4f84312-6cfa-4f17-9707-676aadab1143
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn482054(v=EXCHG.150)
ms:contentKeyID: 59889056
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理健全設定與伺服器健康情況

 

_**適用版本：**Exchange Online, Exchange Server 2013 SP1_

_**上次修改主題的時間：**2013-12-02_

您可以使用內建的健全狀況報告 Cmdlet 執行各種與受管理可用性相關的工作，例如：

  - 檢視一部或一組伺服器的健全狀況

  - 檢視健全設定清單

  - 檢視與特定健全設定相關聯之探查、監視器及回應程式的清單

  - 檢視監視器及其目前健全狀況的清單

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：2 分鐘

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

## 檢視伺服器健全狀況

您可以使用命令介面來取得執行 Exchange 2013 的伺服器的健全狀況摘要。

## 使用命令介面檢視伺服器健全狀況

執行下列任一個命令，檢視執行 Exchange 2013 的伺服器的健全設定和健全狀況資訊。

    Get-HealthReport -Identity <ServerName>

    Get-ServerHealth -Identity <ServerName> | Format-Table Server,CurrentHealthSetState,Name,HealthSetName,AlertValue,HealthGroupName -Auto

執行下列任何一個命令，檢視執行 Exchange 2013 的伺服器或資料庫可用性群組的健全設定。

    Get-ExchangeServer | Get-HealthReport -RollupGroup

    Get-ExchangeServer | Get-HealthReport -RollupGroup -HealthSetName <HealthSet>

    (Get-DatabaseAvailabiltyGroup <DAGName>).Servers | Get-HealthReport -RollupGroup

## 檢視健全設定清單

健全設定是元件的一組探查、監視器及回應程式，可用來判斷元件健全與否。您可以使用命令介面檢視執行 Exchange 2013 的伺服器的健全設定清單。

## 使用命令介面檢視健全設定清單

執行下列命令，檢視執行 Exchange 2013 的伺服器的健全設定。

    Get-HealthReport -Server <ServerName>

## 檢視健全設定的探查、監視器和回應程式

健全設定是元件的一組探查、監視器及回應程式，可用來判斷元件健全與否。您可以使用命令介面檢視與執行 Exchange 2013 的伺服器的健全設定相關聯的探查、監視器及回應程式的清單。

## 使用命令介面檢視健全設定的探查、監視器和回應程式

執行下列命令檢視與執行 Exchange 2013 的伺服器的健全設定相關聯的探查、監視器及回應程式。

    Get-MonitoringItemIdentity -Server <ServerName> -Identity <HealthSetName> | Format-Table Identity,ItemType,Name -Auto

## 檢視監視器及其目前健全狀況的清單

監視器的健全狀況是使用健全設定中最不理想的監視器來進行報告。您可以檢視健全設定的詳細資料，查看哪些監視器健全，哪些監視器不健全。

## 使用命令介面檢視監視器及其目前健全狀況的清單

執行下列命令檢視執行 Exchange 2013 的伺服器的監視器及其目前健全狀況的清單。

    Get-ServerHealth -HealthSet <HealthSetName> -Server <ServerName> | Format-Table Name, AlertValue -Auto

