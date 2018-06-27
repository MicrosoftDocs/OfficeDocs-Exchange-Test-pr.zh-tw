---
title: '管理使用者的語音郵件設定: Exchange Online Help'
TOCTitle: 管理使用者的語音郵件設定
ms:assetid: 73957938-048a-4f9c-bd0f-a3c2c3dcd638
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa998851(v=EXCHG.150)
ms:contentKeyID: 50473488
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理使用者的語音郵件設定

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2013-02-22_

您可以檢視或設定整合通訊 (UM) 和語音信箱功能及使用者已啟用 UM 和語音信箱的組態設定。例如，您可以執行下列動作：

  - 重設其 Outlook Voice Access 的 PIN 碼。

  - 新增個人操作員分機號碼。

  - 新增其他分機號碼。

  - 啟用或停用自動語音辨識 (ASR)。

  - 啟用或停用自動答錄規則。

  - 啟用或停用他們的電子郵件或行事曆存取功能。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>部分設定與功能只能透過命令介面進行設定。</td>
</tr>
</tbody>
</table>


如需與啟用語音信箱之使用者相關的其他管理工作，請參閱[擁有郵件功能的語音使用者程序](voice-mail-enabled-user-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [整合的通訊權限](unified-messaging-permissions-exchange-2013-help.md)主題中的「UM 信箱」項目。

  - 在執行這些程序之前，請確認已建立 UM 撥號對應表。如需詳細步驟，請參閱[建立 UM 撥號對應表](create-a-um-dial-plan-exchange-2013-help.md)。

  - 執行這些程序之前，請確認已建立 UM 信箱原則。如需詳細步驟，請參閱[建立 UM 信箱原則](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 執行這些程序之前，請確認現有使用者目前已啟用整合通訊。如需詳細步驟，請參閱[啟用使用者的語音信箱](enable-a-user-for-voice-mail-exchange-2013-help.md)。

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

## 使用 EAC 來檢視或設定啟用 UM 功能之使用者的內容

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[信箱\]。

2.  在清單檢視中，選擇您要變更 UM 信箱原則的信箱。

3.  在詳細資料窗格中的 \[電話與語音功能\] \> \[整合通訊\] 下方，按一下 \[檢視詳細資料\]。

4.  在 \[UM 信箱\] 頁面上，按一下 \[UM 信箱設定\] 以檢視或變更現有已啟用 UM 功能之使用者的下列 UM 內容：
    
      - **PIN 狀態**  此僅供顯示欄位會顯示使用者的信箱狀態。根據預設，當使用者已啟用 UM 的 PIN 狀態被列為**出未鎖定**。不過，如果使用者已輸入正確Outlook語音存取 PIN 多次，狀態被列為**鎖定取出**。
    
      - **UM 信箱原則**   此方塊可顯示與啟用 UM 的使用者相關聯的 UM 信箱原則名稱。您可以按一下 **\[瀏覽\]**，尋找並指定要與此 UM 信箱相關聯的 UM 信箱原則。
    
      - \[個人操作員分機號碼\]   使用這個方塊來指定使用者的操作員分機號碼。依預設，不會設定分機號碼。分機號碼的長度可以從 1 個到 20 個字元。這樣可讓已啟用 UM 之使用者的來電轉送到您在此方塊中指定的分機號碼。
        
        您可以在撥號對應表和自動語音應答上設定其他類型的操作員分機號碼。不過，這些副檔名通常原本用意是全公司接待員或運算子。當行政助理或個人助理接聽來電之前他們正在接聽電話的特定使用者無法使用個人操作員分機設定。

5.  在 \[UM 信箱\] 頁面上的 \[其他分機\] 下方，您可以新增、變更與檢視使用者的分機號碼。
    
      - 若要新增分機號碼，按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。在 \[新增其他分機\] 頁面上，使用 \[瀏覽\] 來選取 UM 撥號對應表，接著在 \[分機號碼\] 方塊中輸入分機號碼。
    
      - 若要移除分機號碼，選取您想要移除的分機號碼，接著按一下 \[移除\]![\[移除\] 圖示](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[移除] 圖示")。

6.  如果您做了任何變更，請按一下 \[儲存\]。

## 使用命令介面為已啟用 UM 功能的使用者設定功能

此範例會停用「在電話上播放」和未接來電通知，但是會啟用簡訊 (SMS) 通知。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>內部部署和混合式部署中，當您正在整合 Unified Messaging 和 Lync Server 服務未接來電通知都無法提供具有信箱位於 Exchange 2007 或 Exchange 2010 信箱伺服器上的使用者。當使用者中斷通話傳送至信箱伺服器之前，會產生未接的來電通知。</td>
</tr>
</tbody>
</table>


    Set-UMMailbox -Identity tony@contoso.com -UMEnabled $true -UMMailboxPolicy AdminPolicy -MissedCallNotificationEnabled $false -PlayonPhoneEnabled $false -SMSMessageWaitingNotificationEnabled $true

此範例會讓使用者在使用 Outlook 語音存取時無法存取行事曆，但可存取電子郵件。

    Set-UMMailbox -Identity tony@contoso.com -UMEnabled $true -UMMailboxPolicy AdminPolicy -Extension 523456 -FAXEnabled $true -TUIAccessToCal $false -TUIAccessToEmail True

此範例會讓使用者在使用 Outlook 語音存取時無法存取行事曆及電子郵件。

    Set-UMMailbox -Identity tony@contoso.com -TUIAccessToCalendarEnabled $false -TUIAccessToEmailEnabled $false

此範例可防止使用者建立自動答錄規則、接收傳入的傳真與使用 Outlook 語音存取功能，但是會啟用自動語音辨識 (ASR)。

    Set-UMMailbox -Identity tony@contoso.com -AutomaticSpeechRecognitionEnabled $true -CallAnsweringRulesEnabled $false -FaxEnabled $false -SubscriberAccessEnabled $false 

## 使用命令介面來檢視啟用 UM 之使用者的內容

本範例以格式化清單的方式顯示樹系中所有啟用 UM 功能的信箱清單。

    Get-UMMailbox | Format-List

本範例顯示 tonysmith@contoso.com 的 UM 信箱內容。

    Get-UMMailbox -Identity tonysmith@contoso.com

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您正在執行 Exchange 2007 和 Exchange 2013 和使用者的信箱位於 Exchange 2007 信箱執行<strong>Get-UMMailbox</strong>指令程式的伺服器將無法正常運作。若要解決此問題，請從 Exchange 2007 伺服器或執行 Exchange 2007 系統管理工具的電腦執行<strong>Get-UMMailbox</strong>指令程式。</td>
</tr>
</tbody>
</table>

