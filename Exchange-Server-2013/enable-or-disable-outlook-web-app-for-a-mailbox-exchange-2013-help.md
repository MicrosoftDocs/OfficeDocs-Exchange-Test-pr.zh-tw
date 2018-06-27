---
title: '啟用或停用 Outlook Web App 信箱: Exchange Online Help'
TOCTitle: 啟用或停用 Outlook Web App 信箱
ms:assetid: abc19646-6211-4f18-a060-e347452dcc53
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124124(v=EXCHG.150)
ms:contentKeyID: 50554074
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟用或停用 Outlook Web App 信箱

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2012-11-14_

您可以使用 EAC 或命令介面啟用或停用Outlook Web App使用者信箱。啟用Outlook Web App時，使用者可以使用Outlook Web App傳送及接收電子郵件。如果Outlook Web App已停用、 信箱會繼續以接收電子郵件使用者可以存取它傳送及接收電子郵件使用 MAPI 用戶端，例如 Microsoft Outlook 或使用 POP 或 IMAP 電子郵件用戶端，假設信箱的已啟用以支援存取這些用戶端。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>建立使用者信箱時，預設會啟用對 Outlook Web App 及 MAPI、POP3 和 IMAP4 電子郵件用戶端的支援。</td>
</tr>
</tbody>
</table>


其他管理電子郵件用戶端存取信箱的相關管理工作，請參閱下列主題：

  - [啟用或停用信箱的 MAPI](enable-or-disable-mapi-for-a-mailbox-exchange-online-help.md)

  - [啟用或停用使用者的 IMAP4 存取](enable-or-disable-imap4-access-for-a-user-exchange-2013-help.md)

  - [啟用或停用使用者的 POP3 存取](enable-or-disable-pop3-access-for-a-user-exchange-2013-help.md)

## 開始之前有哪些須知？

  - 預估完成時間： 2 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [用戶端和行動裝置權限](clients-and-mobile-devices-permissions-exchange-2013-help.md) 主題中的「用戶端存取使用者設定」項目。

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

## 使用 EAC 啟用或停用 Outlook Web App

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[信箱\]。

2.  在使用者信箱清單中，按一下您想啟用或停用 Outlook Web App 的信箱，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在信箱內容頁面上，按一下 \[信箱功能\]。

4.  在 \[電子郵件連線\] 下，執行下列其中一項操作：
    
      - \[停用Outlook Web App、 **Outlook Web App ︰ 已啟用**，按一下 \[**停用**。
        
        如果您確定要停用Outlook Web App警告詢問。按一下 \[**是\]**。
    
      - \[啟用Outlook Web App、 **Outlook Web App ︰ 已停用**，按一下 \[**啟用**\]。

5.  按一下 \[儲存\] 儲存您的變更。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您可以啟用及使用 EAC 大量編輯功能停用Outlook Web App多個使用者信箱。如需如何執行這項作業的詳細資訊，請參閱 「 大量編輯使用者信箱 」 一節中<a href="manage-user-mailboxes-exchange-2013-help.md">管理使用者信箱</a>。</td>
</tr>
</tbody>
</table>


## 使用命令介面啟用或停用 Outlook Web App

此範例會停用 Yan Li 信箱的 Outlook Web App。

    Set-CASMailbox -Identity "Yan Li" -OWAEnabled $false

此範例會啟用 Elly Nkya 信箱的 Outlook Web App。

    Set-CASMailbox -Identity Ellyn@contoso.com -OWAEnabled $true

如需詳細的語法及參數資訊，請參閱 [Set-CASMailbox](https://technet.microsoft.com/zh-tw/library/bb125264\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要驗證是否成功啟用或停用使用者信箱的 Outlook Web App ，請執行以下其中一個操作：

  - 在 EAC 中，導覽至 \[收件者\] \> \[信箱\]，按一下信箱，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

  - 在信箱內容頁面上，按一下 \[信箱功能\]。

  - 在 \[電子郵件連線\] 下，驗證 Outlook Web App 是否啟用或停用。

或

  - 在命令介面中執行下列命令。
    
        Get-CASMailbox <identity>
    
    如果已啟用Outlook Web App 、 *OWAEnabled*屬性的值是`True`。如果已停用Outlook Web App ，此值為`False`。

