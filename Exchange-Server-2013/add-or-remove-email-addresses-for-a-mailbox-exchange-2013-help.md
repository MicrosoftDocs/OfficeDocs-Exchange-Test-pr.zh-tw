---
title: '新增或移除信箱的電子郵件地址: Exchange Online Help'
TOCTitle: 新增或移除信箱的電子郵件地址
ms:assetid: 93e2d9a4-7558-4509-8641-8381a7eb674f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb123794(v=EXCHG.150)
ms:contentKeyID: 50554035
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 新增或移除信箱的電子郵件地址

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

您可以設定多個相同信箱的電子郵件地址。其他地址稱為*proxy 位址*。Proxy 位址可讓使用者接收電子郵件傳送至不同的電子郵件地址。傳送給使用者的 proxy 位址任何電子郵件傳送到*主要 SMTP 位址*\] 或 \[*預設回覆地址*又稱做為其主要電子郵件地址。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您使用 Office 365 企業版，您應該新增或移除使用者信箱的電子郵件地址中<a href="https://go.microsoft.com/fwlink/p/?linkid=8347775">Office 365 系統管理中心： 新增至 Office 365 中的使用者的其他電子郵件別名</a></td>
</tr>
</tbody>
</table>


管理收件者與相關的其他管理工作，請參閱 ＜ [收件者](recipients-exchange-2013-help.md)的 「 收件者文件 」 表格。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：2 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md) 主題中的「收件者佈建權限」一節。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

本主題中的程序說明如何新增或移除使用者信箱的電子郵件地址。您可以使用類似的程序可新增或移除其他收件者類型的電子郵件地址。

## 您要執行的工作

## 新增至使用者信箱的電子郵件地址

## 使用 EAC 來新增電子郵件地址

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[信箱\]。

2.  中使用者信箱清單中，按一下您想要新增至電子郵件地址的信箱，然後按一下 \[**編輯**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在信箱內容頁面上，按一下 \[**電子郵件地址**。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>在 [<strong>電子郵件地址</strong>] 頁面上的主要 SMTP 位址會顯示在粗體文字的地址清單中，在 [<strong>類型</strong>] 欄中的大寫<strong>SMTP</strong>值。</td>
    </tr>
    </tbody>
    </table>


4.  按一下 \[**新增**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")，並再按一下 \[ **SMTP**新增至此信箱的 SMTP 電子郵件地址。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>SMTP 是預設的電子郵件地址類型。您也可以新增到信箱 Exchange 整合通訊 (EUM) 地址或自訂的地址。如需詳細資訊，請參閱 「 變更使用者信箱內容 」 <a href="manage-user-mailboxes-exchange-2013-help.md">管理使用者信箱</a>主題中。</td>
    </tr>
    </tbody>
    </table>


5.  在 \[**電子郵件地址**\] 方塊中輸入新的 SMTP 位址並再按一下 \[**確定\]**。
    
    在所選取的信箱的電子郵件地址清單中會顯示新的地址。

6.  按一下 \[**儲存**\] 以儲存變更。

## 使用命令介面來新增電子郵件地址

與信箱相關聯的電子郵件地址都包含在信箱的*EmailAddresses*屬性。它可以包含多個電子郵件地址，因為*EmailAddresses*屬性稱為*多重值*屬性。下列範例會顯示不同的方式修改多重值的屬性。

此範例示範如何新增 SMTP 位址 Dan 跳轉的信箱。

    Set-Mailbox "Dan Jump" -EmailAddresses @{add="dan.jump@northamerica.contoso.com"}

本範例會示範如何新增到信箱的多個 SMTP 位址。

    Set-Mailbox "Dan Jump" -EmailAddresses @{add="dan.jump@northamerica.contoso.com","danj@tailspintoys.com"}

如需如何使用此方法的新增和移除多重值屬性值的詳細資訊，請參閱[修改多重值內容](modifying-multivalued-properties-exchange-2013-help.md)。

此範例會顯示另一種方式藉由指定信箱相關聯的所有位址新增至信箱的電子郵件地址。在這個範例中，danj@tailspintoys.com 是您想要新增新電子郵件地址。其他兩個電子郵件地址為現有地址。使用區分大小寫`SMTP`位址為主要 SMTP 位址。您必須使用此命令語法時包含信箱的所有電子郵件地址。如果您未在命令中指定的地址會覆寫現有的地址。

    Set-Mailbox "Dan Jump" -EmailAddresses SMTP:dan.jump@contoso.com,dan.jump@northamerica.contoso.com,danj@tailspintoys.com

如需詳細的語法及參數資訊，請參閱 [Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\))。

## 如何知道這是否正常運作？

若要驗證您已順利是否已新增電子郵件地址給信箱，請執行以下其中一項動作：

  - 在 EAC 中，導覽至 \[收件者\] \> \[信箱\]，按一下信箱，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

  - 在信箱內容頁面上，按一下 \[**電子郵件地址**。

  - 在信箱的電子郵件地址清單中，確認新的電子郵件地址包含在內。

或

  - 在命令介面中執行下列命令。
    
        Get-Mailbox <identity> | fl EmailAddresses

  - 確認新的電子郵件地址包含在結果中。

## 移除使用者信箱的電子郵件地址

## 使用 EAC 來移除電子郵件的地址

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[信箱\]。

2.  在使用者信箱清單中，按一下您想要移除的電子郵件地址、 信箱和 \[**編輯**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

3.  在信箱內容頁面上，按一下 \[**電子郵件地址**。

4.  在電子郵件地址清單中，選取您要移除的地址和 \[**移除**![\[移除\] 圖示](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[移除] 圖示")。

5.  按一下 \[**儲存**\] 以儲存變更。

## 使用命令介面來移除電子郵件地址

本範例會示範如何移除 Janet Schorr 信箱的電子郵件地址。

    Set-Mailbox "Janet Schorr" -EmailAddresses @{remove="janets@corp.contoso.com"}

本範例會示範如何從信箱移除多個地址。

    Set-Mailbox "Janet Schorr" -EmailAddresses @{remove="janet.schorr@corp.contoso.com","janets@tailspintoys.com"}

如需如何使用此方法的新增和移除多重值屬性值的詳細資訊，請參閱 ＜ [修改多重值內容](modifying-multivalued-properties-exchange-2013-help.md)。

您也可以省略命令設定信箱的電子郵件地址中移除電子郵件地址。例如，假設 Janet Schorr 信箱有三個電子郵件地址： janets@contoso.com （主要 SMTP 位址）、 janets@corp.contoso.com 及 janets@tailspintoys.com。若要移除地址 janets@corp.contoso.com，您將執行下列命令。

    Set-Mailbox "Janet Schorr" -EmailAddresses SMTP:janets@contoso.com,janets@tailspintoys.com

因為 janets@corp.contoso.com 已在上一個命令中省略，它會從信箱移除。

如需詳細的語法及參數資訊，請參閱 [Set-Mailbox](https://technet.microsoft.com/zh-tw/library/bb123981\(v=exchg.150\))。

## 如何知道這是否正常運作？

若要確認您是否已成功移除電子郵件地址信箱，請執行下列其中一項：

  - 在 EAC 中，導覽至 \[收件者\] \> \[信箱\]，按一下信箱，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

  - 在信箱內容頁面上，按一下 \[**電子郵件地址**。

  - 在信箱的電子郵件地址清單中，確認電子郵件地址不包含在內。

或

  - 在命令介面中執行下列命令。
    
        Get-Mailbox <identity> | fl EmailAddresses

  - 確認電子郵件地址不包含在結果中。

## 使用命令介面來新增至多個信箱的電子郵件地址

您可以新增多個信箱一次新增電子郵件地址使用命令介面和逗點分隔值 (CSV) 檔案。

本範例會將資料從 C:\\Users\\Administrator\\Desktop\\AddEmailAddress.csv，具有下列格式。

    Mailbox,NewEmailAddress
    Dan Jump,danj@northamerica.contoso.com
    David Pelton,davidp@northamerica.contoso.com
    Kim Akers,kima@northamerica.contoso.com
    Janet Schorr,janets@northamerica.contoso.com
    Jeffrey Zeng,jeffreyz@northamerica.contoso.com
    Spencer Low,spencerl@northamerica.contoso.com
    Toni Poe,tonip@northamerica.contoso.com
    ...

執行下列命令以新增指定 CSV 檔案中每個信箱的電子郵件的地址使用 CSV 檔案中的資料。

    Import-CSV "C:\Users\Administrator\Desktop\AddEmailAddress.csv" | ForEach {Set-Mailbox $_.Mailbox -EmailAddresses @{add=$_.NewEmailAddress}}

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>此 CSV 檔 (<code>Mailbox,NewEmailAddress</code>) 的第一列的欄名是任意的。不論您使用欄名，請確定您在命令介面命令中使用相同的資料行名稱。</td>
</tr>
</tbody>
</table>


## 如何知道這是否正常運作？

若要確認您是否已成功加入電子郵件地址多個信箱，請執行下列其中一項：

  - 在 EAC 中，瀏覽至 \[**收件者**\>**信箱**，按一下 \[新增、 地址的信箱\] 和 \[**編輯**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

  - 在 \[信箱\] 屬性頁面中，按一下 \[**電子郵件地址**。

  - 在信箱的電子郵件地址清單中，確認新的電子郵件地址包含在內。

或

  - 執行下列命令在命令介面中使用相同的 CSV 檔用來新增新的電子郵件地址。
    
        Import-CSV "C:\Users\Administrator\Desktop\AddEmailAddress.csv" | ForEach {Get-Mailbox $_.Mailbox | fl Name,EmailAddresses}

  - 確認新的電子郵件地址包含在結果中的每個信箱。

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

