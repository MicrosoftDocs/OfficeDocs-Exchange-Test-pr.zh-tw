---
title: '設定垃圾郵件隔離信箱: Exchange 2013 Help'
TOCTitle: 設定垃圾郵件隔離信箱
ms:assetid: 907d2f90-2a62-4d59-a4cf-945fef2e963f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Bb123746(v=EXCHG.150)
ms:contentKeyID: 50473726
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定垃圾郵件隔離信箱

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2013-02-19_

郵件取決於是由內容篩選器代理程式的垃圾郵件可以導向到垃圾郵件隔離信箱。啟用垃圾郵件信賴等級 (SCL) 隔離臨界值時，所有已隔離的郵件會被包裝為未傳遞回報 (NDR) 並傳送給您指定為垃圾郵件隔離信箱的 SMTP 位址。您可以檢閱隔離的郵件並在 Microsoft Outlook 中使用一次傳送功能發行給其預定的收件者。

## 開始之前有哪些須知？

  - 完成這項工作預估時間： 45 分鐘。

  - 預設在 Mailbox Server 的 Transport 服務中未啟用反垃圾郵件功能。通常只有在您的 Exchange 組織接受內送郵件之前未進行任何事前的反垃圾郵件篩選的情況下，您才會在 Mailbox Server 上啟用反垃圾郵件功能。如需詳細資訊，請參閱[啟用信箱伺服器上的反垃圾郵件功能](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md)。

  - 負責垃圾郵件隔離信箱的人員可以檢視可能為私人與機密的郵件，並且代表 Exchange 組織中的任何人傳送郵件。

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


## 該怎麼做？

## 步驟 1： 確認已啟用內容篩選

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [反垃圾郵件和反惡意程式的權限](anti-spam-and-anti-malware-permissions-exchange-2013-help.md)主題中的「反垃圾郵件功能」項目。

1.  執行以下命令來驗證 Exchange 伺服器上已安裝並啟用內容篩選器代理程式：
    
        Get-TransportAgent "Content Filter Agent"

2.  執行以下命令來驗證啟用了內容篩選：
    
        Get-ContentFilterConfig | Format-List Enabled

如需詳細資訊，請參閱 [管理內容篩選](manage-content-filtering-exchange-2013-help.md)。

## 步驟 2： 建立專用的信箱的垃圾郵件隔離

若要建立專用的垃圾郵件隔離信箱，請執行以下步驟：

  - **建立專用的 Exchange 資料庫**  我們建議您建立專用的資料庫中的垃圾郵件隔離信箱。垃圾郵件隔離信箱應該有大型的資料庫，因為如果達到儲存配額限制，郵件將會遺失。如需詳細資訊，請參閱[管理 Exchange 2013 中的信箱資料庫](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md)。

  - **建立專用的信箱與使用者帳戶**  我們建議您建立專用的信箱和垃圾郵件隔離信箱的 Active Directory 使用者帳戶。如需詳細資訊，請參閱[建立使用者信箱](create-user-mailboxes-exchange-2013-help.md)。
    
    您可能會套用收件者原則，例如通訊記錄管理、 信箱配額及委派權限，根據您的組織規範遵守原則和需求。如需詳細資訊，請參閱[通訊記錄管理](messaging-records-management-exchange-2013-help.md)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果隔離之郵件被拒絕因儲存配額，郵件將會遺失。Exchange 不產生 Ndr 的隔離郵件因為隔離的郵件會被包裝為 Ndr。</td>
    </tr>
    </tbody>
    </table>


  - **設定 Outlook**  您需要設定以符合組織需求的 Outlook 委派存取權限。此外，我們建議您設定**訊息**檢視中顯示原始`Sender[#0x0069001E]`、 `Recipient[#0x0E04001E]`，以及`Bcc[#0x0E02001E]`欄位的 Outlook 設定檔。如需詳細資訊，請參閱[版本隔離的垃圾郵件隔離信箱的郵件](release-quarantined-messages-from-the-spam-quarantine-mailbox-exchange-2013-help.md)。

## 步驟 3： 指定垃圾郵件隔離信箱

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 [反垃圾郵件和反惡意程式的權限](anti-spam-and-anti-malware-permissions-exchange-2013-help.md)主題中的「反垃圾郵件功能」項目。

執行下列命令：

    Set-ContentFilterConfig -QuarantineMailbox <SmtpAddress>

此範例會將所有超出垃圾郵件隔離閾值的郵件傳送至 spamQ@contoso.com。

    Set-ContentFilterConfig -QuarantineMailbox spamQ@contoso.com

## 如何才能了解此步驟是否正常運作？

若要驗證您是否已成功指定垃圾郵件隔離信箱，請執行下列動作：

1.  執行下列命令：
    
        Get-ContentFilterConfig | Format-List QuarantineMailbox

2.  請確認顯示的值是您所設定的值。

## 步驟 4： 設定 SCL 隔離臨界值

SCL 隔離臨界值是在特定的郵件會被識別為潛在的垃圾郵件已傳遞至垃圾郵件隔離信箱的值。您可以設定為值的 SCL 隔離臨界值是從 0 到 9、 其中 0 會被視為較不可能是垃圾郵件和 9 會被視為很有可能是垃圾郵件。

如需如何調整 SCL 閾值以因應個別組織的需求，以及如何調整各位收件者之 SCL 閾值的相關資訊，請參閱[管理內容篩選](manage-content-filtering-exchange-2013-help.md)。

## 步驟 5： 管理垃圾郵件隔離信箱

管理垃圾郵件隔離信箱時，請遵循下列指示：

  - 使用 Outlook 的「再寄一次」功能，來釋放已傳送至垃圾隔離信箱的項目，以便重新傳送原始郵件。
    
    如需詳細資訊，請參閱 [版本隔離的垃圾郵件隔離信箱的郵件](release-quarantined-messages-from-the-spam-quarantine-mailbox-exchange-2013-help.md)。

  - 監視垃圾郵件隔離信箱，使垃圾郵件隔離信箱的大小保持在可接受的範圍。電子郵件訊息的數量可以因為收件者、 較大的郵件自然趨勢或 SCL 隔離動作的臨界值的較大組變更。

  - 監視誤報為垃圾郵件隔離信箱。如果您的垃圾郵件隔離信箱包含許多誤判，調整 SCL 隔離臨界值。如需如何判斷為何誤判會傳遞至垃圾郵件隔離信箱的詳細資訊，請參閱[反垃圾郵件戳記](anti-spam-stamps-exchange-2013-help.md)。

  - 使用相同的 Outlook 設定檔的垃圾郵件隔離信箱復原隔離的郵件。不支援將權限套用至不同的 Outlook 設定檔復原的郵件。您無法使用不同的 Outlook 設定檔來復原或釋出郵件的垃圾郵件隔離信箱。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>會刪除會被識別為垃圾郵件的 Ndr，即使其 scl 指出應隔離。Ndr 未傳遞至垃圾郵件隔離信箱。若要追蹤這類郵件、 使用代理程式記錄檔或追蹤記錄檔的郵件。如需詳細資訊，請參閱<a href="anti-spam-agent-logging-exchange-2013-help.md">反垃圾郵件代理程式記錄</a>。</td>
</tr>
</tbody>
</table>


## 步驟 6： 調整 SCL 隔離臨界值

設定 SCL 隔離臨界值之後，定期監視設定並調整其根據貴組織的需求。例如，如果將垃圾郵件隔離信箱篩選太多的誤判，引發至較大的數字的 SCL 隔離臨界值。如需如何調整 SCL 隔離臨界值的詳細資訊，請參閱[垃圾郵件信賴等級閾值](spam-confidence-level-threshold-exchange-2013-help.md)。

