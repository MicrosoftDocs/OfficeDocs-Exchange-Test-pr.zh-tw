---
title: '使用批次移轉至 Exchange 2013 公用資料夾移轉至 Exchange Online: Exchange Online Help'
TOCTitle: 使用批次移轉至 Exchange 2013 公用資料夾移轉至 Exchange Online
ms:assetid: 25a5234c-dd2c-487b-8541-3655fbeb030a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Mt798260(v=EXCHG.150)
ms:contentKeyID: 74432752
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用批次移轉至 Exchange 2013 公用資料夾移轉至 Exchange Online

 

_**上次修改主題的時間：**2018-03-26_

**摘要：** 本文會告訴您如何從 Exchange 2013 的現代的公用資料夾移至 Office 365。

將您的 Exchange 2013 公用資料夾遷移至 Exchange Online 需要 Exchange Server 2013 CU15 或更新版本執行內部部署環境中。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您組織中有 Exchange 2013 和 Exchange 2016 的公用資料夾與您想要移往所有 Exchange Online，使用<a href="https://go.microsoft.com/fwlink/p/?linkid=845314">本文的 Exchange 2016 版本</a>來規劃及執行移轉。Exchange 2013 伺服器仍需要有 CU15 或稍後安裝。</td>
</tr>
</tbody>
</table>


## 開始之前有哪些須知？

  - 當您升級為 Exchange Server 2013 CU15 或更新版本時，您還必須先準備 Active Directory 或公用資料夾移轉將會失敗。此 Active Directory 準備工作，可確保所有相關的 PowerShell cmdlet 以及參數提供給您準備及執行移轉。請參閱[準備 Active Directory 及網域](prepare-active-directory-and-domains-exchange-2013-help.md)如需詳細資訊。

  - 在 Exchange Online 中，您需要為組織管理角色群組的成員。此角色群組是不同 Office 365 或 Exchange Online 訂閱時指派給您的權限。如需如何啟用 「 組織管理角色群組的詳細資訊，請參閱[管理角色群組](manage-role-groups-exchange-2013-help.md)。

  - 在 Exchange Server 2013，您需要為組織管理或伺服器管理 RBAC 角色群組的成員。如需詳細資訊，請參閱[新增成員至角色群組](https://go.microsoft.com/fwlink/?linkid=299212)。

  - 公用資料夾移轉，如果您組織中的任何單一公用資料夾大於 25 GB 之前，建議您刪除該資料夾以進行較小、 內容或劃分為公用資料夾的多個、 較小的公用資料夾內容。請注意以下引用 25 GB 限制只適用於公用資料夾而不適用於有問題的資料夾可能會有任何子系或子資料夾。如果這兩個選項是可行的我們建議的您並未移動公用資料夾至 Exchange Online。如需詳細資訊，請參閱[Exchange Online 限制](https://go.microsoft.com/fwlink/p/?linkid=391188)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您在 Exchange Online 中的目前公用資料夾配額少於 25 GB，您可以使用<a href="https://go.microsoft.com/fwlink/p/?linkid=844062">Set-organizationconfig 指令程式</a>來增加這些 DefaultPublicFolderIssueWarningQuota 和 DefaultPublicFolderProhibitPostQuota 參數。</td>
    </tr>
    </tbody>
    </table>


  - 在 Office 365 和 Exchange Online，您可以建立最大值為 1000年公用資料夾信箱。

  - 如果您想要將使用者移轉至 Office 365，您應該完成移轉您的公用資料夾之前先使用者移轉。如需詳細資訊，請參閱 ＜[移轉至 Office 365 的多個電子郵件帳戶的方式](https://go.microsoft.com/fwlink/p/?linkid=842798)。

  - 需要至少一部 Exchange 伺服器，也會主控公用資料夾信箱伺服器上啟用 MRS Proxy。請參閱[啟用遠端移動 MRS Proxy 端點](enable-the-mrs-proxy-endpoint-for-remote-moves-exchange-2013-help.md)如需詳細資訊。

  - 若要執行本文中的移轉程序，您無法使用 Exchange 系統管理中心 (EAC)。而您需要在 Exchange 2013 伺服器上使用 Exchange 管理命令介面。在 Exchange Online 中，您需要使用 Exchange Online PowerShell。如需詳細資訊，請參閱[Connect to Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=842801)。

  - 移轉已刪除的項目，且支援來自 Exchange 2013 已刪除的資料夾遷移至 Exchange Online。開始移轉之前，建議您檢閱所有已刪除的資料夾和資料夾項目並永久刪除您不需要使用 Exchange Online 的任何項目。請注意之後的某個項目會永久刪除它無法復原。
    
    您可以使用下列命令以列出 Exchange 中已刪除公用資料夾暫放 （Exchange 內部部署環境中）：
    
        Get-PublicFolder \NON_IPM_SUBTREE\DUMPSTER_ROOT -Recurse | ?{$_.FolderClass -ne "$null"} | ft name,foldersize
    
    若要永久刪除特定的資料夾，請使用下列命令 （此範例會使用名為 'Calendar2' 的資料夾）：
    
        Get-PublicFolder \NON_IPM_SUBTREE\DUMPSTER_ROOT -Recurse | ?{$_.FolderClass -ne "$null" -and $_.Name -eq "Calendar2"} | Remove-PublicFolder

  - 開始之前，請閱讀本文全文。某些步驟有所需的停機時間。在此停機時間、 期間將無法人都能夠存取公用資料夾。

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


## 步驟 1： 下載移轉指令碼

1.  從[Exchange 2013/2016年公用資料夾移轉指令碼](https://go.microsoft.com/fwlink/p/?linkid=844893)下載所有指令碼和支援的檔案。

2.  將指令碼儲存至將要執行 PowerShell 的本機電腦。例如，C:\\PFScripts。請確定所有的指令碼儲存在相同的位置。

這些指令碼與您要下載的檔案為：

  - `Sync-ModernMailPublicFolders.ps1` 此指令碼進行同步處理在內部部署 Exchange 環境與 Office 365 之間的郵件功能的公用資料夾物件。您將 Exchange 2013 伺服器上執行此指令碼。

  - `SyncModernMailPublicFolders.strings.psd1` 此支援檔案由同步處理 ModernMailPublicFolders.ps1 指令碼及應下載到相同位置。

  - `Export-ModernPublicFolderStatistics.ps1` 此指令碼會建立的資料夾名稱至資料夾大小和已刪除的項目大小的對應檔案。您將 Exchange 2013 伺服器上執行此指令碼。

  - `Export-ModernPublicFolderStatistics.strings.psd1` 此支援檔案由匯出 ModernPublicFolderStatistics.ps1 指令碼及應下載到相同位置。

  - `ModernPublicFolderToMailboxMapGenerator.ps1` 此指令碼的輸出匯出 ModernPublicFolderStatistics.ps1 指令碼會建立公用資料夾至信箱的對應檔案。您將 Exchange 2013 伺服器上執行此指令碼。

  - `ModernPublicFolderToMailboxMapGenerator.strings.psd1` 此支援檔案由 ModernPublicFolderToMailboxMapGenerator.ps1 指令碼及應下載到相同位置。

  - `SetMailPublicFolderExternalAddress.ps1` 此指令碼更新`ExternalEmailAddress`擁有郵件功能之內部環境中的公用資料夾的其 Exchange Online 與對應功能。這可確保移轉後，預設傳送給擁有郵件功能的公用資料夾的電子郵件會正確路由傳送至 Exchange Online。您需要在 Exchange 2013 伺服器上執行此指令碼。

  - `SetMailPublicFolderExternalAddress.strings.psd1` 此支援檔案由 SetMailPublicFolderExternalAddress.ps1 指令碼及應下載到相同位置。

## 步驟 2：準備移轉

開始之前的公用資料夾移轉，下列各節中執行所有必要步驟。

**一般的必要步驟**

進行能順利移轉，您應該：

  - 請確定任何孤立的公用資料夾郵件物件中沒有 Active Directory。這些是在 Active Directory 中沒有對應的 Exchange 物件的物件。

  - 確認設定為 \[Active Directory 中的公用資料夾的 SMTP 電子郵件地址符合 Exchange 物件上的 SMTP 電子郵件地址。

  - 確認 Active Directory 中有無任何重複的公用資料夾物件。這是必要若要避免擁有兩個或多個 Active Directory 物件會指向相同擁有郵件功能的公用資料夾。

**在內部部署 Exchange 2013 server 環境中的必要步驟**

在 Exchange 管理命令介面 （內部） 會執行下列步驟：

1.  移轉完成後，它會需要一些時間讓 DNS 快取網際網路直接在新的位置，您擁有郵件功能的公用資料夾的郵件在 Exchange Online。您可以確保該您新遷移擁有郵件功能的公用資料夾接收訊息此 DNS 轉換期間所使用的已知的名稱建立公認的網域。若要這樣做，請 Exchange 內部部署環境中執行下列命令。在本例中為`target domain`是在 Office 365 或 Exchange Online 網域的傳送連接器已經已由 \[混合組態精靈\]。
    
        New-AcceptedDomain -Name PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99 -DomainName <target domain> -DomainType InternalRelay
    
    **範例：**
    
        New-AcceptedDomain -Name PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99 -DomainName "contoso.mail.onmicrosoft.com" -DomainType InternalRelay
    
    如果您的內部部署環境中的公認的網域已存在，它重新命名為`PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99`並保持不變的其他屬性。
    
    若要檢查是否已存在於內部部署環境中公認的網域：
    
        Get-AcceptedDomain | Where { $_.DomainName -eq "<target domain>" }
    
    若要重新命名公認的網域至`PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99`，執行下列命令：
    
        Get-AcceptedDomain | Where { $_.DomainName -eq "<target domain>" } | Set-AcceptedDomain -Name PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您的預期在 Exchange Online 中接收來自網際網路的外部電子郵件，您擁有郵件功能的公用資料夾，您必須停用目錄架構邊緣封鎖 (DBEB) Exchange Online 和 Exchange Online Protection (EOP) 中。請參閱<a href="https://technet.microsoft.com/zh-tw/library/dn600322(v=exchg.150)">使用目錄架構邊緣封鎖以拒絕傳送至無效收件者的郵件</a>如需詳細資訊。</td>
    </tr>
    </tbody>
    </table>


2.  如果公用資料夾的名稱包含反斜線**\\**或正斜線**/**，它可能不取得移轉至其指定的信箱移轉程序期間。在遷移之前，重新命名這類資料夾中移除這些字元
    
    1.  若要找出名稱中有反斜線的公用資料夾，執行下列命令：
        
            Get-PublicFolder -Recurse -ResultSize Unlimited | Where {$_.Name -like "*\*" -or $_.Name -like "*/*"} | Format-List Name, Identity, EntryId
    
    2.  如果傳回任何公用資料夾，可以執行下列命令將其重新命名：
        
            Set-PublicFolder -Identity "<public folder EntryId>" -Name "<new public folder name>"

3.  執行下列步驟以確認沒有先前成功移轉您組織中的記錄。如果沒有，必須將該值設`$false`。
    
    變更之前的值，請確認舊版的移轉嘗試可以會捨棄使您不小心不要執行第二個移轉。
    
    1.  執行下列命令以檢查任何先前移轉，以及這些遷移的狀態：
        
            Get-OrganizationConfig | Format-List PublicFoldersLockedforMigration, PublicFolderMigrationComplete, PublicFolderMailboxesLockedForNewConnections, PublicFolderMailboxesMigrationComplete
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>如果<code>PublicFoldersLockedforMigration</code>或<code>PublicFolderMigrationComplete</code>參數<code>$true</code>，就表示您已在某些舊版公用資料夾遷移。請確定任何舊版公用資料夾資料庫已解除委任才可以繼續步驟 3b。</td>
        </tr>
        </tbody>
        </table>
    
    2.  如果上述任一會傳回值設為`$true`，使其`$false`執行：
        
            Set-OrganizationConfig -PublicFoldersLockedforMigration:$false -PublicFolderMigrationComplete:$false -PublicFolderMailboxesLockedForNewConnections:$false -PublicFolderMailboxesMigrationComplete:$false

4.  基於確認其完成移轉成功，我們建議您在適當的所有 Exchange 2013 伺服器上執行下列命令。這將會採取的目前的公用資料夾部署，您可以稍後使用進行比較新遷移的公用資料夾的快照。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>根據您的 Exchange 組織的大小，則可能需要一些時間讓執行這些命令。</td>
    </tr>
    </tbody>
    </table>
    
      - 執行下列命令以擷取原始來源資料夾結構的快照。
        
            Get-PublicFolder -Recurse -ResultSize Unlimited | Export-CliXML OnPrem_PFStructure.xml
    
      - 執行下列命令以擷取公用資料夾統計資料的快照，例如項目計數、大小、擁有者。
        
            Get-PublicFolderStatistics -ResultSize Unlimited | Export-CliXML OnPrem_PFStatistics.xml
    
      - 執行下列命令以取得快照的公用資料夾權限。
        
            Get-PublicFolder -Recurse -ResultSize Unlimited | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML OnPrem_PFPerms.xml
    
      - 執行下列命令以取得快照的擁有郵件功能的公用資料夾：
        
            Get-MailPublicFolder -ResultSize Unlimited | Export-CliXML OnPrem_MEPF.xml
    
      - 儲存來自前述命令在安全的地方才能進行移轉結尾處的比較產生的檔案。

5.  如果您使用 Microsoft Azure Active Directory 連線 （Azure AD 連線） 與 Azure Active Directory 同步處理內部部署目錄，您必須採取下列動作 （如果您不使用 Azure AD 連線，您可以略過此步驟）：
    
    1.  內部部署電腦上，開啟 Microsoft Azure Active Directory 連線，並再選取 \[**設定\]**。
    
    2.  在**其他工作**\] 畫面上，選取**自訂同步處理選項**\] 然後再按 \[**下一步**。
    
    3.  在**連線至 Azure AD** \] 畫面上，輸入適當的憑證，並再按 \[**下一步**。一旦連線、 保留按一下 \[**下一步**直到您是**選用的功能**螢幕上。
    
    4.  請確定未選取 \[ **Exchange 郵件公用資料夾**。如果未選取，您可以繼續下一步\] 區段*的先決條件步驟在 Exchange Online*。如果選取，按一下來清除\] 核取方塊，並再按 \[**下一步**。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>如果您未看見<strong>Exchange 郵件公用資料夾</strong>是<strong>選用的功能</strong>] 畫面上的選項，您可以結束 Microsoft Azure Active Directory 連線並繼續進行下一步] 區段<em>的先決條件步驟在 Exchange Online</em>。</td>
        </tr>
        </tbody>
        </table>
    
    5.  已清除**Exchange 郵件公用資料夾**選取項目之後，請按一下 \[**下一步**，直到您已**準備好設定**在畫面上，然後按一下 \[**設定**。

**Exchange Online 中的先決條件步驟**

在 Exchange Online PowerShell 中執行下列動作：

1.  確保沒有任何現有的公用資料夾移轉要求。如果有，請清除其或您自己的移轉要求將會失敗。這是步驟只需要如果您認為可能有現有的移轉要求 （其中已經失敗或您想要中止） 管線中。
    
    現有的移轉要求可以是下列其中一種： 批次移轉或序列移轉。偵測，並移除、 要求每一種命令如下所示。
    
    下列範例會將探索任何現有的序列的移轉要求。
    
        Get-PublicFolderMigrationRequest | Get-PublicFolderMigrationRequestStatistics 
    
    下列範例會移除任何現有的公用資料夾序列的移轉要求：
    
        Get-PublicFolderMigrationRequest | Remove-PublicFolderMigrationRequest
    
    下列範例會將探索任何現有的批次移轉要求。
    
        Get-MigrationBatch | ?{$_.MigrationType.ToString() -eq "PublicFolder"}
    
    下列範例會移除任何現有的公用資料夾批次移轉要求：
    
        Remove-MigrationBatch <name of migration batch> -Confirm:$false

2.  您需要有**PAW**啟用您的 Office 365 租用戶移轉功能。您可以在 Exchange Online PowerShell 中執行下列命令來檢查：
    
        Get-MigrationConfig
    
    如果 \[**功能**下的輸出**PAW**，然後啟用的功能和您可以繼續下一個步驟。
    
    如果不是爪尚未啟用您的租用戶，它可能是因為您有一些現有的遷移批次，公用資料夾批次或使用者批次。這些批次可能是任何的狀態，包括已完成。如果是這樣，請完成並移除任何遷移批次直到您執行`Get-MigrationBatch`時不會傳回任何記錄。移除所有現有的批次之後, 爪應取得自動啟用。請注意，變更可能不會反映在`Get-MigrationConfig`立即，但沒有關係。但如果是使用者移轉，您可以繼續建立新的批次之後完成此步驟。

3.  請確定任何現有的公用資料夾或 Exchange Online 中的公用資料夾信箱。如果您執行 Exchange 中探索公用資料夾後的步驟，其下方的重要決定為何他們有與組織中誰啟動之前的公用資料夾階層的線上開始移除任何公用資料夾和公用資料夾信箱。
    
    1.  在 Office 365 或 Exchange Online PowerShell 中執行下列命令，查看是否有任何公用資料夾信箱存在。
        
            Get-Mailbox -PublicFolder
    
    2.  如果此命令不會傳回任何公用資料夾信箱，請繼續進行步驟 3： 產生.csv 檔案。如果命令沒有傳回任何公用資料夾信箱，請執行下列命令，以查看是否有任何公用資料夾存在：
        
            Get-PublicFolder -Recurse
    
    3.  如果您不要有任何 Office 365 或 Exchange Online 中的公用資料夾，請執行下列 PowerShell 命令加以移除 （之後確認他們不需要）。請確定因為當您移除的公用資料夾永久刪除所有資訊已儲存這些公用資料夾內刪除之前, 的任何資訊。
        
            Get-MailPublicFolder -ResultSize Unlimited | where {$_.EntryId -ne $null}| Disable-MailPublicFolder -Confirm:$false 
            Get-PublicFolder -GetChildren \ -ResultSize Unlimited | Remove-PublicFolder -Recurse -Confirm:$false
    
    4.  會移除公用資料夾之後，請執行下列命令來移除所有的公用資料夾信箱：
        
            $hierarchyMailboxGuid = $(Get-OrganizationConfig).RootPublicFolderMailbox.HierarchyMailboxGuid
            Get-Mailbox -PublicFolder | Where-Object {$_.ExchangeGuid -ne $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
            Get-Mailbox -PublicFolder | Where-Object {$_.ExchangeGuid -eq $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
            Get-Mailbox -PublicFolder -SoftDeletedMailbox | Remove-Mailbox -PublicFolder -PermanentlyDelete:$true 

## 步驟 3： 產生.csv 檔案

使用先前下載指令碼以產生.csv 檔案所採取的移轉。

1.  （內部） Exchange 管理命令介面中執行`Export-ModernPublicFolderStatistics.ps1`指令碼來建立資料夾名稱至資料夾大小的對應檔案。您必須具備本機系統管理員權限才能執行此指令碼。產生的檔案會包含三個欄： **FolderName**、 **FolderSize**，以及**DeletedItemSize**。**FolderSize**和**DeletedItemSize**欄的值將會顯示以位元組為單位。例如**\\PublicFolder01,10240、 100**表示在名為 PublicFolder01 您階層的根目錄中的公用資料夾的大小是 10240 位元組或 10.240 MB，且有 100 個位元組的可復原的項目中。
    
        .\Export-ModernPublicFolderStatistics.ps1 <Folder-to-size map path>
    
    **範例：**
    
        .\Export-ModernPublicFolderStatistics.ps1 stats.csv

2.  執行`ModernPublicFolderToMailboxMapGenerator.ps1`指令碼來建立.csv 檔案對應於 Exchange Online 的目的地的公用資料夾信箱的來源的公用資料夾。此檔案用來計算 Exchange Online 中公用資料夾信箱的正確的號碼。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><code>ModernPublicFolderToMailboxMapGenerator.ps1</code>所產生的檔案不會包含在組織中每個公用資料夾的名稱。它會包含參照到父項資料夾的較大的資料夾樹狀目錄或資料夾的名稱哪些本身會大幅大型。您可考量此檔案的 「 例外狀況 」 檔案用來確定特定資料夾樹狀結構和較大的資料夾取得放入特定的公用資料夾信箱方塊。請正常沒有看到 [公用資料夾此檔案中的每一部。（除非明確地將其導向到不同的公用資料夾信箱的對應檔案內的另一個線條上另提及），此對應檔案中所列的任何資料夾的子資料夾也移轉至相同的公用資料夾信箱作為其上層資料夾。</td>
    </tr>
    </tbody>
    </table>
    
        .\ModernPublicFolderToMailboxMapGenerator.ps1 <Maximum mailbox size in bytes><Maximum mailbox recoverable item size in bytes><Folder-to-size map path><Folder-to-mailbox map path>
    
      - `Maximum mailbox size in bytes`是您要移轉到任何單一公用資料夾信箱在 Exchange Online 的資料數量上限。此欄位的大小上限目前 50 GB，但建議您依照較小的大小，例如 50%的大小上限，以供未來的擴充需要。
    
      - `Maximum mailbox recoverable items size in bytes`是在您的 Exchange Online 信箱的可復原的項目配額。在 Exchange Online 中公用資料夾信箱的大小上限目前為 50 GB。建議您將` RecoverableItemsQuota`設定為 15 GB 或更低。
    
      - `Folder-to-size map path`是執行`Export-ModernPublicFolderStatistics.ps1`指令碼時所建立之.csv 檔案的檔案路徑。
    
      - `Folder-to-mailbox map path`是您要在此步驟中建立資料夾至信箱.csv 檔案的檔案路徑。如果您只指定的檔案名稱，該檔案會產生於本機電腦的目前 PowerShell 目錄中。

**範例：**

    .\ModernPublicFolderToMailboxMapGenerator.ps1 -MailboxSize 25GB -MailboxRecoverableItemSize 1GB -ImportFile .\stats.csv -ExportFile map.csv

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>我們不支援將公用資料夾遷移至 Exchange Online 的 Exchange Online 中的唯一的公用資料夾信箱數目時超過 100。</td>
</tr>
</tbody>
</table>


## 步驟 4： 在 Exchange Online 中建立公用資料夾信箱

接下來，在 Exchange Online PowerShell 中建立目標公用資料夾信箱將包含您已移轉的公用資料夾。

1.  執行下列指令碼來建立目標公用資料夾信箱。指令碼會建立先前產生的.csv 檔案中的每個信箱的目標信箱*步驟 3： 產生.csv 檔案*、 執行`ModernPublicFoldertoMailboxMapGenerator.ps1`指令碼時。
    
        $mappings = Import-Csv <Folder-to-mailbox map path>
        $primaryMailboxName = ($mappings | Where-Object FolderPath -eq "\" ).TargetMailbox
        New-Mailbox -HoldForMigration:$true -PublicFolder -IsExcludedFromServingHierarchy:$false $primaryMailboxName 
        ($mappings | Where-Object TargetMailbox -ne $primaryMailboxName).TargetMailbox | Sort-Object -unique | ForEach-Object { New-Mailbox -PublicFolder -IsExcludedFromServingHierarchy:$false $_ }
    
      - `Folder-to-mailbox map path`是由`ModernPublicFoldertoMailboxMapGenerator.ps1`指令碼中產生之資料夾至信箱.csv 檔案的檔案路徑*步驟 3： 產生.csv 檔案*。

## 步驟 5： 啟動遷移要求

命令的數字現在需要執行 Exchange 2013 內部部署環境中與 Exchange Online。

1.  從任何公用資料夾信箱託管 Exchange 2013 伺服器，執行下列指令碼。此指令碼會同步處理具有郵件功能的公用資料夾從本機 Active Directory 至 Exchange Online。請確定您已下載最新版的這個指令碼並確認已執行 Exchange 管理命令介面。
    
        .\Sync-ModernMailPublicFolders.ps1 -Credential (Get-Credential) -CsvSummaryFile:sync_summary.csv
    
      - `Credential`為您的 Exchange Online 系統管理的使用者名稱和密碼。
    
      - `CsvSummaryFile`是您想要同步處理作業及錯誤位於您記錄檔的檔案路徑。記錄檔會是格式為.csv。

2.  在 Exchange 2013 伺服器上，尋找 MRS proxy 端點伺服器並記下其。您必須執行遷移要求此資訊。儲存步驟 3b 下此資訊。

3.  在 Exchange Online PowerShell 中執行下列命令將上一個步驟的認證資訊及 MRS 資訊傳遞至指令程式將在遷移要求中使用的變數。
    
    1.  傳遞至變數`$Source_Credential`Exchange 2013 內部部署環境中具有管理員權限的使用者認證。您在執行 Exchange Online 的移轉要求將會使用此認證來存取內部部署 Exchange 2013 伺服器，將內容一段的公用資料夾複製到 Exchange Online。
        
            $Source_Credential = Get-Credential <source_domain>\<PublicFolder_Administrator_Account>
    
    2.  執行 Exchange 2013 環境您在上面的步驟 2 找到並將其傳至變數中的 MRS Proxy 伺服器資訊：
        
            $Source_RemoteServer = "<paste the value here>"

4.  在 Exchange Online PowerShell 中執行下列命令來建立公用資料夾遷移端點和公用資料夾移轉要求：
    
        $PfEndpoint = New-MigrationEndpoint -PublicFolder -Name PublicFolderEndpoint -RemoteServer $Source_RemoteServer -Credentials $Source_Credential
         
        [byte[]]$bytes = Get-Content -Encoding Byte <folder_mapping.csv>
        
        New-MigrationBatch -Name PublicFolderMigration -CSVData $bytes -SourceEndpoint $PfEndpoint.Identity -NotificationEmails <email addresses for migration notifications>
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>請使用逗號分隔多個電子郵件地址。</td>
    </tr>
    </tbody>
    </table>
    
    其中`folder_mapping.csv`是在產生的對應檔案*步驟 3： 建立.csv 檔案*。請務必提供的完整檔案路徑。如果對應檔案已移動有任何原因，請務必使用新的位置。

5.  最後，開始移轉 Exchange Online PowerShell 中使用下列命令：
    
        Start-MigrationBatch PublicFolderMigration

批次移轉需要建立在 Exchange Online PowerShell 中使用 New-migrationbatch 指令程式，當進度和完成移轉的可以檢視及管理在 EAC 中或執行 Get-migrationbatch cmdlet。New-migrationbatch 指令程式會信箱移轉要求的每個公用資料夾信箱，且您可以檢視信箱移轉\] 頁面上使用這些要求的狀態。

移至 \[信箱移轉\] 頁面上：

1.  登入 Exchange Online 並開啟 EAC。

2.  瀏覽至 \[**收件者**，然後再選取 \[**移轉**。

3.  選取剛建立的移轉要求，然後在**詳細資料**\] 窗格中，選取 \[**檢視詳細資料**。

移入之前*步驟 6： 鎖定 Exchange 2013 伺服器上的公用資料夾*，確認已複製所有資料及移轉中沒有任何錯誤。一旦您確認批次移動到**已同步**的狀態、 執行中所述的命令*步驟 2： 準備移轉*、 最後一步驟中 \[**內部部署 Exchange 2013 伺服器環境中的先決條件步驟**，為公用資料夾內部的快照。一旦執行這些命令，您可以繼續下一個步驟。請注意這些命令可能需要一段時間才能完成取決於您擁有的資料夾數目。

## 步驟 6： 鎖定進行最終移轉 （需公用資料夾停機） Exchange 2013 環境中的公用資料夾

移轉程序為止，直到使用者已能夠存取您的內部部署公用資料夾。下列步驟將會立即登出使用者從 Exchange 2013 公用資料夾，然後鎖定資料夾為移轉程序完成其最終同步處理。使用者將無法存取公用資料夾在這段時間，並傳送這些擁有郵件功能的公用資料夾的任何郵件會排入佇列並持續開始，直到公用資料夾移轉已完成。

在執行`PublicFolderMailboxesLockedForNewConnections`命令如下所示之前，請確定所有工作都是**已同步**狀態。您可以執行`Get-PublicFolderMailboxMigrationRequest`命令來這麼做。您已驗證的所有工作都會在**已同步**狀態後繼續執行此步驟。

在內部部署環境中，執行下列命令鎖定最終的 Exchange 2013 公用資料夾。

    Set-OrganizationConfig -PublicFolderMailboxesLockedForNewConnections $true

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您不可以存取<code>-PublicFolderMailboxesLockedForNewConnections</code>參數，可能是因為在目前的升級期間未準備 Active Directory 為我們建議您在上述<em>您需要知道之前吗？</em>請參閱<a href="prepare-active-directory-and-domains-exchange-2013-help.md">準備 Active Directory 及網域</a>如需詳細資訊。<br />
也請注意，任何需要存取公用資料夾的使用者應首先，移轉<strong>之前</strong>您移轉公用資料夾本身。</td>
</tr>
</tbody>
</table>


如果您的組織有多個 Exchange 2013 伺服器上的公用資料夾信箱，必須等到 AD 複寫已完成。一旦完成，您可以確認所有的公用資料夾信箱有挑選`PublicFolderMailboxesLockedForNewConnections`旗標及該任何擱置中最近對其公用資料夾的使用者具有收斂整個組織的變更。所有可能需要數小時。

## 步驟 7： 完成公用資料夾移轉 （需公用資料夾停機）

您可以完成您的公用資料夾移轉之前，您必須確認有無其他公用資料夾信箱移動或公用資料夾移動使邁向內部部署 Exchange 環境中。若要執行這項作業，請使用`Get-MoveRequest`和`Get-PublicFolderMoveRequest` cmdlet 可列出任何現有的公用資料夾移動。如果有任何進行中，或在**完成**狀態的移動，請加以移除。

下一步\] 以完成公用資料夾移轉，請在 Exchange Online PowerShell 中執行下列命令：

    Complete-MigrationBatch PublicFolderMigration

當您執行此命令時，Exchange 會執行 Exchange 內部部署組織與 Exchange Online 之間的最終同步處理。在此期間的遷移批次狀態會變更從**已同步完成**，然後最後為 \[**已完成**。如果最終同步處理成功，Exchange Online 中的公用資料夾會解除鎖定。

常見的遷移批次所從**已同步**其狀態變更前的幾小時才需**完成**，最終同步處理會開始在其中點。

## 步驟 8： 測試並解除鎖定 Exchange Online 中的公用資料夾

公用資料夾移轉完成後，執行下列步驟來測試移轉成功，並正式確認其完成。這些最終工作可讓您永久切換組織至 Exchange Online 公用資料夾之前測試遷移的公用資料夾階層。

1.  在 Exchange Online PowerShell 中指派一些測試使用者信箱移轉至其中一個新遷移的公用資料夾信箱作為預設公用資料夾信箱。：
    
        Set-Mailbox -Identity <test user> -DefaultPublicFolderMailbox <public folder mailbox identity>
    
    請確定您的測試使用者必須建立公用資料夾的必要權限。

2.  您在先前步驟中，指定並採取下列公用資料夾測試的測試使用者登入 Outlook。請注意，可能需要 15 到 30 分鐘的變更才會生效。Outlook 知道所做的變更後，它可能會提示您重新啟動一些時間。
    
    1.  檢視階層。
    
    2.  檢查權限。
    
    3.  建立一些公用資料夾，並予以刪除。
    
    4.  張貼內容，以及刪除內容從公用資料夾。
    
    如果您執行發生任何問題，並決定您準備不好要切換完全至 Exchange Online 組織的公用資料夾，請參閱[回復公用資料夾移轉從 Exchange 2013 至 Exchange Online](roll-back-a-public-folder-migration-from-exchange-2013-to-exchange-online-exchange-2013-help.md)。

3.  執行下列命令在 Exchange Online PowerShell 來解除鎖定公用資料夾在 Exchange Online。執行此命令之後，可能需要大約 15 到 30 分鐘的時間變更才會生效。Outlook 會變成知道所做的變更之後，它可能會提示您重新啟動程式好幾次的使用者。
    
        Set-OrganizationConfig -RemotePublicFolderMailboxes $Null -PublicFoldersEnabled Local

## 步驟 9： 完成移轉內部

若要啟用郵件功能的公用資料夾內部電子郵件，請遵循下列步驟：

1.  在內部部署環境中，執行下列指令碼以確定所有擁有郵件功能的公用資料夾的電子郵件會正確路由傳送至 Exchange Online。指令碼會加上戳記擁有郵件功能的公用資料夾以指向其 Exchange Online 與對應功能`ExternalEmailAddress` ：
    
        .\SetMailPublicFolderExternalAddress.ps1 -ExecutionSummaryFile:mepf_summary.csv

2.  如果您測試成功，您的內部部署環境中，執行下列命令以指出公用資料夾移轉完成：
    
        Set-OrganizationConfig -PublicFolderMailboxesMigrationComplete:$true -PublicFoldersEnabled Remote

## 如何知道這是否正常運作？

在步驟 2： 準備移轉、 所需的內部部署公用資料夾結構、 統計資料和權限的快照集。下列步驟將協助您確認您的公用資料夾移轉成功在 Exchange Online 的移轉後採取相同的快照集。比較若要驗證成功這兩個檔案中的資料。

1.  在 Exchange Online PowerShell 中執行下列命令以取得新的資料夾結構的快照：
    
        Get-PublicFolder -Recurse -ResultSize Unlimited | Export-CliXML Cloud_PFStructure.xml

2.  在 Exchange Online PowerShell 中執行下列命令以取得快照的公用資料夾統計資料，包括項目計數、 大小以及擁有者：
    
        Get-PublicFolder -Recurse -ResultSize Unlimited | Get-PublicFolderStatistics | Export-CliXML Cloud_PFStatistics.xml

3.  在 Exchange Online PowerShell 中執行下列命令以取得快照的權限：
    
        Get-PublicFolder -Recurse -ResultSize Unlimited | Get-PublicFolderClientPermission | Select-Object Identity,User, AccessRights | Export-CliXML Cloud_PFPerms.xml

4.  在 Exchange Online PowerShell 中執行下列命令以取得快照的擁有郵件功能的公用資料夾：
    
        Get-MailPublicFolder -ResultSize Unlimited | Export-CliXML Cloud_MEPF.xml

## 已知問題

以下是您在組織中可能會遇到的常見公用資料夾移轉問題。

  - 我們不支援將公用資料夾遷移至 Exchange Online 的 Exchange Online 中的唯一的公用資料夾信箱數目時超過 100。

  - 權限的根公用資料夾和 EFORMS 登錄資料夾將不會移轉至 Exchange Online 與您必須手動套用在 Exchange Online。若要這樣做，請在您的 Exchange Online PowerShell 中執行下列命令。針對每個內部存在的權限項目一次執行此命令但遺失在 Exchange Online：
    
        Add-PublicFolderClientPermission "\" -User <user> -AccessRights <access rights>
        Add-PublicFolderClientPermission "\NON_IPM_SUBTREE\EFORMS REGISTRY" -User <user> -AccessRights <access rights>

  - 如果某些公用資料夾信箱不會提供公用資料夾階層，某些公用資料夾移轉將會失敗。這表示上一或多個信箱`IsExcludedFromServingHierarchy`參數設置為`$true`。若要避免此問題，請將所有信箱 in Exchange Online 服務階層。

  - **下列傳送\]**和 \[**代理傳送者**權限不取得移轉至 Exchange Online。如果發生這種情況與移轉，請內部部署環境中使用下列命令注意有這些權限。
    
    若要查看哪些公用資料夾有下列傳送\] 權限在內部部署：
    
        Get-MailPublicFolder | Get-ADPermission | ?{$_.ExtendedRights -like "*Send-As*"}
    
    若要查看哪些公用資料夾有代理傳送者的權限在內部部署：
    
        Get-MailPublicFolder | ?{$_.GrantSendOnBehalfTo -ne "$null"} | ft name,GrantSendOnBehalfTo
    
    將傳送為 」 權限新增至擁有郵件功能的公用資料夾在 Exchange Online，在 Exchange Online PowerShell 輸入：
    
        Add-RecipientPermission -Identity <mail-enabled public folder primary SMTP address> -Trustee <name of user to be assigned permission> -AccessRights SendAs
    
    **範例：**
    
        Add-RecipientPermission -Identity send1 -Trustee Exo1 -AccessRights SendAs
    
    若要新增傳送代理擁有郵件功能的公用資料夾的權限在 Exchange Online、 Exchange Online PowerShell 輸入：
    
        Set-MailPublicFolder -Identity <name of public folder> -GrantSendOnBehalfTo <user or comma-separated list of users>
    
    **範例：**
    
        Set-MailPublicFolder send2 -GrantSendOnBehalfTo exo1,exo2

  - "\\NON\_IPM\_SUBTREE\\DUMPSTER\_ROOT"資料夾下有 10000 個以上的資料夾會導致移轉失敗。因此，檢查有 10000 個以上的資料夾直接下它 （即時子項目） 的"\\NON\_IPM\_SUBTREE\\DUMPSTER\_ROOT"資料夾。您可以使用下列命令來尋找公用資料夾數目在下列位置：
    
        (Get-PublicFolder -GetChildren "\NON_IPM_SUBTREE\DUMPSTER_ROOT").Count 
    
    Exchange Online 不支援 10000 個以上的子資料夾，這是原因的 10000 個以上的資料夾遷移將會失敗。我們目前開發指令碼以解除封鎖這類的設定。同時，我們建議等待遷移公用資料夾。

  - 移轉工作不會進行進度或已停止。這可以發生如果有太多工作同時執行，而造成失敗發生間歇性錯誤的工作。您可以藉由修改`MaxConcurrentMigrations`和`MaxConcurrentIncrementalSyncs`為較小的數字減少並行工作數目。使用下列範例會設定下列值：
    
        Set-MigrationEndpoint <PublicFolderEndpoint> -MaxConcurrentMigrations 30 -MaxConcurrentIncrementalSyncs 20  -SkipVerification 

  - 移轉工作失敗錯誤 「 錯誤： 暫放資料夾的暫放。 」如果您看到此錯誤時，它應該解決如果停止批次並再重新啟動。

  - 移轉工作失敗而產生"要求遭隔離時因為下列錯誤： 指定的索引鍵不存在字典中 」 錯誤訊息。損毀的項目是出現在移轉工作不能將複製的資料夾時會發生此情況。若要解決此問題：
    
    1.  停止移轉批次。
    
    2.  找出包含錯誤的項目\] 資料夾。移轉報告應該包含錯誤發生時所要複製之資料夾的參照。
    
    3.  在內部部署環境中，將受影響的資料夾移至主要公用資料夾信箱。您可以使用`New-PublicFolderMoveRequest`指令程式來移動資料夾。
    
    4.  等待資料夾移至完成。完成之後，移除的移動要求。然後重新啟動遷移批次。

## 從 Exchange 內部部署環境中移除公用資料夾信箱

移轉已完成且已驗證 Exchange Online 中的公用資料夾運作如預期及包含所有預期的資料之後，您可以移除您在內部部署公用資料夾信箱。

請注意這個步驟不能取消，因為一旦刪除公用資料夾信箱無法復原。因此，我們強烈建議除了驗證移轉成功，您也監視 Exchange Online 公用資料夾的幾週前移除內部部署公用資料夾信箱。

