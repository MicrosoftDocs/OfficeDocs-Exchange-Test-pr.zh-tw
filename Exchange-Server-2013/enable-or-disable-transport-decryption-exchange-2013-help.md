---
title: '啟用或停用傳輸解密: Exchange 2013 Help'
TOCTitle: 啟用或停用傳輸解密
ms:assetid: 4663f54e-dd0a-4a42-983e-8765e2adc412
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd638126(v=EXCHG.150)
ms:contentKeyID: 50473045
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 啟用或停用傳輸解密

 

_**適用版本：**Exchange Online, Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

啟用停用傳輸解密可讓 Microsoft Exchange Server 2013上的傳輸規則代理程式來存取內容的資訊版權管理 (IRM) 保護之訊息中的信箱伺服器。因此，其他傳輸代理程式可以存取郵件內容和可能是進行變更。例如，「 傳輸規則代理程式 」 可能需要檢查郵件內容並套用傳輸規則 （如要對郵件套用免責聲明的規則）。成功解密受 IRM 保護的郵件，您必須將同盟傳遞信箱新增至[Active Directory Rights Management Services (AD RMS)](https://technet.microsoft.com/en-us/library/hh831364.aspx) server 上設定的超級使用者群組。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>超級使用者授與擁有者群組的成員可以使用授權時所要求的授權從 AD RMS 叢集。這可讓其解密建立該 AD RMS 叢集的所有與 RMS 受保護的內容。</td>
</tr>
</tbody>
</table>


當啟用 \[停用傳輸解密，您可以指定下列設定：

  - **必要項目**  拒絕無法解密的郵件的郵件，並傳回給寄件者的未傳遞回報 (NDR)。

  - **選用**  使用解密的最佳方法。請儘可能進行解密的郵件，但他們正在傳遞即使解密失敗。這是預設設定。

深入了解停用傳輸解密、 請參閱 ＜ [傳輸解密](transport-decryption-exchange-2013-help.md)。

若欲瞭解更多與 IRM 相關的管理工作，請參閱 [資訊版權管理程序](information-rights-management-procedures-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：5 分鐘。

  - 您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [郵件原則及符合性權限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主題中的「版權保護」項目。

  - AD RMS 伺服器Active Directory樹系中存在和可以存取。

  - 已新增同盟傳遞信箱至 AD RMS 超級使用者群組。如需詳細資訊，請參閱[至 AD RMS 超級使用者群組新增同盟信箱](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md)。

  - Exchange 系統管理中心 (EAC) 無法用以啟用停用傳輸解密。您必須使用命令介面。

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


## 您要執行的工作

## 使用命令介面來啟用停用傳輸解密

本範例啟用傳輸解密Exchange 2013組織。要拒絕無法解密的郵件的郵件和 NDR 傳回給傳送者。

    Set-IRMConfiguration -TransportDecryptionSetting Mandatory

如需詳細的語法及參數資訊，請參閱 [Set-IRMConfiguration](https://technet.microsoft.com/zh-tw/library/dd979792\(v=exchg.150\))。

## 使用命令介面來停用傳輸解密

本範例會停用傳輸解密Exchange 2013組織。

    Set-IRMConfiguration -TransportDecryptionSetting Disabled

如需詳細的語法及參數資訊，請參閱 [Set-IRMConfiguration](https://technet.microsoft.com/zh-tw/library/dd979792\(v=exchg.150\))。

## 如何才能了解運作是否正常？

若要確認您是否已啟用或停用傳輸解密、 使用**Get-IRMConfiguration**指令程式，並檢查*JournalDecryptionEnabled*屬性的值。

如需如何檢查 IRM 組態的範例，請參閱 **Get-IRMConfiguration** 中的[Examples](https://technet.microsoft.com/zh-tw/e1821219-fe18-4642-a9c2-58eb0aadd61a\(exchg.150\)#examples)。

