---
title: '建立 UM 自動語音應答: Exchange Online Help'
TOCTitle: 建立 UM 自動語音應答
ms:assetid: 773f53fb-d80f-4a79-8bd3-bd753942489f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa998875(v=EXCHG.150)
ms:contentKeyID: 50473526
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.UnifiedMessaging.CreateAutoAttendantWizardForm.CreateAutoAttendantWizardPage
ms.translationtype: MT
---

# 建立 UM 自動語音應答

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-03-08_

建立整合通訊 (UM) 自動語音應答後，由總機接聽人工運算子的外部電話號碼的來電會由自動語音應答接聽電話。不同於其他的整合通訊元件，例如 UM 撥號對應表計劃及 UM IP 閘道器\] 中，您不需要建立 UM 自動語音應答。但是，自動語音應答協助內部及外部來電者尋找使用者或部門的組織中存在，將來電轉接至它們。

如需與 UM 自動語音應答相關的其他管理工作，請參閱[UM 自動語音應答程序](um-auto-attendant-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：3 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 自動語音應答」項目。

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

## 使用 EAC 來建立 UM 自動語音應答

1.  
    
    在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]，選擇要新增自動應答的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 \[ **UM 撥號對應表**\] 頁面的 \[ **UM 自動語音應答**，按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

3.  在 \[**新增 UM 自動語音應答**\] 頁面上輸入下列資訊：
    
      - **名稱**   使用此方塊可建立 UM 自動語音應答的顯示名稱。UM 自動語音應答名稱是必要項目，而且必須是唯一的。但是，它只能在 EAC 和命令介面中作為顯示用途。
        
        如果您在建立自動語音應答後必須變更其顯示名稱，必須先刪除現有的 UM 自動語音應答，然後建立另一個具有適當名稱的自動語音應答。如果您的組織使用多個自動語音應答，則建議為 UM 自動語音應答使用有意義的名稱。UM 自動語音應答名稱的最大長度為 64 個字元，可以包含空格。
        
        雖然您可以將如果將整合通訊整合與 Office Communications Server 2007 R2 或 Microsoft Lync Server 名稱包含空格，新增 UM 自動語音應答、 自動語音應答的名稱不能包含空格。因此，如果您建立自動語音應答有空格的顯示名稱，且您正在與 Office Communications Server 2007 R2 或 Lync Server 的整合，您必須先刪除該自動語音應答並再建立另一個不在顯示名稱包含空格的自動語音應答。
    
      - **建立此自動語音應答為已啟用**  選取此核取方塊以啟用自動語音應答接聽來電時您完成 \[新增 UM 自動語音應答\] 精靈。預設為停用建立新的自動語音應答。
        
        如果您決定建立 UM 自動語音應答為停用，您可以使用 EAC 或命令介面來完成精靈之後啟用自動語音應答。
    
      - \[設定自動應答以回應語音指令\]   選擇此核取方塊以啟用自動語音應答的語音功能。若啟用自動語音應答的語音功能，來電者可使用撥號音或語音輸入，來回應 UM 自動語音應答所使用的系統或自訂提示。依預設，在建立自動語音應答時不會啟用語音。
        
        若要使用已啟用語音的自動語音應答的來電者，您必須安裝適當的 UM 語言套件包含自動語音辨識 (ASR) 支援和設定要使用這種語言的自動語音應答的內容。
    
      - **存取號碼**  使用此方塊可輸入分機號碼或來電者會使用自動語音應答的電話號碼。在 \[\] 方塊中輸入分機號碼\] 或 \[電話號碼，然後按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")新增至清單的數目。分機號碼或您所提供的電話號碼的數字數目沒有要比對的分機號碼相關聯的 UM 撥號對應表上設定的數字數目。這是因為 UM 自動語音應答允許直接來電。
        
        分機號碼或輸入的電話號碼的數字為 unlimited。不過，您可能會建立新的自動語音應答沒有列出分機號碼。分機號碼\] 或 \[電話號碼並非必要。
        
        您可以編輯或移除現有的分機號碼或電話號碼。若要編輯現有的分機號碼或電話號碼，請按一下 \[**編輯**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。若要從清單中移除現有的分機號碼或電話號碼，按一下 \[**移除**![\[移除\] 圖示](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[移除] 圖示")。

4.  按一下 **\[儲存\]**。

## 使用命令介面來建立 UM 自動語音應答

此範例會建立名為 `MyUMAutoAttendant` 的 UM 自動語音應答，它可以接受來電但是未啟用語音。

    New-UMAutoAttendant -Name MyUMAutoAttendant -UMDialPlan MyUMDialPlan -PilotIdentifierList 55000 -Enabled $false

此範例會建立名為 `MyUMAutoAttendant` 且已啟用語音的 UM 自動語音應答。

    New-UMAutoAttendant -Name MyUMAutoAttendant -UMDialPlan MyUMDialPlan -PilotIdentifierList 56000,56100 -SpeechEnabled $true

