---
title: '日誌報告解密: Exchange 2013 Help'
TOCTitle: 日誌報告解密
ms:assetid: c063e2bd-2444-480d-8b35-73f31064a31b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd876936(v=EXCHG.150)
ms:contentKeyID: 50474104
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 日誌報告解密

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2012-10-16_

在 Microsoft Exchange Server 2013、 資訊版權管理 (IRM) 能讓 Microsoft Outlook 2010及更新版本和 Microsoft OfficeOutlook Web App使用者來保護其訊息。您可以建立Outlook自動將 IRM 保護套用至郵件它們傳送自Outlook 2010用戶端之前的保護規則。您也可以建立傳輸保護規則將 IRM 保護套用至符合的規則條件的郵件傳輸。

若要瞭解有關 Outlook 保護規則，請參閱 [Outlook 保護規則](outlook-protection-rules-exchange-2013-help.md)。

## 標準加密解決方案的限制

如果您的組織使用 S/MIME 等的傳統解決方案加密的郵件，記錄管理員將無法檢查或搜尋已加密的內容。封存加密的郵件包含無法存取和無法搜尋的內容可能不會符合法規商務或規範需求。搜尋伺服器與呈現的內容從加密郵件時面臨電子化搜索 (eDiscovery) 要求中，無法解密，可以是挑戰和這樣可能鍰等組織法律與財務風險。

此外，您組織的郵件原則可能需要讓內容可存取 eDiscovery 工具、 自動化程序，或存取日誌記錄信箱的記錄經理解密的日誌訊息。在 Exchange 2010 中的日誌報告解密可協助您符合下列需求。

若要深入了解日誌記錄，請參閱[日誌](journaling-exchange-2013-help.md)。

## 日誌報告解密

日誌報告解密可讓您將受 IRM 保護之訊息的純文字複本儲存除了原始的受 IRM 保護之訊息的日誌報告。如果受 IRM 保護之訊息包含已受到Active Directory Rights Management Services (AD RMS) 叢集中在組織中任何支援的附件，附件同時解密。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要使用日誌報告解密，您必須具備Exchange企業用戶端存取授權 (CAL)。日誌報告解密僅支援 premium 日誌記錄。</td>
</tr>
</tbody>
</table>


解密是由日誌報告解密代理程式規範為主傳輸代理程式執行。日誌報告解密代理程式就會引發**OnCategorizedMessage**事件。受保護的郵件傳送過程中使用傳輸的保護規則已加密來加密代理程式就會引發**OnRoutedMessage**事件之前所要取得日誌報告解密代理程式。日誌報告解密代理程式解密這些訊息。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在Exchange 2013、 日誌報告解密代理程式會為內建的代理程式。內建的代理程式未含的<strong>Get-TransportAgent</strong>指令程式傳回的代理程式清單中。如需詳細資訊，請參閱<a href="transport-agents-exchange-2013-help.md">傳輸代理程式</a>。</td>
</tr>
</tbody>
</table>


代理程式會解密下列類型的 IRM 保護郵件：

  - 由使用者在 Outlook Web App 中 IRM 保護的郵件。

  - 由使用者在 Outlook 2010 中 IRM 保護的郵件。

  - 使用 Outlook 保護規則在 Outlook 2010 中自動 IRM 保護的郵件。

  - 藉由使用傳輸保護規則，在轉送過程中自動 IRM 保護的郵件。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>只是由您組織中的 AD RMS 伺服器受 IRM 保護的郵件進行解密日誌報告解密代理程式。如果它不受保護的郵件同時 （與因此都不會有一個使用授權） 或受 IRM 保護之檔案附加至未受保護的郵件代理程式不會解密附件。</td>
</tr>
</tbody>
</table>


## 設定日誌報告解密

日誌報告解密是 configuredb Exchange管理命令介面中使用[Set-IRMConfiguration](https://technet.microsoft.com/zh-tw/library/dd979792\(v=exchg.150\))指令程式。不過，您設定日誌報告解密之前，您必須指派Exchange 2013伺服器解密 AD RMS 伺服器所受 IRM 保護的內容的權限。為達成此目的，您可以新增同盟信箱來設定您的組織 AD RMS 叢集上超級使用者群組。如需詳細資訊，請參閱[至 AD RMS 超級使用者群組新增同盟信箱](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在每個樹系中都部署 AD RMS 叢集的跨樹系 AD RMS 部署中，您必須將同盟信箱新增至每個樹系的 AD RMS 叢集上的進階使用者群組，以便允許 Exchange 2013 傳輸服務解密受每個 AD RMS 叢集保護的郵件。</td>
</tr>
</tbody>
</table>


如需如何設定日誌報告解密的相關資訊，請參閱 [啟用或停用日誌報告解密](enable-or-disable-journal-report-decryption-exchange-2013-help.md)。

啟用日誌報告解密之後，日誌記錄信箱可能包含敏感資訊未加密的表單中的日誌報告。最佳作法是建議的日誌記錄信箱存取權是密切監視和僅限於授權個人。這是最佳作法即使您不使用 IRM 保護的電子郵件。

