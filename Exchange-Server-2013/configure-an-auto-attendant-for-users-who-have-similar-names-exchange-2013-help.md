---
title: '設定具有相似名稱的使用者自動語音應答: Exchange Online Help'
TOCTitle: 設定具有相似名稱的使用者自動語音應答
ms:assetid: 2e7318a0-67f9-4d7b-8300-5f0ef77656a8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa997135(v=EXCHG.150)
ms:contentKeyID: 52062268
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定具有相似名稱的使用者自動語音應答

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2012-12-16_

您可以設定要使用的使用者使用相似名稱的自動語音應答**處理活頁簿及運算子存取**選項方法或您可以在自動語音應答維持預設設定並在撥號對應表相關聯的自動語音應答上設定此設定。根據預設，自動語音應答可以釐清之間兩個或多個使用者的自動語音應答上設定的預設值是**從撥號對應表繼承**因為具有相同或類似的名稱。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要讓隨附於類似名稱之使用者的資訊正常運作，您必須在 Microsoft Exchange 組織中提供收件者的職稱、部門和位置資訊。</td>
</tr>
</tbody>
</table>


如需與 UM 自動語音應答相關的其他管理工作，請參閱[UM 自動語音應答程序](um-auto-attendant-procedures-exchange-2013-help.md)。

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

## 使用 EAC 為名稱類似的使用者設定 UM 自動語音應答

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。在清單檢視中，選取您要變更的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 **\[UM 撥號對應表\]** 頁面的 **\[UM 自動語音應答\]** 下方，選取您要設定的 UM 自動語音應答，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 **\[UM 自動語音應答\]** 頁面上，按一下 **\[通訊錄和操作員存取\]** 並在 **\[要為同名使用者納入的資訊\]** 下，選取下列其中一者：
    
      - **職稱**   當自動語音應答列出相符項目時會併入每位使用者的職稱。
    
      - **部門**   當自動語音應答列出相符項目時會併入每位使用者的部門。
    
      - **位置**   當自動語音應答列出相符項目時會併入每位使用者的位置。
    
      - **無**   當自動語音應答列出相符項目時不會併入任何其他資訊。
    
      - **提示別名**   自動語音應答會提示來電者輸入使用者的別名。
    
      - **從撥號對應表繼承**   自動語音應答會使用與自動語音應答關聯之撥號對應表中的預設設定。

4.  按一下 **\[儲存\]**。

## 使用命令介面為名稱類似的使用者設定 UM 自動語音應答

此範例會針對名為 `MyUMAutoAttendant` 的 UM 自動語音應答，將為名稱類似的使用者納入的資訊設為 \[提示別名\]。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -MatchedNameSelectionMethod PromptForAlias

此範例會為名為 `MyUMAutoAttendant` 的 UM 自動語音應答，將為名稱類似的使用者納入的資訊設為使用者的職稱、啟用名稱查閱，以及讓撥入自動語音應答的來電者按 \* 即可聽到 Outlook 語音存取歡迎使用問候語。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -MatchedNameSelectionMethod Title -NameLookupEnabled $true -StarOutToDialPlanEnabled $true

