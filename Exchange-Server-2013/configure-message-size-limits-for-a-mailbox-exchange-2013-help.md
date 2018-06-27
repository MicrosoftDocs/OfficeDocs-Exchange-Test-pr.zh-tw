---
title: '設定信箱的郵件大小上限: Exchange 2013 Help'
TOCTitle: 設定信箱的郵件大小上限
ms:assetid: d1220685-14c0-4c4f-abb2-3920f3046212
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124708(v=EXCHG.150)
ms:contentKeyID: 50554064
ms.date: 01/12/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 設定信箱的郵件大小上限

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-11-12_

您可以使用 EAC 與命令介面來設定使用者信箱的郵件大小限制。這些限制控制使用者可收發的郵件大小。依預設，建立信箱時，沒有收發郵件的大小限制。

請記住，Exchange 組織中還有其他設定可決定信箱能夠收發的郵件大小上限 (例如，信箱伺服器上設定的郵件大小上限)。若要深入了解 Exchange 中的郵件大小限制，包括郵件大小限制的類型、其範圍及優先順序，請參閱[郵件大小限制](message-size-limits-exchange-2013-help.md)。

如需與使用者信箱相關的其他管理工作，請參閱[管理使用者信箱](manage-user-mailboxes-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您也可以依郵件使用者並從共用信箱控制收發郵件的大小。</td>
</tr>
</tbody>
</table>


## 開始之前有哪些須知？

  - 預估完成時間：2 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱[收件者權限](recipients-permissions-exchange-2013-help.md) 主題中的「收件者佈建權限」一節。

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

## 使用 EAC 來設定郵件大小限制

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[信箱\]。

2.  在使用者信箱清單中，按一下您想變更郵件大小限制的信箱，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在信箱的屬性頁上，按一下 \[信箱功能\]。

4.  在 \[郵件大小限制\] 之下，按一下 \[檢視詳細資料\] 以檢視與變更以下郵件大小限制：
    
      - \[已傳送郵件\]   若要指定此使用者傳送的最大郵件容量，請選擇 \[郵件大小上限 (KB)\] 核取方塊並在方塊中輸入值。 郵件大小必須介於 0 和 2,097,151 KB 之間。 如果使用者傳送的郵件大於指定的大小，該郵件便會傳回給使用者，並說明為錯誤郵件。
    
      - \[已接收郵件\]   若要指定此使用者接收的最大郵件容量，請選擇 \[郵件大小上限 (KB)\] 核取方塊並在方塊中輸入值。郵件大小必須介於 0 和 2,097,151 KB 之間。 如果使用者收到的郵件大於指定的大小，該郵件便會退回給寄件者，並提供說明錯誤訊息。

5.  按一下 \[確定\]，然後按一下 \[儲存\] 以儲存您的變更。

## 使用命令介面來設定郵件大小限制

此範例針對 Debra Garcia 信箱傳送郵件的大小上限設定為 25 MB，而接收郵件的大小上限為 35 MB。

    Set-Mailbox "Debra Garcia" -MaxSendSize 25mb -MaxReceiveSize 35mb

如需詳細的語法及參數資訊，請參閱 [Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\))。

## 如何知道這是否正常運作？

若要驗證是否成功設定信箱的郵件大小限制，請執行以下其中一個操作：

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[信箱\]。

2.  在使用者信箱清單中，按一下您想確認郵件大小限制的信箱，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在信箱的屬性頁上，按一下 \[信箱功能\]。

4.  在 \[郵件大小限制\] 之下，按一下 \[檢視詳細資料\] 以確認信箱的郵件大小限制。

或

在命令介面中執行下列命令。

    Get-Mailbox <identity> | fl MaxSendSize,MaxReceiveSize

