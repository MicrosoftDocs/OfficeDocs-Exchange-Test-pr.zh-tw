---
title: '啟用或停用信箱的 Exchange ActiveSync: Exchange Online Help'
TOCTitle: 啟用或停用信箱的 Exchange ActiveSync
ms:assetid: dcf7c05b-b1b9-4b0f-800d-fec9f2ddc9e4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124809(v=EXCHG.150)
ms:contentKeyID: 50554099
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟用或停用信箱的 Exchange ActiveSync

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2012-11-13_

您可以使用 EAC 或命令介面啟用或停用使用者信箱的 Microsoft Exchange ActiveSync 。Exchange ActiveSync是可讓使用者同步處理行動裝置與 Exchange 信箱的用戶端通訊協定。建立使用者信箱時預設會啟用Exchange ActiveSync 。若要深入了解，請參閱[Exchange ActiveSync](exchange-activesync-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 2 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [用戶端和行動裝置權限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主題中的 「 Exchange ActiveSync 設定 」 項目。

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

## 使用 EAC 來啟用或停用 Exchange ActiveSync

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[信箱\]。

2.  在使用者信箱清單中，按一下您想要啟用或停用， Exchange ActiveSync的信箱和 \[**編輯**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在信箱的屬性頁上，按一下 \[信箱功能\]。

4.  **行動裝置**\] 下執行下列其中一項：
    
      - 若要停用Exchange ActiveSync按一下 \[**停用 Exchange ActiveSync**\]。
        
        如果您確定要停用Exchange ActiveSync警告詢問。按一下 \[**是\]**。
    
      - 若要啟用Exchange ActiveSync，按一下 \[**啟用 Exchange ActiveSync**\]。

5.  按一下 \[儲存\] 儲存您的變更。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您可以啟用及使用 EAC 大量編輯功能停用Exchange ActiveSync多個使用者信箱。如需如何執行這項作業的詳細資訊，請參閱 「 大量編輯使用者信箱 」 一節中<a href="manage-user-mailboxes-exchange-2013-help.md">管理使用者信箱</a>。</td>
</tr>
</tbody>
</table>


## 使用命令介面啟用或停用 Exchange ActiveSync

本範例會停用Exchange ActiveSync Yan Li 信箱。

    Set-CASMailbox -Identity "Yan Li" -ActiveSyncEnabled $false

此範例會啟用之信箱的 Elly Nkya Exchange ActiveSync 。

    Set-CASMailbox -Identity Ellyn@contoso.com -ActiveSyncEnabled $true

如需詳細的語法及參數資訊，請參閱 [Set-CASMailbox](https://technet.microsoft.com/zh-tw/library/bb125264\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要確認您是否已成功啟用或停用Exchange ActiveSync使用者信箱，請執行下列其中一項：

  - 在 EAC 中，導覽至 \[收件者\] \> \[信箱\]，按一下信箱，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

  - 在信箱內容頁面上，按一下 \[信箱功能\]。

  - 在 \[**行動裝置**，確認是否啟用或停用Exchange ActiveSync 。

或

  - 在命令介面中執行下列命令。
    
        Get-CASMailbox <identity>
    
    如果已啟用Exchange ActiveSync 、 *ActiveSyncEnabled*屬性的值是`True`。如果已停用Exchange ActiveSync ，此值為`False`。

