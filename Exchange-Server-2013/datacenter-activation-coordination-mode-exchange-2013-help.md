---
title: '資料中心啟動協調模式: Exchange 2013 Help'
TOCTitle: 資料中心啟動協調模式
ms:assetid: 57e4bf22-eeae-42a5-beb3-d68d06489592
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd979790(v=EXCHG.150)
ms:contentKeyID: 50473243
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 資料中心啟動協調模式

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-07-14_

資料中心啟動協調 (DAC) 模式為資料庫可用性群組 (DAG) 的屬性。DAC 模式預設為停用但應啟用的所有 Dag 使用連續複寫的兩個或多個成員。不應該啟用使用協力廠商複寫模式，除非和協力廠商所指定的 Dag 的 DAC 模式。

DAC 模式用來控制啟動行為的 DAG 裝載資料庫。此控制項的設計避免 split brain 資料中心容錯回復期間發生資料庫層級。Split brain，又稱為 split brain syndrome，就會導致資料庫複製的相同 DAG 無法進行通訊的兩個成員上所裝載為作用中副本的條件。Split brain 都將無法使用 DAC 模式，因為 DAC 模式需要取得之前可以加以裝載裝載資料庫的權限的 DAG 成員。

例如，請考慮出主要資料中心包含兩個 DAG 成員與見證伺服器和第二個資料中心包含兩個其他 DAG 成員的案例。在此案例中，DAG 不處於 DAC 模式。主要資料中心失去電源，讓您啟用的 DAG 中的第二個資料中心。最後還原至主要資料中心的電源，並中有電源失敗之前的仲裁、 的主要資料中心的 DAG 成員會啟動其資料庫裝載。因為主要資料中心已還原沒有網路連線到第二個資料中心，而且 DAG 使用中的資料庫因為 DAG 不處於 DAC 模式中，輸入 split brain 條件。

## DAC 模式的運作方式

若要避免發生包括呼叫資料中心啟動協調通訊協定 (DACP) 通訊協定 split brain 設計 DAC 模式。啟用 DAC 模式時，DAG 成員不會自動資料庫裝載即使有仲裁。而是 DACP 用於判斷 DAG 和 Active Manager 是否應該嘗試將裝載資料庫的目前狀態。

您想像的 DAC 模式的仲裁應用程式層級的掛載資料庫。了解 DACP 及其運作方式的用途，請務必了解它已經是要處理的主要案例。請考慮的兩個資料中心的案例。假設在主要資料中心有電力完全中斷。此事件，在所有伺服器和 WAN 都是向下，讓組織會啟用待命資料中心的決策。幾乎所有這類的復原案例、 power 還原至主要資料中心時, 的 WAN 連線通常不會立即還原。這表示主要資料中心的 DAG 成員會 power，但他們不能與啟動待命資料中心的 DAG 成員通訊。主要資料中心應一律包含讓大多數 DAG 仲裁投票，這表示 power 還原時，即使在 WAN 連線至 DAG 成員待命資料中心，如果沒有在主要資料中心的 DAG 成員具有多數 」與因此有仲裁。這是問題因為仲裁，與這些伺服器可以裝載及其資料庫，接下來將會導致分歧現在裝載實際現用資料庫中的啟用待命資料中心。

建立 DACP 時若要解決此問題。Active Manager 會儲存在有點中會告知 DAG 已指派為 \[作用中的伺服器上的本機資料庫裝載至來允許的記憶體 （以 0 或 1）。當 DAG 處於 DAC 模式執行時，每次 Active Manager 啟動設定位元設定為 0，這表示它不允許裝載資料庫。由於處於 DAC 模式時，伺服器必須嘗試與該知道要取得以授與其來加以指派給它為作用中的本機資料庫可以裝載是否解答的另一個 DAG 成員的 dag 的所有其他成員通訊。回覆而言位元設定為其他作用中的管理員 DAG 中的表單中。如果另一部伺服器的回應其位元設為 1，就表示允許伺服器裝載資料庫，因此開始的伺服器將其位元設定為 1 並裝載資料庫。

但時您復原在主要資料中心電源中斷所在之伺服器的復原但未還原 WAN 連線，在主要資料中心的 DAG 成員的所有都有 DACP 位元的值為 0;與因此無開始備份復原的主要資料中心伺服器要裝載資料庫，因為不可以與彼此通訊的 DAG 成員的有 DACP 位元的值是 1。

## 具有兩個成員的 Dag 的 DAC 模式

具有兩個成員 Dag 具有防止位元單獨 DACP 完全保護對應用程式層級 split brain syndrome 的固有限制。針對具有兩個成員 Dag、 DAC 模式也會使用 DAG 的見證伺服器啟動時間來判斷其是否可在啟動時裝載資料庫。見證伺服器啟動時間是相較於 DACP 位元設定為 1 時的時間。

  - 系統的 DACP 位元已設定的時間早於見證伺服器啟動時間時，假設 DAG 成員與見證伺服器已同時重新開機 （或許由於 power 遺失主要資料中心），而且 DAG 成員不允許 mou 的來源nt 資料庫。

  - 如果 DACP 位元已設定的時間會比見證伺服器開機時間近，系統會假設 DAG 成員已重新開機因任何原因 (或許排定的維護已執行或許系統損毀或 power 中斷遺失 isolated 至 DAG 成員)，與 DAG 成員可裝載資料庫。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>因為見證伺服器的啟動時間用於判斷 DAG 成員是否可以在啟動時裝載作用中的資料庫，您應該永遠不重新啟動見證伺服器和唯一的 DAG 成員在同一時間。這麼可能會保持在其中它不能裝載狀態的 DAG 成員的資料庫上啟動。如果發生這種情況，您必須執行<a href="https://technet.microsoft.com/zh-tw/library/dd351169(v=exchg.150)">Restore-DatabaseAvailabilityGroup</a>指令程式在 DAG。這會重設為 DACP 元並允許 DAG 成員來裝載資料庫。</td>
</tr>
</tbody>
</table>


## 其他的 DAC 模式的優點

除了防止 split brain syndrome 應用程式層級、 DAC 模式也會啟用使用內建的站台恢復能力 cmdlet 用來執行資料中心轉換。這些包括下列：

  - [Stop-DatabaseAvailabilityGroup](https://technet.microsoft.com/zh-tw/library/dd335133\(v=exchg.150\))

  - [Restore-DatabaseAvailabilityGroup](https://technet.microsoft.com/zh-tw/library/dd351169\(v=exchg.150\))

  - [Start-DatabaseAvailabilityGroup](https://technet.microsoft.com/zh-tw/library/dd335076\(v=exchg.150\))

執行資料中心轉換的 Dag 不處於 DAC 模式包括使用Exchange工具和叢集管理工具的組合。如需詳細資訊，請參閱[資料中心轉換](datacenter-switchovers-exchange-2013-help.md)。

## 啟用 DAC 模式

只能透過使用Exchange管理命令介面可啟用 DAC 模式。特別是，您可以使用[Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/zh-tw/library/dd297934\(v=exchg.150\))指令程式來啟用 DAC 模式下面範例所示。

    Set-DatabaseAvailabilityGroup -Identity DAG2 -DatacenterActivationMode DagOnly

在上述範例中，DAG2 為啟用 DAC 模式。

如需啟用 DAC 模式的詳細資訊，請參閱[設定資料庫可用性群組內容](configure-database-availability-group-properties-exchange-2013-help.md)和[Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/zh-tw/library/dd297934\(v=exchg.150\))。

