---
title: '啟用的一組使用者的傳真功能: Exchange Online Help'
TOCTitle: 啟用的一組使用者的傳真功能
ms:assetid: b8d9f54d-ff06-4942-83e1-fc6c4ad02178
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee423556(v=EXCHG.150)
ms:contentKeyID: 52062401
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟用的一組使用者的傳真功能

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2016-12-09_

您可以啟用傳入傳真\] 連結與整合通訊 (UM) 信箱原則的使用者。根據預設，當您啟用使用者的整合通訊的使用者無法接收傳真訊息直到您指定之伺服器的 URI 傳真協力廠商，針對您的組織部署傳真協力廠商伺服器以及啟用 UM 信箱原則上的傳真功能。如果允許傳入傳真\] 選項已停用 UM 撥號對應表上，連結與 UM 信箱原則的使用者仍將不能夠接收傳真\]。同樣地，如果允許傳入傳真\] 選項已停用在個別使用者，該使用者將無法接收傳真\]。

如需傳真協力廠商的詳細資訊，請參閱[Microsoft PinPoint 傳真協力廠商](https://go.microsoft.com/fwlink/?linkid=190238)。

如需與傳真相關的其他管理工作，請參閱[傳真程序](faxing-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 信箱原則」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

  - 執行這些程序之前，請確認已建立 UM 信箱原則。如需詳細步驟，請參閱[建立 UM 信箱原則](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 您要執行的工作

## 使用 EAC 啟用輸入傳真

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。在清單檢視中，選取您要修改的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 **\[UM 撥號對應表\]** 頁面的 **\[UM 信箱原則\]** 下方，選取您要修改的信箱原則，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 **\[UM 信箱原則\]** 頁面 \> **\[一般\]** 上，選取 **\[允許輸入傳真\]** 旁的核取方塊。

4.  按一下 **\[儲存\]** 以儲存變更。

## 使用命令介面啟用輸入傳真

此範例可讓與 UM 信箱原則 `MyUMMailboxPolicy` 連結的使用者使用輸入傳真。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowFax $true

