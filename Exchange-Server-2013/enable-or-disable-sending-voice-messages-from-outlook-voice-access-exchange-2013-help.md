---
title: '啟用或停用從 Outlook 語音存取傳送語音訊息: Exchange Online Help'
TOCTitle: 啟用或停用從 Outlook 語音存取傳送語音訊息
ms:assetid: 63544ae2-6a28-40b2-82fc-3df83e93ee56
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee423546(v=EXCHG.150)
ms:contentKeyID: 52062328
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟用或停用從 Outlook 語音存取傳送語音訊息

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2012-12-13_

您可以允許 Outlook Voice Access 使用者將語音信箱訊息傳送到與相同撥號對應表相關聯且已啟用 UM 功能的其他使用者，或是防止他們這樣做。

根據預設，會啟用此設定。如果您停用此設定，Outlook 語音存取使用者撥打 Outlook 語音存取號碼將不能夠將語音郵件傳送至同一個撥號對應表內的使用者。

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

## 使用 EAC 來允許或防止 Outlook 語音存取使用者將語音訊息傳送給相同撥號對應表中的使用者

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。

2.  在清單檢視中，選取您要變更的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[UM 撥號對應表\] 頁面上，按一下 \[設定\]。

4.  在**傳輸與搜尋**、 \[**允許來電者**，選取 \[允許傳送語音訊息**留下語音訊息而響鈴使用者的電話**。若要防止傳送語音郵件訊息的使用者，清除此設定。

5.  按一下 **\[儲存\]**。

## 使用命令介面來允許或防止 Outlook 語音存取使用者將語音訊息傳送給相同撥號對應表中的使用者

此範例會允許與名為 `MyUMDialPlan` 的 UM 撥號對應表相關聯的 Outlook 語音存取使用者，傳送語音訊息給與相同撥號對應表相關聯的使用者。

    Set-UMDialPlan -identity MyUMDialPlan -SendVoiceMsgEnabled $true

此範例會防止與名為 `MyUMDialPlan` 的 UM 撥號對應表相關聯的 Outlook 語音存取使用者，傳送語音訊息給與相同撥號對應表相關聯的使用者。

    Set-UMDialPlan -identity MyUMDialPlan -SendVoiceMsgEnabled $false

