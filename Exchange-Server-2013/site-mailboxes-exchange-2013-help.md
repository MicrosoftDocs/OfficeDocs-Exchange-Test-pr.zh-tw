---
title: '網站信箱: Exchange 2013 Help'
TOCTitle: 網站信箱
ms:assetid: 2c4393f4-d274-4e6c-bd09-9577e68c5a33
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ150499(v=EXCHG.150)
ms:contentKeyID: 50472763
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 網站信箱

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

傳統上兩個唯一與不同的資料存放庫中保留電子郵件和文件。大部分組織共同作業使用這兩種媒體。挑戰是確認電子郵件和文件會存取使用不同的用戶端。這通常會產生減少使用者產能與效能降低的使用者經驗。

*站台信箱*會在 Microsoft Exchange 2013嘗試解決此問題的新概念。網站信箱允許存取Microsoft SharePoint 2013文件和 Exchange 電子郵件使用相同的用戶端介面提升共同作業和使用者產能。站台信箱具有相同的作用組成SharePoint 2013網站共用成員資格 （擁有者和成員） 儲存透過電子郵件訊息的Exchange 2013信箱和SharePoint 2013網站的文件並管理介面的佈建的地址和生命週期的需求。

網站信箱需要Exchange 2013和SharePoint Server 2013整合和組態。如需如何使用SharePoint Server 2013組織為Exchange 2013組織設定的詳細資訊，請參閱下列主題：

  - [在 SharePoint Server 2013 中的設定網站信箱](https://go.microsoft.com/fwlink/p/?linkid=258264)。

  - [與 SharePoint 和 Lync 整合](integration-with-sharepoint-and-lync-exchange-2013-help.md)

如需 Exchange Server 2013 中共同作業功能的詳細資訊，請參閱[共同作業](collaboration-exchange-2013-help.md)。

**目錄**

How do site mailboxes work?

Site mailbox provisioning policies

## 站台信箱如何運作？

當一個專案成員檔案郵件或文件使用站台信箱時，任何專案成員然後可以存取內容。站台信箱會在 Outlook 2013 中的呈現並授與使用者容易存取電子郵件和文件的所需注意的專案。此外，內容相同的一組可直接從 SharePoint 網站本身。使用站台信箱內容會保留其所屬位置。Exchange 儲存電子郵件、 提供使用相同的訊息檢視的電子郵件交談他們自己的信箱使用每天的使用者。同時，SharePoint 儲存文件、 文件 coauthoring 和版本設定至表格。Exchange 同步處理只是足夠的中繼資料與 SharePoint Outlook （例如文件標題、 上次修改日期、 上次修改作者、 大小） 中建立的文件檢視。

![站台信箱儲存體和使用量圖表](images/JJ150499.b98be571-d2e0-4ebd-9fe2-440a14e91e35(EXCHG.150).gif "站台信箱儲存體和使用量圖表")

## 網站信箱佈建原則

在 Exchange 管理命令介面中使用**SiteMailboxProvisioningPolicy** cmdlet 可以設定網站信箱配額。站台信箱佈建原則僅適用於電子郵件傳送到與站台信箱及 Exchange 伺服器上的網站信箱的大小。SharePoint 中所設定的文件存放庫的設定。雖然您可以建立多個站台信箱佈建原則使用**New-SiteMailboxProvisioningPolicy**指令程式，佈建原則的預設值將會套用至所有站台信箱。您不能在組織內套用多個原則。佈建原則允許您設定下列配額：


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>配額</th>
<th>描述</th>
<th>預設設定</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>IssueWarningQuota</p></td>
<td><p><em>IssueWarningQuota</em> 參數會指定觸發警告訊息至站台信箱的站台信箱大小。</p></td>
<td><p>4.5 GB</p></td>
</tr>
<tr class="even">
<td><p>MaxReceiveSize</p></td>
<td><p><em>MaxReceiveSize</em> 參數會指定站台信箱可接收的電子郵件大小上限。</p></td>
<td><p>36 MB</p></td>
</tr>
<tr class="odd">
<td><p>ProhibitSendReceiveQuota</p></td>
<td><p><em>ProhibitSendReceiveQuota</em> 參數指定信箱大小，一旦達到此大小，就無法再傳送或接收郵件。</p></td>
<td><p>5 GB</p></td>
</tr>
</tbody>
</table>


若欲瞭解更多設定網站信箱佈建原則的資訊，請參閱 [管理網站信箱佈建原則](manage-site-mailbox-provisioning-policies-exchange-2013-help.md)。

回到頁首

## 生命週期原則與保留

透過 SharePoint 管理的站台信箱生命週期。它會透過 SharePoint 您應該執行建立以及移除站台信箱的所有網站信箱工作。此外，您可以建立 SharePoint 生命週期原則來管理網站信箱的生命週期。例如，您可以建立生命週期原則自動 6 個月之後關閉所有站台信箱的 SharePoint 中。如果使用者仍然需要使用站台信箱，使用者可以重新啟用透過 SharePoint 網站信箱。我們建議您使用是在伺服器陣列中的應用程式生命週期。以手動方式刪除作用中網站信箱從 Exchange 會導致孤立的網站信箱。.

當 SharePoint 中的技術支援週期應用程式會關閉站台信箱時，站台信箱會保留上文生命週期原則處於關閉狀態的期間。由使用者或管理員從 SharePoint 再重新啟用信箱。保留期間之後存放信箱資料庫中的 Exchange 網站信箱必須與加其名稱**MDEL:**指出其具有已標記為刪除。您必須手動移除這些站台信箱的信箱資料庫以免費的儲存空間及別名。如果您不需要啟用 SharePoint 生命週期原則，您將會失去來決定哪一個站台信箱已標記為待刪除的能力。已由系統管理員移除站台信箱，為仍可復原的信箱內容。

可使用下列命令來搜尋並移除已標記為待刪除的網站信箱。

    Get-Mailbox MDEL:* | ?{$_.RecipientTypeDetails -eq "TeamMailbox"} | Remove-Mailbox -Confirm:$false

站台信箱不支援保留項目層級。保留在運作專案層級的網站信箱，所以何時會刪除整個網站信箱、 會刪除保留項目。

## 法規符合性

在 SharePoint 中使用 eDiscovery 主控台，站台信箱可以屬於就地 eDiscovery 範圍和您可以針對使用者信箱或站台信箱的關鍵字搜尋。此外，您可以將站台信箱置於法務保存措施。如需詳細資訊，請參閱[就地 eDiscovery](in-place-ediscovery-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>網站信箱置於Office 365中的合法持有，它必須被指派Exchange Online (Plan 2) 授權。如果站台信箱指派Exchange Online (計劃 1) 授權，您必須將它放在不同Exchange Online封存授權保留指派。</td>
</tr>
</tbody>
</table>


回到頁首

## 備份與還原

備份與還原的站台信箱存放在 mailbox server 上使用相同的備份及還原方法用於所有的 Exchange 信箱 Exchange。如需詳細資訊，請參閱[資料庫可用性群組 (DAGs)](database-availability-groups-dags-exchange-2013-help.md)。

SharePoint 文件，您應該備份與還原到同一個位置。如果您將您的 SharePoint 內容還原至相同的 Url，然後站台信箱會繼續運作並需要進行其他設定。如果您還原至不同的 URL，然後您需要執行**Set-SiteMailbox**指令程式來更新*SharePointURL*屬性。我們建議您不要將 SharePoint 還原到新的樹系。

