---
title: '執行伺服器轉換: Exchange 2013 Help'
TOCTitle: 執行伺服器轉換
ms:assetid: ffcefd56-b0a0-4229-9011-fff4197b7c74
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd298187(v=EXCHG.150)
ms:contentKeyID: 62523865
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 執行伺服器轉換

 

_**適用版本：**Exchange Server 2013 SP1_

_**上次修改主題的時間：**2014-06-23_

執行伺服器轉換工作，可以將所有作用中信箱資料庫複本從目前的信箱伺服器移動到資料庫可用性群組 (DAG) 中一或多個其他信箱伺服器。此工作屬於為目前的信箱伺服器排定之中斷的準備工作的一部分。

## 開始之前有哪些須知？

  - 預估完成時間：每個資料庫 30 秒

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [高可用性和站台回復性權限](high-availability-and-site-resilience-permissions-exchange-2013-help.md)主題中的「資料庫可用性群組」項目。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 使用 EAC 執行伺服器轉換

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [高可用性和站台回復性權限](high-availability-and-site-resilience-permissions-exchange-2013-help.md)主題中的「信箱資料庫副本」項目。

1.  在 EAC 中，移至 \[伺服器\] \> \[伺服器\]。

2.  選取想要轉換的信箱伺服器。

3.  在詳細資料窗格中，選取 \[伺服器轉換\]。

4.  在 \[伺服器轉換\] 頁面上，執行下列其中一個動作：
    
    1.  接受 \[自動選擇目標伺服器\] 的預設設定 (在此情況下，系統會自動為每個要轉換的資料庫選取最佳的信箱伺服器)，然後按一下 \[儲存\]。
    
    2.  依序按一下 \[使用指定的伺服器作為切換目標\]、\[瀏覽\] 以選取信箱伺服器，然後按一下 \[儲存\]。

5.  當轉換完成時，按一下 \[關閉\] 以結束 \[伺服器轉換\] 頁面。

## 使用命令介面執行伺服器轉換

本範例執行名為 MBX1 之伺服器的伺服器轉換。系統會為 MBX1 上的每個作用中資料庫自動選取最佳的信箱伺服器。

    Move-ActiveMailboxDatabase -Server MBX1

本範例執行名為 MBX4 之信箱伺服器的伺服器轉換。當命令完成時，MBX5 會裝載先前於 MBX4 上作用的資料庫主動複本。

    Move-ActiveMailboxDatabase -Server MBX4 -ActivateOnServer MBX5

如需詳細的語法及參數資訊，請參閱 [Move-ActiveMailboxDatabase](https://technet.microsoft.com/zh-tw/library/dd298068\(v=exchg.150\))。

