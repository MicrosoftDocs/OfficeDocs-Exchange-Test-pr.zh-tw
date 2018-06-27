---
title: '建立公用資料夾: Exchange Online Help'
TOCTitle: 建立公用資料夾
ms:assetid: 6d252e60-c8d0-4efd-b9d7-ba5284a6f8ab
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb691104(v=EXCHG.150)
ms:contentKeyID: 50473409
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.PublicFolders.NewPublicFolderWizardForm.NewPublicFolderWizardPage
ms.translationtype: MT
---

# 建立公用資料夾

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2014-02-24_

公用資料夾的設計目的在於共用存取，並提供簡易有效率的方式來收集及組織資訊，以及與工作群組或組織中的其他人員共用資訊。

依預設，公用資料夾會沿用其父項資料夾的設定，包括權限設定在內。

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


如需與管理公用資料夾相關的其他管理工作，請參閱[公用資料夾程序](public-folder-procedures-exchange-2013-help.md)。

如需與公用資料夾相關的其他管理工作，請參閱 [Office 365 和 Exchange Online 中公用資料夾程序](https://technet.microsoft.com/zh-tw/library/jj966272\(v=exchg.150\))。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [共用和協同作業的權限](sharing-and-collaboration-permissions-exchange-2013-help.md)主題中的「公用資料夾」項目。

  - 除非先建立公用資料夾信箱，否則無法建立公用資料夾。如需如何建立公用資料夾信箱的詳細資訊，請參閱[建立公用資料夾信箱](create-a-public-folder-mailbox-exchange-2013-help.md)。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

## 您要執行的工作

## 使用 EAC 建立共用資料夾

當使用 EAC 建立公用資料夾時，只能設定該公用資料夾的名稱與路徑。若要設定其他設定，則需要在建立之後編輯公用資料夾。

1.  瀏覽至 \[公用資料夾\] \> \[公用資料夾\]。

2.  若要建立此公用資料夾作為現有公用資料夾的子資料夾，請按一下清單檢視中現有的公用資料夾。若要建立一個頂層共用資料夾，請略過此步驟。

3.  按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

4.  在 \[公用資料夾\] 中，輸入公用資料夾的名稱。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>建立公用資料夾時，請勿在名稱中使用反斜線 (\)。</td>
    </tr>
    </tbody>
    </table>


5.  在 \[路徑\] 方塊中，驗證公用資料夾的路徑。如果不是想要的路徑，則按一下 \[取消\]，然後依照此程序的步驟 2 進行。

6.  按一下 \[儲存\]。

## 使用命令介面來建立公用資料夾

此範例會在路徑 Marketing\\2013 中建立一個名為 Reports 的公用資料夾。

    New-PublicFolder -Name Reports -Path \Marketing\2013

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>建立公用資料夾時，請勿在名稱中使用反斜線 (\)。</td>
</tr>
</tbody>
</table>


如需詳細的語法及參數資訊，請參閱 [New-PublicFolder](https://technet.microsoft.com/zh-tw/library/aa996405\(v=exchg.150\))。

## 如何知道這是否正常運作？

若要確認是否已成功建立公用資料夾，請執行下列其中一個操作：

  - 在 EAC 中，按一下 \[重新整理\] 來重新整理公用資料夾清單。新的公用資料夾應該會顯示在清單中。

  - 在命令介面中，執行下列任一命令：
    
        Get-PublicFolder -Identity \Marketing\2013\Reports | Format-List
    
        Get-PublicFolder -Identity \Marketing\2013 -GetChildren
    
        Get-PublicFolder -Recurse

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

