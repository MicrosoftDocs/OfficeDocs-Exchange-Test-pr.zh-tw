---
title: '設定 Outlook 語音存取使用者連入的使用者群組: Exchange Online Help'
TOCTitle: 設定 Outlook 語音存取使用者連入的使用者群組
ms:assetid: a8dc0f9e-dc86-4128-af63-d4e550aed5bb
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee423551(v=EXCHG.150)
ms:contentKeyID: 50473906
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定 Outlook 語音存取使用者連入的使用者群組

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2012-11-09_

您可以指定哪些使用者可以接收轉接的通話或語音信箱訊息從 Outlook 語音存取使用者。根據預設，**只有撥號計劃中**已選取選項。您可以變更此設定可讓 Outlook 語音存取使用者將來電轉接或語音訊息傳送給現有 UM 自動語音應答，或特定分機號碼整個組織中的使用者。

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

## 使用 EAC 來設定 Outlook 語音存取使用者連入的使用者群組

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。

2.  在清單檢視中，選取您要修改的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 \[UM 撥號對應表\] 頁面上，按一下 \[設定\]。

4.  在**傳輸與搜尋**、 \[**允許來電者在搜尋會根據名稱或別名的使用者**，選取下列選項之一：
    
      - **僅限撥號計劃中**  使用此選項可讓 Outlook 語音存取使用者撥打 Outlook 語音存取號碼來找出及連絡人在同一個撥號對應表中的使用者。
    
      - **在整個組織中**  使用此選項可讓 Outlook 語音存取使用者撥打 Outlook 語音存取號碼來找出及連絡人在整個組織中的任何人。這包括所擁有信箱功能的所有使用者。
    
      - **僅在此自動語音應答**  使用此選項可讓 Outlook 語音存取使用者撥打 Outlook 語音存取號碼來連線至特定的自動語音應答。您必須在此處指定之前建立的自動語音應答。這可讓 Outlook 語音存取使用者轉接至另一個自動語音應答。您在此處所選擇的自動語音應答可以啟用語音功能或未啟用語音的自動語音應答。
    
      - **僅針對此延伸模組**  使用此選項可允許 Outlook 語音存取使用者連線至您指定的分機號碼。您可以使用數值的數字的副檔名。在此欄位中所定義的數字數目必須符合 UM 撥號對應表所設定的分機號碼中的數字數目。

5.  按一下 **\[儲存\]**。

## 使用命令介面來設定 Outlook 語音存取使用者連入的使用者群組

本範例會設定 Outlook 語音存取使用者連入 UM 撥號對應表名為`MyUMDialPlan`為整個組織的使用者群組。

    Set-UMDialPlan -Identity MyUMDialPlan -ContactScope 'GlobalAddressList' -UMAutoAttendant $null -AllowDialPlanSubscribers $false -AllowExtensions $false

本範例會設定 Outlook 語音存取使用者連入名為`MyUMDialPlan``DialPlan`至 UM 撥號對應表的使用者群組。

    Set-UMDialPlan -Identity MyUMDialPlan -ContactScope DialPlan -AllowDialPlanSubscribers $false -AllowExtensions $false

