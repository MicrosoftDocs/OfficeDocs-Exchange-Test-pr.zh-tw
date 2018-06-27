---
title: '啟用或停用用戶端存取伺服器上的資訊版權管理: Exchange 2013 Help'
TOCTitle: 啟用或停用用戶端存取伺服器上的資訊版權管理
ms:assetid: c7ce069b-a572-4755-90a3-7105472e4c83
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd876938(v=EXCHG.150)
ms:contentKeyID: 50474167
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟用或停用用戶端存取伺服器上的資訊版權管理

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

用戶端存取伺服器上啟用資訊版權管理 (IRM) 啟用下列功能：

  - Microsoft Office Outlook Web App

  - 在 Microsoft Exchange ActiveSync的 IRM

當用戶端存取伺服器上啟用 IRM 時，則Outlook Web App使用者可以藉由套用 AD RMS 叢集上建立一個[Active Directory Rights Management Services (AD RMS)](https://technet.microsoft.com/en-us/library/hh831364.aspx)範本 IRM 保護的郵件。Outlook Web App使用者也可以檢視受 IRM 保護的郵件和支援的附件。在用戶端存取伺服器上啟用 IRM 之前，您必須以 AD RMS 叢集的超級使用者群組新增同盟信箱。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>超級使用者授與擁有者群組的成員可以使用授權時所要求的授權從 AD RMS 叢集。這可讓它們可以由該叢集解密受 RMS 保護的所有內容。</td>
</tr>
</tbody>
</table>


若欲瞭解更多與 IRM 相關的管理工作，請參閱 [資訊版權管理程序](information-rights-management-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間： 1 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的 「 資訊版權管理 (IRM) 組態 」 項目。

  - AD RMS 叢集必須安裝在 Active Directory 樹系中。

  - 同盟信箱已新增到 AD RMS 超級使用者群組。如需詳細指示，請參閱[至 AD RMS 超級使用者群組新增同盟信箱](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md)。

  - 必須啟用組織的 IRM 功能。如需詳細指示，請參閱[啟用或停用內部郵件的 IRM](enable-or-disable-irm-for-internal-messages-exchange-2013-help.md)。

  - 您可以使用**Set-IRMConfiguration**指令程式啟用或Exchange ActiveSync整個Exchange組織或特定層級中停用 IRM Outlook Web App和 IRM。
    
    您可以在下列層級的Outlook Web App控制 IRM：
    
      - **每個 Outlook Web App 虛擬目錄**   若要在 Outlook Web App 中啟用或停用 Outlook Web App 虛擬目錄的 IRM，請使用 **Set-OWAVirtualDirectory** Cmdlet，並且將 *IRMEnabled* 參數設定為 `$false` 或 `$true` (預設)。如此一來，您就可以在 Exchange 2013 用戶端存取伺服器上停用 Outlook Web App 中一個虛擬目錄的 IRM，而在另一部用戶端存取伺服器上的另一個虛擬目錄中讓它維持啟用狀態。
    
      - **每個 Outlook Web App 信箱原則**   若要在 Outlook Web App 中啟用或停用 Outlook Web App 信箱原則的 IRM，請使用 **Set-OWAMailboxPolicy** Cmdlet，並且將 *IRMEnabled* 參數設定為 `$false` 或 `$true` (預設)。如此一來，您就可以指派不同的 Outlook Web App 信箱原則，在 Outlook Web App 中為一組使用者啟用 IRM，並且為另一組使用者停用 IRM。
    
    您可以控制 IRM Exchange ActiveSync個別Exchange ActiveSync信箱原則中。若要停用或啟用 IRM Exchange ActiveSyncExchange ActiveSync信箱原則中，使用**Set-ActiveSyncMailboxPolicy**指令程式並將*IRMEnabled*參數設定為`$false`或`$true` （預設值）。這可讓您在Exchange ActiveSync的一組使用者啟用 IRM 和它的另一組使用者停用其指派不同Exchange ActiveSync信箱原則。

  - 您無法使用 Exchange 系統管理中心 (EAC) 來啟用或停用用戶端存取伺服器上的 IRM。您必須使用命令介面。

## 您要執行的工作

## 使用命令介面來啟用用戶端存取伺服器上的 IRM

本範例會在Exchange組織的用戶端存取伺服器上啟用 IRM。

    Set-IRMConfiguration -ClientAccessServerEnabled $true

如需詳細的語法及參數資訊，請參閱 [Set-IRMConfiguration](https://technet.microsoft.com/zh-tw/library/dd979792\(v=exchg.150\))。

## 使用命令介面來停用用戶端存取伺服器上的 IRM

本範例會停用 IRM Exchange組織的 Client Access server 上。

    Set-IRMConfiguration -ClientAccessServerEnabled $false

如需詳細的語法及參數資訊，請參閱 [Set-IRMConfiguration](https://technet.microsoft.com/zh-tw/library/dd979792\(v=exchg.150\))。

## 如何才能了解這是否正常運作？

若要確認您具有已順利啟用或停用 IRM Client Access server 上，執行下列動作：

  - 執行**Get-IRMConfiguration**指令程式，並檢查*ClientAccessServerEnabled*屬性的值。
    
    如需如何將擷取的 IRM 組態的範例，請參閱**Get-IRMConfiguration**中的[範例](https://technet.microsoft.com/zh-tw/e1821219-fe18-4642-a9c2-58eb0aadd61a\(exchg.150\)#examples)。

  - 若要建立或讀取受 IRM 保護郵件中使用Outlook Web App 。

