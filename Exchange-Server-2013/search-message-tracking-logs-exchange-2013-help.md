---
title: '搜尋郵件追蹤記錄檔: Exchange 2013 Help'
TOCTitle: 搜尋郵件追蹤記錄檔
ms:assetid: e1678327-bcd5-42d4-a363-67f33067fe9a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124926(v=EXCHG.150)
ms:contentKeyID: 51409249
ms.date: 01/04/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 搜尋郵件追蹤記錄檔

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2013-02-25_

在 Microsoft Exchange Server 2013 中，在信箱伺服器、信箱伺服器上的信箱以及邊際傳輸伺服器上，將郵件傳輸至傳輸服務或是從傳輸服務來傳輸，郵件追蹤記錄檔都會詳細記錄所有的郵件活動。

您可以在 Exchange 管理命令介面中使用 **Get-MessageTrackingLog** 指令程式，使用特定的搜尋準則來搜尋郵件追蹤記錄中的項目。

## 開始之前有哪些須知？

  - 預估完成時間：30 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱[郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「郵件追蹤」項目。

  - 搜尋郵件追蹤蹤記錄時，需要 Microsoft Exchange Transport Log Search 服務正在執行中。若您停用或停止此服務，您就無法搜尋郵件追蹤記錄或執行傳遞回報。但是，停止此服務並不會影響 Exchange 中的其它功能。

  - **Get-MessageTrackingLog** Cmdlet的結果所顯示的欄位名稱，與郵件追蹤記錄中使用的實際欄位名稱相類似。最大的差異在於：
    
      - 破折號已從欄位名稱中移除。例如，**internal-message-id** 將顯示為 `InternalMessageId`。
    
      - **date-time** 欄位將顯示為 `Timestamp`。
    
      - **recipient-address** 欄位將顯示為 `Recipients`。
    
      - **sender-address** 欄位將顯示為 `Sender`。

  - 郵件追蹤記錄中的 **date-time** 欄位會以 Coordinated Universal Time (UTC) 儲存資訊。不過，您應該根據執行搜尋之電腦上的地區日期時間格式，來輸入 *Start* 或 *End* 參數的日期時間搜尋準則。

  - 您不能從其他 Exchange 伺服器複製郵件追蹤記錄檔，然後又使用 **Get-MessageTrackingLog** Cmdlet 來搜尋這些郵件追蹤記錄檔。此外，如果您手動儲存現有的郵件追蹤記錄檔，則檔案之日期時間戳記變更時，會破壞 Exchange 用來搜尋郵件追蹤記錄的查詢邏輯。

  - Exchange 2013**Get-MessageTrackingLog** 指令程式可以搜尋相同 Active Directory 站台中 Exchange 2007 和 Exchange 2010 伺服器上的郵件追蹤記錄。

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

## 使用命令介面來搜尋郵件追蹤記錄

若要搜尋特定事件的郵件追蹤記錄項目，請使用下列語法。

    Get-MessageTrackingLog [-Server <ServerIdentity.] [-ResultSize <Integer> | Unlimited] [-Start <DateTime>] [-End <DateTime>] [-EventId <EventId>] [-InternalMessageId <InternalMessageId>] [-MessageId <MessageId>] [-MessageSubject <Subject>] [-Recipients <RecipientAddress1,RecipientAddress2...>] [-Reference <Reference>] [-Sender <SenderAddress>]

若要檢視伺服器上最近 1000 個郵件追蹤記錄項目，請執行下列命令：

    Get-MessageTrackingLog

此範例會搜尋本機伺服器上的郵件追蹤記錄，以獲得從 2013 年 3 月 28 日上午 8:00 到 2013 年 3 月 28 日下午 5:00，郵件寄件者為 pat@contoso.com 之所有 **FAIL** 事件的所有項目。

    Get-MessageTrackingLog -ResultSize Unlimited -Start "3/28/2013 8:00AM" -End "3/28/2013 5:00PM" -EventId "Fail" -Sender "pat@contoso.com"

## 使用命令介面來控制郵件追蹤記錄搜尋的輸出

使用下列語法。

    Get-MessageTrackingLog <SearchFilters> | <Format-Table | Format-List> [<FieldNames>] [<OutputFileOptions>]

本範例會使用下列搜尋準則來搜尋郵件追蹤記錄：

  - 傳回前 1,000 個 **Send** 事件的結果。

  - 以清單格式顯示結果。

  - 只顯示以 `Send` 或 `Recipient` 開頭的欄位名稱。

  - 將輸出寫入名為 `D:\Send Search.txt` 的新檔案

<!-- end list -->

    Get-MessageTrackingLog -EventId Send | Format-List Send*,Recipient* > "D:\Send Search.txt"

## 使用命令介面在多部伺服器上搜尋郵件追蹤記錄中的郵件項目

一般來說，**MessageID:** 標頭欄位中的值，在郵件於整個 Exchange 組織中傳輸時會維持不變。在佇列檢視公用程式中，此內容名為 **InternetMessageId**，在郵件追蹤記錄檢視公用程式中，此內容名為 **MessageId**。在您判斷特定郵件的 `MessageID:` 值之後，即可在 Exchange 組織中每部 Mailbox Server 上的郵件追蹤記錄檔中，搜尋該郵件的相關資訊。

若要在所有 Mailbox Server 中搜尋特定郵件的所有郵件追蹤記錄項目，請使用下列語法。

    Get-ExchangeServer | where {$_.isHubTransportServer -eq $true -or $_.isMailboxServer -eq $true} | Get-MessageTrackingLog -MessageId <MessageID> | Select-Object <CommaSeparatedFieldNames> | Sort-Object -Property <FieldName>

本範例會使用下列搜尋準則，搜尋所有 Exchange 2013 Mailbox Server 上的郵件追蹤記錄：

  - 針對 **MessageID:** 值為 `<ba18339e-8151-4ff3-aeea-87ccf5fc9796@mailbox01.contoso.com>` 的郵件，尋找任何相關項目。請注意，您可以省略角括弧字元 (`<``>`)。如果您不這樣做，則需要將整個 **MessageID:** 值用引號括住。

  - 對於每個項目，顯示 **date-time**、**server-hostname**、**client-hostname**、**source**、**event-id** 和 **recipient-address** 欄位。

  - 依 **date-time** 欄位排序結果。

<!-- end list -->

    Get-ExchangeServer | where {$_.isHubTransportServer -eq $true -or $_.isMailboxServer -eq $true} | Get-MessageTrackingLog -MessageId ba18339e-8151-4ff3-aeea-87ccf5fc9796@mailbox01.contoso.com | Select-Object Timestamp,ServerHostname,ClientHostname,Source,EventId,Recipients | Sort-Object -Property Timestamp

## 使用 EAC 搜尋郵件追蹤記錄

您可以在 Exchange 系統管理中心 (EAC) 中使用系統管理員的「傳遞回報」功能來搜尋郵件追蹤記錄，以取得組織中由特定信箱傳送或接收之郵件的相關資訊。如需詳細資訊，請參閱 [使用傳遞回報追蹤郵件](track-messages-with-delivery-reports-exchange-2013-help.md)。

