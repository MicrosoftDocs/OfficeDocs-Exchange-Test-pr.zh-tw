---
title: '建立電子郵件地址原則: Exchange 2013 Help'
TOCTitle: 建立電子郵件地址原則
ms:assetid: eb2bf42e-2058-4e17-85d5-97546433b40a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb125137(v=EXCHG.150)
ms:contentKeyID: 50474518
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.NewEmailAddressPolicyWizardForm.EmailAddressPolicyIntroductionPage
ms.translationtype: MT
---

# 建立電子郵件地址原則

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-12-10_

接收或傳送電子郵件的收件者、 收件者必須具有電子郵件地址。電子郵件地址原則產生的主要和次要電子郵件地址的收件者 （其中包括使用者、 連絡人及群組），讓他們可以接收並傳送電子郵件。

建立電子郵件地址原則時，您可以使用下列電子郵件地址類型：

  - **預先定義的 SMTP 電子郵件地址**。*「預先定義的」*(Precanned) SMTP 電子郵件地址是提供給您的常用電子郵件地址類型。

  - **自訂 SMTP 電子郵件地址**。如果您不想使用其中一個預先定義的 SMTP 電子郵件地址，可以指定自訂的 SMTP 電子郵件地址。
    
    建立自訂的 SMTP 電子郵件地址時，您可以使用下表中的變數來指定電子郵件地址本機部分的替代值。
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>變數</th>
    <th>值</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>%g</p></td>
    <td><p>名字</p></td>
    </tr>
    <tr class="even">
    <td><p>%i</p></td>
    <td><p>中間名的縮寫</p></td>
    </tr>
    <tr class="odd">
    <td><p>%s</p></td>
    <td><p>姓氏</p></td>
    </tr>
    <tr class="even">
    <td><p>%d</p></td>
    <td><p>顯示名稱</p></td>
    </tr>
    <tr class="odd">
    <td><p>%m</p></td>
    <td><p>Exchange 別名</p></td>
    </tr>
    <tr class="even">
    <td><p>%<em>x</em>s</p></td>
    <td><p>使用姓氏的前 <em>x</em> 個字母。例如，如果 <em>x</em> =2，則會使用姓氏的前兩個字母。</p></td>
    </tr>
    <tr class="odd">
    <td><p>%<em>x</em>g</p></td>
    <td><p>使用名字的前 <em>x</em> 個字母。例如，如果 <em>x</em> =2，則會使用名字的前兩個字母。</p></td>
    </tr>
    </tbody>
    </table>


  - **非 SMTP 電子郵件地址**。可支援的非 SMTP 電子郵件地址類型如下：
    
      - EX (傳統 DN Proxy 位址前置詞顯示名稱)
    
      - X.500
    
      - X.400
    
      - MSMail
    
      - CcMail
    
      - Lotus Notes
    
      - Novell GroupWise
    
      - Exchange 整合通訊 Proxy 位址 (EUM Proxy 位址)
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>在 Exchange 中，所有非 SMTP 電子郵件地址都會被視為自訂地址。Exchange 不會針對 X.400、GroupWise 或 Lotus Notes 電子郵件地址類型提供唯一的對話方塊或內容頁面。若您新增非 SMTP 自訂電子郵件地址，則必須安裝適當的動態連結程式庫 (DLL) 檔案。若不提供適當的 DLL 檔案，將無法建立自訂的電子郵件地址原則。將會在事件檢視器中記錄下列錯誤：「'i386' 電腦上遺失 Microsoft Exchange 目錄中 'SADF' 地址類型的電子郵件地址描述物件。」</td>
    </tr>
    </tbody>
    </table>


如需如何建立電子郵件地址原則的詳細說明，請參閱下列主題：

[建立電子郵件地址原則](create-an-email-address-policy-exchange-2013-help.md)

[使用收件者篩選器來建立電子郵件地址原則](create-an-email-address-policy-by-using-recipient-filters-exchange-2013-help.md)

## 開始前需要瞭解什麼？

  - 預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [電子郵件地址和通訊錄](email-addresses-and-address-books-exchange-2013-help.md) 項目中的「電子郵件地址原則」項目。

  - SMTP 地址網域可使用於電子郵件地址原則之前，您必須設定公認的網域。若要深入了解，請參閱[公認的網域](accepted-domains-exchange-2013-help.md)。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 您要執行的工作

## 使用 EAC 建立電子郵件地址原則

1.  瀏覽至 \[郵件流程\] \> \[電子郵件地址原則\]，然後按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

2.  在 \[電子郵件地址原則\] 中完成下列欄位：
    
      - **原則名稱**
    
      - **電子郵件地址格式**
    
      - **指定此電子郵件地址將套用的收件者類型**

3.  
    
    按一下 \[以進一步限制此原則將會套用至收件者的 \[**新增規則**\]。這會建立布林值**和**陳述式。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dd876857.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您套用過多原則，可能會過度限縮電子郵件地址原則，以至於不含任何使用者。</td>
    </tr>
    </tbody>
    </table>


4.  按一下 \[預覽原則適用於下列內容的收件者\]，查看此通訊清單將套用的收件者。

5.  
    
    按一下 \[儲存\] 以儲存變更並建立原則。

6.  您會看到警告，告知您除非加以更新，否則不會套用電子郵件地址原則。建立後，將其選取，接著在詳細資料窗格中按一下 \[套用\]。

## 使用命令介面來建立電子郵件地址原則

此範例會建立電子郵件地址原則，其中包含美國東南部辦公室 (Southeast offices) 的信箱使用者，並使其電子郵件地址包含其姓氏加上名字前兩個字母的組合。

    New-EmailAddressPolicy -Name "southeast offices" -IncludedRecipients MailboxUsers -ConditionalStateorProvince "Georgia","Alabama","Louisiana" -EnabledEmailAddressTemplates "SMTP:%s%2g@southeast.contoso.com"

如需詳細的語法及參數資訊，請參閱 [New-EmailAddressPolicy](https://technet.microsoft.com/zh-tw/library/aa996800\(v=exchg.150\))。

