---
title: '使用命令介面中準備 MoveRequest.ps1 指令碼的跨樹系移動準備信箱: Exchange 2013 Help'
TOCTitle: 使用命令介面中準備 MoveRequest.ps1 指令碼的跨樹系移動準備信箱
ms:assetid: 2cea59fb-69b7-4a2f-833f-de4d93cf1810
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee861103(v=EXCHG.150)
ms:contentKeyID: 50472765
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用命令介面中準備 MoveRequest.ps1 指令碼的跨樹系移動準備信箱

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2017-11-22_

**摘要：** 了解如何管理跨樹系信箱移動和移轉Exchange 2013中的所述Exchange 管理命令介面準備 MoveRequest.ps1 指令碼。

Microsoft Exchange 2013支援信箱移動和移轉使用**New-MoveRequest**與**New-MigrationBatch** cmdlet。您也可以移動信箱透過 Exchange 系統管理中心 (EAC)。您可以從來源Exchange樹系移動 Exchange 2010 或 Exchange 2013 信箱，目標Exchange 2013樹系。

若要執行 **New-MoveRequest** 與 **New-MigrationBatch**指令程式，目標 Exchange 樹系中必須有郵件使用者，而且郵件使用者必須擁有最低的必要 Active Directory 屬性集。

範例Windows本主題所述的 PowerShell 指令碼支援這個工作同步處理至Exchange 2013目標樹系為擁有郵件功能的使用者的信箱使用者從Exchange 2013來源樹系。指令碼來源樹系中的信箱使用者的Active Directory屬性複製到目標樹系中，並將目標物件變成擁有郵件功能的使用者會使用**Update-Recipient** cmdlet。

如需使用和撰寫指令碼的詳細資訊，請參閱[使用 Exchange 管理命令介面撰寫指令碼](https://technet.microsoft.com/zh-tw/library/bb123798\(v=exchg.150\))。如需準備跨樹系移動的詳細資訊，請參閱[準備跨樹系移動要求的信箱](prepare-mailboxes-for-cross-forest-move-requests-exchange-2013-help.md)。

要尋找其他管理工作相關遠端移動要求嗎？取出[管理內部移動](manage-on-premises-moves-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 在下列位置找到指令碼： 程式 Files\\Microsoft\\Exchange Server\\V15\\Scripts

  - 若要執行此範例指令碼，您需要具備下列必要條件：
    
      - Exchange來源樹系、 信箱目前所在。這可以是 Exchange 2010 或 Exchange 2013 信箱。
    
      - 已安裝 Exchange 2013 的目標樹系 (信箱移動的目標)。

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


## 使用 Prepare-MoveRequest.ps1 指令碼準備信箱的跨樹系移動

從命令介面中執行指令碼執行Exchange 2013目標Exchange 2013樹系中的伺服器角色。指令碼會複製來源樹系中的信箱屬性。

若要指派特定的驗證認證的遠端樹系的網域控制站，必須先執行Windows PowerShell **Get-Credential**指令程式並儲存在暫存變數的使用者輸入。當您執行**Get-Credential**指令程式時，此指令程式會詢問使用者名稱與驗證遠端樹系的網域控制站與期間使用的帳戶密碼。您然後可以準備 MoveRequest.ps1 指令碼中使用之暫存變數。如需**Get-Credential**指令程式的詳細資訊，請參閱[Get-credential](https://go.microsoft.com/fwlink/p/?linkid=142122)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>呼叫此指令碼時，請確定對本機樹系和遠端樹系使用兩個單獨的認證。</td>
</tr>
</tbody>
</table>


1.  執行下列命令以取得本機樹系和遠端樹系認證。
    
        $LocalCredentials = Get-Credential
        $RemoteCredentials = Get-Credential

2.  執行下列命令，將認證資訊傳送到 Prepare-MoveRequest.ps1 指令碼中的 *LocalForestCredential* 與 *RemoteForestCredential*參數。
    
        Prepare-MoveRequest.ps1 -Identity JohnSmith@Fabrikan.com -RemoteForestDomainController DC001.Fabrikam.com -RemoteForestCredential $RemoteCredentials -LocalForestDomainController DC001.Contoso.com -LocalForestCredential $LocalCredentials

## 腳本參數集

下表描述指令碼的參數集。

### Prepare-MoveRequest.ps1 指令碼的參數集

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>參數</th>
<th>必要</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p><em>Identity</em>參數會唯一識別來源樹系中的信箱。Identity 可以是下列其中一項：</p>
<ul>
<li><p>一般名稱 (CN)</p></li>
<li><p>Alias</p></li>
<li><p><strong>proxyAddress</strong> 內容</p></li>
<li><p><strong>objectGuid</strong> 內容</p></li>
<li><p><strong>DisplayName</strong> 內容</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>RemoteForestCredential</em></p></td>
<td><p>必要</p></td>
<td><p><em>RemoteForestCredential</em> 參數可指定有權從來源樹系 Active Directory 複製資料的系統管理員。</p></td>
</tr>
<tr class="odd">
<td><p><em>RemoteForestDomainController</em></p></td>
<td><p>必要</p></td>
<td><p><em>RemoteForestDomainController</em> 參數可指定信箱所在來源樹系中的網域控制站。</p></td>
</tr>
<tr class="even">
<td><p><em>DisableEmailAddressPolicy</em></p></td>
<td><p>選用</p></td>
<td><p><em>DisableEmailAddressPolicy</em> 參數可指定在目標樹系中建立 <strong>MailUser</strong> 物件時，是否應停用可電子郵件地址原則 (EAP)。</p>
<p>如果指定此參數，則不會套用目標樹系中的 EAP。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>當您指定此參數時， <strong>MailUser</strong>物件不會加上戳記本機樹系網域中有電子郵件地址對應。這通常是由 EAP 上戳記。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="odd">
<td><p><em>LinkedMailUser</em></p></td>
<td><p>選用</p></td>
<td><p><em>LinkedMailUser</em> 參數可指定是否在本機樹系中為遠端樹系的信箱使用者建立連結的 MailUser。</p>
<p>如果提供參數，則指令碼會建立連結至來源信箱的目標<strong>MailUser</strong>物件。如果省略這個參數，指令碼會建立規則的目標<strong>MailUser</strong>物件。</p></td>
</tr>
<tr class="even">
<td><p><em>LocalForestCredential</em></p></td>
<td><p>選用</p></td>
<td><p><em>LocalForestCredential</em> 參數可指定有權對目標樹系 Active Directory 寫入資料的系統管理員。</p>
<p>建議您明確指定此參數，以避免 Active Directory 權限問題。</p>
<p>如果遠端樹系和本機樹系設定了信任關係，請勿將遠端樹系的使用者帳戶用作本機樹系認證，即使遠端使用者帳戶有權修改本機樹系中的 Active Directory，也是如此。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalForestDomainController</em></p></td>
<td><p>選用</p></td>
<td><p><em>LocalForestDomainController</em> 參數可指定目標樹系 (將在其中建立啟用郵件功能的使用者) 中的網域控制站。</p>
<p>建議您指定此參數，以避免本機樹系中出現可能的網域控制站複寫延遲問題，如果選取隨機網域控制站，可能會出現這些問題。</p></td>
</tr>
<tr class="even">
<td><p><em>MailboxDeliveryDomain</em></p></td>
<td><p>選用</p></td>
<td><p><em>MailboxDeliveryDomain</em> 參數可指定來源樹系的授權網域，以便指令碼可以選取正確來源信箱使用者的 <strong>proxyAddress</strong> 屬性作為啟用郵件功能的目標使用者的 <strong>targetAddress</strong> 屬性。</p>
<p>依預設，會將來源信箱使用者的主要 SMTP 位址設為啟用郵件功能的目標使用者的 <strong>targetAddress</strong> 屬性。</p></td>
</tr>
<tr class="odd">
<td><p><em>OverWriteLocalObject</em></p></td>
<td><p>選用</p></td>
<td><p><em>OverWriteLocalObject</em>參數用於Active Directory移轉工具所建立的使用者。屬性會從現有的郵件連絡人複製至新建立的郵件使用者。不過，此複本後, 指令碼亦將複製屬性從來源樹系的使用者至新建立的郵件使用者。</p></td>
</tr>
<tr class="even">
<td><p><em>TargetMailUserOU</em></p></td>
<td><p>選用</p></td>
<td><p><em>TargetMailuserOU</em> 參數可指定組織單位 (OU) (將在其下建立啟用郵件功能的目標使用者)。</p></td>
</tr>
<tr class="odd">
<td><p><em>UseLocalObject</em></p></td>
<td><p>選用</p></td>
<td><p>如果指令碼在本機樹系中偵測到與即將建立擁有郵件功能的使用者衝突的物件，<em>UseLocalObject</em> 參數可指定是否將現有本機物件轉換為需要的擁有郵件功能的目標使用者。</p></td>
</tr>
</tbody>
</table>


## 範例

本節包含如何使用 Prepare-MoveRequest.ps1 指令碼的數個範例。

## 範例： 單一連結擁有郵件功能的使用者

此範例在本機樹系中提供了一個已連結的啟用郵件功能的使用者，同時遠端樹系和本機樹系之間存在樹系信任。

1.  執行下列命令以取得本機樹系和遠端樹系認證。
    
        $LocalCredentials = Get-Credential
        $RemoteCredentials = Get-Credential

2.  執行下列命令，將認證資訊傳送到 Prepare-MoveRequest.ps1 指令碼中的 *LocalForestCredential* 與 *RemoteForestCredential* 參數。
    
        Prepare-MoveRequest.ps1 -Identity JamesAlvord@Contoso.com -RemoteForestDomainController DC001.Fabrikam.com -RemoteForestCredential $RemoteCredentials -LocalForestDomainController DC001.Contoso.com -LocalForestCredential $LocalCredentials -LinkedMailUser 

## 範例： 管線

如果您提供信箱識別碼的清單，則此範例支援管線。

1.  執行下列命令。
    
        $UserCredentials = Get-Credential

2.  執行下列命令，將認證資訊傳送到 Prepare-MoveRequest.ps1 指令碼中的 *RemoteForestCredential* 參數。
    
        "IanP@Contoso.com", "JoeAn@Contoso.com" | Prepare-MoveRequest.ps1 -RemoteForestDomainController DC001.Fabrikam.com -RemoteForestCredential $UserCredentials

## 範例： 使用.csv 檔案大量建立擁有郵件功能的使用者

您可以從來源樹系產生包含信箱識別碼清單的 .csv 檔案，從而可以將此檔案內容以管線傳輸至指令碼，以大量建立啟用郵件功能的目標使用者。

例如，.csv 檔案的內容可以是：

識別碼

Ian@contoso.com

John@contoso.com

Cindy@contoso.com

此範例可呼叫 .csv 檔案，以大量建立啟用郵件功能的目標使用者。

1.  執行下列命令以取得遠端樹系認證。
    
        $UserCredentials = Get-Credential

2.  執行下列命令，將認證資訊傳送到 Prepare-MoveRequest.ps1 指令碼中的 *RemoteForestCredential* 參數。
    
        Import-Csv Test.csv | Prepare-MoveRequest.ps1 -RemoteForestDomainController DC001.Fabrikam.com -RemoteForestCredential $UserCredentials

## 依據目標物件的指令碼行為

本節描述目標物件出現數種情況時，指令碼如何執行。

## 存在重複的啟用郵件功能的目標物件

如果指令碼嘗試從來源信箱使用者建立啟用郵件功能的目標使用者，且偵測到存在重複的啟用郵件功能的本機物件，則會使用以下邏輯：

  - 如果來源信箱使用者的 **masterAccountSid** 屬性等於任何目標物件的 **objectSid** 或 **masterAccountSid** 屬性，則：
    
      - 如果目標物件未擁有郵件功能，則指令碼將傳回錯誤，因為指令碼不支援將未擁有郵件功能的物件轉換為擁有郵件功能的使用者。
    
      - 如果目標物件已啟用郵件功能，則該目標物件為重複物件。

  - 如果來源信箱使用者的 **proxyAddress** 內容 (僅 smtp/x500) 中的位址等於目標物件的 **proxyAddress** 內容 (僅 smtp/x500) 中的位址，則該目標物件為重複物件。

指令碼將提示使用者存在重複的物件。

如果擁有郵件功能的目標物件是擁有郵件功能的使用者或連絡人，則很可能是由跨樹系 (以 Identity Lifecycle Management 2007 Service Pack 1 為基礎) 全域通訊清單 (GAL) 同步處理部署建立的，使用者可以使用 *UseLocalObject* 參數再次執行指令碼，以使用擁有郵件功能的目標物件進行信箱移轉。

## 啟用郵件功能的使用者

如果目標物件是啟用郵件功能的使用者，指令碼會將以下屬性從來源信箱使用者複製到啟用郵件功能的目標使用者：

  - **msExchMailboxGUID**

  - **msExchArchiveGUID**

  - **msExchArchiveName**

如果設定 *LinkedMailUser* 參數，指令碼會複製來源 **objectSid**/**masterAccountSid** 屬性。

## 啟用郵件功能的連絡人

如果目標物件是一個擁有郵件功能的連絡人，指令碼會刪除現有的連絡人並將其所有屬性都複製到新郵件功能的使用者。指令碼也會從來源信箱使用者複製下列屬性：

  - **msExchMailboxGUID**

  - **msExchArchiveGUID**

  - **msExchArchiveName**

  - **sAMAccountName**

  - **userAccountControl** (設為 514 //相當於 0x202, ACCOUNTDISABLE | NORMAL\_ACCOUNT)

  - **userPrincipalName**

如果設定 *LinkedMailUser* 參數，指令碼會複製來源 **objectSid**/**masterAccountSid** 屬性。

## LegacyExchangeDN 屬性

當呼叫**Update-Recipient**指令程式時若要將目標物件轉換成擁有郵件功能的使用者時，目標郵件功能的使用者產生新的**LegacyExchangeDN**屬性。指令碼複製的目標所擁有郵件功能的使用者作為 x500 **LegacyExchangeDN**屬性至來源信箱使用者的**proxyAddress**屬性的地址。

