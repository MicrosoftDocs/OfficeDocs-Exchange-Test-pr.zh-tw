---
title: '建立資料庫可用性群組網路: Exchange 2013 Help'
TOCTitle: 建立資料庫可用性群組網路
ms:assetid: 6caec7be-788a-4058-87a7-f31c575b870c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd298051(v=EXCHG.150)
ms:contentKeyID: 50473442
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 建立資料庫可用性群組網路

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-11-02_

必要時，您可以建立其他網路使用的資料庫可用性群組 (DAG) 中。您可以使用 EAC 或命令介面來建立 DAG 網路。

要尋找與 DAG 相關的其他管理工作嗎？請參閱[管理資料庫可用性群組](managing-database-availability-groups-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：1 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [高可用性和站台回復性權限](high-availability-and-site-resilience-permissions-exchange-2013-help.md) 主題中的「資料庫可用性群組」項目。

  - 您可以在只有在已停用自動網路設定的 DAG 時建立的 DAG 網路。如需如何停用自動網路設定 DAG 的詳細步驟，請參閱[設定資料庫可用性群組內容](configure-database-availability-group-properties-exchange-2013-help.md)。

  - 建立 DAG 網路，您必須指派不使用另一個 DAG 網路的唯一子網路。如果您使用指派給現有的 DAG 網路子網路，他們會移除該 DAG 網路並新增至新建立的 DAG 網路。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

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


## 您要執行的工作

## 使用 EAC 來建立資料庫可用性群組網路

1.  在 EAC 中，移至 \[伺服器\] \> \[資料庫可用性群組\]。

2.  選取要設定的 DAG，然後按一下 ![加入 DAG 網路](images/Dd298051.befcdc4e-7f7a-451d-a0a8-608c79f5d186(EXCHG.150).gif "加入 DAG 網路")。

3.  
    
    在 \[新增資料庫可用性群組\] 頁面上，提供下列資訊：
    
      - **資料庫可用性群組網路名稱**   使用此欄位為該網路輸入一個在 DAG 中具唯一性的名稱。
    
      - **說明**   使用此欄位提供 DAG 網路的文字說明。
    
      - **子網路**  使用這個欄位可以建立一個或多個子網路與 DAG 網路的關聯。按一下 \[新增子網路，並按一下 \[編輯的子網路與按一下減號 （-） 中移除子網路的![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示") 。

4.  按一下 \[儲存\] 建立 DAG 網路。

## 使用命令介面來建立資料庫可用性群組網路

本範例會建立網路 ReplicationDagNetwork02 10.0.0.0 的子網路與 8 DAG DAG1 中的位元遮罩。複寫已啟用的網路，並也新增網路的選用描述。

    New-DatabaseAvailabilityGroupNetwork -DatabaseAvailabilityGroup DAG1 -Name ReplicationDagNetwork02 -Description "Replication network 2" -Subnets 10.0.0.0/8 -ReplicationEnabled:$True

## 如何才能了解這是否正常運作？

若要確認是否已成功建立 DAG 網路，請執行下列其中一項操作：

  - 在 EAC 中，瀏覽至 \[**伺服器**\>**資料庫可用性群組**。選取適當的 DAG，並在詳細資料窗格中會顯示新建立的 DAG 網路。

  - 在命令介面中，執行下列命令來驗證是否已建立 DAG 網路並顯示 DAG 網路的組態資訊。
    
        Get-DatabaseAvailabilityGroupNetwork <DAGNetworkName> | Format-List

## 相關資訊

[Set-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/zh-tw/library/dd298008\(v=exchg.150\))

[Get-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/zh-tw/library/dd297938\(v=exchg.150\))

[New-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/zh-tw/library/dd335225\(v=exchg.150\))

[Remove-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/zh-tw/library/dd298131\(v=exchg.150\))

