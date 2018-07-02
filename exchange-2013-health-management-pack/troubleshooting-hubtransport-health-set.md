---
title: 疑難排解 HubTransport 健康情況設定
TOCTitle: 疑難排解 HubTransport 健康情況設定
ms:assetid: e3932ce3-836c-4230-9f64-63af1b704d79
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/ms.exch.scom.hubtransport(v=EXCHG.150)
ms:contentKeyID: 54652650
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 疑難排解 HubTransport 健康情況設定

 

_**適用版本：** Exchange Server 2013_

_**上次修改主題的時間：** 2015-03-09_

**HubTransport**健全設定監視信箱伺服器上傳輸管線負責在組織中的路由傳送郵件的整體狀況。如需詳細資訊，請參閱[郵件流程](https://technet.microsoft.com/zh-tw/library/aa996349\(v=exchg.150\))。

如果您收到警示，指出**HubTransport**健全設定的狀況不良，這會指出有問題可能無法從正在路由傳送，傳遞出的郵件。

## 說明

**HubTransport**服務是使用下列探查與監視器來監視。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Probe</th>
<th>健全設定</th>
<th>關聯的監視器</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ActiveQueueDrainFailureProbe</p></td>
<td><p>HubTransport</p></td>
<td><p>ActiveQueueDrainFailureMonitor</p></td>
</tr>
<tr class="even">
<td><p>DiagnosticsAggregationLocalSnapshotProbe</p></td>
<td><p>HubTransport</p></td>
<td><p>DiagnosticsAggregationLocalSnapshotMonitor</p></td>
</tr>
<tr class="odd">
<td><p>DiagnosticsAggregationWebServiceProbe</p></td>
<td><p>HubTransport</p></td>
<td><p>DiagnosticsAggregationWebServiceMonitor</p></td>
</tr>
<tr class="even">
<td><p>HubAvailabilityProbe</p></td>
<td><p>HubTransport</p></td>
<td><p>HubAvailabilityMonitor</p></td>
</tr>
<tr class="odd">
<td><p>HubTransportServiceRunning</p></td>
<td><p>HubTransport</p></td>
<td><p>HubTransportServiceRunningMonitor</p></td>
</tr>
<tr class="even">
<td><p>ShadowQueueDiscardDrainFailureProbe</p></td>
<td><p>HubTransport</p></td>
<td><p>ShadowQueueDiscardDrainFailureMonitor</p></td>
</tr>
<tr class="odd">
<td><p>ThrottlingServiceRunning</p></td>
<td><p>HubTransport</p></td>
<td><p>ThrottlingServiceRunningMonitor</p></td>
</tr>
<tr class="even">
<td><p>TransportEdgeSync.Service.Probe</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportEdgeSync.Service.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>TransportLogSearchRunningProbe</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportLogSearchRunningMonitor</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>BootloaderOutstandingItemsTriggerMonitor</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>CrashEvent.edgetransport</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>CrashEvent.msexchangethrottling</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>CrashEvent.msexchangetransport</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>CrashEvent.msexchangetransportlogsearch</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>EdgeTransportBackpressureSustainedTimeMonitor</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>FederatedDecryptionAgentFailedToXDecryptMonitor</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>HubTransport.ServiceInconsistentState.Monitor</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>IsMemberOfResolverExpandedGroupsCacheSizeMonitor</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>IsMemberOfResolverResolvedGroupsCacheSizeMonitor</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>Messages.failed.to.be.made.redundant.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>MessagesDeferredDuringCategorizationMonitor</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>MessageTrackingLogsDirQuotaMonitor</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>PrivateWorkingSetError.edgetransport</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>PrivateWorkingSetError.msexchahangetransportlogsearch</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>PrivateWorkingSetError.msexchangethrottling</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>PrivateWorkingSetError.msexchangetransport</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>PrivateWorkingSetWarning.edgetransport</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>PrivateWorkingSetWarning.msexchangethrottling</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>PrivateWorkingSetWarning.msexchangetransport</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>PrivateWorkingSetWarning.msexchangetransportlogsearch</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>ProcessProcessorTimeError.edgetransport</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>ProcessProcessorTimeError.msexchangethrottling</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>ProcessProcessorTimeError.msexchangetransport</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>ProcessProcessorTimeError.msexchangetransportlogsearch</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>ProcessProcessorTimeWarning.edgetransport</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>ProcessProcessorTimeWarning.msexchangethrottling</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>ProcessProcessorTimeWarning.msexchangetransport</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>ProcessProcessorTimeWarning.msexchangetransportlogsearch</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>QueueExternalAggregateMonitor</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>QueueInternalAggregateMonitor</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>QueueInternalAggregateNormalPriorityMonitor</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>QueueInternalHubRetryMonitor</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>QueueInternalHubRetryNormalPriorityMonitor</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>QueueMailboxRetryMonitor</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>QueueNonSMTPRetryMonitor</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>RuleEvaluationFailureEventLogMonitor</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>RuleEvaluationIgnoredFailureEventLogMonitor</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>RuleEvaluationIgnoredFipsFailureEventLogMonitor</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>RuleEvaluationSmallScaleFailureEventLogMonitor</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>RuleEvaluationSmallScaleFipsFailureEventLogMonitor</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>RuleExcessiveForkingEventLogMonitor</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>RuleLoadFailureEventLogMonitor</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>RuleLoadSmallScaleFailureEventLogMonitor</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>SmtpProxyEhloOptionsDoNotMatchContinueProxyingMonitor</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>SubmissionQueueMonitor</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>TlsDomainClientCertificateSubjectMismatchMonitor</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>Total.Shadow.Queue.Length.Above.Threshold.Monitor</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>TotalE2ELatencyHighForMSExchangeTransportMonitor</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>TotalE2ELatencyLowForMSExchangeTransportMonitor</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>TotalE2ELatencyNormalForMSExchangeTransportMonitor</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.CatExpiry.Monitor</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.Critical.Storage.Recovery.Failed.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.DatabaseMoved.Monitor</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.DomainSecureCert.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.DomainSecureCertAuth.Monitor</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.DomainSecureServerCertFailed.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.DomainSecureServerDomainCertFailed.Monitor</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.FailedToCreatePickupDirectory.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.InvalidAcceptedDomain.Monitor</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.LowDiskSpace.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.Messages.Completing.Categorization.Monitor</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.NDRForUnrestrictedLargeDL.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.PickupDelete.Monitor</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.PickupIsBadmailingFile.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.SendConn.AuthKerb.Monitor</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.SendConnAuth.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.SendConnTLS.Monitor</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.ServerCertExpireSoon.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.ServerCertMismatch.Monitor</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.ServiceStartError.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.SmtpSendDirectTrustFailed.Monitor</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.TemplateDoesNotExist.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.TLSValidate.Monitor</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.UnknownTemplateInPublishingLicense.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportCategorizerJobAvailabilityMonitor</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportDatabaseCorruptMonitor</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportDeliveryFailures544Monitor</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportDeliveryFailuresDeliveryStoreDriver520Monitor</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportLogGenerationCheckpointDepthMonitor</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportLogSearchLogPathInvalidMonitor</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportMaxLocalLoopCountMonitor</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportPickupReadMonitor</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportPoisonMessageMonitor</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportRejectingMessageSubmissionsMonitor</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportServerCertPersonalStoreMonitor</p></td>
</tr>
<tr class="even">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>UnreachableQueueMonitor</p></td>
</tr>
<tr class="odd">
<td><p>無 （通知或] 核取）</p></td>
<td><p>HubTransport</p></td>
<td><p>XProxyToTransientInvalidArgumentsMonitor</p></td>
</tr>
</tbody>
</table>


如需探查與監視器的詳細資訊，請參閱[伺服器健康狀況與效能](https://technet.microsoft.com/zh-tw/library/jj150551\(v=exchg.150\))。

## 使用者動作

有可能服務復原之後則發出警示。因此，當您會收到通知，指定**HubTransport**健全設定為不健康，先確認問題仍然存在。如果問題不存在，執行下列一節所述的適當的復原動作。

## 確認問題

1.  識別警示中提供的健全設定名稱與伺服器名稱。

2.  郵件的詳細資訊提供的確切原因的警示的資訊。在大多數情況下，郵件詳細資料會提供足夠來協助識別根本原因的疑難排解資訊。如果不清楚郵件的詳細資訊，請執行下列動作：
    
    1.  開啟 Exchange 管理命令介面，然後執行下列命令，以擷取發出警示之健全設定的詳細資料：
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        例如，若要擷取**HubTransport**健全設定詳細 mailbox1.contoso.com，執行下列命令：
        
            Get-ServerHealth mailbox1.contoso.com | ?{$_.HealthSetName -eq "HubTransport"}
    
    2.  檢閱命令的輸出傳送至決定顯示器回報的錯誤。發出警示監視器**AlertValue**值會是**Unhealthy**。
    
    3.  請為不健康狀態監視重新執行相關聯的探查。請參閱尋找相關聯的探查 \[[說明](troubleshooting-activesync-health-set.md)\] 區段中的表格。若要這樣做，執行下列命令：
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        例如，假設失敗監視是**ActiveQueueDrainFailureMonitor**。相關聯的監視探查是**ActiveQueueDrainFailureProbe**。若要執行此探查 mailbox1.contoso.com 上，執行下列命令：
        
            Invoke-MonitoringProbe HubTransport\ActiveQueueDrainFailureProbe -Server mailbox1.contoso.com | Format-List
    
    4.  命令輸出中，請檢閱"結果 」 一節的探查。如果值為**成功**，問題是暫時性錯誤，並不存在。

