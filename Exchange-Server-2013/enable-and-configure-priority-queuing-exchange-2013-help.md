---
title: '啟用並設定優先順序佇列: Exchange 2013 Help'
TOCTitle: 啟用並設定優先順序佇列
ms:assetid: 1975d85d-2f1d-4852-8d19-e74ba4ba3853
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ891104(v=EXCHG.150)
ms:contentKeyID: 51409160
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟用並設定優先順序佇列

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-12-16_

*優先順序佇列*是 Microsoft Exchange Server 2013可讓已在 Microsoft Outlook 或Outlook Web Access影響信箱伺服器上的傳輸服務處理郵件的寄件者的郵件優先順序的功能。啟用優先順序佇列時，高優先順序的郵件傳送到其目的地之前一般優先順序的郵件和一般優先順序的郵件傳送到其目的地之前低優先順序的郵件。如需詳細資訊，請參閱[優先順序佇列](priority-queuing-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：15 分鐘

  - Exchange 權限無法套用於此主題的程序。在 Exchange 伺服器的作業系統中執行這些程序。

  - 在重新啟動 Microsoft Exchange 傳輸服務之後，就會套用您儲存至 EdgeTransport.exe.config 應用程式組態檔的變更。

  - 重新啟動 Microsoft Exchange 傳輸服務時，會暫時中斷該伺服器上的郵件流程。

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


## 使用命令提示字元來啟用及設定 EdgeTransport.exe.config 檔案中的優先佇列

1.  在命令提示字元視窗中執行下列命令，即可在記事本中開啟 EdgeTransport.exe.config 應用程式組態檔：
    
        Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config

2.  在 `<appSettings>` 區段中尋找下列機碼。
    
        <add key="PriorityQueuingEnabled" value="false" />
        <add key="MaxPerDomainHighPriorityConnections" value="3" />
        <add key="MaxPerDomainNormalPriorityConnections" value="15" />
        <add key="MaxPerDomainLowPriorityConnections" value="2" />
        <add key="HighPriorityMessageExpirationTimeout" value="8:00:00" />
        <add key="NormalPriorityMessageExpirationTimeout" value="2.00:00:00" />
        <add key="LowPriorityMessageExpirationTimeout" value="2.00:00:00" />
        <add key="HighPriorityDelayNotificationTimeout" value="00:30:00" />
        <add key="NormalPriorityDelayNotificationTimeout" value="4:00:00" />
        <add key="LowPriorityDelayNotificationTimeout" value="8:00:00" />
        <add key="MaxHighPriorityMessageSize" value="250KB" />
    
    若要在 Mailbox Server 的傳輸服務中啟用優先佇列，請使用下列值：
    
        <add key="PriorityQueuingEnabled" value="true" />
    
    設定剩餘的優先佇列值，或讓它們沿用預設值。

3.  完成後，儲存並關閉 EdgeTransport.exe.config 檔案。

4.  執行下列命令，以重新啟動 Microsoft Exchange 傳輸服務：
    
        net stop MSExchangeTransport && net start MSExchangeTransport

## 如何才能了解這是否正常運作？

若要確認您是否已成功啟用並設定優先佇列，請執行下列動作：

1.  確認 EdgeTransport.exe.config 檔案中的 **PriorityQueueinEnabled** 機碼具有 `"true"` 值。

2.  使用 Outlook 建立大於 **MaxHighPriorityMessageSize** 機碼所指定值的高優先順序測試郵件，並確認郵件送達情形和正常優先順序的郵件沒有兩樣。

3.  嘗試驗證更高的優先順序郵件送達之前傳送至相同的收件者或目的地的較低優先順序郵件。您可以嘗試使用多個信箱傳送多個、 類似測試同時郵件具有不同的優先順序值到相同的收件者。

