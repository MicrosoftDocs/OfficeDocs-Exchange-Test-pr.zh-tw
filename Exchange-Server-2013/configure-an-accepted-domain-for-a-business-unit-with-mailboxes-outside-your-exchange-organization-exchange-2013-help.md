---
title: '利用 Exchange 組織外部的信箱為業務單位設定公認的網域: Exchange 2013 Help'
TOCTitle: 利用 Exchange 組織外部的信箱為業務單位設定公認的網域
ms:assetid: ff46310b-5392-4eac-97bc-d39d397e1ce1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ657737(v=EXCHG.150)
ms:contentKeyID: 50474668
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 利用 Exchange 組織外部的信箱為業務單位設定公認的網域

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-08-06_

在某些情況下，當某個業務單位在您 Exchange 組織的網域中，全部或部分收件者沒有信箱時，您可能會想為該業務單位設定公認的網域。比如說，當組織在兩個以上不同的電子郵件系統之間共用相同的 SMTP 位址空間時，就有可能發生這種情形。對於這樣的情形，您可將公認的網域設定為內部轉送網域。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱主題中的「公認的網域」[郵件流程權限](mail-flow-permissions-exchange-2013-help.md)項目。

  - 如果您的周邊網路中有訂閱的 Edge Transport Server，則可在 Exchange 組織的 Mailbox Server 上設定公認網域。公認網域組態會在 EdgeSync 同步處理期間複寫至 Edge Transport Server。如需詳細資訊，請參閱[Edge 訂閱](edge-subscriptions-exchange-2013-help.md)。

  - 設定公認的網域之後，必須驗證該 SMTP 命名空間有公用網域名稱系統 (DNS) MX 資源記錄存在，且 MX 資源記錄參照與 Exchange 組織關聯的伺服器名稱及 IP 位址。

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


## 使用 EAC 將公認的網域設定為內部轉送網域

1.  在 EAC 中，瀏覽至 \[郵件流程\] \> \[公認的網域\]，選取要設定的網域，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 \[姓名\] 欄位中輸入公認的網域之顯示名稱。每個組織公認的網域必須有一個唯一的顯示名稱。顯示名稱可能與公認的網域不同。例如，網域 Contoso.com 的顯示名稱可以是 Contoso Local Accepted Domain。

3.  選取 \[內部轉送網域\]。

4.  按一下 **\[儲存\]**。

## 如何知道這是否正常運作？

若要確認是否已成功將公認的網域設定為內部轉送網域，請從內部轉送網域傳送郵件至您 Exchange 組織內的信箱，並確認寄達。

