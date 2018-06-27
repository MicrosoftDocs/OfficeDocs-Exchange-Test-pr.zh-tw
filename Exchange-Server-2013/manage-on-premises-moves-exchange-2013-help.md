---
title: '管理內部移動: Exchange 2013 Help'
TOCTitle: 管理內部移動
ms:assetid: 1691b658-f5af-49c6-9170-5c3cb66c7306
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ150487(v=EXCHG.150)
ms:contentKeyID: 50472633
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理內部移動

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2013-02-25_

將信箱從一個信箱資料庫移至另一個程序是移動要求。本機移動要求為此時間內的單一樹系的信箱移動。在 Microsoft Exchange Server 2013、 信箱和個人封存信箱可位於不同的資料庫。使用移動要求功能，您可以移動主要信箱和相關聯的封存至相同的資料庫或分離類。本主題中的程序可協助您在內部部署信箱移動。

使用下列程序將內部部署組織中的信箱移動。這些程序使用 Exchange 管理命令介面和 Exchange 管理中心 (EAC)。

當您使用移動要求來移動信箱時，移動要求會由以下兩個服務來處理：

  - Microsoft Exchange 信箱複寫服務

  - Microsoft Exchange 信箱複寫 Proxy

如需信箱複寫伺服器和 Proxy 的詳細資訊，請參閱[深入了解 MRS Proxy](https://technet.microsoft.com/zh-tw/library/jj156451\(v=exchg.150\))。

如需信箱移動的相關資訊，請參閱[在 Exchange 2013 移動信箱](mailbox-moves-in-exchange-2013-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 完成每項程序預估時間： 20 分鐘

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「信箱移動與移轉權限」項目。

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


## 您要執行的工作

## 測試信箱是否準備好可以移動

此範例會使用*WhatIf*參數測試 Tony Smith 之信箱是否已準備好要移至新的資料庫 DB01 和是否有任何命令中的錯誤。當您使用*WhatIf*參數時，系統會執行信箱上的檢查。如果信箱不是準備好要移動，您會收到錯誤。

    New-MoveRequest -Identity 'tony@alpineskihouse.com' -TargetDatabase DB01 -WhatIf

如需詳細的語法及參數資訊，請參閱 [New-MigrationBatch](https://technet.microsoft.com/zh-tw/library/jj219166\(v=exchg.150\)) 與 [New-MoveRequest](https://technet.microsoft.com/zh-tw/library/dd351123\(v=exchg.150\))。

## 建立本機移動要求

## 使用 EAC 建立本機移動要求

若要建立本機移動要求，請登入 EAC 並執行下列步驟：

1.  在 EAC 中瀏覽至\[收件者\] \>\[遷移\]，然後按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

2.  在 \[新本機信箱移動精靈\] 中，選取您想要移動的使用者，按一下 \[確定\] 後再按一下 \[下一步\]。

3.  在 \[**移動組態**\] 頁面上，指定新的批次的名稱。選取您要用於封存信箱與信箱資料庫位置並按一下 \[**新增**\] 的選項。

## 使用命令介面建立本機移動要求

如需如何建立本機移動要求的範例，請參照[New-MoveRequest](https://technet.microsoft.com/zh-tw/library/dd351123\(v=exchg.150\))中的範例 2。

## 如何才能了解這是否正常運作？

若要確認您是否已成功完成遷移，執行下列操作：

  - 在 EAC 中，瀏覽至 \[收件者\] \> \[遷移\]。

  - 在 EAC 中驗證您是否已成功移動，按一下 \[所有批次的狀態\]。

  - 從介面執行下列命令，以擷取信箱移動資訊。
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

如需詳細資訊，請參閱 [Get-MigrationUserStatistics](https://technet.microsoft.com/zh-tw/library/jj218695\(v=exchg.150\))。

## 建立批次移動要求

## 使用 EAC 建立批次移動要求

登入到 EAC 並執行下列步驟：

1.  在 EAC 中瀏覽至\[收件者\] \>\[遷移\]，然後按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

2.  在 \[新本機信箱移動精靈\] 中，選取您想要移動的使用者，按一下 \[確定\] 後再按一下 \[下一步\]。

3.  在 \[**移動組態**\] 頁面上，指定新的批次的名稱。選取您要用於封存信箱與信箱資料庫位置並按一下 \[**新增**\] 的選項。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>請確定您不設定不正確的項目限制為 50 個以上的項目。如果您不要移動可能會失敗。如果您想要設定不正確的項目限制 50 個以上的項目，您必須使用Exchange管理命令介面和設定 –<em>AcceptLargeDataLoss</em>參數設為 true。</td>
</tr>
</tbody>
</table>


## 使用命令介面建立批次移動要求

此範例會建立指定之的.csv 檔案的信箱移動至不同的信箱資料庫的本機移動遷移批次。此.csv 檔案包含單一欄包含每個要移動的信箱的電子郵件地址。**EmailAddress**檔案名稱為此資料行的標題。必須手動啟動遷移批次在此範例使用**Start-MigrationBatch**指令程式或 Exchange 系統管理中心 (EAC)。或者，您可以使用*AutoStart*參數為自動啟動遷移批次。

    New-MigrationBatch -Local -Name LocalMove1 -CSVData ([System.IO.File]::ReadAllBytes("C:\Users\Administrator\Desktop\LocalMove1.csv")) -TargetDatabases MBXDB2 -TimeZone "Pacific Standard Time"

    Start-MigrationBatch -Identity LocalMove1

如需詳細的語法及參數資訊，請參閱 [New-MigrationBatch](https://technet.microsoft.com/zh-tw/library/jj219166\(v=exchg.150\)) 與 [Start-MigrationBatch](https://technet.microsoft.com/zh-tw/library/jj219165\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要確認您是否已成功完成遷移，執行下列操作：

  - 在 EAC 中驗證您是否已成功移動，按一下 \[所有批次的狀態\]。

  - 從介面執行下列命令，以擷取信箱移動資訊。
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

如需詳細資訊，請參閱 [Get-MigrationUserStatistics](https://technet.microsoft.com/zh-tw/library/jj218695\(v=exchg.150\))。

## 顯示遷移批次

如需如何使用命令介面來顯示遷移批次的範例，請參閱 [Get-MigrationBatch](https://technet.microsoft.com/zh-tw/library/jj219164\(v=exchg.150\))中的範例 2。

## 只移動使用者的主要信箱

## 使用 EAC 即可只移動使用者的主要信箱

1.  在 EAC 中瀏覽至\[收件者\] \>\[遷移\]，然後按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

2.  在 \[新本機信箱移動精靈\] 中，選取您想要移動的使用者主要信箱，按一下 \[確定\] 後再按一下 \[下一步\]。

3.  在 \[**移動組態**\] 頁面上，指定新的批次的名稱。選取 \[**移動主要信箱僅**、 選取您要針對信箱資料庫位置的選項，然後按一下 \[**新增\]**。

## 使用命令介面即可只移動使用者的主要信箱

本範例會將 Tony Smith 之主要信箱移至 DB01。封存並未移動。

    New-MoveRequest -Identity 'tony@alpineskihouse.com' -PrimaryOnly -TargetDatabase "DB01"

如需詳細的語法及參數資訊，請參閱 [New-MoveRequest](https://technet.microsoft.com/zh-tw/library/dd351123\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要確認您是否已成功完成遷移，執行下列操作：

  - 在 EAC 中，按一下 \[所有批次的狀態\]。

  - 從介面執行下列命令，以擷取信箱移動資訊。
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

如需詳細資訊，請參閱 [Get-MigrationUserStatistics](https://technet.microsoft.com/zh-tw/library/jj218695\(v=exchg.150\))。

## 使用 .csv 批次檔案來建立跨樹系移動

此範例可設定遷移端點，並使用 .csv 檔案從來源樹系將跨樹系批次移動建立到目標樹系。

    New-MigrationEndpoint -Name Fabrikam -ExchangeRemote -Autodiscover -EmailAddress tonysmith@fabrikam.com -Credentials (Get-Credential fabrikam\tonysmith) 
    
    $csvData=[System.IO.File]::ReadAllBytes("C:\Users\Administrator\Desktop\batch.csv")
    New-MigrationBatch -CSVData $csvData -Timezone "Pacific Standard Time" -Name FabrikamMerger -SourceEndpoint Fabrikam -TargetDeliveryDomain "mail.contoso.com"

如需更多關於準備跨樹系移動的樹系資訊，請參閱以下主題：

  - [準備跨樹系移動要求的信箱](prepare-mailboxes-for-cross-forest-move-requests-exchange-2013-help.md)

  - [準備使用程式碼範例的跨樹系移動信箱](prepare-mailboxes-for-cross-forest-moves-using-sample-code-exchange-2013-help.md)

  - [使用命令介面中準備 MoveRequest.ps1 指令碼的跨樹系移動準備信箱](prepare-mailboxes-for-cross-forest-moves-using-the-prepare-moverequest-ps1-script-in-the-shell-exchange-2013-help.md)

如需詳細的語法及參數資訊，請參閱 [New-MigrationBatch](https://technet.microsoft.com/zh-tw/library/jj219166\(v=exchg.150\)) 與 [New-MoveRequest](https://technet.microsoft.com/zh-tw/library/dd351123\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要確認您是否已成功完成遷移，執行下列操作：

  - 從介面執行下列命令，以擷取信箱移動資訊。
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

如需詳細資訊，請參閱 [Get-MigrationUserStatistics](https://technet.microsoft.com/zh-tw/library/jj218695\(v=exchg.150\))。

## 僅移動封存信箱

## 使用 EAC 即可僅移動封存信箱

1.  在 EAC 中瀏覽至\[收件者\] \>\[遷移\]，然後按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

2.  在 \[新本機信箱移動精靈\] 中，選取您想要移動的使用者封存信箱，按一下 \[確定\] 後再按一下 \[下一步\]。

3.  在 \[**移動組態**\] 頁面上，指定新的批次的名稱。選取 \[**將只封存信箱移動**、 選取您要針對信箱資料庫位置的選項，然後按一下 \[**新增\]**。

## 使用命令介面即可僅封存信箱

本範例會將 Tony Smith 的封存信箱移至 DB03。不移動主要信箱。

    New-MoveRequest -Identity 'tony@alpineskihouse.com' -ArchiveOnly -ArchiveTargetDatabase "DB03"

如需詳細的語法及參數資訊，請參閱 [New-MigrationBatch](https://technet.microsoft.com/zh-tw/library/jj219166\(v=exchg.150\)) 與 [New-MoveRequest](https://technet.microsoft.com/zh-tw/library/dd351123\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要確認您是否已成功完成遷移，執行下列操作：

  - 從介面執行下列命令，以擷取信箱移動資訊。
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

如需詳細資訊，請參閱 [Get-MigrationUserStatistics](https://technet.microsoft.com/zh-tw/library/jj218695\(v=exchg.150\))。

## 將使用者的主要信箱和封存信箱移至不同的資料庫

此範例會將 Ayla 的主要信箱和封存信箱來分隔的資料庫。主要資料庫移至 DB01、 及封存會移至 DB03。

    New-MoveRequest -Identity 'ayla@humongousinsurance.com' -TargetDatabase DB01 -ArchiveTargetDatabase -DB03

如需詳細的語法及參數資訊，請參閱 [New-MigrationBatch](https://technet.microsoft.com/zh-tw/library/jj219166\(v=exchg.150\)) 與 [New-MoveRequest](https://technet.microsoft.com/zh-tw/library/dd351123\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要確認您是否已成功完成遷移，執行下列操作：

  - 從介面執行下列命令，以擷取信箱移動資訊。
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

如需詳細資訊，請參閱 [Get-MigrationUserStatistics](https://technet.microsoft.com/zh-tw/library/jj218695\(v=exchg.150\))。

## 移動使用者的主要信箱並允許較大的錯誤項目限制

## 使用 EAC 移動使用者的主要信箱並允許較大的錯誤項目限制

1.  在 EAC 中瀏覽至\[收件者\] \>\[遷移\]，然後按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

2.  在 \[新本機信箱移動精靈\] 中，選取您想要移動的使用者主要信箱，按一下 \[確定\] 後再按一下 \[下一步\]。

3.  在 \[**移動組態**\] 頁面上，指定新的批次的名稱。選取 \[**移動主要信箱僅**、，然後選取 \[您要的信箱資料庫位置的選項。

4.  按一下 \[更多選項\]![更多選項圖示](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "更多選項圖示")，輸入錯誤項目限制後再按一下 \[確定\]。

## 使用命令介面移動使用者的主要信箱並允許較大的錯誤項目限制

本範例會移動 Lisa 的主要信箱到信箱資料庫 DB01 並將錯誤項目設為`100`。若要設定的大型的錯誤項目限制，您必須使用*AcceptLargeDataLoss*參數。

    New-MoveRequest -Identity 'Lisa' -PrimaryOnly -TargetDatabase "DB01" -BadItemLimit 100 -AcceptLargeDataLoss

如需詳細的語法及參數資訊，請參閱 [New-MigrationBatch](https://technet.microsoft.com/zh-tw/library/jj219166\(v=exchg.150\)) 與 [New-MoveRequest](https://technet.microsoft.com/zh-tw/library/dd351123\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要確認您是否已成功完成遷移，執行下列操作：

  - 從介面執行下列命令，以擷取信箱移動資訊。
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

如需詳細資訊，請參閱 [Get-MigrationUserStatistics](https://technet.microsoft.com/zh-tw/library/jj218695\(v=exchg.150\))。

