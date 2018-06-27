---
title: '常見問題集：公用資料夾: Exchange 2013 Help'
TOCTitle: 常見問題集：公用資料夾
ms:assetid: 1cdcdcb7-f11b-45ca-ad23-7c38f640208c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ552408(v=EXCHG.150)
ms:contentKeyID: 50472660
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 常見問題集：公用資料夾

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2017-03-27_

本主題提供與 Exchange Server 2013 中公用資料夾相關的常見問題清單。如要進一步瞭解公用資料夾，請參閱[公用資料夾](public-folders-exchange-2013-help.md)。

有任何此處尚未回答的公用資料夾相關問題嗎？請寄電子郵件至 [Ex2013HelpFeedback@microsoft.com](mailto:ex2013helpfeedback@microsoft.com)。

## 有關公用資料夾移轉的常見問題

本節包含有關公用資料夾移轉的常見問題。如需詳細資訊，請參閱[使用批次移轉公用資料夾從舊版移轉至 Exchange 2013](use-batch-migration-to-migrate-public-folders-to-exchange-2013-from-previous-versions-exchange-2013-help.md)、 [使用批次移轉至 Office 365 和 Exchange Online 移轉舊版公用資料夾](use-batch-migration-to-migrate-legacy-public-folders-to-office-365-and-exchange-online-exchange-online-help.md)或[使用批次移轉至 Exchange 2013 公用資料夾移轉至 Exchange Online](use-batch-migration-to-migrate-exchange-2013-public-folders-to-exchange-online-exchange-online-help.md)。

## 有哪些支援公用資料夾遷移情況？

下列清單詳細說明將公用資料夾遷移至Exchange 2013或 Exchange Online 可用的選項。

  - Exchange 2007 公用資料夾 (SP3 RU15 或更新版本) 可以移轉至Exchange 2013或 Exchange Online。

  - Exchange 2010 公用資料夾 (SP3 RU8 或更新版本) 可以移轉至Exchange 2013或 Exchange Online。

  - Exchange 2013 公用資料夾 (CU15 或更新版本) 可以移轉至 Exchange Online。

目前唯一移轉Exchange 2013相同的 Active Directory 樹系中，以支援。將未來支援跨樹系遷移。

## 移轉之後，來源 Exchange 2010 伺服器上發生什麼事？

在移轉的最後完成階段期間，會鎖定來源伺服器，讓使用者無法存取。此鎖定會持續保持以避免使用者在移轉完成之後存取來源公用資料夾。您可以解除鎖定，但是不建議這麼做，因為變更無法同步至 Exchange 2013。

## 當您移轉公用資料夾時，現有的公用資料夾規則會發生什麼改變？

公用資料夾規則會隨著資料一併移轉，並且保持為公用資料夾規則。它們不會轉換為信箱規則。

## 如果在產生初始 .csv 檔案之後，於來源上執行階層變更，會發生什麼事？這些目的地會有何反映？

.csv 檔案用於決定來源階層與目的信箱之間的對應。它包含唯一的最上層資料夾。在最上層資料夾下的子資料夾會自動移轉。因此，如果已新增新的子資料夾，則會在處理程序期間進行移轉。如果新的最上層資料夾已產生，則會建立在包含可寫入階層副本的信箱中。

## 移轉 Exchange 2013 公用資料夾期間，如果在暫停與完成之間有一段長時間窗口，我該如何強制進行差異同步，讓使用者可在最後同步期間存取公用資料夾？

您可以藉由執行以下 Shell 命令，在完成之前 (鎖定來源之前) 強制進行差異同步：

    Resume-PublicFolderMigrationRequest \PublicFolderMigration

如需詳細的語法及參數資訊，請參閱 [Resume-PublicFolderMigrationRequest](https://technet.microsoft.com/zh-tw/library/jj218689\(v=exchg.150\))。

## 對於地理分布階層的移轉，我該如何確定公用資料夾已建立在最靠近目標使用者的位置？

移轉過程中會產生 .csv 檔 (使用 `publicfoldertomailboxmapgenerator.ps1` 指令碼)。此檔案包含新階層的資料夾對信箱對應。您可以使用此 .csv 檔案在適當的地理位置中建立公用資料夾信箱，並修改檔案，將所需的資料夾放置到適當的信箱中，使其靠近目標使用者。

輸入的 .csv 檔案可藉由執行命令檔 `AggregatePFData.ps1` 而產生，其位於目錄 \<*Exchange 安裝目錄*\>\\V15\\Scripts 中。執行命令檔，如下所示：

    .\AggregatePFData.ps1 | Select-Object -property @{Name="FolderName"; Expression = {$_.Identity}}, @{Name="FolderSize"; Expression = {$_.TotalItemSize.Value.ToBytes()}} | Export-CSV -Path <Path followed by the name of the CSV>

## 現有的公用資料夾權限可移轉嗎？

是的，權限將隨著資料在資料夾層級自動移轉。您不必單獨執行此步驟。

## 公用資料夾是否會停用？

否。公用資料夾非常適合用於 Outlook 整合、簡單的共用案例，以及允許大量對象存取相同資料。

## 哪些用戶端支援公用資料夾？

Outlook 2007、Outlook 2010、Outlook 2013 和 Outlook 2011 for Mac 使用者都可以存取公用資料夾。不過，信箱位於 Exchange 2013 伺服器上的使用者，無法從使用 Exchange Web 服務 (EWS) 的用戶端 (Outlook for Mac) 來連線至 Exchange 2007 或 Exchange 2010 公用資料夾。建議將舊版公用資料夾遷移至 Exchange 2013，讓這些使用者可繼續存取內容。

## 是否有任何限制在用戶端吗？

Outlook Web App 支援，但有一些限制。 您可以新增和移除我的最愛公用資料夾 （若它們位於電子郵件、 文章、 行事曆及連絡人的公用資料夾） 和執行項目層級的作業，例如建立、 編輯、 刪除文章與回覆的文章。但是，您無法執行 Outlook Web App 中的下列：

  - 建立或刪除公用資料夾

  - 拖放內容

  - 存取執行舊版 Exchange 的伺服器上的公用資料夾

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您只能建立包含項目<strong>回覆使用特定範本</strong>中啟用郵件功能的公用資料夾的公用資料夾規則。有可能包含<strong>使用特定範本的回覆</strong>的前現有規則會繼續處理非擁有郵件功能的公用資料夾，但那些資料夾上無法使用此範本項目建立新的規則或編輯現有規則的這個項目。</td>
</tr>
</tbody>
</table>


在混合式案例中，在 web 上的 Outlook 和 Outlook 2011 for Mac 不支援跨部署公用資料夾。使用者必須位於相同的位置存取其有 Outlook 2011 for Mac 或 Outlook web 上的公用資料夾。如果所依循的[混合式部署程序](https://technet.microsoft.com/en-us/library/jj200788\(v=exchg.150\).aspx)下的程序，與 Outlook 2016 for Mac 中的年 4 月 2016年更新已安裝在所有的用戶端上的 Outlook 2016 for Mac 使用者可以存取公用資料夾的混合式案例。

## 我要如何在公用資料夾信箱中儲存非常大的階層？

如需公用資料夾儲存限制的相關資訊，請參閱[公用資料夾的限制](limits-for-public-folders-exchange-2013-help.md)。

## 如何檢視階層公用資料夾信箱？

執行下列命令：

    Get-OrganizationConfig | Format-List RootPublicFolderMailbox

如需詳細的語法及參數資訊，請參閱 [Get-OrganizationConfig](https://technet.microsoft.com/zh-tw/library/aa997571\(v=exchg.150\))。

## 如何利用 Exchange 管理命令介面 Cmdlet 建立公用資料夾的內容信箱？

請執行以下命令建立第一個主要階層共用資料夾與次要階層信箱。

    New-Mailbox -PublicFolder -Name <name of public folder>

如需詳細資料，請參閱[建立公用資料夾](create-a-public-folder-exchange-2013-help.md)。

## 在舊版 Exchange 中，每一個信箱資料庫都有一個選項，可指定其公用資料夾資料庫。如何在 Exchange 2013 中運作？

Exchange 2013 中沒有資料庫層級設定。Exchange 2013 具有信箱層級的功能，可指定共用資料夾信箱，但依預設，Exchange 會自動計算每一使用者階層的信箱。

## 如何在 Exchange 2013 中使用公用資料夾計量工具？

您可以在 Exchange 2013 中使用 [Get-PublicFolderStatistics](https://technet.microsoft.com/zh-tw/library/aa998663\(v=exchg.150\)) 和 [Get-PublicFolderItemStatistics](https://technet.microsoft.com/zh-tw/library/ee332344\(v=exchg.150\)) Cmdlet 取得公用資料夾計量資料。在 Exchange 2010 中也是使用同樣的解決方案，所以此處沒有任何變更。公用資料夾不需要額外的報告附加元件。

## 公用資料夾可分辨內部與第三方對公用資料夾的存取嗎？

在 Exchange 2013 中，公用資料夾權限是使用「角色存取控制」(RBAC) 管理。Exchange 2013 中不會使用存取控制清單 (ACL)。您可以使用 [Get-PublicFolderStatistics](https://technet.microsoft.com/zh-tw/library/aa998663\(v=exchg.150\)) 和 [Get-PublicFolderItemStatistics](https://technet.microsoft.com/zh-tw/library/ee332344\(v=exchg.150\)) Cmdlet 追蹤執行管理工作的帳戶，然後對應地稽核存取權。若要深入了解 RBAC，請參閱[了解角色型存取控制](understanding-role-based-access-control-exchange-2013-help.md)。

## 信箱稽核記錄是對應公用資料夾進行作業嗎？

不是。不是在這個時候。

## 對公用資料夾的限制是什麼？有哪些建議？

如需公用資料夾限制的相關資訊，請參閱[公用資料夾的限制](limits-for-public-folders-exchange-2013-help.md)。

## 對於分割公用資料夾信箱的建議為何？它們應該留在同一個資料庫嗎？

在舊版的 Exchange 中，您可以跨公用資料夾資料庫分割公用資料夾。您可以決定是否要將公用資料夾信箱的內容分割到相同信箱資料庫或不同資料庫上的信箱。一般而言，因為您會想要平衡儲存和 I\\O，因此建議分割到不同資料庫上。

## 您可以在公用資料夾上設定保留原則嗎？

就像是在舊版的 Exchange，您可以設定的保留限制的項目。如需詳細資訊，請參閱[公用資料夾的限制](limits-for-public-folders-exchange-2013-help.md)。

## 您可以指定哪些使用者能夠使用特定的公用資料夾信箱嗎？

在 Exchange 2007 與 Exchange 2010 中，您可以指定哪些使用者可以存取特定公用資料夾。在 Exchange 2013 中，您可以依使用者設定預設公用資料夾信箱。方法是執行 [Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\)) Cmdlet 搭配 *DefaultPublicFolderMailbox* 參數。

    Set-Mailbox -Identity kweku@contoso.com -DefaultPublicFolderMailbox "PF_Administration"

## 如果主要階層下降，對使用者有何影響？

如果主要階層公用資料夾信箱下降，使用者仍可檢視公用資料夾，但無法寫入。若要協助避免階層下降，建議您將公用資料夾包含在資料庫可用性群組 (DAG) 中。若要深入了解 DAG，請參閱[資料庫可用性群組 (DAGs)](database-availability-groups-dags-exchange-2013-help.md)。

## 您可以變更哪些公用資料夾信箱為主要階層信箱嗎？

不可以。如果您嘗試變更主要階層信箱，將會發生錯誤。

## 公用資料夾有全文檢索搜尋功能嗎？

是。您可以在 Exchange 2013 中對公用資料夾執行全文檢索搜尋。不過，您無法跨多個公用資料夾執行搜尋。

