---
title: 'Exchange 工作負載管理: Exchange 2013 Help'
TOCTitle: Exchange 工作負載管理
ms:assetid: 276740c4-bdb7-49f1-9470-ae6f2bfd65aa
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ150503(v=EXCHG.150)
ms:contentKeyID: 50472740
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 工作負載管理

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2014-11-16_

Exchange 工作負載為 Exchange Server 功能、通訊協定或明確定義為 Exchange 系統資源管理的服務。每一個 Exchange 工作負載會耗用系統資源，如 CPU、信箱資料庫作業，或 Active Directory 要求，以執行使用者要求或背景工作。Exchange 工作負載的範例包含 Outlook Web App, Exchange ActiveSync、信箱移轉，以及信箱助理員。

您管理 Exchange 工作負載控制 （有時稱為節流 Exchange 2010 中的使用者） 的個別使用者耗用資源的方式。控制個別使用者耗用 Exchange 系統資源的方式已經可能在Exchange Server 2010，並已展開這項功能的Exchange Server 2013。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>藉由監視貴組織中的 Exchange 伺服器上的系統資源的健康狀況管理工作負載只應依據 Microsoft 客戶服務與支援部門。</td>
</tr>
</tbody>
</table>


## 藉由控制個別使用者耗用資源的方式來管理工作負載

已增強 Exchange 2013 中的節流功能。增強的功能有助於確定由個別使用者過度耗用的資源，不會對伺服器效能或使用者體驗產生不良影響。

根據預設，使用者節流Exchange 2013中可讓使用者沒有發生任何減少的頻寬增加資源已消耗簡短的期間。此外，使用非常大量資源的使用者完成鎖定將非經常性、 或永遠不會發生。而非完全封鎖使用者執行作業，節流發生和處理程序的延遲的短期的時間 （想像其為"microdelays"），其造成重要影響的伺服器上之前發生。

**功能重點**

對於 Exchange 控制個別使用者在 Exchange 2013 中如何耗用資源的方式有幾個重點：

  - **允許高載**    允許高載可讓使用者進行短期增加資源耗用，而無須經歷任何節流。

  - **補給速率**    補給速率藉由使用資源預算系統管理使用者的資源。您可以設定補給使用者資源預算的速率。例如，600,000 的值 (以毫秒為單位) 意味著使用者預算會以每小時十分鐘用量的速率補給。

  - **流量管制**    當使用者的資源使用狀況在一段時間後達到設定的限制，則該使用者會在對伺服器造成顯著影響之前，延遲一段短時間。使用者通常不會注意到這些 "microdelays"。此程序可讓 Exchange 2013 有效地管制流量，而不必阻止使用者生產。流量管制比起提前鎖定，對使用者的影響較小，並且明顯降低了發生鎖定的機會。

  - **最大使用量**    在極少情況下，使用者會在短時間內消耗極大量的資源。為了預防起見，達到最大使用量閾值的使用者會暫時無法使用資源。暫時無法使用資源的使用者會在補給使用量預算之後，盡快解除封鎖。

如指令程式可用來控制個別使用者耗用資源的方式的清單，請參閱本主題稍後的"指令程式來控制個別使用者如何使用資源"。

**Exchange 2013 節流功能與部署考量**

無論您是執行 Exchange 2013 的解除安裝，還是將 Exchange 2013 安裝至包含 Exchange 2010 的共存環境中，在執行 Exchange 2013 的電腦上，會利用新的 Exchange 2013 節流功能來節流所有具備信箱的使用者。不過，當使用者透過 Exchange 2010 用戶端存取伺服器存取信箱時，Exchange 2010 會藉由 Exchange 2010 節流功能保持節流。

當 Exchange 2013 已安裝至共存環境時，Exchange 2013 安裝程序可能會嘗試繼續進行某些您已在 Exchange 2010 組態中設定的節流設定。但是，Exchange 2013 節流功能大有不同，以至於任何舊的節流設定的作用通常不會影響 Exchange 2013 中執行節流的方式。

**利用範圍管理節流原則**

類似 Exchange 2010，Exchange 2013 中有一個單一預設節流原則。在 Exchange 2013 中，預設節流原則稱為 **GlobalThrottlingPolicy**。此原則具有 **Global** 範圍。其他可用的使用者節流範圍為 **Organization** 與 **Regular**。由於推出 Exchange 2013 使用者節流原則的範圍指派，管理節流原則的方式與在 Exchange 2010 中有所不同。除非您已組織的節流原則，否則 **GlobalThrottlingPolicy** 會對於組織中每一個新的現有使用者，定義基準預設節流設定。在許多一般的 Exchange 部署案例中，**GlobalThrottlingPolicy** 將會適當地管理使用者。

強烈建議不要修改 **GlobalThrottlingPolicy** 來自訂節流設定。相反的，您應該建立其他節流原則。建立其他節流原則可幫助您更好地管理工作負載。同時也可在未來 Exchange 2013 更新時，防止節流原則設定的修改被覆寫。

若要自訂適用於組織中所有使用者的節流設定，請利用範圍指派 **Organization** 來新建節流原則。在新的 Organization 範圍原則中，您應該只設定與 **GlobalThrottlingPolicy** 之設定不同的節流設定。若要自訂適用於組織中特定使用者的節流設定，請利用範圍指派 **Regular** 新建節流原則。在新的 Regular 範圍原則中，您應該只設定與 **GlobalThrottlingPolicy** 之設定不同的節流設定，以及其他組織原則。這有助於從 **GlobalThrottlingPolicy** 繼承剩餘的原則設定，並且可讓您從未來 Exchange 更新所新增之節流原則的任何更新受惠。

## 管理工作負載節流設定

利用 Exchange 管理命令介面管理 Exchange 工作負載節流設定。

**控制個別使用者如何使用資源的指令程式**

請利用 Exchange 2010 推出的以下指令程式管理節流設定：

管理節流原則

  - [Get-ThrottlingPolicy](https://technet.microsoft.com/zh-tw/library/dd351264\(v=exchg.150\))

  - [New-ThrottlingPolicy](https://technet.microsoft.com/zh-tw/library/dd351045\(v=exchg.150\))

  - [Remove-ThrottlingPolicy](https://technet.microsoft.com/zh-tw/library/dd351178\(v=exchg.150\))

  - [Set-ThrottlingPolicy](https://technet.microsoft.com/zh-tw/library/dd298094\(v=exchg.150\))

指派節流原則

  - [Get-ThrottlingPolicyAssociation](https://technet.microsoft.com/zh-tw/library/ff459241\(v=exchg.150\))

  - [Set-ThrottlingPolicyAssociation](https://technet.microsoft.com/zh-tw/library/ff459231\(v=exchg.150\))

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>*-ResourcePolicy</strong>、 <strong>*-WorkloadManagementPolicy</strong>及<strong>*-WorkloadPolicy</strong>系統工作負載管理指令程式已被取代。應該只在 Microsoft 客戶服務及支援的方向下自訂系統工作負載管理設定。</td>
</tr>
</tbody>
</table>

