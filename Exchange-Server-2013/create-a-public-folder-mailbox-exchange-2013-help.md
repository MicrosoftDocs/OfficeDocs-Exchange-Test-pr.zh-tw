---
title: '建立公用資料夾信箱: Exchange Online Help'
TOCTitle: 建立公用資料夾信箱
ms:assetid: 64437ffd-231b-4c10-84df-232ccbe9538f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ552410(v=EXCHG.150)
ms:contentKeyID: 50473321
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 建立公用資料夾信箱

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2014-10-23_

建立公用資料夾之前，您必須先建立公用資料夾信箱。公用資料夾信箱包含公用資料夾的階層資訊及內容。您建立的第一個公用資料夾信箱是主要階層信箱，其中包含唯一可寫入的階層副本。您建立的其他任何公用資料夾信箱都是次要信箱，其中包含唯讀的階層副本。

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如需有關公用資料夾之儲存配額和限制的相關資訊，請參閱下列主題：
<ul>
<li><p>若為 Office 365 中的公用資料夾，請參閱 <a href="https://go.microsoft.com/fwlink/?linkid=391188">Exchange Online 限制</a>。</p></li>
<li><p>若為內部部署 Exchange Server 2013 中的公用資料夾，請參閱<a href="limits-for-public-folders-exchange-2013-help.md">公用資料夾的限制</a>。</p></li>
</ul></td>
</tr>
</tbody>
</table>


如需 Exchange 2013 中與公用資料夾相關的其他管理工作，請參閱[公用資料夾程序](public-folder-procedures-exchange-2013-help.md)。

如需 Exchange Online 中與公用資料夾相關的其他管理工作，請參閱 [Office 365 和 Exchange Online 中公用資料夾程序](https://technet.microsoft.com/zh-tw/library/jj966272\(v=exchg.150\))。

## 開始之前有哪些須知？

  - 預估完成時間：少於 5 分鐘。

  - Exchange 2013 公用資料夾與舊版 Exchange 伺服器上的公用資料夾不存在位於相同組織。如果您嘗試建立公用資料夾信箱仍有舊版公用資料夾時，將會收到錯誤**部署已偵測到現有的公用資料夾。若要移轉現有的公用資料夾資料，建立新的公用資料夾信箱使用-HoldForMigration 交換器。**
    
    您可以在 Exchange 2013 中建立公用資料夾之前，您必須將舊版公用資料夾移轉至 Exchange 2013。若要這樣做，請遵循[使用序列遷移公用資料夾從舊版移轉至 Exchange 2013](https://technet.microsoft.com/zh-tw/library/jj150486\(v=exchg.150\))中的步驟。下列步驟將為您示範如何建立可以用來儲存移轉公用資料夾的公用資料夾信箱。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [共用和協同作業的權限](sharing-and-collaboration-permissions-exchange-2013-help.md)主題中的「公用資料夾」項目。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

## 您要執行的工作

## 使用 EAC 建立公用資料夾信箱

1.  瀏覽至 \[公用資料夾\] \> \[公用資料夾信箱\]，然後按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

2.  在 \[公用資料夾信箱\] 中，提供公用資料夾信箱的名稱。

3.  按一下 \[儲存\]。

## 使用命令介面建立公用資料夾信箱

此範例會建立主要公用資料夾信箱。

    New-Mailbox -PublicFolder -Name MasterHierarchy

此範例會建立次要公用資料夾信箱。建立主要階層信箱和次要階層信箱的唯一差異在於，主要信箱是組織中建立的第一個信箱。您可以基於負載平衡目的來建立其他公用資料夾信箱。

    New-Mailbox -PublicFolder -Name Istanbul 

如需詳細的語法及參數資訊，請參閱 [New-Mailbox](https://technet.microsoft.com/zh-tw/library/aa997663\(v=exchg.150\))。

## 如何知道這是否正常運作？

若要確認您是否成功建立主要公用資料夾信箱，請執行下列命令介面命令：

    Get-OrganizationConfig | Format-List RootPublicFolderMailbox

如需詳細的語法及參數資訊，請參閱 [Get-OrganizationConfig](https://technet.microsoft.com/zh-tw/library/aa997571\(v=exchg.150\))。

有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

