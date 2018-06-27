---
title: '重新建立探索系統信箱: Exchange 2013 Help'
TOCTitle: 重新建立探索系統信箱
ms:assetid: 5ae8426b-5661-4ecb-99c4-cdd342107fb1
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg588318(v=EXCHG.150)
ms:contentKeyID: 50473262
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 重新建立探索系統信箱

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2018-01-17_

就地 eDiscovery 使用系統信箱來儲存在就地 eDiscovery 搜尋的中繼資料。此探索系統信箱有顯示名稱為**SystemMailbox {e0dc1c29-89c3-4034-b678-e6c29d823ed9}**。因為系統信箱隱藏在 Exchange 系統管理中心 (EAC) 或Exchange地址清單中，他們會很少刪除不經意。

不過，如果意外刪除探索系統信箱探索管理員將無法執行就地 eDiscovery 搜尋或管理現有的搜尋。在此例中，若要啟用 eDiscovery 功能，您必須重新建立探索系統信箱。

## 您應知道您開始之前

  - 預估完成時間：10 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「收件者佈建權限」一節。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

## 使用命令介面來重新建立探索系統信箱

1.  如果存在，刪除Active Directory、 SystemMailbox {e0dc1c29-89c3-4034-b678-e6c29d823ed9} 的使用者帳戶。根據預設， Exchange Server 2013安裝程式會在Active Directory中的 \[使用者\] 容器中建立信箱。如需如何從Active Directory刪除的使用者帳戶的詳細資訊，請參閱[刪除的使用者帳戶](https://go.microsoft.com/fwlink/p/?linkid=215850)。

2.  使用命令介面啟用探索系統信箱。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您無法使用 EAC 啟用探索系統信箱。<br />
    必須是執行了以下命令從相同的目錄解壓縮 Exchange 安裝媒體中的位置。</td>
    </tr>
    </tbody>
    </table>
    
    若要重新建立探索系統信箱，請執行下列命令：
    
        .\Setup /preparead /IAcceptExchangeServerLicenseTerms

## 如何知道這是否正常運作？

若要確認您已順利重新建立探索系統信箱，請使用具有*Arbitration*參數**Get-Mailbox**指令程式來擷取系統信箱。檢視以確認已重新建立系統信箱`SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}`命令的結果。

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

