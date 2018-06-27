---
title: '建立 UM 信箱原則: Exchange Online Help'
TOCTitle: 建立 UM 信箱原則
ms:assetid: 7f20874b-c46c-4505-9a78-f63eacb578ff
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb123510(v=EXCHG.150)
ms:contentKeyID: 50554015
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.CreateUMMailboxPolicyWizardForm.CreateUMMailboxPolicyWizardPage
ms.translationtype: MT
---

# 建立 UM 信箱原則

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-03-08_

您可以建立整合通訊 (UM) 信箱原則套用至一組已啟用 UM 之信箱的一組通用的 UM 原則設定，例如 PIN 原則設定\] 或 \[撥號限制。UM 信箱原則連結已啟用 UM 的使用者與 UM 撥號對應表和套用至一組已啟用 UM 之信箱的一組通用原則\] 或 \[安全性設定。UM 信箱原則可用套用並標準化的已啟用 UM 之使用者的 UM 組態設定。

根據預設，當建立 UM 撥號對應表、 UM 信箱原則也建立。您可能必須建立額外的 UM 信箱原則或您部署在組織中的 \[整合通訊之後修改現有的 UM 信箱原則。

如需其他與 UM 信箱原則相關的管理工作，請參閱 [UM 信箱原則程序](um-mailbox-policy-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：3 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 信箱原則」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。 如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

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

## 使用 EAC 建立 UM 信箱規則

1.  
    
    在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。在清單檢視中，選取您要修改的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 **\[UM 撥號對應表\]** 頁面的 **\[UM 信箱原則\]** 底下，按一下 **\[新增\]**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

3.  在 **\[新增 UM 信箱原則\]** 頁面的 **\[名稱\]** 方塊中，輸入新 UM 信箱原則的名稱。
    
    使用此方塊可指定之 UM 信箱原則的唯一名稱。這是出現在 EAC 中的顯示名稱。如果您需要變更 UM 信箱原則的顯示名稱建立之後，您必須先刪除現有的 UM 信箱原則，並再建立另一個具有適當的名稱的 UM 信箱原則。您無法刪除 UM 信箱原則若任何已啟用 UM 之使用者有與其相關聯。
    
    UM 信箱原則名稱是必要的但僅顯示用途使用。因為您的組織可能會使用多個 UM 信箱原則，我們建議您使用您的 UM 信箱原則的有意義的名稱。UM 信箱原則名稱的最大長度是 64 個字元，而且它可以包含空格。不過，它不能包含任何下列字元："/ \\ \[\]:; |= , + \* ?\< \>。

4.  按一下 \[儲存\] 儲存新的 UM 信箱原則。儲存 UM 信箱原則時，將啟用所有預設設定，包括 PIN 原則、語音信箱功能，以及受保護的語音信箱設定。如果要自訂或變更任何預設設定，請使用 **Set-UMMailbox** 指令程式，針對您剛才建立的 UM 信箱原則變更設定。

## 使用命令介面來建立 UM 信箱原則

此範例會建立名稱爲 `MyUMMailboxPolicy` 的 UM 信箱原則，並與名爲 `MyUMDialPlan` 的 UM 撥號對應表相關聯。

    New-UMMailboxPolicy -Name MyUMMailboxPolicy -UMDialPlan MyUMDialPlan

