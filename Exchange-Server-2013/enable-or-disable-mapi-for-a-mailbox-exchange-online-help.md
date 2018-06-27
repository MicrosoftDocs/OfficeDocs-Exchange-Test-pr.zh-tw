---
title: '啟用或停用信箱的 MAPI: Exchange Online Help'
TOCTitle: 啟用或停用信箱的 MAPI
ms:assetid: c2c6718c-a2c0-4ed2-b4ed-364c3cb1f592
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124497(v=EXCHG.150)
ms:contentKeyID: 50554058
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟用或停用信箱的 MAPI

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2017-12-31_

您可以使用Exchange 系統管理中心或Exchange 管理命令介面啟用或停用 MAPI 使用者信箱。啟用 MAPI 時，可以Outlook或其他 MAPI 電子郵件用戶端存取使用者的信箱。當停用 MAPI 時，它不能存取Outlook或其他 MAPI 用戶端。不過，信箱會繼續接收電子郵件訊息，並假設信箱會啟用以支援存取這些用戶端，使用者可以存取權傳送及接收電子郵件使用Outlook Web App、 POP 電子郵件用戶端或 IMAP 用戶端的信箱。

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

  - [啟用或停用 Outlook Web App 信箱](enable-or-disable-outlook-web-app-for-a-mailbox-exchange-2013-help.md)

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
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 您要執行的工作

## 使用 EAC 啟用或停用 MAPI

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[信箱\]。

2.  在使用者信箱清單中，按一下您要啟用或停用 MAPI 的信箱，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在信箱的屬性頁上，按一下 \[信箱功能\]。

4.  在 **\[電子郵件連線\]** 下，執行下列其中一項操作。
    
      - 若要停用 MAPI，請在 **\[MAPI：已啟用\]**，按一下 **\[停用\]**。
        
        此時會出現警告，詢問您是否要停用 MAPI。按一下 **\[是\]**。
    
      - 若要啟用 MAPI，請在 **\[MAPI：已停用\]**，按一下 **\[啟用\]**。

5.  按一下 \[儲存\] 儲存您的變更。

## 使用 Exchange 管理命令介面啟用或停用 MAPI

此範例會停用 Ken Sanchez 信箱的 MAPI。

    Set-CASMailbox -Identity "Ken Sanchez" -MAPIEnabled $false

此範例會啟用 Esther Valle 信箱的 MAPI。

    Set-CASMailbox -Identity "Esther Valle" -MAPIEnabled $true

如需詳細的語法及參數資訊，請參閱 [Set-CASMailbox](https://technet.microsoft.com/zh-tw/library/bb125264\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要驗證您是否已成功啟用或停用使用者信箱的 MAPI ，請執行下列其中一項操作：

  - 在 EAC 中，導覽至 **\[收件者\]** \> **\[信箱\]**，按一下信箱，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

  - 在信箱的屬性頁上，按一下 \[信箱功能\]。

  - 在 **\[電子郵件連線\]** 下，驗證 MAPI 是否啟用或停用。

或

  - 在 Exchange 管理命令介面 中執行下列命令。
    
        Get-CASMailbox <identity>
    
    如果已啟用 MAPI，*MapiEnabled* 屬性的值是 `True`。如果已停用 MAPI，則值是 `False`。

