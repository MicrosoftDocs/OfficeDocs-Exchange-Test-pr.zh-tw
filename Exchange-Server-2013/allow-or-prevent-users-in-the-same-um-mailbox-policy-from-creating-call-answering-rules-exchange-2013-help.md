---
title: '允許或防止使用者在相同的 UM 信箱原則建立通話自動答錄服務規則: Exchange Online Help'
TOCTitle: 允許或防止使用者在相同的 UM 信箱原則建立通話自動答錄服務規則
ms:assetid: e44acaa6-d5a8-41e8-94aa-100be0bd6391
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd351209(v=EXCHG.150)
ms:contentKeyID: 50554075
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 允許或防止使用者在相同的 UM 信箱原則建立通話自動答錄服務規則

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-22_

您可以讓與整合通訊 (UM) 信箱原則來設定通話自動答錄規則、 相關聯的使用者或防止能力。如果選項可設定自動答錄規則已停用 UM 撥號對應表上，將與 UM 信箱原則相關聯的已啟用 UM 之使用者可呼叫接聽規則功能。會啟用預設設定。

如需與允許使用者轉接來電相關的其他管理工作，請參閱[轉接通話程序](forwarding-calls-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 2 分鐘。

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

## 使用 EAC 在 UM 信箱原則上啟用或停用自動答錄規則

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。在清單檢視中，選取您要變更的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 \[UM 信箱原則\] 下，選取您要管理的 UM 信箱原則，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[UM 信箱原則\] 頁面中，選取或清除 \[允許使用者設定自動答錄規則\] 旁邊的核取方塊。

4.  按一下 \[儲存\]。

## 使用命令介面來啟用或停用 UM 信箱原則上的自動答錄服務規則

此範例可讓與 UM 信箱原則 `MyUMMailboxPolicy` 相關聯的使用者建立自動答錄規則。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowCallAnsweringRules $true

這個範例會防止與 UM 信箱原則 `MyUMMailboxPolicy` 關聯的使用者建立自動答錄服務規則。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowCallAnsweringRules $false

