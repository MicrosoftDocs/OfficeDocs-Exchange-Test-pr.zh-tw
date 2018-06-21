---
title: 'Exchange 混合式部署中的權限: Exchange 2013 Help'
TOCTitle: Exchange 混合式部署中的權限
ms:assetid: 58b46b2c-a6b2-424a-8fc2-0f1fe1ad8e18
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ906433(v=EXCHG.150)
ms:contentKeyID: 51407019
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 混合式部署中的權限

 

_<strong>適用版本：</strong>Exchange Server 2013, Exchange Server 2016_

_<strong>上次修改主題的時間：</strong>2018-05-02_

Office 365 組織中的 Exchange Online 是以 Exchange Server 為基礎，並且就像內部部署組織一樣，也使用應用角色的存取控制 (RBAC) 來控制權限。系統管理員是透過管理角色群組獲得權限，而使用者則是透過管理角色指派原則獲得權限。

深入了解 Exchange Online 和內部 Exchange 的權限：[權限](https://technet.microsoft.com/zh-tw/library/dd351175\(v=exchg.150\))

## 系統管理員權限

根據預設，用來建立 Office 365 服務的承租人會設為 Exchange Online 組織中 \[組織管理\] 角色群組的成員。這個使用者可以管理整個 Exchange Online 組織，包括設定組織層級的設定以及 Exchange Online 收件者的管理。

您可以根據需要進行的管理工作，在 Exchange Online 組織中新增額外的系統管理員。例如，您可以新增額外的組織系統管理員和收件者系統管理員、讓專家使用者執行合規工作 (例如探索)、設定自訂權限等。Office 365 系統管理員的所有 Exchange Online 權限管理工作，必須在 Exchange Online 組織中使用 Exchange 系統管理中心 (EAC) 或遠端 PowerShell 執行。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ906432.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>內部部署組織與 Office 365 組織之間不會移轉權限。您在內部部署組織內定義的權限必須在 Office 365 組織中重新建立。</td>
</tr>
</tbody>
</table>


如需詳細資訊，請參閱[管理角色群組](https://technet.microsoft.com/zh-tw/library/jj657480\(v=exchg.150\))及[管理角色群組成員](https://technet.microsoft.com/zh-tw/library/jj657492\(v=exchg.150\))。

## 委派信箱權限

在內部部署 Exchange 部署中，使用者可以取得各種其他使用者信箱的權限。這會呼叫委派的信箱權限和它的實用時需要管理其他使用者信箱; 的某些部分行政助理例如，管理主管的行事曆。Exchange 混合式部署支援使用信箱位於內部部署 Exchange 組織與 Office 365 中的信箱之間的一些，但並非所有信箱權限。下列各節將詳細說明哪些權限，並不支援;支援混合式信箱權限 ； 所需的其他設定與信箱權限如何同步處理內部部署組織與 Office 365 之間。

## 支援混合式環境中的信箱權限

下列權限**所**支援：

  - **完整存取權** 在內部部署Exchange伺服器上的信箱可授與 \[**完整存取**權限至 Office 365 信箱，反之亦然。例如，Office 365 信箱可以授與內部部署共用信箱的**完整存取**權限。使用者必須使用 Outlook 桌面用戶端; 開啟信箱跨部署信箱權限不支援在網路上的 Outlook。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ150559.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>當使用者第一次存取其他組織中的信箱，並將其新增至他們的 Outlook 設定檔時，可能會收到其他認證提示</td>
    </tr>
    </tbody>
    </table>


  - **傳送代理者**在內部部署Exchange伺服器上的信箱可授與 「**代理傳送者**」 權限至 Office 365 信箱，反之亦然。例如，Office 365 信箱可以授與至內部部署共用信箱 \[**代理傳送者**\] 權限。使用者必須使用 Outlook 桌面用戶端; 開啟信箱跨部署信箱權限不支援在網路上的 Outlook。
    
    Azure \[Active Directory 連線代理傳送者權限同步處理在內部部署 Exchange 伺服器與 Exchange Online 之間的伺服器上需要一些變更。如需詳細資訊，請參閱本主題稍後的啟用支援的混合式中 Azure 作用中的目錄連線的信箱權限。

  - **Folder permissions** Grants access to the contents of a particular folder.

  - **私人的項目**新增代理人時選項可以設定為允許具有查看私人的行事曆項目資料夾權限的使用者。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ150559.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>年 2 月 2018年以支援完整存取權，傳送代理與資料夾權限跨樹系已導以及預期年 4 月 2018年就是完整的功能。</td>
</tr>
</tbody>
</table>


下列權限或功能支援：

  - **Send-As**可讓使用者將郵件傳送如同它看起來來自另一個使用者的信箱。

  - **自動對應**讓 Outlook 時，若要自動開啟任何使用者授與**完整存取**權的信箱。

從另一個信箱會收到這些權限的任何信箱必須同時為授與信箱移動。如果將信箱從多個信箱接收權限，必須同時移動該信箱，並授與權限給它，信箱的所有。

## 設定您內部部署 Exchange 伺服器，以支援混合式信箱權限

若要啟用完整存取權和權限代表在混合式部署中，額外的設定變更的傳送可能需要根據您安裝的 Exchange 的版本。下表顯示哪些版本的 Exchange 混合部署與 Office 365 中支援委派的信箱權限及需要哪些其他設定。如需如何設定 Exchange 2013 和 2010年伺服器和信箱來支援 Acl 的步驟，請參閱[設定 Exchange 混合部署中支援委派的信箱權限](configure-exchange-to-support-delegated-mailbox-permissions-in-a-hybrid-deployment-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange 版本</th>
<th>必要條件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2016</p></td>
<td><p>需要進行其他設定。</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013</p></td>
<td><p>Exchange 2013 伺服器需要下列各項：</p>
<ul>
<li><p>最新累計更新 (CU) 或前 CU、 安裝。執行較舊的 sharepoing 累計更新的 Exchange 2013 伺服器不支援與可能無法使用混合部署中的委派的信箱權限。</p></li>
<li><p>部署 Exchange 組織已設定為允許存取控制清單 (Acl) 上戳記的郵件物件及與 Office 365 同步處理。</p></li>
<li><p>內部部署遠端信箱移至 Exchange 2013 CU10 之前的 Office 365 相關聯的信箱需要以手動方式設定為支援 Acl。遠端信箱執行 Exchange 2013 CU10 的伺服器上建立或更新版本，升級前後及組織設定來允許 Acl、 Exchange 會自動設定。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Exchange 2010</p></td>
<td><p>Exchange 2010 SP3 伺服器需要下列各項：</p>
<ul>
<li><p>最新的更新彙總套件 (RU) 或前 RU、 安裝。執行 RU 較舊的 Exchange 2010 SP3 伺服器不支援與可能無法使用混合部署中的委派的信箱權限。</p></li>
<li><p>內部部署與 Office 365 信箱相關聯的遠端信箱必須設定為支援 Acl。這需要完成的每個內部部署遠端信箱與 Office 365 信箱的關聯。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Exchange 2007 或更早版本</p></td>
<td><p>不支援。</p></td>
</tr>
</tbody>
</table>


## 啟用混合信箱中的權限 Azure 作用中的目錄連線的支援

除了設定您的內部部署 Exchange 伺服器，您也需要確定 Azure Active Directory 連線 （AAD 連線） 伺服器設為同步處理的混合信箱權限。以下是您要執行動作以確定您 AAD 連線伺服器已準備好可支援這些權限：

  - **升級 AAD 連線**AAD 連線需要至少升級至版本 1.1.553.0。 您可以從[Microsoft Azure Active Directory 連線](http://go.microsoft.com/fwlink/p/?linkid=510956)下載最新版的 AAD 連線。

  - **啟用 Exchange 混合式環境 AAD 連線**若要同步處理屬性可讓混合信箱權限 （特別是代表權限傳送），您需要確定在 AAD 連線會啟用**Exchange 混合部署**組態選項。如需如何執行 AAD 連線安裝精靈一次更新其組態資訊，請參閱[Azure AD 連線同步處理： 執行安裝精靈的第二個時間](https://docs.microsoft.com/en-us/azure/active-directory/connect/active-directory-aadconnectsync-installation-wizard)

## 如何在內部部署和 Office 365 組織之間同步處理信箱權限

## 使用者權限

就像系統管理員權限一樣，您可以授與權限給 Exchange Online 中的使用者。根據預設，使用者的權限是透過預設角色指派原則授與。這項原則適用於 Exchange Online 組織中的每一個信箱。如果預設授與的權限就已足夠，您就不需要進行任何變更。

如果您想要自訂使用者權限，可以修改現有的預設角色指派原則，或是建立新的指派原則。如果您建立多個指派原則，可以將不同的原則指派給不同的信箱群組，如此可讓您根據需求控制授與每一個群組的權限。Exchange Online 使用者的所有權限管理工作，必須在 Exchange Online 組織中使用 EAC 或遠端 PowerShell 執行。

就像系統管理員權限一樣，使用者權限不會在內部部署組織與 Exchange Online 組織之間傳輸。您在內部部署組織內定義的任何權限都必須在 Exchange Online 組織中重新建立。

如需詳細資訊，請參閱[管理角色指派原則](https://technet.microsoft.com/zh-tw/library/jj657511\(v=exchg.150\))及[變更在信箱上的指派原則](https://technet.microsoft.com/zh-tw/library/dd638076\(v=exchg.150\))。

下表列出 Exchange Online 組織中預設角色指派原則所授與的權限。

### 預設角色指派原則權限

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>管理角色</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MyTeamMailboxes</p></td>
<td><p><code>MyTeamMailboxes</code> 管理角色讓個別使用者可建立站台信箱並連線至 Microsoft SharePoint 網站。</p></td>
</tr>
<tr class="even">
<td><p>My Marketplace Apps</p></td>
<td><p><code>My Marketplace Apps</code> 管理角色可讓個別使用者檢視並修改他們的 Microsoft Office 市集應用程式。</p></td>
</tr>
<tr class="odd">
<td><p>MyBaseOptions</p></td>
<td><p><code>MyBaseOptions</code> 管理角色可讓個別使用者檢視和修改專屬信箱和關聯設定的基本組態。</p></td>
</tr>
<tr class="even">
<td><p>MyContactInformation</p></td>
<td><p><code>MyContactInformation</code> 管理角色可讓個別使用者修改其連絡人資訊，包括地址和電話號碼。</p></td>
</tr>
<tr class="odd">
<td><p>MyDistributionGroupMembership</p></td>
<td><p><code>MyDistributionGroupMembership</code> 管理角色可讓個別使用者在組織的通訊群組中檢視和修改其成員資格，使那些通訊群組可以進行群組成員資格的操作。</p></td>
</tr>
<tr class="even">
<td><p>MyDistributionGroups</p></td>
<td><p><code>MyDistributionGroups</code> 管理角色可讓個別使用者建立、修改和檢視通訊群組，並為其所擁有的通訊群組修改、檢視、移除和新增成員。</p></td>
</tr>
<tr class="odd">
<td><p>MyMailSubscription</p></td>
<td><p><code>MyMailSubscription</code> 角色可讓個別使用者檢視和修改其電子郵件訂閱設定，例如郵件格式和通訊協定預設值。</p></td>
</tr>
<tr class="even">
<td><p>MyProfileInformation</p></td>
<td><p><code>MyProfileInformation</code> 管理角色可以讓個別使用者修改其名稱。</p></td>
</tr>
<tr class="odd">
<td><p>MyRetentionPolicies</p></td>
<td><p><code>MyRetentionPolicies</code> 管理角色可讓個別使用者檢視其保留標記，以及檢視和修改其保留標記設定和預設值。</p></td>
</tr>
<tr class="even">
<td><p>MyTextMessaging</p></td>
<td><p><code>MyTextMessaging</code> 管理角色可讓個別使用者建立、檢視及修改其文字訊息設定。</p></td>
</tr>
<tr class="odd">
<td><p>MyVoiceMail</p></td>
<td><p><code>MyVoiceMail</code> 管理角色可讓個別使用者檢視和修改其語音信箱設定。</p></td>
</tr>
<tr class="even">
<td><p>我的 ReadWriteMailbox 應用程式</p></td>
<td><p><code>My ReadWriteMailbox Apps</code> 管理角色可讓使用者以 ReadWriteMailbox 的權限安裝應用程式。</p></td>
</tr>
<tr class="odd">
<td><p>我的自訂應用程式</p></td>
<td><p><code>My Custom Apps</code> 管理角色可讓使用者檢視和修改其自訂應用程式。</p></td>
</tr>
</tbody>
</table>

