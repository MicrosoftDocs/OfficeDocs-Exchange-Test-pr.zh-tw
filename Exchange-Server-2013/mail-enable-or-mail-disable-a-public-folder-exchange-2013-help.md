---
title: '郵件啟用或停用郵件功能的公用資料夾: Exchange Online Help'
TOCTitle: 郵件啟用或停用郵件功能的公用資料夾
ms:assetid: 3d69f76d-ff3c-46c1-b962-6a1baa425d8a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa997560(v=EXCHG.150)
ms:contentKeyID: 50472997
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 郵件啟用或停用郵件功能的公用資料夾

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2016-06-15_

公用資料夾的設計目的在於共用存取並提供簡易有效率的方式來收集、 組織及與工作群組或組織中其他人共用資訊。啟用公用資料夾的擁有郵件功能可讓使用者透過它傳送電子郵件訊息張貼至公用資料夾。公用資料夾時啟用郵件之其他設定變成可用才能進行Exchange系統管理中心 (EAC)，例如電子郵件地址與信箱配額的公用資料夾。在命令介面中的公用資料夾是擁有郵件功能之前您使用**Set-PublicFolder**指令程式來管理其所有設定。公用資料夾擁有郵件功能後，您使用**Set-PublicFolder**和**Set-MailPublicFolder**指令程式來管理設定。

如果您希望將郵件傳送到擁有郵件功能之公用資料夾網際網路上的使用者，您需要設定其他權限使用**Add-PublicFolderClientPermission**指令程式。

如需與管理公用資料夾相關的其他管理工作，請參閱[公用資料夾程序](public-folder-procedures-exchange-2013-help.md)。

如需與公用資料夾相關的其他管理工作，請參閱 [Office 365 和 Exchange Online 中公用資料夾程序](https://technet.microsoft.com/zh-tw/library/jj966272\(v=exchg.150\))。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘

  - 為了確保網際網路上的使用者可以傳送電子郵件至擁有郵件功能之公用資料夾，公用資料夾需要有至少*CreateItems*權右授與匿名帳戶。如果您想要了解如何執行這項作業，請參閱允許匿名使用者傳送電子郵件至擁有郵件功能的公用資料夾。

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


## 您要執行的工作

## 使用 EAC 來啟用郵件功能或停用郵件功能的公用資料夾

1.  瀏覽至 \[公用資料夾\] \> \[公用資料夾\]。

2.  在清單檢視中，選取您想要郵件啟用或停用郵件功能的公用資料夾。

3.  在詳細資料窗格中，\[**郵件設定**\] 下按一下 \[**啟用**或**停用**\]。

4.  警告\] 對話方塊會顯示詢問您是否確定要啟用或停用的公用資料夾的電子郵件。按一下**\[是\]**繼續。

如果您想將郵件傳送到此公用資料夾的外部使用者，請務必遵循允許匿名使用者傳送電子郵件至擁有郵件功能的公用資料夾中的步驟。

## 使用命令介面來啟用公用資料夾的郵件

本範例會啟用郵件功能的公用資料夾 Help Desk。

    Enable-MailPublicFolder -Identity "\Help Desk"

本範例郵件啟用 Marketing 公用資料夾下的公用資料夾報告但隱藏通訊清單的資料夾。

    Enable-MailPublicFolder -Identity "\Marketing\Reports" -HiddenFromAddressListsEnabled $True

如果您希望將郵件傳送到此公用資料夾的外部使用者，請確定您依照中允許匿名使用者傳送電子郵件給擁有郵件功能之公用資料夾的步驟。

如需詳細的語法及參數資訊，請參閱[Enable-MailPublicFolder](https://technet.microsoft.com/zh-tw/library/aa998824\(v=exchg.150\))。

## 使用命令介面來停用郵件功能的公用資料夾

此範例會停用郵件功能的公用資料夾 Marketing\\Reports。

    Disable-MailPublicFolder -Identity "\Marketing\Reports"

如需詳細的語法及參數資訊，請參閱[Disable-MailPublicFolder](https://technet.microsoft.com/zh-tw/library/bb123781\(v=exchg.150\))。

## 允許匿名使用者傳送電子郵件給擁有郵件功能的公用資料夾

您可以使用Outlook或命令介面來設定權限的公用資料夾匿名帳戶。您無法使用 EAC 來設定權限的匿名帳戶。

**使用Outlook設定的匿名帳戶的權限**

1.  開啟Outlook使用的帳戶是擁有者權限電子郵件功能的公用資料夾要匿名使用者傳送郵件給已授與。

2.  瀏覽至 \[**公用資料夾-\< 使用者的名稱 \>**。

3.  瀏覽至您要變更的公用資料夾。

4.  在公用資料夾上按一下滑鼠右鍵、 按一下 \[**內容**\]，然後選取 \[**權限**\] 索引標籤。

5.  選取 \[**匿名**帳戶、 選取 \[**寫入**\]**建立的項目**，然後按一下 \[**確定\]**。

**使用命令介面來設定的匿名帳戶的權限**

本範例會設定 「 客戶意見 」 擁有郵件功能的公用資料夾上的匿名帳戶`CreateItems`權限。

    Add-PublicFolderClientPermission "\Customer Feedback" -AccessRights CreateItems -User Anonymous

如需詳細的語法與參數資訊，請參閱[Add-PublicFolderClientPermission](https://technet.microsoft.com/zh-tw/library/bb124743\(v=exchg.150\))。

