---
title: '設定路由表格記錄: Exchange 2013 Help'
TOCTitle: 設定路由表格記錄
ms:assetid: 7184f8f7-4eb8-468a-aafe-b2d72868f820
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb201696(v=EXCHG.150)
ms:contentKeyID: 50473445
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定路由表格記錄

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-08_

路由表記錄功能會定期記錄 Microsoft Exchange Server 2013 使用的路由表快照，以便將郵件路由傳送至其目的地。

## 開始之前有哪些須知？

  - 預估完成時間：15 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「傳輸服務」和「Edge Transport Server」項目。

  - 您只能使用命令介面來執行此程序。

  - 若要設定的路由表的自動重新計算的時間間隔，您可以修改 EdgeTransport.exe.config XML 應用程式設定檔。您將此檔案的變更會套用之後重新啟動 Microsoft Exchange Transport 服務。當您重新啟動此服務的伺服器上的郵件流程暫時中斷。

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

## 使用命令介面來設定路由表記錄

執行下列命令：

    Set-TransportService <ServerIdentity> -RoutingTableLogMaxAge <dd.hh:mm:ss> -RoutingTableLogMaxDirectorySize <Size>  -RoutingTableLogPath <LocalFilePath>

此範例會在名稱為 Mailbox01 的信箱伺服器上設定以下的路由表記錄：

  - 將 D:\\Routing 表格記錄路由表格記錄檔案的位置。請注意是否資料夾不存在，它會為您建立。

  - 將路由表記錄檔資料夾的大小上限設定為 70 MB。

  - 將路由表記錄檔的保留天數上限設定為 45 天。

<!-- end list -->

    Set-TransportService Mailbox01 -RoutingTableLogPath "D:\Routing Table Log" -RoutingTableLogMaxDirectorySize 70MB -RoutingTableLogMaxAge 45.00:00:00

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>將 <em>RoutingTableLogMaxAge</em> 參數值設成 <code>00:00:00</code> 可以防止因為路由表記錄檔保留天數到期而自動移除路由表記錄檔。</td>
</tr>
</tbody>
</table>


## 如何才能了解這是否正常運作？

如要確認是否已成功設定啟路由表記錄功能，請執行下列動作：

1.  在命令介面中，執行下列命令：
    
        Get-TransportService <ServerIdentity> | Format-List RoutingTableLog*

2.  請確認顯示的值是您所設定的值。

## 使用命令提示字元在 EdgeTransport.exe.config 檔案中設定路由表的自動重新計算間隔

1.  在命令提示字元視窗中執行下列命令，即可在記事本中開啟 EdgeTransport.exe.config 應用程式組態檔：
    
        Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config

2.  修改下列位於 `<appSettings>` 區段的機碼。
    
        <add key="RoutingConfigReloadInterval" value="<hh:mm:ss>" />
    
    例如，若要將路由表的自動重新計算間隔變更為 10 小時，請使用以下的值：
    
        <add key="RoutingConfigReloadInterval" value="10:00:00" />

3.  完成後，儲存並關閉 EdgeTransport.exe.config 檔案。

4.  執行下列命令，以重新啟動 Microsoft Exchange 傳輸服務：
    
        net stop MSExchangeTransport && net start MSExchangeTransport

## 如何才能了解這是否正常運作？

若要確認是否已成功設定路由表的自動重新計算間隔，請在所指定的時間間隔內確認路由表記錄是否已更新。

請注意，若發生下列其中一個狀況，重新計算和記錄路由表的時間會早於 *RoutingConfigReloadInterval* 機碼所指定的值：

  - 偵測到路由的設定變更。例如，新增、 移除或修改，傳送連接器或接收連接器或 Kerberos token 更新 6 小時發生。

  - 已啟動 Microsoft Exchange 傳輸服務。

