---
title: '設定可連絡的使用者群組: Exchange Online Help'
TOCTitle: 設定可連絡的使用者群組
ms:assetid: 45d9d6d5-c9d6-4b73-8aa2-a23599a4381c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee423545(v=EXCHG.150)
ms:contentKeyID: 52062320
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定可連絡的使用者群組

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2012-12-09_

您可以指定來電者可連絡到整合通訊 (UM) 自動語音應答呼叫時的使用者群組。根據預設，來電者可以連絡有關聯的 UM 自動語音應答同一個撥號對應表計劃中的使用者。不過，您可以變更使用者可允許將來電轉接或語音訊息傳送給使用者的來電者所在的組織通訊錄中或一組特定的使用者的群組。

如需與 UM 自動語音應答相關的其他管理工作，請參閱[管理 UM 自動語音應答](manage-a-um-auto-attendant-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 自動語音應答」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在執行這些程序之前，請確認已建立 UM 自動語音應答。 如需詳細步驟，請參閱[建立 UM 自動語音應答](create-a-um-auto-attendant-exchange-2013-help.md)。

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

## 使用 EAC 設定來電者可以連絡的使用者群組

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。在清單檢視中，選取您要變更的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 **\[UM 撥號對應表\]** 頁面的 **\[UM 自動語音應答\]** 下方，選取您要設定的 UM 自動語音應答，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 **\[UM 自動語音應答\]** 頁面 \> **\[通訊錄和操作員存取\]** 中，於 **\[搜尋通訊錄的選項\]** 下方選擇以下選項：
    
      - **\[僅限在此撥號對應表\]**   選取此選項可讓連線到 UM 自動語音應答的來電者找到並連絡位於與 UM 自動語音應答相關聯之撥號對應表中的使用者。
    
      - **在整個組織中**  選取這個選項可讓來電者連接至找出並連絡組織的通訊錄中所列的任何人的 UM 自動語音應答。這包括所擁有信箱功能的所有使用者。

4.  按一下 **\[儲存\]**。

## 使用命令介面設定來電者可以連絡的使用者群組

此範例會在名爲 `MyUMAutoAttendant` 的 UM 自動語音應答上，將來電者可以連絡的使用者範圍設定為組織通訊錄中的所有使用者。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -ContactScope GlobalAddressList

