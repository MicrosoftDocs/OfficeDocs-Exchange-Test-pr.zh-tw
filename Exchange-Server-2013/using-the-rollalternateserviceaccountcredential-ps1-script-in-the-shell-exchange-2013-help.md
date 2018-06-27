---
title: '在命令介面中使用 RollAlternateserviceAccountCredential.ps1 指令碼: Exchange 2013 Help'
TOCTitle: 在命令介面中使用 RollAlternateserviceAccountCredential.ps1 指令碼
ms:assetid: 6ac55aae-472a-4ed6-83df-2d0e7b48e05c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Ff808311(v=EXCHG.150)
ms:contentKeyID: 63915414
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 在命令介面中使用 RollAlternateserviceAccountCredential.ps1 指令碼

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-03-09_

您可以使用 RollAlternateServiceAccountPassword.ps1 指令碼中的 「 Exchange Server 2013 fto 更新備用服務帳戶認證 （ASA 認證） 並散發至指定的用戶端存取伺服器的更新。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Exchange管理命令介面不會自動載入指令碼。您需要使用的所有指令碼前面加上&quot;<strong>。 \</strong>&quot;例如，若要執行 RollAlternateServiceAccountPassword.ps1 指令碼，請輸入 [ <code>.\RollAlternateServiceAccountPassword.ps1</code>。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>此指令碼僅提供英文版。</td>
</tr>
</tbody>
</table>


如需如何使用和撰寫指令碼的詳細資訊，請參閱[使用 Exchange 管理命令介面撰寫指令碼](https://technet.microsoft.com/zh-tw/library/bb123798\(v=exchg.150\))。

## 語法

    RollAlternateServiceAccountPassword.ps1 -Scope <Object> -Identity <Object> -Source <Object> -

## 詳細描述

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱Client Access Permissions 主題中的 「 用戶端存取安全性 」 項目。

## 備用服務帳戶認證指令碼的技術詳細資料

此指令碼有助於安裝和維護 ASA 認證。您已建立 ASA 認證及設定適當的服務主要名稱之後，您可以使用指令碼來散佈至目標的所有用戶端存取伺服器的認證。

若要使用指令碼，您需要找出您想將目標放在和想要作為 ASA 認證的認證哪些伺服器。

## 伺服器範圍

您可以選擇讓指令碼目標樹系中的所有用戶端存取伺服器、 特定的 Client Access server 陣列或特定伺服器的所有成員。可用的參數為*ToEntireForest*、 *ToArraryMembers*及*ToSpecificServers*。如果目標指令碼至特定伺服器或特定伺服器陣列、 *Identity*參數的成員必須使用伺服器或伺服器陣列名稱指定您想要為目標。

## 認證來源

指令碼可以從現有的伺服器複製的備用服務帳戶密碼。或者，您可以指定您想要使用讓指令碼產生新密碼之帳戶的帳戶。可用的參數是*GenerateNewPasswordFor*和*CopyFrom*。*GenerateNewPasswordFor*參數需要您以下列格式指定帳戶字串： 為 「 網域 \\ 名稱。如果您使用的電腦帳戶，您需要附加"$"結尾處的帳戶名稱，例如 CONTOSO\\ClientServerAcct$。*CopyFrom*參數為認證來源採用現有的用戶端存取伺服器的名稱。

## 產生新密碼的認證

指令碼來建立密碼。沒有使用者的輸入是必要的。指令碼會嘗試散佈至所有目標電腦、 密碼和便會嘗試更新Active Directory帳戶認證新產生的密碼。

新產生密碼、 73 字元並將滿足標準的強式密碼需求。如果您的密碼需求不同，可能需要手動設定密碼和再將它複製到目標伺服器。

若要防止服務中斷，指令碼會檢查每個用戶端存取伺服器和維護目前的密碼除了新增新的密碼。共用的 ASA 認證執行指令碼之後，要能夠使用其中一項 2 的密碼： 目前的密碼為儲存在Active Directory或尚未尚未Active Directory中設定的新密碼。

會從目的地伺服器中移除所有已不再有效，例如過期的密碼的密碼。如果無法變更Active Directory中的密碼，或許因為密碼已到期、 指令碼會嘗試重設密碼。此作業需要執行指令碼以具備重設Active Directory電腦帳戶密碼或使用者帳戶的密碼，視您的備用服務帳戶是電腦帳戶或使用者帳戶的權限的帳戶。

如果所有目標用戶端存取伺服器未成功都變更密碼、 更新Active Directory密碼會導致驗證失敗。如果在自動模式中執行指令碼，它將不會Active Directory密碼使用更新的新密碼除非目標的所有用戶端存取伺服器已更新成功。如果在手動模式中執行指令碼，系統會要求您是否要更新的Active Directory的密碼。

## 建立排定的工作來自動化密碼維護

如果您想要建立排定的工作來維護持續密碼的指令碼，請使用*CreateScheduledTask*參數。此參數需要針對您想要建立的工作名稱的字串。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>執行指令碼，並驗證其運作正常在手動模式中建立自動排程的任務之前。</td>
</tr>
</tbody>
</table>


指令碼建立.cmd 檔案指令碼所在的資料夾中。接著會建立執行該.cmd 檔案每三個星期工作。您可以使用Windows工作排程器來修改排定的工作，例如、 將其設為增加或減少經常執行。根據預設，會為目前登入使用者執行工作。此外，指令碼時才會執行使用者登入電腦。我們建議您修改不論使用者登入與否均執行排定的工作。若該帳戶具有Active Directory重設密碼為 Exchange 企業系統管理員角色的權限您也可以選擇執行不同的帳戶下。建立排定的工作，將自動會以自動模式執行指令碼。

## 超出範圍的指令碼的工作

指令碼將不會管理 ASA 認證的 Spn 或可讓您從伺服器中移除的備用服務帳戶。若要移除之伺服器的備用服務帳戶，請參閱[設定負載平衡的 Client Access server 的 Kerberos 驗證](configuring-kerberos-authentication-for-load-balanced-client-access-servers-exchange-2013-help.md)[關閉開啟的 Kerberos 驗證](configuring-kerberos-authentication-for-load-balanced-client-access-servers-exchange-2013-help.md)節。

## 疑難排解指令碼

我們建議您執行指令碼並驗證其運作正常在手動模式中建立自動排程的任務之前。如需疑難排解資訊，請參閱[疑難排解 RollAlternateServiceAccountCredential.ps1 指令碼](troubleshooting-the-rollalternateserviceaccountcredential-ps1-script-exchange-2013-help.md)。

## 驗證指令碼

當您執行的指令碼的輸出以互動方式與-verbose 旗標應該指出哪些指令碼作業成功。若要確認已更新用戶端存取伺服器，您可以確認 ASA 認證上的上次修改的時間戳記。下列範例會將會產生的用戶端存取伺服器清單和上次更新的備用服務帳戶。

    Get-ClientAccessServer -IncludeAlternateServiceAccountCredentialstatus |Fl Name, AlternateServiceAccountConfiguration

您也可以檢查事件記錄檔在其執行指令碼之電腦上。指令碼的事件記錄項目都在應用程式事件記錄檔並從來源*MSExchange Management Application*。下表列出所記錄的事件及事件的意義。

### 事件識別碼和其說明使用指令碼

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>事件</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>14001</p></td>
<td><p>開始</p></td>
</tr>
<tr class="even">
<td><p>14002</p></td>
<td><p>成功 （資訊）</p></td>
</tr>
<tr class="odd">
<td><p>14003</p></td>
<td><p>成功警告但。</p>
<p>指令碼遇到一些問題，但可以克服這些，或使用者的輸入確認他們未必要。如果指令碼以互動式模式執行時，請閱讀進一步警告的詳細資訊的指令碼輸出。</p></td>
</tr>
<tr class="even">
<td><p>14004</p></td>
<td><p>失敗</p></td>
</tr>
</tbody>
</table>


若為排程工作執行指令碼，其結果會記錄Exchange伺服器**記錄**資料夾呼叫**RollAlternateServiceAccountPassword**子資料夾中。

您可以使用記錄檔以確認已成功執行的工作。

## 參數


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
<td><p><em>ToEntireForest</em></p></td>
<td><p>選用</p></td>
<td><p><em>ToEntireForest</em>參數指定目標樹系中的所有用戶端存取伺服器指令碼。</p></td>
</tr>
<tr class="even">
<td><p><em>ToArrayMembers</em></p></td>
<td><p>選用</p></td>
<td><p><em>ToArrayMembers</em>參數是針對指令碼以特定的用戶端存取伺服器陣列中的所有成員。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您使用<em>ToArrayMembers</em>參數或<em>ToSpecificServers</em>參數，您需要指定的伺服器名稱或使用<em>Identity</em>參數的伺服器陣列名稱。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="odd">
<td><p><em>ToSpecificServers</em></p></td>
<td><p>選用</p></td>
<td><p><em>ToSpecificServers</em>參數是針對特定伺服器的指令碼。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您使用<em>ToArrayMembers</em>參數或<em>ToSpecificServers</em>參數，您需要指定的伺服器名稱或使用<em>Identity</em>參數的伺服器陣列名稱。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p><em>Identity</em>參數會指定用戶端存取伺服器陣列中的名稱或您想採用的特定伺服器的名稱。</p></td>
</tr>
<tr class="odd">
<td><p><em>GenerateNewPasswordFor&lt;String&gt;</em></p></td>
<td><p>選用</p></td>
<td><p><em>GenerateNewPasswordFor</em>參數會指定指令碼應該如 ASA 產生新密碼。字串值必須以下列格式的 ASA 帳戶： 為 「 網域 \ 名稱。如果您使用的電腦帳戶，您需要附加 $ 字元結尾處的帳戶名稱。</p></td>
</tr>
<tr class="even">
<td><p><em>CopyFrom&lt;String&gt;</em></p></td>
<td><p>選用</p></td>
<td><p><em>CopyFrom</em>參數會指定認證會複製來自另一個用戶端存取伺服器。指定的字串值是用戶端存取伺服器的名稱。</p></td>
</tr>
<tr class="odd">
<td><p><em>Mode</em></p></td>
<td><p>選用</p></td>
<td><p><em>Mode</em>參數會指定是否在手動或自動模式中執行指令碼。自動的模式不會提示使用者輸入並自動選擇 [更多傳統時所需的選項。</p></td>
</tr>
<tr class="even">
<td><p><em>CreateScheduledTask&lt;String&gt;</em></p></td>
<td><p>選用</p></td>
<td><p><em>CreateScheduledTask</em>參數指示指令碼建立排定的工作來執行 ASA 認證更新。字串值是工作的要建立排定的名稱。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>此指令碼建立.cmd 檔案指令碼所在的資料夾中。排定的工作會執行一次每三個星期.cmd 檔案。您可以編輯任務直接在Windows工作排程器來變更工作的頻率。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p><em>WhatIf</em> 參數會指示命令模擬它將對物件採取的動作。透過使用 <em>WhatIf</em> 參數，不需要套用任何變更，就能檢視變更。您不需要利用 <em>WhatIf</em> 參數指定值。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p><em>Confirm</em> 參數會使得命令暫停處理，並要求確認命令將進行的動作，之後才會繼續處理。您不需要利用 <em>Confirm</em> 參數指定任何值。</p></td>
</tr>
<tr class="odd">
<td><p><em>Verbose</em></p></td>
<td><p>選用</p></td>
<td><p><em>Verbose</em>參數會指示要執行詳細資訊記錄，讓指令碼的動作的其他資訊寫入記錄檔的指令碼。</p></td>
</tr>
<tr class="even">
<td><p><em>Debug</em></p></td>
<td><p>選用</p></td>
<td><p><em>Debug</em>參數會指示要偵錯模式中執行的指令碼。應使用這個參數來決定指令碼失敗的原因。</p></td>
</tr>
</tbody>
</table>


## 範例

## 範例 1

此範例會使用指令碼推送到首次設定的樹系中的所有用戶端存取伺服器的認證。

    .\RollAlternateserviceAccountPassword.ps1 -ToEntireForest -GenerateNewPasswordFor "Contoso\ComputerAccount$" -Verbose

## 範例 2

此範例會產生新密碼的使用者帳戶 ASA 認證並分散每個圖形的名稱必須符合其中的用戶端存取伺服器陣列中的所有成員的密碼 \* 信箱 \*。

    .\RollAlternateserviceAccountPassword.ps1 -ToArrayMembers *mailbox* -GenerateNewPasswordFor "Contoso\UserAccount" -Verbose

## 範例 3

本範例會排程一個月一次的自動化的密碼 roll 排定的工作稱為 「 Exchange RollAsa"。將會更新整個樹系中的所有用戶端存取伺服器 ASA 認證使用新的、 指令碼產生的密碼。建立排定的工作時，但不是執行指令碼。執行排定的工作時，會在自動模式中執行指令碼。

    .\RollAlternateServiceAccountPassword.ps1 -CreateScheduledTask "Exchange-RollAsa" -ToEntireForest -GenerateNewPasswordFor 'contoso\computerAccount$'

## 範例 4

此範例會更新名為 CAS01 的 Client Access server 陣列中的所有用戶端存取伺服器 ASA 認證。它會從 Contoso 網域中的Active Directory電腦帳戶 ServiceAc1 取得認證。

    .\RollAlternateserviceAccountPassword.ps1 -ToArrayMembers "CAS01" -GenerateNewPasswordFor "CONTOSO\ServiceAc1$" 

## 範例 5

此範例顯示如何使用指令碼，散發 ASA 到新電腦或被放回服務可能是因為您正在增加伺服器陣列的大小或是您正在重新簡介 （英文） 陣列成員維護之後的電腦。

您需要更新 ASA 認證之前的用戶端存取伺服器會接收的流量。從任何已正確設定的用戶端存取伺服器複製共用的 ASA 認證。例如，如果伺服器的目前已使用 ASA 認證與您剛新增伺服器 B 陣列，您可用於指令碼複製 （包括密碼） 認證來自伺服器的伺服器 b。這是有用如果 Server B 是向下或尚未陣列當密碼彙上次的成員。

    .\RollAlternateServiceAccountPassword.ps1 -CopyFrom ServerA -ToSpecificServers ServerB -Verbose

