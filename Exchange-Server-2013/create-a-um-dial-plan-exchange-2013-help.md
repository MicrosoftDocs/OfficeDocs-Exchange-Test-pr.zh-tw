---
title: '建立 UM 撥號對應表: Exchange Online Help'
TOCTitle: 建立 UM 撥號對應表
ms:assetid: 963ff2e1-515d-439a-953a-664174e5e283
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb123819(v=EXCHG.150)
ms:contentKeyID: 50473776
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.CreateUMDialPlanWizardForm.CreateUMDialPlanWizardPage
ms.translationtype: MT
---

# 建立 UM 撥號對應表

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-04-16_

整合通訊 (UM) 撥號對應表包含相關電話語音網路的組態資訊。UM 撥號對應表建立自己的信箱的語音信箱啟用的使用者的電話分機號碼從的連結。當您建立 UM 撥號對應表時，您可以設定的分機號碼、 統一資源識別元 (URI) 類型及語音的數字數目 over IP (VoIP) 撥號對應表的安全性設定。

每次您建立 UM 撥號對應表、 UM 信箱原則也會建立。UM 信箱原則命名為 \<*DialPlanName*\> 預設原則。

如需與 UM 撥號對應表相關的其他管理工作，請參閱 [UM 撥號對應表規劃程序](um-dial-plan-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：3 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 撥號對應表」項目。

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

## 使用 EAC 建立 UM 撥號對應表

1.  
    
    在 EAC 中，瀏覽至 **\[整合通訊\]** \> **\[UM 撥號對應表\]**，然後按一下 **\[新增\]**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

2.  在 **\[新增 UM 撥號對應表\]** 頁面上，完成下列方塊的資訊：
    
      - **名稱**  輸入撥號對應表的名稱。UM 撥號對應表名稱，則需要與必須是唯一的。不過，它只適用於 EAC 和命令介面中顯示。如果您有變更撥號對應表的顯示名稱建立之後，必須先刪除現有的 UM 撥號對應表並再建立另一個撥號對應具有適當的名稱。如果您的組織使用多個 UM 撥號對應表，我們建議您使用 UM 撥號對應表計劃的有意義的名稱。UM 撥號對應表名稱的最大長度是 64 個字元，而且它可以包含空格。不過，它不能包含任何下列字元："/ \\ \[\]:; |= , + \* ?\< \>。
        
        雖然您可以包含空格的 UM 撥號對應表名稱，如果您將與 Office Communications Server 2007 R2 或 Microsoft Lync Server 整合 \[整合通訊，但撥號對應表名稱不能包含空格。因此，如果您建立撥號對應表中的顯示名稱、 空格和您正在與 Office Communications Server 2007 R2 或 Lync Server 的整合，必須先刪除該站撥號並再建立另一個不在顯示名稱包含空格的撥號對應表。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>雖然名稱] 方塊中的撥號對應表可以接受 64 個字元，不能超過 49 個字元的撥號對應表名稱。如果您嘗試建立撥號對應表名稱包含多個 49 個字元，將會收到錯誤訊息。郵件會說因為 UM 撥號對應表名稱太長無法產生的 UM 信箱原則。這是因為、 如前所述，當您建立撥號對應表名稱為<em>&lt;DialPlanName&gt;</em>預設 UM 信箱原則也會建立預設原則。預設原則中的 15 個字元新增至撥號對應表的名稱、 時的總字元會超過此限制。兩者的<em>name</em>參數 UM 撥號對應表和 UM 信箱原則可以是 64 個字元。不過，若超過 49 個字元的撥號對應表名稱，預設的 UM 信箱原則的名稱會超過 64 個字元，而且這不允許系統。</td>
        </tr>
        </tbody>
        </table>
    
      - **擴充的長度 （位數）**  撥號對應表輸入數字數目。分機號碼的數字數目根據建立專用交換機 (PBX) 或 IP PBX 上的電話語音撥號。例如，如果使用者相關聯電話語音撥號對應表撥打四位數分機在相同的電話語音撥號呼叫另一位使用者，您選取 \[4 位數分機號碼。
        
        這是必填方塊，值的範圍為 1 到 20。一般分機號碼的長度為 3 到 7 碼。如果您現有的電話語音環境中包含分機號碼，則您指定的位數必須符合那些分機號碼的位數。
        
        當您建立工作階段初始通訊協定 (SIP) 或撥號對應表 E.164，並已啟用 UM 的使用者關聯撥號對應表時，您仍必須輸入分機號碼之使用者所使用。存取其信箱時Outlook語音存取使用者會使用此數字。
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(UI\_URI 類型)
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(UI\_VoIP 安全性)
    
      - **音訊語言**  使用這個清單來指定 Outlook 語音存取使用者所要使用的預設語言。此設定不會套用至在 UM 自動語音應答的語言設定。您可以設定 Outlook 語音存取設為相同或不同從已在 UM 自動語音應答使用的語言的語言。當使用者撥打電話至與撥號對應表連結的使用者時、 音訊語言是語音記錄運算子會使用的預設語言。來電者聽到的系統提示時會播放的相同語言。在 UM 撥號對應表選擇的語言來讀取電子郵件、 語音信箱和行事曆項目 ；以指出使用者的名稱如果個人問候語尚未被記錄;若要同時使用語音郵件預覽功能 ； 語音訊息與啟用才能正常運作的自動語音辨識 (ASR)。
    
      - **國家/地區碼**  使用此方塊可輸入要用於撥出電話的國家 （地區） 程式碼號碼。此號碼會加上等所撥打的電話號碼。此方塊可接受從 1 到 4 位數。例如，在美國、 國家/地區碼為 1。在英國，它的 44。

3.  按一下 **\[儲存\]**。

## 使用命令介面建立 UM 撥號對應表

此範例會建立一個使用四位數分機號碼的新 UM 撥號對應表，稱為 `MyUMDialPlan`。

    New-UMDialplan -Name MyUMDialPlan -NumberofDigits 4

此範例會建立一個使用五位數分機號碼且支援 SIP URI 的新 UM 撥號對應表，稱為 `MyUMDialPlan`。

    New-UMDialplan -Name MyUMDialPlan -UriType SIPName -NumberofDigits 5

