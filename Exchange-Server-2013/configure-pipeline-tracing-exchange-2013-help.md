---
title: '設定管線追蹤: Exchange 2013 Help'
TOCTitle: 設定管線追蹤
ms:assetid: 10293c83-2157-474e-840d-942e064a4672
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ916678(v=EXCHG.150)
ms:contentKeyID: 52062515
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定管線追蹤

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-08_

管線追蹤可在電子郵件通過 Mailbox Server 及 Edge Transport Server 上傳輸服務或信箱傳輸服務中的傳輸管線時擷取其複本。

## 開始之前有哪些須知？

  - 此程序預估完成時間：15 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「傳輸服務」及「信箱傳輸服務」項目。

  - 您只能使用命令介面來執行此程序。

  - 管線追蹤會複製從寄件者的電子郵件地址傳送之電子郵件的完整內容。若要避免機密資訊意外曝光，您需要在管線追蹤資料夾的位置上設定適當的安全性權限。

  - 請不要長時間啟用管線追蹤。管線追蹤會建立多個快速累積的郵件快照檔案。啟用管線追蹤時，請務必監控可用磁碟空間。

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

## 啟用及設定管線追蹤

## 步驟 1：使用命令介面來設定管線追蹤寄件者地址

請使用下列語法來設定管線追蹤寄件者地址。

    <Set-TransportService | Set-MailboxTransportService> <ServerIdentity> -PipelineTracingSenderAddress <SMTPAddress | "<>">

本範例會設定管線追蹤，以在名稱為 Mailbox01 的 Mailbox Server 上的傳輸服務中擷取寄件者 chris@contoso.com 所傳送的所有郵件的快照。

    Set-TransportService Mailbox01 -PipelineTracingSenderAddress chris@contoso.com

本範例會設定管線追蹤，以在名稱為 Mailbox02 的 Mailbox Server 上擷取傳輸服務所收到的所有系統產生的郵件的快照。

    Set-TransportService Mailbox02 -PipelineTracingSenderAddress "<>"

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>設定管線追蹤來擷取傳輸服務中所有伺服器產生的郵件，可能會在伺服器上產生沈重的負荷，因而很快地耗用可用的磁碟空間。啟用管線追蹤時，請務必監控可用磁碟空間。</td>
</tr>
</tbody>
</table>


## 步驟 2：(選用) 使用命令介面來指定自訂管線追蹤資料夾

直到您啟用管線追蹤之後，預設管線追蹤資料夾才會存在，而且符合您使用 *PipelineTracingSenderAddress* 參數指定之準則的郵件會經過伺服器上的傳輸服務。若為 Mailbox Server 上的傳輸服務，預設位置為 `%ExchangeInstallPath%TransportRoles\Logs\Hub\PipelineTracing`。若為 Mailbox Server 上的信箱傳輸服務，預設位置為 `%ExchangeInstallPath%TransportRoles\Logs\Mailbox\PipelineTracing`。如果您指定自訂路徑，則該路徑必須在本機 Exchange 伺服器上。

請使用下列語法來設定管線追蹤資料夾。

    <Set-TransportService | Set-MailboxTransportService> <ServerIdentity> -PipelineTracingPath <LocalFilePath>

本範例會將 Mailbox Server (名稱為 Mailbox01) 上傳輸服務的管線追蹤資料夾設為 D:\\Hub\\Pipeline Tracing。

    Set-TransportService Mailbox01 -PipelineTracingPath "D:\Hub\Pipeline Tracing"

## 步驟 3：使用命令介面來啟用管線追蹤

根據預設，在所有 Exchange 伺服器上，都會停用管線追蹤。當啟用管線追蹤時，您只會在指定的 Exchange 伺服器上指定的傳輸服務中啟用管線追蹤。在啟用管線追蹤之前，您需要依步驟 1 所述來指定寄件者地址。

請使用下列語法來啟用管線追蹤。

    <Set-TransportService | Set-MailboxTransportService> <ServerIdentity> -PipelineTracingEnabled $true

本範例會在 Mailbox Server (名稱為 Mailbox01) 的傳輸服務中啟用管線追蹤。

    Set-TransportService Mailbox01 -PipelineTracingEnabled $true

## 如何知道這是否正常運作？

若要確認您是否已成功設定管線追蹤，請執行下列動作：

1.  執行下列命令：
    
        <Get-TransportService | Get-MailboxTransportService> <ServerIdentity> | Format-List PipelineTracing*

2.  請確認顯示的值是您所設定的值。

3.  檢查傳輸服務或信箱傳輸服務的管線追蹤資料夾，並確認會在資料夾中建立郵件快照檔案。

## 停用管線追蹤

由於磁碟空間以及與管線追蹤相關聯的安全性考量，管線追蹤是基於診斷或疑難排解用途的暫時動作。每當啟用管線追蹤時，請務必記住在作業完成後停用它。

請使用下列語法來停用管線追蹤。

    <Set-TransportService | Set-MailboxTransportService> <ServerIdentity> -PipelineTracingEnabled $false

本範例會在 Mailbox Server (名稱為 Mailbox01) 的傳輸服務中停用管線追蹤。

    Set-TransportService Mailbox01 -PipelineTracingEnabled $false

## 如何知道這是否正常運作？

若要確認您是否已成功停用管線追蹤，請執行下列動作：

1.  執行下列命令：
    
        <Get-TransportService | Get-MailboxTransportService> <ServerIdentity> | Format-List PipelineTracingEnabled

2.  確認 *PipelineTracingEnabled* 參數的值為 $false。

3.  檢查管線追蹤資料夾，並確認資料夾中再也不會建立郵件快照檔案。

