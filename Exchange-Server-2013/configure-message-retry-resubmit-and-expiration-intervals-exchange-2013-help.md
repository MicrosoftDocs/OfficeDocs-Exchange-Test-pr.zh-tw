---
title: '設定郵件重試、 重新提交、 及到期時間間隔: Exchange 2013 Help'
TOCTitle: 設定郵件重試、 重新提交、 及到期時間間隔
ms:assetid: 5420124f-aa4c-4702-b493-40a9a7edb786
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa998043(v=EXCHG.150)
ms:contentKeyID: 51409178
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定郵件重試、 重新提交、 及到期時間間隔

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-12-16_

在 Microsoft Exchange Server 2013 中，您可以在 Mailbox Server 上的傳輸服務和 Edge Transport Server 中設定郵件重試、重新提交及到期間隔。 如需這些設定的說明，請參閱[郵件重試、 重新提交、 及到期時間間隔](message-retry-resubmit-and-expiration-intervals-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：10 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「傳輸服務」和「Edge Transport Server」項目。

  - 在您安裝 Exchange 累計更新 (CU) 後，將會覆寫您在 Exchange XML 應用程式組態檔 (例如 Client Access Server 上的 web.config 檔案，或 Mailbox Server 上的 EdgeTransport.exe.config 檔案) 中任何自訂的個別伺服器設定。請務必儲存此資訊，以便安裝後能輕易地重新設定伺服器。在安裝 Exchange CU 後，您必須重新配置這些設定。

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

## 使用 EdgeTransport.exe.config 來設定佇列問題重試計數、佇列問題重試間隔、信箱傳遞佇列重試間隔及重新提交間隔前的閒置時間上限。

若要設定佇列問題重試計數、佇列問題重試間隔、信箱傳遞佇列重試間隔及重新提交間隔前的閒置時間上限，您需要在 Mailbox Server 或 Edge Transport Server 上修改 %ExchangeInstallPath%Bin\\EdgeTransport.exe.config XML 應用程式組態檔中的機碼。重新啟動 Microsoft Exchange 傳輸服務之後，就會套用您儲存至這檔案的變更。當重新啟動此服務時，會暫時中斷該伺服器上的郵件流程。

1.  在 Mailbox Server 或 Edge Transport Server 上的命令提示字元視窗中，執行以下命令以在記事本中開啟 EdgeTransport.exe.config 檔案。
    
        Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config

2.  找出下列位於 `<appSettings>` 區段的機碼。
    
        <add key="QueueGlitchRetryCount" value="<Integer>" />
        <add key="QueueGlitchRetryInterval" value="<hh:mm:ss>" />
        <add key="MailboxDeliveryQueueRetryInterval" value="<hh:mm:ss>" />
        <add key="MaxIdleTimeBeforeResubmit" value="<hh:mm:ss>" />
    
    此範例會將佇列問題重試計數變更為 6、將佇列問題重試間隔變更為 30 秒、將信箱傳遞佇列重試間隔變更為 3 分鐘，以及將重新提交間隔前的閒置時間上限變更為 6 小時。
    
        <add key="QueueGlitchRetryCount" value="6" />
        <add key="QueueGlitchRetryInterval" value="00:00:30" />
        <add key="MailboxDeliveryQueueRetryInterval" value="00:03:00" />
        <add key="MaxIdleTimeBeforeResubmit" value="6:00:00" />

3.  完成後，儲存並關閉 EdgeTransport.exe.config 檔案。

4.  執行下列命令，以重新啟動 Microsoft Exchange 傳輸服務：
    
        net stop MSExchangeTransport && net start MSExchangeTransport

## 設定暫時性失敗重試嘗試、暫時性失敗重試間隔及輸出連線失敗重試間隔

暫時性失敗重試嘗試次數指定在 `QueueGlitchRetryCount` 和 `QueueGlitchRetryInterval` 機碼所控制的連線嘗試失敗後，所嘗試的連線嘗試次數。 預設的暫時性失敗重試嘗試次數是 6。此參數的有效輸入範圍是從 0 到 15。如果將暫時性失敗重試嘗試次數設為 0，則下個連線嘗試，是由*輸出連線失敗重試間隔*所控制。

「暫時性失敗重試間隔」會指定暫時性失敗重試嘗試次數所指定之每個連線嘗試之間的間隔。 在 Mailbox Server 上的傳輸服務中，預設的暫時性失敗重試間隔是 5 分鐘。 而在 Edge Transport Server 上，預設的暫時性失敗重試間隔是 10 分鐘。

「輸出連線失敗重試間隔」會指定先前失敗之傳出連線嘗試的重試間隔。 先前失敗的連線嘗試是由「暫時性失敗重試嘗試」及「暫時性失敗重試間隔」所控制。 在 Mailbox Server 上的傳輸服務中，輸出連線失敗重試間隔的預設值是 10 分鐘。 Edge Transport Server 上的預設值是 30 分鐘。

## 使用 EAC 設定暫時性失敗重試嘗試、暫時性失敗重試間隔或輸出連線失敗重試間隔

1.  在 Exchange 系統管理中心 (EAC) 中按一下 **\[伺服器\]** \> **\[伺服器\]**，選取伺服器，按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")，然後按一下 **\[傳輸限制\]**。

2.  在 **\[重試\]** 區段中輸入 **\[輸出連線失敗重試間隔 (秒)\]**、**\[暫時性失敗重試間隔 (分鐘)\]** 或 **\[暫時性失敗重試嘗試\]** 的值。

3.  完成後，按一下 **\[儲存\]**。

## 使用命令介面設定暫時性失敗重試嘗試、暫時性失敗重試間隔及輸出連線失敗重試間隔

使用下列語法設定 Mailbox Server 上之傳輸服務中或 Edge Transport Server 上的暫時性失敗重試嘗試、暫時性失敗重試間隔及輸出連線失敗重試間隔。

    Set-TransportService <ServerIdentity> -TransientFailureRetryCount <Integer> -TransientFailureRetryInterval <hh:mm:ss> -OutboundConnectionFailureRetryInterval <dd.hh:mm:ss>

此範例會變更 Edge Transport Server Exchange01 上名為 Mailbox01: 之 Mailbox Server 上的以下各值。

  - 將暫時性失敗重試嘗試次數設定為 8。

  - 將暫時性失敗重試間隔設定為 1 分鐘。

  - 將輸出連線失敗重試間隔設定為 45 分鐘。

<!-- end list -->

    Set-TransportService Mailbox01 -TransientFailureRetryCount 8 -TransientFailureRetryInterval 00:01:00 -OutboundConnectionFailureRetryInterval 00:45:00

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在用於 Client Access Server 上之前端傳輸服務的 <strong>Set-FrontEndTransportService</strong>指令程式上，您也可以使用 <em>TransientFailureRetryCount</em> 和 <em>TransientFailureRetryInterval</em> 參數。</td>
</tr>
</tbody>
</table>


## 設定暫時性失敗重試嘗試、暫時性失敗重試間隔及輸出連線失敗重試間隔

## 使用 EAC 設定暫時性失敗重試嘗試、暫時性失敗重試間隔及輸出連線失敗重試間隔

1.  在 EAC 中按一下 **\[伺服器\]** \> **\[伺服器\]**，選取伺服器，按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")，然後按一下 **\[傳輸限制\]**。

2.  在 **\[重試\]** 區段中輸入 **\[輸出連線失敗重試間隔 (秒)\]**、**\[暫時性失敗重試間隔 (分鐘)\]** 或 **\[暫時性失敗重試嘗試\]** 的值。

3.  完成後，按一下 **\[儲存\]**。

## 使用命令介面設定暫時性失敗重試嘗試、暫時性失敗重試間隔及輸出連線失敗重試間隔

使用下列語法設定 Mailbox Server 上之傳輸服務中或 Edge Transport Server 上的暫時性失敗重試嘗試、暫時性失敗重試間隔及輸出連線失敗重試間隔。

    Set-TransportService <ServerIdentity> -TransientFailureRetryCount <Integer> -TransientFailureRetryInterval <hh:mm:ss> -OutboundConnectionFailureRetryInterval <dd.hh:mm:ss>

此範例會變更 Edge Transport Server Exchange01 上名為 Mailbox01: 之 Mailbox Server 上的以下各值。

  - 將暫時性失敗重試嘗試次數設定為 8。

  - 將暫時性失敗重試間隔設定為 1 分鐘。

  - 將輸出連線失敗重試間隔設定為 45 分鐘。

<!-- end list -->

    Set-TransportService Mailbox01 -TransientFailureRetryCount 8 -TransientFailureRetryInterval 00:01:00 -OutboundConnectionFailureRetryInterval 00:45:00

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在用於 Client Access Server 上之前端傳輸服務的 <strong>Set-FrontEndTransportService</strong>指令程式上，您也可以使用 <em>TransientFailureRetryCount</em> 和 <em>TransientFailureRetryInterval</em> 參數。</td>
</tr>
</tbody>
</table>


## 使用命令介面來設定郵件重試間隔

根據預設，郵件重試間隔會是`00:15:00`或 15 分鐘。我們建議您不要修改預設值除非 Microsoft 客戶服務與支援部門通知您這樣做。

使用以下語法來設定郵件重試間隔。

    Set-TransportService <ServerIdentity> -MessageRetryInterval <dd.hh:mm:ss>

本範例會將郵件重試間隔變更為 20 分鐘名為 Mailbox01 的 Mailbox server 上。

    Set-TransportService Mailbox01 -MessageRetryInterval 00:20:00

## 設定延遲 DSN 逾時設定

您可以使用 EAC 或命令介面來設定延遲 DSN 通知逾時間隔。 此設定僅適用於本機傳輸伺服器。 您只能使用命令介面來啟用或停用將延遲 DSN 郵件傳送給內部和外部寄件者的傳送功能。 這些設定適用於組織中的所有傳輸伺服器。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在 Exchange 2007 Hub Transport Server 上，所有 <em>ExternalDSN*</em> 及 <em>InternalDSN*</em> 參數都可在 <strong>Set-TransportServer</strong>指令程式上使用，但不能在 <strong>Set-TransportConfig</strong>指令程式上使用。 如果您的組織有任何 Exchange 2007 Hub Transport Server，則您需要在每一部 Exchange 2007 Hub Transport Server 上使用 <strong>Set-TransportServer</strong> 指令程式，來對這些值進行變更。</td>
</tr>
</tbody>
</table>


## 使用 EAC 來設定延遲 DSN 郵件通知逾時間隔

1.  在 EAC 中按一下 **\[伺服器\]** \> **\[伺服器\]**，選取伺服器，按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")，然後按一下 **\[傳輸限制\]**。

2.  在 **\[通知\]** 區段中，輸入 **\[當郵件的延遲時間超過下列時間 (小時) 時，通知寄件者\]** 的值。

3.  完成後，按一下 **\[儲存\]**。

## 使用命令介面來設定延遲 DSN 郵件通知逾時間隔

使用以下語法來設定郵件重試間隔。

    Set-TransportService <ServerIdentity> -DelayNotificationTimeout <dd.hh:mm:ss>

此範例會將名為 Mailbox01 之 Mailbox Server 上的延遲 DSN 郵件通知逾時間隔變更為 6 小時。

    Set-TransportService Mailbox01 -DelayNotificationTimeout 06:00:00

## 使用命令介面來啟用或停用將延遲 DSN 通知傳送給外部或內部郵件寄件者的傳送功能

使用下列語法來設定延遲 DSN 通知設定。

    Set-TransportConfig -ExternalDelayDSNEnabled <$true | $false> -InternalDelayDSNEnabled <$true |$false>

這個範例會禁止向外部寄件者傳送延遲 DSN 通知郵件。

    Set-TransportConfig -ExternalDelayDSNEnabled $false

這個範例會禁止向內部寄件者傳送延遲 DSN 通知郵件。

    Set-TransportConfig -InternalDelayDSNEnabled $false

## 設定郵件到期逾時間隔

## 使用 EAC 來設定郵件到期逾時間隔

1.  在 EAC 中按一下 **\[伺服器\]** \> **\[伺服器\]**，選取伺服器，按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")，然後按一下 **\[傳輸限制\]**。

2.  在 **\[郵件到期\]** 區段中，輸入 **\[提交之後的最長時間 (天)\]** 的值。

3.  完成後，按一下 **\[儲存\]**。

## 使用命令介面來設定郵件到期逾時間隔

若要設定郵件到期逾時間隔，請使用下列語法。

    Set-TransportService <ServerIdentity> -MessageExpirationTimeout <dd.hh:mm:ss>

此範例會將名為 Mailbox01 之 Exchange 伺服器上的郵件到期逾時間隔變更為 4 天。

    Set-TransportService Mailbox01 -MessageExpirationTimeout 4.00:00:00

