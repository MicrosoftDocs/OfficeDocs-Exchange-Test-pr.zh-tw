---
title: '從受管理的資料夾遷移: Exchange 2013 Help'
TOCTitle: 從受管理的資料夾遷移
ms:assetid: 6796a79d-501e-4216-9370-77965bc5835d
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd298032(v=EXCHG.150)
ms:contentKeyID: 52062549
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 從受管理的資料夾遷移

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-07_

Microsoft Exchange Server 2013 中，使用保留標記和保留原則來執行通訊記錄管理 (MRM)。保留原則是可以套用至信箱的一組保留標記。如需詳細資訊，請參閱[保留標記和保留原則](retention-tags-and-retention-policies-exchange-2013-help.md)。不支援受管理的資料夾 (Exchange Server 2007 中引進的 MRM 技術)。

您可以遷移已套用受管理的資料夾信箱原則的信箱，以使用保留原則。若要這樣做，您建立的保留標記必須等同於連結至使用者之受管理資料夾信箱原則的受管理資料夾。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>建議您先在測試環境中測試處理程序，再於生產環境中從受管理的資料夾遷移至保留原則。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您可以為信箱設定保留功能，以暫停處理保留原則或受管理資料夾信箱原則。在遷移案例中設定信箱的保留功能很實用，在測試信箱或少量工作信箱上測試新的原則設定之前，可避免刪除郵件或移至封存。如需詳細資訊，請參閱<a href="place-a-mailbox-on-retention-hold-exchange-2013-help.md">就地保留信箱保留 」 狀態</a>。</td>
</tr>
</tbody>
</table>


如需有關 MRM 的其他管理工作相關資訊，請參閱[通訊記錄管理程序](messaging-records-management-procedures-exchange-2013-help.md)。

## 比較保留標記與受管理的資料夾

和受管理的資料夾不同，這些資料夾需要使用者根據保留設定將項目移動到受管理的資料夾，但保留標記可以套用到信箱中的資料夾或個別項目。此處理程序最不會影響使用者的工作流程和電子郵件組織方法。當資料夾套用保留標記時，該資料夾中的所有項目都會繼承保留設定。使用者可以進一步指定保留設定，對該資料夾中的個別項目套用不同的保留標記。

受管理的資料夾支援一個資料夾有不同的受管理內容設定，且各有不同的郵件類別 (例如電子郵件項目或行事項項目)。保留標記不需要單獨的受管理內容設定物件，因為已在標記的內容中指定保留設定。除了語音信箱郵件的預設原則標記 (DPT)，不支援為特定郵件類別建立保留標記。保留標記也不允許您使用受管理的資料夾助理員所執行的日誌。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>日誌規則 (用來將郵件副本和日誌報告傳送至日誌信箱) 由日誌代理程式在傳輸管線中強制執行，而且與 MRM 無關。如需詳細資訊，請參閱<a href="journaling-exchange-2013-help.md">日誌</a>。</td>
</tr>
</tbody>
</table>


下表會比較在使用保留標記或受管理的資料夾時可用的 MRM 功能。

### 保留標記與受管理的資料夾

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>保留標記</th>
<th>受管理的資料夾</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>指定預設資料夾 (如 [收件匣]) 的保留設定</p></td>
<td><p>使用保留原則標記 (RPT)</p></td>
<td><p>使用受管理的預設資料夾</p></td>
</tr>
<tr class="even">
<td><p>指定整個信箱的保留設定</p></td>
<td><p>使用預設原則標記 (DPT)</p></td>
<td><p>使用受管理的預設資料夾</p></td>
</tr>
<tr class="odd">
<td><p>使用自訂資料夾的保留設定</p></td>
<td><p>使用個人標記</p></td>
<td><p>使用受管理的自訂資料夾</p></td>
</tr>
<tr class="even">
<td><p>需要受管理的內容設定</p></td>
<td><p>否 (保留設定包含在保留標記中)</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>使用不同郵件類別 (例如電子郵件、語音信箱或行事曆項目) 的保留設定</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>支援「移到封存」動作，此動作會將項目移動到使用者的封存信箱</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>支援「移到受管理的資料夾」動作</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>允許使用受管理的資料夾助理員來記錄日誌</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>套用到使用者的原則</p></td>
<td><p>保留原則</p></td>
<td><p>受管理的資料夾信箱原則</p></td>
</tr>
<tr class="even">
<td><p>可以套用到信箱使用者的原則數目上限</p></td>
<td><p>1</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p>由受管理的資料夾助理員處理</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>用戶端支援</p></td>
<td><p>Microsoft Outlook 2010 和 OfficeOutlook Web App</p></td>
<td><p>Outlook 2010、Office Outlook 2007 和 Outlook Web App</p></td>
</tr>
</tbody>
</table>


## 開始之前有哪些須知？

  - 預估完成時間：20 分鐘。

  - 本主題中的程序需要特定權限。請查看每個程序以取得權限資訊。

  - 您無法使用 Exchange 系統管理中心 (EAC) 以根據保留原則建立保留標記。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

## 從受管理的資料夾遷移信箱使用者

以下是將使用者從此受管理的資料夾信箱原則遷移到保留原則的一般步驟。本主題稍後會詳述每一個步驟：

1.  蒐集套用至所有Exchange 2010和Exchange 2007信箱、 受管理的資料夾中的每個原則及受管理的每個受管理的資料夾的內容設定的受管理的資料夾信箱原則的相關資訊。您可以在Exchange 2010或Exchange 2007伺服器上使用 EMC 或命令介面，取得此資訊。

2.  建立遷移的保留標記。

3.  建立保留原則，並將最近建立的保留標記連結到該原則。

4.  移除受管理的資料夾信箱原則，然後將保留原則套用至使用者信箱。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>在您套用保留原則至使用者且受管理的資料夾助理員執行之後，使用者信箱中的受管理的資料夾會成為不受管理的資料夾。</td>
    </tr>
    </tbody>
    </table>


對於以下程序，Contoso 信箱所套用的受管理資料夾信箱原則包含下列受管理的資料夾。

### Contoso 的受管理資料夾

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>受管理的資料夾</th>
<th>受管理的內容設定</th>
<th>已啟用保留</th>
<th>保留時間</th>
<th>保留動作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Corp-DeletedItems</p></td>
<td><p>CS-Corp-DeletedItems</p></td>
<td><p>是</p></td>
<td><p>30 天</p></td>
<td><p>刪除並允許復原</p></td>
</tr>
<tr class="even">
<td><p>Corp-SentItems</p></td>
<td><p>CS-Corp-SentItems</p></td>
<td><p>是</p></td>
<td><p>1,825 天</p></td>
<td><p>移至刪除的郵件</p></td>
</tr>
<tr class="odd">
<td><p>Corp-JunkMail</p></td>
<td><p>CS-Corp-JunkMail</p></td>
<td><p>是</p></td>
<td><p>30 天</p></td>
<td><p>永久刪除</p></td>
</tr>
<tr class="even">
<td><p>Corp-EntireMailbox</p></td>
<td><p>CS-Corp-EntireMailbox</p></td>
<td><p>是</p></td>
<td><p>365 天</p></td>
<td><p>移至刪除的郵件</p></td>
</tr>
<tr class="odd">
<td><p>30 天</p></td>
<td><p>CS-30Days</p></td>
<td><p>是</p></td>
<td><p>30 天</p></td>
<td><p>移至刪除的郵件</p></td>
</tr>
<tr class="even">
<td><p>5 年</p></td>
<td><p>CS-5Years</p></td>
<td><p>是</p></td>
<td><p>1,825 天</p></td>
<td><p>移至刪除的郵件</p></td>
</tr>
<tr class="odd">
<td><p>永遠不過期</p></td>
<td><p>CS-NeverExpire</p></td>
<td><p>否</p></td>
<td><p>365 天</p></td>
<td><p>不適用</p></td>
</tr>
</tbody>
</table>


## 該怎麼做？

## 步驟 1：建立遷移的保留標記

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「郵件記錄管理」項目。

您可以在這個步驟中使用兩種方法：

  - **根據受管理的資料夾及其對應的受管理內容設定來建立保留標記：**使用此方法時，您在 **New-RetentionPolicyTag** 指令程式中需要指定 *ManagedFolderToUpgrade* 參數。當您指定此參數時，對應的保留標記就會自動套用到受管理的資料夾。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您要移植的受管理資料夾具有多個受管理內容設定可用於不同的郵件類別，則只會建立一個保留標記；而無論受管理內容設定的郵件類別為何，都會將所有受管理內容設定的最長保留時間用作所移植標記的保留時間。<br />
    例如，檢閱受管理資料夾 Corp-DeletedItems 的下列受管理內容設定。</td>
    </tr>
    </tbody>
    </table>


  - **手動指定保留設定來建立保留標記：**使用此方法時，您在 **New-RetentionPolicyTag** 指令程式中不需要指定 *ManagedFolderToUpgrade* 參數。當您未指定此參數時，就會對預設資料夾套用新增到原則的任何保留原則標記，並對整個信箱套用預設原則標記。不過，新增到原則的任何個人標記不會自動套用到受管理的資料夾。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您是使用Exchange 2013和Exchange 2010伺服器的混合環境中，您可以使用<strong>的連接埠受管理的資料夾</strong>精靈在 Exchange 管理主控台 (EMC) 輕鬆地連接埠受管理的資料夾Exchange 2010伺服器上與對應受管理的內容設定可保留標記。</td>
</tr>
</tbody>
</table>


**根據受管理的資料夾建立保留標記**

此範例會根據 Contoso 受管理的資料夾信箱原則中顯示的對應受管理內容設定，來建立保留標記。

    New-RetentionPolicyTag Corp-DeletedItems -ManagedFolderToUpgrade Corp-DeletedItems
    New-RetentionPolicyTag Corp-SentItems -ManagedFolderToUpgrade Corp-SentItems
    New-RetentionPolicyTag Corp-JunkMail -ManagedFolderToUpgrade Corp-JunkMail
    New-RetentionPolicyTag Corp-EntireMailbox -ManagedFolderToUpgrade Corp-EntireMailbox
    New-RetentionPolicyTag 30Days -ManagedFolderToUpgrade 30Days
    New-RetentionPolicyTag 5Years -ManagedFolderToUpgrade 5Years
    New-RetentionPolicyTag NeverExpire -ManagedFolderToUpgrade NeverExpire

如需詳細的語法及參數資訊，請參閱 [New-RetentionPolicyTag](https://technet.microsoft.com/zh-tw/library/dd335226\(v=exchg.150\))。

**手動建立保留標記**

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您也可以使用 EAC 手動建立保留標記 (而不是根據受管理資料夾中的設定)。如需詳細資訊，請參閱<a href="create-a-retention-policy-exchange-2013-help.md">建立保留原則</a>。</td>
</tr>
</tbody>
</table>


此範例會根據 Contoso 受管理的資料夾信箱原則中顯示的受管理資料夾和對應的受管理內容設定，來建立保留標記。保留設定是以手動方式指定，而未使用 *ManagedFolderToUpgrade* 參數。

    New-RetentionPolicyTag Corp-DeletedItems -Type DeletedItems -RetentionEnabled $true -AgeLimitForRetention 30 -RetentionAction DeleteAndAllowRecovery
    New-RetentionPolicyTag Corp-SentItems -Type SentItems -RetentionEnabled $true -AgeLimitforRetention 1825 -RetentionAction MoveToDeletedItems
    New-RetentionPolicyTag Corp-JunkMail -Type JunkMail -RetentionEnabled $true -AgeLimitforRetention 30 -RetentionAction PermanentlyDelete
    New-RetentionPolicyTag Corp-EntireMailbox -Type All -RetentionEnabled $true -AgeLimitForRetention 365 -RetentionAction MoveToDeletedItems
    New-RetentionPolicyTag 30Days -Type Personal -RetentionEnabled $true -AgeLimitForRetention 30 -RetentionAction MoveToDeletedItems
    New-RetentionPolicyTag 5Years -Type Personal -RetentionEnabled $true -AgeLimitForRetention 1825 -RetentionAction MoveToDeletedItems
    New-RetentionPolicyTag NeverExpire -Type Personal -RetentionEnabled $false

如需詳細的語法及參數資訊，請參閱 [New-RetentionPolicyTag](https://technet.microsoft.com/zh-tw/library/dd335226\(v=exchg.150\))。

## 步驟 2：建立保留原則

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「郵件記錄管理」項目。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您也可以使用 EAC 建立保留原則，並將保留標記新增至原則。如需詳細資訊，請參閱<a href="create-a-retention-policy-exchange-2013-help.md">建立保留原則</a>。</td>
</tr>
</tbody>
</table>


此範例會建立保留原則 RP-Corp，並將最近建立的保留標記連結到該原則。

    New-RetentionPolicy RP-Corp -RetentionPolicyTagLinks Corp-DeletedItems,Corp-SentItems,Corp-JunkMail,Corp-EntireMailbox,30Days,NeverExpire

如需詳細的語法及參數資訊，請參閱 [New-RetentionPolicy](https://technet.microsoft.com/zh-tw/library/dd297970\(v=exchg.150\))。

## 步驟 3：從使用者信箱移除受管理的資料夾信箱原則

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「套用保留原則」項目。

此範例會從 Ken Kwok 的信箱中移除受管理的資料夾信箱原則和任何受管理的資料夾。含有任何郵件的受管理資料夾不會移除。

    Set-Mailbox -Identity Kwok -RemoveManagedFolderAndPolicy RP-Corp

## 步驟 4：將保留原則套用至使用者信箱

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「套用保留原則」項目。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您也可以使用 EAC 將保留原則套用至使用者。如需詳細資訊，請參閱<a href="apply-a-retention-policy-to-mailboxes-exchange-2013-help.md">將保留原則套用至信箱</a>。</td>
</tr>
</tbody>
</table>


此範例會將最近建立的保留原則 RP-Corp 套用到信箱使用者 Ken Kwok。

    Set-Mailbox -Identity Kwok -RetentionPolicy RP-Corp

如需詳細的語法及參數資訊，請參閱 [Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\))。

## 如何才能了解此工作是否正常運作？

若要驗證您是否已從受管理的資料夾遷移至保留原則，請執行下列動作：

  - 產生所有使用者信箱的報告，並對它們套用保留原則。
    
    此命令會擷取已套用至組織中所有信箱的保留原則，以及信箱的保留狀態。
    
        Get-Mailbox -ResultSize unlimited -Filter {Name -NotLike "DiscoverySearch*�?} | Format-Table Name,RetentionPolicy,RetentionHoldEnabled -Auto

  - 在受管理的資料夾助理員以保留原則處理信箱後，使用 [Get-RetentionPolicyTag](https://technet.microsoft.com/zh-tw/library/dd298009\(v=exchg.150\)) 指令程式來擷取使用者信箱中佈建的保留標記。
    
    此命令會擷取實際套用至 April Stewart 信箱的保留標記。
    
        Get-RetentionPolicyTag -Mailbox astewart

