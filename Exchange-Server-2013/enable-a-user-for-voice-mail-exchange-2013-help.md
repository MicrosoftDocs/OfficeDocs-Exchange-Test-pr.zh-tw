---
title: '啟用使用者的語音信箱: Exchange Online Help'
TOCTitle: 啟用使用者的語音信箱
ms:assetid: ad027767-5e14-4cb1-9f8a-0791d9188db5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124147(v=EXCHG.150)
ms:contentKeyID: 50473977
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.EnableUnifiedMessagingWizardForm.EnableUnifiedMessagingWizardPage
ms.translationtype: MT
---

# 啟用使用者的語音信箱

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-22_

當您啟用使用者的整合通訊 (UM) 時，一組預設屬性套用至使用者和使用者將能夠使用整合通訊所含的語音信箱功能。啟用使用者的語音信箱後，您必須新增使用者工作階段初始通訊協定 (SIP) 位址如果它們指派給 UM 信箱原則連結至 SIP URI 撥號對應表的選項。或者，您可以將 E.164 號碼之使用者如果它們指派給 UM 信箱原則連結至撥號對應表 E.164。在這兩種情況下，使用者仍必須設定分機號碼。

需要與電話分機號碼、 SIP 統一資源識別元 (URI) 或 E.164 撥號對應表關聯每位使用者的分機號碼。分機號碼必須是正確的號碼的數字，指定在 UM 撥號對應表的 UM 信箱原則。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您必須新增、 移除或修改所有已啟用 UM 之使用者的分機號碼使用 EAC 或命令介面中，即使其所連結的 SIP URI 或撥號對應表 E.164。若要新增、 移除或修改 SIP 位址或使用者的 E.164 號碼、 您需要使用命令介面，因為這些選項不適用於 live @ EAC。</td>
</tr>
</tbody>
</table>


如需與啟用語音信箱之使用者相關的其他管理工作，請參閱[擁有郵件功能的語音使用者程序](voice-mail-enabled-user-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 信箱」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

  - 執行這些程序之前，請確認已建立 UM 信箱原則。如需詳細步驟，請參閱[建立 UM 信箱原則](create-a-um-mailbox-policy-exchange-2013-help.md)。

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

## 使用 EAC 來啟用使用者的語音信箱

1.  在 EAC 中，按一下 \[收件者\]。

2.  在 \[清單\] 檢視中，選取您要對於整合通訊啟用信箱的使用者。

3.  在 \[詳細資料\] 窗格中，於 \[電話和語音功能\] 下方，按一下 \[啟用\]。

4.  在 **\[啟用 UM 信箱\]** 頁面上，按一下 **\[UI 信箱原則\]** 旁邊的 **\[瀏覽\]** 按鈕，從清單中找出 UM 信箱原則以便指派使用者，然後按一下 **\[確定\]**。

5.  在 \[啟用 UM 信箱\] 頁面上，完成下列方塊：
    
      - **SIP 位址**或**E.164 號碼**的**SIP 位址**或**E.164 號碼**\] 文字方塊中，輸入使用者的 SIP 位址或 E.164 號碼。當您啟用整合通訊的使用者指派給 UM 信箱原則連結至 \[SIP URI\] 或 \[撥號對應表 E.164 則這些選項。您無法新增的 SIP 位址或使用者的 E.164 號碼如果使用者是與電話分機撥號對應表相關聯。
        
        當您將使用者指派給 UM 信箱原則連結至 SIP URI 或撥號對應表 E.164 時，您必須輸入使用者的分機號碼。當存取其信箱透過Outlook語音存取使用者會使用此分機號碼。您在此方塊中設定的數字數目必須符合的 SIP URI 上設定的數字數目或撥號對應表 E.164。
    
      - **分機號碼**   使用此文字方塊可針對您要其啟用 UM 的使用者，手動輸入分機號碼。
        
        您必須為使用者提供有效的分機號碼和必須符合撥號對應表上指定的數字數目。您只可以輸入數字 1 到 20。典型的分機號碼是 3 到 7 位數字長。連結至 UM 信箱原則指派給使用者的撥號對應表上設置分機中的數字數目。
    
      - 在 \[PIN 碼設定\] 底下，完成下列操作：
        
          - **自動產生的 PIN**  按一下此按鈕可自動產生用於透過 Outlook 語音存取語音信箱存取已啟用 UM 之使用者的 PIN。這是預設設定。PIN 會自動產生 PIN 原則指派給使用者的 UM 信箱原則上設定為基礎。使用此設定可協助保護使用者的 PIN。PIN 傳送給他們收到之後他們正在啟用 UM 的歡迎訊息中的使用者。根據預設，他們必須先登入他們的信箱若要取得其語音信箱時變更此 PIN。
        
          - **類型 PIN**  按一下此按鈕可輸入使用者用以存取語音信箱系統的 pin 碼。PIN 必須符合在已啟用 UM 的使用者相關聯的 UM 信箱原則上設定 PIN 原則設定。例如，如果 UM 信箱原則設定為接受包含七個或多個字的 Pin，您在此方塊中輸入的 pin 碼必須至少七位數字的 long。
        
          - **要求使用者第一次登入時必須重設 PIN 碼**   選取此核取方塊可強制使用者第一次從電話使用 Outlook Voice Access 存取語音信箱系統時，重設其語音信箱 PIN 碼。系統會提示使用者輸入他們更熟悉的 PIN 碼。這種安全性最佳實務可強制啟用 UM 的使用者在第一次登入時變更 PIN 碼，有助於防範未經授權而存取使用者的資料和收件匣。預設會選取此核取方塊。

6.  在 \[**啟用 UM 信箱**\] 頁面上檢閱您的設定。按一下 \[**完成**\] 以啟用使用者的語音信箱。按一下 \[**備份**進行組態變更。

## 使用命令介面來啟用使用者的語音信箱

此範例會針對 tonysmith@contoso.com 這個信箱啟用整合通訊、將分機號碼設定為 51234、將使用者的 PIN 碼設定為 5643892，並將使用者指派到名稱為 `MyUMMailboxPolicy` 的 UM 信箱原則。

    Enable-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy -Extensions 51234 -PIN 5643892 -PINExpired $true

此範例會針對 tonysmith@contoso.com 這個信箱啟用整合通訊、將使用者指派到名稱為 `MyUMMailboxPolicy` 的 UM 信箱原則，並設定使用者的分機號碼、SIP 位址及 PIN 碼。

    Enable-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy -Extensions 51234 -PIN 5643892 -SIPResourceIdentifier "tonysmith@contoso.com" -PINExpired $true

