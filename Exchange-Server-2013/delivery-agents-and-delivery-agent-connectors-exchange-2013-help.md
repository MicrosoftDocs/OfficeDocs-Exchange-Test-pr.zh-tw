---
title: '傳遞代理程式及傳遞代理程式連接器: Exchange 2013 Help'
TOCTitle: 傳遞代理程式及傳遞代理程式連接器
ms:assetid: 38c942ee-b59d-47ec-87eb-bebad441ada5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd638118(v=EXCHG.150)
ms:contentKeyID: 50472881
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 傳遞代理程式及傳遞代理程式連接器

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

傳遞代理程式可從您的 SMTP Exchange 伺服器環境傳送郵件至不使用 SMTP 通訊協定的系統。每個傳遞代理程式皆與傳遞代理程式連接器相關聯，該連接器會佇列路由傳送至非 SMTP 裝置或系統進行處理程序的郵件。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>雖然 Microsoft Exchange 2013 保留了外部連接器架構，但建議儘可能使用傳遞代理程式將郵件路由至非 SMTP 系統。主要原因為您可以佇列郵件管理，無須管理檔案傳輸至放置目錄，且您可驗證郵件傳遞。</td>
</tr>
</tbody>
</table>


**目錄**

Function and benefits of Delivery Agents

Adding Delivery Agents to your organization

Delivery Agent connectors

Default text messaging Delivery Agent connector

## 傳遞代理程式的功能與優勢

傳遞代理程式為安裝在信箱伺服器的傳輸服務中的元件，可執行下列工作：

  - 建立外部系統連線以傳遞郵件。

  - 從信箱伺服器上的傳遞佇列擷取郵件。

  - 將郵件傳送到外部系統。

  - 提供每個成功傳遞郵件的認可。

雖然 Microsoft Exchange Server 2013 保留了外部連接器架構，但建議儘可能使用傳遞代理程式將郵件路由至非 SMTP 系統。傳遞代理程式具有下列好處：

  - 它們可進行路由傳輸至外部系統郵件的佇列管理。

  - 因為再也不需要在檔案系統中寫入與讀取郵件，所以改善了郵件傳遞效能。

  - 讓代理程式開發人員能夠以豐富的事件存取郵件內容。

  - 傳遞代理程式的開發時間比實行外部連接器的速度快，因為傳遞代理程式可使用 Exchange 的郵件表示與管理功能。

  - 可驗證郵件是否傳遞至外部系統，而非僅寫入至放置目錄。

  - 使用傳遞代理程式連接器可進行服務等級協定 (SLA) 分析，因為可以追蹤傳遞到外部系統的郵件的延遲。

## 將傳遞代理程式新增至您的組織

若要在組織中使用傳遞代理程式，您必須完成下列動作：

1.  取得傳遞代理程式。通常，傳遞代理程式是由協力廠商所撰寫。Exchange 2013 預設只隨附一個傳遞代理程式連接器：簡訊傳遞代理程式連接器。

2.  在要作為傳遞代理程式連接器之來源伺服器的信箱傳輸服務中，安裝傳遞代理程式。

3.  為特定通訊協定建立傳遞代理程式連接器。

這些步驟全都完成後，傳遞至外部系統的郵件將透過傳遞代理程式連接器路由，且由傳遞代理程式處理。

[Microsoft.Exchange.Data.Transport.Delivery 命名空間](https://go.microsoft.com/fwlink/?linkid=262690)提供更多關於研發傳遞代理程式的資訊。

## 傳遞代理程式連接器

Exchange 2013 中的傳遞代理程式連接器與 Exchange 2010 中使用的傳遞代理程式連接器相似。他們會路由傳輸送至不使用 SMTP 通訊協定的外部系統郵件。當郵件路由至傳遞代理程式連接器時，關聯的傳遞代理程式會執行內容轉換與郵件傳遞。一般來說，傳遞代理程式由協力廠商建立並設定為與組織中的傳遞代理程式連接器搭配使用。

傳遞代理程式連接器無法於 Exchange Administration Center 中建立。您可透過 [New-DeliveryAgentConnector](https://technet.microsoft.com/zh-tw/library/dd351063\(v=exchg.150\)) 指令程式在 Exchange 管理命令介面中建立傳遞代理程式連接器，並以 [Set-DeliveryAgentConnector](https://technet.microsoft.com/zh-tw/library/dd351159\(v=exchg.150\)) 編輯傳遞代理程式連接器的屬性。可使用 *SourceTransportServers* 參數為連接器指定一個或多個信箱伺服器。

## 預設文字郵件傳遞代理程式連接器

可使用簡訊傳遞代理程式連接器來路由傳輸郵件至行動裝置。在您的 Exchange 伺服器上，執行 `Get-DeliveryAgentConnector | fl` 來檢視連接器與所有參數。請注意 *DeliveryProtocol* 設為 `MOBILE`。

