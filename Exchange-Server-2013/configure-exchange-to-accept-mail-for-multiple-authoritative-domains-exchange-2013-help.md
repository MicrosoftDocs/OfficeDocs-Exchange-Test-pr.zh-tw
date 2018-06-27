---
title: '將 Exchange 設定為接受多個授權網域的郵件: Exchange 2013 Help'
TOCTitle: 將 Exchange 設定為接受多個授權網域的郵件
ms:assetid: 11801f73-4934-4025-a1c1-3935dada7e9b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa996314(v=EXCHG.150)
ms:contentKeyID: 51409156
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 將 Exchange 設定為接受多個授權網域的郵件

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-06-15_

在 Microsoft Exchange Server 2013 中，可以輕易地將多個授權網域新增至您的組織。不過，在新增授權網域之後，您需要決定如何在組織中使用授權網域。例如：

  - 如果想要在新的授權網域中為組織中的收件者新增電子郵件地址，您是想要取代收件者的現有主要 (回覆) 地址，還是新增電子郵件地址作為 Proxy (次要) 地址？

  - 您是否想要讓新授權網域中的電子郵件地址套用至所有收件者，以及所有的收件者類型？或者，您是否想要讓新的電子郵件地址套用至特定的收件者類型，或根據其使用者內容的特定收件者，例如，僅限財務部門中的使用者？

下列範例為 Exchange 組織必須接收及處理多個授權 SMTP 網域的電子郵件的案例：

  - 您想要變更 SMTP 網域名稱，但必須繼續接收舊網域名稱的電子郵件一段時間，以防客戶將電子郵件傳送到先前的電子郵件地址。您可以將新的電子郵件地址設為主要 (回覆) 地址。這表示新地址將成為顯示在收件者傳送的所有電子郵件上的預設電子郵件地址。您可以設定舊的電子郵件地址為次要地址。這樣可讓收件者繼續接收傳送至舊電子郵件地址的電子郵件。

  - 您可以為組織內的業務單位提供不同的電子郵件地址。例如，如果 contoso.com Active Directory 樹系包含 Tailspin Toys 和 Fourth Coffee 這兩家分公司的子網域，您可以將 SMTP 網域名稱 contoso.com、tailspintoys.com 及 fourthcoffee.com 指派給那些個別業務單位的收件者。

  - 您提供電子郵件裝載服務，且必須接受多個 SMTP 網域名稱的電子郵件。

## 開始之前有哪些須知？

  - 完成此工作的預估時間：30 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「公認的網域」項目，以及[收件者權限](recipients-permissions-exchange-2013-help.md)主題中的「電子郵件地址原則」項目。

  - 如果您的周邊網路中有訂閱的 Edge Transport Server，則可在 Exchange 組織的 Mailbox Server 上設定公認網域。公認網域組態會在 EdgeSync 同步處理期間複寫至 Edge Transport Server。如需詳細資訊，請參閱[Edge 訂閱](edge-subscriptions-exchange-2013-help.md)。

  - 建立公認的網域時，可以在位址空間中使用萬用字元 (\*)，以指出 Exchange 組織也接受 SMTP 位址空間的所有子網域。例如，若要將 contoso.com 及其所有子網域設定為公認的網域，請輸入 **\*.contoso.com** 作為 SMTP 位址空間。不過，如果子網域名稱要用於電子郵件地址原則中，則每個子網域都必須要有明確的公認網域項目。

  - 您從網際網路接受其電子郵件的每一個 SMTP 網域，都需要公用 DNS 中的 MX 記錄。每一個 MX 記錄應解析收取您組織之電子郵件的外部網際網路伺服器。

  - 您需要設定傳送連接器和接收連接器，使 Exchange 組織可以在網際網路上收送電子郵件。網際網路傳送連接器和接收連接器的組態是由 Exchange 拓撲決定。如需設定連接器的詳細資訊，請參閱[連接器](connectors-exchange-2013-help.md)。

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


## 該怎麼做？

## 步驟 1：建立授權網域

## 使用 Exchange 系統管理中心來建立授權網域

1.  在 EAC 中，瀏覽至 \[郵件流程\] \> \[公認的網域\]，並且按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

2.  在 \[姓名\] 欄位中輸入公認的網域之顯示名稱。每個組織公認的網域必須有一個唯一的顯示名稱。顯示名稱可能與公認的網域不同。例如，網域 contoso.com 的顯示名稱可以是 Contoso Local Accepted Domain。

3.  在 **\[公認的網域\]** 欄位中，指定您組織接受其電子郵件的 SMTP 命名空間。例如，contoso.com。

4.  選取 \[授權網域\]。

5.  按一下 **\[儲存\]**。

## 使用命令介面來建立授權網域

若要建立新的授權網域，請使用下列語法。

    New-AcceptedDomain -Name "<Unique Name>" -DomainName <SMTP domain> -DomainType Authoritative

例如，若要為網域 fourthcoffee.com 建立名稱為 "Fourth Coffee subsidiary" 的新授權網域，請執行下列命令：

    New-AcceptedDomain -Name "Fourth Coffee subsidiary" -DomainName fourthcoffee.com -DomainType Authoritative

## 如何才能了解此步驟是否正常運作？

若要確認您是否已成功建立授權網域，請執行下列其中一個動作：

  - 在 EAC 中，瀏覽至 **\[郵件流程\]** \> **\[公認的網域\]**。確認已顯示所建立的公認網域，而且 **\[網域類型\]** 值為 **\[授權\]**。

  - 在命令介面中，執行命令 **Get-AcceptedDomain**。確認已顯示所建立的網域，而且 **DomainType** 值為 `Authoritative`。

## 步驟 2：設定授權網域的電子郵件地址原則

若要使用所建立的授權公認網域，您需要為符合案例目標的授權網域設定電子郵件地址原則。例如，您可能需要建立新的電子郵件地址原則，或修改現有的原則。您可以選擇取代您的部分或全部收件者的主要電子郵件地址，也可以選擇保留或移除舊的主要電子郵件地址。有兩個範例案例會呈現在本節中。

## 變更現有的主要電子郵件地址

若要變更已指派給收件者的主要 (回覆) 電子郵件地址，並保留舊的主要電子郵件地址作為 Proxy (次要) 電子郵件地址，請遵循下列步驟：

## 使用 EAC 來變更現有的主要電子郵件地址

1.  在 EAC 中，瀏覽至 **\[郵件流程\]** \> **\[電子郵件地址原則\]**。選取您要修改的電子郵件地址原則，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

2.  在 **\[電子郵件地址原則\]** 頁面上，按一下 **\[電子郵件地址格式\]** 索引標籤。在 **\[電子郵件地址格式\]** 區段中，按一下 **\[新增\]**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

3.  在出現的 **\[電子郵件地址格式\]** 頁面上，進行下列選取：
    
      - **\[選取公認的網域\]**   按一下下拉式清單，然後選取新的授權網域。
    
      - 選取 **\[將此格式設為回覆電子郵件地址\]**。
    
    完成後，按一下 **\[儲存\]**。

4.  在 **\[電子郵件地址原則\]** 頁面上，按一下 **\[儲存\]** 來儲存您對原則所做的變更。

5.  您會看到警告，告知您除非加以更新，否則不會套用電子郵件地址原則。建立後，將其選取，接著在詳細資料窗格中按一下 \[套用\]。

## 使用命令介面來變更現有的主要電子郵件地址

在命令介面中，您可以使用兩個個別的命令：一個命令用來修改現有的電子郵件地址原則，而另一個命令則用來將更新的電子郵件地址原則套用至您組織中的收件者。

若要變更現有的主要電子郵件地址，並保留舊的主要電子郵件地址作為 Proxy 地址，請執行下列命令：

    Set-EmailAddressPolicy <EmailAddressPolicyIdentity> -EnabledEmailAddressTemplates SMTP:<NewPrimaryEmailAddress>,smtp:<OldPrimaryEmailAddress>

例如，假設您組織中的電子郵件地址原則使用電子郵件地址格式 *useralias*`@contoso.com`。本範例會將電子郵件地址原則 (名稱為 "Default Policy") 中主要 (回覆) 地址的網域變更為 `@fourthcoffee.com`，並保留 `@contoso.com` 網域中舊的主要回覆地址作為 Proxy (次要) 地址。

    Set-EmailAddressPolicy "Default Policy" -EnabledEmailAddressTemplates SMTP:@fourthcoffee.com,smtp:@contoso.com

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>大寫字母的 <code>SMTP</code> 限定詞會指定主要 (回覆) 地址。小寫字母的 <code>smtp</code> 限定詞則會指定 Proxy (次要) 地址。</td>
</tr>
</tbody>
</table>


若要將更新的電子郵件地址原則套用至收件者，請使用下列語法。

    Update-EmailAddressPolicy <EamilAddressPolicyIdentity>

例如，若要套用已更新的電子郵件地址原則 (名稱為 "Default Policy")，請執行下列命令：

    Update-EmailAddressPolicy "Default Policy"

## 取代一組已篩選收件者的現有主要電子郵件地址

您無法修改要套用至一組已篩選收件者的預設電子郵件地址原則。您需要建立新的電子郵件地址原則，或修改現有的自訂電子郵件地址原則。本節中的範例會建立新的電子郵件地址原則。在這些範例中，新的公認網域中的主要 (回覆) 地址會取代指定收件者的舊主要地址，而不會保留舊的主要地址作為 Proxy (次要) 電子郵件地址。因此，受影響的收件者再也無法在其舊的主要電子郵件地址收到電子郵件。

此外，套用至特定使用者的電子郵件地址原則也應該具有比其他電子郵件地址原則 (包括預設原則) 還要高的優先順序 (以較低的整數值表示)，以便首先套用特定原則。因為兩個原則不能具有相同的優先順序值，所以您可能需要先降低組織的預設電子郵件地址原則的優先順序。

## 使用 EAC 來取代一組已篩選收件者的現有主要電子郵件地址

若要建立作為一組已篩選收件者的主要電子郵件地址的其他電子郵件地址，請遵循下列步驟：

1.  在 EAC 中，瀏覽至 **\[郵件流程\]** \> **\[電子郵件地址原則\]**，然後按一下 **\[新增\]**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

2.  在 **\[電子郵件地址原則\]** 頁面上，填妥下列欄位：
    
    1.  **原則名稱**   輸入唯一的描述名稱。
    
    2.  **電子郵件地址格式**   按一下 **\[新增\]**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。在出現的 **\[電子郵件地址格式\]** 頁面上，進行下列選取：
        
          - **\[選取公認的網域\]**   按一下下拉式清單，然後選取新的授權網域。
        
          - **電子郵件地址格式**   選取組織適用的電子郵件地址格式。
        
          - 選取 **\[將此格式設為回覆電子郵件地址\]**。
        
        完成後，按一下 **\[儲存\]**。

3.  **依此順序執行此原則與其他原則**   通常，套用至特定使用者的原則應該會具有比其他電子郵件地址原則 (包括預設原則) 還要高的優先順序 (以較低的整數值表示)。

4.  **指定將套用此電子郵件地址的收件者類型**   選取您要套用電子郵件地址原則的收件者類型。

5.  **建立規則以進一步定義將套用此電子郵件地址原則的收件者**   按一下 **\[新增規則\]**，以限制將套用此原則的收件者。如此會建立布林值 **And** 陳述式。視需要重複此步驟多次。
    
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


6.  按一下 \[預覽原則適用於下列內容的收件者\]，查看此通訊清單將套用的收件者。

7.  
    
    按一下 \[儲存\] 以儲存變更並建立原則。

8.  您會看到警告，告知您除非加以更新，否則不會套用電子郵件地址原則。建立後，將其選取，接著在詳細資料窗格中按一下 \[套用\]。

## 使用命令介面來取代一組已篩選收件者的現有主要電子郵件地址

若要取代一組已篩選收件者的主要電子郵件地址，請使用下列命令：

    New-EmailAddressPolicy -Name <Policy Name> -Priority <Integer> -IncludedRecipients <RecipientTypes> <Conditional Recipient Properties> -EnabledEmailAddressTemplates SMTP:@<NewPrimaryEmailAddress>

本範例會建立名稱為 "Fourth Coffee Recipients" 的電子郵件地址原則、將該原則指派給 Fourth Coffee 部門中的信箱使用者，並對該電子郵件地址原則設定最高優先順序，以便最先套用該原則。請注意，不會為這些收件者保留舊的主要電子郵件地址，因此他們無法在其舊的主要電子郵件地址收到電子郵件。

    New-EmailAddressPolicy -Name "Fourth Coffee Recipients" -Priority 1 -IncludedRecipients MailboxUsers -ConditionalDepartment "Fourth Coffee" -EnabledEmailAddressTemplates SMTP:@fourthcoffee.com

若要將新的電子郵件地址原則套用至受影響的收件者，請執行下列命令：

    Update-EmailAddressPolicy "Fourth Coffee Recipients"

## 如何才能了解此步驟是否正常運作？

若要確認您是否已成功設定授權網域的電子郵件地址原則，請執行下列其中一個動作：

  - 在 EAC 中，瀏覽至 **\[郵件流程\]** \> **\[電子郵件地址原則\]**。確認已依正確順序套用原則。此外，選取任何新的或更新的原則，並在詳細資料窗格中，確認電子郵件地址格式、包含的收件者，以及是否已套用原則。

  - 在命令介面中執行命令 **Get-EmailAddressPolicy** 和 `Get-EmailAddressPolicy "<Policy Name>"| Format-List`，以驗證原則的詳細資料。

## 如何才能了解此工作是否正常運作？

若要確認您是否已將 Exchange 設定為接受多個授權網域的郵件，請執行下列動作：

1.  從 Exchange 組織外的信箱傳送測試郵件至受影響的收件者。確認已成功接受郵件的電子郵件地址。

2.  將測試郵件從受影響的收件者信箱傳送至外部收件者，並確認郵件的「寄件者」地址。

