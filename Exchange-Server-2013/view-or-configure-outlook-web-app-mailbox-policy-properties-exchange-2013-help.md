---
title: '檢視或設定 Outlook Web App 信箱原則屬性: Exchange Online Help'
TOCTitle: 檢視或設定 Outlook Web App 信箱原則屬性
ms:assetid: be012ffe-8fdb-4fb7-aebd-78b3a55593fa
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd351097(v=EXCHG.150)
ms:contentKeyID: 50474141
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 檢視或設定 Outlook Web App 信箱原則屬性

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2016-04-13_

建立Outlook Web App信箱原則之後，您可以設定各種選項來控制使用者Outlook Web App中可用的功能。例如，您可以啟用或停用收件匣規則或建立允許的附件檔案類型清單。

## 開始之前有哪些須知？

  - 完成每項程序預估時間： 3 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [用戶端和行動裝置權限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主題中的「Outlook Web App 信箱原則」項目。

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

## 使用 EAC 檢視或設定 Outlook Web App 信箱原則

1.  在系統管理中心中，按一下 \[權限\] \> \[Outlook Web App 原則\]。

2.  在結果窗格中，按一下以選取您要檢視或設定的信箱原則。

3.  按一下 \[編輯\] 按鈕。

4.  
    
    在 \[一般\] 索引標籤上，您可以檢視與編輯原則的名稱。

5.  
    
    在 \[**功能**\] 索引標籤上使用\] 核取方塊以啟用或停用功能。根據預設，會顯示最常見的功能。如需可啟用或停用的所有功能，請按一下 \[**更多選項**\]。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>功能設定為Outlook Web App信箱原則會覆寫Outlook Web App虛擬目錄設定。您可以在命令介面中使用<strong>Set-CASMailbox</strong>指令程式變更個別使用者區隔的設定。</td>
    </tr>
    </tbody>
    </table>


6.  
    
    在 \[**檔案存取**\] 索引標籤上使用**直接檔案存取**\] 核取方塊來設定檔案存取和檢視使用者的選項。檔案存取可讓使用者開啟或檢視檔案附加至電子郵件的內容。
    
    檔案存取可以根據使用者登入的公用或私人電腦上是否加以控制。只有當您使用表單型驗證時使用的使用者選取 \[私人電腦存取或公用電腦存取選項。其他所有形式的驗證會預設為私人電腦存取。

7.  在 \[離線存取\] 索引標籤上，使用選項按鈕設定離線存取可用性。

8.  按一下 \[儲存\] 以更新原則。

## 使用命令介面來設定 Outlook Web App 信箱原則

此範例會在預設信箱原則中啟用行事曆存取功能。

    Set-OwaMailboxPolicy -Identity Default -CalendarEnabled $true

如需語法及參數的相關資訊，請參閱 [Set-OwaMailboxPolicy](https://technet.microsoft.com/zh-tw/library/dd297989\(v=exchg.150\))。

## 使用命令介面來檢視 Outlook Web App 信箱原則

此範例會擷取組織 `Executives` 中的Outlook Web App 信箱原則 `Fabrikam` 的內容。

    Get-OwaMailboxPolicy -Identity Fabrikam\Executives

如需語法及參數的相關資訊，請參閱 [Get-OwaMailboxPolicy](https://technet.microsoft.com/zh-tw/library/dd351095\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要確認是否已成功編輯 Outlook Web App 信箱原則：

1.  在 EAC 中，按一下 **\[權限\]** \> **\[Outlook Web App 原則\]**，然後選擇特定的 Outlook Web App 信箱原則。

2.  按一下 \[編輯\] 按鈕來檢視信箱原則的內容。

3.  按一下 \[儲存\] 或 \[取消\] 關閉內容頁面。

