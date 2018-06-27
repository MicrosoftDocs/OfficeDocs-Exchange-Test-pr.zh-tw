---
title: '保護語音信箱: Exchange 2013 Help'
TOCTitle: 保護語音信箱
ms:assetid: a88d41d5-2e70-4193-bcd3-dec50dff412b
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd351041(v=EXCHG.150)
ms:contentKeyID: 52062371
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 保護語音信箱

 

_**適用版本：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上次修改主題的時間：**2016-12-09_

部分舊型專用交換機 (PBX) 和 IP PBX 電話語音系統可讓來電者將語音信箱訊息標示為私人，以防止訊息的預定收件者轉寄給其他人。 在整合的語音信箱系統中，有許多方式可以存取語音訊息，因此更難以防止將已標示為私人的語音訊息洩露給非預定的接聽者。

整合通訊 (UM) 可以設定為使用 Active Directory Rights Management Services (AD RMS) 來保護組織的語音訊息。 此功能稱為「受保護的語音信箱」。

當語音訊息受到保護時，收件者不僅無法轉寄訊息，UM 也會確保只有訊息的一或多個預定收件者才能存取訊息的內容。 使用 MicrosoftOutlook 2010 或更新版本、Outlook Web App 或 Outlook 語音存取，可以存取受保護的語音訊息。

**目錄**

Overview of Protected Voice Mail

Overview of Active Directory Rights Management Services

Client support and end-user features

Protected voice mail structure

Composing a Protected Voice Mail message

UM mailbox policies

Text message notifications and Protected Voice Mail

## 受保護的語音信箱的概觀

使用Exchange 2010及更新版本的整合通訊 (UM) 的受保護的語音信箱功能。它可以在 UM 信箱原則，設定與所有受保護的語音信箱設定可使用 Exchange 管理主控台或命令介面中Exchange 2010或Exchange 2013在命令介面中使用Exchange系統管理中心 (EAC) 或 cmdlet 來設定。

將資訊版權管理 (IRM) 套用至語音訊息可以實作「受保護的語音信箱」。 當語音訊息受到 UM 保護時：

  - 使用者可以回覆受保護的語音訊息。

  - 收件者無法轉寄語音訊息。

  - 使用者無法儲存語音訊息的副本。

  - 使用者無法儲存或複製語音訊息的附加音訊。

  - 只有預定的一或多個收件者才能開啟語音訊息。

UM 可以保護自動答錄語音訊息和人際語音訊息 (使用 Outlook 語音存取傳送給使用者的語音訊息)。 但是，保護不會套用至下列類型的訊息：

  - 傳真訊息。

  - 無語音訊息。 例如，電子郵件訊息或會議邀請，即使是使用 Outlook 語音存取 (語音回覆) 建立也一樣。

回到頁首

## Active Directory Rights Management Services 的概觀

AD RMS (Windows Server 2008 和更新版本的元件) 可用來協助保護檔案，只有寄件者預定的收件者才能檢視檔案。 AD RMS 會指定使用者存取檔案必須具有的權限，以保護檔案。 權限可以設定為允許使用者開啟、修改、列印、轉寄或對權限管理的資訊採取其他動作。 透過 AD RMS，您可以保護散佈到網路外的資料。

AD RMS 系統具有伺服器和用戶端元件，包括：

  - 安裝有 Windows Server 2008 R2 或更新版本的伺服器，執行 Active Directory Rights Management Services server role，負責處理憑證和授權。

  - 資料庫伺服器。

  - AD RMS 用戶端。 Windows 7 和 Windows 8 作業系統包含最新版本的 AD RMS 用戶端。

伺服器元件由 Microsoft 伺服器上執行的數項 Web 服務組成，例如 Windows Server 2008 或更新版本。 用戶端元件可以在用戶端或伺服器作業系統上執行，包含的功能可讓應用程式加密和解密內容、擷取範本和撤銷清單，以及從伺服器取得授權和憑證。

使用 AD RMS 及 AD RMS 用戶端，您可增強組織的安全性策略來保護使用資訊，無論移出透過保持的持續性的使用狀況原則資訊。您可以使用 AD RMS 避免敏感資訊 — 例如財務報告、 產品規格、 客戶資料和機密的電子郵件和語音信箱訊息 — 從有意或無意快速錯誤送到。如需詳細資訊，請參閱[AD RMS 概觀 （英文)](https://go.microsoft.com/fwlink/p/?linkid=199436)。

您可以在 Exchange UM 中使用資訊版權管理 (IRM) 功能，對郵件和附件套用持續性的保護。

組織和使用者可以使用 IRM 功能和「受保護的語音信箱」，以控制收件者存取電子郵件和語音信箱訊息所需的權限。 IRM 也可以用來限制收件者動作，例如將訊息轉寄給其他收件者、列印訊息或附件，或經由複製和貼上來擷取訊息或附件內容。

## IRM 需求

您可以在 Exchange 中實作 IRM 之前，您必須先部署並設定 AD RMS 基礎結構。如需詳細資訊，請參閱[Active Directory Rights Management Services](https://go.microsoft.com/fwlink/p/?linkid=199439)。若要實作 IRM 以支援您的 Exchange 組織中的受保護的語音信箱，您的部署必須符合下列需求。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>伺服器</th>
<th>需求</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AD RMS 叢集</p></td>
<td><ul>
<li><p>Windows Server 2008 R2 Standard 或 Enterprise SP1 或 Windows Server 2012 Standard 或 Datacenter。如需系統需求的詳細資訊，請參閱<a href="exchange-2013-system-requirements-exchange-2013-help.md">Exchange 2013 系統需求</a>。</p></li>
<li><p><strong>服務連線點 (SCP)</strong>   Exchange 2013 和 AD RMS 感知應用程式使用 Active Directory 中登錄的 SCP 來探索 AD RMS 叢集和 URL。 AD RMS 可讓您在 AD RMS 安裝內登錄 SCP。 如果用於安裝 AD RMS 的帳戶不是 Enterprise Admins 安全性群組的成員，則 SCP 登錄可在安裝之後執行。 在 Active Directory 樹系中，AD RMS 只有一個 SCP。</p></li>
<li><p><strong>權限</strong>   必須指派 AD RMS 伺服器憑證管線的讀取和執行權限給 Exchange 伺服器群組中的伺服器，或個別 Exchange 伺服器。 AD RMS 伺服器上的預設路徑是 \inetpub\wwwroot\_wmcs\certification\ServerCertification.asmx。</p></li>
<li><p><strong>AD RMS 進階使用者</strong>   若要啟用傳輸解密、日誌報告解密、Outlook Web App 中的 IRM，以及 Exchange 搜尋的 IRM，您必須將 [同盟傳遞信箱] (由 Exchange 安裝建立的系統信箱) 新增至 AD RMS 叢集的 AD RMS 進階使用者群組。 如需詳細資訊，請參閱<a href="add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md">至 AD RMS 超級使用者群組新增同盟信箱</a>。</p></li>
</ul></td>
</tr>
</tbody>
</table>


## 設定和測試 IRM

您必須使用命令介面來設定 IRM 功能。若要設定個別的 IRM 功能、 使用[Set-IRMConfiguration](https://technet.microsoft.com/zh-tw/library/dd979792\(v=exchg.150\))指令程式。如需關於如何設定 IRM 功能會查看[資訊版權管理程序](information-rights-management-procedures-exchange-2013-help.md)。

在設定 Exchange 伺服器之後，您可以使用 [Test-IRMConfiguration](https://technet.microsoft.com/zh-tw/library/dd979798\(v=exchg.150\)) 指令程式來執行 IRM 部署的端對端測試。 此指令程式會驗證組織的 IRM 組態，應該在啟用「受保護的語音信箱」之前執行。 **Test-IRMConfiguration** 指令程式會執行下列測試：

  - 檢查 Exchange 組織的 IRM 的組態。

  - 檢查 AD RMS 伺服器的版本與 Hotfix 資訊。

  - 透過擷取權限帳戶憑證和用戶端授權人憑證 (CLC)，驗證是否能啟動 RMS 的 Exchange 伺服器。

  - 從 AD RMS 伺服器取得 AD RMS 權限原則範本。

  - 確定指定的寄件者可以傳送受 IRM 保護的訊息。

  - 為指定的收件者擷取超級使用者使用授權。

  - 為指定的收件者取得預先授權。

回到頁首

## 用戶端支援和使用者功能

用來聽取「受保護的語音信箱」訊息的電子郵件用戶端軟體必須支援 IRM，也必須知道如何讀取 UM 保護的語音訊息。 支援的電子郵件用戶端包括 MicrosoftOutlook 2010 或更新版本、Outlook Web App 和 Outlook 語音存取。 下表包含電子郵件用戶端的清單，以及支援與否。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>電子郵件用戶端</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook</p></td>
<td><ul>
<li><p>Outlook 2010 和更新版本支援受保護的語音訊息。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Outlook Web App</p></td>
<td><ul>
<li><p>Outlook Web App Exchange 2010或更新版本支援受保護的語音信箱訊息。舊版的Outlook Web App，又稱為Outlook Web Access，不支援它們。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Outlook 語音存取</p></td>
<td><ul>
<li><p>Outlook Exchange 2010和更新版本中的語音存取支援受保護的語音信箱。Outlook語音存取隨附Exchange 2007不支援受保護的語音信箱。</p></li>
<li><p>使用者信箱必須位於Exchange 2010或更新版本中信箱伺服器。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Windows Mobile 或 Windows Phone</p></td>
<td><ul>
<li><p>Windows Mobile 不支援「受保護的語音信箱」。 不過，Windows Phone 7 和 Windows Phone 8 支援「受保護的語音信箱」。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Exchange ActiveSync</p></td>
<td><ul>
<li><p>Exchange 2010 SP1 和更新版本支援「受保護的語音信箱」。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>其他電子郵件用戶端</p></td>
<td><ul>
<li><p>不支援「受保護的語音信箱」。</p></li>
</ul></td>
</tr>
</tbody>
</table>


回到頁首

## 受保護的語音訊息結構

每個「受保護的語音信箱」訊息實際上包含兩個訊息。 第一個訊息是未加密的外部訊息。 它包含名為 message.rpmsg 的附件。此附件包含 IRM 保護的語音訊息和內容權限管理控制資料。 權限管理控制資料包含內容金鑰和權限資訊，權限資訊指定誰可以存取語音訊息和這些使用者如何才能存取訊息。

受保護的語音訊息會出現在使用者 \[收件匣\] 的 \[語音信箱\] 搜尋資料夾中。 使用者可以使用內嵌音訊播放程式來聽取語音訊息，如同聽取一般語音訊息，差別在於 \[轉寄\] 按鈕會停用，且訊息上方會出現附註，指出訊息受到保護，因而無法轉寄。

在不支援「受保護的語音信箱」的電子郵件用戶端，則會顯示外部訊息的內文。 用戶端軟體不支援「受保護的語音信箱」時，系統管理員可以使用 UM 信箱原則來加入文字。 您可以設定 UM 信箱原則，以自訂電子郵件訊息包含的預設文字。 例如，您可以使用自訂文字來設定 UM 信箱原則，例如 *\[您無法開啟此語音信箱訊息，因為它受到保護。 若要檢視或聽取此語音訊息，請登入信箱 https://mail.contoso.com，或撥 +1 (425) 555-1234 來撥入 Outlook Voice Access\]*。

回到頁首

## 製作受保護的語音信箱訊息

有兩種情況可以建立受保護的語音訊息：

  - **自動答錄服務**   當來電者撥給已啟用 UM 的使用者時，就執行自動答錄服務，但使用者無法接聽電話或直接轉寄至語音信箱。 在自動答錄服務案例中，當來電者錄製語音訊息之後，語音信箱系統會播放一連串語音提示。
    
    接著，來電者可以選擇其他訊息選項，包括按井字鍵 (\#) 將語音訊息標示為私人。 如果來電者按下 \# 字鍵，他們可以遵循 UM 提供的指示，將訊息標示為私人、從私人語音訊息中移除私人標記，或以 \[高\] 重要性來標示語音訊息。 下圖顯示來電者留下私人語音訊息給使用者時可用的功能表選項。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>以自動答錄服務來電而言，UM 會使用訊息的預定收件者在 UM 信箱原則上的「受保護的語音信箱」設定，因為來電者未經過驗證。</td>
    </tr>
    </tbody>
    </table>
    
    **使用自動答錄服務建立受保護的語音信箱訊息**
    
    ![使用自動答錄服務建立受保護的語音信箱](images/Dd351041.4e9f50bf-5066-4d0a-b3eb-0515a2fc4560(EXCHG.150).jpg "使用自動答錄服務建立受保護的語音信箱")  

  - **Outlook 語音存取**   Outlook 語音存取可讓已啟用 UM 的使用者使用類比、數位或行動電話來撥打 Outlook 語音存取號碼，以存取他們的信箱。 已啟用 UM 的使用者有兩個 \[整合通訊\] 使用者介面可用： 電話使用者介面 (TUI) 及語音使用者介面 (VUI)。
    
    Outlook Voice Access 使用者可以在目錄中搜尋連絡人並傳送語音息給他們。 如果已啟用 UM 的收件者已啟用「受保護的語音信箱」，來電者可以在錄製訊息之後將訊息標示為私人。 另外，系統管理員也可以設定 UM 信箱原則，以確保 UM 可以保護已驗證的使用者傳送的所有語音訊息。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果來電者經過驗證，則套用連結至來電者的 UM 信箱原則上的「受保護的語音信箱」設定，而不論語音訊息的預定收件者的 UM 信箱原則設定。</td>
    </tr>
    </tbody>
    </table>
    
    **使用語音使用者介面建立受保護的語音信箱訊息**
    
    ![使用語音介面建立受保護的語音信箱](images/Dd351041.6b425ee4-5171-4a63-961f-bdbc6c79e1be(EXCHG.150).jpg "使用語音介面建立受保護的語音信箱")  
    
    **使用電話使用者介面建立受保護的語音信箱訊息**
    
    ![使用按鍵式輸入建立受保護的語音信箱](images/Dd351041.dd58fd38-c4c3-437c-adc1-497deb3c8a9f(EXCHG.150).jpg "使用按鍵式輸入建立受保護的語音信箱")  

回到頁首

## UM 信箱原則

您可以建立整合通訊信箱原則套用至一組已啟用 UM 之信箱的一組通用 PIN 原則設定、 撥號限制及受保護的語音信箱設定等的 UM 原則設定。若要深入了解 UM 信箱原則，請參閱[管理 UM 信箱原則](manage-a-um-mailbox-policy-exchange-2013-help.md)。

您可以使用 EAC 或命令介面中的 **Set-UMMailboxPolicy** 指令程式來設定「受保護的語音信箱」選項。 下表列出「受保護的語音信箱」可設定的設定。

**受保護的語音信箱設定**


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>命令介面參數</th>
<th>EAC 中有可用的設定嗎？</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ProtectAuthenticatedVoiceMail</em></p></td>
<td><p>是</p></td>
<td><p><em>ProtectAuthenticatedVoiceMail</em>參數指定已啟用 UM 的使用者使用 Outlook Voice Access 存取信箱時，是否可以傳送受保護的語音信箱訊息。 預設值是 <code>None</code>。 這表示在製作語音訊息時不套用保護，且來電者也沒有選項可將語音訊息標示為 [私人]。 如果值設為 <code>Private</code>，則只會保護來電者已標示為 [私人] 的訊息。 如果值設為 <code>All</code>，則會保護每一個語音訊息，無論來電者選擇的選項為何。</p></td>
</tr>
<tr class="even">
<td><p><em>ProtectUnauthenticatedVoiceMail</em></p></td>
<td><p>是</p></td>
<td><p><em>ProtectUnauthenticatedVoiceMail</em> 參數指定 Mailbox Server 在代替與 UM 信箱原則關聯的已啟用 UM 的使用者接聽電話時，是否建立受保護的語音訊息。 當訊息從 UM 自動語音應答傳送至已啟用 UM 的使用者時，也套用此設定。 預設值是 <code>None</code>。 這表示語音訊息不套用保護，且不提供選項給來電者將訊息標示為 [私人]。 如果值設為 <code>Private</code>，則只會保護來電者已標示為 [私人] 的訊息。 如果值設為 <code>All</code>，則會保護每一個語音訊息，而不論來電者是否已將訊息標示為私人。</p></td>
</tr>
<tr class="odd">
<td><p><em>ProtectedVoiceMailText</em></p></td>
<td><p>是</p></td>
<td><p><em>ProtectedVoiceMailText</em> 參數指定「受保護的語音信箱」訊息的外部訊息內文中要包含的文字。 所有不支援「受保護的語音信箱」訊息的電子郵件用戶端應用程式中會顯示此文字。 請注意，當此內容設為 <code>Null</code> 或空白時，UM 一律會提供預設訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>RequireProtectedPlayOnPhone</em></p></td>
<td><p>是</p></td>
<td><p><em>RequireProtectedPlayOnPhone</em> 參數指定是否強制與 UM 信箱原則關聯的使用者在電話上聽取受保護的語音訊息 (使用 [在電話上播放])。 預設值是 <code>$false.</code>。當值設為 <code>$true</code> 時，在 Outlook 或 Outlook Web App 中的「受保護的語音信箱」表單上，音訊媒體播放程式會顯示為停用。 請注意，永遠可存取語音訊息的預覽文字。 使用者無法使用任何媒體播放軟體來播放音訊檔，也無法使用內嵌媒體播放程式來傾聽語音訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowVoiceResponseToOtherMessageTypes</em></p></td>
<td><p>是</p></td>
<td><p><em>AllowVoiceResponseToOtherMessageTypes</em> 參數指定通過 Outlook 語音存取驗證來存取電子郵件的來電者，是否能夠製作語音回覆給電子郵件和會議邀請。</p></td>
</tr>
</tbody>
</table>


如需有關如何管理「受保護的語音信箱」設定的相關資訊，請參閱[受保護的語音信箱程序](protected-voice-mail-procedures-exchange-2013-help.md)或 [Set-UMMailboxPolicy](https://technet.microsoft.com/zh-tw/library/bb124903\(v=exchg.150\))。

回到頁首

## 簡訊通知和受保護的語音信箱

設定 UM 帳戶來傳送簡訊通知 (也稱為 SMS 通知) 至行動電話的使用者在收到語音訊息時，也會在簡訊內文中收到音訊轉譯 (語音信箱預覽) 文字。 不過，以受保護的語音訊息而言，這代表安全性問題，因為語音訊息的內容應該一律受到保護。

當 UM 建立受保護語音訊息的簡訊通知時，它會檢查語音訊息是否標示為 \[私人\]。 如果是的話，則不會在傳送至行動電話的簡訊中加入轉譯的音訊文字。 反而會在簡訊中包含下列文字： \[使用 Outlook 語音存取來存取這則受保護的語音信箱訊息。\]

回到頁首

