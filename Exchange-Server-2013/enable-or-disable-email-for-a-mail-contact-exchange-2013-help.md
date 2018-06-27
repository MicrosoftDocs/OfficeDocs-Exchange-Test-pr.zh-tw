---
title: '啟用或停用郵件連絡人的電子郵件: Exchange 2013 Help'
TOCTitle: 啟用或停用郵件連絡人的電子郵件
ms:assetid: ca47441f-1aa4-4958-aba5-18d51e59837e
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb124552(v=EXCHG.150)
ms:contentKeyID: 50554062
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟用或停用郵件連絡人的電子郵件

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-12-05_

您可以為 Exchange 組織中停用現有的郵件連絡人的電子郵件。當您停用郵件連絡人的電子郵件時，它已從 Exchange 和貴組織的通訊錄。如果郵件連絡人的通訊群組的成員，連絡人不會再收到郵件傳送至群組。另外，Exchange 屬性已從 Active Directory 中，擁有郵件功能的連絡人物件，但連絡人和非 Exchange 屬性 （如連絡人及組織資訊） 都會保留在 Active Directory 中。

停用郵件連絡人的電子郵件之後，您可以啟用郵件功能連絡人再次使用**Enable-MailContact**指令程式在命令介面中。您也可以使用此指令程式來啟用任何 Active Directory 連絡人的郵件功能。

郵件連絡人相關的其他管理工作，請參閱[管理郵件連絡人](manage-mail-contacts-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：2 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [收件者權限](recipients-permissions-exchange-2013-help.md)主題中 「 郵件連絡人"的項目。

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

## 停用郵件連絡人的電子郵件

如先前另有說明，當您停用郵件連絡人的電子郵件、 Exchange 屬性已從對應的 Active Directory 連絡人物件，但保留連絡人。在 EAC 中，郵件連絡人清單中移除郵件連絡人，但您可以檢視和使用 Active Directory 使用者及電腦或命令介面中使用**Get-Contact**和**Set-Contact**指令程式來管理對應的 Active Directory 連絡人物件。

## 使用 EAC 來停用郵件連絡人的電子郵件

1.  在 EAC 中，瀏覽至 \[收件者\] \> \[連絡人\]。

2.  在連絡人清單中，按一下您要停用電子郵件的郵件連絡人。

3.  按一下 \[更多\]![更多選項圖示](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "更多選項圖示")，然後按一下 \[停用\]。

4.  一則警告訊息會出現詢問是否確定要停用所選的郵件連絡人。按一下 \[**是\]**以停用它。

會從連絡人清單中移除郵件連絡人。

## 使用命令介面來停用郵件連絡人的電子郵件

本範例會停用 Neil 黑色的郵件連絡人的電子郵件。

    Disable-MailContact -Identity "Neil Black"

如需詳細的語法及參數資訊，請參閱[Disable-MailContact](https://technet.microsoft.com/zh-tw/library/aa997465\(v=exchg.150\))。

## 如何知道這是否正常運作？

若要確認您是否已成功停用郵件連絡人的電子郵件，請執行下列其中一項：

1.  在 EAC 中，瀏覽至 \[**收件者**\>**連絡人**並確認已不再列出郵件連絡人。

2.  Active Directory 使用者及電腦\] 中以滑鼠右鍵按一下連絡人，並再按一下 \[**內容**。在 \[**一般**\] 索引標籤上注意到**電子郵件**\] 方塊是空白。這會驗證該連絡人不會啟用郵件功能。

3.  在命令介面中，執行下列命令。
    
        Get-MailContact
    
    將不會在結果中傳回停用的電子郵件連絡人，因為此指令程式只會傳回擁有郵件功能的連絡人。

4.  在命令介面中，執行下列命令。
    
        Get-Contact
    
    因為此 cmdlet 會傳回所有 Active Directory 連絡人物件的結果被傳回停用的電子郵件連絡人。

## 使用命令介面來啟用郵件連絡人

您可以使用**Enable-MailContact**指令程式來啟用現有的 Active Directory 連絡人的郵件功能。您可以擁有郵件功能的單一連絡人或多名連絡人啟用郵件功能使用 CSV 檔案。

## 使用命令介面來啟用單一連絡人的郵件功能

本範例會啟用郵件功能的連絡人 Rene Valdes。您必須提供外部電子郵件地址。

    Enable-MailContact -Identity "Rene Valdes" -ExternalEmailAddress renev@tailspintoys.com

## 使用命令介面和 CSV 檔案來啟用多個連絡人的郵件功能

當您正在啟用擁有郵件功能連絡人大量您先匯出未啟用郵件功能為 CSV （逗點分隔值） 檔案，並使用 \[記事本\] 之類的文字編輯器或例如 Microsoft Excel 試算表應用程式再新增至 CSV 檔案的外部電子郵件地址的連絡人清單。然後您可以使用更新的 CSV 檔案中的命令介面命令來啟用 CSV 檔案中所列的連絡人的郵件功能。

1.  執行下列命令以匯出不上名為 Contacts.csv 的系統管理員的桌面檔案具有郵件功能的現有連絡人的清單。
    
        Get-Contact | Where { $_.RecipientType -eq "Contact" } | Out-File "C:\Users\Administrator\Desktop\Contacts.csv"
    
    產生的檔案類似下列檔案。
    
        Name
        Walter Harp
        James Alvord
        Rainer Witt
        Susan Burk
        Ian Tien
        ...

2.  新增名為**EmailAddress**欄標題，並再檔案中新增的每位連絡人的電子郵件地址。必須以逗號分隔的名稱和每個連絡人的外部電子郵件地址。更新的 CSV 檔案應該類似下列的檔案。
    
        Name,EmailAddress
        James Alvord,james@contoso.com
        Susan Burk,sburk@tailspintoys.com
        Walter Harp,wharp@tailspintoys.com
        Ian Tien,iant@tailspintoys.com
        Rainer Witt,rainerw@fourthcoffee.com
        ...

3.  執行下列命令，以使用 CSV 檔案中的資料檔案中所列的連絡人啟用郵件功能。
    
        Import-CSV C:\Users\Administrator\Desktop\Contacts.csv | ForEach-Object {Enable-MailContact -Identity $_.Name -ExternalEmailAddress $_.EmailAddress}
    
    命令結果會顯示新的擁有郵件功能連絡人的相關資訊。

## 如何知道這是否正常運作？

若要確認您已成功啟用郵件功能的 Active Directory 連絡人，執行下列其中一項：

  - 在 EAC 中，瀏覽至 \[**收件者**\>**連絡人**。新的郵件連絡人會顯示在連絡人清單中。\[**連絡人類型**\] 下方類型是**郵件連絡人**。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您必須按一下 [<strong>重新整理</strong><img src="images/Dn624163.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif" title="重新整理圖示" alt="重新整理圖示" />以顯示新郵件連絡人。</td>
    </tr>
    </tbody>
    </table>


  - 在命令介面中執行下列命令以顯示新郵件連絡人的相關資訊。
    
        Get-MailContact | Format-Table Name,RecipientTypeDetails,ExternalEmailAddress

