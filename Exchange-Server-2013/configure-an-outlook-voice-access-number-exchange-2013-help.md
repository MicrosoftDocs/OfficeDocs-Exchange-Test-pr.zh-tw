---
title: '設定 Outlook 語音存取號碼: Exchange Online Help'
TOCTitle: 設定 Outlook 語音存取號碼
ms:assetid: 443c838e-f266-4893-b6b2-e5fc96579b55
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa997680(v=EXCHG.150)
ms:contentKeyID: 50553974
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定 Outlook 語音存取號碼

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2016-12-09_

Outlook Voice Access 號碼可讓整合通訊 (UM) 及語音信箱啟用的使用者存取使用Outlook語音存取其信箱。當您設定 Outlook 語音存取或訂戶存取號碼撥號對應表時、 已啟用 UM 的使用者可以撥打的號碼、 登入他們的信箱和存取其電子郵件、 語音信箱、 行事曆及個人連絡資訊。

根據預設，當您建立 UM 撥號對應表、 數字不設定 Outlook 語音存取。若要設定 Outlook 語音存取號碼，您需要建立的撥號對應表，並則設定在**Outlook 語音存取**的撥號\] 選項底下 Outlook 語音存取號碼。Outlook 語音存取號碼不一定，您需要設定至少一個啟用用來存取其信箱的Outlook語音存取已啟用 UM 之使用者的 Outlook 語音存取號碼。您可以設定單一撥號對應表的多個 Outlook Voice Access 的號碼。

Outlook 語音存取號碼可以包含字母、 數字，和特殊字元、 分隔符號和空格。例如：

  - \+14255551010

  - \+1-425-555-1010

  - 4255551010

  - \+1 425 555 1010

  - 1-800-555-CALL

如需Outlook語音存取使用者可用的功能表選項的詳細資訊，請參閱適用於Outlook語音存取的快速參考指南是可從[Microsoft 下載中心](https://go.microsoft.com/fwlink/p/?linkid=64645)。

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

## 使用 EAC 設定 Outlook 語音存取號碼

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。

2.  在清單檢視中，選取您要修改的 UM 撥號對應表，然後在工具列上按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[UM 撥號對應表\] 頁面上，按一下 \[設定\]。

4.  在 \[Outlook 語音存取\] 的 \[Outlook 語音存取號碼\] 下方，使用方塊輸入您要使用的號碼，然後按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

5.  按一下 \[儲存\]。

## 使用命令介面設定 Outlook 語音存取號碼

此範例會將名爲 `MyUMDialPlan` 的 UM 撥號對應表的 Outlook 語音存取號碼設為 4255550100。

    Set-UMDialPlan -identity MyUMDialPlan -AccessTelephoneNumbers 4255550100

