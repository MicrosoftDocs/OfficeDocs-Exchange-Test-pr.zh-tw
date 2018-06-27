---
title: '在 Exchange 2013 移動信箱: Exchange 2013 Help'
TOCTitle: 在 Exchange 2013 移動信箱
ms:assetid: 9c0a0bc9-2a39-4cf0-aa6e-6e5ef3fd38b5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ150543(v=EXCHG.150)
ms:contentKeyID: 50473809
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 在 Exchange 2013 移動信箱

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-07_

當您將信箱移動時，您從*來源信箱資料庫*移至*目標信箱資料庫*。目標信箱資料庫可以在不同的網域、 不同Active Directory網站或其他樹系中的不同伺服器上的相同伺服器上。

## 移動信箱的理由

在下列情況下，您可能需要移動信箱：

  - **升級**   當您將現有的 Microsoft Exchange Server 2007 或 Exchange Server 2010 組織升級成 Exchange Server 2013 時，會從現有的 Exchange 伺服器將信箱移至 Exchange 2013 信箱伺服器。

  - **重新對齊**  您可以移動信箱進行重新對齊。例如，您可能會想要將信箱從一個資料庫移至具有較大的信箱大小限制的資料庫。

  - **調查問題**  如果您需要調查信箱有問題，您可以移動該信箱至不同的伺服器。例如，您可以移動至另一部伺服器的高活動的所有信箱。

  - **已損毀的信箱**  發生損毀的信箱時，您可以將信箱移至不同的伺服器或資料庫中。將不會移動損毀的郵件。

  - **實體位置變更**  您可以將信箱移至不同Active Directory網站中的伺服器。例如，如果使用者移至不同的實體位置，您可以將該使用者的信箱移至新位置更接近的伺服器。

  - **區分管理角色**  若要分隔Exchange管理從Windows作業系統帳戶管理。為達成此目的，您可以從單一樹系移動信箱到資源樹系案例。在此案例中， Exchange信箱位於在一個樹系和其相關聯的Windows使用者帳戶位於不同的樹系中。

  - **外包電子郵件管理**  您可能會想要將電子郵件的管理及保留Windows的使用者帳戶的管理。為達成此目的，您可以從單一樹系移動信箱到資源樹系案例。

  - **整合電子郵件和使用者帳戶管理**  若要變更從分隔或外包的電子郵件的管理模型中的電子郵件和使用者帳戶可以從管理在同一個樹系內的模型。為達成此目的，您可以將信箱從資源樹系案例移至單一樹系。在此案例中， Exchange信箱及Windows使用者帳戶位於同一個樹系中。

## Exchange 2013 移動

Microsoft Exchange Server 2013介紹*批次移動*與*移轉端點*的概念。移轉端點所說明的遠端伺服器及可以與一個或多個批次相關聯的連線的管理物件。與新的批次移動架構可改善信箱複寫服務 (MRS) 上移動具有增強型的管理功能。批次移動Exchange 2013功能架構下列功能：

  - 可大批次移動多個信箱的功能。

  - 移動與報告期間所進行的電子郵件通知。

  - 自動重試並確定移動作業的優先次序。

  - 可一起移動主要和個人封存信箱，或分開移動。

  - 手動移動要求最終處理選項，允許您完成移動前先預覽移動結果。

  - 週期性增量同步更新移動變化。

在 Exchange 2013 中，您必須從 Exchange 2013 系統管理中心 (EAC) 和 Exchange 管理命令介面才能在 Exchange 2007 和 Exchange 2010 以及 Exchange 2013 之間移動信箱。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要在 Exchange 2013 中移動單一信箱，仍可使用 Exchange Server 2010 中的類似方法，以 EAC 或移動要求或移轉批次指令程式進行。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您不能將內部部署信箱從 Exchange Server 2003 移動到 Exchange 2013。</td>
</tr>
</tbody>
</table>


如需管理新的和現有移動作業之詳細資訊，請參閱[管理內部移動](manage-on-premises-moves-exchange-2013-help.md)。

## 移轉端點

移轉端點擷取遠端伺服器資訊及保存資料與節流設定的來源的移轉必要的認證。您可用於移轉端點設定遠端且跨樹系移動。本機移動不需要使用個端點。（本機移動是兩個不同的內部Exchange資料庫之間移動信箱的移動）。

下列清單顯示支援移轉端點的移動作業類型：

  - **跨樹系移動**  兩個不同的內部Exchange樹系之間移動信箱。跨樹系移動需要使用Exchange RemoteMove 端點。

  - **遠端移動**  在混合式部署中，遠端移動涉及*onboarding*或*offboarding*移轉。遠端移動要求 RemoteMove 端點的使用。Onboarding 將信箱從內部部署Exchange組織移至Exchange Online 中 Microsoft Office 365，並使用 RemoteMove 端點與來源端點的遷移批次。Offboarding 將信箱從Exchange線上Office 365中移至內部部署Exchange組織並使用Exchange RemoteMove 端點作為目標端點的遷移批次。

下表顯示 Exchange 2013 中可管理的移動端點類型和值。

### 移動端點類型值

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange RemoteMove</th>
<th>Exchange LocalMove</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MaxConcurrentMigrations</p></td>
<td><p>MaxConcurrentMigrations</p></td>
</tr>
<tr class="even">
<td><p>RemoteServer</p></td>
<td><p>Site</p></td>
</tr>
<tr class="odd">
<td><p>ArchiveDomain</p></td>
<td><p>Database</p></td>
</tr>
<tr class="even">
<td><p>BadItemLimit</p></td>
<td><p>ArchiveDatabase</p></td>
</tr>
<tr class="odd">
<td><p>LargeItemLimit</p></td>
<td><p>BadItemLimit</p></td>
</tr>
<tr class="even">
<td><p>資料庫</p></td>
<td><p>LargeItemLimit</p></td>
</tr>
<tr class="odd">
<td><p>TargetDeliveryDomain</p></td>
<td><p>PrimaryOnly</p></td>
</tr>
<tr class="even">
<td><p>PrimaryOnly</p></td>
<td><p>ArchiveDatabase</p></td>
</tr>
<tr class="odd">
<td><p>ArchiveDatabase</p></td>
<td><p>DAG</p></td>
</tr>
<tr class="even">
<td><p>ArchiveOnly</p></td>
<td><p>Forest</p></td>
</tr>
</tbody>
</table>


如需有關遷移端點的詳細資訊，請參閱 EAC 中的 **\[遷移\]** 使用者介面和 [New-MigrationEndpoint](https://technet.microsoft.com/zh-tw/library/jj218611\(v=exchg.150\))。

如需管理新的和現有移動作業之詳細資訊，請參閱[管理內部移動](manage-on-premises-moves-exchange-2013-help.md)。

