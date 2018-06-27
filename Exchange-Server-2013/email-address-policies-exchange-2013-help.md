---
title: '電子郵件地址原則: Exchange 2013 Help'
TOCTitle: 電子郵件地址原則
ms:assetid: b63b63bb-6faf-4337-8441-50bc64b49bb8
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb232171(v=EXCHG.150)
ms:contentKeyID: 50474034
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 電子郵件地址原則

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-07-21_

（其中包括使用者、 資源、 連絡人及群組） 的收件者是擁有郵件功能中任何物件Active Directory哪些 microsoft Exchange可以傳遞，或路由傳送的郵件。傳送或接收的電子郵件的收件者、 收件者必須具有電子郵件地址。電子郵件地址原則會產生的主要和次要電子郵件地址的收件者，讓他們可以接收並傳送電子郵件。

根據預設，Exchange 對於每一個擁有郵件功能的使用者都會包含一個電子郵件地址原則。這個預設原則會指定收件者的別名做為電子郵件地址的本機部分，並且使用預設的公認的網域。電子郵件地址的本機部分就是出現於 @ 符號前的名稱。不過，您可以變更收件者電子郵件地址的顯示方式。例如，您可以指定地址顯示為 *firstnamelastname*@contoso.com。

此外，如果您想要指定其他的電子郵件地址的所有收件者或剛子集，您可以修改預設原則或建立額外的原則。例如，使用者信箱的 David Hamilton 可以接收寄給 hdavid@mail.contoso.com 和 hamilton.david@mail.contoso.com 的電子郵件。

要尋找與電子郵件地址原則相關的管理工作嗎？請參閱[電子郵件地址原則程序](email-address-policy-procedures-exchange-2013-help.md)。

## 收件者原則的行為

Exchange 會將原則套用至符合收件者篩選準則的所有收件者：

  - 收件者原則會順序的最高優先順序套用至最低優先順序。兩個或多個原則之間的衝突的情況下會套用優先順序最高的原則。預設的收件者原則一定是具有最低優先順序且沒有其他原則的比對要套用。
    
    當您建立收件者原則，但沒有明確地指定優先順序時，則將會新增為最高優先順序。如果您指定已相關聯的現有原則、 現有的原則與較低優先順序的所有原則的優先順序會向下移動以下列一項。在您指定的優先順序就會插入新的原則。
    
    收件者原則功能可分為下列兩項功能： 電子郵件地址原則和公認的網域。如需公認的網域的詳細資訊，請參閱[公認的網域](accepted-domains-exchange-2013-help.md)。

  - 在 Exchange 管理命令介面中執行 **Update-EmailAddressPolicy** Cmdlet 時，會以電子郵件地址原則更新收件者物件。

  - 收件者物件是修改並儲存，每次Exchange強制執行電子郵件地址準則和設定正確的應用程式。電子郵件地址原則已修改並儲存，以變更所更新所有相關聯的收件者。此外，如果已修改的收件者物件，該收件者的電子郵件地址原則的成員資格是重新評估並強制執行。

## 建立電子郵件地址原則

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

