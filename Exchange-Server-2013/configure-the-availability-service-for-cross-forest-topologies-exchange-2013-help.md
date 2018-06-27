---
title: '設定跨樹系拓撲的可用性服務: Exchange 2013 Help'
TOCTitle: 設定跨樹系拓撲的可用性服務
ms:assetid: f1e7d407-f0d3-47a7-8cc3-03c5980445d5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb125182(v=EXCHG.150)
ms:contentKeyID: 52062603
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定跨樹系拓撲的可用性服務

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2014-10-22_

透過提供執行 MicrosoftOutlook 的用戶端安全、一致且最新的空閒/忙碌資訊，可用性服務改善了增進資訊工作者的空閒/忙碌資訊。依預設，此服務會與 Exchange Server 2013 一起安裝。在所有連接的用戶端都執行 Outlook 的跨樹系拓撲中，可用性服務是擷取空閒/忙碌資訊的唯一方法。您可以使用命令介面來設定跨樹系拓撲的可用性服務。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您無法使用 EAC 來設定跨樹系拓撲的可用性服務。</td>
</tr>
</tbody>
</table>


## 在信任和不信任的樹系中使用「可用性」服務

您可以在跨越信任或不信任樹系的跨樹系拓撲中使用可用性服務。可用的空閒/忙碌資訊類型，會視您目前使用的是信任或不信任的樹系而定。

**信任的樹系**   在信任的樹系中，您可以設定可用性服務，以每位使用者為基礎擷取空閒/忙碌資訊。當可用性服務設為以每位使用者為基礎擷取空閒/忙碌資訊，服務可以代表特定使用者進行跨樹系要求。如此可讓遠端樹系中的使用者為其他樹系中的特定對象擷取詳細的空閒/忙碌資訊。

**不信任的樹系**   在不信任的樹系中，您只能設定可用性服務，以全組織為基礎擷取空閒/忙碌資訊。當可用性服務於組織層級進行空閒/忙碌跨樹系要求時，會傳回組織中每位使用者的空閒/忙碌資訊。在不信任的樹系中，您無法控制以每位使用者為基礎所傳回的空閒/忙碌資訊層級。

## 設定適合跨樹系拓撲的 Windows

依預設，全域通訊清單 (GAL) 包含來自單一樹系的郵件收件者。如果您有跨樹系環境，則建議使用 Microsoft Identity Lifecycle Manager (ILM) 2007 Feature Pack 1 (FP1)，確保任何指定樹系中的 GAL 包含來自其他樹系的郵件收件者。ILM 2007 FP1 可建立郵件使用者來代表來自其他樹系的收件者，進而讓使用者得以在 GAL 中檢視這些連絡人，並傳送郵件。例如，樹系 A 的使用者在樹系 B 中是郵件使用者，反之亦然。然後，目標樹系中的使用者即可選取代表其他樹系收件者的郵件使用者物件，以傳送郵件。

若要啟用「GAL 同步處理」，您必須建立管理代理程式，以便將擁有信箱功能的使用者、連絡人及群組，從指定的 Active Directory 服務匯入集中式的中繼目錄。在中繼目錄中，擁有郵件功能的物件將被當成郵件使用者。群組則代表不具任何相關成員的連絡人。管理代理程式會將這些郵件使用者匯出至指定之目標樹系的組織單位中。

## 開始之前有哪些須知？

  - 每項程序的預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [用戶端和行動裝置權限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主題中的「可用性服務權限」項目。

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

## 使用命令介面，在信任的跨樹系拓撲中設定每一使用者空閒/忙碌資訊

此範例會設定可用性服務，擷取目標樹系中 Mailbox Server 上每位使用者的空閒/忙碌資訊。

    Get-MailboxServer | Add-ADPermission -Accessrights Extendedright -Extendedrights "ms-Exch-
    EPI-Token-Serialization" -User "<Remote Forest Domain>\Exchange servers"

此範例會定義可用性服務在來源樹系中本機 Mailbox Server 上使用的空閒/忙碌存取方法。會設定本機 Mailbox Server 以每位使用者為基礎，從樹系 ContosoForest.com 存取空閒/忙碌資訊。此範例會使用服務帳戶擷取空閒/忙碌資訊。

    Add-AvailabilityAddressSpace -Forestname ContosoForest.com -AccessMethod PerUserFB -UseServiceAccount:$true

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要設定雙向跨樹系可用性，請在目標樹系中重複這些步驟。</td>
</tr>
</tbody>
</table>


如果您選擇設定信任的跨樹系可用性，且同時選擇使用服務帳戶 (而非指定全組織或每位使用者的認證)，您必須依照 \[使用命令介面，設定服務帳戶之信任的跨樹系可用性\] 區段中的範例所示擴充權限。在目標樹系中執行該程序，會將序列化原始使用者內容的權限授予來源樹系中的 Mailbox Server。

## 使用命令介面，設定服務帳戶之信任的跨樹系可用性

本範例會設定服務帳戶之信任的跨樹系可用性。

    Get-MailboxServer | Add-ADPermission -Accessrights Extendedright -Extendedright "ms-Exch-EPI-Token-Serialization" -User "<Remote Forest Domain>\Exchange servers"

如需詳細的語法及參數資訊，請參閱下列主題：

  - [Get-MailboxServer](https://technet.microsoft.com/zh-tw/library/bb123539\(v=exchg.150\))

  - [Add-ADPermission](https://technet.microsoft.com/zh-tw/library/bb124403\(v=exchg.150\))

  - [Add-AvailabilityAddressSpace](https://technet.microsoft.com/zh-tw/library/bb124122\(v=exchg.150\))

  - [Set-AvailabilityConfig](https://technet.microsoft.com/zh-tw/library/bb124103\(v=exchg.150\))

## 使用命令介面，在不信任的跨樹系拓撲中設定全組織的空閒/忙碌資訊

此範例會針對全組織帳戶的可用性設定物件進行設定，以設定目標樹系中空閒/忙碌資訊的存取層級。

    Set-AvailabilityConfig -OrgWideAccount "Contoso.com\User"

此範例會為來源樹系新增可用性位址空間設定物件。

    $a = Get-Credential (Enter the credentials for organization-wide user in Contoso.com domain)
    Add-AvailabilityAddressspace -Forestname Contoso.com -Accessmethod OrgWideFB -Credential:$a

