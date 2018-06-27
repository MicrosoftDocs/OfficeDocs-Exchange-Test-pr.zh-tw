---
title: '將共用原則套用至信箱: Exchange 2013 Help'
TOCTitle: 將共用原則套用至信箱
ms:assetid: dd4cc765-8469-4176-bb6e-d5b0f5235927
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ657501(v=EXCHG.150)
ms:contentKeyID: 50474431
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 將共用原則套用至信箱

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-02-15_

共用原則屬於同盟共用的一部份，可讓使用者自行建立，與不同類型的外部使用者對其行事曆資訊進行人員對人員共用。系統管理員套用至使用者信箱的共用原則可以判斷使用者可共用以及與誰共用的存取層級。如果您未做任何變更，則預設共用原則會套用到所有使用者。如果您建立新的共用原則，則必須將該原則套用至信箱，它才會生效。共用原則可套用於單一使用者信箱，也可同時套用於多個使用者信箱。系統管理員也可以停用使用者的共用原則，以防止外部存取行事曆。

若要深入了解同盟共用，請參閱[共用](sharing-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中的*Recipient Provisioning Permissions* 項目。

  - 共用原則必須存在。如需詳細資訊，請參閱[建立共用原則](create-a-sharing-policy-exchange-2013-help.md)。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

## 您要執行的工作

## 使用 EAC 將共用原則套用到單一信箱

1.  瀏覽至 \[收件者\] \> \[信箱\]。

2.  在清單檢視中，選取所需的信箱，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在 **\[使用者信箱\]** 中，按一下 **\[信箱功能\]**。

4.  在 \[共用原則\] 清單中，選取要套用到此信箱的共用原則。

5.  按一下 **\[儲存\]** 以套用共用原則。

## 使用 EAC 將共用原則套用到多個信箱

1.  瀏覽至 \[收件者\] \> \[信箱\]。

2.  在清單檢視中，按住 Ctrl 鍵，以選取多個信箱。

3.  在詳細資料窗格中，信箱內容將被設定為大量編輯。按一下 \[更多選項\]。

4.  在 \[共用原則\] 下，按一下 \[更新\]。

5.  在 \[大量指派共用原則\] 中，使用 \[選取共用原則\] 清單來選取要指派給信箱的共用原則。

6.  按一下 **\[儲存\]**，將共用原則套用於選取的信箱。

## 使用命令介面將共用原則套用到一個或多個信箱

此範例將共用原則 Contoso 套用到使用者 Barbara 的單一信箱。

    Set-Mailbox -Identity Barbara -SharingPolicy "Contoso"

此範例會指定「行銷」部門的所有使用者信箱都使用共用原則 Contoso Marketing。

    Get-Mailbox -Filter {Department -eq "Marketing"} | Set-Mailbox -SharingPolicy "Contoso Marketing"

此範例會傳回已套用共用原則 Contoso 的所有信箱，並將使用者排序到只顯示使用者別名及電子郵件地址的表格中。

    Get-Mailbox -ResultSize unlimited | Where {$_.SharingPolicy -eq "Contoso" } | format-table Alias, EmailAddresses

如需詳細的語法及參數資訊，請參閱 [Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\)) 與 [Get-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123685\(v=exchg.150\))。

## 如何知道這是否正常運作？

若要確認您是否將共用原則成功到用到信箱資料庫，請進行下列其中一項：

  - 在 EAC 中，瀏覽至 \[收件者\] \> \[信箱\]，然後選取已套用共用原則的信箱。按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")，並按一下 \[信箱功能\]，然後確定正確的共用原則出現在 \[共用原則\] 清單中。

  - 執行下列命令介面指令，確認已將共用原則指派到使用者信箱。確認正確的共用原則列在 *SharingPolicy* 參數中。
    
        Get-Mailbox <user name> | format-list

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

