---
title: '變更佇列資料庫的位置: Exchange 2013 Help'
TOCTitle: 變更佇列資料庫的位置
ms:assetid: f170cb0c-04a9-4fa7-b594-206e3a787e14
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb125177(v=EXCHG.150)
ms:contentKeyID: 51409233
ms.date: 01/04/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 變更佇列資料庫的位置

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

*queue* 是等候進入下一個處理階段之訊息的暫存位置。每個佇列代表傳輸伺服器以特定順序處理的訊息邏輯集合。

與舊版的 Exchange 類似，Microsoft Exchange Server 2013 會使用「可延伸儲存引擎」(ESE) 資料庫作為佇列訊息儲存。所有不同的佇列都是儲存在單一 ESE 資料庫中。佇列僅會存放於 Mailbox Server 或 Edge Transport Server。

佇列資料庫與佇列資料庫交易記錄的位置，是由 `%ExchangeInstallPath%Bin\EdgeTransport.exe.config` XML 應用程式組態檔中的機碼進行控制。此檔案會與 Microsoft Exchange Transport 服務產生關聯。下表將更詳細地說明每一個機碼。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>機碼</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>QueueDatabasePath</em></p></td>
<td><p>此機碼會指定佇列資料庫檔案的位置。檔案如下：</p>
<ul>
<li><p>Mail.que</p></li>
<li><p>Trn.chk</p></li>
</ul>
<p>預設位置是 <code>%ExchangeInstallPath%TransportRoles\data\Queue</code>。</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseLoggingPath</em></p></td>
<td><p>此機碼會指定佇列資料庫交易記錄檔的位置。檔案如下：</p>
<ul>
<li><p>Trn.log</p></li>
<li><p>Trntmp.log</p></li>
<li><p>Trn<em>nnn</em>.log</p></li>
<li><p>Trnres00001.jrs</p></li>
<li><p>Trnres00002.jrs</p></li>
<li><p>Temp.edb</p></li>
</ul>
<p>請注意，Temp.edb 可在 Microsoft Exchange Transport 服務啟動時，用於驗證佇列資料庫架構。Temp.edb 雖然不是交易記錄檔，但仍會與交易記錄檔存放在相同的位置上。</p>
<p>預設位置是 <code>%ExchangeInstallPath%TransportRoles\data\Queue</code>。</p></td>
</tr>
</tbody>
</table>


## 開始之前有哪些須知？

  - 預估完成時間：15 分鐘。

  - Exchange 權限無法套用於此主題的程序。在 Exchange 伺服器的作業系統中執行這些程序。

  - 您在停止或重新啟動 Microsoft Exchange Transport 服務時，系統會中斷伺服器上的郵件流程。

  - 變更佇列資料庫或交易記錄的位置時，不會移動現有的佇列資料庫與交易記錄。系統會在新位置建立新的佇列資料庫與交易記錄。現有的檔案會保留在舊位置上。但不會再使用這些檔案。若您想要在新位置重新使用現有的佇列資料庫或交易記錄，則必須在 Microsoft Exchange Transport 服務已停止但尚未再次啟動之前，將現有的檔案移至新位置。

  - 若佇列資料庫或交易記錄的目標資料夾不存在，而父項資料夾已針對目標資料夾套用下列權限，則系統會為您建立目標資料夾：
    
      - 網路服務：完全控制
    
      - 系統：完全控制
    
      - 系統管理員：完全控制

  - 在您安裝 Exchange 累計更新 (CU) 後，將會覆寫您在 Exchange XML 應用程式組態檔 (例如 Client Access Server 上的 web.config 檔案，或 Mailbox Server 上的 EdgeTransport.exe.config 檔案) 中任何自訂的個別伺服器設定。請務必儲存此資訊，以便安裝後能輕易地重新設定伺服器。在安裝 Exchange CU 後，您必須重新配置這些設定。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

## 您要執行的工作

## 使用命令提示字元在新位置上建立新的佇列資料庫與交易記錄

1.  建立用以保存佇列資料庫與交易記錄的資料夾。確認資料夾所套用的權限正確無誤。

2.  在 \[命令提示字元\] 視窗中執行下列命令，即可在記事本中開啟 EdgeTransport.exe.config 檔案：
    
        Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config

3.  修改下列位於 `<appSettings>` 區段的機碼。
    
        <add key="QueueDatabasePath" value="<LocalPath>" />
        <add key="QueueDatabaseLoggingPath" value="<LocalPath>" />
    
    例如，若要在 D:\\Queue\\QueueDB 中建立新佇列資料庫，並在 D:\\Queue\\QueueLogs 中建立新交易記錄，請使用下列值：
    
        <add key="QueueDatabasePath" value="D:\Queue\QueueDB" />
        <add key="QueueDatabaseLoggingPath" value="D:\Queue\QueueLogs" />

4.  完成後，儲存並關閉 EdgeTransport.exe.config 檔案。

5.  執行下列命令，以重新啟動 Microsoft Exchange 傳輸服務：
    
        net stop MSExchangeTransport && net start MSExchangeTransport

## 如何才能了解這是否正常運作？

若要確認已在新位置上成功建立新的佇列資料庫與交易記錄，請執行下列動作：

1.  確認新的 Mail.que 與 Trn.chk 資料庫檔案已位於新位置上。

2.  確認新的 Trn.log、Trntmp.log、Trnres00001.jrs、Trnres00002.jrs 和 Temp.edb 交易記錄檔位於新位置上。

3.  若您在啟動 Microsoft Exchange Transport 服務後可從原本位置刪除舊的佇列資料庫與交易記錄檔，即無法再使用這些檔案。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

您要執行的工作

## 使用命令提示字元將現有的佇列資料庫與交易記錄移至新位置

只有在因 Microsoft Exchange Transport 服務未正確關閉或硬碟故障所導致的嚴重損壞修復作業中，才必須還原及重新尋找現有的佇列資料庫及其既有交易記錄。

您通常無須重複使用現有的交易記錄。Microsoft Exchange Transport 服務的正常關閉程序，會將所有尚未認可的交易記錄項目寫入至佇列資料庫中。此外亦會使用循環記錄，因此若交易記錄內含先前認可的資料庫變更，則不會保留。

使用下列程序將現有的佇列資料庫與交易記錄移至新位置：

1.  建立用以保存佇列資料庫與交易記錄的資料夾。確認資料夾所套用的權限正確無誤。

2.  在 \[命令提示字元\] 視窗中執行下列命令，即可在記事本中開啟 EdgeTransport.exe.config 檔案：
    
        Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config

3.  修改下列位於 `<appSettings>` 區段的機碼：
    
        <add key="QueueDatabasePath" value="<LocalPath>" />
        <add key="QueueDatabaseLoggingPath" value="<LocalPath>" />
    
    例如，若要將佇列資料庫的位置變更為 D:\\Queue\\QueueDB，並將交易記錄的位置變更為 D:\\Queue\\QueueLogs，請使用下列值：
    
        <add key="QueueDatabasePath" value="D:\Queue\QueueDB" />
        <add key="QueueDatabaseLoggingPath" value="D:\Queue\QueueLogs" />

4.  完成後，儲存並關閉 EdgeTransport.exe.config 檔案。

5.  執行下列命令，以停止 Microsoft Exchange Transport 服務：
    
        net stop MSExchangeTransport

6.  將現有的 Mail.que 與 Trn.chk 資料庫檔案從原始位置移至新位置上。

7.  將現有的 Trn.log、Trntmp.log、Trn*nnnnn*.log、Trnres00001.jrs、Trnres00002.jrs 和 Temp.edb 從原有位置移至新位置。

8.  執行下列命令，以啟動 Microsoft Exchange Transport 服務：
    
        net start MSExchangeTransport

## 如何才能了解這是否正常運作？

若要確認已將現有的佇列資料庫與交易記錄成功移至新位置，請執行下列動作：

1.  確認 Mail.que 與 Trn.chk 佇列資料庫檔案已位於新位置上。

2.  確認 Trn.log、Trntmp.log、Trnres00001.jrs、Trnres00002.jrs 和 Temp.edb 交易記錄檔位於新位置上。

3.  確認原有位置上已無任何佇列資料庫或交易記錄檔。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

您要執行的工作

