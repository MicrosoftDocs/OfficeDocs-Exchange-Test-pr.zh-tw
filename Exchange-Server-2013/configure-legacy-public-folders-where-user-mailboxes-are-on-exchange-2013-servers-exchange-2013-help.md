---
title: '使用者信箱位於 Exchange 2013 伺服器上時設定舊版公用資料夾: Exchange 2013 Help'
TOCTitle: 使用者信箱位於 Exchange 2013 伺服器上時設定舊版公用資料夾
ms:assetid: 1d5ca19e-696e-4054-a634-15dd34d952b7
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn690134(v=EXCHG.150)
ms:contentKeyID: 62281105
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用者信箱位於 Exchange 2013 伺服器上時設定舊版公用資料夾

 

_**適用版本：**Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2017-03-27_

如何讓 Exchange 2013 或 Exchange 2016 使用者存取 Exchange 2010 或更舊版本公用資料夾 （也稱為舊版公用資料夾）。

## 開始之前有哪些須知？

信箱位於 Exchange Server 2013 或 Exchange Server 2016 的使用者將無法存取舊版公用資料夾從 Outlook Web App、 在 web 上的 Outlook 或 Outlook for mac。本文中的步驟適用於 Exchange 2013 和 Exchange 2016。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Outlook 2016 for Mac 使用者可以存取舊版公用資料夾後您依照本文中的步驟。如果您組織中的用戶端使用 Outlook 2016 for Mac，請務必先安裝年 4 月 2016年更新。否則，這些使用者將無法存取並行或混合式拓撲中的公用資料夾。如需詳細資訊，請參閱<a href="accessing-public-folders-with-outlook-2016-for-mac-exchange-2013-help.md">存取公用資料夾與 Outlook 2016 for Mac</a>。</td>
</tr>
</tbody>
</table>


## 步驟 1：將 Exchange 2010 公用資料夾設為可探索

1.  如果您的公用資料夾在 Exchange 2010 或更新版本的伺服器上，您必須具備公用資料夾資料庫的所有信箱伺服器上安裝 Client Access Server role。這可讓 Microsoft Exchange RpcClientAccess 服務來執行，允許所有用戶端存取公用資料夾。用戶端存取角色不需要 Exchange 2007 公用資料夾伺服器，並不需要此步驟。如需詳細資訊，請參閱[安裝 Exchange Server 2010](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>此伺服器沒有為一部分的用戶端存取負載平衡。如需詳細資訊，請參閱<a href="https://technet.microsoft.com/en-us/library/ff625247(v=exchg.141).aspx">在 Exchange 2010 了解負載平衡</a>。</td>
    </tr>
    </tbody>
    </table>


2.  在每個公用資料夾伺服器上建立空的信箱資料庫。
    
    在 Exchange 2010 中執行下列命令。此命令會將信箱資料庫排除在信箱佈建負載平衡器以外。這樣可以防止自動將新的信箱新增至此資料庫中。
    
        New-MailboxDatabase -Server <PFServerName_with_CASRole> -Name <NewMDBforPFs> -IsExcludedFromProvisioning $true 
    
    在 Exchange 2007 中執行下列命令：
    
        New-MailboxDatabase -StorageGroup "<PFServerName>\StorageGroup>" -Name <NewMDBforPFs>
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>我們建議您增加到此資料庫的唯一信箱就是您將在步驟 3 中建立的 Proxy 信箱。不得在此信箱資料庫上建立其他信箱。</td>
    </tr>
    </tbody>
    </table>


3.  在新的信箱資料庫中建立 Proxy 信箱，然後在通訊錄中隱藏該信箱。「自動探索」會傳回此信箱的 SMTP 作為 *DefaultPublicFolderMailbox* SMTP，因此只要解析此 SMTP，用戶端即可連到舊版 Exchange 伺服器來存取公用資料夾。
    
        New-Mailbox -Name <PFMailbox1> -Database <NewMDBforPFs> 
    
        Set-Mailbox -Identity <PFMailbox1> -HiddenFromAddressListsEnabled $true

4.  在 Exchange 2010 中，讓「自動探索」傳回 Proxy 公用資料夾信箱。對於 Exchange 2007，無須執行此步驟。
    
        Set-MailboxDatabase <NewMDBforPFs> -RPCClientAccessServer <PFServerName_with_CASRole>

5.  對組織中的每部公用資料夾伺服器重複前述步驟。

## 步驟 2：設定使用者信箱來存取舊版公用資料夾

此程序的最後一個步驟是設定使用者信箱來允許存取舊版內部部署公用資料夾。

讓 Exchange Server 2013 內部部署使用者能夠存取舊版公用資料夾。您將會指向先前在[Step 2: Make remote public folders discoverable](configure-legacy-on-premises-public-folders-for-a-hybrid-deployment-exchange-2013-help.md)中建立的所有 Proxy 公用資料夾信箱。從套用 CU5 或更新版本更新的 Exchange 2013 伺服器執行下列命令。

    Set-OrganizationConfig -PublicFoldersEnabled Remote -RemotePublicFolderMailboxes ProxyMailbox1,ProxyMailbox2,ProxyMailbox3

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您必須等到 ActiveDirectory 同步處理完成後，才會看見變更。此程序可能會花幾小時的時間。</td>
</tr>
</tbody>
</table>


## 如何知道這是否正常運作？

選擇信箱位於 Exchange Server 2013 CU5 或更新版本伺服器的使用者，登入此使用者的 Outlook，然後執行下列公用資料夾測試：

1.  確定 Outlook 用戶端已執行。

2.  按住 CTRL 鍵，然後以滑鼠右鍵按一下 Windows 工作列右邊通知區域中的 Outlook 圖示。

3.  選取 **\[測試電子郵件自動設定…\]**

4.  請確定「測試電子郵件自動設定」工具的 XML 索引標籤中傳回下列資訊：
    
      - \<PublicFolderInformation\>
    
      - \<SmtpAddress\>\<公用資料夾信箱的 SMTP 位址\</SmtpAddress\>
    
      - \</PublicFolderInformation\>

5.  在 Outlook 用戶端，執行下列工作：
    
      - 檢視公用資料夾階層。
    
      - 檢查權限。
    
      - 建立與刪除公用資料夾。
    
      - 張貼內容至公用資料夾以及刪除公用資料夾的內容。

