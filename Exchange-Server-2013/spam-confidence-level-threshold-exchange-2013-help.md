---
title: '垃圾郵件信賴等級閾值: Exchange 2013 Help'
TOCTitle: 垃圾郵件信賴等級閾值
ms:assetid: 0009b4af-be6d-41d2-98bc-b5487272c74a
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Aa995744(v=EXCHG.150)
ms:contentKeyID: 50472437
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 垃圾郵件信賴等級閾值

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-11-17_

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在 2016 年 11 月 1，Microsoft 停止產生 Exchange 和 Outlook 中 SmartScreen 篩選器的垃圾郵件定義更新。現有的 SmartScreen 垃圾郵件定義將會保留，但其效果可能會隨著時間降低。如需詳細資訊，請參閱 <a href="https://go.microsoft.com/fwlink/p/?linkid=835894">Outlook 和 Exchange 中 SmartScreen 的取代支援</a>。</td>
</tr>
</tbody>
</table>


在 Microsoft Exchange Server 2013 中，您可以根據垃圾郵件信賴等級 (SCL) 閾值來定義特定的動作。例如，您可以定義不同閾值，來拒絕、刪除或隔離正在執行內容篩選代理程式之 Exchange 伺服器上的郵件。

內容篩選代理程式上的這個 SCL 閾值組態，以及使用者信箱上的 \[SCL 垃圾郵件\] 資料夾組態的組合，可協助您執行更全面且精確的反垃圾郵件策略。Exchange 2013 中的這個更精確且詳盡的 SCL 閾值調整功能，可幫助您減少在 Exchange 組織上部署及維護反垃圾解決方案的整體成本。

內容篩選器代理程式會在反垃圾郵件週期的後期指派 SCL 評級給郵件，亦即在其他反垃圾郵件代理程式已經處理所有的輸入郵件之後。在內容篩選器代理程式處理輸入郵件之前，就先處理它們的許多其他反垃圾郵件代理程式，在其對郵件的作用方式上具有決定性。例如，Edge Transport Server 上的連線篩選器代理程式會拒絕從即時封鎖清單上之 IP 位址所傳送的任何郵件。寄件者篩選器代理程式和收件者篩選器代理程式會以同樣的決定性方式來處理郵件。

在 Exchange 2013 中，這些決定性反垃圾郵件代理程式會先處理郵件，因而可大幅減少內容篩選器代理程式必須處理的郵件數。如需反垃圾郵件代理程式處理郵件之順序的相關資訊，請參閱[反垃圾郵件保護](anti-spam-protection-exchange-2013-help.md)。

因為內容篩選不是確切且具決定性的程序，所以調整內容篩選器代理程式對不同 SCL 值執行之動作的能力很重要。請謹慎地調整 SCL 閾值組態，您可以將下列各項最小化：

  - 垃圾郵件隔離儲存區的大小

  - 遭錯誤隔離的合法電子郵件數

  - 合法電子郵件抵達 Microsoft Outlook 使用者垃圾郵件資料夾的件數

  - 抵達Outlook 使用者之 \[收件匣\] 或 \[垃圾郵件\] 資料夾的討厭垃圾電子郵件數

  - 抵達 Outlook 使用者之 \[收件匣\] 的垃圾電子郵件數

## SCL 閾值動作

藉由調整 SCL 閾值動作，您可以提升對於很有可能成為垃圾郵件之郵件採取的內容篩選動作。若要了解這個功能，先了解不同的 SCL 閾值動作及其執行方式會很有幫助。

  - **SCL 刪除閾值**   當特定郵件的 SCL 值等於或大於 SCL 刪除閾值時，內容篩選器代理程式會刪除該郵件。沒有通訊協定層級的通訊，可告知傳送系統或寄件者該郵件已遭刪除。如果郵件的 SCL 值低於 SCL 刪除閾值，則內容篩選器代理程式不會刪除郵件。相反地，內容篩選器代理程式會比較 SCL 值與 SCL 拒絕閾值。

  - **SCL 拒絕閾值**   當特定郵件的 SCL 值等於或大於 SCL 拒絕閾值時，內容篩選器代理程式會刪除該郵件，並傳送拒絕回應給傳送系統。您可以自訂拒絕回應。在某些情況下，未傳遞回報 (NDR) 會傳送給郵件的原始寄件者。如果郵件的 SCL 值低於 SCL 刪除和 SCL 拒絕閾值，則內容篩選器代理程式不會刪除或拒絕郵件。相反地，內容篩選器代理程式會比較 SCL 值與 SCL 隔離閾值。

  - **SCL 隔離閾值**   當特定郵件的 SCL 值等於或大於 SCL 隔離閾值時，內容篩選器代理程式會將該郵件傳送至隔離信箱。電子郵件管理員必須定期檢閱隔離信箱。如果郵件的 SCL 值低於 SCL 刪除、拒絕和隔離閾值，則內容篩選器代理程式不會刪除、拒絕或隔離郵件。相反地，內容篩選器代理程式會將郵件傳送至適當的信箱伺服器，並評估郵件之每位收件者 \[SCL 垃圾郵件\] 資料夾閾值。

  - **SCL 垃圾郵件資料夾閾值**   若特定郵件的 SCL 值超出 SCL 垃圾郵件資料夾閾值，郵件將傳遞至使用者的垃圾郵件資料夾。如果郵件的 SCL 值低於 SCL 刪除、拒絕、隔離和垃圾郵件資料夾閾值，郵件會傳遞至使用者的 \[收件匣\] 內。

內容篩選器代理程式和垃圾郵件資料夾會以不同的方式處理 SCL 閾值。內容篩選器代理程式會在達到您設定的 SCL 閾值時採取動作。垃圾郵件資料夾則會在達到您設定的 SCL 閾值加 1 時採取動作。例如，如果您將內容篩選器代理程式上的刪除動作設為 SCL 值 8，所有 SCL 為 8 或更高值的郵件都會遭到刪除。不過，如果您設定 SCL 閥值為 4 的垃圾郵件資料夾，則所有 SCL 為 5 或更高值的郵件都會被移到垃圾郵件資料夾。

例如，若您將 SCL 刪除閾值設為 8、將 SCL 拒絕閾值設為 7、將 SCL 隔離閾值設為 6，並將 SCL 垃圾電子郵件資料夾閾值設為 4，則 SCL 5 以下的所有郵件都將傳送至使用者的信箱。SCL 值為 5 的郵件將置於使用者的垃圾郵件資料夾中。SCL 值為 4 的郵件將置於使用者的垃圾郵件 \[收件匣\] 中。

您可以於下列地點設定 SCL 刪除、拒絕、隔離以及垃圾郵件資料夾設定：

  - **內容篩選代理程式設定 (依傳輸伺服器 SCL 設定)**   您使用 **Set-ContentFilterConfig** 指令程式於執行內容篩選代理程式的 Exchange 伺服器上啟用或停用並設定 SCL 刪除、拒絕與隔離閾值。假以時日，當您分析垃圾郵件功能，以及由反垃圾郵件記錄和報告功能所提供的估計值時，可以依需要對這些 SCL 閾值組態進行其他調整。
    
    **Set-ContentFilterConfig** 指令上可用的 SCL 參數說明於下表中：
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>參數</th>
    <th>描述</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><em>SCLDeleteEnabled</em></p></td>
    <td><p>當郵件的 SCL 值大於或等於由 <em>SCLDeleteThreshold</em> 參數指定的值時，參數在啟用或停用刪除郵件不使用未傳遞回報 (NDR) 。這個參數的有效輸入是 <code>$true</code> 或 <code>$false</code>。</p></td>
    </tr>
    <tr class="even">
    <td><p><em>SCLDeleteThreshold</em></p></td>
    <td><p>此參數的有效輸入是 0 到 9 的整數。此參數的值須大於其他 SCL 閾值參數。僅有當 <em>SCLDeleteEnabled</em> 參數的值為 <code>$true</code> 時，此參數才有意義。</p></td>
    </tr>
    <tr class="odd">
    <td><p><em>SCLRejectEnabled</em></p></td>
    <td><p>當郵件的 SCL 值大於或等於由 <em>SCLRejectThreshold</em> 參數指定的值時，參數在啟用或停用拒絕郵件不使用 NDR。這個參數的有效輸入是 <code>$true</code> 或 <code>$false</code>。</p></td>
    </tr>
    <tr class="even">
    <td><p><em>SCLRejectThreshold</em></p></td>
    <td><p>此參數的有效輸入是 0 到 9 的整數。此參數的值須小於 <em>SCLDeleteThreshold</em> 參數，但是大於其他 SCL 閾值參數。此參數僅在 <em>SCLRejectEnabled</em> 參數的值為 <code>$true</code> 時有意義。</p></td>
    </tr>
    <tr class="odd">
    <td><p><em>SCLQuarantineEnabled</em></p></td>
    <td><p>當郵件的 SCL 值大於或等於由 <em>SCLQuarantineThreshold</em> 參數指定的值時，參數在啟用或停用傳送郵件至垃圾隔離信箱時不使用 NDR。這個參數的有效輸入是 <code>$true</code> 或 <code>$false</code>。</p>
    <p>如需垃圾郵件隔離信箱的詳細資訊，請參閱<a href="spam-quarantine-exchange-2013-help.md">垃圾郵件隔離</a>。</p></td>
    </tr>
    <tr class="even">
    <td><p><em>SCLQuarantineThreshold</em></p></td>
    <td><p>此參數的有效輸入是 0 到 9 的整數。此參數的值應小於 <em>SCLRejectThreshold</em> 參數，但是大於 <strong>Set-OrganizationConfig</strong> 或 <strong>Set-Mailbox</strong> 指令程式上的 <em>SCLJunkThreshold</em> 參數。僅有當 <em>SCLQuarantineThreshold</em> 參數的值為 <code>$true</code> 時，此參數才有意義。</p></td>
    </tr>
    </tbody>
    </table>


  - **在組織組態設定上 (全組織的 SCL 設定)**   您使用 **Set-OrganizationConfig** 指令程式來設定所有組織中信箱的 SCL 垃圾郵件資料夾閾值。
    
    **Set-OrganizationConfig** 指令上可用的 SCL 參數說明於下表中：如需使用 SCLJunkThreshold 的範例，請參閱[在信箱上設定反垃圾郵件設定](configure-anti-spam-settings-on-mailboxes-exchange-2013-help.md)。
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>參數</th>
    <th>描述</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><em>SCLJunkThreshold</em></p></td>
    <td><p>此參數指定移動至收件者信箱中垃圾郵件資料夾的郵件 SCL 值需大於郵件。此參數的有效輸入是 0 到 9 的整數。此參數的值須小於其他 SCL 閾值參數。例如，若您指定值 4，則閾值為 5 或更高的 SCL 值郵件將移動至垃圾郵件資料夾。</p></td>
    </tr>
    </tbody>
    </table>


  - **在使用者信箱上 (每位收件者 SCL 組態)**   您使用 **Set-Mailbox** 指令程式，對個別信箱設定每位收件者啟用或停用 SCL 刪除、拒絕和垃圾郵件閾值。您僅可使用 **Set-Mailbox** 指令程式來啟用或停用個別信箱的 SCL 垃圾郵件資料夾閾值。每位收件者 SCL 刪除、拒絕和隔離閾值是儲存於 Active Directory 中，並由 Microsoft Exchange EdgeSync 服務複寫到訂閱的 Edge Transport Server。即使您已設定每部傳輸伺服器 SCL 組態，內容篩選器代理程式仍會使用每位收件者 SCL 閾值組態。因此，如果您已設定每位收件者 SCL 閾值，內容篩選器代理程式將對特定使用者使用每位收件者 SCL 閾值，而不是內容篩選器代理程式上的 SCL 組態。例如，請參閱[在信箱上設定反垃圾郵件設定](configure-anti-spam-settings-on-mailboxes-exchange-2013-help.md)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>對於透過通訊群組收到的郵件，並不會強制執行每個收件者 SCL 閾值。</td>
    </tr>
    </tbody>
    </table>
    
    **Set-Mailbox** 指令程式可用的的參數與 **Set-ContentFilterConfig** 及 **Set-OrganizationConfig** 指令程式上可用的參數相同：
    
      - *SCLDeleteEnabled*
    
      - *SCLDeleteThreshold*
    
      - *SCLRejectEnabled*
    
      - *SCLRejectThreshold*
    
      - *SCLQuarantineEnabled*
    
      - *SCLQuarantineThreshold*
    
      - *SCLJunkThreshold*
    
    但是，所有在 **Set-Mailbox** 指令程式上的 SCL 參數也會接受值 `$null`。如果信箱上的 SCL 設定為空白 (`$null`)，相對的內容篩選代理程式設定或組織組態設定將套用至信箱。若信箱上的 SCL 設定擁有 `$true` 或 `$false` 值，則信箱上的設定會覆寫內容篩選代理程式或組織組態中相對的全組織設定。
    
    僅於 **Set-Mailbox** 指令上可用的 SCL 參數說明於下表中：
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>參數</th>
    <th>描述</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><em>SCLJunkEnabled</em></p></td>
    <td><p>當郵件的 SCL 值大於或等於由 <em>SCLQuarantineThreshold</em> 參數指定的值時，參數在啟用或停用傳遞郵件至使用者垃圾郵件資料夾時不使用 NDR。這個參數的有效輸入是 <code>$true</code>、<code>$false</code>、或 <code>$null</code>。</p>
    <p>請注意，垃圾郵件篩選將預設為所有組織中的使用者信箱啟用。依預設，<em>Enabled</em> 參數在所有使用者信箱的 <strong>Set-MailboxJunkEmailConfiguration</strong> 指令程式將設為值 <code>$true</code>。</p></td>
    </tr>
    </tbody>
    </table>
    
    如需為信箱設定 SCL 閾值的相關資訊，請參閱[在信箱上設定反垃圾郵件設定](configure-anti-spam-settings-on-mailboxes-exchange-2013-help.md)。

## 監控 SCL 閾值

您可以使用 `%ExchangeInstallPath%Scripts` 資料夾中的數個內建指令碼 (例如**get-AntispamSCLHistogram.ps1**) 來收集篩選結果資料。如果資料指出您必須進行立即調整，請重新設定 SCL 閾值。否則，請收集資料並分析垃圾郵件報告，以判斷是否需要調整。

