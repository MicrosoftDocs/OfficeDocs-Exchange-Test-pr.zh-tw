---
title: '設定受管理的可用性覆寫: Exchange 2013 Help'
TOCTitle: 設定受管理的可用性覆寫
ms:assetid: c8f315b3-1d5e-4ad9-8bea-9c3a4a13ebfc
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn482055(v=EXCHG.150)
ms:contentKeyID: 59889057
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定受管理的可用性覆寫

 

_**適用版本：**Exchange Online, Exchange Server 2013 SP1_

_**上次修改主題的時間：**2015-11-30_

受管理的可用性會執行持續性的探查，以偵測 Exchange 元件或其依存項目的可能問題，它也會執行復原動作，確定使用者體驗不受這些元件問題的影響。但在某些情況下，現成可用的設定可能不適合您的環境使用。您可以藉由建立覆寫來自訂受管理的可用性探查、監視器和回應程式。

有兩種類型的覆寫： 本機和全域。如其名稱暗示，本機覆寫為僅適用於伺服器建立、 和全域覆寫可用來套用至多部伺服器覆寫。針對特定期間或Exchange、 但不可同時在同一時間的特定版本可以建立這兩種類型的覆寫。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您建立的覆寫時，它不會立即生效。Microsoft Exchange狀況管理服務的組態變更檢查每隔 10 分鐘並載入任何偵測到的設定變更。如果您不想要等待，您可以重新啟動服務。</td>
</tr>
</tbody>
</table>


如需其他與受管理可用性相關的管理工作資訊，請參閱[管理健全設定與伺服器健康情況](manage-health-sets-and-server-health-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘

  - 您只能使用命令介面來執行此程序。 若要了解如何在內部部署 Exchange 組織中開啟 Exchange 管理命令介面，請參閱[開啟命令介面。](https://technet.microsoft.com/zh-tw/library/dd638134\(v=exchg.150\))。

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

## 使用Exchange 管理命令介面建立本機覆寫

若要建立本機覆寫特定的持續期間，使用下列語法。

    Add-ServerMonitoringOverride -Server <ServerName> -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <Probe | Monitor | Responder | Maintenance> -PropertyName <PropertyName> -PropertyValue <Value> -Duration <dd.hh:mm:ss>

若要建立Exchange的特定版本的本機覆寫，請使用下列語法。

    Add-ServerMonitoringOverride -Server <ServerName> -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <Probe | Monitor | Responder | Maintenance> -PropertyName <PropertyName> -PropertyValue <Value> -Version <15.01.xxxx.xxx>

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您建立的覆寫時， <em>Identity</em>參數中所使用的值會區分大小寫。</td>
</tr>
</tbody>
</table>


此範例會停用回應程式`ActiveDirectoryConnectivityConfigDCServerReboot`名 EXCH03 為 20 天的伺服器上的本機覆寫。

    Add-ServerMonitoringOverride -Server EXCH03 -Identity "AD\ActiveDirectoryConnectivityConfigDCServerReboot" -ItemType Responder -PropertyName Enabled -PropertyValue 0 -Duration 20.00:00:00

## 如何知道這是否正常運作？

若要確認您已成功建立本機覆寫，請使用**Get-ServerMonitoringOverride**指令程式來檢視本機覆寫清單：

    Get-ServerMonitoringOverride  -Server <ServerIdentity> | Format-List

覆寫應該會出現在清單中。

## 使用Exchange 管理命令介面移除本機覆寫

若要移除本機覆寫，請使用下列語法。

    Remove-ServerMonitoringOverride -Server <ServerName> -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <ExistingItemTypeValue> -PropertyName <PropertytoRemove>

本範例會移除現有的本機覆寫`ActiveDirectoryConnectivityConfigDCServerReboot`回應程式Exchange健全設定從伺服器 EXCH01 中。

    Remove-ServerMonitoringOverride -Server EXCH01 -Identity Exchange\ActiveDirectoryConnectivityConfigDCServerReboot -ItemType Responder -PropertyName Enabled

## 如何知道這是否正常運作？

若要確認您已成功移除本機覆寫，請使用**Get-ServerMonitoringOverride**指令程式來檢視本機覆寫清單：

    Get-ServerMonitoringOverride  -Server <ServerIdentity> | Format-List

已移除的覆寫應該不會出現在清單中。

## 使用Exchange 管理命令介面建立全域覆寫

若要建立全域覆寫特定的持續期間，使用下列語法。

    Add-GlobalMonitoringOverride -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <Probe | Monitor | Responder | Maintenance> -PropertyName <PropertytoOverride> -PropertyValue <NewPropertyValue> -Duration <dd.hh:mm:ss>

若要建立Exchange的特定版本的全域覆寫，請使用下列語法。

    Add-GlobalMonitoringOverride -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <Probe | Monitor | Responder | Maintenance> -PropertyName <PropertytoOverride> -PropertyValue <NewPropertyValue> -ApplyVersion <15.01.xxxx.xxx>

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您建立的覆寫時， <em>Identity</em>參數中所使用的值會區分大小寫。</td>
</tr>
</tbody>
</table>


此範例會停用`OnPremisesInboundProxy`探查 30 天的全域覆寫。

    Add-GlobalMonitoringOverride -Identity "FrontendTransport\OnPremisesInboundProxy" -ItemType Probe -PropertyName Enabled -PropertyValue 0 -Duration 30.00:00:00

此範例會停用的所有伺服器執行Exchange版 15.01.0225.042 `StorageLogicalDriveSpaceEscalate`回應的全域覆寫。

    Add-GlobalMonitoringOverride -Identity "MailboxSpace\StorageLogicalDriveSpaceEscalate" -PropertyName Enabled -PropertyValue 0 -ItemType Responder -ApplyVersion "15.01.0225.042"

## 如何知道這是否正常運作？

若要確認您已成功建立全域覆寫，請使用 **Get-GlobalMonitoringOverride** Cmdlet 檢視全域覆寫清單：

    Get-GlobalMonitoringOverride

覆寫應該會出現在清單中。

## 使用Exchange 管理命令介面移除全域覆寫

若要移除全域覆寫，請使用下列語法。

    Remove-GlobalMonitoringOverride -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <ExistingItemTypeValue> -PropertyName <OverriddenProperty>

本範例會移除現有的全域覆寫`OnPremisesInboundProxy`探查的`ExtensionAttributes`屬性`FrontEndTransport`健全設定中。

    Remove-GlobalMonitoringOverride -Identity FrontEndTransport\OnPremisesInboundProxy -ItemType Probe -PropertyName ExtensionAttributes

## 如何知道這是否正常運作？

若要確認您已成功移除全域覆寫，請使用 **Get-GlobalMonitoringOverride** Cmdlet 檢視全域覆寫清單：

    Get-GlobalMonitoringOverride

已移除的覆寫應該不會出現在清單中。

