---
title: '設定最新附件與商務用 OneDrive 及 Exchange 2016 內部部署: Exchange 2013 Help'
TOCTitle: 設定最新附件與商務用 OneDrive 及 Exchange 2016 內部部署
ms:assetid: 799518aa-7cfe-4708-92ee-98057ff168f5
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Mt589761(v=EXCHG.150)
ms:contentKeyID: 70318164
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 設定最新附件與商務用 OneDrive 及 Exchange 2016 內部部署

 

_<strong>適用版本：</strong>Exchange Server 2016_

_<strong>上次修改主題的時間：</strong>2016-12-09_

**摘要：**如何允許您的內部部署 Exchange Server 2016 使用者在混合式組態中利用與商務用 OneDrive 與 SharePoint Online 的文件共同作業。

最近新的附件選項已可在 Office 365 中使用。在 Exchange 2016 中，此選項稱為*「文件共同作業」*，可讓內部部署使用者直接在 Web 用戶端上的 Outlook 中整合儲存在商務用 OneDrive 上的附件。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ150559.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>從 Exchange Server 2016 版本開始，Outlook Web App 現在稱為網頁型 Outlook。</td>
</tr>
</tbody>
</table>


傳統上，使用者會藉由將檔案附加至訊息，將檔案傳送給其他人。然後，一或多個收件者會在各自的檔案複本中進行變更，最終在某個時間點將所有變更合併。此外，這些附加的檔案會佔用每位使用者信箱中的儲存空間。使用文件共同作業，使用者不用插入儲存在商務用 OneDrive 帳戶中檔案的連結，而是允許多人在相同的來源位置編輯檔案，不需要額外儲存空間。

為文件共同作業適當設定 Exchange 2016 環境之前，網頁型 Outlook 使用者的預設附件對話方塊如下所示：

![傳統附件對話方塊](images/Mt589761.f8c74d70-42f9-48c6-b263-ce6cef8591a8(EXCHG.150).png "傳統附件對話方塊")

使用以下指示設定您的環境之後，網頁型 Outlook 附件對話方塊如下所示：

![已啟用現代附件的附件對話方塊](images/Mt589761.89eeae65-ce3a-4c47-b57e-db734a1de95b(EXCHG.150).png "已啟用現代附件的附件對話方塊")

您的組織中具有內部部署信箱的使用者，以及在 Office 365 中具有商務用 OneDrive 帳戶的使用者，可以使用最新的附件方法，讓他們與多位收件者共用儲存在商務用 OneDrive 中的文件。收件者的位置 (線上與內部部署) 不重要。

若要深入了解混合部署，請參閱[Exchange Server 混合部署](exchange-server-hybrid-deployments-exchange-2013-help.md)。

## 開始之前有哪些須知？

  - 預估完成時間：15 分鐘

  - 請檢閱[Exchange Server 混合部署](exchange-server-hybrid-deployments-exchange-2013-help.md)，確認您了解設定混合部署將影響的範圍。

  - 請檢閱並完成[混合部署必要條件](hybrid-deployment-prerequisites-exchange-2013-help.md)中所述的所有混合部署需求。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](https://technet.microsoft.com/zh-tw/library/jj150484\(v=exchg.150\))。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ906432.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有問題嗎？在 Exchange 論壇中尋求協助。 論壇的網址為：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 設定 Exchange 2016 以在混合式環境中啟用文件共同作業

請確認下列的必要條件步驟都完成後，然後使用後續的程序以啟用文件共同作業。

**必要條件**

  - 使用[混合組態精靈](hybrid-configuration-wizard-exchange-2013-help.md) (HCW) 設定您的 Exchange 混合式環境。

  - Exchange 2016 必須安裝在您的內部部署組織。Exchange 2016 可以與舊版的 Exchange 共存，但是文件共同作業只能用於 Exchange 2016 伺服器上的信箱。

  - 必須安裝驗證伺服器，並且同步處理所有使用者。您可以使用 [Get-AuthServer](https://technet.microsoft.com/zh-tw/library/jj218613\(v=exchg.150\)) Cmdlet 來尋找您的驗證伺服器。我們建議從 Exchange 2016 伺服器使用 HCW 進行任何必要的 OAuth 組態。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ906432.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Exchange 2016 與 Office 365 之間的 OAuth 必須正確設定。如需詳細資訊，請參閱<a href="https://technet.microsoft.com/zh-tw/library/dn594521(v=exchg.150)">設定 Exchange 與 Exchange Online 組織之間的 OAuth 驗證</a>。</td>
    </tr>
    </tbody>
    </table>


  - 使用者必須擁有適當的授權。具有商務用 OneDrive 帳戶的使用者必須獲得 SharePoint Online 或商務用 OneDrive 的授權。您可以驗證使用者的授權，方法是在 Office 365 入口網站中選取使用者，然後選取 **\[編輯\]** 按鈕。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ150559.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如需詳細資訊，請參閱<a href="http://go.microsoft.com/fwlink/p/?linkid=627455">在 Office 365 中設定商務用 OneDrive</a>。</td>
    </tr>
    </tbody>
    </table>


請執行下列步驟：

1.  設定預設網頁型 Outlook 信箱原則，以便設定商務用 OneDrive 主機 URL。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ150559.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您可以移至 Office 365 SharePoint Online 租用戶管理以擷取商務用 OneDrive 主機 URL。例如，https://contoso-my.sharepoint.com 是在 Contoso 的 O365 租用戶的我的網站主機 URL。<br />
    雖然網頁型 Outlook 信箱原則隨附於 Exchange 2016，稱為「預設」，它不會自動套用至任何信箱，除非您讓它成為預設原則，或者直接將它指派給信箱。</td>
    </tr>
    </tbody>
    </table>
    
    請使用下列的範例為基礎，使用 Exchange 管理命令介面 來設定預設網頁型 Outlook 信箱原則上的內部和外部 MySite URL：
    
        Set-OwaMailboxPolicy Default -InternalSPMySiteHostURL https://Contoso-my.sharepoint.com -ExternalSPMySiteHostURL https://Contoso-my.sharepoint.com

2.  接下來，將您剛才設定的原則設為預設原則，如此它就會套用到所有的信箱，或將原則指派給個別使用者。
    
    若要讓原則成為預設網頁型 Outlook 信箱原則，請在 Exchange 管理命令介面 中輸入下列命令：
    
        Set-OwaMailboxPolicy Default -IsDefault 
    
    若要將原則指派給個人信箱，請在 Exchange 管理命令介面 中輸入下列命令：
    
        Set-CASMailbox <user mailbox> -OwaMailboxPolicy Default

3.  (選擇性) 在每個 Exchange 2016 伺服器上，重新啟動 **OWAApplicationPool**，這樣能讓組態立即運作。如果您未執行這項命令，則需要幾分鐘讓您的 Exchange 2016 伺服器套用更新的信箱原則。在 Exchange 管理命令介面 中，執行︰
    
        Restart-WebAppPool MSExchangeOWAAppPool

一旦設定，網頁型 Outlook 使用者可以選擇他們要套用至其訊息的附件類型：傳統或現代。

![附件選項對話方塊、與 OneDrive 共用或以附件傳送](images/Mt589761.7d2f27c2-3638-479a-a577-029ac61e7d95(EXCHG.150).png "附件選項對話方塊、與 OneDrive 共用或以附件傳送")

