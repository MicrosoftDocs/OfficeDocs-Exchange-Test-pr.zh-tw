---
title: 'Exchange Server 2013 效能建議: Exchange 2013 Help'
TOCTitle: Exchange Server 2013 效能建議
ms:assetid: 6d0aea68-10d5-4a18-b632-a814ce3daa43
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn879084(v=EXCHG.150)
ms:contentKeyID: 63763781
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange Server 2013 效能建議

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

Exchange Server 2013效能調整及疑難排解時最有效地您的環境具有正常大小及計劃。 雖然 Exchange 2013 的設計目的在於簡化基礎資源基礎結構，它仍然可以耗用大量的系統資源，例如記憶體、 儲存容量和 CPU 容量。

Exchange 效能小組所撰寫本節中的文章。它們包含從 Exchange 產品\] 群組中的專業知識，以及盡可能作法以及從客戶支援的情況。這些文章的目標是可協助您了解 Exchange 2013 和適當大小調整您的 Exchange 2013 基礎結構的重要性中變更的影響。我們也會包含建議的最佳化並識別效能問題的指導。

## 在 Exchange 2013 及其他資源的架構變更

TechNet 上與[Exchange 團隊部落格](https://go.microsoft.com/fwlink/p/?linkid=35786)中已經記載 Exchange 2013 的架構變更。 我們先將觸控時應考慮以進一步暸解效能的一些高階變更成本及調整大小。然後，下方，我們包含清單中的內容及下列重要方面的背景進一步提供建議的參照。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>請參閱<a href="exchange-2013-virtualization-exchange-2013-help.md">Exchange 2013 虛擬化</a>如需在虛擬環境中部署 Exchange Server 2013 效能最佳化指引。</td>
</tr>
</tbody>
</table>


在 Exchange 2013 Client Access server role 為無狀態的 proxy 伺服器。 現在的用戶端存取伺服器角色的主要責任，來驗證傳入的要求，然後 proxy 至適當的信箱伺服器每次要求一個架設的使用者信箱的主動副本。 這表示不再需要設定用戶端存取伺服器之間的相似性及負載平衡器特定通訊協定。

Exchange 2013 中的另一個值得變更是在資訊儲存庫。 資訊儲存庫現在所組成的程序的兩種類型： 主應用程式和工作者。 每個資料庫執行個體相關聯自己 Microsoft.Exchange.Store.Worker.exe 程序。 此問題的資料庫問題的較佳的隔離且可減少一個工作者實例該資料庫的資料庫發生問題的效能影響。

Microsoft Exchange 複寫服務會負責所有信箱伺服器角色的相關的高可用性服務。 此複寫服務會裝載 Active Manager 元件，這是負責監視失敗並採取更正動作。

在[Exchange 2013 Server Role 架構](https://go.microsoft.com/fwlink/p/?linkid=523735)可以找到更好的文章包括影響來重新調整大小與舊版不同的 Exchange 2013 環境的架構變更上。

您可以找到更多有關 Exchange 2013 的架構變更、 與其他相關的區域上的背景資訊在下列：

[Exchange Server 2013 架構](https://go.microsoft.com/fwlink/p/?linkid=523769)

[規劃它的右邊的方式： Exchange Server 2013 調整大小案例](https://go.microsoft.com/fwlink/p/?linkid=523773)

[Exchange Server 2013 效能監視與調整 Microsoft](https://go.microsoft.com/fwlink/p/?linkid=523774)

[實作 Exchange Server 2013： (01) 升級並部署 Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=523775)

[實作 Exchange Server 2013： (02) 規劃它右側的方式： Exchange Server 2013 調整](https://go.microsoft.com/fwlink/p/?linkid=523776)

[實作 Exchange Server 2013: (03) Exchange Server 2013 虛擬化的作法](https://go.microsoft.com/fwlink/p/?linkid=523777)

[實作 Exchange Server 2013： (04) 的 Exchange 架構： 高可用性和站台回復性](https://go.microsoft.com/fwlink/p/?linkid=523779)

[實作 Exchange Server 2013： (05) Outlook 連線](https://go.microsoft.com/fwlink/p/?linkid=523781)

[慣用的架構](https://go.microsoft.com/fwlink/p/?linkid=523782)

[Exchange 2013 用戶端存取伺服器角色](https://go.microsoft.com/fwlink/p/?linkid=386373)

[Exchange Server 2013 虛擬化的最佳作法](https://go.microsoft.com/fwlink/p/?linkid=523783)

[負載平衡](load-balancing-exchange-2013-help.md)

[Exchange Server 更新：組建編號與發行日期](https://technet.microsoft.com/zh-tw/library/hh135098\(v=exchg.150\))

[Exchange 2013 版本資訊](release-notes-for-exchange-2013-exchange-2013-help.md)

[更新 Exchange 2013](updates-for-exchange-2013-exchange-2013-help.md)

[在 IIS 7.5，IIS 7.0，以及 IIS 6.0 ASP.NET 執行緒流量](https://go.microsoft.com/fwlink/p/?linkid=169626)

