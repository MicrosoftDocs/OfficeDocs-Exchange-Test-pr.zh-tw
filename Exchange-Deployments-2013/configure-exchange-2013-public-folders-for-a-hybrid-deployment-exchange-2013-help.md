---
title: '設定混合式部署的 Exchange 2013 公用資料夾: Exchange Online Help'
TOCTitle: 設定混合式部署的 Exchange 2013 公用資料夾
ms:assetid: b828520f-022c-4fcb-ab68-e1c330e87c33
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn986544(v=EXCHG.150)
ms:contentKeyID: 65296579
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定混合式部署的 Exchange 2013 公用資料夾

 

_<strong>適用版本：</strong>Exchange Server 2013, Exchange Server 2016_

_<strong>上次修改主題的時間：</strong>2016-12-09_

**摘要：** 啟用 Exchange Online 使用者存取內部部署 Exchange 2013 環境中的公用資料夾的指示。

在混合式部署中，您的使用者可以在 Exchange Online、 內部，或兩者，且您的公用資料夾其在 Exchange 線上\] 或 \[內部部署。有時 online 使用者可能會需要用來存取 Exchange Server 2013 內部部署環境中的公用資料夾。同樣地，Exchange 2013 使用者可能需要存取 Office 365 或 Exchange Online 中的公用資料夾。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ150559.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您有 Exchange 2010 或 Exchange 2007 公用資料夾，請參閱<a href="configure-legacy-on-premises-public-folders-for-a-hybrid-deployment-exchange-2013-help.md">為混合部署設定舊版的內部部署公用資料夾</a>。</td>
</tr>
</tbody>
</table>


本文說明如何啟用 Exchange Online/Office 365 使用者存取 Exchange 2013 公用資料夾。若要啟用內部部署 Exchange 2013 使用者可以存取公用資料夾在 Exchange Online，請參閱[設定 Exchange Online 公用資料夾以進行混合部署](configure-exchange-online-public-folders-for-a-hybrid-deployment-exchange-2013-help.md)。

Exchange Online/Office 365 使用者必須是物件所代表 MailUser Exchange 內部部署環境中才可存取 Exchange 2013 公用資料夾。此 MailUser 物件也必須是本機 Exchange 2013 公用資料夾階層的目標。如果您有 Office 365 使用者目前不在內部物件所表示之 MailUser、 參照 Microsoft 知識庫文章 3106618 ["Exchange Online 使用者無法存取舊版內部部署公用資料夾 」](https://go.microsoft.com/fwlink/p/?linkid=699451)建立比對內部實體。

## 開始之前有哪些須知？

1.  這些指示假設您已使用混合組態精靈來設定及同步處理您的內部部署與 Exchange Online 環境，且使用者的「自動探索」所使用的 DNS 記錄是參考內部部署端點。如需詳細資訊，請參閱 [混合組態精靈](hybrid-configuration-wizard-exchange-2013-help.md)。

2.  這些指示假設 Outlook 無所不在 」 是已啟用且在內部部署 Exchange 伺服器功能。如需如何啟用 Outlook 無所不在 」 的資訊，請參閱[Outlook 無所不在](https://technet.microsoft.com/zh-tw/library/bb123741\(v=exchg.150\))。

3.  實作 Exchange 與 Office 365 的混合式部署的公用資料夾共存可能需要修正匯入程序期間發生衝突。因為指派給郵件已啟用的公用資料夾與其他使用者和群組的 Office 365 及其他屬性發生衝突的非路由傳送的電子郵件地址就會發生衝突。

4.  若要能夠跨部署來存取公用資料夾，使用者必須將其 Outlook 用戶端升級至 2012 年 11 月或更新的 Outlook 公用更新。
    
    1.  若要下載 November 2012 Outlook 更新 Outlook 2010，請參閱[Microsoft Outlook 2010 (KB2687623) 32 位元版本的更新](https://www.microsoft.com/en-us/download/details.aspx?id=35702)。
    
    2.  若要下載 November 2012 Outlook 更新 Outlook 2007，請參閱[Microsoft Office Outlook 2007 (KB2687404) 的更新](https://www.microsoft.com/en-us/download/details.aspx?id=35718)。

5.  Outlook 2011 for Mac 與 Outlook for Mac 中的 Office 365 不支援跨部署的公用資料夾。使用者必須位於相同的位置存取其有 Outlook 2011 for Mac 或 Outlook for Mac for Office 365 的公用資料夾。此外，信箱已在 Exchange Online 使用者將無法存取使用Outlook Web App的內部部署公用資料夾。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ150559.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Outlook 2016 for Mac 支援跨部署公用資料夾。如果您組織中的用戶端使用 Outlook 2016 for Mac，請務必先安裝年 4 月 2016年更新。否則，這些使用者將無法存取之混合式拓撲的公用資料夾。如需詳細資訊，請參閱<a href="https://technet.microsoft.com/zh-tw/library/mt788631(v=exchg.150)">存取公用資料夾與 Outlook 2016 for Mac</a>。</td>
    </tr>
    </tbody>
    </table>


## 步驟 1： 下載指令碼

1.  從[擁有郵件功能的公用資料夾-目錄同步處理指令碼](https://www.microsoft.com/en-us/download/details.aspx?id=46381)下載下列檔案：
    
      - `Sync-MailPublicFolders.ps1`
    
      - `SyncMailPublicFolders.strings.psd1`

2.  將檔案儲存至將要執行 PowerShell 的本機電腦。例如，C:\\PFScripts。

## 步驟 2： 設定目錄同步處理

目錄同步處理服務不會同步處理具有郵件功能的公用資料夾。執行下列指令碼將擁有郵件功能的公用資料夾部署之間同步處理內部部署和Office 365。 指派給擁有郵件功能的公用資料夾的特殊權限必須在重新建立雲端自混合部署案例中不支援跨內部部署權限。詳細資訊，請參閱[Exchange Server 2013 混合式部署](exchange-server-hybrid-deployments-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ150559.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>同步處理具有郵件功能的公用資料夾會出現郵件連絡人物件的郵件流程目的並不會在 EExchange 系統管理中心中檢視。 請參閱 ＜ Get MailPublicFolder 命令。 若要重新建立雲端中的 SendAs 權限、 使用 Add Add-recipientpermission 指令。</td>
</tr>
</tbody>
</table>


1.  在 Exchange 2013 伺服器上，執行下列命令來同步處理具有郵件功能的公用資料夾從本機在內部部署 Active Directory 至 O365。
    
        Sync-MailPublicFolders.ps1 -Credential (Get-Credential) -CsvSummaryFile:sync_summary.csv
    
    其中`Credential`是 Office 365 使用者名稱及 \[密碼\] 和 \[ `CsvSummaryFile`是您想要記錄同步作業與.csv 格式中的錯誤的路徑。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ150559.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在執行指令碼、 之前建議您首先模擬指令碼會採取的動作環境中如前文所述<code>-WhatIf</code>參數執行它。<br />
也建議您執行此指令碼每天同步處理具有郵件功能的公用資料夾。</td>
</tr>
</tbody>
</table>


## 步驟 3： 設定 Exchange Online 使用者存取 Exchange 2013 內部部署公用資料夾

此程序的最後一個步驟是設定 Exchange online 組織並允許存取 Exchange 2013 公用資料夾。

啟用 exchange online 組織來存取內部部署公用資料夾。您將會指向所有您內部部署公用資料夾信箱。

    Set-OrganizationConfig -PublicFoldersEnabled Remote -RemotePublicFolderMailboxes PFMailbox1,PFMailbox2,PFMailbox3

<table>
<thead>
<tr class="header">
<th><img src="images/JJ150559.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您必須等到 ActiveDirectory 同步處理已完成查看所做的變更。此程序可能需要最多 3 小時才能完成。如果您不想要等候的每一個三個小時就會發生週期性同步，您就可以強制任何時候的目錄同步作業。不要強制目錄同步作業詳細步驟，請參閱<a href="http://technet.microsoft.com/en-us/library/jj151771.aspx">強制目錄同步</a>。</td>
</tr>
</tbody>
</table>


## 如何知道這是否正常運作？

1.  代表存在於 Exchange Online 的使用者登入 Outlook，並執行下列公用資料夾測試：
    
      - 檢視階層。
    
      - 檢查權限
    
      - 建立與刪除公用資料夾。
    
      - 張貼內容至公用資料夾以及刪除公用資料夾的內容。

