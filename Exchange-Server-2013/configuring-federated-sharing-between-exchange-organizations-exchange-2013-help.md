---
title: '設定 Exchange 組織之間的同盟共用: Exchange 2013 Help'
TOCTitle: 設定 Exchange 組織之間的同盟共用
ms:assetid: 94e31454-b027-4757-b52f-d3c2ead6d916
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ657473(v=EXCHG.150)
ms:contentKeyID: 50473807
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 設定 Exchange 組織之間的同盟共用

 

_**適用版本：**Exchange Server 2013_

_**上次修改主題的時間：**2016-12-09_

有了同盟共用，內部部署 Exchange 組織中的使用者可與其他也已針對同盟共用進行設定的 Exchange 組織中的收件者共用空閒/忙碌行事曆資訊。可在兩個執行 Exchange 2013 的組織之間啟用空閒/忙碌資訊的共用功能，也可在採用混合型 Exchange 部署的組織之間啟用。若要深入了解同盟共用，請參閱[共用](sharing-exchange-2013-help.md)。

本主題提供了必要的需求和配置步驟之摘要，以協助您在下列各式常見的 Exchange 部署之間啟用空閒/忙碌資訊的共用功能：

  - 兩個 Exchange 2013 組織。

  - 一個 Exchange 2013 組織和 Exchange 2010 SP2 組織。

  - Exchange 2007 組織（或混合式 Exchange 2007 與 Exchange 2010 SP2 組織）以及 Exchange 2013 組織。

  - Exchange 2003 組織（或混合式 Exchange 2003 與 Exchange 2010 SP2 組織）以及 Exchange 2013 組織。

若欲瞭解更多與同盟共用相關的管理工作，請參閱 [同盟程序](federation-procedures-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要事項" alt="重要事項" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>此 Exchange Server 2013 功能與中國的 21Vianet 所運作的 Office 365 不完全相容，部分功能可能受限。如需詳細資訊，請參閱<a href="https://go.microsoft.com/fwlink/?linkid=313640">了解 21Vianet 運作的 Office 365</a>。</td>
</tr>
</tbody>
</table>


## 開始之前有哪些須知？

  - 每項程序的預估完成時間：2 小時。

  - 本主題中的程序需要特定權限。請查看每個程序以取得權限資訊。

  - 在您執行本主題中的程序前，請確認您了解整個 Exchange 組織中與共用空閒/忙碌資訊相關聯的限制。如需詳細資訊，請參閱[Limitations of free/busy sharing](sharing-exchange-2013-help.md)。

  - 如需適用於此主題中程序的快速鍵相關資訊，請參閱 [Exchange 系統管理中心的鍵盤快速鍵](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

## 您要執行的工作

## 設定 Exchange 2013 組織之間的空閒/忙碌共用

為兩個組織完成[設定同盟共用](configure-federated-sharing-exchange-2013-help.md)中的步驟。

## 設定 Exchange 2013 和 Exchange 2010 SP2 之間的空間/忙碌共用

  - 為Exchange 2013組織設定同盟共用。完成[設定同盟共用](configure-federated-sharing-exchange-2013-help.md)中的步驟。

  - 設定 Exchange 2010 SP2 組織的同盟的委派 （同盟共用的舊名稱）。完成步驟中[設定同盟委派](https://go.microsoft.com/fwlink/p/?linkid=268410)。

## 設定 Exchange 2013 和 Exchange 2007 組織之間的空閒/同盟共用

  - 為Exchange 2013組織設定同盟共用。完成[設定同盟共用](configure-federated-sharing-exchange-2013-help.md)中的步驟。

  - 完成 Exchange 2007 組織中的下列步驟：
    
    1.  **新增一個 Exchange 2010 SP2 伺服器**
        
        用戶端存取伺服器角色的 Exchange 2010 SP2 伺服器必須安裝 Exchange 2007 組織中。如果您有現有的 Exchange 2010 伺服器、 他們應該也更新至 Exchange 2010 SP2。如需 Exchange 2007 組織中安裝 Exchange 2010 的詳細資訊，請參閱[Exchange 2007-規劃升級及共存的藍圖](https://go.microsoft.com/fwlink/p/?linkid=268411)。
    
    2.  **設定同盟委派**
        
        設定 Exchange 2007 組織的同盟的委派。在 Exchange 2007 組織中的 Exchange 2010 SP2 伺服器、 完成步驟中[設定同盟委派](https://go.microsoft.com/fwlink/p/?linkid=268410)。
    
    3.  **設定 Active Directory 同步處理**
        
        Active Directory 同步處理必須為所有必須在組織間共用空閒/忙碌資訊的使用者設定同步處理功能。您可手動設定 Active Directory 同步處理功能，或使用自動化的 Active Directory 同步處理服務。若要設定 Active Directory 同步處理，請參見下面的步驟：
        
          - **必要條件**   請確定您的組織符合安裝 Active Directory 同步處理的要求。
            
            深入了解，請參閱 ＜[準備 Active Directory 同步作業](https://go.microsoft.com/fwlink/p/?linkid=247302)
        
          - **規劃**   瞭解 Microsoft Online Services Directory Synchronization 工具與安裝藍圖。
            
            若要深入了解，請參閱 [Active Directory 同步處理：藍圖](http://go.microsoft.com/fwlink/p/?linkid=203007)
        
          - **安裝與設定**   設定您內部部署組織與 Office 365 用戶服務組織之間的 Active Directory 同步處理。
            
            如需了解，請參閱[安裝與升級 Microsoft Online Services 目錄同步作業工具](https://go.microsoft.com/fwlink/p/?linkid=247303)
    
    4.  **建立可用性位址空間**
        
        建立一個將可用性要求從 Exchange 2007 信箱使用者導向 Exchange 2007 組織中 Exchange 2010 SP2 用戶端伺服器之遠端 Exchange 2013 組織的可用位址空間。此設定能讓遠端 Exchange 2013 組織的使用者，透過 Exchange 2007 組織中的 Exchange 2010 用戶端存取伺服器來代理 Exchange 2007 使用者的使用者可用性要求。Exchange 2007 中的 Exchange 2010 用戶端存取伺服器會利用同盟信任及組織關係，將可用性要求傳送至遠端 Exchange 2013 組織樹系可用性端點。
        
        若要設定可用性位址空間，請在 Exchange 2007 組織中之 Exchange 2010 用戶端存取伺服器的 Exchange 管理命令介面執行以下命令：
        
            Add-AvailabilityAddressSpace -AccessMethod InternalProxy -ProxyUrl https://<Exchange 2010 CAS server name>/ews/exchange.asmx -ForestName <SMTP domain of the remote Exchange organization> -UseServiceAccount $True
        
        如需詳細的語法及參數資訊，查看[Add-availabilityaddressspace](https://go.microsoft.com/fwlink/p/?linkid=268413)

## 在 Exchange 2013 和 Exchange 2003 組織之間設定空閒/忙碌共用

  - 為Exchange 2013組織設定同盟共用。完成[設定同盟共用](configure-federated-sharing-exchange-2013-help.md)中的步驟。

  - 完成 Exchange 2003 組織中的下列步驟：
    
    1.  **新增 Exchange 2010 SP2 伺服器**。
        
        用戶端存取伺服器角色的 Exchange 2010 SP2 伺服器必須安裝在 Exchange 2003 組織中。如果您有現有的 Exchange 2010 伺服器時，他們應該也更新至 Exchange 2010 SP2。如需 Exchange 2003 組織中安裝 Exchange 2010 的詳細資訊，請參閱[Exchange 2003-規劃升級及共存的藍圖](https://go.microsoft.com/fwlink/?linkid=268414)。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb125224.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>如需如何讓 Exchange 2013 和 Exchange 2003 組織之間的空閒/忙碌共用運作正常的相關資訊，公用資料夾階層中必須存在 <strong>OU=EXTERNAL (FYDIBOHF25SPDLT)</strong> 公用資料夾。在 Exchange 2010 設定過程中，只有在您配置 Outlook 2003 支援用戶端設定的同時選取建立公用資料夾的選項，才會自動在 Exchange 2003 組織內的 Exchange 2010 Mailbox 伺服器上建立此資料夾。此外，Exchange 2010 信箱伺服器必須是組織中第一個安裝的信箱伺服器，此選項才會在安裝過程中出現。若未在安裝過程中建立 <strong>OU=EXTERNAL (FYDIBOHF25SPDLT)</strong> 公用資料夾，您將必須手動建立此資料夾。如需有關如何建立此公用資料夾的詳細資料，請參閱 <a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=2555008">在 Microsoft Office 365 企業環境中，使用 Exchange 聯盟時，如何疑難排解閒置/忙碌的問題</a>。</td>
        </tr>
        </tbody>
        </table>
    
    2.  **設定同盟委派**。
        
        設定 Exchange 2003 組織的同盟的委派。在 Exchange 2003 組織中的 Exchange 2010 SP2 伺服器，填妥中[設定同盟委派](https://go.microsoft.com/fwlink/p/?linkid=268410)步驟。
    
    3.  **設定 Active Directory 同步處理**。
        
        必須設定需要共用空閒/忙碌資訊的組織之間的所有使用者的 active Directory 同步處理。您可以手動設定 Active Directory 同步處理或使用自動化的 Active Directory 同步處理服務。若要深入了解 Active Directory 同步處理，請參閱 ＜ [Forefront Identity Management](https://go.microsoft.com/fwlink/?linkid=294645)。
        
          - **必要條件**   請確定您的組織符合安裝 Active Directory 同步處理的要求。
            
            若要深入了解，請參閱[準備 Active Directory 同步處理](https://go.microsoft.com/fwlink/p/?linkid=247302)
        
          - **規劃**   瞭解 Microsoft Online Services Directory Synchronization 工具與安裝藍圖。
            
            若要深入了解，請參閱 [Active Directory 同步處理：藍圖](http://go.microsoft.com/fwlink/p/?linkid=203007)
        
          - **安裝與設定**   設定您內部部署組織與 Office 365 用戶服務組織之間的 Active Directory 同步處理。
            
            如需了解，請參閱安裝與升級 Microsoft Online Services 目錄同步作業工具的[](https://go.microsoft.com/fwlink/p/?linkid=247303)
    
    4.  **設定 Exchange 2003 組織中公用資料夾的空閒/忙碌共用。**
        
        在 Exchange 2003 伺服器上完成下列步驟：
        
          - 在 Exchange 系統管理員的主控台樹狀目錄中，瀏覽至 \[系統管理群組\] \> \[預設系統管理群組\] \> \[伺服器\]。
        
          - 選取您的 Exchange 2003 伺服器，然後瀏覽至 \[預設儲存群組\] \> \[公用資料夾儲存區\] \> \[公用資料夾\] \> \[排程+ 空閒忙碌\]。
        
          - 在執行窗格中，為 \[預設系統管理群組\] 選取 **OU=EXTERNAL (FYDIBOHF25SPDLT)** 資料夾。
        
          - 在 **OU=EXTERNAL (FYDIBOHF25SPDLT)** 資料夾上按一下滑鼠右鍵，然後按一下 \[內容\]。
        
          - 在 \[OU=EXTERNAL (FYDIBOHF25SPDLT) 內容\] 中，選取 \[複寫\] 索引標籤。
        
          - 若要將 **OU=EXTERNAL (FYDIBOHF25SPDLT)** 資料夾複寫至 Exchange 2010 用戶端存取/信箱伺服器，請按一下 \[新增\]。
        
          - 在 \[選取公用資料夾儲存區\] 中，選取 Exchange 2010 用戶端存取/信箱伺服器的 \[公用資料夾資料庫\]，然後按一下 \[確定\]。
            
            <table>
            <thead>
            <tr class="header">
            <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意事項" alt="注意事項" />注意事項：</th>
            </tr>
            </thead>
            <tbody>
            <tr class="odd">
            <td>依預設，Exchange 會使用公用資料夾資料庫上設定的複寫排程。</td>
            </tr>
            </tbody>
            </table>
        
          - 按一下 \[確定\] 以關閉 \[OU=EXTERNAL (FYDIBOHF25SPDLT) 內容\] 並儲存變更。
        
          - 針對 **OU=Exchange Administrative Group (FYDIBOHF23SPDLT)** 資料夾，完成上述相同步驟。
            
            <table>
            <thead>
            <tr class="header">
            <th><img src="images/Bb125224.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
            </tr>
            </thead>
            <tbody>
            <tr class="odd">
            <td>視公用資料夾的大小而定，此複寫動作可能需要數小時才能完成。</td>
            </tr>
            </tbody>
            </table>
        
          - 將 **OU=EXTERNAL (FYDIBOHF25SPDLT)** 與 **OU=Exchange Administrative Group (FYDIBOHF23SPDLT)** 公用資料夾複寫至 Exchange 2010 用戶端存取/信箱伺服器後，您必須將 Exchange 2003 伺服器上這些公用資料夾的複本移除。
    
    5.  **修改 LegacyExchangeDN 參數**
        
        修改 Exchange 2003 組織中參照遠端 Exchange 2013 組織之所有擁有郵件功能之物件的 *LegacyExchangeDN* 參數。將已啟用郵件功能的物件之現有組織單位 (OU) 值變更為 **External (FYDIBOHF25SPDLT)**，例如，**LegacyExchangeDN=/o=First Organization/ou=External (FYDIBOHF25SPDLT)/cn=Recipients/cn=User Name**。
        
        若要修改 Exchange 2003 組織中擁有郵件功能的物件，您可以使用 \[ [Active Directory 服務介面編輯器 （ADSI 編輯） 工具](https://go.microsoft.com/fwlink/?linkid=294644) \] 或 \[ [Microsoft Exchange Server LegacyDN 公用程式](http://go.microsoft.com/fwlink/?linkid=294643)。

