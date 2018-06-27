---
title: '建立保留原則: Exchange Online Help'
TOCTitle: 建立保留原則
ms:assetid: d8806c98-fea5-492f-906d-f514e25361b2
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ150573(v=EXCHG.150)
ms:contentKeyID: 50474341
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 建立保留原則

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

在Exchange Online和Exchange Server 2013，您可以使用保留原則來管理電子郵件生命週期。建立保留標記、 將它們新增至保留原則，並將原則套用到信箱使用者套用保留原則。

以下是教您如何建立保留原則並將其套用到信箱中Exchange Online[視訊](https://go.microsoft.com/fwlink/?linkid=825854)問題。

與保留原則相關的其他管理工作，請參閱[通訊記錄管理程序](messaging-records-management-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 完成此工作的預估時間：30 分鐘。

  - 本主題中的程序需要特定權限。請查看每個程序以取得權限資訊。

  - 您套用保留原則的信箱必須位於Exchange Server 2010或更新版本的伺服器。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

## 該怎麼做？

## 步驟 1： 建立保留標記

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中 「 郵件記錄管理 」 的項目。

**使用 EAC 來建立保留標記**

1.  瀏覽至 \[**相符性管理**\>**保留標記**，然後按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")

2.  選取下列其中一個選項：
    
      - **自動適整個信箱 （預設值）**  選取此選項可建立預設原則標記 (DPT)。您可以使用 dpt 套用建立預設刪除與預設封存原則，它會套用至信箱中的所有項目。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>您無法使用 EAC 建立 DPT 刪除語音信箱項目。如需如何建立 DPT 刪除語音信箱項目相關的詳細資訊，請參閱下面的命令介面範例。</td>
        </tr>
        </tbody>
        </table>
    
      - **Applied 自動至特定資料夾**  選取此選項可建立保留原則標記 （印） 如**收件匣**或**刪除的郵件**的預設資料夾。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>您僅可建立 Rpt 搭配 [<strong>刪除並允許復原</strong>或 [<strong>永久刪除</strong>] 動作。</td>
        </tr>
        </tbody>
        </table>
    
      - **Applied 由使用者的項目和資料夾 （個人）**  選取此選項可建立個人標記。這些標記允許Outlook和Outlook Web App使用者封存或刪除設定套用到一則訊息或不同設定套用到上層資料夾或整個信箱的資料夾。

3.  **新的保留標記**\] 頁面上標題和選項目視您所選取的標籤的類型。完成以下欄位：
    
      - **名稱**  輸入保留標記的名稱。標籤名稱僅供顯示與資料夾或項目標籤套用至不造成任何影響。請考慮在佈建使用者的個人標記可用Outlook和Outlook Web App中。
    
      - **套用此標籤下的預設資料夾**  此選項是只有當您選取 \[**自動適在特定的資料夾**。
    
      - **保留動作**  選取其中一個項目大小達到其保留期間之後所要採取下列動作：
        
          - **刪除並允許復原**  選取要刪除的項目，但允許使用者在 Outlook 中使用 \[**復原刪除的項目**\] 選項進行復原此動作或 Outlook Web app 項目，直到到達設定的信箱資料庫或信箱使用者的已刪除的項目保留期間會保留。
        
          - **永久刪除**  選取此選項可永久刪除信箱資料庫中的項目。
            
            <table>
            <thead>
            <tr class="header">
            <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
            </tr>
            </thead>
            <tbody>
            <tr class="odd">
            <td>會保留與就地 eDiscovery 搜尋中傳回信箱或受限於就地保留或訴訟保留項目。深入了解，請參閱 ＜ <a href="in-place-hold-and-litigation-hold-exchange-2013-help.md">就地保留與訴訟暫止</a>。</td>
            </tr>
            </tbody>
            </table>
        
          - **移至封存**  只有當您建立 DPT 或個人標記為此巨集指令。選取 \[將項目移至使用者的就地封存此巨集指令。
    
      - **保留期間**  選取下列選項之一：
        
          - **永不**  選取此選項即可指定絕對不應刪除或移到封存的項目。
        
          - **當項目達到下列年齡 （天數）**  選取這個選項，並指定要保留的項目之前他們正在移動或刪除的天數。行事曆和任務以外的所有受支援項目保留期間被計算日期接收或建立項目。結束日期為計算的行事曆及工作項目保留期間。
    
      - **註解**  使用者輸入的任何系統管理附註解此選用\] 欄位。欄位不會對使用者顯示。

**使用命令介面來建立保留標記**

使用**New-RetentionPolicyTag**指令程式來建立保留標記。此指令程式中可用的不同選項可讓您建立不同類型的保留標記。若要建立 DPT (`All`) 印使用*Type*參數 （指定預設資料夾類型，例如`Inbox`） 或個人標記 (`Personal`)。

此範例會建立 DPT 7 年 （2,556 天） 後刪除信箱中的所有郵件。

    New-RetentionPolicyTag -Name "DPT-Corp-Delete" -Type All -AgeLimitForRetention 2556 -RetentionAction DeleteAndAllowRecovery

此範例會建立 DPT 中 2 年 （730 天） 將所有郵件移至就地封存。

    New-RetentionPolicyTag -Name "DPT-Corp-Move" -Type All -AgeLimitForRetention 730 -RetentionAction MoveToArchive

此範例會建立 20 天後刪除語音郵件訊息的 DPT。

    New-RetentionPolicyTag -Name "DPT-Corp-Voicemail" -Type All -MessageClass Voicemail -AgeLimitForRetention 20 -RetentionAction DeleteAndAllowRecovery

此範例會建立印永久刪除垃圾郵件\] 資料夾中的郵件 30 天後。

    New-RetentionPolicyTag -Name "RPT-Corp-JunkMail" -Type JunkEmail -AgeLimitForRetention 30 -RetentionAction PermanentlyDelete

此範例會建立個人標記永不刪除訊息。

    New-RetentionPolicyTag -Name "Never Delete" -Type Personal -RetentionAction DeleteAndAllowRecovery -RetentionEnabled $false

## 步驟 2：建立保留原則

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中 「 郵件記錄管理 」 的項目。

**使用 EAC 來建立保留原則**

1.  瀏覽至 \[**相符性管理**\>**保留原則**，然後按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")

2.  在**新的保留原則**中，完成下列欄位：
    
      - **名稱**  輸入保留原則的名稱。
    
      - **保留標記**  按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")以選取您想要新增至此保留原則的標記。
        
        保留原則可包含下列標籤：
        
          - 搭配 **\[移至封存\]** 動作的一個 DPT
        
          - 一個 DPT，搭配 \[刪除並允許復原\] 或 \[永久刪除\] 動作
        
          - 一個 DPT，適用於搭配 \[刪除並允許復原\] 或 \[永久刪除\] 動作的語音信箱訊息
        
          - 一個 rpt，適每例如刪除項目的**收件匣**\] 預設資料夾
        
          - 任意數目的個人標記
            
            <table>
            <thead>
            <tr class="header">
            <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
            </tr>
            </thead>
            <tbody>
            <tr class="odd">
            <td>雖然您可以將任何數目的個人標記新增至保留原則，有許多的個人標記使用不同的保留設定可能會混淆使用者。建議您將不超過十個個人標記連結到的保留原則。</td>
            </tr>
            </tbody>
            </table>
        
        您可以建立保留原則不透過新增任何保留標記，但將不會移動或刪除的信箱要套用該原則中的項目。您也可以新增和保留原則中移除保留標記會在建立之後。

**使用命令介面來建立保留原則**

本範例會建立保留原則 Retentionpolicy-corp 套用和使用*RetentionPolicyTagLinks*參數來建立關聯至原則五名標記。

    New-RetentionPolicy "RetentionPolicy-Corp"  -RetentionPolicyTagLinks "DPT-Corp-Delete","DPT-Corp-Move","DPT-Corp-Voicemail","RPT-Corp-JunkMail","Never Delete"

如需詳細的語法及參數資訊，請參閱 [New-RetentionPolicy](https://technet.microsoft.com/zh-tw/library/dd297970\(v=exchg.150\))。

## 步驟 3： 將保留原則套用至信箱使用者

建立保留原則之後，必須將其套用至信箱使用者中。您可以將不同的保留原則套用至不同的一組使用者。如需詳細指示，請參閱[將保留原則套用至信箱](apply-a-retention-policy-to-mailboxes-exchange-2013-help.md)。

## 如何才能了解此工作是否正常運作？

在建立保留標記、 將其新增至保留原則，並將原則套用到信箱使用者之後下, 一次 MRM 的信箱助理員處理的信箱，郵件所移動或刪除根據中設定設定您的保留標記。

確認您已套用保留原則，請執行下列動作：

1.  執行下列命令介面命令，以針對單一信箱手動執行 MRM 小幫手。
    
        Start-ManagedFolderAssistant -Identity <mailbox identity>

2.  登入使用Outlook或Outlook Web App信箱並確認郵件已刪除或移至封存符合原則設定。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>

