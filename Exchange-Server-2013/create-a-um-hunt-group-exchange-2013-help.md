---
title: '建立 UM 群組搜尋: Exchange Online Help'
TOCTitle: 建立 UM 群組搜尋
ms:assetid: 43ecb1ec-5f82-4516-9010-de8f954d3758
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa997679(v=EXCHG.150)
ms:contentKeyID: 50553973
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.CreateUMHuntGroupWizardForm.CreateUMHuntGroupWizardPage1
ms.translationtype: MT
---

# 建立 UM 群組搜尋

 

_<strong>適用版本：</strong> Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>上次修改主題的時間：</strong> 2013-04-16_

整合通訊 (UM) 群組搜尋是專用交換機 (PBX) 或 IP PBX 群組以邏輯方式呈現。連線或連結的 UM IP 閘道和 UM 撥號對應表扮演 UM 群組搜尋。


> [!NOTE]  
> 如果您在建立 UM IP 閘道時讓 UM 撥號對應表與 UM IP 閘道產生關聯，則還會建立 UM 搜尋群組。





> [!NOTE]  
> 如果您要變更 UM 群組搜尋設定，則必須刪除該群組搜尋，然後再建立另一個具有適當設定值的群組搜尋。




如需其他與 UM 群組搜尋相關的管理工作資訊，請參閱 [UM 群組搜尋的程序](https://docs.microsoft.com/zh-tw/exchange/voice-mail-unified-messaging/connect-voice-mail-system/um-hunt-group-procedures)。

## 開始之前有哪些須知？

  - 預估完成時間： 2 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 群組搜尋」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](https://docs.microsoft.com/zh-tw/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan)。

  - 執行這些程序之前，請確認已建立 UM IP 閘道器。如需詳細步驟，請參閱[建立 UM IP 閘道器](https://docs.microsoft.com/zh-tw/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-ip-gateway)。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。


> [!TIP]  
> 有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.




## 您要執行的工作

## 使用 EAC 建立 UM 群組搜尋

1.  在 EAC 中，瀏覽至 \[整合通訊\] \> \[UM 撥號對應表\]。在清單檢視中，選取您要修改的 UM 撥號對應表，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 <strong>\[UM 撥號對應表\]</strong> 頁面的 <strong>\[UM 群組搜尋\]</strong> 下，按一下 <strong>\[新增\]</strong>![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

3.  在 <strong>\[新增 UM 群組搜尋\]</strong> 頁面上，輸入下列資訊：
    
      - \[名稱\]   使用此方塊可建立 UM 群組搜尋的顯示名稱。UM 群組搜尋名稱是必要項目，而且必須是唯一的，但是，它只能在 EAC 和命令介面中作為顯示用途。如果您在建立群組搜尋之後，必須變更其顯示名稱，則必須先刪除現有的群組搜尋，然後再建立另一個具有適當名稱的群組搜尋。
        
        如果您的組織使用多個群組搜尋，建議為您的群組搜尋使用有意義的名稱。UM 群組搜尋名稱的長度上限是 64 個字元，且可以包含空格。不過不可包含下列任何一個字元：" / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - <strong>UM IP 閘道器</strong>  使用此方塊可指定要使用的 UM IP 閘道。按一下以選取 UM IP 閘道器的 \[<strong>瀏覽\]</strong>及 \[<strong>確定\]</strong>。
    
      - <strong>引導識別碼</strong>   使用此方塊可指定一個字串，以唯一識別 PBX 或 IP PBX 上所設定的引導識別碼。
        
        您可以在此方塊中使用分機號碼，或使用工作階段初始通訊協定 (SIP) 統一資源識別碼 (URI)。此方塊可接受英數字元。若為傳統 PBX，則會使用數值來作為引導識別碼。不過，有些 IP PBX 可以使用 SIP URI。

4.  
    
    按一下 \[儲存\]。

## 使用命令介面來建立 UM 群組搜尋

此範例會建立引導識別碼為 12345 且名為 `MyUMHuntGroup` 的 UM 群組搜尋。

    New-UMHuntGroup -Name MyUMHuntGroup -PilotIdentifier 12345 -UMDialplan MyUMDialPlan -UMIPGateway MyUMIPGateway

此範例會建立有多個引導識別碼且名為 `MyUMHuntGroup` 的 UM 群組搜尋。

    New-UMHuntGroup -Name MyUMHuntGroup -PilotIdentifier 5551234,55555 -UMDialplan MyUMDialPlan -UMIPGateway MyUMIPGateway

