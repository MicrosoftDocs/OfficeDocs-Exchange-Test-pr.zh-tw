---
title: '設定最大錄製持續時間: Exchange Online Help'
TOCTitle: 設定最大錄製持續時間
ms:assetid: 18eeb567-1048-4c82-93cf-612cb12ec5e3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee423539(v=EXCHG.150)
ms:contentKeyID: 50472715
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定最大錄製持續時間

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2012-11-09_

您可以指定允許的每個語音通話記錄時來電者留下語音信箱訊息的分鐘數數目上限。此值可設介於 1 到 100 數字。對於大多數的組織而言，此值應設為預設值是 20 分鐘。將此值過低可能會造成長語音訊息，他們正在完成之前會中斷連線。將此值過高可讓使用者較長的語音訊息儲存在其收件匣。

此設定，請務必如果您已經實作嚴格磁碟配額的使用者。其必須設為大於**最大通話持續時間 （分鐘）**的一組較低值。

如需與 UM 撥號對應表相關的其他工作，請參閱[UM 撥號對應表規劃程序](um-dial-plan-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 少於 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md) 主題中的「UM 撥號對應表」項目。

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

## 使用 EAC 來設定最大記錄期間

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。

2.  在清單檢視中，選取您要修改的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[UM 撥號對應表\] 頁面上，按一下 \[設定\]。

4.  在 \[設定\] 中的 \[最大記錄持續期間 (分鐘)\] 下，輸入分鐘數字。

5.  按一下 \[儲存\]。

## 使用命令介面來設定最大記錄持續期間

此範例會在名爲 `MyUMDialPlan` 的 UM 撥號對應表上，將最大記錄持續期間設為 10 分鐘。

    Set-UMDialPlan -identity MyUMDialPlan -MaxRecordingDuration 10

