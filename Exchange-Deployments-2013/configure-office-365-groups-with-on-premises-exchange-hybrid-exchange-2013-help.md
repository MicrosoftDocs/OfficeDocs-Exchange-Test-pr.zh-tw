---
title: '使用內部部署 Exchange 混合式設定 Office 365 群組: Exchange 2013 Help'
TOCTitle: 使用內部部署 Exchange 混合式設定 Office 365 群組
ms:assetid: 184dfcfe-4b8e-450a-adc6-e647213b9501
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Mt668829(v=EXCHG.150)
ms:contentKeyID: 72513047
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 使用內部部署 Exchange 混合式設定 Office 365 群組

 

_<strong>上次修改主題的時間：</strong>2016-12-06_

了解如何讓內部部署的 Exchange 使用者可以在混和式部署中使用 Office 365 群組。

群組是 Office 365 服務，讓小組可以輕易地通訊、排程會議，以及對文件進行共用作業。與群組共用的所有資訊，從傳送給群組的電子郵件訊息，到儲存在群組的商務用 OneDrive 或 SharePoint 文件庫中的檔案，都可供群組的任何成員取用。如果您在內部部署 Exchange 組織與 Office 365 之間設定混合式部署，您可以讓在 Office 365 中建立的群組可供您的內部部署使用者使用，方法是遵循本主題中的步驟。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ906432.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用 Office 365 群組與 Exchange 混合式部署中的內部部署使用者，是一項新功能。因為它是新功能，您可能會在設定時遇到一些問題。請務必參閱本主題結尾的已知問題章節，以修正您可能會遇到的問題。</td>
</tr>
</tbody>
</table>


## 必要條件

在開始之前，請確定已完成下列項目︰

  - 為您的租用戶購買 Azure Active Directory 進階授權。這樣才能啟用在 Azure Active Directory Connect 中的群組回寫功能。

  - 設定您的 Exchange 內部部署組織與 Office 365 之間的混合式部署，並且確認其運作正常。如需 Exchange 混合式部署的詳細資訊，請參閱下列項目：
    
      - [Exchange Server 混合部署](exchange-server-hybrid-deployments-exchange-2013-help.md)
    
      - [混合部署必要條件](hybrid-deployment-prerequisites-exchange-2013-help.md)

  - 已安裝支援的 Exchange 內部部署 Exchange 版本，與 Office 365 群組的整合可用於 CU1 和更新版本的 Exchange 2016，以及 CU11 和更新版本的 Exchange 2013。然而，Exchange 混合式需要最新的 Exchange 2013 或 Exchange 2016 累積更新 (CU) 安裝在您的內部部署 Exchange 伺服器上。如果您無法安裝最新的 CU，可以使用目前的 CU 之前發行的更新。

  - 使用 Azure Active Directory Connect (Azure AD Connect) 設定單一登入。需要這個設定以允許使用者按一下群組電子郵件訊息中的**檢視群組檔案**或雲端附件連結。
    
    在 Exchange 混合式部署中設定單一登入 Azure AD Connect 時，我們建議您使用密碼同步化。Active Directory 同盟服務 (AD FS) 只應該用於下列情況：如果您身處於大型組織；如果您擁有複雜的內部部署 Active Directory 部署 (例如，多個 Active Directory 樹系)；如果另一個 Microsoft 產品需要 AD FS 與 Office 365 搭配使用；或者，如果基於合規性政策，您無法在內部部署網路之外同步密碼。如需單一登入的詳細資訊，請參閱[整合內部部署身分識別與 Azure Active Directory](http://go.microsoft.com/fwlink/p/?linkid=723513)。

## 在 Azure AD Connect 中啟用群組回寫

1.  在 Azure AD Connect 精靈中，選取 **\[自訂同步處理選項\]**，然後按 **\[下一步\]**。

2.  在**連線到 Azure AD** 頁面上，輸入您的 Office 365 和內部部署認證。按 **\[下一步\]**。

3.  在 **\[選擇性功能\]** 頁面上，確認您先前設定的選項仍然選取。最常選取的選項是 **\[Exchange 混合式\]** 和 **\[密碼雜湊同步化\]**。

4.  選取 **\[群組回寫\]**，然後按 **\[下一步\]**。

5.  在 **\[回寫\]** 頁面上，選取一個 Active Directory 組織單位用來儲存從 Office 365 同步處理至您的內部部署組織的物件，然後按 **\[下一步\]**。

6.  在 **\[準備設定\]** 頁面上，按一下 **\[設定\]**。

7.  精靈完成時，按一下 **\[組態完成\]** 頁面上的 **\[結束\]**。

8.  在 Active Directory 網域控制站上開啟 \[Active Directory 使用者和電腦\]，並尋找以 **AAD\_** 開頭的使用者帳戶。記下這個帳戶的名稱。

9.  在內部部署 Exchange 伺服器上開啟 Exchange 管理命令介面，並且執行下列命令。
    
        $AzureADConnectSWritebackAccount = <AAD_ account name from step 8>
        
        $GroupsOU = <writeback Active Directory OU selected in step 5>
        
        Import-Module "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1"
        
        Initialize-ADSyncGroupWriteBack -ADConnectorAccount $AzureADConnectSWritebackAccount -GroupWriteBackContainerDN $GroupsOU

## 設定群組網域

主要的 SMTP 網域的 Office 365 群組稱為*群組網域*。根據預設，已選擇預設公認的網域作為您組織中的群組網域。如果您想要新增專用的群組網域時，可以使用下列步驟加入網域。如需多網域支援 Office 365 群組的詳細資訊，請參閱[多網域支援 Office 365 群組](https://support.office.com/zh-tw/article/multi-domain-support-for-office-365-groups-admin-help-7cf5655d-e523-4bc3-a93b-3ccebf44a01a)

1.  將新網域新增至您的 Office 365 組織。如需將網域新增至 Office 365 的說明，請參閱[在 Office 365 中新增使用者和網域](https://support.office.com/zh-tw/article/add-your-users-and-domain-to-office-365-6383f56d-3d09-4dcb-9b41-b5f5a5efd611)

2.  使用下列命令，在您的內部部署 Exchange 組織中新增群組網域作為公認的網域。這樣才能讓混合式傳送連接器可用來將外寄郵件傳送到 Office 365 中的群組網域。
    
        New-AcceptedDomain -Name groups.contoso.com -DomainName groups.contoso.com -DomainType InternalRelay

3.  使用您的 DNS 提供者建立下列公用 DNS 記錄。
    
    
    <table>
    <colgroup>
    <col style="width: 33%" />
    <col style="width: 33%" />
    <col style="width: 33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><p>DNS 記錄名稱</p></th>
    <th><p>DNS 記錄類型</p></th>
    <th><p>DNS 記錄值</p></th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>groups.contoso.com</p></td>
    <td><p>MX</p></td>
    <td><p>groups-contoso-com.mail.protection.outlook.com</p>
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ150559.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>這個 DNS 記錄值的格式是 <em>&lt;domain key&gt;</em>.mail.protection.outlook.com。若要找出您的網域金鑰，請參閱<a href="https://support.office.com/zh-tw/article/gather-the-information-you-need-to-create-office-365-dns-records-77f90d4a-dc7f-4f09-8972-c1b03ea85a67">收集建立 Office 365 DNS 記錄所需的資訊</a>。</td>
    </tr>
    </tbody>
    </table>

</td>
    </tr>
    <tr class="even">
    <td><p>autodiscover.groups.contoso.com</p></td>
    <td><p>CNAME</p></td>
    <td><p>autodiscover.outlook.com</p></td>
    </tr>
    </tbody>
    </table>
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Mt668829.Caution(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果群組網域的 MX DNS 記錄設定為內部部署 Exchange 伺服器，內部部署 Exchange 組織與 Office 365 群組中使用者之間的郵件流程不會正常運作。</td>
    </tr>
    </tbody>
    </table>


4.  使用下列命令，將群組網域新增至混合式傳送連接器，該連接器是由內部部署 Exchange 組織中的混合式組態精靈所建立。
    
        Set-SendConnector -Identity "Outbound to Office 365" -AddressSpaces "contoso.mail.onmicrosoft.com","groups.contoso.com"
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ150559.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果沒有更新傳送連接器，或如果群組網域未新增為內部部署 Exchange 組織中公認的網域，則從內部部署信箱傳送的郵件不會傳遞至群組，除非該群組已設定為接收來自外部寄件者的郵件。</td>
    </tr>
    </tbody>
    </table>


## 如何知道這是否正常運作？

若要確定群組會使用 Exchange 混合式部署，您應該使用內部部署信箱，以及使用從內部部署組織移至 Office 365 的信箱測試它們。使用下列各節的步驟，來執行每項測試。

## 使用內部部署信箱進行測試

1.  將內部部署信箱新增至 Office 365 群組。

2.  將 Office 365 信箱新增至相同的 Office 365 群組。

3.  使用網頁型 Outlook 登入 Office 365 信箱。

4.  使用 Office 365 信箱將訊息張貼至群組。

5.  使用 Outlook 2016 或網頁型 Outlook 開啟內部部署信箱。

6.  請確認收到電子郵件訊息的信箱包含傳送到 Office 365 群組的文章。

7.  在同一個信箱中，撰寫郵件的回覆，將它傳送給群組。

8.  請確認訊息可以由群組的所有成員檢視。

## 使用移至 Office 365 的信箱進行測試

1.  將信箱從內部部署 Exchange 組織移至 Office 365。

2.  將信箱新增至 Office 365 群組。

3.  在新的瀏覽器工作階段，登入已移至 Office 365 的信箱。

4.  在網頁型 Outlook 中，確認群組列在左側的導覽列。

5.  將訊息張貼至群組。

6.  請確認訊息可以由群組的所有成員檢視。

## 已知問題

  - **群組不會針對移至 Office 365 的信箱顯示** 當使用者從內部部署 Exchange 組織移至 Office 365 時，群組不會出現在 Outlook 或網頁型 Outlook 的左側瀏覽窗格中。若要修正這個問題，從它是其成員的任何群組中移除信箱，並將它重新新增至每個群組。

  - **新的群組不會出現在內部部署 Exchange 全域通訊清單 (GAL) 中** 在 Office 365 中建立新的群組時，它不會自動出現在內部部署 GAL。若要修正這個問題，在內部部署 Exchange 伺服器上開啟 Exchange 管理命令介面，並且執行下列命令。
    
        Update-Recipient "<group name>"

  - **群組不會接收來自內部部署使用者的郵件** 當下列條件成立時，內部部署使用者將無法傳送郵件給 Office 365 群組：
    
      - 群組網域已設定為內部部署 Exchange 組織中的授權網域。
    
      - 群組最近才建立，它的資訊尚未回寫至內部部署 Active Directory。
    
    當 Azure AD Connect 執行 Office 365 與您的內部部署組織之間的下次同步處理時，這個問題就會自行解決。Azure AD Connect 同步處理每 30 分鐘進行一次。

  - **內部部署使用者無法使用包含在群組訊息頁尾的連結**內部部署使用者無法使用**檢視群組對話**或**取消訂閱**連結，這些連結包含在傳送給他們的每個群組訊息頁尾。若要從群組取消訂閱，內部部署使用者需要連絡群組管理員。

  - **傳送給群組的次要 SMTP 地址的郵件無法傳遞** 當多個電子郵件地址新增至群組時，只有主要 SMTP 地址會回寫至您的內部部署 Active Directory。如果內部部署使用者嘗試傳送訊息給群組的次要 SMTP 地址，將無法傳遞訊息。若要避免這個問題，請在每個群組上僅設定一個 SMTP 地址。

  - **內部部署使用者無法成為群組的系統管理員** 內部部署使用者無法直接存取群組空間。因此，它們無法新增為群組的系統管理員。

  - **如果您已啟用集中式郵件流程，外部郵件傳遞至群組可能會失敗**如果已啟用集中式郵件流程，即使群組允許來自外部寄件者的郵件，由外部使用者傳送到群組的郵件仍無法傳遞。

  - **內部部署使用者無法作為群組傳送郵件** 嘗試以 Office 365 群組傳送訊息的內部部署使用者，將會收到沒有使用權限的錯誤，即使他們在群組上指定有 Send As 權限。群組上的 Send As 權限只適用於 Exchange Online 信箱使用者。

  - **從 Outlook 的左方瀏覽窗格中選取一個群組並不會開啟該群組的信箱** Outlook 會使用自動探索 URL 來開啟群組信箱。如果群組的主要電子郵件地址位於未指向 Office 365 自動探索 URL (autodiscover.outlook.com) 的網域中，則 Outlook 無法開啟群組的信箱。若要修正這個問題，群組可以在指向 Office 365 自動探索 URL 的網域中佈建主要地址。您可以設定電子郵件地址原則，對指向 Office 365 自動探索 URL 的每個群組信箱新增主要電子郵件地址。如需詳細資訊，請參閱[多網域支援 Office 365 群組](https://support.office.com/zh-tw/article/multi-domain-support-for-office-365-groups-admin-help-7cf5655d-e523-4bc3-a93b-3ccebf44a01a)。

