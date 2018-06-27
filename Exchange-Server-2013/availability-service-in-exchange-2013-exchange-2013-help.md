---
title: 'Exchange 2013 中的可用性服務: Exchange 2013 Help'
TOCTitle: Exchange 2013 中的可用性服務
ms:assetid: 9722dea2-2bf8-437c-85c0-3ab65b8a07b9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb232134(v=EXCHG.150)
ms:contentKeyID: 52062564
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013 中的可用性服務

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

Exchange 2013 可用性服務會對 Microsoft Outlook 和 Outlook Web App 用戶端提供空閒/忙碌資訊。可用性服務會提供安全、一致且最新的空閒及忙碌資訊，以提升資訊工作者在行事曆及會議排程方面的體驗。

Outlook 和 Outlook Web App 會使用可用性服務執行下列工作：

  - 擷取 Exchange 2013 信箱的目前空閒/忙碌資訊

  - 從其他 Exchange 2013 組織擷取目前空閒/忙碌資訊

  - 從具有舊版 Exchange 之伺服器上信箱的公用資料夾中，擷取已發佈的空閒/忙碌資訊

  - 檢視出席者工作時間

  - 顯示會議時間建議

**目錄**

Overview of the Availability service

Information about away status

Availability service API

Availability service Network Load Balancing

Methods used to retrieve free/busy information

## 可用性服務概觀

可用性服務擷取空閒/忙碌資訊直接從目標信箱上Exchange 2013、 Exchange 2010或Exchange 2007的使用者，並可設定要擷取空閒/忙碌資訊的使用者在舊版的Exchange上。如有Exchange 2007、 Exchange 2010或Exchange 2013的信箱中的所有用戶端正在執行Outlook 2007或可用性服務更高，用以擷取空閒/忙碌資訊的拓撲。

Outlook 使用 Exchange 自動探索服務來取得可用性服務的 URL。如需自動探索服務的相關資訊，請參閱[自動探索服務](autodiscover-service-for-exchange-2013.md)。

您可以使用 Exchange 管理命令介面設定可用性服務。您無法使用 Exchange 系統管理中心 (EAC) 設定可用性服務。

## 離開狀態的相關資訊

可用性服務還可讓使用者存取其不在辦公室或離開一段時間時傳送的自動回覆郵件。

當資訊工作者無法回應電子郵件時，可使用 Outlook 和 Outlook Web App 中的 \[自動回覆\] (以前稱為「郵件答錄機」) 功能來通知其他人。此功能同時方便資訊工作者和系統管理員設定和管理自動回覆郵件。

## 可用性服務 API

可用性服務為 Exchange 2013 程式設計介面的一部分。它可作為 Web 服務使用，讓開發人員編寫用於整合目的之協力廠商工具。

## 可用性服務網路負載平衡

在執行可用性服務的 Client Access server 上使用網路負載平衡 (NLB)，可以針對倚賴空閒/忙碌資訊的使用者改善效能和可靠性。Outlook 會使用自動探索服務，來探索可用性服務 URL。若要將 NLB 搭配可用性服務使用，必須變更您的組態。

內部 URL 是從內部網路使用，外部 URL 則是從網際網路使用。如果您希望內部及外部流量使用相同的 URL，請務必正確設定 DNS，以便將內部流量直接路由傳送到內部 URL。此外，務必確定無論從內部或外部都可存取 URL。若要讓自動探索和可用性服務運作，您需要設定 DNS，讓 mail.\<*domain name*\>.com 和 autodiscover.mail.\<*domain name*\>.com 指向負載平衡解決方案的虛擬 IP (VIP)，其中 \<*domain name*\> 是您網域的名稱。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如需詳細資訊，請參閱<a href="https://go.microsoft.com/fwlink/p/?linkid=45959">網路負載平衡技術參考 （英文)</a>和<a href="https://go.microsoft.com/fwlink/p/?linkid=49315">網路負載平衡的叢集</a>。您也可以搜尋的協力廠商負載平衡軟體網站。</td>
</tr>
</tbody>
</table>


## 用來擷取空閒/忙碌資訊的方法

下表列出在各種單一樹系拓撲中用以擷取空閒/忙碌資訊的不同方法。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>用戶端</th>
<th>擷取空閒/忙碌資訊的信箱正在執行</th>
<th>目標信箱正在執行</th>
<th>空閒/忙碌資訊擷取方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2013</p></td>
<td><p>Exchange 2013、 Exchange 2010或Exchange 2007</p></td>
<td><p>Exchange 2013、 Exchange 2010或Exchange 2007</p></td>
<td><p>可用性服務會從目標信箱讀取空閒/忙碌資訊。</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2007</p></td>
<td><p>Exchange 2013、 Exchange 2010或Exchange 2007</p></td>
<td><p>Exchange 2010或Exchange 2007</p></td>
<td><p>可用性服務會從目標信箱讀取空閒/忙碌資訊。</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 2007</p></td>
<td><p>Exchange 2010或Exchange 2007</p></td>
<td><p>Exchange 2003</p></td>
<td><p>可用性服務會建立對 Exchange 2003 信箱之 /public 虛擬目錄的 HTTP 連線。</p></td>
</tr>
<tr class="even">
<td><p>Outlook Web App</p></td>
<td><p>Exchange 2013、 Exchange 2010或Exchange 2007</p></td>
<td><p>Exchange 2013、 Exchange 2010或Exchange 2007</p></td>
<td><p>在Exchange 2010Outlook Web App或Outlook Web AccessExchange 2007中會呼叫可用性服務 API，其可從目標信箱讀取空閒/忙碌資訊。</p></td>
</tr>
</tbody>
</table>

