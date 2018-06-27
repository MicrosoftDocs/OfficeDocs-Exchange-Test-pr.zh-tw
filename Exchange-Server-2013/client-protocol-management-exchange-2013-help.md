---
title: '用戶端通訊協定管理: Exchange 2013 Help'
TOCTitle: 用戶端通訊協定管理
ms:assetid: 89ba6d24-d1d3-46d5-a0ae-61f0d4c6df21
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ657727(v=EXCHG.150)
ms:contentKeyID: 50473688
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 用戶端通訊協定管理

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

管理 Exchange ActiveSync、 Outlook Web App、 POP3、 IMAP4、 自動探索服務、 Exchange Web 服務及可用性服務的用戶端通訊協定發生在三個不同的區域： Exchange 系統管理中心 (EAC)、 Exchange 管理命令介面及網際網路資訊服務 (IIS) 管理員\]。管理每個位置中的設定而異每個用戶端通訊協定。

## 管理 Outlook Web App 設定

大部分的設定會影響 Outlook Web App 的功能可用的使用者可以在 Outlook Web App 虛擬目錄上設定或可設定在 Outlook Web App 信箱原則。使用 Outlook Web App 信箱原則，您可以個別使用者定義的可用功能。信箱原則設定會覆寫虛擬目錄設定。如需有關管理 Outlook Web App 的詳細資訊，請參閱[Outlook Web App](outlook-web-app-exchange-2013-help.md)。

## 管理 Exchange ActiveSync 設定

在 Exchange 2010、 所有的用戶端存取通訊協定所實作及單一伺服器角色、 用戶端存取伺服器角色上進行管理。在 IIS 單一執行個體上執行的通訊協定管理、 有單一的虛擬目錄物件在 Active Directory 中的每個用戶端通訊協定及指令程式的單一集會用來設定虛擬目錄。

Exchange 2013、 Exchange ActiveSync 用戶端通訊協定管理會分別 Client Access server 和 Mailbox server。因為此架構變更，而您可以在 Client Access server 和 Mailbox server 上執行不同的虛擬目錄的管理工作。如果這些兩個伺服器未安裝在同一部實體電腦上，您指令程式會變更的虛擬目錄搭配使用的參數會根據在其執行這些伺服器的伺服器角色。

如需 Exchange 2013 中之架構變更的相關資訊，請參閱[Exchange 2013 的新功能](what-s-new-in-exchange-2013-exchange-2013-help.md)。

Exchange ActiveSync 虛擬目錄可套用的設定有兩類：

  - 適用於信箱工作階段的設定

  - 適用於伺服器和虛擬目錄的設定

適用於信箱工作階段的設定是使用者工作階段設定。當使用者連接至用戶端存取伺服器時、 連線代理包含使用者信箱的信箱伺服器。虛擬目錄的唯一識別碼所含的代理的要求。Mailbox server 然後從 Active Directory 擷取虛擬目錄設定，並將其套用至工作階段。虛擬目錄設定快取來增進效能的 Mailbox server 上。

如果連線被另一個 Active Directory 站台代理，就會從與信箱伺服器位在同一個站台的用戶端伺服器載入虛擬目錄設定，而不是從建立連線的用戶端伺服器載入虛擬目錄設定。

下表指出哪些虛擬目錄設定可管理哪些伺服器上。如果您嘗試要管理其不適用的伺服器上的特定設定，您會收到錯誤訊息指出您嘗試要設定的屬性唯讀的進行操作的伺服器。

**用戶端存取伺服器上的 Exchange ActiveSync 虛擬目錄設定**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>設定</th>
<th>伺服器</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>BadItemReportingEnabled</p></td>
<td><p>用戶端存取</p></td>
</tr>
<tr class="even">
<td><p>BasicAuthEnabled</p></td>
<td><p>用戶端存取</p></td>
</tr>
<tr class="odd">
<td><p>ClientCertAuth</p></td>
<td><p>用戶端存取</p></td>
</tr>
<tr class="even">
<td><p>CompressionEnabled</p></td>
<td><p>用戶端存取</p></td>
</tr>
<tr class="odd">
<td><p>ExternalAuthenticationMethods</p></td>
<td><p>用戶端存取</p></td>
</tr>
<tr class="even">
<td><p>ExternalURL</p></td>
<td><p>用戶端存取</p></td>
</tr>
<tr class="odd">
<td><p>InternalAuthenticationMethods</p></td>
<td><p>用戶端存取</p></td>
</tr>
<tr class="even">
<td><p>InternalURL</p></td>
<td><p>用戶端存取</p></td>
</tr>
<tr class="odd">
<td><p>MobileClientCertificateAuthorityURL</p></td>
<td><p>用戶端存取</p></td>
</tr>
<tr class="even">
<td><p>MobileClientCertificateProvisioningEnabled</p></td>
<td><p>用戶端存取</p></td>
</tr>
<tr class="odd">
<td><p>MobileClientCertTemplateName</p></td>
<td><p>用戶端存取</p></td>
</tr>
<tr class="even">
<td><p>RemoteDocumentsActionForUnknownServers</p></td>
<td><p>用戶端存取</p></td>
</tr>
<tr class="odd">
<td><p>RemoteDocumentsAllowedServers</p></td>
<td><p>用戶端存取</p></td>
</tr>
<tr class="even">
<td><p>RemoteDocumentsBlockedServers</p></td>
<td><p>用戶端存取</p></td>
</tr>
<tr class="odd">
<td><p>RemoteDocumentsInternalDomainSuffixList</p></td>
<td><p>用戶端存取</p></td>
</tr>
<tr class="even">
<td><p>SendWatsonReport</p></td>
<td><p>用戶端存取</p></td>
</tr>
</tbody>
</table>


**用戶端存取和信箱伺服器上的 Exchange ActiveSync 虛擬目錄設定**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>設定</th>
<th>伺服器</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ApplicationRoot</p></td>
<td><p>用戶端存取與信箱</p></td>
</tr>
<tr class="even">
<td><p>AppPoolID</p></td>
<td><p>用戶端存取與信箱</p></td>
</tr>
<tr class="odd">
<td><p>MetabasePath</p></td>
<td><p>用戶端存取與信箱</p></td>
</tr>
<tr class="even">
<td><p>Name</p></td>
<td><p>用戶端存取與信箱</p></td>
</tr>
<tr class="odd">
<td><p>Path</p></td>
<td><p>用戶端存取與信箱</p></td>
</tr>
<tr class="even">
<td><p>ProxySubVdir</p></td>
<td><p>用戶端存取與信箱</p></td>
</tr>
<tr class="odd">
<td><p>VirtualDirectoryName</p></td>
<td><p>用戶端存取與信箱</p></td>
</tr>
<tr class="even">
<td><p>WebsiteName</p></td>
<td><p>用戶端存取與信箱</p></td>
</tr>
</tbody>
</table>


## 管理 POP3 及 IMAP4 設定

Exchange 2013，在具有也已 POP3 與 IMAP4 通訊協定的實作區分之間的用戶端存取和信箱伺服器角色。由於實作新 POP3 和 IMAP4 連線是每個受管理的服務在用戶端存取伺服器上，以及由 Mailbox server 上的服務。用戶端存取伺服器上執行的服務名稱是存在於 Exchange 2010 中的名稱相同 ︰ Microsoft Exchange IMAP4 服務和 Microsoft Exchange POP3 服務。在信箱伺服器執行兩個新的服務名稱是 Microsoft Exchange IMAP4 後端服務和 Microsoft Exchange POP3 後端服務。

當您管理組織中的 POP3 和 IMAP4 連線時請考慮以下事項：

  - 如果您在同一台電腦上執行用戶端存取伺服器角色和信箱伺服器角色，針對 POP3 或 IMAP4 設定所作的所有變更都會自動套用到正確的 POP3 和 IMAP4 服務中。

  - 如果您在不同的電腦上執行用戶端存取伺服器角色和信箱伺服器角色，您必須在管理變更設定的電腦上管理設定。

使用下表指出每一個伺服器角色的 POP/IMAP 設定為何。

**用戶端存取伺服器上的 POP3 和 IMAP4 設定**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>設定</th>
<th>伺服器</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AuthenticatedConnectionTimeout</p></td>
<td><p>用戶端存取</p></td>
</tr>
<tr class="even">
<td><p>Banner</p></td>
<td><p>用戶端存取</p></td>
</tr>
<tr class="odd">
<td><p>ExternalConnectionSettings</p></td>
<td><p>用戶端存取</p></td>
</tr>
<tr class="even">
<td><p>InternalConnectionSettings</p></td>
<td><p>用戶端存取</p></td>
</tr>
<tr class="odd">
<td><p>MaxCommandSize</p></td>
<td><p>用戶端存取</p></td>
</tr>
<tr class="even">
<td><p>MaxConnectionFromSingleIP</p></td>
<td><p>用戶端存取</p></td>
</tr>
<tr class="odd">
<td><p>MaxConnections</p></td>
<td><p>用戶端存取</p></td>
</tr>
<tr class="even">
<td><p>MaxConnectionsPerUser</p></td>
<td><p>用戶端存取</p></td>
</tr>
<tr class="odd">
<td><p>PreAuthenticatedConnectionTimeout</p></td>
<td><p>用戶端存取</p></td>
</tr>
<tr class="even">
<td><p>UnencryptedOrTLSBindings</p></td>
<td><p>用戶端存取</p></td>
</tr>
</tbody>
</table>


**信箱伺服器上的 POP3 和 IMAP4 設定**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>設定</th>
<th>伺服器</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CalendarItemRetrivalOption</p></td>
<td><p>信箱</p></td>
</tr>
<tr class="even">
<td><p>EnableExactRFC822Size</p></td>
<td><p>信箱</p></td>
</tr>
<tr class="odd">
<td><p>MessageRetrievalSortOrder</p></td>
<td><p>信箱</p></td>
</tr>
<tr class="even">
<td><p>OWAServerURL</p></td>
<td><p>信箱</p></td>
</tr>
<tr class="odd">
<td><p>ProxyTargetPort</p></td>
<td><p>信箱</p></td>
</tr>
<tr class="even">
<td><p>ShowHiddenFoldersEnabled</p></td>
<td><p>信箱</p></td>
</tr>
<tr class="odd">
<td><p>SuppressReadReceipt</p></td>
<td><p>信箱</p></td>
</tr>
</tbody>
</table>


**用戶端存取和信箱伺服器上的 POP3 和 IMAP4 設定**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>設定</th>
<th>伺服器</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>X509CertificateName</p></td>
<td><p>用戶端存取與信箱</p></td>
</tr>
<tr class="even">
<td><p>EnforceCertificateErrors</p></td>
<td><p>用戶端存取與信箱</p></td>
</tr>
<tr class="odd">
<td><p>LogFileLocation</p></td>
<td><p>用戶端存取與信箱</p></td>
</tr>
<tr class="even">
<td><p>LogFileRolloverSettings</p></td>
<td><p>用戶端存取與信箱</p></td>
</tr>
<tr class="odd">
<td><p>LoginType</p></td>
<td><p>用戶端存取與信箱</p></td>
</tr>
<tr class="even">
<td><p>LogPerFileSizeQuota</p></td>
<td><p>用戶端存取與信箱</p></td>
</tr>
<tr class="odd">
<td><p>ProotocolLogEnabled</p></td>
<td><p>用戶端存取與信箱</p></td>
</tr>
<tr class="even">
<td><p>Server</p></td>
<td><p>用戶端存取與信箱</p></td>
</tr>
<tr class="odd">
<td><p>X509CertificateName</p></td>
<td><p>用戶端存取與信箱</p></td>
</tr>
</tbody>
</table>

