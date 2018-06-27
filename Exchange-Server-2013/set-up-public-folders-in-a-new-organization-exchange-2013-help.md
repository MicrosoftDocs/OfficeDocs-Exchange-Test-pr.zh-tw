---
title: '設定新的組織中的公用資料夾: Exchange Online Help'
TOCTitle: 設定新的組織中的公用資料夾
ms:assetid: 7b419906-8977-47f0-8687-a87911b5ebec
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ651147(v=EXCHG.150)
ms:contentKeyID: 50473570
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定新的組織中的公用資料夾

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2015-11-09_

**摘要：** 如何設定包括在 EAC 中將權限指派給他們的公用資料夾。

本主題說明如何設定公用資料夾，以及在新組織或在先前沒有公用資料夾的組織中執行公用資料夾。

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


如需 Exchange Server 2013 中與公用資料夾相關的其他管理工作，請參閱[公用資料夾程序](public-folder-procedures-exchange-2013-help.md)。

如需 Exchange Online 中與公用資料夾相關的其他管理工作，請參閱[Office 365 和 Exchange Online 中公用資料夾程序](https://technet.microsoft.com/zh-tw/library/jj966272\(v=exchg.150\))。

## 開始之前有哪些須知？

  - 完成此工作的預估時間：30 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [共用和協同作業的權限](sharing-and-collaboration-permissions-exchange-2013-help.md)主題中的「公用資料夾」項目。

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


## 該怎麼做？

## 步驟 1：建立主要公用資料夾信箱

主要公用資料夾信箱包含公用資料夾階層及內容的可寫入複本，也是您為您組織建立的第一個公用資料夾信箱。後續的公用資料夾信箱將會是次要公用資料夾信箱，將會包含此階層及內容的唯讀複本。

如需詳細步驟，請參閱[建立公用資料夾信箱](create-a-public-folder-mailbox-exchange-2013-help.md)。

## 步驟 2：建立您的第一個公用資料夾

如需詳細步驟，請參閱[建立公用資料夾](create-a-public-folder-exchange-2013-help.md)。

## 步驟 3：指派權限到公用資料夾

建立公用資料夾後，您將需要指派 \[擁有者\] 權限層級，至少一位使用者可以從用戶端存取公用資料夾並建立子資料夾。在此之後建立的任何公用資料夾將繼承父公用資料夾的權限。

1.  在 Exchange 管理中心 (EAC) 內，瀏覽至 **\[公用資料夾\]** \> **\[公用資料夾\]**。

2.  在清單檢視中，選取公用資料夾。

3.  在詳細資訊窗格中，\[資料夾權限\] 下，按一下 \[管理\]。

4.  在 \[公用資料夾權限\] 中，按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

5.  按一下 \[瀏覽\] 來選取使用者。

6.  在 \[權限等級\] 清單中，選取一個等級。至少一名使用者應為 \[擁有者\]。

7.  按一下 \[儲存\]。

8.  您可以按一下按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示") 並使用上述步驟指派適當的權限來新增多個使用者。您也可以選取或清除核取方塊來自訂權限層級。編輯預先定義權限層級時，例如 \[擁有者\]，權限層級會變更至 \[自訂\]。

如需如何使用命令介面以指派權限給公用資料夾的資訊，請參閱[Add-PublicFolderClientPermission](https://technet.microsoft.com/zh-tw/library/bb124743\(v=exchg.150\))。

## 步驟 4 (選用)：擁有郵件功能的公用資料夾

如果您希望使用者能寄送郵件到公用資料夾，您可以啟用它的郵件功能。此步驟是選用的。如果您不啟用公用資料夾的郵件功能，使用者可以透過從 Outlook 中拖曳項目到公用資料夾中來張貼郵件。

1.  在 EAC 中，瀏覽至 \[公用資料夾\] \> \[公用資料夾\]。

2.  在清單檢視中，選取要啟用郵件功能的公用資料夾。

3.  在詳細資料窗格中，在 \[郵件設定 – 已停用\] 下，按一下 \[啟用\]。
    
    將會顯示警告，詢問您是否確定要啟用該公用資料夾的郵件功能。按一下 **\[是\]**。

公用資料夾將可使用郵件，公用資料夾的名稱將成為公用資料夾的別名。如果您有使用該名稱的多個收件者，公用資料夾的別名將會加上編號。例如，如果您有一個名為 SalesTeam 的通訊群組，而您建立一個名為 SalesTeam 的共用資料夾，然後啟用資料夾的郵件，公用資料夾的別名將會是 SalesTeam1。

如需如何使用命令介面以啟用公用資料夾的郵件，請參閱[Enable-MailPublicFolder](https://technet.microsoft.com/zh-tw/library/aa998824\(v=exchg.150\))。

