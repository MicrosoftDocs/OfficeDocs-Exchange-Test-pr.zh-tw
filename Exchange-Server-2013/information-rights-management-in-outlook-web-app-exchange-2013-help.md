---
title: 'Outlook Web App 中的資訊版權管理: Exchange 2013 Help'
TOCTitle: Outlook Web App 中的資訊版權管理
ms:assetid: 60a49dab-17ac-4d2c-9b41-7d87250d6c00
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dd876891(v=EXCHG.150)
ms:contentKeyID: 50473323
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook Web App 中的資訊版權管理

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

資訊工作者逐漸使用電子郵件交換敏感資訊。為了安全這項資訊、 組織可以使用資訊版權管理 (IRM) 套用至訊息內容的持續性的保護。在 Microsoft Exchange Server 2010、 之前有效地利用 IRM 保護限於Outlook用戶端。在Exchange Server 2007、 Microsoft Outlook Web Access使用者才能下載版權管理增益集的 Microsoft Internet Explorer ，讓他們可以存取受 IRM 保護的內容。

在 Exchange 2013 中，Outlook Web App 中的 IRM 可讓您的使用者存取 Exchange 所提供的豐富 IRM 功能，對通訊內容進行持續 IRM 保護。

Outlook Web App 中提供了下列 IRM 功能：

  - **傳送 IRM 保護的郵件**  如下圖所示、 Outlook Web App使用者可以使用的權限\] 下拉式清單並選取要套用至郵件的權限原則範本。這可讓使用者可以傳送受 IRM 保護之郵件的內Outlook Web App。郵件是 IRM 保護之用戶端存取伺服器。
    
    ![從 OWA 傳送受 IRM 保護的郵件](images/Dd876891.fa8cabb5-c049-46dc-8b29-9d9957dbfd3e(EXCHG.150).gif "從 OWA 傳送受 IRM 保護的郵件")  

  - **受 IRM 保護的附件**  當使用者傳送受 IRM 保護之訊息從Outlook Web App時、 附加至郵件任何檔案也會收到相同的 IRM 保護及保護郵件中使用相同的權限原則範本。在Exchange 2013，IRM 保護套用至 Microsoft OfficeWord、 Excel，及PowerPoint，以及.xps 檔案和電子郵件訊息相關聯的檔案。只有當它已經不受 IRM 保護之 IRM 保護套用至附件。若要深入了解Active Directory Rights Management Services (AD RMS) 權限原則範本，請參閱[資訊版權管理](information-rights-management-exchange-2013-help.md)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Outlook Web App中的 IRM 保護只有此節中提及的支援的檔案附件。使用不受支援的檔案格式的附件未受到保護。當Outlook Web App使用者保護郵件和附加不支援類型的檔案時、 通知會顯示以通知使用者受到只支援的檔案類型。</td>
    </tr>
    </tbody>
    </table>
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>IRM 保護無法套用到已簽署或加密使用 S/MIME 郵件。若要將 IRM 保護套用、 S/MIME 簽章和加密必須是從郵件中移除。相同的受 IRM 保護的郵件，適用於使用者無法登入或使用 S/MIME 加密它們。</td>
    </tr>
    </tbody>
    </table>


  - **讀取 IRM 保護的郵件**  Outlook Web App中的 \[預覽\] 窗格中呈現寄件者使用您的組織 AD RMS 叢集受保護的郵件。沒有增益集需要安裝，和電腦不需要 AD RMS 部署中註冊。當使用者開啟訊息或檢視 \[預覽\] 窗格中時，將郵件解密使用預先授權的代理程式所新增的使用授權。解密之後, 預覽窗格中會顯示訊息。如果預先授權無法使用， Outlook Web App要求一個從 AD RMS 伺服器並再轉譯郵件。讀取受 IRM 保護之附件Outlook Web App、 時 Web 就緒文件檢視無法使用。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Outlook Web App 中的 IRM 無法阻止使用者像 Outlook 和其他 Office 應用程式一樣使用 [列印螢幕] 功能進行螢幕擷取。這對於可防止複製郵件內容的 EXTRACT 權限有很大的影響 (如果在 AD RMS 權限原則範本中指定)。</td>
    </tr>
    </tbody>
    </table>


  - **跨瀏覽器、 多個 IRM 支援的平台**  IRM 在Outlook Web App提供跨瀏覽器、 多個 IRM 支援的平台。IRM 在Outlook Web AppExchange 2013，包括 Apple Macintosh 和 Linux 作業系統所支援的所有瀏覽器支援。若要深入了解支援的瀏覽器與作業系統，請參閱[Outlook Web App 支援的瀏覽器](https://go.microsoft.com/fwlink/p/?linkid=129362)。

  - **\[WebReady 文件檢視**  在Exchange 2013，使用者可以使用 \[WebReady 文件檢視檢視支援受 IRM 保護的附件。這可讓使用者檢視而不需要下載附件使用受支援的附件相關聯的應用程式。

要尋找與管理 IRM 相關的管理工作嗎？請參閱[資訊版權管理程序](information-rights-management-procedures-exchange-2013-help.md)。

## 啟用 Outlook Web App 中的 IRM

若要在Outlook Web App啟用 IRM，您必須新增同盟信箱，由Exchange 2013安裝程式，以在 AD RMS 超級使用者群組建立系統信箱。如需詳細資訊，請參閱[至 AD RMS 超級使用者群組新增同盟信箱](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md)。這可讓Exchange 2013伺服器存取受 IRM 保護的郵件。

您也必須在Outlook Web App中啟用 IRM Exchange Management Shell 中使用[Set-IRMConfiguration](https://technet.microsoft.com/zh-tw/library/dd979792\(v=exchg.150\))指令程式。此Outlook Web AppExchange 2013組織中啟用 IRM。您可以停用或啟用 IRM Outlook Web AppOutlook Web App虛擬目錄中。您也可以在下列層級的資料粒度Outlook Web App中控制 IRM：

  - **每個 Outlook Web App 虛擬目錄**   若要在 Outlook Web App 中啟用或停用 Outlook Web App 虛擬目錄的 IRM，請使用 **Set-OWAVirtualDirectory** Cmdlet，並且將 *IRMEnabled* 參數設定為 `$false` 或 `$true` (預設)。如此一來，您就可以在 Exchange 2013 用戶端存取伺服器上停用 Outlook Web App 中一個虛擬目錄的 IRM，而在另一部用戶端存取伺服器上的另一個虛擬目錄中讓它維持啟用狀態。

  - **每個 Outlook Web App 信箱原則**   若要在 Outlook Web App 中啟用或停用 Outlook Web App 信箱原則的 IRM，請使用 **Set-OWAMailboxPolicy** Cmdlet，並且將 *IRMEnabled* 參數設定為 `$false` 或 `$true` (預設)。如此一來，您就可以指派不同的 Outlook Web App 信箱原則，在 Outlook Web App 中為一組使用者啟用 IRM，並且為另一組使用者停用 IRM。

如需詳細資訊，請參閱[啟用或停用用戶端存取伺服器上的資訊版權管理](enable-or-disable-information-rights-management-on-client-access-servers-exchange-2013-help.md)。

