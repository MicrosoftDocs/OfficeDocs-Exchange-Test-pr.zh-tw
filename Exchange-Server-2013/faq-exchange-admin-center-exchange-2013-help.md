---
title: '常見問題集： Exchange 系統管理中心: Exchange 2013 Help'
TOCTitle: 常見問題集： Exchange 系統管理中心
ms:assetid: 3de0042f-74a6-458f-947c-3cd6eeacd6ab
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ552409(v=EXCHG.150)
ms:contentKeyID: 50472936
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 常見問題集： Exchange 系統管理中心

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

本主題提供的新 Exchange 系統管理中心 (EAC) 中 Microsoft Exchange Server 2013常見問題集的清單。有其他疑問 EAC 未回應以下吗？電子郵件至 ex2013helpfeedback 在[Ex2013HelpFeedback@microsoft.com](mailto:ex2013helpfeedback@microsoft.com)。

## 開發察覺 Exchange Online 的 EAC 吗？

EAC 做所有Exchange 2013，包括要部署在內部、 Exchange Online、 或混合式部署與雲端中的客戶的部署選項。

## 因為您正在建立之介面的主要針對小型和中型客戶未移除 Exchange 管理主控台 (EMC) 吗？

EAC 能夠針對所有的客戶提供單一、 直覺式管理經驗及旨在協助簡化執行的最常見的管理工作。

我們建立單一介面透過 Exchange 管理主控台 (EMC) 與 Exchange 控制台 (ECP) 和一個定址重要的挑戰與案例的客戶提供更多的案例涵蓋範圍。

此外，我們聆聽各種規模的客戶而且其主要考量下列：

  - 維護及操作系統管理工具才能下載修補程式是作業負荷的客戶它會依次增加營運成本。

  - IT 人力變成逐漸行動裝置，為客戶想要能夠從任何地方、 不只從桌面和其系統管理工具安裝所在的伺服器管理其環境。

  - 使用多個工具不同的部署選項會變成費解並增加訓練與操作成本

## 是 PowerShell 記錄和 EAC 回傳入的指令程式衝擊吗？

我們已在此採取早期客戶意見，而所評估的未來更新中處理這可能性。

## 將 EMC 會重新引入即將來臨的 service pack 吗？

\[否\]。我們完全支援 EAC 經驗。

## 您可以使用 Exchange 2010 EMC 來管理 Exchange 2013 物件吗？

\[否\]。您無法使用 Exchange 2010 EMC 管理Exchange 2013物件與伺服器。雖然客戶升級至Exchange 2013，我們鼓勵他們能夠使用 EAC：

1.  管理Exchange 2013信箱、 伺服器及對應的服務。

2.  檢視並更新 Exchange 2010 信箱和屬性。

3.  檢視並更新 Exchange 2007 信箱和屬性。

我們鼓勵使用 Exchange 2010 EMC 來建立及管理 Exchange 2010 信箱的客戶。

我們鼓勵使用 Exchange 2007 EMC 來建立及管理 Exchange 2007 信箱的客戶。

客戶可以繼續執行管理工作使用 Exchange 管理命令介面與指令碼的工作。

## 為什麼要選擇看不到 \[搜尋\] 方塊中一律？

針對Exchange 2013我們設計準則的一部分，我們想要協助確定 nothing 您方式直到您需要它。此簡化了程序被表示在所有 （包括 EAC） 我們使用者體驗。在搜尋方塊投影片出後按一下圖示\]。此提供更多空間給使用者在 \[文字\] 方塊中輸入查詢，同時也提供 \[顯示即時查詢比對發生之後的類型清單。這項改進功能可讓我們沒有降低管理經驗隱藏不必要的複雜性。我們會繼續增強所有根據意見反應我們體驗。

## 平板電腦是否將 EAC 中運作吗？

透過平板電腦與行動裝置管理不支援這一次。

## 為什麼沒有 Exchange 2010 ECP 開啟當我嘗試存取 Exchange 2013 EAC？

如果您的信箱存在的 Exchange 2010 信箱伺服器，Exchange 2010 ECP 會自動載入在瀏覽器中。這是根據設計。您可以存取 EAC 中新增的 Exchange 版本的 url。例如，若要存取的 EAC 中之虛擬目錄架設在 Client Access server CAS01 NA，使用下列 URL： `https://CAS01-NA/ecp?ExchClientVer=15`。

## 如何限制可使用 EAC 的？

若要限制網際網路與內部網路存取，Exchange 會提供分割在 IIS 中的虛擬目錄層級。系統管理員可以明確允許或拒絕 IT 管理案例 （例如，從未加入網域內公司防火牆用戶端） 的外部網際網路用戶端正在執行。如需詳細資訊，請參閱[關閉 Exchange 系統管理中心存取](turn-off-access-to-the-exchange-admin-center-exchange-2013-help.md)。

## 變更功能的 Exchange 2013 工具箱

在 Exchange 2007 和 Exchange 2010，EMC 所包含的工具箱\] 中，提供各種工具存取的 Exchange 組織管理。Exchange 2013 工具箱許多精簡從舊的版本。詳細資料範本編輯器、 遠端連線分析程式、 及佇列檢視器均仍然可以使用 Exchange 2013 工具箱中。其餘工具已可用於其他目的或移至 EAC。

下表列出在 Exchange 2013 工具箱變更：


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>工具</th>
<th>其中現在是？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Best Practices Analyzer (ExBPA)</p></td>
<td><p>ExBPA 已遭淘汰。整備檢查已取代以確定您的 Active Directory 樹系與 Exchange 伺服器準備好讓 Exchange 2013 ExBPA。每個整備] 核取主題說明以解決問題的發現整備檢查執行的時間所能採取的動作。您應該只執行如果在安裝期間所顯示的整備] 核取整備] 核取主題中所述的步驟。</p></td>
</tr>
<tr class="even">
<td><p>郵件流程疑難排解員</p></td>
<td><p>郵件流程疑難排解員已遭淘汰。您現在可以在 EAC 中使用的郵件追蹤功能。移至 [<strong>郵件流程</strong>&gt;<strong>傳遞回報</strong>。</p></td>
</tr>
<tr class="odd">
<td><p>效能監視器</p></td>
<td><p>從 [工具箱] 中已遭淘汰效能監視器。您仍然可以在 Windows Server 2008 和 Windows Server 2012 中找到 [<strong>系統管理工具]</strong>下的效能監視器。</p></td>
</tr>
<tr class="even">
<td><p>效能疑難排解員</p></td>
<td><p>效能疑難排解員已遭淘汰從 [工具箱]。</p></td>
</tr>
<tr class="odd">
<td><p>路由記錄檢視器</p></td>
<td><p>路由記錄檢視器已遭淘汰。</p></td>
</tr>
<tr class="even">
<td><p>公用資料夾管理主控台</p></td>
<td><p>從 EAC 中現在管理公用資料夾。在 EAC 中，移至 [<strong>公用資料夾</strong>。</p></td>
</tr>
<tr class="odd">
<td><p>角色型存取控制 (RBAC) 使用者編輯器</p></td>
<td><p>從 EAC 中現在管理 RBAC。在 EAC 中，移至 [<strong>權限</strong>。</p></td>
</tr>
</tbody>
</table>

