---
title: 'Outlook 語音存取使用者中斷連線之前設定輸入失敗的次數: Exchange Online Help'
TOCTitle: Outlook 語音存取使用者中斷連線之前設定輸入失敗的次數
ms:assetid: 64c13d17-a26a-4c9b-b495-bd69c716456a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee423547(v=EXCHG.150)
ms:contentKeyID: 50473356
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook 語音存取使用者中斷連線之前設定輸入失敗的次數

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2012-11-09_

您可以設定撥打 Outlook 語音存取號碼的使用者可以輸入不正確的資料之前所要中斷連線的次數。此設定會套用到Outlook語音存取使用者與未經過驗證的來電者使用目錄搜尋。

以下是會視為不正確資料類型的範例：

  - 系統中找不到來電者要求的分機號碼。

  - 系統找不到該使用者的分機號碼來轉接來電。

  - 來電者按下無效的功能表選項。

此設定的值可以是介於 1 到 20。對於大多數的組織而言，此值應設為預設值是三個嘗試。將此值過低可能會提前中斷來電者。

如需與 UM 撥號對應表相關的其他管理工作，請參閱 [UM 撥號對應表規劃程序](um-dial-plan-procedures-exchange-2013-help.md)。

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

## 使用 EAC 來設定中斷連線前的輸入錯誤次數

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。

2.  在清單檢視中，選取您要修改的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[UM 撥號對應表\] 頁面上，按一下 \[設定\]。

4.  在 \[設定\]中，在 \[中斷連線之前發生輸入錯誤\]底下，輸入輸入錯誤的次數。

5.  按一下 \[儲存\]。

## 使用命令介面設定中斷連線之前發生輸入錯誤的次數

此範例會在名爲 `MyUMDialPlan` 的 UM 撥號對應表上將中斷連線之前發生輸入錯誤的次數設定為 5。

    Set-UMDialPlan -identity MyUMDialPlan -InputFailuresBeforeDisconnect 5

