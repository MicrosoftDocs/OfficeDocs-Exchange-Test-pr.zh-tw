---
title: '設定資料庫可用性群組網路內容: Exchange 2013 Help'
TOCTitle: 設定資料庫可用性群組網路內容
ms:assetid: 41197639-988f-476c-9788-51d5191a7dce
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd297927(v=EXCHG.150)
ms:contentKeyID: 50473085
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定資料庫可用性群組網路內容

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-31_

每一個資料庫可用性群組 (DAG) 網路都具有數個可設定的內容，包含 DAG 網路的名稱、DAG 網路的描述欄位、DAG 網路使用的子網路清單，以及是否為 DAG 網路啟用複寫。

要尋找與 DAG 相關的其他管理工作嗎？請參閱[管理資料庫可用性群組](managing-database-availability-groups-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：1 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [高可用性和站台回復性權限](high-availability-and-site-resilience-permissions-exchange-2013-help.md) 主題中的「資料庫可用性群組」項目。

  - 您可以在已停用自動網路設定的 DAG 時才設定 DAG 網路。如需如何停用自動網路設定 DAG 的詳細步驟，請參閱[設定資料庫可用性群組內容](configure-database-availability-group-properties-exchange-2013-help.md)。

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

## 使用 EAC 設定資料庫可用性群組網路內容

1.  在 EAC 中，移至 \[伺服器\] \> \[資料庫可用性群組\]。

2.  選擇要設定的 DAG，然後在要設定的 DAG 網路下的 \[詳細資料\] 窗格選擇：
    
      - \[停用複寫\] 或 \[啟用複寫\]   設定 DAG 網路的複寫設定。
    
      - **移除**  會移除 DAG 網路。您可以移除 DAG 網路之前，您必須先移除所有相關聯的子網路的 DAG 網路。
    
      - **檢視詳細資料**  設定 DAG 網路內容，例如名稱、 描述與關聯的子網路 DAG 網路。您也可以檢視這些的子網路相關聯的網路介面並啟用或停用的 DAG 網路的複寫。

## 使用命令介面來設定資料庫可用性群組網路內容

此範例會將子網路 10.0.0.0 和子網路遮罩 255.0.0.0 新增至 DAG DAG1 的 DAG 網路 MapiDagNetwork。

    Set-DatabaseAvailabilityGroupNetwork -Subnets 10.0.0.0/8 -Identity DAG1\MapiDagNetwork

## 如何才能了解這是否正常運作？

若要確認您是否已成功設定 DAG 網路，請執行下列操作：

  - 在命令介面中，執行下列命令以顯示 DAG 網路組態設定，並確認 DAG 網路已成功設定。
    
        Get-DatabaseAvailabilityGroupNetwork <DAGNetworkName> | Format-List

## 相關資訊

[Set-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/zh-tw/library/dd298008\(v=exchg.150\))

[Get-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/zh-tw/library/dd297938\(v=exchg.150\))

[New-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/zh-tw/library/dd335225\(v=exchg.150\))

[Remove-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/zh-tw/library/dd298131\(v=exchg.150\))

