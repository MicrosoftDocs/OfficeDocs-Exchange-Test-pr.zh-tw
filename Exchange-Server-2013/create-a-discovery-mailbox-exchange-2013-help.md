---
title: '建立探索信箱: Exchange Online Help'
TOCTitle: 建立探索信箱
ms:assetid: bc20285d-35e2-4e49-9bd3-38abf96114ba
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd638177(v=EXCHG.150)
ms:contentKeyID: 50474120
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 建立探索信箱

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

Microsoft Exchange Server 2013安裝程式會建立預設探索信箱。探索信箱中Exchange Online，也會建立預設。探索信箱可用為目標信箱[就地 eDiscovery](in-place-ediscovery-exchange-2013-help.md)搜尋Exchange 系統管理中心 (EAC) 中。您可以建立所需的其他探索信箱。建立新的探索信箱後，您必須將完整存取權限指派給適當的使用者，讓他們可以存取 eDiscovery 搜尋結果時，複製到探索信箱。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>探索管理員將 eDiscovery 搜尋的結果複製到探索信箱之後，信箱可能就會包含敏感資訊。您應該控制對探索信箱的存取權，並確定只有授權的使用者才能存取這些信箱。</td>
</tr>
</tbody>
</table>


如需詳細資訊，請參閱 [Discovery mailboxes](in-place-ediscovery-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：3 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「建立探索信箱」項目。

  - 探索信箱擁有 50 GB 的信箱儲存配額。無法增加此儲存配額。

  - 您不能使用 EAC 來建立探索信箱或將存取權限指派。您必須使用命令介面。在Office 365、 使用遠端 PowerShell 連線至Exchange Online組織。

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

## （選用）步驟 1： 連線至 Exchange Online 使用遠端 PowerShell

您只需要執行這個步驟中若有Exchange Online或Office 365組織。 如果您必須前往下一個步驟並執行Exchange 管理命令介面命令Exchange Server 2013組織。

1.  在您的本機電腦上開啟 Windows PowerShell 並執行下列命令。
    
        $UserCredential = Get-Credential
    
    在 **\[Windows PowerShell 認證要求\]** 對話方塊中，輸入 Office 365 全域管理員帳戶的使用者名稱和密碼，然後按一下 **\[確定\]**。

2.  執行下列命令。
    
        $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $UserCredential -Authentication Basic -AllowRedirection

3.  執行下列命令。
    
        Import-PSSession $Session

4.  若要確認您要連線至Exchange Online組織，請執行下列命令以取得組織中的所有信箱的清單。
    
        Get-Mailbox

如需詳細資訊或如果您有連線至Exchange Online組織的問題，請參閱 ＜ [Connect to Exchange Online 使用遠端 PowerShell](https://go.microsoft.com/fwlink/p/?linkid=517283)。

## 步驟 2： 建立探索信箱

此範例會建立名為 SearchResults 的探索信箱。

    New-Mailbox -Name SearchResults -Discovery 

如需詳細的語法及參數資訊，請參閱 [New-Mailbox](https://technet.microsoft.com/zh-tw/library/aa997663\(v=exchg.150\))。

若要顯示 Exchange 組織中的所有探索信箱清單，請執行下列命令：

    Get-Mailbox -Resultsize unlimited -Filter {RecipientTypeDetails -eq "DiscoveryMailbox"}

如需詳細的語法及參數資訊，請參閱 [Get-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123685\(v=exchg.150\))。

## 步驟 3： 指派權限給探索信箱

您必須明確指派給使用者或群組的必要權限來開啟您建立探索信箱。使用下列語法來指派給使用者或群組的權限將開啟探索信箱和檢視搜尋結果：

    Add-MailboxPermission <Name of the discovery mailbox> -User <Name of user or group> -AccessRights FullAccess -InheritanceType all

例如，下列命令會將完整存取權指派給 Litigation Managers 群組，讓群組成員可以開啟 Fabrikam Litigation 探索信箱。

    Add-MailboxPermission "Fabrikam Litigation" -User "Litigation Managers" -AccessRights FullAccess -InheritanceType all

如需詳細的語法及參數資訊，請參閱 [Add-MailboxPermission](https://technet.microsoft.com/zh-tw/library/bb124097\(v=exchg.150\))。

## 其他資訊

  - 根據預設，\[探索管理\] 角色群組的成員只有預設 \[探索搜尋信箱\] 的完整存取權。如果您想要讓成員開啟所建立的探索信箱，則必須對 \[探索管理\] 角色群組明確指派完整存取權。

  - 雖然使用者會出現在 Exchange 通訊清單中，但是無法將電子郵件傳送至探索信箱。使用傳遞限制可禁止將電子郵件傳遞至探索信箱。這可保留複製到探索信箱的搜尋結果的完整性。

  - 探索信箱無法用於其他目的或轉換成另一種類型的信箱。

  - 您可以移除探索信箱，如同移除任何其他類型的信箱一般。

