---
title: '設定信箱的郵件傳遞限制: Exchange Online Help'
TOCTitle: 設定信箱的郵件傳遞限制
ms:assetid: c4b8b89f-3dbe-4cb8-8839-9a4e8067e00c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb397214(v=EXCHG.150)
ms:contentKeyID: 50554060
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 設定信箱的郵件傳遞限制

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2012-11-29_

您可以使用 EAC 或命令介面來限制是否要將郵件傳遞給個別收件者。郵件傳遞限制在控制誰能傳送郵件給組織中的使用者時十分好用。例如，您可以設定信箱接收或拒絕特定使用者所傳送的郵件，或只接收來自您 Exchange 組織中使用者的郵件。

本主題涵蓋的郵件傳遞限制適用於所有收件者類型。若要進一步了解不同的收件者類型，請參閱＜[收件者](recipients-exchange-2013-help.md)＞。

如需收件者相關的其他管理工作，請參閱下列主題：

  - [管理使用者信箱](manage-user-mailboxes-exchange-2013-help.md)

  - [建立並管理通訊群組](create-and-manage-distribution-groups-exchange-2013-help.md)

  - [管理動態通訊群組](manage-dynamic-distribution-groups-exchange-2013-help.md)

  - [管理郵件使用者](manage-mail-users-exchange-2013-help.md)

  - [管理郵件連絡人](manage-mail-contacts-exchange-2013-help.md)

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘。

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

## 使用 EAC 設定郵件傳遞限制

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[信箱\]。

2.  在使用者信箱清單中，按一下您要設定郵件傳遞限制的信箱，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在信箱的屬性頁上，按一下 \[信箱功能\]。

4.  在 \[郵件傳遞限制\] 下，按一下 \[檢視詳細資料\] 以檢視及變更下列傳遞限制：
    
      - \[接受郵件的來源\]   使用此區段來指定誰可以傳送郵件給此位使用者。
        
          - \[所有寄件者\]   此選項會指定使用者可接收來自所有寄件者的郵件。其中同時包括 Exchange 組織和外部寄件者中的寄件者。此為預設選項。只有在您清除 \[需要驗證所有寄件者\] 核取方塊時，這個選項才會包括外部使用者。如果您選取此核取方塊，則來自外部使用者的郵件將遭拒。
        
          - \[僅下列清單中的寄件者\]   此選項會指定使用者只可接受來自 Exchange 組織中指定之一組寄件者的郵件。按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示") 以顯示所有在您 Exchange 組織中的收件人。選取想要的收件者，將他們新增至清單，然後按一下 \[確定\]。您也可以在搜尋方塊中輸入收件者的名稱，然後按一下 \[搜尋\]![搜尋圖示](images/Dn624163.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "搜尋圖示")，就可以搜尋特定的收件者。
        
          - \[需要驗證所有寄件者\]   此選項可防止匿名使用者傳送郵件給使用者。這包括在您 Exchange 組織以外的外部使用者。
    
      - \[拒絕郵件的來源\]   使用此區段來指定傳送郵件給此位使用者的封鎖對象。
        
          - \[沒有寄件者\]   此選項可指定信箱不會拒絕來自 Exchange 組織中任何寄件者的郵件。這是預設選項。
        
          - \[下列清單中的寄件者\]   此選項會指定信箱拒絕來自 Exchange 組織中一組指定寄件者的郵件。按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示") 以顯示所有在您 Exchange 組織中的收件人。選取想要的收件者，將他們新增至清單，然後按一下 \[確定\]。您也可以在搜尋方塊中輸入收件者的名稱，然後按一下 \[搜尋\]![搜尋圖示](images/Dn624163.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "搜尋圖示")，就可以搜尋特定的收件者。

5.  按一下 \[確定\] 關閉 \[郵件傳遞限制\] 頁面，然後按一下 \[儲存\] 以儲存變更。

## 使用命令介面設定郵件傳遞限制

下列範例顯示如何使用命令介面來設定信箱的郵件傳遞限制。如果是其他收件者類型，請使用對應的 **Set-** Cmdlet 搭配相同參數。

此範例會設定 Robin Wood 的信箱只接收來自使用者 Lori Penor、Jeff Phillips 和通訊群組 Legal Team 1 成員的郵件。

    Set-Mailbox -Identity "Robin Wood" -AcceptMessagesOnlyFrom "Lori Penor","Jeff Phillips" -AcceptMessagesOnlyFromDLMembers "Legal Team 1"

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果設定信箱只接收來自個別寄件者的郵件，則必須使用 <em>AcceptMessagesOnlyFrom</em> 參數。如果設定信箱只接收來自特定通訊群組成員之寄件者的郵件，則必須使用 <em>AcceptMessagesOnlyFromDLMembers</em> 參數。</td>
</tr>
</tbody>
</table>


此範例會將名稱為 David Pelton 的使用者新增至 Robin Wood 信箱將會接收郵件的使用者清單中。

    Set-Mailbox -Identity "Robin Wood" -AcceptMessagesOnlyFrom @{add="David Pelton"}

此範例會設定 Robin Wood 信箱要求驗證所有的寄件者。這表示信箱只會接收來自 Exchange 組織中其他使用者所傳送的郵件。

    Set-Mailbox -Identity "Robin Wood" -RequireSenderAuthenticationEnabled $true

此範例會設定 Robin Wood 的信箱拒絕來自使用者 Joe Healy、Terry Adams 和通訊群組 Legal Team 2 成員的郵件。

    Set-Mailbox -Identity "Robin Wood" -RejectMessagesFrom "Joe Healy","Terry Adams" -RejectMessagesFromDLMembers "Legal Team 2"

此範例會設定 Robin Wood 的信箱也拒絕群組 Legal Team 3 成員所傳送的郵件。

    Set-Mailbox -Identity "Robin Wood" -RejectMessagesFromDLMembers @{add="Legal Team 3"}

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果設定信箱拒絕來自個別寄件者的郵件，則必須使用 <em>RejectMessagesFrom</em> 參數。如果設定信箱拒絕來自特定通訊群組成員之寄件者的郵件，則必須使用 <em>RejectMessagesFromDLMembers</em> 參數。</td>
</tr>
</tbody>
</table>


如需設定不同類型收件者之傳遞限制相關的詳細語法與參數資訊，請參閱下列主題：

  - [Set-DistributionGroup](https://technet.microsoft.com/zh-tw/library/bb124955\(v=exchg.150\))

  - [Set-DynamicDistributionGroup](https://technet.microsoft.com/zh-tw/library/bb123796\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\))

  - [Set-MailContact](https://technet.microsoft.com/zh-tw/library/aa995950\(v=exchg.150\))

  - [Set-MailUser](https://technet.microsoft.com/zh-tw/library/aa995971\(v=exchg.150\))

## 如何知道這是否正常運作？

若要驗證您是否已成功設定使用者信箱的郵件傳遞限制，請執行下列其中一項操作：

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[信箱\]。

2.  在使用者信箱清單中，按一下您要驗證郵件傳遞限制的信箱，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在信箱的屬性頁上，按一下 \[信箱功能\]。

4.  在 \[郵件傳遞限制\] 下，按一下 \[檢視詳細資料\] 以確認信箱的傳遞限制。

或

在命令介面中執行下列命令。

    Get-Mailbox <identity> | fl AcceptMessagesOnlyFrom,AcceptMessagesOnlyFromDLMembers,RejectMessagesFrom,RejectMessagesFromDLMembers,RequireSenderAuthenticationEnabled

