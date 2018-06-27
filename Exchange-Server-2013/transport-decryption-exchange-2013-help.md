---
title: '傳輸解密: Exchange 2013 Help'
TOCTitle: 傳輸解密
ms:assetid: 4267c46d-f488-404d-a5cb-51f9127461c0
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd638122(v=EXCHG.150)
ms:contentKeyID: 50473114
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 傳輸解密

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2015-04-07_

在 Microsoft Exchange Server 2013、 Microsoft Outlook 2010和更新版本、 Microsoft OfficeOutlook Web App，使用者可以使用資訊版權管理 (IRM) 來保護其訊息。您可以建立Outlook自動將 IRM 保護套用至郵件它們傳送自Outlook 2010用戶端之前的保護規則。您也可以建立傳輸保護規則將 IRM 保護套用至符合的規則條件的郵件傳輸。停用傳輸解密允許以強制執行郵件原則受 IRM 保護之訊息內容的存取權。

如需管理 IRM 的相關管理工作之詳細資訊，請參閱[資訊版權管理程序](information-rights-management-procedures-exchange-2013-help.md)。

## 其他加密解決方案的限制

如果是關鍵貴組織保護機密資訊，包括高的業務影響 (HBI) 資訊及個人識別資訊 (PII)，請考慮加密電子郵件訊息與附件。S/MIME 等的電子郵件加密解決方案已提供較長的時間。這些加密解決方案看過採用在組織中的不同類型的程度。但是，這類解決方案會呈現下列挑戰：

  - **無法套用郵件原則**  組織也會面臨需要檢查有以確定它遵守郵件原則的郵件內容的規範需求。不過，使用最用戶端型加密解決方案，包括 S/MIME 加密的郵件會防止在伺服器上的內容進行檢查。不含內容檢查組織無法驗證傳送或接收其使用者所擁有的所有郵件都遵守通訊原則。例如，遵守法律法規，您已設定偵測 PII，例如社會安全號碼，並自動要對郵件套用免責聲明的傳輸規則。如果，加密郵件上的傳輸服務的傳輸規則代理程式無法存取郵件內容與因此將不會套用免責聲明。這會產生衝突的原則。

  - **減少安全性**  防毒軟體仍無法掃描加密的郵件內容，例如病毒和蠕蟲惡意內容從進一步公開風險的組織。加密的郵件通常會視為信任大部分的使用者，進而提高分配整個組織中的病毒的可能性。例如，您已設定自動將 IRM 保護套用到所有郵件傳送給所有員工通訊群組清單與公司機密 rights management service (RMS) 範本Outlook保護規則。自動回覆郵件使用 \[全部回覆傳播病毒感染使用者的工作站。如果要加密郵件運輸病毒、 防毒掃描程式無法掃描 \[郵件\]。

  - **自訂傳輸代理程式的影響**  許多組織開發自訂傳輸代理程式不同的用途，例如會議規範、 安全性或自訂的郵件路由的其他處理需求。自訂傳輸代理程式所組織開發，檢查或修改的郵件都無法處理加密的郵件。如果自訂傳輸代理程式所開發您的組織無法存取郵件內容、 加密可能會防止從會議的自訂傳輸代理程式所開發的目標組織的郵件。

## 將傳輸解密用於加密內容

Exchange 2013、 中的 IRM 功能會解決這些挑戰。如果受 IRM 保護的郵件，停用傳輸解密可讓您將其解密傳送過程中。解密代理程式規範為主傳輸代理程式所對進行解密受 IRM 保護的郵件。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在Exchange 2013、 解密代理程式會為內建的代理程式。內建的代理程式未含的<strong>Get-TransportAgent</strong>指令程式傳回的代理程式清單中。如需詳細資訊，請參閱<a href="transport-agents-exchange-2013-help.md">傳輸代理程式</a>。</td>
</tr>
</tbody>
</table>


解密代理程式將解密下列類型的 IRM 保護郵件：

  - Outlook Web App 中使用者以 IRM 保護的郵件。

  - Outlook 2010 中使用者以 IRM 保護的郵件。

  - Outlook 與 Outlook 2010中由 Exchange 2013 保護規則自動以 IRM 保護的郵件。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>只有組織中由 AD RMS Server 以 IRM 保護的郵件可由解密代理程式進行解密。</td>
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
<td>受保護的郵件傳送過程中使用傳輸的保護規則都可省略解密代理程式所進行解密。解密代理程式就會引發<strong>OnEndOfData</strong>和<strong>OnSubmit</strong>傳輸事件。傳輸保護規則會套用由傳輸規則代理程式，就會引發<strong>OnRoutedMessage</strong>事件，並 IRM 保護套用由加密代理程式上<strong>OnRoutedMessage</strong>事件。如需傳輸代理程式並在其他們可以註冊的 SMTP 事件清單的詳細資訊，請參閱<a href="transport-agents-exchange-2013-help.md">傳輸代理程式</a>。</td>
</tr>
</tbody>
</table>


停用傳輸解密是在第一個Exchange 2013處理Active Directory樹系中的郵件的傳輸服務上執行。如果郵件傳送給其他Active Directory樹系中的傳輸服務之後，會再次解密訊息。解密之後, 未加密的內容是可在該伺服器上的其他傳輸代理程式。例如上傳輸服務, 的傳輸規則代理程式可檢查郵件內容並套用傳輸規則。在未加密的郵件採取任何規則，例如套用免責聲明或修改任何其他方法中的郵件中指定的動作。第三方傳輸代理程式，例如防毒掃描程式，可以描病毒和惡意程式碼的郵件。之後其他傳輸代理程式已檢查訊息和可能進行修改它，它會再次使用加密前解密代理程式所要解密的相同使用者權限。解密的相同郵件不是一次由其他傳輸服務在組織中其他 Mailbox server 上。

解密代理程式所解密的郵件不保留的傳輸服務而不重新加密。如果解密或加密郵件時則會傳回暫時性錯誤的傳輸服務重試作業兩次。第三個故障後的錯誤都會視為永久錯誤。如果發生任何永久錯誤，包括當暫時性錯誤視為永久錯誤重試次數之後, 的傳輸服務來說它們，如下所示：

  - 如果解密期間發生永久錯誤，只有當停用傳輸解密設為`Mandatory`，且具有 NDR 傳送加密的郵件傳送未傳遞回報 (NDR)。如需可用以停用傳輸解密的組態選項的詳細資訊，請參閱本主題稍後的設定停用傳輸解密。

  - 如果重新加密期間發生永久性錯誤，則一律傳送 NDR，而不會傳送解密的郵件。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>傳輸服務上安裝任何自訂或協力廠商代理程式可以存取已解密的郵件。您必須考慮這類傳輸代理程式的行為。我們建議您先徹底測試所有自訂或協力廠商的傳輸代理程式部署在實際執行環境之前。<br />
將郵件解密解密代理程式所之後新增一個新的郵件至原始郵件如果傳輸代理程式會建立新的訊息與內嵌 （附加） 受到保護。原始郵件會變成新郵件的附件，不會取得重新加密。接收這類郵件的收件者可以開啟附加的郵件，並採取動作如轉寄或回覆，這會略過強制執行權限。</td>
</tr>
</tbody>
</table>


## 設定傳輸解密

停用傳輸解密Exchange管理命令介面中使用[Set-IRMConfiguration](https://technet.microsoft.com/zh-tw/library/dd979792\(v=exchg.150\))指令程式來設定。不過，您設定停用傳輸解密之前，您必須提供Exchange 2013伺服器解密受保護您的 AD RMS 伺服器的內容的權限。做法是設定在組織中的 AD RMS 叢集超級使用者群組新增同盟信箱。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在跨樹系 AD RMS 部署中必須在每個樹系中部署 AD RMS 叢集，您必須將同盟信箱新增至每個樹系中的 AD RMS 叢集的超級使用者群組允許Exchange 2013 Mailbox server 或解密針對每個 AD RMS 叢集受保護的郵件Exchange 2010 Hub Transport server 上的傳輸服務。</td>
</tr>
</tbody>
</table>


如需詳細資訊，請參閱[至 AD RMS 超級使用者群組新增同盟信箱](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md)。

Exchange 2013 允許啟用傳輸解密時使用兩個不同的設定：

  - **必要項目**  停用傳輸解密設為`Mandatory`、 時解密代理程式拒絕郵件，並如果永久錯誤會傳回時解密郵件會 NDR 傳回給寄件者。如果您的組織不想如果它不能順利解密及動作，例如防毒掃描和傳輸規則會套用傳遞訊息，您必須選擇此設定。

  - **選用**  停用傳輸解密設為選用、 時解密代理程式會使用最佳的方法。進行解密進行解密的郵件，但也會傳遞永久錯誤上解密的郵件。如果您的組織設定與郵件原則優先順序的訊息傳遞，您必須使用此設定。

如需設定傳輸解密的詳細資訊，請參閱[啟用或停用傳輸解密](enable-or-disable-transport-decryption-exchange-2013-help.md)。

