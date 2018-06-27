---
title: '自動信箱發佈: Exchange 2013 Help'
TOCTitle: 自動信箱發佈
ms:assetid: f4db4636-948c-466b-839c-300c1a3a9544
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ff477621(v=EXCHG.150)
ms:contentKeyID: 59637264
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 自動信箱發佈

 

_**適用版本：**Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013_

_**上次修改主題的時間：**2013-08-13_

當您建立或移動信箱，或郵件啟用現有使用者時，該信箱必須存放在信箱資料庫中。在 Microsoft Exchange Server 2013 中，您可以選擇讓 Exchange 使用自動信箱發佈來為您選擇資料庫。

使用自動信箱發佈時，Exchange 會查看組織中的信箱資料庫、使用本主題稍後討論的準則來排除不適合的資料庫，然後隨機選擇信箱所在的資料庫。這個處理程序會在組織中所有合適的信箱資料庫中，隨機發佈信箱。

當您在 **New-Mailbox** 和 **Enable-Mailbox** 指令程式上未指定 *Database* 參數，或者未在 **New-MoveRequest** 指令程式上指定 *TargetDatabase* 參數時，會使用自動發佈。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>只有當信箱是在 Exchange 2013 伺服器上建立、移到 Exchange 2013 伺服器或者使用者已啟用郵件時，才會執行自動信箱發佈。<strong>New-Mailbox</strong>、<strong>New-MoveRequest</strong> 及 <strong>Enable-Mailbox</strong> Cmdlet 必須是從執行 Exchange 2013 的伺服器上執行。Exchange 不會自動根據伺服器負載，重新發佈信箱以將負載分散給各資料庫。</td>
</tr>
</tbody>
</table>


可以使用下列處理程序來尋找其中具有新增或所移動信箱的合適信箱資料庫：

1.  Exchange 會擷取 Exchange 2013 組織中所有信箱資料庫的清單。

2.  會從可用的資料庫清單中，移除標示為要從發佈處理程序中排除的任何信箱資料庫。您可以控制要排除哪些資料庫。如需詳細資訊，請參閱本主題稍後的Exclude Databases from Automatic Distribution。

3.  在資料庫管理範圍外部而且適用於執行作業之系統管理員的任何信箱資料庫，會從可用的資料庫清單中移除。如需詳細資訊，請參閱本主題稍後的Database Scopes。

4.  在本機 Active Directory 站台外部 (執行作業的位置) 的任何信箱資料庫，會從可用的資料庫清單中移除。

5.  Exchange 會從信箱資料庫的剩餘清單中隨機選擇資料庫。如果資料庫處於連線及健全狀態，則會由 Exchange 使用。如果是離線或不健全狀態，則會隨機選擇其他資料庫。如果找不到連線或健全的資料庫，作業則會失敗並發生錯誤。

選取信箱資料庫的處理程式會由「信箱資源管理代理程式」指令程式擴充代理程式來執行。`Mailbox Resources Management Agent`是數個指令程式擴充代理程式的其中一個，可擴充執行中指令程式的功能。如需指令程式延伸代理程式的詳細資訊，請參閱[Cmdlet 延伸代理程式](cmdlet-extension-agents-exchange-2013-help.md)。

如果不要自動發佈信箱，則可停用`Mailbox Resources Management Agent`。當您停用代理程式時，所做變更會套用到整個 Exchange 組織。如需如何停用指令程式擴充代理程式的詳細資訊，請參閱[管理指令程式延伸代理程式](manage-cmdlet-extension-agents-exchange-2013-help.md)。

## 從自動發佈中排除資料庫

根據預設，自動信箱發佈可以選擇本機 Exchange 2013 站台之 Active Directory 伺服器上的所有連線及健全的信箱資料庫，以存放新的或移動的信箱。不過，您可能會基於各種原因，而從發佈處理程序中排除某些資料庫。例如，您可能將信箱資料庫指定為日誌資料庫，其中應該只有手動指定的信箱。或者，可能要從輪替中暫時移除資料庫，以執行排定的維護。Exchange 2013 會提供一些選項，讓您使用 *IsExcludedFromProvisioning* 參數 (可透過 **Set-MailboxDatabase** Cmdlet 加以設定) 從排除處理程序中永久或暫時排除資料庫。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在 <strong>Set-MailboxDatabase</strong> Cmdlet 中還有另外兩個參數 (<em>IsSuspendedFromProvisioning</em> 和 <em>IsExcludedFromInitialProvisioning</em> ) 可用。後續的 Exchange 版本會移除這些參數，因此不支援使用這些參數。</td>
</tr>
</tbody>
</table>


*IsExcludedFromProvisioning* 參數有兩個有效值：`$True` 和 `$False`。當您將此內容設定為 `$True` 時，此信箱資料庫便會排除在自動發佈處理程序之外。當您將此內容設定為 `$False` 時，此信箱資料庫便會納入到自動發佈處理程序中。預設值為 `$False`。

若要將信箱資料庫排除在自動發佈之外，請使用下列命令：

    Set-MailboxDatabase <database name> -IsExcludedFromProvisioning $True

從自動發佈中排除信箱資料庫時，在資料庫中建立信箱或將信箱移到資料庫的唯一方法，便是在 **New-Mailbox** 和 **Enable-Mailbox** 指令程式上使用 *Database* 參數，或在 **New-MoveRequest** 指令程式上使用 *TargetDatabase* 參數。

## 資料庫範圍

資料庫管理範圍是對在 Exchange 2013 中提供的自動信箱發佈處理程序以外，多加的一層控制。如果信箱資料庫處於連線且健全狀態，則表示它位於本機 Active Directory 站台中，而且未從自動發佈處理程序中排除。Exchange 2013 會檢查信箱資料庫是否包含在對執行 Cmdlet 的系統管理員套用的資料庫範圍中。如果包含在資料庫範圍中，則表示包含在該系統管理員可使用的資料庫清單中。

資料庫範圍是「角色存取控制」(RBAC) 權限模型的一部分。如需 RBAC 和資料庫範圍的詳細資訊，請參閱下列主題：

  - [了解角色型存取控制](understanding-role-based-access-control-exchange-2013-help.md)

  - [了解管理角色範圍](understanding-management-role-scopes-exchange-2013-help.md)

如果在本機 Active Directory 站台中具有許多可用於自動發佈的信箱資料庫，但您想要限制特定一組系統管理員可使用的資料庫，則資料庫範圍十分有用。例如，您的 Exchange 2013 伺服器可能服務數個代理程式，但您只想讓每個代理程式建立或移動信箱到自己被配置的信箱資料庫。

根據預設，Exchange 2013 組織中的所有系統管理員都可以看見組織中的所有信箱資料庫。若要限制可以看見的資料庫，進而限制系統管理員可能在其中建立信箱或移入信箱的資料庫，您必須執行下列動作：

1.  使用 **New-ManagementScope** 指令程式建立自訂資料庫管理範圍，這個範圍中僅包含您要系統管理員使用的信箱資料庫。

2.  以下列其中一種方式，讓新資料庫範圍與管理角色指派產生關聯：
    
      - 使用 **Set-ManagementRoleAssignment** 指令程式上的 *CustomConfigWriteScope* 參數，將新資料庫範圍新增到現有的管理角色指派。資料庫範圍現在會套用到管理角色群組、萬用安全性群組 (USG) 或指定角色指派的使用者。
    
      - 使用 **New-ManagementRoleAssignment** 指令程式建立管理角色指派，並使用 *CustomConfigWriteScope* 參數來指定新資料庫範圍。您可以在管理角色和角色群組、USG 或使用者之間建立角色指派。

3.  如果對角色群組或 USG 建立角色指派，請將使用者新增到角色群組或 USG，以便將角色指派和資料庫範圍套用至使用者。

4.  適用時，從所指派的資料庫範圍中包含您不想讓使用者存取之資料庫的任何其他角色或 USG 中，移除您對其指定新角色指派的使用者 (或屬於您在前面的步驟中所建立之角色群組或 USG 成員的使用者)。

5.  確認系統管理員只能存取應該具有存取權的資料庫。

完成這些步驟後，以您建立的資料庫範圍指定角色指派的系統管理員，只能在指定的資料庫中建立信箱或移入信箱。

如需如何使用資料庫範圍來限制系統管理員可使用信箱資料庫的詳細資訊，請參閱[使用資料庫範圍控制自動信箱發佈](control-automatic-mailbox-distribution-using-database-scopes-exchange-2013-help.md)。

