---
title: 'Exchange 2013 部署權限參考: Exchange 2013 Help'
TOCTitle: Exchange 2013 部署權限參考
ms:assetid: b13412d0-0cc4-4c1d-bf31-cae3d3e211a9
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ee681663(v=EXCHG.150)
ms:contentKeyID: 59637262
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013 部署權限參考

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

本主題說明設定 Microsoft Exchange Server 2013 組織所需的權限。與管理角色群組相關聯的萬用安全性群組 (USG)，以及其他 Windows 安全性群組與安全性主體，都會新增到各種 Active Directory 物件的存取控制清單 (ACL) 中。ACL 會控制每個物件上能夠執行的作業。了解已將哪些權限授與每個角色群組、安全性群組或安全性主體，即可判斷安裝 Exchange 2013 所需的最低權限。

在某些情況下，ACL 不會套用至慣用的 **ntSecurityDescriptor** 內容，而是套用至其他內容 (例如 **msExchMailboxSecurityDescriptor**)。目錄服務無法強制執行 Windows 安全性描述元中未指定的安全性。在大多數情況下，儲存服務會複寫 ACL 並儲存到適當的物件上。可惜的是，沒有任何工具能夠使用原始二進位資料格式以外的格式檢視這些 ACL。

每個權限表的欄位都包含下列資訊：

  - **帳戶**   授與或拒絕權限的安全性主體。

  - **ACE 類型**   存取控制項目 (ACE) 類型
    
      - **允許 ACE**   允許 ACE 可讓與 ACE 相關聯的使用者或群組存取項目。
    
      - **拒絕 ACE**   拒絕 ACE 可防止與 ACE 相關聯的使用者或群組存取項目。

  - **繼承**   用於子物件的繼承類型。
    
      - \[全部\] 表示權限會套用至物件及所有子物件。
    
      - **\[描述\]** 表示權限會套用至 \[屬性/套用至\] 資料列中所列的物件類別。
    
      - \[無\] 表示權限只會套用至物件。

  - **權限**   授與帳戶的權限。

  - **開啟內容/套用至**   在某些情況下，權限只會套用至指定的內容、內容設定或物件類別。這些受限制的權限可在此指定。

  - **註解**   此欄位會適當地說明為何需要權限，或者提供權限的其他相關資訊。

權限通常是依照 Active Directory 服務介面 (ADSI) 編輯器 (AdsiEdit.msc)，\[檢視/編輯\] 索引標籤上 \[進階\] 檢視中的 \[安全性\] 內容頁所使用的名稱，在表格中列出。ADSI 編輯器 \[安全性\] 內容頁列出權限的更簡要檢視。LDP 工具 (Ldp.exe) 會直接將存取遮罩顯示為數值。安裝代碼依預先定義的常數參考權限。

下表顯示這些值之間的關係。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>ADSI 編輯器摘要頁面</th>
<th>ADSI 編輯器進階檢視，檢視/編輯索引標籤</th>
<th>套用至指定物件的 ACL 項目</th>
<th>二進位值 (LDP 中的存取遮罩)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>完全控制</p></td>
<td><p>完全控制</p></td>
<td><p><code>WRITE_OWNER | WRITE_DAC | READ_CONTROL | DELETE | ACTRL_DS_CONTROL_ACCESS | ACTRL_DS_LIST_OBJECT | ACTRL_DS_DELETE_TREE | ACTRL_DS_WRITE_PROP | ACTRL_DS_READ_PROP | ACTRL_DS_SELF | ACTRL_DS_LIST | ACTRL_DS_DELETE_CHILD | ACTRL_DS_CREATE_CHILD</code></p></td>
<td><p><code>0x000F01FF</code></p></td>
</tr>
<tr class="even">
<td><p>閱讀</p></td>
<td><p>清單內容 + 讀取所有內容 + 讀取權限</p></td>
<td><p><code>ACTRL_DS_LIST | ACTRL_DS_READ_PROP | READ_CONTROL</code></p></td>
<td><p><code>0x00020014</code></p></td>
</tr>
<tr class="odd">
<td><p>寫入</p></td>
<td><p>寫入所有內容 + 所有已驗證的寫入</p></td>
<td><p><code>ACTRL_DS_WRITE_PROP | ACTRL_DS_SELF</code></p></td>
<td><p><code>0x00000028</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>列出內容</p></td>
<td><p><code>ACTRL_DS_LIST</code></p></td>
<td><p><code>0x00000004</code></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>讀取所有內容</p></td>
<td><p><code>ACTRL_DS_READ_PROP</code></p></td>
<td><p><code>0x00000010</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>寫入所有內容</p></td>
<td><p><code>ACTRL_DS_WRITE_PROP</code></p></td>
<td><p><code>0x00000020</code></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>刪除</p></td>
<td><p><code>DELETE</code></p></td>
<td><p><code>0x00010000</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>刪除樹狀子目錄</p></td>
<td><p><code>ACTRL_DS_DELETE_TREE</code></p></td>
<td><p><code>0x00000040</code></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>讀取權限</p></td>
<td><p><code>READ_CONTROL</code></p></td>
<td><p><code>0x00020000</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>修改權限</p></td>
<td><p><code>WRITE_DAC</code></p></td>
<td><p><code>0x00040000</code></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>修改擁有者</p></td>
<td><p><code>WRITE_OWNER</code></p></td>
<td><p><code>0x00080000</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>所有已驗證的寫入</p></td>
<td><p><code>ACTRL_DS_SELF</code></p></td>
<td><p><code>0x00000008</code></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>所有延伸權利</p></td>
<td><p><code>ACTRL_DS_CONTROL_ACCESS</code></p></td>
<td><p><code>0x00000100</code></p></td>
</tr>
<tr class="even">
<td><p>建立所有子物件</p></td>
<td><p>建立所有子物件</p></td>
<td><p><code>ACTRL_DS_CREATE_CHILD</code></p></td>
<td><p><code>0x00000001</code></p></td>
</tr>
<tr class="odd">
<td><p>刪除所有子物件</p></td>
<td><p>刪除所有子物件</p></td>
<td><p><code>ACTRL_DS_DELETE_CHILD</code></p></td>
<td><p><code>0x00000002</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p></p></td>
<td><p><code>ACTRL_DS_LIST_OBJECT</code></p></td>
<td><p><code>0x00000080</code></p></td>
</tr>
</tbody>
</table>


延伸權利是個別應用程式指定的自訂權利。這些權利是在 ACL 中指定。不過，這些權利對 Active Directory 而言沒有作用。特定應用程式會強制執行所有延伸權利。「建立公用資料夾」或「在資訊儲存庫中建立具名內容」都是 Exchange 延伸權利的例子。

如需 Microsoft Exchange Server 2010安裝過程所設定的權限的資訊，請參閱[Exchange 2010 部署權限參考](https://go.microsoft.com/fwlink/p/?linkid=402924)。

## 準備 Active Directory 權限

本節的權限表會顯示您執行 `Setup /PrepareAD` 命令時設定的權限。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>本節描述的權限是您使用共用權限模式部署 Exchange 2013 時所設定的預設權限。如果是使用 Active Directory 分割權限模式來部署 Exchange 2013，則預設的權限會不同。如需有關使用 Active Directory 分割權限時預設權限變更的詳細資訊，以及共用和分割權限模式的整體資訊，請參閱＜<a href="understanding-split-permissions-exchange-2013-help.md">了解分割權限</a>＞中的＜<a href="understanding-split-permissions-exchange-2013-help.md">Active Directory split permissions</a>＞。如果您安裝 Exchange 時未選擇使用 Active Directory 分割權限，Exchange 會使用共用權限。</td>
</tr>
</tbody>
</table>


## Microsoft Exchange 容器權限

下表顯示組態磁碟分割內的 Microsoft Exchange 容器上設定的權限。

### 物件的辨別名稱：CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<domain\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>帳戶</th>
<th>ACE 類型</th>
<th>繼承</th>
<th>權限</th>
<th>開啟內容/套用至</th>
<th>註解</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Installation Account</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>完全控制</p></td>
<td><p></p></td>
<td><p>這是用來執行 <code>/PrepareAD</code> 的帳戶。</p></td>
</tr>
<tr class="even">
<td><p>組織管理</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>完全控制</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>完全控制</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Authenticated Users</p></td>
<td><p>允許 ACE</p></td>
<td><p>無</p></td>
<td><p>讀取內容</p>
<p>列出內容</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>修改權限</p></td>
<td><p>msExchSmtpRceiveConnector</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Public Folder Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取</p>
<p>列出物件</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Delegated Setup</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取</p>
<p>列出物件</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Microsoft Exchange 自動探索容器權限

下表顯示組態磁碟分割內的 Microsoft Exchange 自動探索容器上設定的權限。

### 物件的辨別名稱：CN=Microsoft Exchange Autodiscover,CN=Services,CN=Configuration,DC=\<domain\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>帳戶</th>
<th>ACE 類型</th>
<th>繼承</th>
<th>權限</th>
<th>屬性/套用至</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Microsoft Exchange 組織容器權限

本節的權限表會顯示組態磁碟分割內的 Microsoft Exchange 組織和子容器上設定的權限。

### 物件的辨別名稱：CN=\<organization\>,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<domain\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>帳戶</th>
<th>ACE 類型</th>
<th>繼承</th>
<th>權限</th>
<th>屬性/套用至</th>
<th>註解</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Enterprise Admins</p>
<p>Root Domain Admins</p>
<p>Installation Account</p>
<p>Organization Management</p></td>
<td><p>拒絕 ACE</p></td>
<td><p>全部</p></td>
<td><p>傳送身分</p>
<p>接收身分</p></td>
<td><p></p></td>
<td><p>Windows 系統管理員不可以開啟信箱。</p></td>
</tr>
<tr class="even">
<td><p>Enterprise Admins</p>
<p>Schema Admins</p>
<p>Root Domain Admins</p>
<p>Installation Account</p>
<p>Organization Management</p></td>
<td><p>拒絕 ACE</p></td>
<td><p>全部</p></td>
<td><p>Exchange Web 服務模擬</p>
<p>Exchange Web 服務 Token 序列化</p></td>
<td><p></p></td>
<td><p>延伸權利</p></td>
</tr>
<tr class="odd">
<td><p>Enterprise Admins</p>
<p>Schema Admins</p>
<p>Root Domain Admins</p>
<p>Installation Account</p></td>
<td><p>拒絕 ACE</p></td>
<td><p>全部</p></td>
<td><p>儲存傳輸存取</p>
<p>儲存限制的委派</p>
<p>儲存讀取權限</p>
<p>儲存讀取寫入權限</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Local System</p></td>
<td><p>允許</p></td>
<td><p>全部</p></td>
<td><p>所有延伸權利</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Authenticated Users</p></td>
<td><p>拒絕 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p></td>
<td><p><code>msExchAvailabilityUserPassword / msExchAvailabilityAddressSpace</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Authenticated Users</p></td>
<td><p>允許</p></td>
<td><p>無</p></td>
<td><p>讀取</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取權限</p>
<p>列出內容</p>
<p>讀取內容</p>
<p>列出物件</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Public Folder Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取權限</p>
<p>列出內容</p>
<p>讀取內容</p>
<p>列出物件</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>NT Authority\Network Service</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Managed Availability Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取權限</p>
<p>列出內容</p>
<p>讀取內容</p>
<p>列出物件</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>所有延伸權利</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>groupType</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchOwningServer</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchMailboxSecurityDescriptor</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchUMServerWritableFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchDatabaseCreated</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchUserCulture</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchMobileMailboxFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>siteFolderGUID</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>siteFolderServer</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchEDBOffline</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>userCertificate</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchUMDtmfMap</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchBlockedSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>Public Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchPatchMDB</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>publicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchUMSpokenName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchUMPinChecksum</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>legacyExchangeDN</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchSafeSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>thumbnailPhoto</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>建立最上層公用資料夾</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Public Folder Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>建立最上層公用資料夾</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>檢視資訊儲存庫狀態</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Public Folder Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>檢視資訊儲存庫狀態</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>管理資訊儲存庫</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Public Folder Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>管理資訊儲存庫</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>在資訊儲存庫中建立具名內容</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Public Folder Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>在資訊儲存庫中建立具名內容</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>修改公用資料夾 ACL</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Public Folder Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>修改公用資料夾 ACL</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>修改公用資料夾配額</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Public Folder Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>修改公用資料夾配額</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>修改公用資料夾管理 ACL</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Public Folder Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>修改公用資料夾管理 ACL</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>修改公用資料夾到期</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Public Folder Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>修改公用資料夾到期</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>修改公用資料夾複本清單</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Public Folder Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>修改公用資料夾複本清單</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>修改公用資料夾刪除項目保留</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Public Folder Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>修改公用資料夾刪除項目保留</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>建立公用資料夾</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Public Folder Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>建立公用資料夾</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Public Folder Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>擁有郵件功能的公用資料夾</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>任何人</p>
<p>NT Authority\Anonymous Logon</p>
<p></p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>在資訊儲存庫中建立具名內容</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Everyone</p>
<p>NT Authority\Anonymous Logon</p>
<p></p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>建立公用資料夾</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Everyone</p>
<p>NT Authority\Anonymous Logon</p>
<p></p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取權限</p>
<p>列出內容</p>
<p>讀取內容</p>
<p>列出物件</p></td>
<td><p><code>/ msExchPrivateMDB</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Everyone</p>
<p>NT Authority\Anonymous Logon</p>
<p></p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取權限</p>
<p>列出內容</p>
<p>讀取內容</p>
<p>列出物件</p></td>
<td><p><code>/ msExchPublicMDB</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取權限</p>
<p>列出內容</p>
<p>讀取內容</p>
<p>列出物件</p></td>
<td><p><code>/ siteAddressing</code></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 物件的辨別名稱：CN=All Address Lists,CN=Address Lists Container,CN=\<organization\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>帳戶</th>
<th>ACE 類型</th>
<th>繼承</th>
<th>權限</th>
<th>屬性/套用至</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Authenticated Users</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>列出內容</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchLastAppliedRecipientFilter</code></p>
<p><code>msExchRecipientFilterFlags</code></p></td>
</tr>
<tr class="odd">
<td><p>Public Folder Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchLastAppliedRecipientFilter</code></p>
<p><code>msExchRecipientFilterFlags</code></p></td>
</tr>
</tbody>
</table>


### 物件的辨別名稱：CN=Offline Address Lists,CN=Address Lists Container, CN=\<organization\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>帳戶</th>
<th>ACE 類型</th>
<th>繼承</th>
<th>權限</th>
<th>屬性/套用至</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Authenticated Users</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>下載離線通訊錄</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 物件的辨別名稱：CN=Addressing,CN=\<organization\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>帳戶</th>
<th>ACE 類型</th>
<th>繼承</th>
<th>權限</th>
<th>屬性/套用至</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Authenticated Users</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 物件的辨別名稱：CN=Recipient Policies,CN=\<organization\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>帳戶</th>
<th>ACE 類型</th>
<th>繼承</th>
<th>權限</th>
<th>屬性/套用至</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchLastAppliedRecipientFilter</code></p>
<p><code>msExchRecipientFilterFlags</code></p></td>
</tr>
<tr class="even">
<td><p>Public Folder Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchLastAppliedRecipientFilter</code></p>
<p><code>msExchRecipientFilterFlags</code></p></td>
</tr>
</tbody>
</table>


## 組態磁碟分割容器權限

本節的權限表會顯示 `Setup /PrepareAD` 命令對組態磁碟分割內的各種容器所設定的權限。

### 物件的辨別名稱：CN=Sites,CN=Configuration,DC=\<domain\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>帳戶</th>
<th>ACE 類型</th>
<th>繼承</th>
<th>權限</th>
<th>屬性/套用至</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Organization Management</p>
<p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchVersion / site</code></p></td>
</tr>
<tr class="even">
<td><p>Organization Management</p>
<p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchVersion / site-link</code></p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p>
<p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchPartnerId / site</code></p></td>
</tr>
<tr class="even">
<td><p>Organization Management</p>
<p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchMinorPartnerId / site</code></p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p>
<p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchResponsibleforSites / site</code></p></td>
</tr>
<tr class="even">
<td><p>Organization Management</p>
<p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p></p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchTransportSiteFlags / site</code></p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p>
<p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchCost / site-link</code></p></td>
</tr>
<tr class="even">
<td><p>Organization Management</p>
<p>Exchange Trusted Subsystem</p>
<p>Local System</p>
<p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取權限</p>
<p>列出內容</p>
<p>讀取內容</p>
<p>列出物件</p></td>
<td><p><code>/ msExchEdgeSyncEHFConnector</code></p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p>
<p>Exchange Trusted Subsystem</p>
<p>Local System</p>
<p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取權限</p>
<p>列出內容</p>
<p>讀取內容</p>
<p>列出物件</p></td>
<td><p><code>/ msExchEdgeSyncMservConnector</code></p></td>
</tr>
<tr class="even">
<td><p>Organization Management</p>
<p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>子項</p></td>
<td><p>建立子項</p>
<p>刪除子項</p>
<p>刪除樹狀目錄</p></td>
<td><p><code>msExchEdgeSyncServiceConfig / site</code></p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p>
<p>Exchange Trusted Subsystem</p>
<p>Local System</p>
<p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取權限</p>
<p>列出內容</p>
<p>讀取內容</p>
<p>列出物件</p></td>
<td><p><code>/ msExchEdgeSyncServiceConfig</code></p></td>
</tr>
<tr class="even">
<td><p>Organization Management</p>
<p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>子項</p></td>
<td><p>建立子項</p>
<p>刪除子項</p>
<p>刪除樹狀目錄</p></td>
<td><p><code>msExchEdgeSyncMservConnector / msExchEdgeSyncServiceConfig</code></p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p>
<p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>子項</p></td>
<td><p>建立子項</p>
<p>刪除子項</p>
<p>刪除樹狀目錄</p></td>
<td><p><code>msExchEdgeSyncEHFConnector / msExchEdgeSyncServiceConfig</code></p></td>
</tr>
</tbody>
</table>


### 物件的辨別名稱：CN=Deleted Objects,CN=Configuration,DC=\<domain\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>帳戶</th>
<th>ACE 類型</th>
<th>繼承</th>
<th>權限</th>
<th>屬性/套用至</th>
<th>註解</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>列出內容</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Organization Administration</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取</p>
<p>列出物件</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Installation Account</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取權限</p>
<p>寫入權限</p>
<p>列出內容</p>
<p>讀取內容</p>
<p>列出物件</p></td>
<td><p></p></td>
<td><p>這是用來執行 <code>/PrepareAD</code> 的帳戶。</p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取</p>
<p>列出物件</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Network Service</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>列出內容</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Exchange 系統管理群組權限

`Setup /PrepareAD` 命令也會對組織內的系統管理群組設定下列權限。

### 物件的辨別名稱：CN=\<admin group\>,CN=Administrative Groups,CN=\<organization\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>帳戶</th>
<th>ACE 類型</th>
<th>繼承</th>
<th>權限</th>
<th>屬性/套用至</th>
<th>註解</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>存取收件者更新服務</p></td>
<td><p><code>msExchExchangeServer</code></p></td>
<td><p>允許 Exchange 收件者系統管理員利用 Proxy 位址資訊為收件者加上戳記。</p></td>
</tr>
<tr class="even">
<td><p>Local System</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>存取收件者更新服務</p></td>
<td><p><code>msExchExchangeServer</code></p></td>
<td><p>允許伺服器利用 Proxy 位址資訊為收件者加上戳記。</p></td>
</tr>
<tr class="odd">
<td><p>Public Folder Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>存取收件者更新服務</p></td>
<td><p><code>msExchExchangeServer</code></p></td>
<td><p>允許 Exchange 公用資料夾系統管理員利用 Proxy 位址資訊為收件者加上戳記。</p></td>
</tr>
</tbody>
</table>


### 物件的辨別名稱：CN=Advanced Security Settings,CN=\<admin group\>,CN=Administrative Groups,CN=\<organization\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>帳戶</th>
<th>ACE 類型</th>
<th>繼承</th>
<th>權限</th>
<th>屬性/套用至</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Authenticated Users</p></td>
<td><p>允許 ACE</p></td>
<td><p>無</p></td>
<td><p>列出內容</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 物件的辨別名稱：CN=Encryption,CN=Advanced Security Settings,CN=\<admin group\>,CN=Administrative Groups,CN=\<organization\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>帳戶</th>
<th>ACE 類型</th>
<th>繼承</th>
<th>權限</th>
<th>屬性/套用至</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Authenticated Users</p></td>
<td><p>允許 ACE</p></td>
<td><p>無</p></td>
<td><p>讀取內容</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 物件的辨別名稱：CN=Arrays,CN=\<admin group\>,CN=Administrative Groups,CN=\<organization\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>帳戶</th>
<th>ACE 類型</th>
<th>繼承</th>
<th>權限</th>
<th>屬性/套用至</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Authenticated Users</p></td>
<td><p>允許 ACE</p></td>
<td><p>無</p></td>
<td><p>列出內容</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 物件的辨別名稱：CN=Database Availability Groups,CN=\<admin group\>,CN=Administrative Groups,CN=\<organization\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>帳戶</th>
<th>ACE 類型</th>
<th>繼承</th>
<th>權限</th>
<th>屬性/套用至</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Authenticated Users</p></td>
<td><p>允許 ACE</p></td>
<td><p>無</p></td>
<td><p>列出內容</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 物件的辨別名稱：CN=Databases,CN=\<admin group\>,CN=Administrative Groups,CN=\<organization\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>帳戶</th>
<th>ACE 類型</th>
<th>繼承</th>
<th>權限</th>
<th>屬性/套用至</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Authenticated Users</p></td>
<td><p>允許 ACE</p></td>
<td><p>無</p></td>
<td><p>列出內容</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 物件的辨別名稱：CN=Servers,CN=\<admin group\>,CN=Administrative Groups,CN=\<organization\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>帳戶</th>
<th>ACE 類型</th>
<th>繼承</th>
<th>權限</th>
<th>屬性/套用至</th>
<th>註解</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>拒絕 ACE</p></td>
<td><p>全部</p></td>
<td><p>以下列接收</p></td>
<td><p></p></td>
<td><p>Exchange Server 不可以開啟信箱。</p></td>
</tr>
<tr class="even">
<td><p>Authenticated Users</p></td>
<td><p>允許 ACE</p></td>
<td><p>無</p></td>
<td><p>列出內容</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Microsoft Exchange 安全性群組容器權限

本節的權限表會顯示根網域磁碟分割內的 Microsoft Exchange 安全性群組容器上設定的權限。

### 物件的辨別名稱：OU=Microsoft Exchange Security Groups,DC=\<root domain\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>帳戶</th>
<th>ACE 類型</th>
<th>繼承</th>
<th>權限</th>
<th>屬性/套用至</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>完全控制</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>建立子項</p></td>
<td><p><code>/ Group</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>刪除</p></td>
<td><p><code>/ group</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>寫入內容</p></td>
<td><p><code>Member / group</code></p></td>
</tr>
</tbody>
</table>


### 物件的辨別名稱：CN=Organization Management,OU=Microsoft Exchange Security Groups,DC=\<root domain\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>帳戶</th>
<th>ACE 類型</th>
<th>繼承</th>
<th>權限</th>
<th>屬性/套用至</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>完全控制</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 物件的辨別名稱：CN=Public Folder Management,OU=Microsoft Exchange Security Groups,DC=\<root domain\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>帳戶</th>
<th>ACE 類型</th>
<th>繼承</th>
<th>權限</th>
<th>屬性/套用至</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>完全控制</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 物件的辨別名稱：CN=ExchangeLegacyInterop,OU=Microsoft Exchange Security Groups,DC=\<root domain\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>帳戶</th>
<th>ACE 類型</th>
<th>繼承</th>
<th>權限</th>
<th>屬性/套用至</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>完全控制</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 物件的辨別名稱：CN=Exchange Servers,OU=Microsoft Exchange Security Groups,DC=\<root domain\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>帳戶</th>
<th>ACE 類型</th>
<th>繼承</th>
<th>權限</th>
<th>屬性/套用至</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>完全控制</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Root Domain Administrators</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取成員</p>
<p>寫入成員</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Child Domain Administrators</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取成員</p>
<p>寫入成員</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## 準備網域

以下表格顯示您執行 `Setup /PrepareDomain` 命令時設定的權限。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>本節描述的權限是您使用共用權限模式部署 Exchange 2013 時所設定的預設權限。如果是使用 Active Directory 分割權限模式來部署 Exchange 2013，則預設的權限會不同。如需有關使用 Active Directory 分割權限時預設權限變更的詳細資訊，以及共用和分割權限模式的整體資訊，請參閱＜<a href="understanding-split-permissions-exchange-2013-help.md">了解分割權限</a>＞中的＜<a href="understanding-split-permissions-exchange-2013-help.md">Active Directory split permissions</a>＞。如果您安裝 Exchange 時未選擇使用 Active Directory 分割權限，Exchange 會使用共用權限。</td>
</tr>
</tbody>
</table>


### 物件的辨別名稱：DC=\<domain\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>帳戶</th>
<th>ACE 類型</th>
<th>繼承</th>
<th>權限</th>
<th>屬性/套用至</th>
<th>註解</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Authenticated Users</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取內容</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>NT AUTHORITY\NETWORK</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取內容</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p>授與傳輸服務讀取權限。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>groupType</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchMailboxSecurityDescriptor</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchUMServerWritableFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取內容</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取內容</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchUserCultulre</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取內容</p></td>
<td><p><code>memberOf</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取內容</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取內容</p></td>
<td><p><code>userAccountControl</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取內容</p></td>
<td><p><code>canonicalName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>複寫同步處理</p></td>
<td><p></p></td>
<td><p>延伸權利</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>建立子項</p>
<p>刪除子項</p>
<p>列出子項</p></td>
<td><p><code>msExchActiveSyncDevices / User</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>建立子項</p>
<p>刪除子項</p>
<p>列出子項</p></td>
<td><p><code>msExchActiveSyncDevices / inetOrgPerson</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchSafeSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchMobileMailboxFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchSafeRecipientsHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>userCertificate</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchUMDtmfMap</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchBlockedSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchUMSpokenName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchUMPinChecksum</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>thumbnailPhoto</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取</p>
<p>列出物件</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>legacyExchangeDN</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>textEncodedORAddress</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>proxyAddresses</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>mail</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>displayNamePrintable</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>showInAddressBook</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>完全控制</p></td>
<td><p><code>/ msExchDynamicDistributionList</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>adminDisplayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>displayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取</p>
<p>列出物件</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>displayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>Public Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>adminDisplayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>完全控制</p></td>
<td><p><code>/ msExchDynamicDistributionList</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>textEncodedORAddress</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>showInAddressBook</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>legacyExchangeDN</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>proxyAddresses</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>displayNamePrintable</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>mail</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows Permissions</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>pwdLastSet</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows Permissions</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>WriteDACL</p></td>
<td><p><code>/ user</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows Permissions</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>WriteDACL</p>
<p></p></td>
<td><p><code>/ inetOrgPerson</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows Permissions</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>刪除樹狀目錄</p></td>
<td><p><code>/ user</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows Permissions</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>刪除樹狀目錄</p>
<p></p></td>
<td><p><code>/ inetOrgPerson</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows Permissions</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>sAMAccountName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows Permissions</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>建立子項</p>
<p>刪除</p></td>
<td><p><code>/ contact</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows Permissions</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>建立子項</p>
<p>刪除</p></td>
<td><p><code>/ inetOrgPerson</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows Permissions</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>建立子項</p>
<p>刪除</p></td>
<td><p><code>/ user</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows Permissions</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>建立子項</p>
<p>刪除</p></td>
<td><p><code>/ organizationUnit</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows Permissions</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>建立子項</p>
<p>刪除</p></td>
<td><p><code>/ group</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows Permissions</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>建立子項</p>
<p>刪除子項</p></td>
<td><p><code>/ computer</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows Permissions</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>Member</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows Permissions</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>wwwHomePage</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows Permissions</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>countryCode</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows Permissions</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>userAccountControl</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows Permissions</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>managedBy</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows Permissions</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>在下次登入時重設密碼</p></td>
<td><p></p></td>
<td><p>延伸權利</p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows Permissions</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>變更密碼</p></td>
<td><p><code> / user</code></p></td>
<td><p>延伸權利</p></td>
</tr>
<tr class="odd">
<td><p>Delegated Setup</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取內容</p></td>
<td><p><code>User Account Restrictions</code></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 物件的辨別名稱：CN=AdminSDHolder,CN=System,DC=\<domain\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>帳戶</th>
<th>ACE 類型</th>
<th>繼承</th>
<th>權限</th>
<th>屬性/套用至</th>
<th>註解</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Authenticated Users</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取內容</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>NT AUTHORITY\NETWORK</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取內容</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p>授與傳輸服務讀取權限。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>groupType</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchMailboxSecurityDescriptor</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchUMServerWritableFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取內容</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取內容</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchUserCultulre</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取內容</p></td>
<td><p><code>memberOf</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取內容</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取內容</p></td>
<td><p><code>userAccountControl</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取內容</p></td>
<td><p><code>canonicalName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>複寫同步處理</p></td>
<td><p></p></td>
<td><p>延伸權利</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>建立子項</p>
<p>刪除子項</p>
<p>列出子項</p></td>
<td><p><code>msExchActiveSyncDevices / User</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>建立子項</p>
<p>刪除子項</p>
<p>列出子項</p></td>
<td><p><code>msExchActiveSyncDevices / inetOrgPerson</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchSafeSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchMobileMailboxFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchSafeRecipientsHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>userCertificate</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchUMDtmfMap</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchBlockedSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchUMSpokenName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchUMPinChecksum</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>thumbnailPhoto</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取</p>
<p>列出物件</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>legacyExchangeDN</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>textEncodedORAddress</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>proxyAddresses</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>mail</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>displayNamePrintable</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>showInAddressBook</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>完全控制</p></td>
<td><p><code>/ msExchDynamicDistributionList</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>adminDisplayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>displayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取</p>
<p>列出物件</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>displayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>Public Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>adminDisplayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>完全控制</p></td>
<td><p><code>/ msExchDynamicDistributionList</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>textEncodedORAddress</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>showInAddressBook</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>legacyExchangeDN</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>proxyAddresses</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>displayNamePrintable</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>mail</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows Permissions</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>pwdLastSet</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows Permissions</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>sAMAccountName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows Permissions</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>Member</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows Permissions</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>wwwHomePage</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows Permissions</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>countryCode</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Windows Permissions</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>userAccountControl</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Windows Permissions</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p><code>managedBy</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Delegated Setup</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取內容</p></td>
<td><p><code>User Account Restrictions</code></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 物件的辨別名稱：CN=Deleted Objects,DC=\<domain\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>帳戶</th>
<th>ACE 類型</th>
<th>繼承</th>
<th>權限</th>
<th>屬性/套用至</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>列出內容</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 物件的辨別名稱：CN=Microsoft Exchange System Objects,DC=\<domain\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>帳戶</th>
<th>ACE 類型</th>
<th>繼承</th>
<th>權限</th>
<th>屬性/套用至</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NT AUTHORITY\NETWORK</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取內容</p>
<p>列出內容</p>
<p>讀取權限</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Authenticated Users</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取權限</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Authenticated Users</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取內容</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
</tr>
<tr class="even">
<td><p>Authenticated Users</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取內容</p></td>
<td><p><code>adminDisplayName</code></p></td>
</tr>
<tr class="odd">
<td><p>Authenticated Users</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取內容</p></td>
<td><p><code>modifyTimeStamp</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>拒絕 ACE</p></td>
<td><p>全部</p></td>
<td><p>刪除樹狀目錄</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取權限</p>
<p>列出內容</p>
<p>讀取內容 刪除樹狀結構</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>建立子項</p>
<p></p></td>
<td><p><code>/ msExchSystemMailbox</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>建立子項</p>
<p>刪除子項</p></td>
<td><p><code>/ publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>建立子項</p>
<p></p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>刪除子項</p>
<p></p></td>
<td><p><code>/ msExchSystemMailbox</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>刪除子項</p>
<p></p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>寫入內容</p></td>
<td><p><code>/ publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>寫入內容</p></td>
<td><p><code>/ msExchSystemMailbox</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>寫入內容</p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>變更密碼</p>
<p>在下次登入時重設密碼</p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取權限</p>
<p>列出內容</p>
<p>讀取內容</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>寫入內容</p></td>
<td><p><code>/ msExchSystemMailbox</code></p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>建立子項</p>
<p>刪除子項</p></td>
<td><p><code>/ msExchSystemMailbox</code></p></td>
</tr>
<tr class="even">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>寫入內容</p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>建立子項</p>
<p>刪除子項</p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="even">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>mail / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>displayNamePrintable / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>displayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>textEncodedORAddress / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>proxyAddresses / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>cn / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>showInAddressBook / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>Exchange Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p>legacyExchangeDN / publicFolder</p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>Exchange Personal Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>msDSPhoneticDisplayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>msExchPFContacts / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>garbageCollPeriod / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>name / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>msExchPublicDelegates / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Public Folder Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取權限</p>
<p>列出內容</p>
<p>讀取內容</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Public Folder Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>mail / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Public Folder Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>displayNamePrintable / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Public Folder Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>displayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Public Folder Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>textEncodedORAddress / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Public Folder Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>proxyAddresses / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Public Folder Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>cn / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Public Folder Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>showInAddressBook / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Public Folder Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>Exchange Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Public Folder Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>legacyExchangeDN / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Public Folder Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>Exchange Personal Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Public Folder Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>msDSPhoneticDisplayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Public Folder Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>msExchPFContacts / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Public Folder Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>garbageCollPeriod / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Public Folder Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>name / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Public Folder Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>msExchPublicDelegates / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取權限</p>
<p>列出內容</p>
<p>讀取內容</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>mail / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>displayNamePrintable / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>displayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>textEncodedORAddress / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>proxyAddresses / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>cn / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>showInAddressBook / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>Exchange Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>legacyExchangeDN / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>Exchange Personal Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>msDSPhoneticDisplayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>msExchPFContacts / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>garbageCollPeriod / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>name / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Exchange Trusted Subsystem</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p>
<p>寫入內容</p></td>
<td><p><code>msExchPublicDelegates / publicFolder</code></p></td>
</tr>
</tbody>
</table>


### 物件的辨別名稱：CN=Exchange Install Domain Servers,CN=Microsoft Exchange System Objects,DC=\<domain\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>帳戶</th>
<th>ACE 類型</th>
<th>繼承</th>
<th>權限</th>
<th>屬性/套用至</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Organization Management</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>完全控制</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## 伺服器角色安裝

在安裝 Client Access server role 和 Mailbox server role 期間，安裝程式會將 Organization Management USG 加入本機電腦上的系統管理員安全性群組，這樣一來，名為 Organization Management 的管理角色群組成員就可以管理伺服器。

下列權限表會顯示您安裝 Client Access server role 和 Mailbox server role 時設定的權限。

### 物件的辨別名稱：CN=\<server\>,CN=Servers,CN=\<admin group\>,CN=Administrative Groups,CN=\<organization\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>帳戶</th>
<th>ACE 類型</th>
<th>繼承</th>
<th>權限</th>
<th>屬性/套用至</th>
<th>註解</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MACHINE$</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取權限</p>
<p>列出內容</p>
<p>讀取內容</p>
<p>列出物件</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>MACHINE$</p></td>
<td><p>允許 ACE</p></td>
<td><p>無</p></td>
<td><p>寫入內容</p></td>
<td><p><code>msExchServerSite</code></p>
<p><code>msExchEdgeSyncCredential</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>儲存傳輸存取</p>
<p>儲存限制的委派</p>
<p>儲存唯讀權限</p>
<p>儲存讀取和寫入權限</p></td>
<td><p></p></td>
<td><p>延伸權利</p></td>
</tr>
<tr class="even">
<td><p>NT AUTHORITY\NETWORK</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>Exchange Web 服務 Token 序列化</p></td>
<td><p></p></td>
<td><p>延伸權利</p>
<p>只授與 Mailbox server role 物件。</p></td>
</tr>
<tr class="odd">
<td><p>NT AUTHORITY\NETWORK</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取權限</p>
<p>列出內容</p>
<p>讀取內容</p>
<p>列出物件</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Local System</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取權限</p>
<p>列出內容</p>
<p>讀取內容</p>
<p>列出物件</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Delegated Setup</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>完全控制</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Delegated Setup</p></td>
<td><p>拒絕 ACE</p></td>
<td><p>全部</p></td>
<td><p>建立子項</p>
<p>刪除子項</p></td>
<td><p><code>/ msExchPublicMDB</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Authenticated Users</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>讀取內容</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Delegated Setup</p></td>
<td><p>拒絕 ACE</p></td>
<td><p>全部</p></td>
<td><p>以下列接收</p>
<p>以下列傳送</p></td>
<td><p></p></td>
<td><p>延伸權利</p></td>
</tr>
</tbody>
</table>


## 資料庫可用性群組

本節的權限表會顯示針對資料庫可用性群組及其成員所設定的權限。

### 物件的辨別名稱：CN=\<DAGName\>,CN=Database Availability Groups,CN=\<admin group\>,CN=Administrative Groups,CN=\<organization\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>帳戶</th>
<th>ACE 類型</th>
<th>繼承</th>
<th>權限</th>
<th>屬性/套用至</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Authenticated Users</p></td>
<td><p>允許 ACE</p></td>
<td><p>無</p></td>
<td><p>讀取內容</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## 邊際傳輸

如果您安裝 Edge Transport Server，並建立 Exchange 組織的 Edge 訂閱，則 Edge Transport Server 在組織中產生實體時，就會設定以下權限表中的權限。

### 物件的辨別名稱：CN=\<server\>,CN=Servers,CN=\<admin group\>,CN=Administrative Groups,CN=\<organization\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>帳戶</th>
<th>ACE 類型</th>
<th>繼承</th>
<th>權限</th>
<th>屬性/套用至</th>
<th>註解</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>寫入內容</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Authenticated Users</p></td>
<td><p>允許 ACE</p></td>
<td><p>無</p></td>
<td><p>讀取內容</p></td>
<td><p></p></td>
<td><p>ACE 是在 <code>msExchExchangeServer</code> 類別物件 <code>defaultSecurityDescriptor</code> 的結構描述中定義。</p></td>
</tr>
</tbody>
</table>


## 信箱伺服器安裝

在安裝第一個信箱伺服器的過程中會建立下列容器 (若不存在)。下列權限表會顯示所套用的權限。

### 物件的辨別名稱：CN=Availability Configuration,CN=\<organization\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>帳戶</th>
<th>ACE 類型</th>
<th>繼承</th>
<th>權限</th>
<th>屬性/套用至</th>
<th>註解</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>描述</p></td>
<td><p>讀取內容</p></td>
<td><p><code>msExchAvailabilityUserPassword / msExchAvailabilityAddressSpaceObjects</code></p></td>
<td><p>延伸權利</p></td>
</tr>
</tbody>
</table>


### 物件的辨別名稱：CN=Default \<Server\>,CN=SMTP Receive Connectors,CN=Protocols,CN=\<Server\>,CN=Servers,CN=\<admin group\>,CN=\<organization\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>帳戶</th>
<th>ACE 類型</th>
<th>繼承</th>
<th>權限</th>
<th>屬性/套用至</th>
<th>註解</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>拒絕 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受樹系標頭</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>拒絕 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受組織標頭</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受任何寄件者</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受任何寄件者</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受任何寄件者</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知安全性識別碼 (SID)。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受任何寄件者</p></td>
<td><p></p></td>
<td><p>這是 Edge Transport Server 的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受任何寄件者</p></td>
<td><p></p></td>
<td><p>這是外部保護伺服器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 EXCH50</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 EXCH50</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 EXCH50</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 EXCH50</p></td>
<td><p></p></td>
<td><p>這是 Edge Transport Server 的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 EXCH50</p></td>
<td><p></p></td>
<td><p>這是外部保護伺服器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>提交郵件到任何收件者</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>提交郵件到任何收件者</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>提交郵件到任何收件者</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>提交郵件到任何收件者</p></td>
<td><p></p></td>
<td><p>這是 Edge Transport Server 的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>提交郵件到任何收件者</p></td>
<td><p></p></td>
<td><p>這是外部保護伺服器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 XShadow</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 XShadow</p></td>
<td><p></p></td>
<td><p>這是 Edge Transport Server 的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受路由標頭</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受路由標頭</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受路由標頭</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受路由標頭</p></td>
<td><p></p></td>
<td><p>這是 Edge Transport Server 的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受路由標頭</p></td>
<td><p></p></td>
<td><p>這是外部保護伺服器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 XSessionParams</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 XSessionParams</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 XSessionParams</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受樹系標頭</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受樹系標頭</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受樹系標頭</p></td>
<td><p></p></td>
<td><p>這是 Edge Transport Server 的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 xAttr</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 xAttr</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 xAttr</p></td>
<td><p></p></td>
<td><p>這是 Edge Transport Server 的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 XProxyFrom</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受樹系 XProxyFrom</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受樹系 XProxyFrom</p></td>
<td><p></p></td>
<td><p>這是 Edge Transport Server 的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 XSysProbe</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受樹系 XSysProbe</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受樹系 XSysProbe</p></td>
<td><p></p></td>
<td><p>這是 Edge Transport Server 的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>傳送 XMessageContext 延伸屬性</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>傳送 XMessageContext 延伸屬性</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>傳送 XMessageContext 延伸屬性</p></td>
<td><p></p></td>
<td><p>這是 Edge Transport Server 的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>傳送 XMessageContext 快速索引</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>傳送 XMessageContext 快速索引</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>傳送 XMessageContext 快速索引</p></td>
<td><p></p></td>
<td><p>這是 Edge Transport Server 的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>傳送 XMessageContext AD 收件者快取</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>傳送 XMessageContext AD 收件者快取</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>傳送 XMessageContext AD 收件者快取</p></td>
<td><p></p></td>
<td><p>這是 Edge Transport Server 的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受驗證旗標</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受驗證旗標</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受驗證旗標</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受驗證旗標</p></td>
<td><p></p></td>
<td><p>這是 Edge Transport Server 的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受驗證旗標</p></td>
<td><p></p></td>
<td><p>這是外部保護伺服器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>略過反垃圾郵件</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>略過反垃圾郵件</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>略過反垃圾郵件</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>略過反垃圾郵件</p></td>
<td><p></p></td>
<td><p>這是 Edge Transport Server 的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>略過反垃圾郵件</p></td>
<td><p></p></td>
<td><p>這是外部保護伺服器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>略過郵件大小限制</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>略過郵件大小限制</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>略過郵件大小限制</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>略過郵件大小限制</p></td>
<td><p></p></td>
<td><p>這是 Edge Transport Server 的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>略過郵件大小限制</p></td>
<td><p></p></td>
<td><p>這是外部保護伺服器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受組織標頭</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受組織標頭</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受組織標頭</p></td>
<td><p></p></td>
<td><p>這是 Edge Transport Server 的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>提交郵件到伺服器</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>提交郵件到伺服器</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>提交郵件到伺服器</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>提交郵件到伺服器</p></td>
<td><p></p></td>
<td><p>這是 Edge Transport Server 的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>提交郵件到伺服器</p></td>
<td><p></p></td>
<td><p>這是外部保護伺服器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受授權網域寄件者</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受授權網域寄件者</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受授權網域寄件者</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受授權網域寄件者</p></td>
<td><p></p></td>
<td><p>這是 Edge Transport Server 的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受授權網域寄件者</p></td>
<td><p></p></td>
<td><p>這是外部保護伺服器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Authenticated Users</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>提交郵件到任何收件者</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Authenticated Users</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受路由標頭</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Authenticated Users</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>略過反垃圾郵件</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Authenticated Users</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>提交郵件到伺服器</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### 物件的辨別名稱：CN=Client \<Server\>,CN=SMTP Receive Connectors,CN=Protocols,CN=\<Server\>,CN=Servers,CN=\<admin group\>,CN=\<organization\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>帳戶</th>
<th>ACE 類型</th>
<th>繼承</th>
<th>權限</th>
<th>屬性/套用至</th>
<th>註解</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Authenticated Users</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>提交郵件到任何收件者</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Authenticated Users</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受路由標頭</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Authenticated Users</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>略過反垃圾郵件</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Authenticated Users</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>提交郵件到伺服器</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 XSessionParams</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 XSessionParams</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 XSessionParams</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受任何寄件者</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受任何寄件者</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知安全性識別碼 (SID)。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受任何寄件者</p></td>
<td><p></p></td>
<td><p>這是 Edge Transport Server 的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受任何寄件者</p></td>
<td><p></p></td>
<td><p>這是外部保護伺服器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 Exch50</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 Exch50</p></td>
<td><p></p></td>
<td><p>這是 Edge Transport Server 的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 Exch50</p></td>
<td><p></p></td>
<td><p>這是外部保護伺服器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 Exch50</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>提交郵件到任何收件者</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>提交郵件到任何收件者</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>提交郵件到任何收件者</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>提交郵件到任何收件者</p></td>
<td><p></p></td>
<td><p>這是 Edge Transport Server 的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>提交郵件到任何收件者</p></td>
<td><p></p></td>
<td><p>這是外部保護伺服器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 XShadow</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 XShadow</p></td>
<td><p></p></td>
<td><p>這是 Edge Transport Server 的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受路由標頭</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受路由標頭</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受路由標頭</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受路由標頭</p></td>
<td><p></p></td>
<td><p>這是 Edge Transport Server 的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受路由標頭</p></td>
<td><p></p></td>
<td><p>這是外部保護伺服器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受樹系標頭</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受樹系標頭</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受樹系標頭</p></td>
<td><p></p></td>
<td><p>這是 Edge Transport Server 的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 xAttr</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 xAttr</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 xAttr</p></td>
<td><p></p></td>
<td><p>這是 Edge Transport Server 的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 XProxyFrom</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受樹系 XProxyFrom</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受樹系 XProxyFrom</p></td>
<td><p></p></td>
<td><p>這是 Edge Transport Server 的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受驗證旗標</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受驗證旗標</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受驗證旗標</p></td>
<td><p></p></td>
<td><p>這是 Edge Transport Server 的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受驗證旗標</p></td>
<td><p></p></td>
<td><p>這是外部保護伺服器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受 XSysProbe</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受樹系 XSysProbe</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受樹系 XSysProbe</p></td>
<td><p></p></td>
<td><p>這是 Edge Transport Server 的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受驗證旗標</p></td>
<td><p></p></td>
<td><p>這是外部保護伺服器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>略過反垃圾郵件</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>略過反垃圾郵件</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>略過反垃圾郵件</p></td>
<td><p></p></td>
<td><p>這是 Edge Transport Server 的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>略過反垃圾郵件</p></td>
<td><p></p></td>
<td><p>這是外部保護伺服器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>傳送 XMessageContext 延伸屬性</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>傳送 XMessageContext 延伸屬性</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>傳送 XMessageContext 延伸屬性</p></td>
<td><p></p></td>
<td><p>這是 Edge Transport Server 的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>傳送 XMessageContext 快速索引</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>傳送 XMessageContext 快速索引</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>傳送 XMessageContext 快速索引</p></td>
<td><p></p></td>
<td><p>這是 Edge Transport Server 的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>略過郵件大小限制</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>略過郵件大小限制</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>略過郵件大小限制</p></td>
<td><p></p></td>
<td><p>這是 Edge Transport Server 的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>略過郵件大小限制</p></td>
<td><p></p></td>
<td><p>這是外部保護伺服器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受組織標頭</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受組織標頭</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受組織標頭</p></td>
<td><p></p></td>
<td><p>這是 Edge Transport Server 的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>傳送 XMessageContext AD 收件者快取</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>傳送 XMessageContext AD 收件者快取</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>傳送 XMessageContext AD 收件者快取</p></td>
<td><p></p></td>
<td><p>這是 Edge Transport Server 的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>提交郵件到伺服器</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>提交郵件到伺服器</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>提交郵件到伺服器</p></td>
<td><p></p></td>
<td><p>這是 Edge Transport Server 的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>提交郵件到伺服器</p></td>
<td><p></p></td>
<td><p>這是外部保護伺服器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受授權網域寄件者</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受授權網域寄件者</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受授權網域寄件者</p></td>
<td><p></p></td>
<td><p>這是 Edge Transport Server 的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>接受授權網域寄件者</p></td>
<td><p></p></td>
<td><p>這是外部保護伺服器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## 建立 SMTP 傳送連接器

下表顯示您建立傳送連接器時設定的權限。

### 物件的辨別名稱：CN=\<Connector Name\>,CN=Connections,CN=\<routing group\>,CN=Routing Groups, CN=\<admin group\>,CN=\<organization\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>帳戶</th>
<th>ACE 類型</th>
<th>繼承</th>
<th>權限</th>
<th>屬性/套用至</th>
<th>註解</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NT AUTHORITY\ANONYMOUS LOGON</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>傳送路由標頭</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>傳送組織標頭</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>傳送組織標頭</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>傳送組織標頭</p></td>
<td><p></p></td>
<td><p>這是 Edge Transport Server 的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>傳送樹系標頭</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>傳送樹系標頭</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>傳送樹系標頭</p></td>
<td><p></p></td>
<td><p>這是 Edge Transport Server 的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>傳送 XShadow</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>傳送 XShadow</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>傳送 XShadow</p></td>
<td><p></p></td>
<td><p>這是 Edge Transport Server 的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>傳送路由標頭</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-10</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>傳送路由標頭</p></td>
<td><p></p></td>
<td><p>這是協力程式伺服器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>傳送路由標頭</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>傳送路由標頭</p></td>
<td><p></p></td>
<td><p>這是 Edge Transport Server 的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>傳送路由標頭</p></td>
<td><p></p></td>
<td><p>這是外部保護伺服器的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-24</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>傳送路由標頭</p></td>
<td><p></p></td>
<td><p>這是傳統 Exchange Server 的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Servers</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>傳送 Exch50</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>傳送 Exch50</p></td>
<td><p></p></td>
<td><p>這是信箱伺服器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>傳送 Exch50</p></td>
<td><p></p></td>
<td><p>這是 Edge Transport Server 的已知 SID。</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>傳送 Exch50</p></td>
<td><p></p></td>
<td><p>這是外部保護伺服器的已知 SID。</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-24</p></td>
<td><p>允許 ACE</p></td>
<td><p>全部</p></td>
<td><p>傳送 Exch50</p></td>
<td><p></p></td>
<td><p>這是傳統 Exchange Server 的已知 SID。</p></td>
</tr>
</tbody>
</table>

