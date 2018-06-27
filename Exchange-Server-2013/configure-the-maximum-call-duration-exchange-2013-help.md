---
title: '設定最大的通話時間: Exchange Online Help'
TOCTitle: 設定最大的通話時間
ms:assetid: 01aa40d2-f918-472b-bace-158222143484
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee423535(v=EXCHG.150)
ms:contentKeyID: 50472461
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定最大的通話時間

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2012-11-09_

您可以指定來電可連接至系統沒有之前結束通話轉接至有效的分機號碼的分鐘數數目上限。對於大多數的組織而言，此值應設為預設值： 30 分鐘。此設定會套用到所有通話，包括 Outlook 語音存取來電、 語音通話內部組織、 語音通話將整合通訊 (UM) 自動語音應答及從放置在組織外的傳真呼叫。

此值可設介於 10%到 120 數字。將此值過低可能會造成來電轉接給他們正在完成之前會中斷連線。例如，如果您的組織會收到許多大型傳真訊息，可能要考慮增加此值從預設使接收傳真訊息的所有頁面。

如需與 UM 撥號對應表相關的其他工作，請參閱[UM 撥號對應表規劃程序](um-dial-plan-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 撥號對應表」項目。

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

## 使用 EAC 來設定最大的通話時間

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。

2.  在清單檢視中，選取您要修改的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[UM 撥號對應表\] 頁面上，按一下 \[設定\]。

4.  在 \[**設定**\] 下**最多通話持續時間 （分鐘）**，請輸入數字以分鐘為單位。

5.  按一下 **\[儲存\]**。

## 使用命令介面來設定最大的通話時間

本範例會設定名為`MyUMDialPlan`建立 UM 撥號對應表計劃為 10 分鐘的最大的通話時間。

    Set-UMDialPlan -identity MyUMDialPlan -MaxCallDuration 10

