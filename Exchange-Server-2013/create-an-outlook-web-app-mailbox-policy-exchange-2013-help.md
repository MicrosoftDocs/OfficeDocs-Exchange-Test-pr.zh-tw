---
title: '建立 Outlook Web App 信箱原則: Exchange Online Help'
TOCTitle: 建立 Outlook Web App 信箱原則
ms:assetid: 347207fa-cfb7-40a6-b19a-831dcdb54ad5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd335191(v=EXCHG.150)
ms:contentKeyID: 50472949
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 建立 Outlook Web App 信箱原則

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2013-05-30_

您可以建立 Outlook Web App 信箱原則來套用一組共通的原則設定。Outlook Web App 信箱原則在套用與標準化特定使用者群組的設定時相當實用，例如使用者特定群組的附件設定。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此指令程式。雖然這個指令程式的所有參數都已列於本主題中，不過，如果某些參數並未包含在指派給您的權限中，您可能就無法存取這些參數。若要查看您需要的權限，請參閱 [用戶端和行動裝置權限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主題中的「Outlook Web App 信箱原則」項目。

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

## 使用 EAC 建立 Outlook Web App 信箱原則

1.  在系統管理中心中，按一下 \[權限\] \> \[Outlook Web App 原則\]。

2.  按一下 **\[新增\]** 按鈕。

3.  
    
    輸入原則的名稱。

4.  
    
    使用核取方塊來啟用或停用功能。最常用的功能預設為顯示。若要查看所有可啟用或停用的功能，請按一下 \[其他選項\]。
    
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


5.  按一下 \[儲存\] 以儲存原則。

## 使用命令介面建立 Outlook Web App 信箱原則

範例會建立 Outlook Web App 名為 `Policy1` 的信箱原則。

  - 在命令介面中，執行下列命令。
    
        New-OwaMailboxPolicy -Name Policy1

如需詳細的語法及參數的詳細資訊，請參閱[New-OwaMailboxPolicy](https://technet.microsoft.com/zh-tw/library/dd351067\(v=exchg.150\))。如需使用命令介面來設定Outlook Web App信箱原則的詳細資訊，請參閱[Set-OwaMailboxPolicy](https://technet.microsoft.com/zh-tw/library/dd297989\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要確定您已成功建立Outlook Web App信箱原則：

  - 在 EAC 中按一下 \[權限\] \>\[Outlook Web App 原則\] ，然後尋找新的信箱原則。

