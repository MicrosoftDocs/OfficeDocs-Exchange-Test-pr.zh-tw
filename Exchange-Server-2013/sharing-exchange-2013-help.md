---
title: '共用: Exchange 2013 Help'
TOCTitle: 共用
ms:assetid: 09e6732a-4e99-44d0-801d-9463fdc57a9b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd638083(v=EXCHG.150)
ms:contentKeyID: 50472523
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 共用

 

_**適用版本：**Exchange Server 2013, Outlook 2013_

_**上次修改主題的時間：**2015-02-27_

您可能會需要與不同組織的人或是親友協調排程，以便合作執行專案或規劃社交活動。透過 Exchange 2013，系統管理員將可設定不同層級的行事曆存取，讓企業能夠與其他企業共同合作，並且讓使用者可將其排程與他人共用。企業對企業的行事曆共用可藉由建立「組織關係」來設定。使用者對使用者的行事曆共用，則可藉由套用「共用原則」來設定。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>此 Exchange Server 2013 功能與中國的 21Vianet 所運作的 Office 365 不完全相容，部分功能可能受限。如需詳細資訊，請參閱<a href="https://go.microsoft.com/fwlink/?linkid=313640">了解 21Vianet 運作的 Office 365</a>。</td>
</tr>
</tbody>
</table>


**目錄**

Sharing Scenarios in Exchange 2013

Limitations of free/busy sharing

Firewall considerations for federated sharing

Coexistence with Exchange 2010

Coexistence with Exchange 2007

Sharing Documentation

## Exchange 2013 中的共用案例

以下是 Exchange 2013 所支援的共用案例：


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>共用目標</th>
<th>要使用的設定</th>
<th>需求</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>與 Office 365 組織共用行事曆</p></td>
<td><p>組織關聯性</p></td>
<td><p>Office 365 組織已可進行設定。內部部署 Exchange 系統管理員必須設定與雲端之間的驗證關係 (也稱為「同盟」)，且必須符合最低軟體需求。若要深入了解如何設定同盟，請參閱<a href="federation-exchange-2013-help.md">同盟</a>。</p></td>
</tr>
<tr class="even">
<td><p>與其他內部部署 Exchange 組織共用行事曆</p></td>
<td><p>組織關係</p></td>
<td><p>兩個內部部署 Exchange 組織都必須設定同盟，且必須符合最低軟體需求</p></td>
</tr>
<tr class="odd">
<td><p>與網際網路使用者共用 Exchange 使用者的行事曆</p></td>
<td><p>共用原則</p></td>
<td><p>無，已可進行設定</p></td>
</tr>
<tr class="even">
<td><p>與其他 Exchange 內部部署使用者共用 Exchange 使用者的行事曆</p></td>
<td><p>共用原則</p></td>
<td><p>兩個內部部署 Exchange 組織都必須設定同盟，且必須符合最低軟體需求。</p></td>
</tr>
</tbody>
</table>


下表列出組織關係與共用原則之間的差異。

### 組織關係與共用原則的比較

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>組織關係</th>
<th>共用原則</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>需要您組織的同盟信任</p></td>
<td><p>是</p></td>
<td><p>是，如果與其他同盟網域組織共用的話。不是網際網路共用原則所必需。</p></td>
</tr>
<tr class="even">
<td><p>建議外部網域加入同盟</p></td>
<td><p>是</p></td>
<td><p>是，如果與其他同盟網域組織共用的話。不是網際網路共用原則所必需。</p></td>
</tr>
<tr class="odd">
<td><p>允許與外部組織共用一組使用者的空閒/忙碌資訊 (包括主旨與位置)。</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>允許共用含空閒/忙碌資訊的行事曆資料夾</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>允許共用含空閒/忙碌資訊 (包括主旨及內文) 的行事曆資料夾</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>需要使用者將共用邀請寄給外部收件者</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>提供存取方法</p></td>
<td><p>您的 Client Access Server 會存取外部組織的 Client Access Server，並在要求時擷取外部使用者的空閒/忙碌資訊。</p></td>
<td><p>您的 Client Access Server 會存取外部組織的 Client Access Server，並訂閱外部使用者的行事曆資料夾。針對網際網路共用原則，外部使用者可存取 Client Access Server 上的受限或公開 URL。</p></td>
</tr>
<tr class="even">
<td><p>可套用至所有外部網域</p></td>
<td><p>否 (兩個 Exchange 2013 組織之間一對一的關係)</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>提供使用者與外部收件者共用的不同經驗</p></td>
<td><p>否</p></td>
<td><p>是，根據套用的共用原則</p></td>
</tr>
<tr class="even">
<td><p>停用某些使用者的共用</p></td>
<td><p>是，藉由為組織關係指定安全性通訊群組</p></td>
<td><p>是，藉由停用套用的共用原則</p></td>
</tr>
<tr class="odd">
<td><p>需要信箱位於 Exchange 2013 信箱伺服器上</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
</tr>
</tbody>
</table>


回到頁首

## 空閒/忙碌資訊共用的限制

在同盟 Exchange 組織之間共用空閒/忙碌資訊時，將有下列限制：

1.  **Outlook Web Access 2003**   當 Exchange 2003 組織中的使用者利用 Outlook Web Access 存取遠端 Exchange 2013 組織使用者的空閒/忙碌資訊時，請求將會失敗。來自 Exchange 2003 的 Outlook Web Access 連線無法對空閒/忙碌資訊系統資料夾建立 WebDAV (網頁導向分工編寫及版本管理) 連線來擷取遠端使用者的空閒/忙碌資訊。因為 Exchange 2013 不支援 WebDAV 連線，Exchange 2003 伺服器無法為 Outlook Web Access 請求連接 Exchange 2013 CAS 伺服器上的至外部 (FYDIBOHF25SPDLT)。Outlook 用戶端無法體驗此限制，因為他們在連接至外部 (FYDIBOHF25SPDLT) 時以 MAPI 取代 WebDAV。

2.  **廣域網路 (WAN) 延遲**   在 Exchange 2003 組織中，所有空閒/忙碌資訊資料夾的複本，皆必須存在 Exchange 2010 SP2 或更新版本的信箱伺服器上。若 Exchange 2003 公用資料夾資料庫位於多個實體站台中，且內部的空閒/忙碌資訊查詢數必須周遊 WAN 連結以存取不在相同實體站台內的 Exchange 2010 公用資料夾資料庫，則可能會出現過多的延遲及效能問題。

3.  **空閒/忙碌資訊期間**   若 Exchange 2013 組織向 Exchange 2007 組織提出空閒/忙碌資訊要求，可能會因為要求的空閒/忙碌資訊期間不符，而導致要求失敗。依預設，Exchange 2007 接受的可用性要求為 42 天的空閒/忙碌資訊，而 Exchange 2013 可能會要求提供 62 天的空閒/忙碌資訊。若 Exchange 2007 要求的天數高於 42 天 ( 所作的預設限制)，要求將會失敗。
    
    請依照以下步驟來設定您的 Exchange 2007 CAS 伺服器，以接受更長期間的空閒/忙碌資訊要求：
    
    1.  在您所有的 Exchange 2007 CAS 伺服器上，使用文字編輯器 (例如記事本) 開啟下列檔案。\<Exchange 安裝路徑\>\\V14\\ClientAccess\\ExchWeb\\EWS\\web.config
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>在變更 web.config 檔案之前，請先將檔案複製到安全的位置。</td>
        </tr>
        </tbody>
        </table>
    
    2.  在 web.config 檔案中找出 **appSettings** 區段。
    
    3.  新增「\<add key="maximumQueryIntervalDays" value="62" /\>」機碼，並儲存 web.config 檔案。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>依預設，maximumQueryIntervalDays 值並不會存在。若此值不存在， Exchange 2007 會使用預設的 42 天時間間隔。</td>
        </tr>
        </tbody>
        </table>
    
    4.  在所有 Exchange 2007 CAS 伺服器上，停止並重新啟動 Microsoft 網際網路資訊服務 (IIS)。

4.  **同時具有內部部署及雲端使用者的 Exchange 組織**   若您透過 Microsoft Office 365，設定了與另一個在混合部署中設定的 Exchange 組織之間的行事曆共用，將無法對已移至雲端的 Office 365 使用者或遠端使用者，進行空閒/忙碌資訊可用性查詢。由於與您 Exchange 組織存在組織關係的，是遠端的內部部署 Exchange 組織而非 Office 365 架構 Exchange Online 組織，因此空閒/忙碌資訊要求無法查詢 Office 365 架構使用者。Exchange 2013 並不支援代理這些從內部部署組織到 Office 365 的可用性要求。

若要了解關於於一般 Exchange 部署間設定空閒/忙碌共用的詳細資訊，請參閱 [設定 Exchange 組織之間的同盟共用](configuring-federated-sharing-between-exchange-organizations-exchange-2013-help.md)。

## 同盟共用的防火牆考慮事項

同盟共用功能需要您組織中的用戶端存取伺服器使用 HTTPS 來有輸出至網際網路的存取。您必須在組織中的所有Exchange 2013 Mailbox server 都允許輸出 HTTPS 存取 （連接埠 443 tcp）。

為了讓外部組織存取您組織的空閒/忙碌資訊，您必須至少將一個 Client Access Server 發行至網際網路。這需要 HTTPS 從網際網路向內存取 Client Access Server。Active Directory 站台若未將 Client Access Server 發行至網際網路，則站台中的 Client Access Server 可以使用其他可從網際網路存取的 Active Directory 站台中的 Client Access Server。尚未發行至網際網路的 Client Access Server 必須有 Web 服務虛擬目錄的外部 URL，該虛擬目錄已設定外部組織看得到的 URL。

回到頁首

## 與 Exchange 2010 共存

在同時包含 Exchange 2010 和 Exchange 2013 伺服器的組織中，在 Exchange 2010 信箱伺服器上有信箱的使用者可以使用組織關係，與外部 Exchange 2013 同盟網域組織中的收件者共用空閒/忙碌資訊。Exchange 2010 用戶端存取與信箱伺服器應執行 SP2 或更新版本，且您在 Exchange 2013 組織中必須至少有一個 Exchange 2010 用戶端存取伺服器。

## 與 Exchange 2007 共存

在同時包含 Exchange 2013 和 Exchange 2007 伺服器的組織中，在 Exchange 2007 信箱伺服器上有信箱的使用者可以使用組織關係，與外部同盟網域組織中的收件者共用空閒/忙碌資訊。信箱伺服器必須執行 Exchange 2007 SP2 或更新版本，且您在 Exchange 2013 組織中必須至少有一個 Exchange Client Access Server。您可以透過在組織中引入單一 Exchange 2013 Client Access Server 來使用組織關係，以提供比同步化空閒/忙碌資訊且需要 GAL 同步處理的解決方案更健全的解決方案。

使用 Outlook 2010 或 Outlook Web App 在 Exchange 2007 伺服器上排程會議時，在 Exchange 2007 伺服器上有信箱的使用者可以看到外部組織中使用者的空閒/忙碌資訊。外部組織中的收件者可看見 Exchange 2007 信箱的空閒/忙碌資訊。

共用原則會指派給 Exchange 2013 信箱使用者。若要使用共用原則，信箱必須位在 Exchange 2013 信箱伺服器上。只有 Outlook 2010 與 Outlook Web App 用戶端可用於產生或回應共用邀請。

回到頁首

## 共用文件

下列表格包含與各主題的連結，將協助您了解並管理 Exchange 2013 中的共用。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>主題</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="federation-exchange-2013-help.md">同盟</a></p></td>
<td><p>深入了解支援同盟共用的基礎信任基礎結構；對使用者而言，這是與其他外部收件者共用行事曆資訊的簡易方法。</p></td>
</tr>
<tr class="even">
<td><p><a href="organization-relationships-exchange-2013-help.md">組織關係</a></p></td>
<td><p>深入了解支援行事曆空閒/忙碌共用的 Exchange 組織之間的一對一關係。</p></td>
</tr>
<tr class="odd">
<td><p><a href="sharing-policies-exchange-2013-help.md">共用原則</a></p></td>
<td><p>深入了解支援共用功能的個人對個人原則。</p>
<p></p></td>
</tr>
</tbody>
</table>

