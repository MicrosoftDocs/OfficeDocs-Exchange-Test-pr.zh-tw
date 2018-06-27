---
title: '設定撥號對應表具有相似名稱的使用者: Exchange Online Help'
TOCTitle: 設定撥號對應表具有相似名稱的使用者
ms:assetid: 14783f45-95f5-49de-8215-0a3aef7dc034
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb266943(v=EXCHG.150)
ms:contentKeyID: 51409155
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定撥號對應表具有相似名稱的使用者

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-21_

您可以設定整合通訊 (UM) 撥號來指定當使用者有相同或類似的名稱提供給來電者的資訊。UM 使用此設定來區分之間具有相同或類似的名稱與這項資訊提供給來電者的使用者。來電者或Outlook語音存取使用者會出現提示時輸入來尋找特定使用者的字母，有時多個名稱比對來電者的輸入。您可用於其中一個可用的選項來提供來電者的詳細資訊與協助他們找出的使用者他們正在嘗試連絡。

您可以在 UM 撥號對應表和 UM 自動語音應答上設定此設定。建立 UM 自動語音應答、 時加以繼承此設定撥號對應表相關聯的自動語音應答。根據預設，此設定未設定撥號對應表讓沒有額外資訊會提供給來電者可協助他們找出正確的使用者。

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

## 使用 EAC 為具有類似名稱的使用者設定 UM 撥號對應表

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。在清單檢視中，選取您要變更的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 **\[UM 撥號對應表\]** 頁面上，按一下 **\[設定\]** \> **\[傳輸與搜尋\]**，然後在 **\[要為具有相同名稱的使用者併入的資訊\]** 下，選取下列其中一個選項：
    
      - **職稱**   撥號對應表會在找到兩個以上具有類似名稱的使用者時併入每一個使用者的職稱。
    
      - **部門**   撥號對應表會在找到兩個以上具有類似名稱的使用者時併入每一個使用者的部門。
    
      - **位置**   撥號對應表會在找到兩個以上具有類似名稱的使用者時併入每一個使用者的位置。
    
      - **無**  當使用者有類似的名稱撥號對應表不包含任何其他資訊。雖然這是預設設定，我們建議您加入一個來電者的可用選項。如果您沒有來電者將不能夠告知使用相似名稱的兩個或多個使用者之間的差異。
    
      - **提示的別名**  撥號對應表會提示來電者的使用者的別名。別名是使用者的電子郵件或之前的 SMTP 地址的一部分在 (@) 符號。

3.  按一下 **\[儲存\]**。

## 使用命令介面為具有類似名稱的使用者設定 UM 撥號對應表

本範例會設定要與具有類似名稱的使用者一起併入的資訊，以提示輸入 UM 撥號對應表 (名稱為 `MyDialPlan`) 上的使用者別名。

    Set-UMDialplan -Identity MyDialPlan -MatchedNameSelectionMethod PromptForAlias

本範例會將要與具有類似名稱的使用者一起併入的資訊設為 UM 撥號對應表 (名稱為 `MyDialPlan`) 上的部門。

    Set-UMDialplan -Identity MyDialPlan -MatchedNameSelectionMethod Department

本範例會將要與具有類似名稱的使用者一起併入的資訊設為 UM 撥號對應表 (名稱為 `MyDialPlan`) 上的位置。

    Set-UMDialplan -Identity MyDialPlan -MatchedNameSelectionMethod Location

