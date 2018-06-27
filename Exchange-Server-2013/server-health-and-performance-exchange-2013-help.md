---
title: '伺服器健康狀況與效能: Exchange 2013 Help'
TOCTitle: 伺服器健康狀況與效能
ms:assetid: 9d1fdec8-8273-4c71-88f1-b4edfd542c4f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ150551(v=EXCHG.150)
ms:contentKeyID: 50473848
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 伺服器健康狀況與效能

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

了解伺服器健康狀況與效能十分重要來設計和維護高效能訊息基礎結構。Microsoft Exchange Server 2013介紹伺服器健康狀況與效能改良的功能。

要尋找的所有伺服器健康狀況與效能主題清單嗎？請參閱伺服器健康狀況與效能文件。

## 受管理的可用性

Exchange 2013介紹的概念*受管理的可用性*。受管理的每一部Exchange 2013伺服器上執行的可用性。它是由兩個程序、 Exchange 健全狀況管理員服務 (MSExchangeHMHost.exe) 及 Exchange 健全狀況管理員工作者處理序 (MSExchangeHMWorker.exe) 及下列的非同步元件組成：

  - **探查引擎**  *探查引擎*會在伺服器上的度量值。

  - **監視探查引擎**  *監視探查引擎*儲存關於什麼構成良好的商務邏輯。功能類似圖樣辨識引擎，尋找模式和良好，與不同的度量值，並再評估元件或功能是否為不健康。

  - **回應程式引擎**  當*回應程式引擎*會收到通知關於不健康的元件時，其第一個巨集指令會嘗試復原該元件。受管理的可用性會啟用多階段復原動作。第一次嘗試可能會重新啟動應用程式集區、 第二次嘗試可能會重新啟動對應的服務和第三個嘗試可能會重新啟動伺服器。和最後一個嘗試可能會使伺服器離線，如此就不再接受流量。如果所有的這些動作失敗，會將通知傳送給服務台。

如需受管理可用性的相關資訊，請參閱[受管理的可用性](managed-availability-exchange-2013-help.md)。

## 工作負載管理

Exchange 2013工作負載管理包含下列元件：

  - *使用者工作負載管理*是 Exchange Server 2010 的使用者節流功能的新名稱。您可以自訂這些設定根據您的環境所需的需求。

  - *系統工作量管理*'s new for Exchange 2013與用來自動藉由監視關鍵伺服器資源的健康狀況節流特定 Exchange 工作負載。應該只在 Microsoft 客戶服務及支援的方向下自訂這些設定。

如需詳細資訊，請參閱[Exchange 工作負載管理](exchange-workload-management-exchange-2013-help.md)。

## 伺服器健康狀況與效能文件

下表包含可協助您了解並管理伺服器健康狀況與效能Exchange 2013中的主題連結。


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
<td><p><a href="exchange-workload-management-exchange-2013-help.md">Exchange 工作負載管理</a></p></td>
<td><p>了解管理 Exchange 工作負載控制個別使用者耗用資源的方式。</p></td>
</tr>
<tr class="even">
<td><p><a href="managed-availability-exchange-2013-help.md">受管理的可用性</a></p></td>
<td><p>了解Exchange 2013中可用的內建的資源監控和復原動作。</p></td>
</tr>
</tbody>
</table>

