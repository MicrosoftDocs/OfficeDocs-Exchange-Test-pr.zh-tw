---
title: '設定郵件流程和用戶端存取: Exchange 2013 Help'
TOCTitle: 設定郵件流程和用戶端存取
ms:assetid: 4acc7f2a-93ce-468c-9ace-d5f7eecbd8d4
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ218640(v=EXCHG.150)
ms:contentKeyID: 50473184
ms.date: 01/04/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 設定郵件流程和用戶端存取

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

Exchange Server 2013 郵件流程與用戶端存取的安裝後期工作，包括如何設定 SSL 憑證。

您在組織中安裝 Microsoft Exchange Server 2013 之後，需要為郵件流程及用戶端存取設定 Exchange Server 2013。少了這些步驟的話，您將無法寄送郵件至網際網路，至於外部用戶端，例如 Microsoft Office Outlook 及 Exchange ActiveSync 裝置，將無法連結到您的 Exchange 組織。

本主題中的步驟會設定一個基本部署，包含單一的 Active Directory 站台以及簡易郵件傳輸通訊協定 (SMTP) 命名空間。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>本主題使用如 Ex2013CAS、contoso.com、mail.contoso.com 及 172.16.10.11 等範例值。請將範例值取代為組織中的伺服器名稱、FQDN 及 IP 位址。</td>
</tr>
</tbody>
</table>


如需郵件流程及用戶端和裝置等相關管理工作的資訊，請參閱＜[郵件流程](mail-flow-exchange-2013-help.md)＞和＜[用戶端和行動裝置](clients-and-mobile-exchange-2013-help.md)＞。

## 開始之前有哪些須知？

  - 完成此工作的預估時間：50 分鐘

  - 本主題中的程序需要特定權限。請查看每個程序以取得權限資訊。

  - 除非在 Client Access Server 上設定安全通訊端層 (SSL) 憑證，否則當您連線到 Exchange 系統管理中心 (EAC) 網站時將會收到憑證警告。本主題稍後將指示您如何操作這部份。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>每個組織的 Active Directory 樹系中至少都要有一部 Client Access Server 與一部 Mailbox Server。此外，每個含有 Mailbox Server 的 Active Directory 網站也至少要包含一部 Client Access Server。如果您要分離您的伺服器角色，建議您先安裝 Mailbox server role。</td>
</tr>
</tbody>
</table>


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

## 步驟 1：建立傳送連接器

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱[郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「傳送連接器」項目。

傳輸郵件至網際網路之前，您需要在郵件伺服器建立一個傳送連接器。請執行下列動作。

1.  瀏覽至用戶端存取伺服器的 URL 以開啟 EAC。例如，https://Ex2013CAS/ECP。

2.  在 \[網域\\使用者名稱\] 和 \[密碼\] 中輸入您的使用者名稱和密碼，然後按一下 \[登入\]。

3.  到 \[郵件流程\] \>\[傳送連接器\]。在 \[傳送連接器\] 頁面上，按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

4.  在 \[新傳送連接器\] 精靈中，為傳送連接器指定一個名稱，然後選取 \[網際網路\]。 按 \[下一步\]。

5.  請驗證 \[與收件者網域的MX記錄相關\] 已選取。按 \[下一步\]。

6.  在 \[位址空間\] 底下按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。在 \[新增網域\] 視窗中，確定 \[類型\] 欄位中已選取 \[SMTP\]。在 \[完整網域名稱 (FQDN)\] 欄位中，輸入 **\***。按一下 \[儲存\]。

7.  請確定 \[範圍傳送連接器\] 未選取，然後按 \[下一步\]。

8.  在 \[來源伺服器\] 之下，按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。在 \[選取伺服器\] 視窗中，選取一部信箱伺服器。選取伺服器後，按一下 \[新增\]，接著按一下 \[確定\]。

9.  按一下 **\[完成\]**。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Exchange 2013 安裝完畢時，將會建立一個預設的內部接收連接器。此接收連接器接受來自外部伺服器的匿名 SMTP 連接。假如這是您想要的功能，您便無需進行任何額外的設定。假如您想限制外部伺服器進行內部連結，請至用戶端存取伺服器上的 [預設前端 &lt;用戶端存取伺服器&gt;] 接收連接器進行調整。</td>
</tr>
</tbody>
</table>


## 如何才能了解此步驟是否正常運作？

若要確認您是否已成功啟用或停用寄件者識別碼，請執行下列動作：

1.  在 EAC 中，驗證在 \[郵件流程\] \> \[傳送連接器\] 中出現的新傳送連接器。

2.  開啟 Outlook Web App 並傳送一封郵件給外部收件者。如果收件者收到郵件，表示您已經成功設定了傳送連接器。

## 步驟 2：新增公認的網域

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱[郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「公認的網域」項目。

經由預設，當您在 Active Directory 樹系部署新的 Exchange 2013 組織，Exchange 會使用執行設定/預備 AD之Active Directory 網域的網域名稱。假如您想要透過另一個網域來傳送或接收訊息，您必須將該網域新增為公認的網域。在下一個步驟中，依照預設電子郵件位址原則，此網域也將新增為主要的 SMTP 地址。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您要從網際網路接受電子郵件的每一個 SMTP 網域，都需要有公用網域名稱系統 (DNS) MX 資源記錄。每一個 MX 記錄應解析收取您組織之電子郵件的網際網路對向伺服器。</td>
</tr>
</tbody>
</table>


1.  瀏覽至用戶端存取伺服器的 URL 以開啟 EAC。例如，https://Ex2013CAS/ECP。

2.  在 \[網域\\使用者名稱\] 和 \[密碼\] 中輸入您的使用者名稱和密碼，然後按一下 \[登入\]。

3.  前往 \[郵件流程\] \>\[公認的網域\]。在 \[公認的網域\] 頁面上，按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

4.  在 \[新增公認的網域\] 精靈中，為該網域指定名稱。

5.  在 \[公認的網域\] 欄位中，指定你想新增的 SMTP 收信者網域。例如：contoso.com。

6.  選擇 \[授權網域\]，然後按一下 \[儲存\]。

## 如何才能了解此步驟是否正常運作？

若要確認您是否已成功建立一個公認的網域，請執行下列動作：

  - 在 EAC 中，驗證在 \[郵件流程\] \> \[公認的網域\] 中驗證新增之公認的網域。

## 步驟 3：設定預設電子郵件地址原則

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱[電子信箱地址與通訊錄權限](email-address-and-address-book-permissions-exchange-2013-help.md) 項目中的「電子郵件地址原則」項目。

如果您在上一個步驟新增了一個公認的網域，而您希望該網域能新增到組織中的每位收件者，您必須更新預設電子郵件地址原則。

1.  瀏覽至用戶端存取伺服器的 URL 以開啟 EAC。例如，https://Ex2013CAS/ECP。

2.  在 \[網域\\使用者名稱\] 和 \[密碼\] 中輸入您的使用者名稱和密碼，然後按一下 \[登入\]。

3.  到 \[郵件流程\] \> \[電子郵件地址原則\]。在 \[電子郵件地址原則\] 頁面，選取 \[預設原則\]，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

4.  在 \[預設電子郵件地址原則\] 頁面，按一下 \[電子郵件地址格式\]。

5.  在 \[電子郵件地址格式\] 之下，點按一下您想要改變的 SMTP 地址，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

6.  在 \[電子郵件地址格式\] 頁面之 \[電子郵件地址參數\] 欄位中，指定您想套用在 Exchange 組織中所有收件人的 SMTP 收件人網域。此網域必須符合您在上一步驟新增之公認的網域。例如：@contoso.com。按一下 \[儲存\]。

7.  按一下 \[儲存\]。

8.  在 \[預設原則\] 資料窗格中，按一下 \[套用\]。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>我們建議您設定一個使用者主要名稱 (UPN)，符合每一位使用者的主要電子郵件地址。如果您未提供符合一位使用者的電子郵件地址之 UPN，使用者除了電子郵件地址之外，將被要求以手動方式，提供他們的網域/使用者名稱或者 UPN。如果他們的 UPN 與他們的電子郵件地址相符，Outlook Web App，ActiveSync，以及 Outlook 將會自動搭配他們的電子郵件地址和他們的 UPN。</td>
</tr>
</tbody>
</table>


## 如何才能了解此步驟是否正常運作？

若要確認您是否已成功設定預設電子郵件地址原則，請執行下列動作：

1.  在 EAC 中，前往 \[收件者\]\>\[信箱\]。

2.  選取一個信箱，然後在收件者資料窗格中，驗證 \[使用者信箱\] 欄位已設定為 *\<alias\>*＠*\<new accepted domain\>*。例如：david@contoso.com。

3.  您也可以選擇建立一個新信箱，驗證該信箱獲取新公認的網域之電子郵件地址，請執行下列操作：
    
    1.  移至 **\[收件者\]** \> **\[信箱\]**，按一下 **\[新增\]**![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")，然後選取 **\[使用者信箱\]**。
    
    2.  在新使用者頁面，提供所要求的資訊以建立新信箱。按一下 \[儲存\]。
    
    3.  選取這個新信箱，然後在收件者資料窗格中，驗證 \[使用者信箱\] 欄位已設定為 *\<alias\>*＠*\<new accepted domain\>*。例如：david@contoso.com。

## 步驟 4：設定外部 URL

您必須先對用戶端存取伺服器的虛擬目錄設定內部網域 (即 URL)，然後設定私人網域名稱服務 (DNS) 記錄，然後用戶端才可以從您的內部網路連線至新的伺服器。

您必須先對用戶端存取伺服器的虛擬目錄設定外部網域 (即 URL)，然後設定公用網域名稱服務 (DNS) 記錄，然後用戶端才可以從網際網路連線至新伺服器。下列步驟將在每個虛擬目錄之外部 URL 設定相同的外部網域。如果您想在一個或多個虛擬目錄外部 URL 設定不同的外部網域，您需要以手動方式設定外部 URL。如需詳細資訊，請參閱＜[虛擬目錄管理](virtual-directory-management-exchange-2013-help.md)＞。

1.  瀏覽至用戶端存取伺服器的 URL 以開啟 EAC。例如，https://Ex2013CAS/ECP。

2.  在 \[網域\\使用者名稱\] 和 \[密碼\] 中輸入您的使用者名稱和密碼，然後按一下 \[登入\]。

3.  前往 \[伺服器\] \>\[伺服器\]，選取外部網際網路用戶端存取伺服器，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

4.  按一下 \[Outlook Anywhere\]。

5.  在 \[指定外部主機名稱\] 欄位中，指定用戶端存取伺服器之外部可存取 FQDN。例如，mail.contoso.com。

6.  既然已經在此步驟，我們不妨也一併為用戶端存取伺服器設定可從內部存取的 FQDN。在 **\[指定內部主機名稱\]** 欄位中，插入您在上一個步驟中使用的 FQDN。例如，mail.contoso.com。

7.  按一下 \[儲存\]。

8.  移至 **\[伺服器\]** \>**\[虛擬目錄\]**，然後按一下 **\[設定外部存取網域\]**![設定圖示](images/JJ218640.a9c33f23-3d44-44e7-a5d0-8446200c746e(EXCHG.150).gif "設定圖示")。

9.  在 \[選取和外部URL一起使用之用戶端存取伺服器\]之下，按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

10. 選取你想要設定之用戶端存取伺服器，然後按一下 **\[新增\]**。在您將要設定的所有用戶端存取伺服器新增完成之後，按一下 **\[確定\]**。

11. 在 \[輸入您想和外部用戶端存取伺服器一起使用之網域名稱\] 中，輸入您想套用之外部網域名稱。例如：mail.contoso.com。按一下 \[儲存\]。
    
    <table>
    <colgroup>
    <col style="width: 100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>部分組織會將 Outlook Web App FQDN 設為唯一，以保護使用者不受基礎伺服器 FQDN 變更的影響。許多組織會使用 owa.contoso.com (而非 mail.contoso.com) 來作為其 Outlook Web App FQDN。若您要設定唯一的 Outlook Web App FQDN，請在完成先前步驟後執行下列動作。此檢查清單是假設您已經設定一個唯一的 Outlook Web App FQDN。
    <ol>
    <li><p>選取 <strong>[owa (預設的網站)]</strong>，然後按一下 <strong>[編輯]</strong><img src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="編輯圖示" alt="編輯圖示" />。</p></li>
    <li><p>在 <strong>[外部 URL]</strong> 中照順序輸入 <strong>https://</strong> 和您要使用的唯一 Outlook Web App FQDN，最後加上 <strong>/owa</strong>。例如，https://owa.contoso.com/owa。</p></li>
    <li><p>按一下 [儲存]。</p></li>
    <li><p>選取 <strong>[ecp (預設的網站)]</strong>，然後按一下 <strong>[編輯]</strong><img src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="編輯圖示" alt="編輯圖示" />。</p></li>
    <li><p>在 <strong>[外部 URL]</strong> 中照順序輸入 <strong>https://</strong> 和您在上一個步驟中指定的同一個 Outlook Web App FQDN，最後加上 <strong>/ecp</strong>。例如，https://owa.contoso.com/ecp。</p></li>
    <li><p>按一下 [儲存]。</p></li>
    </ol></td>
    </tr>
    </tbody>
    </table>


將用戶端存取伺服器虛擬目錄的外部 URL 設定完成之後，您必須為自動探索、Outlook Web App 及郵件流程設定公用 DNS 記錄。公用 DNS 記錄應指向您的網際網路對向用戶端存取伺服器的外部 IP 位址或 FQDN，並使用您在用戶端存取伺服器上設定之可從外部存取的 FQDN。 以下是建議之 DNS 記錄舉例，說明您應建立此記錄，以便啟用郵件流程及外部用戶連線。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>FQDN</th>
<th>DNS 記錄類型</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Contoso.com</p></td>
<td><p>MX</p></td>
<td><p>Mail.contoso.com</p></td>
</tr>
<tr class="even">
<td><p>Mail.contoso.com</p></td>
<td><p>A</p></td>
<td><p>172.16.10.11</p></td>
</tr>
<tr class="odd">
<td><p>Owa.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Mail.contoso.com</p></td>
</tr>
<tr class="even">
<td><p>Autodiscover.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Mail.contoso.com</p></td>
</tr>
</tbody>
</table>


## 如何才能了解此步驟是否正常運作？

若要確認您是否已成功在 Client Access Server 虛擬目錄上設定外部 URL，請執行下列動作：

1.  在EAC 中，前往 \[伺服器\] \> \[虛擬目錄\]。

2.  在\[選取伺服器\] 欄位中，選取外部網際網路用戶端存取伺服器。

3.  選取一個虛擬目錄，然後在虛擬目錄資料窗格中，驗證 \[外部URL\] 欄位是由正確之 FQDN 及下列所顯示之服務所生成。
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>虛擬目錄</th>
    <th>外部 URL 值</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>自動探索</strong></p></td>
    <td><p>沒有顯示外部 URL</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>ECP</strong></p></td>
    <td><p>https://owa.contoso.com/ecp</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>EWS</strong></p></td>
    <td><p>https://mail.contoso.com/EWS/Exchange.asmx</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Microsoft-Server-ActiveSync</strong></p></td>
    <td><p>https://mail.contoso.com/Microsoft-Server-ActiveSync</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>OAB</strong></p></td>
    <td><p>https://mail.contoso.com/OAB</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>OWA</strong></p></td>
    <td><p>https://owa.contoso.com/owa</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>PowerShell</strong></p></td>
    <td><p>http://mail.contoso.com/PowerShell</p></td>
    </tr>
    </tbody>
    </table>


若要確認您是否已成功設定公用 DNS 記錄，請執行下列動作：

1.  開啟命令提示字元並執行 `nslookup.exe`。

2.  切換至可查詢您公用 DNS 區域的 DNS 伺服器。

3.  在 `nslookup` 中，查詢您建立的每個 FQDN 的記錄。確認每個 FQDN 傳回的值均正確無誤。

4.  在 `nslookup` 中，輸入 `set type=mx`，然後查看您在步驟1新增之公認的網域。驗證返回值是否符合用戶端存取伺服器之 FQDN。

## 步驟 5：設定內部 URL

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱 *\<Service\>*主題中的「[用戶端和行動裝置權限](clients-and-mobile-devices-permissions-exchange-2013-help.md) 虛擬目錄設定」項目。

您必須先對用戶端存取伺服器的虛擬目錄設定內部網域 (即 URL)，然後設定公用網域名稱服務 (DNS) 記錄，然後用戶端才可以從網際網路連線至新伺服器。

下列程序可讓您應選擇要讓使用者在內部網路和網際網路上使用同一個 URL 還是不同的 URL 來存取 Exchange 伺服器。您應根據目前使用中或想要實作的定址配置來進行選擇。若您要實作新的定址配置，我們建議您讓內部和外部 URL 使用同一個 URL。使用同一個 URL 可讓使用者更容易存取您的 Exchange 伺服器，因為他們只要記得一組位址即可。無論您選擇哪一個，都務必要針對您設定的位址空間設定私人 DNS 區域。如需有關管理 DNS 區域的詳細資訊，請參閱＜[管理 DNS 伺服器](https://go.microsoft.com/fwlink/p/?linkid=190631)＞。

如需有關虛擬目錄的內部與外部 URL 的詳細資訊，請參閱＜[虛擬目錄管理](virtual-directory-management-exchange-2013-help.md)＞。

## 將內部和外部 URL 設為相同

1.  在用戶端存取伺服器上開啟 Exchange 管理命令介面。

2.  在命令介面中執行下列每個命令，以將每個內部 URL 設定為與虛擬目錄的外部 URL 相符。例如，Ex2013CAS。
    
        $HostName = "Ex2013CAS"

3.  在命令介面中執行下列每個命令，以將每個內部 URL 設定為與虛擬目錄的外部 URL 相符。
    
        Set-EcpVirtualDirectory "$HostName\ECP (Default Web Site)" -InternalUrl ((Get-EcpVirtualDirectory "$HostName\ECP (Default Web Site)").ExternalUrl)
        
        Set-WebServicesVirtualDirectory "$HostName\EWS (Default Web Site)" -InternalUrl ((get-WebServicesVirtualDirectory "$HostName\EWS (Default Web Site)").ExternalUrl)
        
        Set-ActiveSyncVirtualDirectory "$HostName\Microsoft-Server-ActiveSync (Default Web Site)" -InternalUrl ((Get-ActiveSyncVirtualDirectory "$HostName\Microsoft-Server-ActiveSync (Default Web Site)").ExternalUrl)
        
        Set-OabVirtualDirectory "$HostName\OAB (Default Web Site)" -InternalUrl ((Get-OabVirtualDirectory "$HostName\OAB (Default Web Site)").ExternalUrl)
        
        Set-OwaVirtualDirectory "$HostName\OWA (Default Web Site)" -InternalUrl ((Get-OwaVirtualDirectory "$HostName\OWA (Default Web Site)").ExternalUrl)
        
        Set-PowerShellVirtualDirectory "$HostName\PowerShell (Default Web Site)" -InternalUrl ((Get-PowerShellVirtualDirectory "$HostName\PowerShell (Default Web Site)").ExternalUrl)

4.  雖然我們在命令介面中，我們也要設定離線通訊錄 (OAB) 以便自動探索選取正確的虛擬目錄來發佈 OAB。若要這樣做，請執行下列命令。
    
        Get-OfflineAddressBook | Set-OfflineAddressBook -GlobalWebDistributionEnabled $True -VirtualDirectories $Null

對用戶端存取伺服器虛擬目錄設定好內部 URL 之後，您必須為 Outlook Web App 及其他連線設定私人 DNS 記錄。依您的設定而定，您將必須設定私人 DNS 記錄，使其指向用戶端存取伺服器的內部或外部 IP 位址或是完整網域名稱 (FQDN)。以下是您應該建立以便啟用內部用戶端連線能力的建議 DNS 記錄範例。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>FQDN</th>
<th>DNS 記錄類型</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mail.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Ex2013CAS.corp.contoso.com</p></td>
</tr>
<tr class="even">
<td><p>Owa.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Ex2013CAS.corp.contoso.com</p></td>
</tr>
</tbody>
</table>


## 如何才能了解此步驟是否正常運作？

若要確認您是否已成功在 Client Access Server 虛擬目錄上設定內部 URL，請執行下列動作：

1.  在EAC 中，前往 \[伺服器\] \> \[虛擬目錄\]。

2.  在\[選取伺服器\] 欄位中，選取外部網際網路用戶端存取伺服器。

3.  選取虛擬目錄，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

4.  確認 **\[內部 URL\]** 欄位已填入如下所示的正確 FQDN 與服務：
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>虛擬目錄</th>
    <th>內部 URL 值</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>自動探索</strong></p></td>
    <td><p>沒有顯示內部 URL</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>ECP</strong></p></td>
    <td><p>https://owa.contoso.com/ecp</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>EWS</strong></p></td>
    <td><p>https://mail.contoso.com/EWS/Exchange.asmx</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Microsoft-Server-ActiveSync</strong></p></td>
    <td><p>https://mail.contoso.com/Microsoft-Server-ActiveSync</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>OAB</strong></p></td>
    <td><p>https://mail.contoso.com/OAB</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>OWA</strong></p></td>
    <td><p>https://owa.contoso.com/owa</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>PowerShell</strong></p></td>
    <td><p>http://mail.contoso.com/PowerShell</p></td>
    </tr>
    </tbody>
    </table>


若要確認您是否已成功設定私人 DNS 記錄，請執行下列動作：

1.  開啟命令提示字元並執行 `nslookup.exe`。

2.  切換至可查詢您私人 DNS 區域的 DNS 伺服器。

3.  在 `nslookup` 中，查詢您建立的每個 FQDN 的記錄。確認每個 FQDN 傳回的值均正確無誤。

## 設定不同的內部和外部 URL

1.  瀏覽至用戶端存取伺服器的 URL 以開啟 EAC。例如，https://Ex2013CAS/ECP。

2.  在EAC 中，前往 \[伺服器\] \> \[虛擬目錄\]。

3.  在\[選取伺服器\] 欄位中，選取外部網際網路用戶端存取伺服器。

4.  選取要變更的虛擬目錄，然後按一下 **\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

5.  在 \[內部 URL\] 中，以您要使用的新 FQDN 來取代 **https://** 與第一個正斜線 (**/**) 之間的主機名稱。例如，若您要將 EWS 虛擬目錄 FQDN 從 Ex2013CAS.corp.contoso.com 變更為 internal.contoso.com，則將內部 URL 從 https://Ex2013CAS.corp.contoso.com/ews/exchange.asmx 變更為 https://internal.contoso.com/ews/exchange.asmx。

6.  按一下 \[儲存\]。

7.  針對您要變更的每個虛擬目錄重複步驟 5 與 6。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>ECP 和 OWA 虛擬目錄的內部 URL 必須相同。<br />
    您不能對自動探索虛擬目錄設定內部 URL。</td>
    </tr>
    </tbody>
    </table>


8.  最後，我們必須開啟命令介面並設定離線通訊錄 (OAB)，以便自動探索選取正確的虛擬目錄來發佈 OAB。若要這樣做，請執行下列命令。
    
        Get-OfflineAddressBook | Set-OfflineAddressBook -GlobalWebDistributionEnabled $True -VirtualDirectories $Null

對用戶端存取伺服器虛擬目錄設定好內部 URL 之後，您必須為 Outlook Web App 及其他連線設定私人 DNS 記錄。依您的設定而定，您將必須設定私人 DNS 記錄，使其指向用戶端存取伺服器的內部或外部 IP 位址或是 FQDN。若您已將虛擬目錄的內部 URL 設定為使用 internal.contoso.com，以下是建議您建立的 DNS 記錄範例，以便啟用內部用戶端連線能力。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>FQDN</th>
<th>DNS 記錄類型</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>internal.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Ex2013CAS.corp.contoso.com</p></td>
</tr>
</tbody>
</table>


## 如何才能了解此步驟是否正常運作？

若要確認您是否已成功在 Client Access Server 虛擬目錄上設定內部 URL，請執行下列動作：

1.  在EAC 中，前往 \[伺服器\] \> \[虛擬目錄\]。

2.  在\[選取伺服器\] 欄位中，選取外部網際網路用戶端存取伺服器。

3.  選取虛擬目錄，然後按一下 \[編輯\]![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

4.  確認 **\[內部 URL\]** 欄位已填入正確的 FQDN。例如，您可以將內部 URL 設定為使用 internal.contoso.com。
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>虛擬目錄</th>
    <th>內部 URL 值</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>自動探索</strong></p></td>
    <td><p>沒有顯示內部 URL</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>ECP</strong></p></td>
    <td><p>https://internal.contoso.com/ecp</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>EWS</strong></p></td>
    <td><p>https://internal.contoso.com/EWS/Exchange.asmx</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Microsoft-Server-ActiveSync</strong></p></td>
    <td><p>https://internal.contoso.com/Microsoft-Server-ActiveSync</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>OAB</strong></p></td>
    <td><p>https://internal.contoso.com/OAB</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>OWA</strong></p></td>
    <td><p>https://internal.contoso.com/owa</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>PowerShell</strong></p></td>
    <td><p>http://internal.contoso.com/PowerShell</p></td>
    </tr>
    </tbody>
    </table>


若要確認您是否已成功設定私人 DNS 記錄，請執行下列動作：

1.  開啟命令提示字元並執行 `nslookup.exe`。

2.  切換至可查詢您私人 DNS 區域的 DNS 伺服器。

3.  在 `nslookup` 中，查詢您建立的每個 FQDN 的記錄。確認每個 FQDN 傳回的值均正確無誤。

## 步驟 6：設定 SSL 憑證

您必須已獲指派權限，才能執行此程序或這些程序。若要查看您需要的權限，請參閱[郵件流程權限](mail-flow-permissions-exchange-2013-help.md)主題中的「憑證管理」項目。

部分服務 (例如 Outlook 無所不在 及 Exchange ActiveSync) 會要求在您的 Exchange 2013 伺服器上設定憑證。下列步驟會說明如何設定協力廠商憑證授權單位 (CA) 核發的 SSL 憑證：

1.  瀏覽至用戶端存取伺服器的 URL 以開啟 EAC。例如，https://Ex2013CAS/ECP。

2.  在 \[網域\\使用者名稱\] 和 \[密碼\] 中輸入您的使用者名稱和密碼，然後按一下 \[登入\]。

3.  前往 \[伺服器\] \>\[憑證\]。在 \[憑證\] 頁面上，確定已在 \[選取伺服器\] 欄位中選取用戶端存取伺服器，然後按一下 \[新增\]![加入圖示](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "加入圖示")。

4.  在 **\[新 Exchange 憑證\]** 精靈中，選取 **\[建立從憑證授權請求憑證\]**，然後按 **\[下一步\]**。

5.  指定此憑證的名稱，然後按 \[下一步\]。

6.  如果您想請求多子網域通用憑證，選取 **\[請求多子網域通用憑證\]**，然後在 **\[根網域\]** 欄位內，指定所有子網域之根網域。如果您不想請求多子網域通用憑證，而是要指定您想新增憑證的每個網域，本頁請保留空白不填。按 **\[下一步\]**。

7.  按一下 \[瀏覽\]，並指定一個 Exchange 伺服器來儲存憑證。您選擇的伺服器應為外部網際網路用戶端存取伺服器。按 \[下一步\]。

8.  針對所示列表中的每一項服務，驗證使用者將用來連線至 Exchange 伺服器的外部或內部伺服器名稱正確無誤。例如：
    
      - 若您將內部和外部 URL 設為相同，則 **\[Outlook Web App (從網際網路存取時)\]** 與 **\[Outlook Web App (從內部網路存取時)\]** 應會顯示 owa.contoso.com；**\[OAB (從網際網路存取時)\]** 與 **\[OAB (從內部網路存取時)\]** 應會顯示 mail.contoso.com。
    
      - 若您將內部 URL 設定為 internal.contoso.com，則 **\[Outlook Web App (從網際網路存取時)\]** 應會顯示 owa.contoso.com，而 **\[Outlook Web App (從內部網路存取時)\]** 應會顯示 internal.contoso.com。
    
    這些網域將用於建立 SSL 憑證請求。按 **\[下一步\]**。

9.  新增您想要包含在 SSL 憑證內的任何額外網域。

10. 選取您要作為憑證一般名稱的網域，然後按一下 **\[設為一般名稱\]**。例如：contoso.com。按 **\[下一步\]**。

11. 提供您的組織相關資訊。此資訊將包含在 SSL 憑證內。按 **\[下一步\]**。

12. 指定您希望儲存此項憑證請求的網路位置。按一下 **\[完成\]**。

儲存憑證請求之後，向您的憑證管理中心 (CA) 提出請求。這可能是內部憑證管理中心或第三方憑證管理中心，端視您的組織而定。連結到用戶端存取伺服器的用戶必須相信您使用之憑證管理中心。從 CA 取得憑證後，請完成下列步驟：

1.  在 EAC 的 \[伺服器\] \>\[憑證\] 頁面中，選取您在先前步驟中所建立之憑證請求。

2.  在憑證請求資料窗格中，在 **\[狀態\]** 下按一下 **\[完成\]**。

3.  在 \[完成擱置的要求\] 頁面上，指定 SSL 憑證的檔案路徑，然後按一下 \[確定\]。

4.  選取您剛新增的新憑證，然後按一下**\[編輯\]**![編輯圖示](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編輯圖示")。

5.  在憑證頁面按一下 **\[服務\]**。

6.  選取您想要指派給這項憑證之服務。您至少應選取 \[SMTP\] 及 \[IIS\]。按一下 \[儲存\]。

7.  若您收到 **\[是否覆寫現有的預設 SMTP 憑證？\]** 警告，請按一下 **\[是\]**。

## 如何才能了解此步驟是否正常運作？

若要確認您是否已成功新增新的憑證，請執行下列動作：

1.  在EAC 中，前往 \[伺服器\] \> \[憑證\]。

2.  選取新憑證，然後在憑證資料窗格中，驗證已下是否屬實：
    
      - \[狀態\]顯示為 \[有效\]
    
      - \[指派給服務\] 至少會顯示 \[IIS\] 和 \[SMTP\]。

## 如何才能了解此工作是否正常運作？

若要確認您是否已設定郵件流程和外部用戶端存取，請執行下列動作：

1.  在 Outlook、Exchange ActiveSync 裝置，或者兩者皆建立新的設定檔。驗證 Outlook 或行動裝置成功建立了新的設定檔。

2.  從 Outlook 或行動裝置傳送新訊息給一位外部收件者。驗證外部收件者接收到訊息。

3.  在外部收件者的信箱，回覆訊息到你剛才傳送訊息的 Exchange 信箱。驗證 Exchange 信箱接收到訊息。

4.  瀏覽 https://owa.contoso.com/owa，並驗證沒有憑證警示。

