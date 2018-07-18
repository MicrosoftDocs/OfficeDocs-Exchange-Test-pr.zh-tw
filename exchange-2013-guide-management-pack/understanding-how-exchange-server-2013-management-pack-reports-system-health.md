---
title: 瞭解 Exchange Server 2013 管理組件如何報告系統健康狀況
TOCTitle: 瞭解 Exchange Server 2013 管理組件如何報告系統健康狀況
ms:assetid: 6ca8847f-93fe-458d-bd43-7afad7fdd2f4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn195910(v=EXCHG.150)
ms:contentKeyID: 53276429
ms.date: 08/29/2014
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 瞭解 Exchange Server 2013 管理組件如何報告系統健康狀況

 

_**上次修改主題的時間：**  2013-04-17_

本主題提供 Exchange Server 2013 管理組件如何監視和報告 Exchange 系統健全狀態的相關資訊。在 Exchange 2013 管理組件中，健全狀態資訊以簡單的方式進行彙總。每當健全設定狀況不良並觸發呈報回應程式時，Windows 記錄檔中會記錄下列事件：

## 受管理的可用性

在 Exchange Server 2013 中，架構已進行了諸多變更。其中一項重要變更就是 *「受管理的可用性」(Managed Availability)* 功能，所有 Exchange 2013 元件都有內建的監視器，可偵測問題並嘗試復原服務可用性。Exchange 2013 管理組件依賴此功能。任何無法自動復原的問題，都會以警示形式呈報給 Exchange 2013 管理組件。Exchange 2013 中的每個元件會使用三個基本元件來我自監視：探查、監視器和回應程式。

![受管理的可用性](images/Dn195910.dd5febae-d05e-4089-a3f5-1691b2d9a3d7(EXCHG.150).png "受管理的可用性")


  - **探查** 這些是測量各種元件的一組資料收集器。探查有三種不同類型：

    
      - 可測量綜合端對端使用者作業的綜合交易，以及可測量實際流量的檢查。
    
      - 測量實際客戶流量的檢查。
    
      - 可讓 Exchange 立即採取行動的通知。憑證到期時觸發的通知就是一個很好的例子。


  - **監視器** 探查所收集的資料會傳給監視器來分析資料的特定狀況，並會根據這些狀況來判斷特定元件是否健全。

  - **回應程式** 如果監視器判定元件狀況不良，則會觸發回應程式。如果問題可復原，回應程式會嘗試利用內建的邏輯來復原元件。每個元件有數個回應程式可用，但與 Exchange 2013 管理組件有關的一個回應程式是 *「呈報回應程式」(Escalate Responder)*。當呈報回應程式觸發時，它會產生 Exchange 2013 管理組件可辨識的事件，並在警示中加入適當的資訊，以提供系統管理員解決問題所需的資訊。


Exchange 2013 的每個元件會使用一組特定的探查、監視器和回應程式來自我監視。這幾組探查和監視器稱為 *「健全設定」(Health Set)*。例如，許多探查會收集 ActiveSync 服務各方面的相關資料。有一組指定的監視器會處理此資料，並觸發適當的回應程式來更正它們在 ActiveSync 服務中偵測到的任何問題。總而言之，這些元件一起構成 ActiveSync 健全設定。

Exchange 中的健全設定分成下列四個類別，對應於管理套件儀表板：

  - 客戶觸控點

  - 服務元件

  - 伺服器資源

  - 主要依存項目

如需 Exchange 健全設定的完整清單，請參閱[Appendix A: Exchange health sets](appendix-a-exchange-health-sets.md)。

若要深入了解「受管理的可用性」的相關資訊，請參閱[伺服器健全狀況與效能](https://technet.microsoft.com/zh-tw/library/jj150551\(v=exchg.150\))。

## 健全狀態如何彙總

本主題提供 Exchange Server 2013 管理組件如何監視和報告 Exchange 系統健全狀態的相關資訊。在 Exchange 2013 管理組件中，健全狀態資訊以簡單的方式進行彙總。每當健全設定狀況不良並觸發呈報回應程式時，Windows 記錄檔中會記錄下列事件：


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>記錄檔名稱</p></td>
<td><p>Microsoft-Exchange-ManagedAvailability/Monitoring</p></td>
</tr>
<tr class="even">
<td><p>來源</p></td>
<td><p>ManagedAvailability</p></td>
</tr>
<tr class="odd">
<td><p>日期</p></td>
<td><p>&lt;<em>事件的日期和時間</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>事件識別碼</p></td>
<td><p>4</p></td>
</tr>
<tr class="odd">
<td><p>工作類別</p></td>
<td><p>監視</p></td>
</tr>
<tr class="even">
<td><p>層級</p></td>
<td><p>錯誤</p></td>
</tr>
<tr class="odd">
<td><p>關鍵字</p></td>
<td><p>&lt;<em>無</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>User</p></td>
<td><p>SYSTEM</p></td>
</tr>
<tr class="odd">
<td><p>電腦</p></td>
<td><p>&lt;<em>Exchange 伺服器的 FQDN</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>描述</p></td>
<td><p>&lt;<em>由呈報回應程式動態產生</em>&gt;</p></td>
</tr>
</tbody>
</table>


管理組件代理程式會偵測並處理此事件。透過此事件，「受管理的可用性」就能夠在 SCOM 內產生警示。解決相關的問題，且健全設定回到健全狀態之後，Windows 事件記錄檔中會記錄下列事件：


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>記錄檔名稱</p></td>
<td><p>Microsoft-Exchange-ManagedAvailability/Monitoring</p></td>
</tr>
<tr class="even">
<td><p>來源</p></td>
<td><p>ManagedAvailability</p></td>
</tr>
<tr class="odd">
<td><p>日期</p></td>
<td><p>&lt;<em>事件的日期和時間</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>事件識別碼</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p>工作類別</p></td>
<td><p>監視</p></td>
</tr>
<tr class="even">
<td><p>層級</p></td>
<td><p>參考</p></td>
</tr>
<tr class="odd">
<td><p>關鍵字</p></td>
<td><p>&lt;<em>無</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>User</p></td>
<td><p>SYSTEM</p></td>
</tr>
<tr class="odd">
<td><p>電腦</p></td>
<td><p>&lt;<em>Exchange 伺服器的 FQDN</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>描述</p></td>
<td><p>&lt;<em>由呈報回應程式動態產生</em>&gt;</p></td>
</tr>
</tbody>
</table>


監視舊版 Exchange 的管理組件已完全集中。每個 Exchange 伺服器的代理程式會收集資料，而中央關聯性引擎會比較並評估代理程式所報告的所有資料，以判斷整體服務健全狀態。在大型環境中，此程序會產生複雜的關聯性，導致延遲產生警示。在 Exchange 2013 中，不再使用警示關聯性。反之，每個伺服器會執行自己的監視作業，並在必要時向 SCOM 提出警示，從而打造具有高度延展性的架構。

根據事件的影響及觸發事件的健全設定而定，SCOM 主控台會以不同類別來顯示問題。如果事件造成使用者影響，則客戶觸控點指示器會顯示為狀況不良。如果造成整個元件 (如 OWA) 無法使用，則服務元件指示器會顯示為狀況不良。如果是特定伺服器的問題，則對應的伺服器健全狀態指示器會顯示為狀況不良。最後，如果問題出在 Exchange 仰賴的資源上，則主要依存項目指示器會顯示為狀況不良。如需這些類別的詳細資訊，請參閱[Exchange Server 2013 管理組件快速入門](getting-started-with-exchange-server-2013-management-pack.md)。

