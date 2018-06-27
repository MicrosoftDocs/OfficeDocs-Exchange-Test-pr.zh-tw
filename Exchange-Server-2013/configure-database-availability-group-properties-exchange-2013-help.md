---
title: '設定資料庫可用性群組內容: Exchange 2013 Help'
TOCTitle: 設定資料庫可用性群組內容
ms:assetid: 50daeac5-a16f-4362-a325-19e0fe25d59d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd297985(v=EXCHG.150)
ms:contentKeyID: 50473106
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定資料庫可用性群組內容

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-06-24_

您可以使用 EAC 或命令介面設定資料庫可用性群組 (DAG) 的內容，包含 DAG IP 位址設定以及由 DAG 使用的見證伺服器和見證目錄。命令介面可讓您設定在 EAC 中不可用的 DAG 內容，例如替代見證伺服器以及替代見證目錄資訊、用於複寫的 TCP 連接埠，以及資料中心啟動協調 (DAC) 模式。

## 開始之前有哪些須知？

  - 預估完成時間：1 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [高可用性和站台回復性權限](high-availability-and-site-resilience-permissions-exchange-2013-help.md) 主題中的「資料庫可用性群組」項目。

  - DAG 內容值會儲存在 Active Directory 和叢集資料庫中。但是，某些內容只會儲存在叢集資料庫中。因此，DAG 的基礎叢集必須正在執行並具有仲裁，才能設定下列項目的內容：
    
      - ReplicationPort
    
      - NetworkCompression
    
      - NetworkEncryption
    
      - DiscoverNetworks

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

## 使用 EAC 設定資料庫可用性群組內容

1.  在 EAC 中，移至 \[伺服器\] \> \[資料庫可用性群組\]。

2.  選取要設定的 DAG，然後按一下![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  
    
    使用 \[一般\] 頁面來檢視 DAG 成員與操作狀態，並設定 DAG 的「見證」伺服器、「見證」目錄以及自動網路設定：
    
      - \[見證伺服器\]   DAG 見證伺服器的主機名稱或完整網域名稱 (FQDN) 。雖然此為所有 DAG 都需要的內容，見證伺服器將用於 DAG 成員為偶數，且叢集使用的仲裁模型為節點與檔案共用多數的情況。
    
      - \[見證目錄\]   用於在見證伺服器上儲存見證 .log 檔案的完整目錄路徑。雖然此為所有 DAG 都需要的內容，但見證目錄將僅用於 DAG 見證伺服器使用中時。
    
      - \[可操作伺服器\]   顯示 DAG 成員以及其目前可操作狀態的唯讀欄位。
    
      - \[手動設定資料庫群組網路\]   若您想要手動設定所有 DAG 網路，請選取此方塊。當您保留核取方塊為清除狀態時，系統會根據網路介面設定自動設定 DAG 網路。如果清除此核取方塊， **Set-DatabaseAvailabilityGroupNetwork** 和 **New-DatabaseAvailabilityGroupNetwork** Cmdlet 會停用，不能對 DAG 進行系統管理用途。

4.  
    
    使用 \[IP 位址\] 頁面可檢視和修改指派給 DAG 的 IP 位址：
    
      - 選擇一個現有的 IP 位址然後按一下 ![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示") 進行修改。
    
      - 選擇現有的 IP 位址然後按一下減號圖示 (刪除) 來移除。
    
      - 輸入 IP 位址然後按一下 ![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示") 以新增至 DAG。

5.  
    
    按一下 \[儲存\] 來儲存任何進行的變更。

## 使用命令介面設定資料庫可用性群組內容

本範例將名為 DAG1 的 DAG 的見證目錄設定為 C:\\DAG1DIR。

    Set-DatabaseAvailabilityGroup -Identity DAG1 -WitnessDirectory C:\DAG1DIR

本範例預先設定 DAG DAG1 的替代見證伺服器 CAS3 和替代見證目錄 C:\\DAGFileShareWitnesses\\DAG1.contoso.com。

    Set-DatabaseAvailabilityGroup -Identity DAG1 -AlternateWitnessDirectory C:\DAGFileShareWitnesses\DAG1.contoso.com -AlternateWitnessServer CAS3

此範例會將名為 DAG1 的 DAG 設定為使用動態主機設定通訊協定 (DHCP) 以取得 IP 位址。

    Set-DatabaseAvailabilityGroup -Identity DAG1 -DatabaseAvailabilityGroupIPAddresses 0.0.0.0

本範例將名為 DAG1 的 DAG 設定為使用靜態 IP 位址 10.0.0.8。

    Set-DatabaseAvailabilityGroup -Identity DAG1 -DatabaseAvailabilityGroupIPAddresses 10.0.0.8

本範例以多重靜態 IP 位址設定名為 DAG1 的多重子網路 DAG。

    Set-DatabaseAvailabilityGroup -Identity DAG1 -DatabaseAvailabilityGroupIPAddresses 10.0.0.8,10.0.1.8

本範例針對 DAC 模式設定 DAG DAG1。

    Set-DatabaseAvailabilityGroup -Identity DAG1 -DatacenterActivationMode DagOnly

此範例會將名爲 DAG1 的 DAG 複寫連接埠設定為 63132。

    Set-DatabaseAvailabilityGroup -Identity DAG1 -ReplicationPort 63132

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>變更 DAG 的預設複寫通訊埠後，您必須手動修改 DAG 每個成員上的 Windows 防火牆例外狀況，以允許透過指定通訊埠進行通訊。</td>
</tr>
</tbody>
</table>


## 如何才能了解這是否正常運作？

若要驗證您是否已成功設定 DAG，執行下列操作：

  - 在命令介面中，執行下列命令來顯示 DAG 組態設定並驗證 DAG 已成功設定。
    
        Get-DatabaseAvailabilityGroup <DAGName> | Format-List

## 相關資訊

[建立資料庫可用性群組](create-a-database-availability-group-exchange-2013-help.md)

[移除資料庫可用性群組](remove-a-database-availability-group-exchange-2013-help.md)

[建立資料庫可用性群組網路](create-a-database-availability-group-network-exchange-2013-help.md)

[管理資料庫可用性群組成員資格](manage-database-availability-group-membership-exchange-2013-help.md)

[Get-DatabaseAvailabilityGroup](https://technet.microsoft.com/zh-tw/library/dd351226\(v=exchg.150\))

[Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/zh-tw/library/dd297934\(v=exchg.150\))

